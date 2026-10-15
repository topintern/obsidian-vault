---
kind: "project-document"
title: "Langchain-tools"
collection: "AI Builder Challenge"
topic: "Project Documentation"
imported: "2026-10-13"
source_files: ["AI Builder/AI Builder Challenge/docs/prompts/langchain-tools.md"]
tags: ["career/library"]
source_status: "source-claims-not-verified"
---

# Langchain-tools

[[The Climb/Career Library/Career Library]]

# LangChain Tooling Prompt Log

## Prompt 1: Agent role

```text
Write the system prompt for an LLM agent that serves marketers and category strategists. It should turn public signals into intelligence briefs with trends, motivations, audience hypotheses, activation ideas, confidence, caveats, and source notes. It must avoid overstating public data as purchase or location behavior.
```

### Rationale

The system prompt makes the agent an insights partner rather than a generic assistant.

## Prompt 2: Tool definitions

```text
Create LangChain tool definitions that call a separate MCP server rather than public APIs directly. The tools should map to the MCP wrapper: search trend signals, get trend timeline, compare topics, and get market demographics. Use structured args so the model has a clear schema.
```

### Rationale

This protects the architecture boundary. The agent can choose tools, but the wrapper owns public API mechanics.

## Prompt 2B: Behavior-like signal tools

```text
Add LangChain tools for search_youtube_discussions, search_news_narratives, search_yelp_local_trends, and search_product_hunt_trends. These should help the agent answer what consumers are saying, what media is amplifying, what local demand looks like, what products are emerging, which objections repeat, and how engagement-weighted discussion changes audience and campaign recommendations.
```

### Rationale

The agent needs behavior-like public signals. YouTube comments, Yelp review texture, NewsAPI articles, and Product Hunt launches are not purchase truth, but they make the brief read like consumer intelligence rather than a reference-page summary.

## Prompt 3: Fallback path

```text
Design a fallback response path for the agent backend when no LLM API key is configured. The fallback should still call the MCP server, return a useful public-data brief, label itself clearly, and keep the app demoable for reviewers.
```

### Rationale

Take-home projects are often reviewed quickly. The app should still run and tell its architectural story even if the reviewer has not configured an LLM key.

## Prompt 4: Output shape

```text
Make the final answer readable as a marketer-ready brief, not a raw JSON response. Include an executive read, signal-backed trends, consumer motivations, audience hypotheses, campaign ideas, confidence, and caveats.
```

### Rationale

The project should demonstrate contextual relevance, not just successful function calls.


## Source provenance

- [Original MD](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/AI%20Builder/AI%20Builder%20Challenge/docs/prompts/langchain-tools.md) · AI Builder/AI Builder Challenge/docs/prompts/langchain-tools.md

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
