---
kind: "project-document"
title: "Architecture"
collection: "AI Builder Challenge"
topic: "Project Documentation"
imported: "2026-10-13"
source_files: ["AI Builder/AI Builder Challenge/docs/architecture.md"]
tags: ["career/library"]
source_status: "source-claims-not-verified"
---

# Architecture

[[The Climb/Career Library/Career Library]]

# Architecture

## Why This Architecture Exists

The assignment asks for a public REST API, an MCP server wrapper, an LLM agent backend, and a frontend. The architecture mirrors that request directly, but the product reason is bigger than compliance.

Marketers should not have to know which API has which parameter shape. They should ask business questions. The agent should translate those questions into tool calls. The wrapper should translate those tool calls into public-data API requests. The frontend should make the reasoning trail visible enough for a human to trust, challenge, or refine it.

## High-Level Flow

```text
User
  |
  v
Frontend insight workspace
  |
  v
Agent backend
  |
  | LangChain tool calls
  v
MCP server wrapper
  |
  | Public API requests
  v
YouTube / NewsAPI / Yelp / Product Hunt / GDELT / Census / Open Food Facts / Wikipedia
```

## Frontend

The frontend is a static web app because the take-home benefits from a low-friction setup. It still behaves like a product workspace:

- It captures the marketer's business question.
- It asks for category, geography, timeframe, and output type.
- It displays the generated brief, tool trace, sources, and caveats.

Rationale: the UI is designed around trust. The user can see not only the answer, but how the agent got there.

## Agent Backend

The agent backend owns LLM orchestration. It defines tools with marketer-friendly names and calls the MCP server on the user's behalf.

The main insight path is a phased intelligence pipeline:

1. A query-planning phase turns the user question into source-specific searches. YouTube gets review, comparison, and taste-test language; NewsAPI gets market and narrative language; Yelp gets local discovery language; Product Hunt gets launch and product-momentum language.
2. A collection phase calls the MCP wrapper and keeps records separated by source type.
3. A filtering phase removes records with weak relevance, low text volume, low engagement, or over-representation from one source type.
4. A sentiment inference phase reads each retained source as its own evidence unit and labels the consumer tension it supports.
5. A trend-analysis phase groups those source-level inferences into the final sections: executive read, signal-backed trends, consumer motivation, audience hypotheses, market stats, and campaign ideas.

Rationale: source is the basic evidence unit. A YouTube video, article, Yelp business/review record, or Product Hunt launch should be judged on its own before it influences the story.

When a Groq API key is present, the query-planning phase uses Groq through LangChain's OpenAI-compatible client:

1. The user request is rendered into a structured prompt.
2. The model creates source-specific searches for YouTube, NewsAPI, Yelp, Product Hunt, and public web context.
3. The MCP wrapper collects public evidence from those searches.
4. The deterministic filtering, source-sentiment, and trend-analysis phases build the final brief from retained evidence.

When no Groq key is present, the backend still calls the MCP server and returns a deterministic public-data brief. This is not a replacement for the LLM path; it is a demo resilience feature.

## MCP Server Wrapper

The MCP server is a public-data abstraction layer. Instead of exposing raw GDELT or Census mechanics, it exposes tools that match the user's task:

- `search_youtube_discussions`
- `search_news_narratives`
- `search_yelp_local_trends`
- `search_product_hunt_trends`
- `search_trend_signals`
- `get_trend_timeline`
- `compare_topics`
- `get_market_demographics`

Rationale: this is where the project demonstrates separation of concerns. The agent can reason in business terms, while the wrapper handles API-specific query construction, response normalization, and caveats.

YouTube is the primary consumer-language layer for creator/review culture. NewsAPI adds media narrative and freshness. Yelp adds local demand/review texture. Product Hunt adds emerging product momentum. The wrapper normalizes these sources into motivations, objections, competitor mentions, engagement summaries, sources, and caveats so the agent can write one coherent trend story while staying honest about what public data can and cannot prove.

Consumer-signal responses also carry evidence-volume counters: raw text characters collected, excerpt characters retained, and engagement units. These counters make source quality visible during demos. If a brief feels thin, the team can immediately see whether the issue is lack of source volume, lack of public text, or a source mismatch.

For CPG-style questions, the wrapper can use Open Food Facts as a secondary signal source. This keeps demos resilient when live media APIs throttle and gives the agent concrete public product records to reason from.

## Data Interpretation

The app distinguishes between three kinds of claims:

- **Public signal:** what appears in public media or web coverage.
- **Market context:** stable demographic or geographic context from official datasets.
- **Behavioral proof:** purchase, visitation, campaign, or audience membership data.

This prototype only covers the first two. The third would require proprietary data.

## Deployment Shape

A production deployment could use:

- Two containerized FastAPI services.
- Managed secrets for `GROQ_API_KEY` and public-source API credentials.
- API gateway or reverse proxy routing `/api` to the agent backend and `/mcp` to the wrapper.
- Observability for tool latency, source failures, and LLM cost.
- Optional static frontend hosting through CDN.

For a larger organization, the MCP server could become a gateway across internal insight sources: transaction data, location signals, audience segments, measurement summaries, and public context.


## Source provenance

- [Original MD](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/AI%20Builder/AI%20Builder%20Challenge/docs/architecture.md) · AI Builder/AI Builder Challenge/docs/architecture.md

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
