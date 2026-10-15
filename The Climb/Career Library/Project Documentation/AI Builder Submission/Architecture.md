---
kind: "project-document"
title: "Architecture"
collection: "AI Builder Submission"
topic: "Project Documentation"
imported: "2026-10-13"
source_files: ["AI Builder/AI Builder Submission/docs/architecture.md"]
tags: ["career/library"]
source_status: "source-claims-not-verified"
---

# Architecture

[[The Climb/Career Library/Career Library]]

# Architecture

> How the Consumer Trend Intelligence Agent is structured, why the layers exist, and how a single user question becomes a structured intelligence brief.

---

## The Three-Layer Model

The application is split into three services with hard boundaries between them.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                              User's browser                                 │
│                                                                             │
│   [ Question input ]   [ Geography / Timeframe ]   [ Quick-start chips ]   │
└──────────────────────────────────┬──────────────────────────────────────────┘
                                   │  POST /chat  (JSON)
                                   ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                         Agent Backend  :8000                                │
│                                                                             │
│  1. Classify intent (sentiment / competitive / market / campaign / brief)   │
│  2. Extract product category from question text                             │
│  3. Select tools and sections for the detected intent                       │
│  4. Build system prompt with evidence-gating rules                          │
│  5. Run LangChain tool-calling agent (≤5 tool calls)                        │
│  6. Collect intermediate steps → tool trace + source links                  │
│  7. Return ChatResponse (brief + sources + caveats + trace)                 │
└──────────────────────────────────┬──────────────────────────────────────────┘
                                   │  HTTP JSON-RPC  (one call per tool)
                                   ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                         MCP Tool Server  :8001                              │
│                                                                             │
│   /tools/search_trend_signals        /tools/get_trend_timeline              │
│   /tools/search_youtube_discussions  /tools/compare_topics                  │
│   /tools/search_news_narratives      /tools/get_market_demographics         │
│   /tools/get_youtube_trending_now    /tools/get_news_top_headlines           │
│                                                                             │
│        ↓ YouTube Data API v3     ↓ NewsAPI     ↓ US Census ACS              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Layer 1 — MCP Tool Server

### What it does

The MCP server is the only part of the system that talks to the outside world. It exposes eight stateless HTTP endpoints, each wrapping one external data source or one analytical operation (e.g. topic comparison). Every endpoint accepts a structured JSON request and returns a `TrendResponse` — a normalised envelope of `TrendSignal` objects plus metadata — or a typed structured response for timeline, comparison, and demographic tools.

The server is stateless: it holds no session state, no cache, and no knowledge of the agent or the user's question. Each incoming request is handled in full isolation.

### What it deliberately does NOT do

- **No business logic.** The server does not decide which tools to call, which signals matter, or how to interpret the results. It fetches and normalises; the agent backend reasons.
- **No prompt assembly.** It has no concept of an LLM, a chat history, or a response format.
- **No session or user state.** Every call is stateless; the server cannot be told "what did you return last time".

### Why this boundary exists

External API keys (YouTube, NewsAPI) live only in the MCP server's environment. If the agent backend called these APIs directly, every change to an external integration would require touching the orchestration layer. Keeping I/O isolated means you can swap, mock, or rate-limit any data source without touching the agent logic. It also makes unit testing trivial: the agent backend can be tested with a mock MCP server that returns fixture JSON, while the MCP server can be tested with mocked `httpx` responses.

---

## Layer 2 — Agent Backend

### What it does

The agent backend is the orchestration layer. It receives a user question from the frontend, classifies it into one of five **intents** (see Intent Classification below), extracts the product category from the question text, selects the appropriate subset of tools and report sections for that intent, builds a system prompt with evidence-gating rules, and hands everything to a LangChain `create_tool_calling_agent` executor.

The executor runs the LLM in a tool-calling loop (maximum five iterations). Each iteration the LLM decides which MCP tool to call next, the backend dispatches the call via `MCPClient`, and the result is appended to the agent's context. After the loop the backend collects every intermediate step, extracts source URLs from the signals, and returns a `ChatResponse` Pydantic model.

The backend also owns the **fallback path**: if no LLM key is configured, it calls the MCP tools directly, bypasses the LLM entirely, and returns the raw signals as a plain-text summary.

### What it deliberately does NOT do

- **No external API calls.** All data fetching goes through `MCPClient` → MCP server. The backend never imports `httpx` to call YouTube or NewsAPI directly.
- **No presentation logic.** It returns structured JSON; it has no knowledge of how the frontend renders sections or source cards.
- **No persistent storage.** Session state is held in memory for the duration of a single request. There is no database, no cache layer, and no cross-session memory.

### Why this boundary exists

Separating orchestration from I/O means the agent can be developed and tested against a mock MCP server that returns deterministic fixture data. The LLM prompt, tool selection logic, and output schemas can all change without touching any API integration code. It also enforces the security principle that the LLM — which is inherently unpredictable — can only affect the outside world via the narrow, validated interface of the MCP tool endpoints, not by making arbitrary HTTP calls.

---

## Layer 3 — Frontend

### What it does

The frontend is a single HTML page (`frontend/index.html`) with a plain JavaScript event handler (`frontend/app.js`). It collects a question, geography, and timeframe from the user, posts them to `POST /chat` on the agent backend, and renders the response. It parses the `brief` field as Markdown, displays `sources` as a card grid with clickable links, lists `caveats`, shows the intent and detected category in a mode badge, and renders tool trace entries in a collapsible panel.

The frontend is served as static files by the agent backend itself (`StaticFiles` mount at `/`), so no separate web server or build step is required.

### What it deliberately does NOT do

