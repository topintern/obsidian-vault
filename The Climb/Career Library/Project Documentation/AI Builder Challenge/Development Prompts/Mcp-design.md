---
kind: "project-document"
title: "Mcp-design"
collection: "AI Builder Challenge"
topic: "Project Documentation"
imported: "2026-10-13"
source_files: ["AI Builder/AI Builder Challenge/docs/prompts/mcp-design.md"]
tags: ["career/library"]
source_status: "source-claims-not-verified"
---

# Mcp-design

[[The Climb/Career Library/Career Library]]

# MCP Design Prompt Log

These prompts are written as a progressive development record. They can be shown during the video demo to explain how the MCP wrapper was planned and refined.

## Prompt 1: Pick the wrapper concept

```text
We need a take-home project for an AI Builder role at a company focused on consumer intelligence and marketing activation. Design an MCP-style wrapper around public APIs that can support a Consumer Trend Intelligence Agent. Avoid proprietary data claims. Recommend tools that are useful to marketers, not generic API passthroughs.
```

### Rationale

This prompt frames the wrapper around the business domain. The goal is not to expose every API operation. The goal is to create a small tool surface the LLM can reason about.

## Prompt 2: Define tool names and boundaries

```text
Create a minimal MCP server API for a public-data consumer signal agent. Tools should include trend search, timeline volume, topic comparison, and market demographics. Each tool should have clear inputs, normalized outputs, and caveats that remind the user that public signals do not prove purchase or location behavior.
```

### Rationale

This led to:

- `search_trend_signals`
- `get_trend_timeline`
- `compare_topics`
- `get_market_demographics`

The names are intentionally business-readable.

## Prompt 3: Handle source limitations

```text
Add response caveats to the MCP wrapper. GDELT and Census should be represented honestly: useful public signal and market context sources, but not direct evidence of consumer purchases, visitation, or individual behavior. Make these caveats available to the agent and frontend.
```

### Rationale

The caveats are part of product trust. The user should know when an output is a hypothesis, not a measurement claim.

## Prompt 4: Add demo resilience

```text
If GDELT throttles or returns no articles, add a secondary public CPG data source that can still provide useful product/category context. Label the fallback clearly so reviewers understand it is product signal context, not a replacement for media trend volume.
```

### Rationale

Public APIs can rate-limit during demos. Open Food Facts gives the app a second public source that fits the chosen category examples while preserving transparency.

## Prompt 5: Add behavior-like public API layers

```text
Add YouTube Data API comments, NewsAPI, Yelp Fusion, and Product Hunt. Each MCP tool should return a normalized signal response with sources, themes, motivations, objections, competitor mentions, engagement summary, and caveats. The agent should use these public signals as behavior-like evidence without claiming verified purchase behavior.
```

### Rationale

Reference and product APIs give context, but YouTube comments, local reviews, media coverage, and emerging product launches give richer motivation, objection, and momentum signals.


## Source provenance

- [Original MD](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/AI%20Builder/AI%20Builder%20Challenge/docs/prompts/mcp-design.md) · AI Builder/AI Builder Challenge/docs/prompts/mcp-design.md

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
