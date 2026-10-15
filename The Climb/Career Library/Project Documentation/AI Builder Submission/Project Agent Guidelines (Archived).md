---
kind: "project-document"
title: "Project Agent Guidelines (Archived)"
collection: "AI Builder Submission"
topic: "Project Documentation"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["AI Builder/AI Builder Submission/AGENTS.md"]
tags: ["career/library","career/project-docs"]
---

# Project Agent Guidelines (Archived)

[[Project Library]] · [[Career Library]]

> [!info] Archived project guidance
> This is source material from the external project, not instructions governing this vault or authorisation to run its commands.

# AGENTS.md — AI Session Context

> This file is the authoritative context document for AI coding assistants working in this repository.
> Read it fully before making any changes. It governs intent, architecture, style, and demo behaviour.

---

## Project Intent

**Consumer Trend Intelligence Agent** — an agentic web application that helps marketers discover, analyse, and act on emerging consumer trends in near-real time.

The agent ingests signals from configurable data sources (social media, search trends, news, retail data), synthesises them into structured trend reports, and surfaces actionable recommendations tailored to the marketer's brand category and campaign goals.

Core value proposition:
- Replace hours of manual trend research with a conversational, tool-augmented agent
- Ground every insight in cited evidence, not hallucination
- Allow marketers to iterate on briefs through natural language chat

---

## Target Users

| Persona | Description | Primary Need |
|---|---|---|
| Brand Marketer | Mid-to-senior marketer at a consumer goods or retail brand | Spot trends before competitors; brief creative teams |
| Insights Analyst | Research/strategy role supporting marketing | Deep-dive reports with data citations |
| Campaign Manager | Execution-focused marketer with tight deadlines | Quick trend summaries tied to campaign calendar |

Users are **non-technical**. All outputs must be plain-language, skimmable, and export-friendly (Markdown / PDF). No raw JSON or code should ever surface in the UI.

---

## Architecture Rules

### Service Boundaries

```
mcp_server/       — MCP-compliant tool server; exposes search, fetch, and analysis tools
agent_backend/    — Orchestration layer; hosts the LangGraph agent loop and session state
frontend/         — Conversational UI; streams agent responses; no business logic here
```

- **mcp_server** owns all external I/O (API calls, scraping, database reads). It must be stateless per request.
- **agent_backend** owns agent state, memory, tool dispatch, and prompt assembly. It must never call external APIs directly — only via MCP tools.
- **frontend** owns only presentation and user input. It must never call MCP tools directly.

### Communication
- `frontend` → `agent_backend`: REST + SSE streaming (FastAPI)
- `agent_backend` → `mcp_server`: MCP protocol over HTTP (JSON-RPC 2.0)
- All service ports defined in `.env`; never hardcode

### Agent Design
- Framework: **LangChain tool-calling agent** (`create_tool_calling_agent`); LangGraph is an optional extension
- LLM: configurable via env var `LLM_PROVIDER`; default `openai/gpt-4o`
- Tool calls must be **logged** with input, output, and latency
- Agent must support **streaming** token output to the frontend
- All agent responses must include a `sources` field listing evidence citations
- Maximum tool call depth per turn: **5**

### Data & State
- Session state stored in-memory during demo; persistent store (Redis/Postgres) is a future concern
- No PII collected or stored at any point
- All trend data treated as ephemeral; no caching beyond a single session

### Error Handling
- MCP tool failures return structured error objects; the agent must degrade gracefully
- Never expose raw exception traces to the frontend
- Retry transient errors up to 2 times with exponential backoff

---

## Working Style Notes

These rules apply to all AI assistants editing this codebase.

### General
- **Python 3.11+** throughout; use `from __future__ import annotations` in all modules
- Type-annotate all function signatures; use `pydantic` models for all data contracts
- Prefer composition over inheritance
- No global mutable state

### File & Module Conventions
- One class or one logical group of functions per module
- Module names: `snake_case`; class names: `PascalCase`
- All public functions and classes require a one-line docstring (no param/return blocks unless complex)
- Keep files under 300 lines; split if larger

### Dependencies
- Add every new dependency to `requirements.txt` with a pinned minor version (e.g. `fastapi>=0.111,<0.112`)
- Never install packages silently; always update `requirements.txt`

### Testing
- All tests live in `tests/`; mirror the source tree (e.g. `tests/agent_backend/`)
- Use `pytest` + `pytest-asyncio`; no `unittest`
- Mock all external calls in unit tests; integration tests are clearly labelled
- Target: every public function has at least one test

### Git Hygiene
- Commit messages: `<type>(<scope>): <subject>` (conventional commits)
- Never commit `.env`; only `.env.example`
- Do not commit generated files or `__pycache__`

---

## Demo Defaults

These values are used when running the app for demonstration or stakeholder review.

| Setting | Default Value |
|---|---|
| Demo brand category | `Functional Beverages` |
| Demo market | `United States` |
| Demo time horizon | `Next 90 days` |
| Seed query | `"What are the top 3 emerging consumer trends in functional beverages this quarter?"` |
| LLM | `openai/gpt-4o` |
| MCP server URL | `http://localhost:8001` |
| Agent backend URL | `http://localhost:8000` |
| Frontend URL | `http://localhost:3000` |
| Streaming | Enabled |
| Max tool calls | 5 |

Demo mode must work fully offline from external trend APIs using the fixture data in `tests/fixtures/` (to be created).

---

## Out of Scope (v1)

- User authentication / multi-tenancy
- Persistent trend history across sessions
- Scheduled / automated trend reports (push model)
- Fine-tuned or custom LLMs
- Mobile-native UI


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/AI%20Builder/AI%20Builder%20Submission/AGENTS.md) · AI Builder/AI Builder Submission/AGENTS.md

Project code and dependencies remain outside the vault. No source commands were executed.
