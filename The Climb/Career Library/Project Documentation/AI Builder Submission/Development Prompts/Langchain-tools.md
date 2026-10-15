---
kind: "project-document"
title: "Langchain-tools"
collection: "AI Builder Submission"
topic: "Project Documentation"
imported: "2026-10-13"
source_files: ["AI Builder/AI Builder Submission/docs/prompts/langchain-tools.md"]
tags: ["career/library"]
source_status: "source-claims-not-verified"
---

# Langchain-tools

[[The Climb/Career Library/Career Library]]

# Agent Backend Design — Prompt Log

> A narrative record of the design session that produced the agent backend layer.
> Prompt text is shown as blockquotes. Commentary after each prompt explains what changed and why it was needed.

---

## Session overview

The agent backend was designed in six stages. Each stage addressed a specific failure mode or gap observed in the previous round. The arc ran from: a single undifferentiated tool set → typed StructuredTool definitions → intent-aware tool routing → dynamic section prompts → competitive brief specialisation → evidence-gated output rules.

---

## Stage 1 — Basic StructuredTool wrappers

The first prompt established the structural contract between the LangChain agent and the MCP server.

> Write the LangChain tool layer for the agent backend. For each MCP endpoint there should be a StructuredTool defined using StructuredTool.from_function with a coroutine= parameter (all tools are async). Each tool needs a Pydantic input schema, a name, and a one-paragraph description written from the LLM's point of view — the description should tell the LLM when to use the tool, not just what it calls. All tools call the MCPClient class which handles HTTP. Export them as ALL_TOOLS.

This produced the initial `tools.py` with five tools: `search_trend_signals`, `search_youtube_discussions`, `search_news_narratives`, `get_trend_timeline`, and `compare_topics`. The key structural decision from this prompt was `StructuredTool.from_function(coroutine=...)` rather than inheriting from `BaseTool`. The `coroutine=` path gives full async execution without the boilerplate of overriding `_arun`; it also makes the tool's implementation a plain async function that can be unit-tested without wrapping it in a tool instance.

The description writing convention was also set here: descriptions are instructions, not labels. `"Search YouTube for consumer discussions"` vs `"YouTube search tool"`. The LLM reads tool descriptions at inference time to decide which to call; a description that says *when* to use a tool produces better call sequences than one that describes what it returns.

---

## Stage 2 — Adding category enrichment to query-bearing tools

After the first integration test, a pattern emerged: the agent would receive a question like "what are Gen Z consumers saying about adaptogens?" and call `search_youtube_discussions(query="Gen Z adaptogens")`. The query was correct but too generic — the YouTube API ranked fitness and lifestyle channels over CPG-relevant content. Adding the detected product category to the query string ("adaptogens supplements") improved result relevance significantly.

> Add a _enrich_query(query, category) helper function to tools.py. It should append the category string to the query if: (1) the category is not blank, (2) the category is not "general", and (3) the category string is not already present in the query (case-insensitive check to prevent "energy drinks energy drinks"). Add a category: str = Field(default="") parameter to the input schemas for all query-bearing tools: YouTubeInput, NewsInput, TrendSignalsInput, TrendTimelineInput, and CompareTopicsInput. Each async tool function should call _enrich_query(query, category) before passing the query to MCPClient. DemographicsInput should not get a category parameter — it takes a state name, not a query.

The deduplication guard (`if cat.lower() in query.lower()`) was the non-obvious piece. Without it, a question like "tell me about energy drinks trends" — where "energy drinks" is already the detected category — would generate the query `"energy drinks trends energy drinks"`. The guard makes enrichment a no-op when the category is already present.

`DemographicsInput` was explicitly excluded because `get_market_demographics` takes a US state name (`state: str`), not a search query. Appending "energy drinks" to "Texas" would break the Census FIPS lookup.

---

## Stage 3 — Intent classification before the executor runs

The first executor runs used a single system prompt and all tools for every question. Two problems appeared immediately:

1. A sentiment question ("what are people saying about oat milk?") would sometimes call `get_market_demographics` because demographics were in the tool list and the LLM inferred a vague relevance.
2. A competitive question ("Celsius vs Monster") would receive a full-brief prompt asking for Campaign Ideas, which the agent attempted to fill by inventing campaign suggestions unsupported by the tool results.

The fix required routing questions to a restricted tool set and section list before the executor ran.

> Write an intent classification module at agent_backend/intent.py. Define five intent labels: sentiment, competitive, market, campaign, full_brief. For each intent, define a list of output section names — for example, sentiment maps to [Executive Read, Signal-Backed Trends, Consumer Motivation, Confidence & Caveats, Source Notes]. Write a classify_intent(question, category, geography) async function that: (1) checks a prioritised list of regex patterns (competitive first, then market, campaign, sentiment, with full_brief as the catch-all), and (2) falls back to a short single-turn LLM call if no pattern matches and GROQ_API_KEY is set. The LLM fallback should use max_tokens=10 and return only the label. Also write _extract_category(text) to scan the question for one of eight CPG category strings using compiled regex patterns.

