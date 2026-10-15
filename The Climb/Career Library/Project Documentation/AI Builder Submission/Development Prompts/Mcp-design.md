---
kind: "project-document"
title: "Mcp-design"
collection: "AI Builder Submission"
topic: "Project Documentation"
imported: "2026-10-13"
source_files: ["AI Builder/AI Builder Submission/docs/prompts/mcp-design.md"]
tags: ["career/library"]
source_status: "source-claims-not-verified"
---

# Mcp-design

[[The Climb/Career Library/Career Library]]

# MCP Server Design — Prompt Log

> A narrative record of the design session that produced the MCP tool server layer.
> Prompt text is shown as blockquotes. Commentary between prompts explains the reasoning, what changed, and why.

---

## Session overview

The MCP server was designed in five distinct stages, each triggered by a constraint or observation from the previous round. The session started with a single broad fetch-everything tool and ended with eight focused, typed endpoints. The core tension throughout was between simplicity (fewer tools, less surface area) and precision (the agent needs to ask different questions that cannot be collapsed into one).

---

## Stage 1 — First-pass tool inventory

The session opened with a broad statement of requirements. The immediate goal was to enumerate what external signals the agent would need and translate them into a preliminary tool list.

> Build an MCP-compliant FastAPI tool server for a consumer trend intelligence agent. The server needs to fetch signals from YouTube, NewsAPI, and Google Trends. Each tool should accept a query string and return a normalised list of signals. Use Pydantic models for all request and response shapes. The server should be stateless — no caching, no session state. All API keys come from environment variables loaded via pydantic-settings.

The first draft that emerged from this prompt had three tools:

- `fetch_youtube(query, max_results)` → list of video signals
- `fetch_news(query, timeframe_days, max_results)` → list of article signals  
- `fetch_trends(query, timeframe)` → Google Trends interest-over-time data

The shared response shape was established at this stage: a `TrendSignal` model with `title`, `source`, `url`, `summary`, `sentiment_hint`, `engagement_score`, and `caveats`. The `caveats` field was deliberate from the start — the AGENTS.md brief required that every tool result be self-documenting about its reliability limitations so the LLM could incorporate them into the response without inventing hedges.

The `TrendResponse` envelope (`query_used`, `source_type`, `evidence_volume`, `signals`) was also introduced here. The `evidence_volume` dict (e.g. `{"youtube_videos": 12}`) exists so the agent has a machine-readable count of how much raw material a tool retrieved, which the system prompt uses to apply evidence-gating rules — a section requiring "≥3 distinct sources" can be checked against this field.

**What was still missing:** the three-tool design treated all YouTube use as query-based search. The trending use case — "what is viral *right now* regardless of query" — was not represented. It also had no comparison tool, no geographic demographics, and no way to differentiate breaking news from deep-search narratives.

---

## Stage 2 — Splitting YouTube into two tools

During testing of the first draft, a key insight emerged: query-based YouTube search (`/search?q=...&order=relevance`) and the YouTube trending chart (`/videos?chart=mostPopular`) are answering fundamentally different questions.

> The YouTube search endpoint returns videos that match a query by relevance. But I also want the agent to be able to ask "what is actually trending on YouTube right now in the food and health space?" — not searching for a topic, but checking what consumers are already watching without being prompted. These are different signals. The search result proves interest exists; the trending chart proves it is peaking. Split the YouTube tool into two: one for query-based search, one for the mostPopular chart. The trending tool should accept a consumer category string (e.g. "energy drinks", "functional beverages") and map it to a YouTube video category ID, since the chart endpoint filters by category rather than by keyword.

This prompt produced the `YouTubeTrendingService` class and the `_CATEGORY_YT_ID` mapping. The mapping problem was non-trivial: YouTube's category taxonomy does not match CPG category language. "Energy drinks" is not a YouTube category. The resolution was to map all food, health, beverage, and supplement strings to YouTube category ID 26 (Howto & Style), which is the closest available bucket. Sports-adjacent categories map to 17, tech to 28. The mapping is explicit rather than dynamic because YouTube's category list is stable, and the agent needs deterministic results.

Two additional details were resolved in this stage:

