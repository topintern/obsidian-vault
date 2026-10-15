---
kind: "project-document"
title: "Design Decisions"
collection: "AI Builder Submission"
topic: "Project Documentation"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["AI Builder/AI Builder Submission/DECISIONS.md"]
tags: ["career/library","career/project-docs"]
---

# Design Decisions

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# DECISIONS.md — Architecture Decision Records

> This file records significant design decisions made during the build of the Consumer Trend Intelligence Agent.
> Each entry documents what was decided, what was considered instead, why the decision was made, and what was accepted as the cost.

---

## ADR-001 — MCP server as a separate process, not a library

**Decision:** External data fetching (YouTube, NewsAPI, Google Trends, US Census) is implemented as a standalone FastAPI service (`mcp_server/`) running on its own port. The agent backend communicates with it over HTTP JSON-RPC rather than importing service classes directly.

**Alternatives considered:**
- Import `mcp_server/services.py` directly into the agent backend as a library module.
- Inline all API calls inside the LangChain tool functions in `agent_backend/tools.py`.

**Rationale:**
The separation enforces a hard contract between data fetching and orchestration. API keys for external services live only in the MCP server's environment; the agent backend never sees them. The MCP server can be mocked entirely for testing — the agent backend test suite points `MCP_SERVER_URL` at a local fixture server and never touches real APIs. The boundary also matches the architecture described in the AGENTS.md brief, which specifies that the agent backend "must never call external APIs directly — only via MCP tools". Future additions (a new data source, a rate-limiting proxy, a caching layer) can be made inside the MCP server without changing any agent logic.

**Tradeoff accepted:**
Every tool call incurs a local HTTP round-trip (typically <5 ms on localhost) that would not exist with a direct function call. This is immaterial at demo scale but would need measurement before a high-throughput production deployment. Operating two processes also adds a startup-order dependency: the MCP server must be running before the agent backend is started.

---

## ADR-002 — LangChain `create_tool_calling_agent` over raw LLM calls

**Decision:** The agent is implemented using LangChain's `create_tool_calling_agent` + `AgentExecutor` rather than writing a manual prompt-and-parse loop or using raw OpenAI/Groq function-calling APIs directly.

**Alternatives considered:**
- Call the LLM API directly, parse tool-call JSON from the response, dispatch the call, append the result to context, and loop manually.
- Use LangGraph for a full state-machine graph with explicit node transitions.
- Use a pure prompt-chaining approach (no tools, just few-shot examples and structured output parsing).

**Rationale:**
`create_tool_calling_agent` provides the tool-calling loop, intermediate step collection, and `AgentExecutor` streaming support in a single well-tested abstraction. It is LLM-provider-agnostic: switching from Groq to Gemini (or any `BaseChatModel`) requires changing only `_build_llm()`, with no changes to the executor, tool dispatch, or prompt structure. The `return_intermediate_steps=True` flag gives the backend the full tool trace for free — input, output, and tool name — which drives the source-link extraction and tool trace UI panel without additional instrumentation.

LangGraph was considered but rejected for v1. LangGraph is the right choice when the agent needs conditional branching between named nodes, human-in-the-loop interrupts, or persistent checkpointed state. This agent's loop is linear (call tools, synthesise, return) and the added complexity of defining explicit graph nodes and edges would not yet pay for itself.

**Tradeoff accepted:**
`AgentExecutor` is less transparent than a hand-rolled loop — debugging unexpected tool-call sequences requires reading LangChain internals. The abstraction also constrains how the loop can be customised (e.g. injecting logic between individual tool calls). These are acceptable constraints at v1 scale, with LangGraph identified as the migration path if more complex control flow is needed later.

---

## ADR-003 — Intent classification before the agent runs, not inside the agent's reasoning

**Decision:** The user's question is classified into one of five intent labels (`sentiment`, `competitive`, `market`, `campaign`, `full_brief`) by a dedicated `classify_intent()` function before the LangChain agent executor is invoked. The intent determines which tools and which output sections are offered to the agent.

**Alternatives considered:**
- Expose all eight tools to the agent on every call and let the LLM decide which ones to use.
- Include all possible output sections in the system prompt and let the LLM decide which to write.
- Use a single "router" LLM call to decompose the question into sub-tasks before the main agent call.

**Rationale:**
Exposing all tools unconditionally has two costs. First, it consumes the five-call budget on tools that are irrelevant to the question — a sentiment question does not need `get_market_demographics`, but a naive LLM might call it anyway because it is available. Second, larger tool sets expand the LLM's decision space and increase the chance of an unexpected call sequence. Pre-routing narrows both the tool list and the section list to exactly what the intent requires, making the agent's decisions more predictable and the output more focused.

The classification itself is fast: it is a regex match against a prioritised pattern list, completing in microseconds. An LLM fallback fires only if no pattern matches, and that fallback uses a single short prompt rather than a full agent turn.

**Tradeoff accepted:**
Intent classification adds a pre-processing step that can misfire. A question like "how is Monster doing in Texas?" sits at the intersection of competitive and market intents; the pattern priority order determines which wins. Errors propagate silently — the user receives a valid response, just scoped to the wrong intent. The mitigation is that `full_brief` is both the safe fallback and the default for ambiguous questions, so misclassification typically means a broader report rather than a missing one.

---

## ADR-004 — Evidence-gated section writing over mandatory fixed sections

**Decision:** The system prompt instructs the agent to include an output section only when it has sufficient evidence from tool results to write it meaningfully. Sections requiring specific evidence types (brand-level data for Market Stats, persona signals for Audience Hypotheses, both trend and audience signals for Campaign Ideas) are skipped if the evidence is absent, and the omission is noted in Confidence & Caveats.