The priority order in `_PRIORITY = ["competitive", "market", "campaign", "sentiment"]` was deliberate. Competitive patterns are the most distinctive (they contain "vs", "versus", "compare") and should not be confused with market patterns. Market patterns include geographic references that could appear in any brief, so market is checked before the less specific campaign and sentiment patterns. `full_brief` is the implicit default — it is not in the pattern list because it only fires when nothing else matches.

The `_extract_category` function uses eight CPG-specific keyword lists including brand names (Red Bull, Celsius, Alani, Poppi, Olipop) as well as ingredient and format terms. Brand names were included because the most common way a marketer specifies a category is by naming a brand in it.

---

## Stage 4 — Geographic pattern extension for market intent

After the intent classifier was running, a class of market questions was mis-routing to `full_brief`: questions with a geographic qualifier but no explicit "market size" or "demographics" language. "What are the top trends in functional beverages in Texas?" contains no market-intent keywords, so it fell through to the full-brief catch-all even though it needed `get_market_demographics` and `get_news_top_headlines` rather than a full eight-tool sweep.

> The market intent pattern list needs to catch geo-qualified questions — "trends in Texas", "functional beverages in California", "energy drink market in Florida". Add a regex pattern to the market intent patterns that matches "in" followed by any of the 50 US state names, DC, and common international regions (UK, EU, Europe, Asia, Canada, Australia, "the us", "the uk"). The pattern should be case-insensitive and use word boundaries.

This produced the long alternation pattern that now appears in `_PATTERNS["market"]`:

```python
r"\bin\s+(texas|california|florida|new york|...|australia)\b"
```

All 50 states are listed individually (no abbreviations, because the regex checks the question text as typed by the user). The international regions are the most common non-US geographies a CPG marketer would name. The `\bin\s+` prefix anchors the match — it only fires when the geography appears as a destination ("trends *in* Texas"), not as a coincidental substring.

---

## Stage 5 — Dynamic prompt builder with per-intent tool recommendations

With intent classification working, the next problem was the system prompt. A single static prompt could not simultaneously be correctly scoped for a five-section sentiment brief and an eight-section full brief. The prompt needed to dynamically compose the right section instructions and tool recommendations for each intent.

> Write a prompts.py module. Define a _BASE_PROMPT string that sets the agent's role, writing style, and invariant rules (always call tools before drawing conclusions, write like an insights partner, format source links inline in prose, be careful with purchase behaviour claims). Define _SECTION_GUIDANCE as a dict mapping section heading strings to detailed writing instructions for that section. Define _INTENT_TOOLS as a dict mapping intent labels to the subset of tools recommended for that intent. Write a _build_system_prompt(intent, sections) function that composes the base prompt + a section target list + tool recommendations + per-section guidance blocks for only the sections in the list. Export a build_prompt(intent, sections) function that wraps the system prompt in a ChatPromptTemplate with agent_scratchpad and chat_history placeholders.

The `_SECTION_GUIDANCE` dict was the most important output of this prompt. Each section has specific writing rules that go well beyond "write this section". For example:

- **Executive Read** specifies: single narrative paragraph (4–6 sentences), no bullet points, must name the top 2–3 dominant sentiments from tool results, must show how they relate to each other.
- **Signal-Backed Trends** specifies: exactly 5 trends, bold `###` title for each, 2–3 sentence narrative paragraph, source hyperlinks must appear *inline in prose* (not in a separate list at the bottom).
- **Audience Hypotheses** specifies: exactly four groups (Loyalists, Value Buyers, Family Shoppers, Brand Switchers), exactly two sentences per group, second sentence must name the specific signal that supports the hypothesis.
- **Campaign or Activation Ideas** is split into two labelled subsections: "Strong Adopter Plays" for segments already signalled in the data, "Unexplored Opportunities" for gaps and whitespace inferred from what the data *doesn't* show.

The `_INTENT_TOOLS` dict was initially populated with the four primary tools per intent and all eight for `full_brief`. New tools (`get_youtube_trending_now`, `get_news_top_headlines`) were added to the relevant buckets later.

The `ChatPromptTemplate` structure uses `MessagesPlaceholder(variable_name="agent_scratchpad")` for the tool-calling loop and `MessagesPlaceholder(variable_name="chat_history", optional=True)` for optional multi-turn context. The scratchpad placeholder is required by `create_tool_calling_agent` — it is where LangChain injects tool call results between reasoning steps.

---

## Stage 6 — Competitive brief specialisation rules

