---
kind: "project-document"
title: "Design Decisions"
collection: "AI Builder Challenge"
topic: "Project Documentation"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["AI Builder/AI Builder Challenge/DECISIONS.md"]
tags: ["career/library","career/project-docs"]
---

# Design Decisions

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# Decision Log

## 001. Use a public-data prototype instead of pretending to have proprietary data

**Decision:** The app uses GDELT and Census-style public data as a stand-in for consumer signals.

**Rationale:** This keeps the project honest and runnable while still aligning with inMarket's world of audience intelligence and marketing activation.

**Tradeoff:** Public data is not the same as purchase, location, or campaign measurement data. The app handles this by surfacing caveats in every response.

## 002. Put public APIs behind an MCP-style wrapper

**Decision:** The frontend and agent backend do not call GDELT or Census directly. They call `mcp_server/`.

**Rationale:** The assignment asks for a wrapper service, and the separation of concerns is one of the highest-weighted evaluation areas.

**Tradeoff:** There is one extra service to run, but the architecture is easier to explain and extend.

## 003. Expose marketer-friendly tools

**Decision:** Tools are named around user intent: `search_trend_signals`, `compare_topics`, and `get_market_demographics`.

**Rationale:** The LLM should operate through domain concepts. Raw API endpoints would make the agent look like a thin proxy.

**Tradeoff:** The wrapper has to normalize and interpret the source APIs, but that is exactly the architectural value this take-home wants to see.

## 004. Provide a fallback when no LLM key exists

**Decision:** The backend includes a deterministic public-data fallback brief.

**Rationale:** Reviewers can still run and inspect the web app without configuring an LLM key. The LangChain tool-calling code remains present for the intended path.

**Tradeoff:** The fallback is less nuanced than a real LLM response. It is labeled clearly in the UI as `public_data_fallback`.

## 005. Use a static frontend served by FastAPI

**Decision:** The frontend uses HTML, CSS, and JavaScript served by the agent backend.

**Rationale:** This keeps setup simple for a take-home project and avoids a separate Node build chain. The assignment asks for a web app, not necessarily a frontend framework.

**Tradeoff:** A React app would scale better for a larger product. For this demo, a focused static UI is easier to run and explain.

## 006. Treat documentation as part of the product

**Decision:** The repo includes AI context files and prompt logs.

**Rationale:** The evaluation rubric directly scores agentic development, prompt quality, presentation, and documentation. The documentation layer gives the evaluator evidence of process.

**Tradeoff:** More files exist than a minimal implementation needs, but every one supports the presentation.

## 007. Add a secondary CPG public signal source

**Decision:** The MCP wrapper can fall back to Open Food Facts product records for CPG-style queries.

**Rationale:** GDELT is useful for public media narratives, but live public APIs can throttle. Open Food Facts gives the demo another public, no-key source that is especially relevant for grocery, beverage, snack, and packaged goods examples.

**Tradeoff:** Product records are not trend measurements. The app labels them as secondary CPG signals and keeps caveats visible.

## 008. Treat public APIs as a source portfolio, not a single dependency

**Decision:** The MCP server combines GDELT, Wikipedia, Open Food Facts, and Census instead of relying on one public API.

**Rationale:** GDELT is the best fit for public narrative signals, but it enforces strict public rate limits. Wikipedia improves entity/category grounding, Open Food Facts adds product context for CPG categories, and Census adds market context.

**Tradeoff:** The agent must explain what each source can and cannot prove. The brief uses public signals for hypotheses and avoids claiming measured purchase behavior.

## 009. Add a broader behavior-like API stack

**Decision:** The MCP server now exposes YouTube, NewsAPI, Yelp, and Product Hunt tools.

**Rationale:** The new stack covers more use cases: YouTube for public comments/reviews, NewsAPI for media narratives, Yelp for local review texture, and Product Hunt for emerging product momentum.

**Tradeoff:** Each API requires its own credential and has a different bias. The agent treats all of them as public signals, not verified purchase, demographic, or location data.

## 010. Expose data-volume counters at the MCP boundary

**Decision:** Consumer-signal responses include raw text character count, retained excerpt character count, and engagement units.

**Rationale:** The demo needs to show not only which sources were called, but how much evidence was actually available for synthesis. This makes weak-source runs easy to diagnose without exposing API keys or dumping raw source text into the UI.

**Tradeoff:** Character counts are a practical proxy for ingestion volume, not a quality score. A long article can still be low-signal, and a short comment can contain a sharp consumer objection.

## 011. Move synthesis into a phased intelligence pipeline

**Decision:** The agent backend now runs query planning, source collection, filtering, source-level sentiment inference, trend analysis, and final brief writing as separate phases.

**Rationale:** The brief should feel like an insight article built from evidence, not a metadata recap. Separating phases makes it clear when the system is searching, when it is rejecting weak data, when it is inferring consumer motivation, and when it is turning those inferences into campaign strategy.

**Tradeoff:** The pipeline is more opinionated than a generic chat agent. That is intentional for the take-home: the product is a marketer-facing intelligence workflow, not a general-purpose search assistant.

## 012. Prefer Groq for LLM-assisted planning

**Decision:** LLM calls use `GROQ_API_KEY` and Groq's OpenAI-compatible API when configured. OpenAI remains only as a secondary local fallback for older `.env` files.

**Rationale:** The user supplied a Groq key and the current pipeline only needs a fast, low-latency model for source-specific query planning. The rest of the brief stays grounded in collected public evidence and deterministic filtering/synthesis.

**Tradeoff:** Groq model availability can change, so the model name is configurable through `GROQ_MODEL`.


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/AI%20Builder/AI%20Builder%20Challenge/DECISIONS.md) · AI Builder/AI Builder Challenge/DECISIONS.md

Project code and dependencies remain outside the vault. No source commands were executed.
