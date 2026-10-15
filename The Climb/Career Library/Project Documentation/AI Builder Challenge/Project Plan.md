---
kind: "project-document"
title: "Project Plan"
collection: "AI Builder Challenge"
topic: "Project Documentation"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["AI Builder/AI Builder Challenge/PLAN.md"]
tags: ["career/library","career/project-docs"]
---

# Project Plan

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# Project Plan

## Goal

Create a take-home-ready, agentic web application that demonstrates:

- A public REST API wrapped behind an MCP-style microservice.
- An LLM agent backend that uses tool calling through LangChain.
- A frontend web app where a marketer can ask for consumer trend intelligence.
- Documentation that preserves product intent, architecture, prompts, and rationale.

## Build Sequence

### 1. Project Framing - Complete

The project is framed as a public-data prototype for consumer trend intelligence. The target user is a marketer or strategist who needs fast public-signal context before planning an audience, message, or campaign.

### 2. MCP Wrapper - Complete

The MCP server exposes domain-specific tools:

- `search_trend_signals`
- `get_trend_timeline`
- `compare_topics`
- `get_market_demographics`

Rationale: the agent should reason in marketing concepts instead of raw API mechanics.

### 3. Agent Backend - Complete

The backend accepts an insight request, uses Groq for LLM-assisted query planning when `GROQ_API_KEY` is present, and falls back to a deterministic planner when no LLM key is present.

Rationale: the evaluator can run the project even without an LLM key, while the intended LLM-assisted agent phase remains visible and testable.

The current synthesis path is phased:

- Query planning creates source-specific searches.
- Source collection stores records by source.
- Filtering removes low-relevance, low-engagement, and low-text records.
- Sentiment inference runs source by source.
- Trend analysis turns inferred sentiments into the final brief sections.

Rationale: this makes the app feel like an intelligence workflow rather than a single prompt wrapped around search results.

### 4. Frontend Workspace - Complete

The web app presents a focused intelligence workspace:

- Business question input.
- Category, geography, timeframe, and output controls.
- Insight brief output.
- Tool trace, sources, and caveats.

Rationale: the UI reinforces transparency. A marketer can see both the answer and the evidence trail.

### 5. Documentation Layer - Complete

The repo includes:

- `README.md`
- `AGENTS.md`
- `PLAN.md`
- `DECISIONS.md`
- `docs/architecture.md`
- `docs/prompts/`

Rationale: the assignment explicitly asks candidates to show approach and prompts. The docs make that easy to present on camera.

## Demo Story

1. Start with the business context: marketers are flooded with public signals, but translating them into action is slow.
2. Show the web app with a query about a category and market.
3. Point out that the frontend calls the agent backend, not the public APIs directly.
4. Show the tool trace and explain the MCP wrapper.
5. Explain the production path: replace public APIs with proprietary audience, purchase, location, and measurement sources.
6. Open the prompt logs and explain how the agentic development process was structured.

## Remaining Nice-to-Haves

- Add charts for trend timelines.
- Add saved briefs.
- Add an export-to-markdown button.
- Add a second public source for product/category detail, such as Open Food Facts for CPG examples.


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/AI%20Builder/AI%20Builder%20Challenge/PLAN.md) · AI Builder/AI Builder Challenge/PLAN.md

Project code and dependencies remain outside the vault. No source commands were executed.