The first competitive brief outputs had a structural problem: the LLM would bury the head-to-head comparison result — the number that `compare_topics` returned — three paragraphs into the Executive Read. A marketer reading the brief needed to see the volume comparison in the first sentence. The generic section guidance did not enforce this.

> Add an _INTENT_EXTRA_RULES dict to prompts.py. For the competitive intent, add three specific rules that override or extend the general section guidance: (1) if compare_topics was called, the first sentence of Executive Read MUST state the signal volume numbers directly — name the winner and the exact counts. (2) In Market Stats, the brand that won compare_topics must be labelled Growing; the compare_topics signal volume figures must be cited as primary evidence. (3) After calling compare_topics, any follow-up calls to search tools must use the specific brand names from the user's question, never the category name — so "Monster vs Alani Nu" follow-ups query "Monster energy drink consumer sentiment", not "functional beverages".

Rule (3) was the most important. Before it was added, a competitive question about "Celsius vs PRIME" would result in the agent calling `compare_topics(topic_a="Celsius", topic_b="PRIME")` correctly, then calling `search_trend_signals(query="functional beverages")` for follow-up depth — producing undifferentiated category signals that could not be attributed to either brand. The rule forces the agent to use brand names in follow-up queries, which means every signal in the brief can be tied back to a specific brand and cited as evidence for that brand's trajectory.

---

## Stage 7 — Evidence-gated sections replacing the hard section list

The final structural problem: the prompt said "target the following sections", but the agent sometimes produced sections it had no evidence for — inventing brand figures for Market Stats, or writing Audience Hypotheses from training data when no persona signals had been collected.

> Change the section instructions in _build_system_prompt from a strict "produce ONLY these sections" rule to an evidence-gating rule. For each section type, define a minimum evidence threshold: Signal-Backed Trends requires signals from at least 3 distinct sources. Market Stats requires brand-level signals — named brands must appear explicitly in tool results. Audience Hypotheses requires persona or demographic data. Campaign Ideas requires both a trend signal and an audience/persona signal. Executive Read, Consumer Motivation, Confidence & Caveats, and Source Notes have no threshold and are always included. For every skipped section, the agent must add a one-sentence note in Confidence & Caveats stating which section was omitted and why.

This replaced the earlier hard constraint with the `evidence_rules` block that now appears in `_build_system_prompt`. The section list header changed from `"produce ONLY the following sections"` to `"target the following sections"` — the word "target" signals intent rather than mandate, leaving room for the evidence gate to exclude a section.

The Confidence & Caveats section is always written, which means even a brief that omits Market Stats and Audience Hypotheses gives the reader a complete account of what evidence was collected, what was missing, and why certain sections do not appear. This makes a shorter brief more honest than a padded brief.

The evidence rules are injected as a named block (`## Evidence-gating rules`) between the tool recommendations line and the per-section guidance blocks, so the LLM sees them before it reads the section-specific writing instructions.

---

## Stage 8 — AgentExecutor wiring

With the prompt builder, intent classifier, and tools complete, the final step was assembling the executor.

> Write agent_backend/agent.py. Define _build_llm() that tries Groq first (GROQ_API_KEY), then Gemini (GEMINI_API_KEY via langchain_google_genai, deferred import), then raises ValueError if both are empty. Define build_agent_executor(intent, sections) that calls _build_llm(), build_prompt(intent, sections), create_tool_calling_agent(llm, tools, prompt), and wraps it in AgentExecutor with max_iterations=settings.max_tool_calls, return_intermediate_steps=True, and handle_parsing_errors=True. Also write a run_fallback(question, category, geography, timeframe) async function that calls MCPClient directly without an LLM and returns a deterministic Markdown brief labelled as public_data_fallback — used when both LLM keys are absent.

`return_intermediate_steps=True` is load-bearing for the source-link system. Without it, the executor returns only the final `output` string. With it, `result["intermediate_steps"]` contains a list of `(AgentAction, observation)` pairs — every tool call with its exact input and the full response from the MCP server. The `main.py` handler iterates these pairs to extract `signal.url` values and build the `SourceLink` objects that populate the frontend source card grid.

`handle_parsing_errors=True` prevents a malformed tool call from crashing the executor. Instead it logs a warning and continues the loop, which is the correct behaviour for a demo where model output is not fully predictable.

The Gemini import is deferred (`from langchain_google_genai import ChatGoogleGenerativeAI` inside the `if` branch) so a deployment with only a Groq key never imports the Google genai package. This avoids a hard dependency on `langchain-google-genai` being installed in environments that will only use Groq.


## Source provenance

- [Original MD](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/AI%20Builder/AI%20Builder%20Submission/docs/prompts/langchain-tools.md) · AI Builder/AI Builder Submission/docs/prompts/langchain-tools.md

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