**Alternatives considered:**
- Require the agent to produce every section in every response, filling gaps with general knowledge.
- Require the agent to produce exactly the sections listed, no more and no fewer, treating missing evidence as a reason to hedge rather than omit.
- Let the agent freely decide which sections to write based on its own judgment.

**Rationale:**
The core promise of the application is that every insight is grounded in data retrieved in the same session. A rule that forces the agent to produce Market Stats regardless of whether any brand-level signals were returned leads to one of two failure modes: the agent invents plausible-sounding brand figures, or the agent writes a section so hedged it conveys nothing. Both undermine trust.

Evidence gating makes the contract explicit: a section only appears when the agent can support it with named tool results. The Confidence & Caveats section, which is always written, documents what was omitted and why. This gives the user a complete picture of what the brief does and does not cover, and ensures that a shorter report with three well-evidenced sections is preferred over a longer report with two hallucinated ones.

**Tradeoff accepted:**
A response that omits sections may feel incomplete to users who expected a full brief. The Caveats section partially mitigates this, but users who do not read it may perceive the agent as less capable than one that always produces every section. Communicating the evidence-gating model clearly in the UI — which the mode badge and source card grid partially do — is an ongoing product concern.

---

## ADR-005 — Dynamic category inference from the question, replacing a user-supplied dropdown

**Decision:** The product category (e.g. "energy drinks", "plant-based") is inferred from the user's question text by `_extract_category()` in `intent.py`, rather than requiring the user to select a category from a dropdown before submitting. The inferred category is used to enrich tool queries via `_enrich_query()` in `tools.py`. The frontend category dropdown was removed.

**Alternatives considered:**
- Keep the category dropdown as a required field and pass `body.category` directly to tools.
- Keep the dropdown as optional and use it when provided, falling back to inference.
- Require the user to always specify a category; refuse to proceed without one.

**Rationale:**
The target users (brand marketers, insights analysts) phrase questions naturally: "What are consumers saying about adaptogens?" not "Category: Supplements | Query: consumer sentiment". A dropdown creates friction and a false hierarchy — the category is almost always inferable from the question itself. Removing the dropdown simplifies the UI and eliminates a class of user error (selecting "Coffee" but typing a question about energy drinks).

The inference is intentionally conservative: it matches against eight specific category strings using substring search. If no match is found, `category` is set to `"general"` and queries are not enriched — a safe no-op rather than a wrong enrichment.

The `effective_category` logic in `main.py` provides a final safety net: if detection yields `"general"`, the backend falls back to `body.category` if the API caller supplied one, and ultimately to `"Functional Beverages"` as the demo default. This means the inference path is always tried first, but programmatic callers (e.g. an integration test or a future Slack integration) can still supply a category explicitly.

**Tradeoff accepted:**
The eight-bucket category list covers only the most common CPG categories. A question about, say, "pet food trends" will produce `category="general"` and queries will not be enriched. This is a limitation of the current keyword list, not the design pattern — the list can be extended without changing any other code.

---

## ADR-006 — Gemini as the secondary LLM fallback, not a parallel option

**Decision:** The LLM selection logic in `_build_llm()` is a sequential fallback chain: Groq is tried first if `GROQ_API_KEY` is set; Gemini (`ChatGoogleGenerativeAI`) is tried second if `GEMINI_API_KEY` is set; a `ValueError` is raised only if both are absent. There is no toggle, no configuration flag, and no way to run both simultaneously.

**Alternatives considered:**
- Make LLM choice a single required config value (`LLM_PROVIDER=groq|gemini|openai`) and raise an error on any missing key.
- Implement a retry-then-failover pattern: use Groq by default, switch to Gemini only if a Groq call returns an error or rate-limit response at runtime.
- Support OpenAI as the primary LLM, with Groq and Gemini as equals behind a config flag.

**Rationale:**
The goal is a demo-ready application that works out of the box for as many developers as possible. Groq's free tier has a generous rate limit and the fastest inference latency of the available options, making it the best primary choice. Gemini's free tier (via Google AI Studio) has no credit-card requirement and covers the demo workload comfortably. OpenAI's free tier was removed from active consideration because it requires a paid account to access GPT-4o at useful throughput.

A runtime failover (switching mid-session on rate-limit errors) was considered but rejected for v1 because it adds state — the executor would need to be rebuilt mid-request with a different LLM instance. A configuration-flag approach (`LLM_PROVIDER=groq`) would require the developer to know in advance which provider they have keys for, and would raise a confusing error if they set the wrong flag. The sequential-fallback pattern requires zero configuration: set whichever key(s) you have, and the correct LLM is selected automatically.

`langchain_google_genai` is imported lazily inside `_build_llm()` rather than at module level so that the package is only required if Gemini is actually used. A deployment that only has a Groq key will never import `langchain_google_genai` and is not affected if the package is absent.

**Tradeoff accepted:**
The fallback chain is implicit: a developer who sets both keys gets Groq without realising Gemini is configured as a backup. If Groq degrades silently (e.g. slow responses rather than errors), the fallback will never trigger because the runtime error condition is "key is empty", not "request failed". A production deployment should add explicit LLM health-check monitoring rather than relying on the fallback chain to catch provider degradation.


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/AI%20Builder/AI%20Builder%20Submission/DECISIONS.md) · AI Builder/AI Builder Submission/DECISIONS.md

Project code and dependencies remain outside the vault. No source commands were executed.
