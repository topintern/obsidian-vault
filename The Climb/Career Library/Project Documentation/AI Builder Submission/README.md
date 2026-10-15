---
kind: "project-document"
title: "README"
collection: "AI Builder Submission"
topic: "Project Documentation"
imported: "2026-10-13"
source_files: ["AI Builder/AI Builder Submission/README.md"]
tags: ["career/library"]
source_status: "source-claims-not-verified"
---

# README

[[The Climb/Career Library/Career Library]]

# Consumer Trend Intelligence Agent

A conversational, tool-augmented agent that helps marketers discover emerging consumer trends in near-real time. You ask a question in plain English — about sentiment, competitors, market size, campaign ideas, or a full trend brief — and the agent fetches live signals from YouTube, NewsAPI, and Google Trends, synthesises them with an LLM, and returns a structured, evidence-grounded report with clickable source citations. Every insight is backed by data retrieved in the same session; nothing is hallucinated from training data alone.

---

## Architecture

The project is split into three independent services.

| Layer | Path | Responsibility |
|---|---|---|
| **MCP Tool Server** | `mcp_server/` | Stateless FastAPI service that owns all external I/O — YouTube Data API v3, NewsAPI, US Census ACS; one endpoint per tool. |
| **Agent Backend** | `agent_backend/` | FastAPI service that hosts the LangChain tool-calling agent, classifies intent, assembles prompts, dispatches tools via the MCP server, and streams structured responses. |
| **Frontend** | `frontend/` | Single-page HTML/JS UI served as static files by the agent backend; handles user input, streaming display, and source-link cards. |

---

## Prerequisites

- **Python 3.11 or later** (`python --version` to check)
- **Git**
- API keys for the services below — all have free tiers sufficient for demo use:

| Key | Where to get it | Env var |
|---|---|---|
| Groq *(primary LLM)* | [console.groq.com](https://console.groq.com) → API Keys | `GROQ_API_KEY` |
| Google Gemini *(fallback LLM)* | [aistudio.google.com](https://aistudio.google.com) → Get API key | `GEMINI_API_KEY` |
| YouTube Data API v3 | [console.cloud.google.com](https://console.cloud.google.com) → APIs & Services → Credentials | `YOUTUBE_API_KEY` |
| NewsAPI | [newsapi.org/register](https://newsapi.org/register) | `NEWS_API_KEY` |

You need **at least one** LLM key (Groq or Gemini). Both data-source keys are required for full functionality; the agent degrades gracefully if they are absent.

---

## Setup

### 1. Clone the repository

```bash
git clone <repo-url>
cd "AI Builder Submission"
```

### 2. Create and activate a virtual environment

```bash
python -m venv .venv
```

**Windows (PowerShell):**
```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned
.\.venv\Scripts\Activate.ps1
```

**macOS / Linux:**
```bash
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Create your `.env` file

```bash
cp .env.example .env          # Windows: copy .env.example .env
```

Open `.env` in any text editor and fill in your API keys:

```dotenv
# LLM — pick at least one
GROQ_API_KEY=gsk_...          # Groq key (primary)
GEMINI_API_KEY=AIza...        # Gemini key (fallback if Groq key is blank)

# Data sources
YOUTUBE_API_KEY=AIza...
NEWS_API_KEY=abc123...
```

Leave any key blank if you do not have it. Groq is tried first; if `GROQ_API_KEY` is empty the agent automatically falls back to Gemini. If both LLM keys are empty the app runs in **Fallback Mode** (see below).

---

## Running the Application

The MCP server must be started **before** the agent backend, because the backend calls it on every request.

### Step 1 — Start the MCP Tool Server (port 8001)

Open a terminal in the project root with the venv active:

```bash
uvicorn mcp_server.main:app --host localhost --port 8001 --reload
```

Verify it is healthy:
```bash
curl http://localhost:8001/health
# {"status":"ok"}
```

### Step 2 — Start the Agent Backend + Frontend (port 8000)

Open a **second** terminal with the venv active:

```bash
uvicorn agent_backend.main:app --host localhost --port 8000 --reload
```

### Step 3 — Open the app

Navigate to **http://localhost:8000** in your browser.

---

## Using the App

Type a question into the chat box and press **Ask**. The agent classifies your question into one of five intent types and selects the appropriate tools and report sections automatically.

### Example queries by intent

| Intent | What it produces | Example question |
|---|---|---|
| **Full Brief** | All sections: trends, motivation, audience, market stats, campaign ideas | `What are the top 3 emerging consumer trends in functional beverages this quarter?` |
| **Sentiment** | Consumer mood, viral signals, trending content | `What are people saying about energy drinks on YouTube right now?` |
| **Competitive** | Brand comparison, market share signals, head-to-head evidence | `How does Celsius compare to PRIME in social buzz and market presence?` |
| **Market** | Demographics, geographic size, income/age data | `What is the market size and consumer profile for plant-based dairy in Texas?` |
| **Campaign** | Audience hypotheses and activation ideas grounded in trend data | `Give me campaign ideas for a new adaptogen coffee targeting Gen Z.` |

You can also use the **quick-start chips** beneath the input box to load a pre-filled query.

The response includes:
- A structured report divided into evidence-gated sections
- A **Sources** panel with clickable links to every piece of evidence used
- A mode badge (e.g. `Agent · Competitive · Energy Drinks`) showing intent and detected category

---

## Fallback Mode

If **both** `GROQ_API_KEY` and `GEMINI_API_KEY` are empty, the app enters **Fallback Mode**. In this mode:

- No LLM is invoked.
- The agent backend calls the MCP tools directly and returns the raw signals as a plain-text summary.
- The response will include a caveat: *"LLM synthesis unavailable — showing raw public data only."*
- Source links are still populated.

Fallback Mode is useful for testing data-source connectivity without spending LLM quota, or for running the app on a machine without internet access to LLM providers (provided the data-source keys are still valid).

---

## Project Structure

```
.
├── mcp_server/             # MCP Tool Server
│   ├── main.py             # FastAPI app — 9 tool endpoints
│   ├── services.py         # YouTube, NewsAPI, Trends, Census fetch logic
│   ├── models.py           # Pydantic response models
│   └── config.py           # Settings loaded from .env
├── agent_backend/          # Agent Backend
│   ├── main.py             # FastAPI app — POST /chat + static files
│   ├── agent.py            # LangChain AgentExecutor builder
│   ├── intent.py           # Intent classification + category extraction
│   ├── prompts.py          # System prompt builder with evidence-gating rules
│   ├── tools.py            # StructuredTool wrappers around MCPClient
│   ├── mcp_client.py       # Async HTTP client for the MCP server
│   ├── models.py           # ChatRequest / ChatResponse Pydantic models
│   └── config.py           # Settings loaded from .env
├── frontend/
│   ├── index.html          # Single-page UI
│   └── app.js              # Form handler, streaming, source-link rendering
├── tests/                  # pytest test suite
├── docs/                   # Architecture and API docs
├── requirements.txt
├── .env.example            # Template — copy to .env and fill in keys
├── AGENTS.md               # AI session context (architecture rules, style guide)
└── PLAN.md                 # Phased build plan with completion status
```


## Source provenance

- [Original MD](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/AI%20Builder/AI%20Builder%20Submission/README.md) · AI Builder/AI Builder Submission/README.md

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