**The `engagement_score` gap.** The YouTube search endpoint (`/search`) does not return view counts — that requires a separate `Videos.list` call. Rather than making two API calls per search request, the `YouTubeService.search` tool sets `engagement_score=0.0` and notes this in `caveats`. The trending tool, however, calls `Videos.list?chart=mostPopular&part=snippet,statistics`, which returns `statistics.viewCount` directly. So the trending tool *does* populate `engagement_score`, set to raw view count. The caveat on the trending signal notes the chart source and the resolved category ID so the LLM can cite correctly.

**GET vs POST.** The trending endpoint became a `GET /tools/get_youtube_trending_now?category=&max_results=` rather than a POST, because it has no body — the parameters are small, scalar, and read-only. All body-bearing tools remained POST.

---

## Stage 3 — Adding `compare_topics` and the timeline tool

With two YouTube tools and two NewsAPI tools, the next gap was analytical: the agent had no way to directly compare two entities. A marketer asking "how does Celsius compare to PRIME?" needed the LLM to call two separate search queries, receive two result sets, and reason about relative volumes in its head — an unreliable chain that could produce different orderings on different runs.

> Add a compare_topics tool. It should accept two topic strings and a timeframe, query both against the combined YouTube + NewsAPI sources, count the signal volumes for each, identify any titles that appear in both result sets (shared signals), and return a typed TopicComparisonResponse with topic_a, topic_b, volume_a, volume_b, a winner field, and the shared_signals list. This is a read tool — it calls the existing services internally rather than making new API calls.

The `TopicComparisonService` was implemented as a composition: it instantiates `YouTubeService` and `NewsAPIService` internally and calls them for each topic. The `winner` field is `topic_a`, `topic_b`, or `"tie"`. The `shared_signals` list is a simple title intersection — items whose titles appear (case-insensitively) in both result sets.

This mattered for the prompt system. The competitive intent prompt was later given an explicit rule: if `compare_topics` was called, the very first sentence of the Executive Read section must state the volume numbers directly — `"Monster generated 18 signals vs Alani Nu's 11 over the past 30 days."` Without a tool that returns a `winner` field and explicit volume counts, that rule would have no data to cite.

The timeline tool followed from the same observation that a single data point is less useful than a trend:

> Add a get_trend_timeline tool that shows how signal volume for a query has changed over time. It should accept a query and a timeframe string ('Last 24 hours', 'Last 7 days', 'Last 30 days', 'Last 90 days'). The implementation should divide the timeframe into 2-3 buckets and query YouTube + News for each bucket, returning a TimelineResponse with a list of TimelinePoint objects (date, signal_volume). The date can be approximate — use the end date of each bucket.

The `_TIMEFRAME_BUCKETS` dict maps each timeframe string to a list of `days` values representing the bucket endpoints (`[7, 14, 30]` for "Last 30 days"). For each bucket, `YouTubeService` and `NewsAPIService` are called with the bucket's `timeframe_days`. This is a best-effort approximation — NewsAPI supports date-range filtering via `from=`, but YouTube search does not, so the YouTube counts are the same across all buckets. The `TimelineResponse` caveats document this limitation.

---

## Stage 4 — Adding geographic demographics

After the timeline and comparison tools were complete, the market-size intent was still underserved. A marketer asking "what is the market in Texas?" needed more than news and YouTube volumes — they needed the structural facts about who lives there.

