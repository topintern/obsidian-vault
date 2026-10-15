---
kind: "project-document"
title: "README"
collection: "AI Builder Challenge"
topic: "Project Documentation"
imported: "2026-10-13"
source_files: ["AI Builder/AI Builder Challenge/README.md"]
tags: ["career/library"]
source_status: "source-claims-not-verified"
---

# README

[[The Climb/Career Library/Career Library]]

# Consumer Signal Intelligence Agent

This is a take-home project prototype for an AI Builder role: a full-stack, agent-driven web app that turns public consumer signals into marketer-ready intelligence briefs.

The product idea is intentionally close to inMarket's world without pretending to use private inMarket data. The app asks: if a strategist could talk to public news, market context, and demographic data through an agent, how quickly could they move from "what is happening?" to "what should we test?"

## The Story

A marketer is preparing a campaign for a category such as better-for-you energy drinks, private label groceries, or convenience-store coffee. They do not need a wall of raw articles. They need the pattern: what signals are showing up, what consumer motivation might be underneath them, what audiences might matter, and what campaign angles are worth testing.

This app gives them a small intelligence workspace:

- Ask a market or category question.
- Choose a geography and timeframe.
- Let the agent call public-data tools through an MCP-style wrapper.
- Receive a concise brief with source links, caveats, and a visible tool trace.

The important production idea is that public APIs are replaceable. In a real marketing intelligence environment, the same pattern could connect to proprietary purchase, location, audience, and campaign measurement sources.

## What It Demonstrates

- A public REST API wrapped behind a dedicated MCP-style microservice.
- A LangChain agent backend with tool definitions and tool-calling flow.
- A web frontend for interacting with the agent.
- API-key separation and public-data caveats.
- A documentation layer that preserves intent, architecture, decisions, and AI prompts.

## Repository Structure

```text
.
├── agent_backend/          # FastAPI agent service, LangChain tool-calling, frontend serving
├── mcp_server/             # FastAPI public-data wrapper service
├── frontend/               # Static web app
├── tests/                  # Focused sanity tests
├── docs/
│   ├── architecture.md
│   └── prompts/            # Recorded development prompts by area
├── AGENTS.md               # AI-session context and working rules
├── PLAN.md                 # Project plan and demo narrative
├── DECISIONS.md            # Rationale behind major choices
├── requirements.txt
└── .env.example
```

## Data Sources

### YouTube Data API

Used for public video and comment discussion. YouTube gives consumer language, objections, creator framing, engagement proxies such as views/comments, and public timedtext captions where available.

Freshness: recent videos filtered by selected timeframe.

Range: public YouTube videos and comment threads available through the YouTube Data API.

Publicness: public video/comment data accessed with an API key.

Volume: strongest for categories with active creator/review culture.

### NewsAPI

Used for media narrative context. NewsAPI adds freshness, article framing, public issue narratives, and competitor/news hooks. The wrapper follows article URLs and extracts article paragraphs where publisher pages allow it.

Freshness: recent news articles by selected timeframe.

Range: public news/media coverage indexed by NewsAPI.

Publicness: public article metadata/snippets accessed with an API key.

Volume: depends on NewsAPI plan and query breadth.

### Yelp Fusion API

Used for local consumer trend context. Yelp adds business categories, ratings, review volume, and review excerpts where the API plan permits.

Freshness: local discovery and review signals; exact freshness depends on Yelp data availability.

Range: local businesses by term and geography.

Publicness: public Yelp business/review data accessed with a bearer token.

Volume: strongest for restaurants, retail, local services, and place-based consumer categories.

### Product Hunt API

Used for emerging product and maker-market momentum. Product Hunt adds launches, tags, votes, comments, and early product positioning.

Freshness: recent launches and active product listings.

Range: Product Hunt posts available through the GraphQL API.

Publicness: public launch data accessed with an API token.

Volume: strongest for software, AI, productivity, creator, and startup/product trends.

### GDELT

Used for public news and web signal discovery. GDELT is useful here because it provides a large, frequently updated public signal layer across global media. The MCP server uses it to search article signals and timeline volume.

Freshness: near real-time public web/news signal updates.

Range: long historical coverage, with richer GDELT 2.0 document data for modern analysis.

Publicness: open public API.

Volume: broad global media coverage, large enough for category and narrative scans.

### U.S. Census API

Used for stable market context such as population, income, age, and education.

