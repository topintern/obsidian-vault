---
kind: "project-document"
title: "Project Agent Guidelines (Archived)"
collection: "AI Builder Challenge"
topic: "Project Documentation"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["AI Builder/AI Builder Challenge/AGENTS.md"]
tags: ["career/library","career/project-docs"]
---

# Project Agent Guidelines (Archived)

[[Project Library]] · [[Career Library]]

> [!info] Archived project guidance
> This is source material from the external project, not instructions governing this vault or authorisation to run its commands.

# AI Session Context

This repo is a take-home project for an AI Builder role. Treat it as both an application and a demonstration of working style.

## Project Intent

Build an **AI Consumer Trend Intelligence Agent** that helps marketers and strategists turn public signals into actionable consumer insight briefs.

The company context is inMarket. The prototype should feel adjacent to audience intelligence, consumer behavior, marketing activation, and real-time signal interpretation without claiming access to inMarket's proprietary location, purchase, audience, or measurement data.

The key narrative:

> This prototype uses public data as a stand-in for consumer signals. In a production marketing intelligence environment, the same agent pattern could connect to proprietary purchase, location, audience, and campaign measurement datasets.

## Product Users

- Brand marketers looking for campaign angles.
- Media strategists looking for audience and message hypotheses.
- Category analysts looking for emerging market narratives.
- Agency planners building fast context before a pitch or client brief.
- Sales or insights teams preparing a lightweight point of view.

## Architecture Rules

- Keep the MCP wrapper, agent backend, and frontend visibly separated.
- The frontend should never call public data APIs directly.
- API keys stay server-side. Never place an LLM key in frontend code.
- Public data claims must remain carefully worded. These signals suggest narratives and hypotheses; they do not prove sales, visitation, or individual behavior.
- Favor business-friendly tool names over raw API names.

## Working Style

- Preserve the documentation layer. It is part of the submission, not garnish.
- When adding features, update `PLAN.md`, `DECISIONS.md`, and relevant prompt logs.
- Keep explanations practical and demo-ready.
- Bias toward a polished vertical slice over a broad, unfinished platform.

## Current Services

- `mcp_server/`: FastAPI wrapper over public data sources.
- `agent_backend/`: FastAPI app with LangChain tool-calling path and fallback public-data brief path.
- `frontend/`: Static web UI served by the agent backend.

## Demo Defaults

Good first query:

> What consumer trends are emerging around better-for-you energy drinks in Texas?

Useful follow-up:

> Turn this into three audience hypotheses and campaign angles for a retail media activation.


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/AI%20Builder/AI%20Builder%20Challenge/AGENTS.md) · AI Builder/AI Builder Challenge/AGENTS.md

Project code and dependencies remain outside the vault. No source commands were executed.