- **No business logic.** It does not classify intent, select tools, build prompts, or parse trend signals.
- **No MCP tool calls.** The frontend never contacts the MCP server directly.
- **No state beyond the current response.** There is no client-side session store, local storage, or history.

### Why this boundary exists

A presentation layer that contains no logic can be fully replaced (e.g. with a React app, a Slack bot, or a CLI) without touching either backend service. It also means no API keys or internal service URLs ever reach the browser.

---

## MCP Tool Design

### Why 8 tools instead of 1

A single `search(query)` tool would force the LLM to pack every information need into one call and receive an undifferentiated blob of results. The agent would have no way to express "I need a time-series view" vs "I need a head-to-head comparison" vs "I need demographic composition data" — all of which require different API endpoints, different request parameters, and different response shapes.

Each of the eight tools corresponds to a **distinct question type** a marketer might ask:

| Tool | Question it answers |
|---|---|
| `search_trend_signals` | What signals exist across news + YouTube for this topic right now? |
| `search_youtube_discussions` | What are real consumers saying about this in video content? |
| `search_news_narratives` | What editorial narratives are forming around this topic? |
| `get_trend_timeline` | Is interest in this topic rising, falling, or flat over time? |
| `compare_topics` | Which of these two topics is generating more signal volume? |
| `get_market_demographics` | Who are the people in this geography, by age and income? |
| `get_youtube_trending_now` | What is viral *today*, right now, regardless of a specific query? |
| `get_news_top_headlines` | What are editors leading with in this geography today? |

Keeping tools focused means the LLM's tool-calling decisions are interpretable, the results are attributable to a specific source, and individual tools can be swapped or mocked without side effects on the others.

### How tool selection maps to intent

The backend does not expose all eight tools to the LLM for every question. `prompts.py` maintains an `_INTENT_TOOLS` mapping that narrows the tool set to the subset relevant for each intent:

| Intent | Tools made available |
|---|---|
| `sentiment` | `search_trend_signals`, `search_youtube_discussions`, `search_news_narratives`, `get_youtube_trending_now` |
| `competitive` | `compare_topics`, `search_trend_signals`, `search_news_narratives`, `get_news_top_headlines` |
| `market` | `get_market_demographics`, `search_trend_signals`, `search_news_narratives`, `get_news_top_headlines` |
| `campaign` | `search_trend_signals`, `search_youtube_discussions`, `get_trend_timeline`, `get_youtube_trending_now` |
| `full_brief` | All eight tools |

This matters for two reasons. First, it reduces the LLM's decision space so it focuses tool calls on what the user actually asked for. Second, it enforces the maximum-five-calls budget more effectively: a sentiment question does not need demographic data, so `get_market_demographics` is not offered and cannot consume one of the five slots.

### Why the Census API is a separate tool rather than baked into the prompt

The US Census Bureau American Community Survey API returns structured demographic statistics — median age, median household income, population count — for a given US state. These numbers change annually, are highly specific to geography, and cannot be reliably reproduced from LLM training data (which may be outdated or averaged across regions).

If demographic figures were injected directly into the system prompt as static text, three problems arise:

1. **Stale data.** The prompt would encode a snapshot from whenever the developer last updated it. The Census API call retrieves the current ACS release.
2. **Irrelevance.** Most questions do not need demographic data at all. Injecting it unconditionally bloats the context and can mislead the LLM into treating demographic data as relevant when it is not.
3. **No citation path.** Source links in the response are built from tool call results. Demographic data in the prompt has no URL, no `source_type`, and no way to surface as a cited source in the UI.

By making it a tool, demographic data is only fetched when the LLM (guided by intent routing) decides it is needed, the figures are always fresh, and the API URL appears in `Source Notes` as a citable evidence item.

---

## Intent Classification

`classify_intent()` in `agent_backend/intent.py` maps a user question to one of five labels using a two-stage process:

1. **Keyword patterns** — a prioritised list of regexes is checked in order (competitive → market → campaign → sentiment → full_brief). The first match wins. Market patterns include geo-qualified phrases covering all 50 US states and several international regions so that "market size in Texas" correctly routes to the market intent rather than the full brief.

2. **LLM fallback** — if no pattern matches and a Groq key is configured, a single-turn LLM call is made to classify the intent. If the LLM is unavailable, the intent defaults to `full_brief`, which is the safe over-inclusive choice.

`_extract_category()` runs independently of intent classification and scans the question for one of eight consumer product category strings (energy drinks, coffee, plant-based, dairy, snacks, supplements, personal care, functional beverages). The detected category is used to enrich tool queries via `_enrich_query()` in `tools.py`, which appends the category to the query string if it is not already present.

---

## Communication Contracts

| Boundary | Protocol | Format |
|---|---|---|
| Browser → Agent Backend | HTTP REST | `ChatRequest` / `ChatResponse` (JSON) |
| Agent Backend → MCP Server | HTTP JSON-RPC | Per-tool request models / `TrendResponse` |
| MCP Server → External APIs | HTTPS | Each API's own format, normalised on return |

All service ports are defined in `.env` and read via `pydantic-settings`. No port is hardcoded in application code.

Error responses at both service boundaries follow the same envelope:

```json
{
  "error": "validation_error | internal_server_error",
  "detail": "...",
  "source": "agent_backend | mcp_server"
}
```

The agent backend catches MCP tool failures (HTTP errors, timeouts, missing API keys) and treats them as empty result sets, so a single unavailable data source degrades the brief rather than crashing the request.


## Source provenance

- [Original MD](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/AI%20Builder/AI%20Builder%20Submission/docs/architecture.md) · AI Builder/AI Builder Submission/docs/architecture.md

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