Freshness: dataset-dependent, not real time.

Range: official U.S. demographic and economic datasets.

Publicness: open government API.

Volume: many official datasets across geographies.

### Open Food Facts

Used as a secondary CPG/product signal source when the user asks about food, beverage, or grocery categories, or when live GDELT calls are throttled.

Freshness: crowdsourced and product-dependent.

Range: global packaged product records.

Publicness: open public API and open product database.

Volume: millions of product records across many countries and categories.

## Setup

Create and activate a virtual environment:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

Create your local environment file:

```powershell
Copy-Item .env.example .env
```

Optional but recommended: set `GROQ_API_KEY` in `.env` to enable LLM-assisted query planning through Groq's OpenAI-compatible API. Without it, the app still runs with a deterministic query planner and produces a public-data brief.

To enable the richer public API signal stack, add any credentials you have:

```env
GROQ_API_KEY=your_groq_api_key
GROQ_MODEL=llama-3.3-70b-versatile
YOUTUBE_API_KEY=your_youtube_data_api_key
NEWS_API_KEY=your_newsapi_key
YELP_API_KEY=your_yelp_fusion_api_key
PRODUCT_HUNT_TOKEN=your_product_hunt_token
PRODUCT_HUNT_CLIENT_ID=your_product_hunt_client_id
PRODUCT_HUNT_CLIENT_SECRET=your_product_hunt_client_secret
```

Without these credentials, the app still runs, but the brief will disclose which source layers are not configured.

For Product Hunt, either use a developer token in `PRODUCT_HUNT_TOKEN`, or use client-only OAuth with `PRODUCT_HUNT_CLIENT_ID` and `PRODUCT_HUNT_CLIENT_SECRET`. The user authorization redirect flow is only needed when an app needs user-context/private/write permissions.

## Run The App

Start the MCP server:

```powershell
uvicorn mcp_server.main:app --reload --port 8001
```

In a second terminal, start the agent backend and frontend:

```powershell
uvicorn agent_backend.main:app --reload --port 8000
```

Open:

```text
http://localhost:8000
```

Try:

```text
What consumer trends are emerging around better-for-you energy drinks in Texas?
```

## How The Agent Works

The frontend sends an insight request to `agent_backend`.

The agent backend defines tools that call the MCP server:

- `search_youtube_discussions`
- `search_news_narratives`
- `search_yelp_local_trends`
- `search_product_hunt_trends`
- `search_trend_signals`
- `get_trend_timeline`
- `compare_topics`
- `get_market_demographics`

When `GROQ_API_KEY` is configured, the query-planning phase uses Groq to turn the user's broad question into source-specific searches. The backend uses LangChain's OpenAI-compatible client with Groq's base URL, so no LLM key ever reaches the browser.

When no LLM key is configured, the backend uses the same MCP tools with a deterministic planner so the application remains demoable.

## Security And Constraints

- LLM keys stay in `.env` and are only used server-side.
- The frontend calls the agent backend, not public APIs directly.
- Public-data outputs are framed as hypotheses and signals, not proof of purchase behavior.
- YouTube/Yelp/Product Hunt/News outputs are public signals, not private user behavior or verified purchases.
- Source links and caveats are shown in the UI so the user can inspect what supported the brief.

## Video Demo Outline

1. Introduce the problem: marketers need to turn noisy public signals into campaign-ready insight.
2. Show the repo structure and the three layers: frontend, agent backend, MCP wrapper.
3. Run a query in the web app.
4. Explain the tool trace and source/caveat panels.
5. Open `mcp_server/main.py` and `agent_backend/agent.py` to show wrapper tools and LangChain tool definitions.
6. Open `docs/prompts/` to show how prompts were structured during development.
7. Open `docs/data-quality.md` to show how public API limits, freshness, and source quality were assessed.
8. Close with deployment: Dockerize both FastAPI services, serve the static frontend through the agent backend or a CDN, store secrets in a managed secret store, and deploy behind an API gateway.

## Tests

Run:

```powershell
pytest
```

The current tests cover model defaults and deterministic public-data story generation. A production version would add mocked GDELT/Census/Wikipedia API tests, integration tests for the agent route, and frontend smoke tests.


## Source provenance

- [Original MD](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/AI%20Builder/AI%20Builder%20Challenge/README.md) · AI Builder/AI Builder Challenge/README.md

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
