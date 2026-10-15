---
kind: "project-document"
title: "Project Plan"
collection: "AI Builder Submission"
topic: "Project Documentation"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["AI Builder/AI Builder Submission/PLAN.md"]
tags: ["career/library","career/project-docs"]
---

# Project Plan

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# PLAN.md — Build Sequence

> Phased delivery plan for the Consumer Trend Intelligence Agent.
> Each phase is independently deployable and testable before the next begins.

---

## Status Key

| Symbol | Meaning |
|---|---|
| ✅ | Complete |
| 🔄 | In progress |
| ⬜ | Not started |

---

## Phase 0 — Bootstrap ✅

**Goal:** Establish project skeleton, conventions, and AI context.

- ✅ Create monorepo folder structure (`mcp_server/`, `agent_backend/`, `frontend/`, `tests/`, `docs/`)
- ✅ Add top-level `requirements.txt`, `.env.example`, `.gitignore`, `README.md`
- ✅ Write `AGENTS.md` (AI session context: intent, users, architecture, style, demo defaults)
- ✅ Write `PLAN.md` (this file)

---

## Phase 1 — MCP Server ⬜

**Goal:** Expose all external data fetching as a single FastAPI service the agent backend can call.

- [ ] `mcp_server/config.py` — Settings loaded from `.env` via `pydantic-settings`
- [ ] `mcp_server/models.py` — Pydantic request/response models for all tool endpoints
- [ ] `mcp_server/services.py` — All tool logic: news fetch, trends, YouTube, web search
- [ ] `mcp_server/main.py` — FastAPI app; one route per tool; wire up services

### Tests
- [ ] `tests/mcp_server/test_services.py` — Unit tests with mocked HTTP calls
- [ ] `tests/fixtures/` — Offline fixture JSON for each data source (enables demo mode)

---

## Phase 2 — Agent Backend ⬜

**Goal:** Build the LangChain tool-calling agent backend.

- [ ] `agent_backend/config.py` — Settings (LLM provider, MCP server URL, max tool calls)
- [ ] `agent_backend/models.py` — Chat message and response Pydantic models
- [ ] `agent_backend/mcp_client.py` — `httpx` client that calls `mcp_server` tool endpoints
- [ ] `agent_backend/prompts.py` — System prompt and trend-analysis prompt templates
- [ ] `agent_backend/agent.py` — LangChain tool-calling agent using `create_tool_calling_agent` and `AgentExecutor`; Groq LLM when key is present, deterministic fallback when not
- [ ] `agent_backend/main.py` — FastAPI app; `/chat` SSE endpoint; wire up agent

### Tests
- [ ] `tests/agent_backend/test_agent.py` — Graph logic with mocked MCP client
- [ ] `tests/agent_backend/test_mcp_client.py` — MCP client with mocked HTTP responses

---

## Phase 3 — Frontend ⬜

**Goal:** Build a static conversational UI served directly by the `agent_backend` FastAPI app.

No Python files in `frontend/`. The `agent_backend` mounts `frontend/` as a `StaticFiles` directory and serves `index.html` at the root.

- [ ] `frontend/index.html` — App shell: chat thread, sources panel, and brand/market inputs
- [ ] `frontend/styles.css` — Layout and typography; mobile-readable, no framework dependency
- [ ] `frontend/app.js` — SSE client; streams tokens from `/chat`; renders Markdown responses and cited sources

### Tests
- [ ] `tests/frontend/test_static.py` — Smoke test: verify `agent_backend` serves `index.html` at `/`

---

## Phase 4 — Documentation Layer ⬜

**Goal:** Produce developer and user-facing documentation.

- [ ] `docs/architecture.md` — Service diagram, data flow, and decision log
- [ ] `docs/mcp_tools.md` — Tool catalogue: name, description, inputs, outputs, example
- [ ] `docs/agent_design.md` — Agent design walkthrough: tool-calling loop, prompt structure, LLM selection
- [ ] `docs/demo_guide.md` — Step-by-step stakeholder demo script
- [ ] `docs/runbook.md` — Local setup, environment variables, and troubleshooting

---

## Phase 5 — Hardening & Polish ⬜

**Goal:** Production-readiness gate before any external review.

- [ ] End-to-end integration test covering full request → MCP → agent → SSE → UI flow
- [ ] Error handling audit: verify no raw traces reach the frontend
- [ ] Offline demo smoke test using `tests/fixtures/` data
- [ ] `requirements.txt` version pin audit
- [ ] `README.md` — Fill in full getting-started guide
- [ ] Final `AGENTS.md` review — confirm all sections reflect shipped behaviour


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/AI%20Builder/AI%20Builder%20Submission/PLAN.md) · AI Builder/AI Builder Submission/PLAN.md

Project code and dependencies remain outside the vault. No source commands were executed.