> Add a get_market_demographics tool. It should call the US Census Bureau ACS 1-Year Estimates API (https://api.census.gov/data/2022/acs/acs1) to fetch population, median household income, and median age for a given US state. The API requires no key. Map the state name to a FIPS code (keep the mapping in the service). Return a DemographicsResponse with state, population, median_income, median_age, and caveats. Guard against the Census sentinel value -666666666 (which means missing data) by returning 0.0 for any field that returns a negative value.

The FIPS mapping covers all 50 states and DC. The sentinel value guard — `if v >= 0 else 0.0` in `_safe_float()` — was a direct result of the Census API returning `-666666666` for suppressed or unavailable fields. Without this guard the LLM would receive a large negative number and likely include it verbatim in the Market Stats section.

The decision to use the Census API rather than injecting demographic figures into the system prompt was deliberate (see ADR-004 in DECISIONS.md). The key practical constraint was citation: tool results have a URL that appears in Source Notes; prompt text does not. Demographic data needs to be citable.

This stage also introduced the `DemographicsResponse` model — a separate response type rather than a `TrendResponse` — because demographics are a structured fact, not a ranked list of signals. Forcing it into `TrendResponse` shape would have required inventing fake `TrendSignal` objects with no title, no URL, and no engagement score.

---

## Stage 5 — Adding `get_news_top_headlines`

The original `search_news_narratives` tool calls the NewsAPI `/v2/everything` endpoint, which searches the full article archive by relevance. This is the right tool for "find all articles about adaptogens in the last 7 days". But it is the wrong tool for "what are the top stories dominating news in Texas today?" — that question is about editorial priority and breaking news, not about a topic's archival presence.

> Add a get_news_top_headlines tool using the NewsAPI /top-headlines endpoint instead of /everything. It should accept a topic string, a geography string, and max_results. The /top-headlines endpoint only supports filtering by country code, not by US state — so build a _GEO_TO_COUNTRY mapping that resolves geography strings to ISO country codes. US states should all resolve to "us" with a caveat noting the state-level filter is not supported. "Global", "EU", and "Southeast Asia" should resolve to empty string, meaning no country filter is applied. Return a TrendResponse with source_type="news_headlines". Add a caveat to every signal noting that top-headlines content reflects editorial selection, not trend volume.

This produced `NewsHeadlinesService.get_top_headlines()` and the `_GEO_TO_COUNTRY` dict. The distinction between `search_news_narratives` (deep archive search, relevance-ranked, query-driven) and `get_news_top_headlines` (today's breaking stories, editorial selection, geography-filtered) was then reflected in the intent routing: `get_news_top_headlines` is offered to competitive and market intents (where "what is the market saying today?" is relevant) but not to sentiment or campaign intents (where historical volume and discussion depth matter more than today's headlines).

---

## Final tool inventory

After the five stages, the tool set was:

| Tool | Endpoint | HTTP method | Service class |
|---|---|---|---|
| `search_trend_signals` | `/tools/search_trend_signals` | POST | `YouTubeService` + `NewsAPIService` (combined) |
| `search_youtube_discussions` | `/tools/search_youtube_discussions` | POST | `YouTubeService` |
| `search_news_narratives` | `/tools/search_news_narratives` | POST | `NewsAPIService` |
| `get_trend_timeline` | `/tools/get_trend_timeline` | GET | `TrendTimelineService` |
| `compare_topics` | `/tools/compare_topics` | POST | `TopicComparisonService` |
| `get_market_demographics` | `/tools/get_market_demographics` | POST | `MarketDemographicsService` |
| `get_youtube_trending_now` | `/tools/get_youtube_trending_now` | GET | `YouTubeTrendingService` |
| `get_news_top_headlines` | `/tools/get_news_top_headlines` | POST | `NewsHeadlinesService` |

The `search_trend_signals` tool (which internally calls both `YouTubeService` and `NewsAPIService` and merges the results) was preserved as a convenience tool for the full-brief and sentiment intents. It means the agent can get cross-source coverage in a single tool call — useful when the intent is broad and the 5-call budget is tight.

---

## Design principles that emerged

**One question type, one tool.** Each tool corresponds to a question a marketer might ask. If two questions require different API endpoints, different request parameters, or produce different response shapes, they are different tools. This was the driving logic behind every split (YouTube search vs trending, news archive vs headlines).

**Caveats are first-class.** Every service class embeds known limitations directly into the `caveats` field of the signals it returns. This is more reliable than hoping the LLM hedges correctly from training data. Caveats include: engagement score unavailability on the YouTube search endpoint; editorial selection bias on top-headlines; Census ACS data currency; YouTube's approximate category matching.

**Graceful degradation over hard failure.** Every service method catches `httpx.HTTPStatusError` and `httpx.RequestError` and returns an empty result set with a warning log rather than raising. The agent backend treats an empty result set as "no evidence for this tool" and adjusts the output accordingly, rather than crashing the entire request.

**No tool is aware of any other tool.** Services are instantiated as singletons in `mcp_server/main.py` and are never imported by each other, except in the composition patterns (`TrendTimelineService` and `TopicComparisonService` compose `YouTubeService` and `NewsAPIService` directly rather than calling their own HTTP endpoints). This keeps the dependency graph a DAG and makes individual services testable in isolation.


## Source provenance

- [Original MD](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/AI%20Builder/AI%20Builder%20Submission/docs/prompts/mcp-design.md) · AI Builder/AI Builder Submission/docs/prompts/mcp-design.md

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
