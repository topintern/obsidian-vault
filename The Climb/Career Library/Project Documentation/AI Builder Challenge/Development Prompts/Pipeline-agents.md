---
kind: "project-document"
title: "Pipeline-agents"
collection: "AI Builder Challenge"
topic: "Project Documentation"
imported: "2026-10-13"
source_files: ["AI Builder/AI Builder Challenge/docs/prompts/pipeline-agents.md"]
tags: ["career/library"]
source_status: "source-claims-not-verified"
---

# Pipeline-agents

[[The Climb/Career Library/Career Library]]

# Pipeline Agents Prompt Log

## Intent

The brief should read like a strategist worked through the evidence, not like a search engine exported metadata.

The working model is a small chain of specialist phases:

1. Query planner
2. Source collector
3. Filtering agent
4. Source sentiment analyst
5. Trend analyzer
6. Final brief writer

## Query Planner

Provider: Groq when `GROQ_API_KEY` is configured. The app calls Groq through LangChain's OpenAI-compatible client and keeps the key server-side.

Prompt shape:

```text
Create source-specific search queries for a consumer trend intelligence brief.
Return compact JSON only with keys youtube, news, yelp, product_hunt, public_web.
Each value must be an array of 1-3 queries optimized for high-engagement, hot, relevant sources.
YouTube queries should favor reviews, comparisons, taste tests, and comments.
News queries should favor market narrative, health, retail, and brand momentum.
Yelp queries should be local business-discovery terms.
Product Hunt queries should only use launch/product language.
```

Rationale: the same user question should not be sent verbatim to every API. Each source rewards a different search grammar.

## Filtering Agent

Filtering looks at each source record as its own evidence unit. It scores:

- Query relevance in title, excerpt, and themes.
- Engagement units when available.
- Raw text volume.
- Whether the source type is a good fit for the category.
- Over-representation from one source type.

Rationale: a high-volume source can bias the story if every weak record is allowed through. Filtering makes the final brief narrower, but more defensible.

## Source Sentiment Analyst

Each retained source is labeled with one or more consumer tensions:

- Brand comparison and switching
- Performance proof seeking
- Cleaner energy / wellness permission
- Taste and repeat-purchase risk
- Price and value skepticism
- Crash, jitters, and safety concern
- Availability and routine fit

Rationale: the final story should emerge from repeated tensions across sources, not from one isolated quote or headline.

## Trend Analyzer

The trend analyzer groups source-level inferences into the user-facing sections:

- Executive read
- Signal-backed trends
- Consumer motivation
- Audience hypotheses
- Market stats
- Campaign / activation ideas

Rationale: marketers need the why, who, and what-to-do-next. The final brief should preserve links inside claims so a reader can click when a claim feels interesting or questionable.


## Source provenance

- [Original MD](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/AI%20Builder/AI%20Builder%20Challenge/docs/prompts/pipeline-agents.md) · AI Builder/AI Builder Challenge/docs/prompts/pipeline-agents.md

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
