---
kind: "company-prep"
title: "Round2 Prep V2"
collection: "EM1"
topic: "Interview Prep"
imported: "2026-10-13"
source_files: ["Interview Prep company prep docs/EM1/Round2_Prep_v2.html","Interview Prep company prep docs/EM1/Round2_Prep_v2.md"]
tags: ["career/library"]
source_status: "source-claims-not-verified"
---

# Round2 Prep V2

[[The Climb/Career Library/Career Library]]

> [!info] Source context
> Historical preparation or source notes. First-person stories and numeric outcomes remain source claims until confirmed; this import does not verify them.

# EM1 — Round 2 Interview Prep
### Gunnar Holwerda, CTO / Co-Founder | Wednesday June 10, 2026 | 60–90 min

---

> **How to use this doc:**
> - **Monday:** Read Part 1 (company context) + Part 2 (system design). These are the highest-risk questions. Know them cold.
> - **Tuesday AM:** Work through Part 3 (technical deep-dives) + Part 4 (stack-specific).
> - **Tuesday PM:** Read Part 5 (behavioral) out loud — practice the stories, not just read them.
> - **Wednesday morning:** Part 0 only (cheat sheet). Do not re-read the whole doc. Trust the prep.

---

# PART 0 — DAY-OF CHEAT SHEET
> Wednesday morning. One read. Then close it.

## Key Numbers (use these — they signal you did your homework)
- **60+ agencies** on the platform (state, county, city)
- **111 guidelines** per standard FEMA HMP evaluation
- **500–2000 pages** per emergency plan
- **~6,600 LLM calls/month** at current scale (111 × 60) → ~66K at 10x
- **4 engineers** including Gunnar (+ 2 early-career, data analyst, EM operators)
- **3 modules:** E01 Evaluate, E02 Improve, E03 Operationalize/Chat
- **Near-term focus:** Vanta-style compliance module — replacing email/manual intake with self-serve form + automated async crosswalk

## One-Line Answers (alignment table)
| What Gunnar Needs | Your One-Liner |
|---|---|
| "Vanta-style compliance module" | "I built this at Samay — the mapping from SOC2 controls to FEMA guidelines is a configuration change, the architecture is identical" |
| "Graph-RAG" | "Right for multi-hop cross-doc queries; overkill for single-plan retrieval — I used Neo4j for exactly the use case where it earns its complexity" |
| "Sentence-level citations" | "That's the evidence-gating pattern — Pydantic schema forces a verbatim quote, no quote = INCONCLUSIVE, no hallucination path to PASS" |
| "Human in the loop" | "Automate the tedious, preserve the judgment — LLM does the 2000-page reading, human signs off on the verdict" |
| "Full-stack ownership" | "Not 'I own the backend' — CDK infrastructure, Lambda suite, API, and React UI. All of it, no handoffs" |
| "Small team / 4 engineers" | "Samay was effectively solo — I owned everything and prefer that context" |
| "Mentor junior engineers" | "OSU GTA for a year, code reviews that teach not just flag, picked up test coverage for a struggling junior without being asked" |
| "Next.js" | "React + TypeScript is the foundation — App Router, RSC model are the ramp. Productive in a week." |
| "Terraform" | "Deep CDK (same discipline, different syntax) + Azure Terraform at Samay. Contributing to existing codebase within a sprint." |

## Opening Line
> "I'm Neel — six years full-stack, last two deep in AI systems. The most directly relevant work is TrustX at Samay — I was the sole engineer on a compliance automation platform. The core was: collect evidence from multiple sources, assemble grounded context, send to an LLM for a scored verdict with citations. When you describe the Evaluate module — automated FEMA crosswalk, Smart References — that's the same architecture in a different domain. I've been looking forward to this conversation."

## Closing Line
> "This has been exactly the kind of technical conversation I was hoping for. What you're building — grounded AI with citation accountability in a domain where wrong answers have real stakes — is the problem I care about. I'd love to keep moving forward."

## Questions to Ask (pick 3)
1. "The crosswalk — are you chunking plans structurally by section or by token count? I'd expect section-aware parsing to be the hard part for citation precision."
2. "For Deconflict — are you doing cross-document contradiction detection today, or is that upcoming? Curious whether you're modelling it as a graph problem."
3. "The 2 early-career engineers — how do you think about mentoring in a small team? I want to understand what supporting them well looks like."
4. "Coming from OpenSesame and Olo — what engineering habits are you deliberately bringing to EM1, and what are you leaving behind?"
5. "What's the biggest technical problem on the roadmap right now — something an engineer joining now would own end-to-end?"

---

# PART 1 — KNOW THE COMPANY FIRST
> Read this before any answers. Context shapes everything.

## What's Built vs. What You're Building

| Component | Current State | What Changes |
|---|---|---|
| Core AI | "Simple RAG" — indexes large EM PDFs, retrieves relevant passages | Extend: better structural retrieval, cross-doc reasoning |
| Document library | Aggregates public plans + customer-contributed docs, cross-share between non-competing agencies | Improve cross-sharing, search, library ↔ agent integration |
| Compliance crosswalk | Separate product — breaks FEMA requirements into checklists, validates plan against them | Automate with Vanta-style self-serve intake |
| Current intake | **Email or manual upload; human manually triggers compliance checks** | Replace entirely with self-serve form + automated trigger |
| Customer base | **60+ agencies** (state, county, city) | — |
| Evaluation scale | **~111 FEMA guidelines** per standard HMP evaluation | — |

**The job of this role:** Build the form-based intake, automate the trigger, ship the async evaluation pipeline, extend the RAG, contribute to agent skills. Own it across backend + infra + frontend.

## The Three Modules (know these cold)

| Module | What It Does | Key Feature |
|---|---|---|
| **E01 — Evaluate** | Automated FEMA crosswalk of plans | Smart References: which page answers which guideline |
| **E02 — Improve** | Plan Library + Peer Docs + Deconflict | Deconflict: finds contradictions ACROSS multiple plans |
| **E03 — Operationalize** | Custom knowledge base + real-time chat Q&A | Surfaced as "Chat" in the nav |

**Custom evaluations:** Agencies can build their own guideline checklists — not just FEMA library. The guideline store is multi-tenant and user-editable. Architectural implication: guidelines have an `owner` field (system vs. agency).

## Domain Terminology (know these, use them naturally)
| Term | Meaning |
|---|---|
| **EOP** | Emergency Operations Plan — master disaster response plan |
| **HMP** | Hazard Mitigation Plan — FEMA-required; must pass periodic assessments |
| **COOP** | Continuity of Operations Plan — how the agency keeps running during a disaster |
| **IAP** | Incident Action Plan — operational plan for a specific incident |
| **AAR** | After Action Report — post-incident lessons learned |
| **EOC** | Emergency Operations Center — command hub during a disaster |
| **FEMA** | Sets national doctrine; EM1 evaluates plans against FEMA guidelines |
| **Doctrine** | The authoritative federal/state guidance EMs are required to follow |

## Samay ↔ EM1 Translation (your experience maps directly)
| Samay (what you built) | EM1 (what you're describing) |
|---|---|
| SOC2/NIST/ISO27001 controls | FEMA guidelines |
| AWS infra + GitHub/Jira data | Emergency plan document sections |
| Evidence collection Lambda (6 sources) | Document parsing + chunking pipeline |
| LLM compliance scoring (Bedrock) | Guideline crosswalk evaluation |
| Structured output with evidence quotes | Smart References (guideline → exact plan page) |
| Controls dashboard (React) | Evaluate module UI |
| Per-tenant S3 / schema isolation | Per-agency document isolation |

## The Team
- Gunnar Holwerda — CTO/Co-founder. Engineering leader at OpenSesame (enterprise B2B SaaS) and Olo (restaurant tech, high-scale). Knows production engineering at scale. Respects concrete numbers over buzzwords.
- Tyler Felous — CEO/Co-founder. Built and sold Wisely (fintech).
- 4 engineers total including Gunnar. 2 early-career engineers. Data analyst/researcher. EM operators on the team.


---

# PART 2 — SYSTEM DESIGN (MASTER ANSWERS)
> **Study Monday. Highest-risk questions. Know these cold before anything else.**
> The system design question will come in many forms — they all map to one of these answers.

---

## 2A: FULL END-TO-END SYSTEM — THE VANTA-STYLE MODULE
> **The master answer. Lead with this for any broad system design question. ~4-5 min, then let him steer.**

### Critical framing (say this first):
> "The current flow is: plans come in by email, a human manually uploads and manually triggers the compliance check. The Vanta module automates everything from intake to results — the human only re-enters at the review and sign-off step. That is exactly the right place for them to be."

### The 6-Stage Flow:

**Stage 1 — Self-Serve Intake Form**
Replaces email. The form collects: plan type (EOP/HMP/COOP), agency (pre-populated from account), plan version/date, file upload, guideline library selection (FEMA standard, state, or custom). File upload uses a **presigned S3 PUT URL** — large PDFs go directly browser→S3, not through the API server. On submit: `POST /evaluations` returns `{job_id, status: "QUEUED"}` immediately. User sees: "Your plan has been submitted. We'll notify you when the evaluation is complete."

**Stage 2 — Async Job Queue**
API handler writes `evaluation_jobs` record + publishes to SQS. Worker consumes and processes. Double-submit protection: unique constraint on `(agency_id, plan_file_hash)` returns the existing job instead of starting a duplicate. This is the core architectural change from the current model — the human coordinator is replaced by a job queue.

**Stage 3 — Document Ingestion (if new plan version)**
Check if this exact file hash has been indexed before — if yes, skip. If no:
1. Structure-aware parsing: extract section map (section number → heading → page range), not naive token chunking
2. Two-level indexing: section summaries (~500 tokens) AND paragraph chunks (~150-200 tokens with overlap)
3. Every chunk tagged with provenance: `{agency_id, doc_id, section, heading, page, chunk_index}`
4. Embed + write to pgvector; metadata to PostgreSQL

**Stage 4 — Crosswalk Evaluation Loop (111 guidelines)**
For each guideline:
1. Hierarchical retrieval: query section summaries → identify top 2-3 sections → retrieve paragraph chunks from within those sections only
2. LLM call with Pydantic output schema: `{verdict: PASS|PARTIAL|FAIL|INCONCLUSIVE, evidence_quote: str, page_reference: str, gaps: list[str]}`
3. Evidence gate: if `evidence_quote` is empty or not in the retrieved context → force `INCONCLUSIVE`. The LLM cannot hallucinate a PASS.
4. Write result to `evaluation_results` per guideline; update progress counter

**Cost optimization:** Cache results keyed on `(guideline_id, chunk_hash)`. If plan section hasn't changed since last run, reuse the cached result. Repeat evaluations are 60-70% cheaper than first-time runs.

**Stage 5 — Human-in-the-Loop Review**
The LLM output is the first-pass reviewer, not the final verdict.

- **PASS (high confidence):** One-click accept. Minimal friction.
- **PARTIAL / NEEDS ATTENTION:** Evidence quote shown inline. EM can accept, override with annotation, or flag.
- **INCONCLUSIVE:** Mandatory review. Cannot be submitted without human resolution.
- **FAIL:** Specific gaps listed from LLM. EM sees exactly what's missing.

Audit trail: LLM verdict + human decision stored together. FEMA submission includes both.

**Stage 6 — Report & History**
Structured scorecard generated. Export to PDF for submission. Evaluation history stored: `{agency_id, plan_id, run_id, overall_score, run_date}` → enables "improved from 68% to 84% since last submission" trend view.

---

## 2B: HUMAN-IN-THE-LOOP — DESIGN PHILOSOPHY
> **EM1's core product philosophy. He will ask this in some form.**

The distinction: **tasks where AI can be the final decision-maker** vs. **tasks where AI should accelerate a human decision.** Crosswalk evaluation is firmly the second category.

A FEMA compliance verdict requires contextual judgment — the agency's local hazard profile, FEMA's current assessment priorities, the jurisdiction's history. The LLM has none of that. It has the document and the guideline text.

**The right division of labor:**
- LLM does: read 2000 pages, match 111 guidelines, extract evidence quotes, flag gaps. Days of work done in minutes.
- Human does: decide whether the evidence is sufficient for this agency's specific situation. That judgment cannot be automated.

**The system enforces this:**
1. `INCONCLUSIVE` cannot be submitted without human resolution — no bypass
2. Evidence quotes are verbatim, not paraphrased — human can verify in 5 seconds
3. Human overrides stored alongside LLM verdicts — full audit trail
4. Confidence scores surface low-confidence PASS verdicts — the system is honest about uncertainty

**How it evolves over time:** As the system accumulates history of LLM verdicts that match human decisions for stable plan sections, high-confidence PASSes on unchanged sections become one-click approvals. The loop gets shorter for routine cases. Human is still in the loop — just less friction.

**The Samay parallel:** The automated control testing system generated evidence and score; the compliance auditor reviewed and signed off. The LLM is a first reviewer, not the final one. Same principle.

---

## 2C: RETRIEVAL FROM LARGE DOCUMENTS
> **2000-page plans + 111 guidelines = retrieval precision is everything.**

Three problems with naive token chunking on a 2000-page plan:
1. **Context loss** — a chunk has no idea it came from "Section 4: Resource Management"
2. **Citation imprecision** — "somewhere in the plan" is useless; "Page 91, Section 4.2" is what Smart References needs
3. **Retrieval noise** — top-5 chunks by pure vector similarity may be from totally different sections

**How to handle it:**

**Structure-aware parsing first.** Extract section map before embedding: section number → heading → page range. This is the load-bearing step. At Samay I faced this with multi-format policy docs (docx, PDF, RTF) — metadata preservation during ingestion matters more than the chunking strategy itself.

**Two-level indexing.** Section summaries (~500 tokens) for coarse navigation. Paragraph chunks (~150-200 tokens with overlap) for precision. Both indexed.

**Hierarchical retrieval.** For each guideline: query section summaries → find the 2-3 most relevant sections → retrieve paragraph chunks from within those sections only. Same principle as a book index — find the chapter, then find the paragraph.

**Contextual chunk enrichment.** Every chunk carries full provenance: `{doc_title, version, section, heading, page, paragraph_index}`. LLM receives this metadata alongside the text. The Smart References citation is assembled from the metadata — not extracted from LLM output.

---

## 2D: DECONFLICT ARCHITECTURE
> **Cross-plan contradiction detection — a harder problem than it looks.**

Two sections can be semantically *similar* but logically *contradictory*: "The EOC is activated by the Director" and "The Deputy Director activates the EOC" are close embeddings that directly conflict. Vector similarity won't catch this.

**Three-phase approach:**

**Phase 1 — Topic clustering.** For all plans belonging to an agency, group sections by topic across plans: "all sections across EOP, HMP, and COOP that address EOC activation." This creates candidate groups for contradiction analysis without comparing every pair (which is O(n²) across a large corpus).

**Phase 2 — Pairwise LLM contradiction detection within clusters.** For each cluster: "Given these two sections from different plans, do they give conflicting guidance on the same subject?" Structured output: `{contradicts: bool, topic: str, plan_a_section: {...}, plan_b_section: {...}, conflict_description: str}`.

**Phase 3 — Conflict store.** `{agency_id, topic, plan_a_id, plan_a_section, plan_b_id, plan_b_section, conflict_description, status: open|resolved}`. This is the data model for the Deconflict UI — unresolved contradictions surfaced, resolved ones tracked.

**Where graph fits:** Model the corpus as a graph — sections as nodes, `addresses_same_topic_as` and `contradicts` as edges. Queries like "all unresolved contradictions involving EOC activation across active plans" become trivial traversals. This is the same pattern as the Samay identity graph — Neo4j is the right tool when the important queries are relationship traversals.

---

## 2E: AAR PIPELINE & REVIEW SKILL
> **AARs are part of E03 knowledge base + the upcoming agent skills direction.**

**What makes AARs architecturally different from plans:**
- Unstructured narrative (no fixed section schema like a compliant EOP)
- Incident-typed — a wildfire AAR is relevant to wildfire planners, irrelevant for active shooter
- Lessons-first — the valuable content is "what we learned / what we'd do differently"
- Cross-shareable (with consent) — other agencies' AARs are valuable learning material

**Ingestion pipeline:** Upload → S3 → structure-aware parsing (look for section markers: "Lessons Learned," "Recommendations," "What Worked," "What Didn't Work") → chunk + embed → knowledge base.

**Key metadata difference from plans:** Every AAR chunk tagged with `incident_type` (extracted by a classification LLM call or selected at upload), `section_type` (lessons_learned | recommendations | timeline | other), `incident_date`, `source_agency_id`. Without incident tagging, retrieval is noisy across all incident types.

**Two retrieval use cases:**
1. E03 Chat: "What have agencies learned from active shooter responses?" → filter `incident_type: active_shooter`, `section_type: lessons_learned` → retrieve top-k
2. Plan improvement workflow: after a crosswalk flags PARTIAL on EOC activation, surface AARs from similar agencies who had the same gap and how they resolved it

**The AAR review skill (stateful LangGraph agent):** When an agency finishes an incident and needs to write their AAR, the agent guides them through it step by step — timeline collection (structured form), what worked, what didn't, recommendations. Each step retrieves relevant peer AARs as examples. Final step: draft generation from the structured inputs. State persists across sessions — the user can stop and resume. This is a stateful multi-step workflow agent, not a Q&A agent.

**Cross-sharing governance:** Explicit consent flag per document: `{is_shared: bool, anonymize_agency: bool, shared_incident_types: [...]}`. Agencies opt in per AAR.

---

## 2F: AGENT SKILLS ARCHITECTURE
> **New product direction: E03 evolves from Q&A to guided multi-step workflows.**

**The shift:** From reactive stateless Q&A (user asks, agent answers) to **stateful conversation with a workflow graph** (agent guides user through a structured process with memory across turns).

**Four components:**

**State schema.** Each skill has a state object persisting across the conversation: where the user is, what's been collected, what's still needed. For plan creation: `{current_section: "hazard_identification", completed_sections: [...], draft_content: {...}, gaps: [...]}`. State lives in the session (PostgreSQL), not in the context window.

**Workflow graph.** Each skill is a directed graph of steps. Nodes = stages (gather jurisdiction info, identify hazards, draft mitigation actions). Edges = transitions triggered by user response or tool result. LangGraph provides this natively — I built LangGraph-based agentic workflows at Epik for security triage pipelines with branching logic. Same pattern.

**Scoped tool access per step.** At each node, the agent has access to only the tools relevant to that step. For "hazard identification": retrieve peer agency hazard sections from library, query FEMA doctrine for that hazard type, check agency's existing plan. Not all tools — just the relevant ones. Keeps the agent focused and reduces noise.

**Persistence and resumability.** A plan creation workflow is not done in one session. State persisted to PostgreSQL keyed on `(agency_id, skill_type, workflow_instance_id)`. User returns → load state → resume.

**Build order:** Start with the simplest possible skill — single-step, no branching, no resumability. Prove the pattern end-to-end. Then add persistence, then multi-step, then branching. The ugly single-step version first is the same discipline as Samay — ugly scripts before architecture.


---

# PART 3 — TECHNICAL DEEP-DIVES
> **Study Tuesday AM. Be ready to go narrow and deep on any of these.**

---

## 3A: GRAPH-RAG — THE 1-MINUTE ANSWER
> *They'll say "Graph-RAG" — be able to position it without overselling.*

**The honest take:** Graph-RAG is a specific solution to a specific problem — answering questions that require multi-hop relationship traversal across documents. For the main E01 crosswalk (one plan, 111 guidelines), it is **overkill**. Dense vector retrieval on well-structured chunks is faster, cheaper, and simpler.

**Where it actually earns its cost:**
1. "Which other agencies in our region have mitigation strategies that address our highest-risk hazards?" — cross-agency, cross-hazard, cross-section traversal. That's a graph query.
2. Deconflict cross-reference graph — sections as nodes, contradiction/alignment as edges, queries like "all unresolved contradictions involving EOC activation"
3. Doctrine dependency chains — "this guideline references that standard which requires this other certification" — that is a graph by definition

**Decision rule (what I applied at Samay):** If the critical queries are "find the most semantically similar content to this text" → vector. If the critical queries are "traverse relationships between named entities across documents" → graph. If the system needs both → dual store with explicit routing at query time.

**What I'd propose for EM1:** Vector (pgvector) as the primary retrieval layer for all single-plan queries. Knowledge graph (lightweight, possibly in PostgreSQL itself as an adjacency model) for cross-plan deconflict and inter-agency queries. Add Neo4j when the cross-document relationship traversal earns its operational overhead.

---

## 3B: ASYNC JOB ARCHITECTURE
> *They'll want to understand how you handle long-running operations. This is the design.*

**Why async is mandatory:** At 111 LLM calls × 1-3 seconds each → 2-5 minutes per evaluation. A synchronous HTTP request will time out. The only right answer is async + polling/webhook.

**The pattern:**

1. `POST /evaluations` — validates input, writes job record with status `QUEUED`, publishes to SQS, returns `{job_id, status: "QUEUED"}` immediately. HTTP response is fast (< 200ms).

2. SQS queue → ECS worker picks up job. Worker updates status `PROCESSING`, runs the evaluation loop, writes results per guideline, updates progress counter (`progress_counter` column, incremented after each guideline completion).

3. Client polls `GET /evaluations/{job_id}` every 5 seconds: status + `{completed: 45, total: 111}` — progress bar is live. Or: webhook callback registered at job creation.

4. Worker completes → status `COMPLETED`, final report written. Or `FAILED` with `error_message`.

**Schema:**
```
evaluation_jobs(id, agency_id, plan_id, guideline_set_id, status, progress_counter, total_guidelines, created_at, completed_at, error_message)
evaluation_results(id, job_id, guideline_id, verdict, evidence_quote, page_reference, gaps, cached_from_job_id)
```

**Idempotency:** Unique constraint on `(agency_id, plan_file_hash, guideline_set_id)`. If the same plan+guidelines are submitted again, return the existing job_id, don't requeue.

**Cache hit logic:** Before running a guideline, check if `(guideline_id, chunk_hash)` has a result from a prior run. If yes — copy result with `cached_from_job_id` reference. Skip the LLM call. Repeat evaluations can be 60-70% cheaper.

---

## 3C: SCALABILITY + LLM COST
> *The 111 × 60 = 6,600 call math. He knows the numbers — show you do too.*

**Current scale:** 111 guidelines × 60 agencies = 6,600 LLM calls per full evaluation cycle. If agencies run evaluations monthly: 6,600/month. At 10x growth: ~66,000/month.

**Cost breakdown (rough):**
- GPT-4o at ~$5/1M output tokens, ~1,000 tokens output per call → ~$0.005/call
- 111 calls × $0.005 = $0.55 per evaluation. Fine at 60 agencies. Fine at 600 agencies ($330/month).
- The cost problem isn't the per-evaluation price — it's inefficiency from re-running unchanged plan sections.

**Three levers:**

**Lever 1 — Result caching (biggest win).** Key: `{guideline_id, chunk_hash}`. If plan section hasn't changed since last evaluation, cache hit, skip LLM. Plans are mostly stable — an agency might update 10-15% of sections between evaluations. Caching can eliminate 60-80% of calls on re-evaluations.

**Lever 2 — Model tiering.** Not all 111 guidelines need GPT-4o reasoning. Simple structural checks ("Does the plan have a resource management section?") → fast, cheap model (GPT-4o-mini, Haiku). Complex judgment calls ("Is the mitigation strategy adequately specific?") → full model. Route at inference time. Rough split: 30-40% of guidelines are structural → 35% cost reduction with no quality loss.

**Lever 3 — Hierarchical retrieval reduces tokens.** Better retrieval = smaller, more precise context = fewer tokens in = lower cost. Every improvement to retrieval precision has a direct cost payoff.

**The architecture implication:** Cost at scale is mostly a retrieval quality problem and a caching problem, not a model size problem.

---

## 3D: HALLUCINATION PREVENTION
> *EM1 is a domain where wrong answers have real stakes. This matters.*

**The risk:** LLM returns `verdict: PASS` with a plausible-sounding evidence quote that doesn't actually exist in the plan. Agency submits to FEMA. FEMA assessment fails.

**Four-layer defense:**

**Layer 1 — Evidence gating (the core constraint).** Pydantic output schema requires `evidence_quote: str`. Post-processing: verify the quote exists verbatim in the retrieved context. If not: force `verdict = INCONCLUSIVE`. The LLM **cannot** hallucinate a PASS — missing evidence means the system doesn't have enough confidence to emit a verdict. This is the same pattern I built at Samay: no quote → no PASS verdict.

**Layer 2 — Quote-then-reason prompting.** Prompt structure: "First, copy the exact sentence from the context that addresses this guideline. Then, based solely on that sentence, assign a verdict." Forces the LLM to ground in source material before reasoning. Reduces confabulation significantly vs. open-ended prompts.

**Layer 3 — Post-processing reconciliation.** Pipeline step after LLM response: check evidence quote exists in chunks, check page reference exists in doc metadata, check no verdict contradicts the evidence quote. Flag inconsistencies for mandatory review. This catches cases where the LLM is inconsistent with itself.

**Layer 4 — Eval harness.** Golden test set: 20-30 known evaluations (manual expert assessments) checked against the pipeline nightly. Track precision by guideline type, precision by doc structure complexity. I built this at Epik with Langfuse — the infra is straightforward, the discipline is making sure the golden set stays current. If evaluation quality drifts, you catch it before a customer does.

---

## 3E: MULTI-TENANT ARCHITECTURE
> *60+ agencies. Each one's data cannot leak to another.*

**Three layers of isolation:**

**Layer 1 — Request-level.** JWT contains `agency_id`. API middleware extracts it, validates it against the session, sets it in request context. Every downstream call to the database or vector store receives `agency_id` explicitly. No request can operate on data without an `agency_id` in its context.

**Layer 2 — Database-level (PostgreSQL).** `agency_id` foreign key on every data table. Row-level security policies: `CREATE POLICY tenant_isolation ON evaluation_jobs USING (agency_id = current_setting('app.current_agency_id')::UUID)`. Even if application code has a bug and forgets to filter, the database enforces it.

**Layer 3 — Vector store namespace isolation.** pgvector: filter condition `agency_id = $1` on every retrieval query. If using Pinecone: namespace per agency. No cross-tenant vector retrieval is structurally possible at the query layer.

**Guideline store multi-tenancy:** System guidelines (`agency_id IS NULL`) are shared read-only. Agency custom guidelines have `agency_id` set. Retrieval query: `WHERE agency_id = $1 OR agency_id IS NULL`. Agencies cannot read each other's custom guidelines.

**The Samay parallel:** Per-tenant S3 buckets, per-tenant Neo4j databases, per-tenant RDS schema. The model was total physical isolation. For EM1 at this scale, logical isolation (RLS + namespace filtering) is the right tradeoff — lower cost, same security properties when implemented correctly.

---

## 3F: POSTGRESQL SCHEMA + PGVECTOR
> *The core data store. Be ready for schema-level questions.*

**Core tables:**
```
agencies(id, name, state, plan_count, created_at)
plans(id, agency_id, type[EOP|HMP|COOP|IAP|AAR], version, file_hash, s3_key, ingested_at)
plan_sections(id, plan_id, section_number, heading, page_start, page_end)
plan_chunks(id, plan_id, section_id, text, chunk_index, embedding vector(1536), page)
guidelines(id, agency_id NULLABLE, title, text, source, category)
evaluation_jobs(id, agency_id, plan_id, guideline_set_id, status, progress_counter, total_guidelines, ...)
evaluation_results(id, job_id, guideline_id, verdict, evidence_quote, page_reference, gaps, cached_from_job_id)
```

**Indexes that matter:**
- `CREATE INDEX ON plan_chunks USING ivfflat (embedding vector_cosine_ops)` — ANN index for pgvector
- `CREATE INDEX ON plan_chunks (plan_id, section_id)` — hierarchical retrieval by section
- `CREATE INDEX ON evaluation_results (job_id, guideline_id)` — fast job result aggregation
- `CREATE INDEX ON evaluation_jobs (agency_id, status)` — dashboard queries per agency

**pgvector vs Pinecone decision:** pgvector when: data is already in PostgreSQL, retrieval needs joins with structured metadata (e.g., filter by `plan_id` AND `section_id`), scale doesn't require horizontal vector scaling. Pinecone when: retrieval is pure semantic similarity at millions of vectors with no join requirements, latency SLA is < 10ms. For EM1 at current scale: pgvector is the right call — one less operational system, metadata joins come for free.

---

## 3G: TESTING + OBSERVABILITY
> *How you'd keep the AI pipeline honest in production.*

**Two categories of tests:**

**Deterministic tests (straightforward):** API contract tests, schema validation (does the Pydantic model parse?), business logic (does the result cache logic correctly skip LLM when chunk_hash matches?), idempotency (double-submit returns existing job_id). These are unit/integration tests, fast, run in CI.

**AI behavior tests (different problem):** The LLM output is probabilistic. Standard unit tests cannot assert exact outputs. The right approach:

1. **Schema contract tests:** Does the response always have `verdict`, `evidence_quote`, `page_reference`? These pass/fail deterministically even though the content is probabilistic.
2. **Golden set evaluation:** 20-30 labeled examples (guideline + plan section + expected verdict). Run nightly. Track `precision@k` and `recall@k` per guideline category. Not pass/fail — drift detection.
3. **Tracing + span logging:** Every LLM call gets a `run_id`. Log: input prompt hash, retrieved chunk IDs, model version, latency, token counts, output schema validation result. This is what Langfuse or LangSmith provides — I built this at Epik. When a user files a bug on a specific evaluation, you can replay the exact run.

**Monitoring in production:**
- `INCONCLUSIVE` rate per guideline: sudden spike = retrieval quality problem or guideline text change
- Cache hit rate: dropping cache hits = plans changing more than expected, or cache key logic broken
- p99 latency per evaluation: early warning of slow workers or SQS queue backup
- Evidence quote verification failure rate: leading indicator of hallucination pressure


---

# PART 4 — STACK-SPECIFIC
> **Study Tuesday PM. EM1 is TypeScript/Next.js/Terraform — be confident, not defensive.**

---

## 4A: TYPESCRIPT DEPTH
> *They will probe whether you actually write TypeScript or just "use" it.*

**The foundation is solid:** TypeScript is the language of every modern frontend I've built — React UIs at Samay, Epik, TrustX. The discipline I care about:

**Shared domain types.** Define once, use everywhere. For EM1:
```typescript
// Defined in @em1/types, imported by API handler, database layer, and UI component
type EvaluationVerdict = 'PASS' | 'PARTIAL' | 'FAIL' | 'INCONCLUSIVE';

interface EvaluationResult {
  guidelineId: string;
  verdict: EvaluationVerdict;
  evidenceQuote: string;         // never undefined — required by schema
  pageReference: string;
  gaps: string[];
  cachedFromJobId: string | null;
}
```
If the LLM response doesn't match `EvaluationResult`, the Zod parse throws before it reaches any business logic.

**Discriminated unions for job status:** Instead of `status: string`, use:
```typescript
type EvaluationJob =
  | { status: 'QUEUED'; queuedAt: Date }
  | { status: 'PROCESSING'; startedAt: Date; progress: number; total: number }
  | { status: 'COMPLETED'; completedAt: Date; resultId: string }
  | { status: 'FAILED'; failedAt: Date; error: string };
```
The UI component that renders status can exhaustively switch — TypeScript will warn if you add a new status and forget to handle it.

**Zod for LLM response parsing.** The boundary where TypeScript type safety is most important is exactly where you have the least control — the LLM response. Parse it with Zod at the edge:
```typescript
const EvaluationResultSchema = z.object({
  verdict: z.enum(['PASS', 'PARTIAL', 'FAIL', 'INCONCLUSIVE']),
  evidence_quote: z.string().min(1),
  page_reference: z.string(),
  gaps: z.array(z.string()),
});
// If this throws, the pipeline writes INCONCLUSIVE — no untyped data downstream
const parsed = EvaluationResultSchema.parse(llmResponse);
```

**RSC boundary consideration in Next.js App Router.** Server Components cannot pass non-serializable objects to Client Components as props. When designing the eval results page: fetch data in a Server Component, serialize to primitives (not class instances), pass as props. This is the main footgun in RSC — you hit it once and understand the model immediately.

**Ramp timeline:** The App Router mental model is a 2-3 day adjustment for a React developer. The type fundamentals (union types, generics, Zod patterns) are already there from Samay + Epik. Contributing productively within a week.

---

## 4B: TERRAFORM vs. CDK — HONEST POSITIONING
> *Gunnar will likely probe this. Don't oversell. He's worked at real infra companies.*

**What I've actually built:**
- AWS CDK (TypeScript): 15+ stacks at Samay — VPC, ECS, Lambda, RDS PostgreSQL, Neo4j on EC2, S3, Secrets Manager, Step Functions, AppRunner. Wrote, deployed, debugged.
- Terraform: Used for Azure infrastructure at Samay (AKS, managed Postgres, storage). Worked in an existing Terraform codebase, added resources, understood provider patterns.

**The honest positioning:** CDK is production depth, Terraform is working proficiency. The discipline is the same — both are infra-as-code with state management, both require understanding provider APIs and how changes are planned before applied. The syntax difference is real but not the hard part; understanding AWS resource relationships is the hard part, and that's what I have.

**For EM1's stack:** If EM1 uses Terraform, I'm contributing to existing modules within a sprint. If there are new modules to write, I'd be referencing provider docs alongside Gunnar the first time — that's honest. What I'd bring is the CDK depth that maps directly: I've debugged circular dependency errors between stacks, written custom constructs, handled secret injection to Lambda from Secrets Manager, done blue/green deploys with CodePipeline.

**The answer to "have you used Terraform?" is yes, not no. The answer to "Terraform depth = CDK depth?" is no — and that honesty builds more trust than overclaiming.**

---

## 4C: NEXT.JS APP ROUTER
> *Be specific. Not "I know React" — know the App Router model.*

**The App Router shift:** The main conceptual change from Pages Router is the server/client boundary. Components are Server Components by default — they run on the server, have direct access to the database/secrets, don't ship JavaScript to the client. Client Components are explicitly opted in with `'use client'`.

**What this means for EM1's UI:**
- The evaluation results page: Server Component fetches the job and results from the database directly (no API route needed), renders the list, passes serialized data to a Client Component that handles expand/collapse interactions.
- The intake form: Client Component (interactive), but form submission goes to a Server Action or API route.
- The progress polling during evaluation: Client Component with `useState` + `useEffect` for the polling interval, or Server-Sent Events.

**RSC mental model:** Think of the component tree as a waterfall — Server Components at the top (data fetching, layout, no interactivity), Client Components at the leaves (buttons, forms, real-time updates). The mistake people make is adding `'use client'` to everything — that defeats the purpose.

**Where I am:** React is deep, TypeScript is deep, the RSC mental model is the 2-3 day ramp. I've read the App Router docs and the RSC RFC. The honest answer is: I'd be confident with the patterns within a week of first commit.

---

## 4D: FULL-STACK SHIPPING STORY
> *A concrete example of owning a feature end-to-end. Use this when they ask about scope of ownership.*

**The story (TrustX at Samay):**

The compliance team needed a "Test Control" button in the React dashboard — click it, and the system runs the automated evidence collection and LLM evaluation for a single control, showing the result in real-time. The scope of that one button:

1. **React UI:** New button component in the controls dashboard. Loading state, error state, result display (verdict badge, evidence quote, confidence score).
2. **API layer (Flask/Python):** `POST /controls/{id}/test` endpoint. Validates the control exists and belongs to the tenant. Publishes to the job queue. Returns job_id.
3. **Worker logic (Lambda):** Pulled evidence from 6 sources (GitHub, Jira, AWS Config, Confluence, Slack, file uploads). Assembled context. Called Bedrock (Llama 3.3 70B) with Pydantic output schema. Wrote result to RDS.
4. **Infrastructure (CDK):** New SQS queue for on-demand test jobs (separate from the nightly batch queue). Lambda trigger. IAM permissions. Secret mounting for the 6 source integrations.

All four layers in one sprint. No handoffs — I wrote the React, the Flask endpoint, the Lambda, and the CDK stack. That's what "full-stack ownership" means in practice, not just "I've done frontend and backend."


---

# PART 5 — BEHAVIORAL & CULTURE
> **Study Tuesday PM — out loud. Practice the stories, don't just read them.**
> Format: STAR (Situation, Task, Action, Result). Max 2 minutes per story.

---

## 5A: OWNERSHIP — SOLO FOUNDING ENGINEER
> *"Tell me about a time you owned something end-to-end."*

**S/T:** At Samay I was hired as the sole engineer to build TrustX — a compliance automation SaaS. No existing codebase, no architecture, no other engineers. The founders had a product vision and customers lined up. Everything from infrastructure to UI was my decision and my responsibility.

**A:** I started with the ugliest version that could demonstrate the value — manual evidence collection scripts, hard-coded output, no UI. Showed it to the first customer. They got it. Then I built infrastructure: 15+ CDK stacks, per-tenant S3/RDS/Neo4j isolation, Lambda suite for evidence collection. Then the AI layer: Bedrock integration, Pydantic output schema, evidence-gating logic. Then the React dashboard. Shipped to 3 customers.

**R:** Three paying B2B customers on a platform I designed and built alone. Every architectural decision — multi-tenant isolation model, async job pattern, graph DB for identity relationships — was mine to make and mine to defend. That's the context I work best in.

**Bridge:** "That's the context I'm looking for at EM1 — small team, big ownership, high-stakes domain where the engineering decisions matter."

---

## 5B: WORKING WITH DOMAIN EXPERTS (EM OPERATORS)
> *"How do you work with non-technical stakeholders?"*

**The principle:** Before writing a line of code, watch the person doing the work manually. The first week on a new domain I am an observer, not a builder.

**S/T:** At Samay, the compliance auditor (the domain expert) was manually running the compliance checks: reading through control frameworks, cross-referencing AWS Config output, writing assessment summaries in Word. She knew every edge case, every ambiguity, every place the framework language was vague. I didn't.

**A:** I shadowed her for two full sessions before designing anything. I asked: "Which step takes the longest?" (Reading evidence from 6 sources). "Where do you still have to use judgment?" (Is this GitHub commit actually evidence for this control, or just adjacent?). "What would you never trust a tool to decide without reviewing?" (Any PASS verdict on a high-risk control). Those three answers shaped the architecture: automate the multi-source collection, preserve judgment on verdicts, make INCONCLUSIVE mandatory review.

**R:** The final system matched her mental model — she trusted it because it didn't try to replace her judgment, it accelerated her review. She signed off on PASS verdicts for routine controls in 30 seconds instead of 10 minutes.

**For EM operators:** Same principle. Before designing the intake form or the review UI, I'd want to watch an EM coordinator run a FEMA evaluation manually. What's tedious? What requires contextual judgment they'd never delegate? The answers drive the design.

---

## 5C: MENTORING JUNIOR ENGINEERS
> *"How do you work with early-career engineers?"*

**Two examples:**

**OSU (GTA):** Taught discrete math and mobile app development. The gap between "understanding the concept yourself" and "teaching it clearly" is large. I learned to give students the smallest working example first, then generalize — not the theorem, then the example. Same approach in code reviews.

**Zemoso:** A junior engineer was struggling with test coverage — writing tests that tested implementation rather than behavior, tests that broke whenever internals changed. Instead of flagging it in review comments, I wrote one example test alongside his code: same feature, behavior-focused, no knowledge of internals. Showed the difference in a 20-minute pairing session. Coverage improved. He understood the principle, not just the fix.

**The pattern I follow:**
- Code reviews that explain the "why" behind the feedback, not just "change this to that"
- One pairing session beats five rounds of async review comments
- Never fix a junior's bug for them unless time is genuinely critical — walk through the debugging process together
- Pick up coverage for things they're struggling with quietly — don't let it become a pressure issue, just get the team unblocked

**For EM1's 2 early-career engineers:** First thing I'd do is understand what they're working on and where they feel uncertain. Then invest in the pairing, not the code review.

---

## 5D: HARD ARCHITECTURAL DECISION
> *"Tell me about a difficult technical decision you made."*

**S/T:** At Samay, I needed to decide whether to use Neo4j (graph database) or extend PostgreSQL for the identity relationship graph — the system that tracked multi-hop relationships between users, roles, permissions, and AWS resources across multi-tenant compliance evidence.

**A:** The case for PostgreSQL: already in the stack, team knows it, one less operational system. The case for Neo4j: the queries I needed were 4-6 hop traversals ("find all AWS resources accessible by this user through role chains, across accounts, given this permission delegation"). I wrote both implementations for the simplest version of the query. The PostgreSQL recursive CTE was correct but took 800ms. The Neo4j traversal was 20ms.

**R:** Used Neo4j for the identity graph layer only. PostgreSQL for everything else. Per-tenant Neo4j databases for isolation. Added operational complexity — I had to learn Neo4j deployment, backup, the Cypher query language. The first two weeks were slower. But the query performance was non-negotiable for the use case.

**What I'd say to Gunnar:** "I don't add architectural complexity unless I've seen the simple version fail. I added Neo4j after writing the PostgreSQL version and seeing it wasn't fast enough. That's the order to approach it."

---

## 5E: MOTIVATION — WHY EM1, WHY NOW
> *"Why are you interested in this role?"*

Three honest reasons:

**1. The problem has real stakes.** At Samay, I built compliance automation for SOC2/NIST frameworks — the same pattern as FEMA crosswalk evaluation. What drew me there was that a wrong answer had real consequences: a company gets a compliance finding, a customer's data protection is incomplete. EM1 raises the stakes further — a plan with an unaddressed gap in an actual disaster has different consequences. That matters to me as an engineer. I want the work to matter.

**2. The architecture is the right level of hard.** RAG on 2000-page documents with citation accountability, multi-tenant isolation, async job pipelines, agent skills — this is the class of problems I've been solving for two years. It's not trivially easy (interesting) and it's not research (achievable). It's applied AI engineering with clear production requirements.

**3. Small team, full ownership.** I've worked in large microservices teams (Zemoso) where my scope was one service out of twelve. I've worked solo (Samay). I strongly prefer the solo/small-team context — decisions are faster, ownership is clearer, the engineering judgment that matters is yours. A 4-engineer team where each person has real scope is the right environment for the kind of engineering I want to do.

---

## 5F: PRODUCTION FAILURE STORY
> *"Tell me about a time something broke in production."*

**S/T:** At Epik, we had a multi-stage data preprocessing pipeline for AI agent training data. One stage used Spark for distributed processing. In production, Spark was silently dropping records that failed schema validation — not raising an error, just filtering them out. We didn't know until a downstream model evaluation showed degraded performance on edge case inputs.

**A:** Diagnosed by adding a reconciliation check at the end of the pipeline: count records in → count records out → alert if out < in × 0.99. Found the drop immediately. Then traced: Spark's default behavior on malformed records in a DataFrame is to drop and continue, not fail. Added explicit schema enforcement at the read step with `mode='FAILFAST'` — fail loudly if any record doesn't match the schema. Also added logging of the error records to a dead-letter S3 prefix so nothing is silently lost.

**R:** The silent drop had been running for 3 sprints. The reconciliation check caught it permanently going forward. The lesson: in data pipelines, "it ran without errors" is not the same as "it ran correctly." You need explicit output validation, not just absence of exceptions.

**Bridge to EM1:** The INCONCLUSIVE verdict + mandatory review is the same principle. Don't let the system silently fail into a wrong answer. Make the failure loud and require a human to handle it.

---

## 5G: CHANGING REQUIREMENTS
> *"Tell me about a time requirements changed mid-project."*

**S/T:** At Samay, the initial spec for TrustX was to track controls against SOC2 only. Three weeks into development, the customer asked if we could also support NIST 800-53. Different framework, different control numbering system, different evidence categories.

**A:** The original design had the control framework baked in — hardcoded SOC2 categories, hardcoded control IDs in the schema. Extending to NIST would have required schema migration and code changes in 12 places. I stopped, reviewed the schema, and extracted the framework as a first-class entity: `frameworks(id, name, version)`, `controls(id, framework_id, control_number, title, description)`. Two days of refactoring. Then adding NIST was a data import, not a code change.

**R:** SOC2 + NIST shipped two weeks after the pivot. ISO 27001 was added the following month with zero code changes — just data. The pivot to a framework-agnostic model was the right call, and the two-day investment paid back within the same month.

**Bridge:** This maps directly to EM1's custom evaluation feature — agencies build their own guideline libraries. Same design: guidelines as a first-class entity, not hardcoded to FEMA. The architecture was correct because requirements changed and we'd anticipated that.

---

## 5H: DOMAIN ONBOARDING (NEW DOMAIN)
> *"How do you get up to speed on a new domain?"*

**The process:**
1. Watch the person doing the work manually. Not "explain the domain to me" — sit with them while they do the actual task.
2. Build the ugliest possible version of the core workflow. Not the full product — the 30-minute script that demonstrates value. Breaking it is how you learn where the real complexity lives.
3. Talk to the customers directly, early. Not feature requests — "what's the worst part of your current process?" The answer to that is the product.

**Emergency management specifically:** I've spent serious time on EM1's public docs and the FEMA National Preparedness Goal since the first-round conversation. The planning cycle (EOP → HMP → COOP → AAR), the FEMA assessment process, the doctrine hierarchy — these are the vocabulary I'd need to be useful. The gap is I haven't worked with EM coordinators directly. The first thing I'd want to do after joining is shadow one evaluation review session — watch a coordinator actually go through a FEMA assessment, see where the friction is, understand what "good enough" means in practice for this domain.


---

# PART 6 — QUICK-FIRE ANSWERS
> **Wednesday morning only. Short, confident, no rambling.**

---

**Q: How do you know when something is done?**
> "Deployed, monitored for one business day, and the person who asked for it has used it and confirmed it solves the problem. Not 'the PR is merged' — the thing actually works."

**Q: How do you think about technical debt?**
> "There's debt that costs a little now and a lot later — I don't take that on. There's debt that costs a little now and a predictable, manageable amount later — that's called a trade-off, and it's fine. The 'ugly scripts before architecture' principle I used at Samay: build the prototype that proves the value, then build it properly when you know the shape of the problem."

**Q: What makes a good API?**
> "It doesn't surprise you. The resource model is consistent, the error responses are structured and actionable, the async operations return job IDs with a status polling contract. The test for a good API is: can a developer integrate against it using only the response bodies, without reading docs?"

**Q: Tell me about a time you pushed back on a technical decision.**
> "At Monarch Tractor, the team wanted to use Workato (a third-party integration platform) for the HR system sync — UKG to JumpCloud to Azure AD. My pushback: Workato added $20K/year in licensing, required a vendor dependency for infrastructure that was core to employee onboarding, and the same workflow was straightforward AWS Lambda + EventBridge for pennies. I built a working proof-of-concept over a weekend. That became the production system. The pushback wasn't 'this is wrong' — it was 'here's the alternative, let me show you.' Evidence, not opinion."

**Q: When do you ship fast vs. when do you slow down?**
> "Fast: prototypes that prove the concept, internal tools, features with an obvious rollback path. Slow: anything that handles multi-tenant data isolation, anything that writes to customer records in production, anything that touches auth or permissions. The rule: if a bug here means a customer sees another customer's data, or a compliance report is wrong, that gets extra review. If a bug here means a UI element is in the wrong color, ship it and fix it."

---

# PART 7 — CLOSE OUT
> **Read Wednesday morning after Part 0. Then close the doc.**

---

## 7A: QUESTIONS TO ASK GUNNAR (pick 3, not all 5)

> Always ask about the technical work first — shows you care about the problems, not just the role.

1. **Technical / product:**
   > "The crosswalk — how are you chunking the plans right now? Structurally by section or by token count? I'd expect section-aware parsing to be the hard part for citation precision."

2. **Technical / future:**
   > "For Deconflict — are you doing the cross-document contradiction detection today, or is that upcoming? Curious whether you're modeling it as a graph problem internally."

3. **Team / growth:**
   > "The 2 early-career engineers — how do you think about the mentoring dynamic in a team this small? I want to understand what being genuinely helpful to them looks like from day one."

4. **Engineering culture:**
   > "Coming from OpenSesame and Olo — what engineering habits or standards from those places are you deliberately bringing to EM1? And what are you intentionally leaving behind?"

5. **Ownership / trajectory:**
   > "If I joined and was fully up to speed in 60 days — what would you want me to own that you don't have enough bandwidth for right now?"

---

## 7B: OPENING LINE (say this in the first 90 seconds)
> "I'm Neel — six years full-stack, last two deep in AI systems. The most relevant thing I've built is TrustX at Samay — compliance automation platform where the core was: collect evidence from multiple sources, assemble grounded context, run LLM evaluation with citation enforcement. When you describe the Evaluate module — automated FEMA crosswalk, Smart References — that's the same architecture in a different domain. Looking forward to getting into the specifics."

## 7C: CLOSING LINE
> "This has been exactly the kind of technical conversation I was hoping for. What you're building — grounded AI with citation accountability in a domain where wrong answers have real stakes — is the problem I care about. I'd love to keep moving forward."

---

## 7D: STUDY SCHEDULE (2 days)

| Day | Focus | Goal |
|---|---|---|
| **Monday** | Parts 1 + 2 | Know the company cold. Know the E2E flow and human-in-the-loop philosophy cold. |
| **Tuesday AM** | Part 3 | Be ready for technical deep-dives on retrieval, async jobs, hallucination, multi-tenant |
| **Tuesday PM** | Parts 4 + 5 | TypeScript/Terraform honest positioning. Practice behavioral stories out loud. |
| **Wednesday AM** | Part 0 only | Cheat sheet. One read. Then close the doc. |

---

## 7E: ENERGY + MINDSET

**The tone that works with Gunnar:** He's a CTO who came from high-scale engineering orgs. He respects precision and dislikes vagueness. The right register is: confident, specific, honest about gaps, curious about their problems.

**When you don't know something:** Don't bluff. The right answer is: "I haven't worked with that specific tool directly, but here's how I'd think through it..." or "I know the adjacent thing — let me trace how it maps." He knows what he's hiring; he's not looking for encyclopedic knowledge, he's looking for engineering judgment.

**The numbers rule:** When you can use a number, use it. "~111 guidelines", "500-2000 pages", "60+ agencies", "4-engineer team." Numbers signal you did the homework.

**The bridge rule:** At the end of every technical answer, connect to a specific thing you built. Not "I understand this pattern" — "I built this pattern at Samay, here's what it looked like."

**On Terraform/Next.js gaps:** Acknowledge them cleanly, don't over-explain. "CDK is deep, Terraform is working proficiency — contributing within a sprint" is better than three sentences justifying why that's okay. Say it once, move on.

---

## 7F: LOGISTICS

- **Format:** 60-90 min conversation. Likely technical architecture first, then behavioral, then questions. May overlap throughout.
- **Prep done by:** Monday (Parts 1-2), Tuesday (Parts 3-5), Wednesday AM (Part 0 only)
- **The old doc:** `Round2_Interview_Prep.md` — 588 lines, full reference. If you want to check a specific answer in more detail, it is there.

---

*Built: June 8, 2026 | Interview: June 10, 2026 | Role: Software Engineer, EM1*



> [!example]- Alternate source version (html)
> ## EM1 — Round 2 Interview Prep 
>
>  
>
> #### Gunnar Holwerda, CTO / Co-Founder | Wednesday June 10, 2026 | 60–90 min 
>
>    
>
> How to use this doc:
>
>   
> - Monday: Read Part 1 (company context) + Part 2 (system design). These are the highest-risk questions. Know them cold. 
> - Tuesday AM: Work through Part 3 (technical deep-dives) + Part 4 (stack-specific). 
> - Tuesday PM: Read Part 5 (behavioral) out loud — practice the stories, not just read them. 
> - Wednesday morning: Part 0 only (cheat sheet). Do not re-read the whole doc. Trust the prep.    
>
> ## PART 0 — DAY-OF CHEAT SHEET 
>
>   
>
> Wednesday morning. One read. Then close it.
>
>   
>
> ### Key Numbers (use these — they signal you did your homework) 
>
>   
> - 60+ agencies on the platform (state, county, city) 
> - 111 guidelines per standard FEMA HMP evaluation 
> - 500–2000 pages per emergency plan 
> - ~6,600 LLM calls/month at current scale (111 × 60) → ~66K at 10x 
> - 4 engineers including Gunnar (+ 2 early-career, data analyst, EM operators) 
> - 3 modules: E01 Evaluate, E02 Improve, E03 Operationalize/Chat 
> - Near-term focus: Vanta-style compliance module — replacing email/manual intake with self-serve form + automated async crosswalk  
>
> ### One-Line Answers (alignment table) 
>
>    
>
>   | What Gunnar Needs  | Your One-Liner 
>
>    
>
>   | "Vanta-style compliance module"  | "I built this at Samay — the mapping from SOC2 controls to FEMA guidelines is a configuration change, the architecture is identical" 
>
>  
>
>   | "Graph-RAG"  | "Right for multi-hop cross-doc queries; overkill for single-plan retrieval — I used Neo4j for exactly the use case where it earns its complexity" 
>
>  
>
>   | "Sentence-level citations"  | "That's the evidence-gating pattern — Pydantic schema forces a verbatim quote, no quote = INCONCLUSIVE, no hallucination path to PASS" 
>
>  
>
>   | "Human in the loop"  | "Automate the tedious, preserve the judgment — LLM does the 2000-page reading, human signs off on the verdict" 
>
>  
>
>   | "Full-stack ownership"  | "Not 'I own the backend' — CDK infrastructure, Lambda suite, API, and React UI. All of it, no handoffs" 
>
>  
>
>   | "Small team / 4 engineers"  | "Samay was effectively solo — I owned everything and prefer that context" 
>
>  
>
>   | "Mentor junior engineers"  | "OSU GTA for a year, code reviews that teach not just flag, picked up test coverage for a struggling junior without being asked" 
>
>  
>
>   | "Next.js"  | "React + TypeScript is the foundation — App Router, RSC model are the ramp. Productive in a week." 
>
>  
>
>   | "Terraform"  | "Deep CDK (same discipline, different syntax) + Azure Terraform at Samay. Contributing to existing codebase within a sprint." 
>
>    
>
> ### Opening Line 
>
>   
>
> "I'm Neel — six years full-stack, last two deep in AI systems. The most directly relevant work is TrustX at Samay — I was the sole engineer on a compliance automation platform. The core was: collect evidence from multiple sources, assemble grounded context, send to an LLM for a scored verdict with citations. When you describe the Evaluate module — automated FEMA crosswalk, Smart References — that's the same architecture in a different domain. I've been looking forward to this conversation."
>
>   
>
> ### Closing Line 
>
>   
>
> "This has been exactly the kind of technical conversation I was hoping for. What you're building — grounded AI with citation accountability in a domain where wrong answers have real stakes — is the problem I care about. I'd love to keep moving forward."
>
>   
>
> ### Questions to Ask (pick 3) 
>
>   
> - "The crosswalk — are you chunking plans structurally by section or by token count? I'd expect section-aware parsing to be the hard part for citation precision." 
> - "For Deconflict — are you doing cross-document contradiction detection today, or is that upcoming? Curious whether you're modelling it as a graph problem." 
> - "The 2 early-career engineers — how do you think about mentoring in a small team? I want to understand what supporting them well looks like." 
> - "Coming from OpenSesame and Olo — what engineering habits are you deliberately bringing to EM1, and what are you leaving behind?" 
> - "What's the biggest technical problem on the roadmap right now — something an engineer joining now would own end-to-end?"   
>
> ## PART 1 — KNOW THE COMPANY FIRST 
>
>   
>
> Read this before any answers. Context shapes everything.
>
>   
>
> ### What's Built vs. What You're Building 
>
>    
>
>   | Component  | Current State  | What Changes 
>
>    
>
>   | Core AI  | "Simple RAG" — indexes large EM PDFs, retrieves relevant passages  | Extend: better structural retrieval, cross-doc reasoning 
>
>  
>
>   | Document library  | Aggregates public plans + customer-contributed docs, cross-share between non-competing agencies  | Improve cross-sharing, search, library ↔ agent integration 
>
>  
>
>   | Compliance crosswalk  | Separate product — breaks FEMA requirements into checklists, validates plan against them  | Automate with Vanta-style self-serve intake 
>
>  
>
>   | Current intake  | Email or manual upload; human manually triggers compliance checks  | Replace entirely with self-serve form + automated trigger 
>
>  
>
>   | Customer base  | 60+ agencies (state, county, city)  | — 
>
>  
>
>   | Evaluation scale  | ~111 FEMA guidelines per standard HMP evaluation  | — 
>
>    
>
> The job of this role: Build the form-based intake, automate the trigger, ship the async evaluation pipeline, extend the RAG, contribute to agent skills. Own it across backend + infra + frontend.
>
>  
>
> ### The Three Modules (know these cold) 
>
>    
>
>   | Module  | What It Does  | Key Feature 
>
>    
>
>   | E01 — Evaluate  | Automated FEMA crosswalk of plans  | Smart References: which page answers which guideline 
>
>  
>
>   | E02 — Improve  | Plan Library + Peer Docs + Deconflict  | Deconflict: finds contradictions ACROSS multiple plans 
>
>  
>
>   | E03 — Operationalize  | Custom knowledge base + real-time chat Q&A  | Surfaced as "Chat" in the nav 
>
>    
>
> Custom evaluations: Agencies can build their own guideline checklists — not just FEMA library. The guideline store is multi-tenant and user-editable. Architectural implication: guidelines have an owner field (system vs. agency).
>
>  
>
> ### Domain Terminology (know these, use them naturally) 
>
>    
>
>   | Term  | Meaning 
>
>    
>
>   | EOP  | Emergency Operations Plan — master disaster response plan 
>
>  
>
>   | HMP  | Hazard Mitigation Plan — FEMA-required; must pass periodic assessments 
>
>  
>
>   | COOP  | Continuity of Operations Plan — how the agency keeps running during a disaster 
>
>  
>
>   | IAP  | Incident Action Plan — operational plan for a specific incident 
>
>  
>
>   | AAR  | After Action Report — post-incident lessons learned 
>
>  
>
>   | EOC  | Emergency Operations Center — command hub during a disaster 
>
>  
>
>   | FEMA  | Sets national doctrine; EM1 evaluates plans against FEMA guidelines 
>
>  
>
>   | Doctrine  | The authoritative federal/state guidance EMs are required to follow 
>
>    
>
> ### Samay ↔ EM1 Translation (your experience maps directly) 
>
>    
>
>   | Samay (what you built)  | EM1 (what you're describing) 
>
>    
>
>   | SOC2/NIST/ISO27001 controls  | FEMA guidelines 
>
>  
>
>   | AWS infra + GitHub/Jira data  | Emergency plan document sections 
>
>  
>
>   | Evidence collection Lambda (6 sources)  | Document parsing + chunking pipeline 
>
>  
>
>   | LLM compliance scoring (Bedrock)  | Guideline crosswalk evaluation 
>
>  
>
>   | Structured output with evidence quotes  | Smart References (guideline → exact plan page) 
>
>  
>
>   | Controls dashboard (React)  | Evaluate module UI 
>
>  
>
>   | Per-tenant S3 / schema isolation  | Per-agency document isolation 
>
>    
>
> ### The Team 
>
>   
> - Gunnar Holwerda — CTO/Co-founder. Engineering leader at OpenSesame (enterprise B2B SaaS) and Olo (restaurant tech, high-scale). Knows production engineering at scale. Respects concrete numbers over buzzwords. 
> - Tyler Felous — CEO/Co-founder. Built and sold Wisely (fintech). 
> - 4 engineers total including Gunnar. 2 early-career engineers. Data analyst/researcher. EM operators on the team.   
>
> ## PART 2 — SYSTEM DESIGN (MASTER ANSWERS) 
>
>   
>
> Study Monday. Highest-risk questions. Know these cold before anything else.
>  The system design question will come in many forms — they all map to one of these answers.
>
>    
>
> ### 2A: FULL END-TO-END SYSTEM — THE VANTA-STYLE MODULE 
>
>   
>
> The master answer. Lead with this for any broad system design question. ~4-5 min, then let him steer.
>
>   
>
> #### Critical framing (say this first): 
>
>   
>
> "The current flow is: plans come in by email, a human manually uploads and manually triggers the compliance check. The Vanta module automates everything from intake to results — the human only re-enters at the review and sign-off step. That is exactly the right place for them to be."
>
>   
>
> #### The 6-Stage Flow: 
>
>  
>
> Stage 1 — Self-Serve Intake Form
>  Replaces email. The form collects: plan type (EOP/HMP/COOP), agency (pre-populated from account), plan version/date, file upload, guideline library selection (FEMA standard, state, or custom). File upload uses a presigned S3 PUT URL — large PDFs go directly browser→S3, not through the API server. On submit: POST /evaluations returns {job_id, status: "QUEUED"} immediately. User sees: "Your plan has been submitted. We'll notify you when the evaluation is complete."
>
>  
>
> Stage 2 — Async Job Queue
>  API handler writes evaluation_jobs record + publishes to SQS. Worker consumes and processes. Double-submit protection: unique constraint on (agency_id, plan_file_hash) returns the existing job instead of starting a duplicate. This is the core architectural change from the current model — the human coordinator is replaced by a job queue.
>
>  
>
> Stage 3 — Document Ingestion (if new plan version)
>  Check if this exact file hash has been indexed before — if yes, skip. If no:
>
>   
> - Structure-aware parsing: extract section map (section number → heading → page range), not naive token chunking 
> - Two-level indexing: section summaries (~500 tokens) AND paragraph chunks (~150-200 tokens with overlap) 
> - Every chunk tagged with provenance: {agency_id, doc_id, section, heading, page, chunk_index} 
> - Embed + write to pgvector; metadata to PostgreSQL  
>
> Stage 4 — Crosswalk Evaluation Loop (111 guidelines)
>  For each guideline:
>
>   
> - Hierarchical retrieval: query section summaries → identify top 2-3 sections → retrieve paragraph chunks from within those sections only 
> - LLM call with Pydantic output schema: {verdict: PASS|PARTIAL|FAIL|INCONCLUSIVE, evidence_quote: str, page_reference: str, gaps: list[str]} 
> - Evidence gate: if evidence_quote is empty or not in the retrieved context → force INCONCLUSIVE. The LLM cannot hallucinate a PASS. 
> - Write result to evaluation_results per guideline; update progress counter  
>
> Cost optimization: Cache results keyed on (guideline_id, chunk_hash). If plan section hasn't changed since last run, reuse the cached result. Repeat evaluations are 60-70% cheaper than first-time runs.
>
>  
>
> Stage 5 — Human-in-the-Loop Review
>  The LLM output is the first-pass reviewer, not the final verdict.
>
>   
> - PASS (high confidence): One-click accept. Minimal friction. 
> - PARTIAL / NEEDS ATTENTION: Evidence quote shown inline. EM can accept, override with annotation, or flag. 
> - INCONCLUSIVE: Mandatory review. Cannot be submitted without human resolution. 
> - FAIL: Specific gaps listed from LLM. EM sees exactly what's missing.  
>
> Audit trail: LLM verdict + human decision stored together. FEMA submission includes both.
>
>  
>
> Stage 6 — Report & History
>  Structured scorecard generated. Export to PDF for submission. Evaluation history stored: {agency_id, plan_id, run_id, overall_score, run_date} → enables "improved from 68% to 84% since last submission" trend view.
>
>   
>
> ### 2B: HUMAN-IN-THE-LOOP — DESIGN PHILOSOPHY 
>
>   
>
> EM1's core product philosophy. He will ask this in some form.
>
>   
>
> The distinction: tasks where AI can be the final decision-maker vs. tasks where AI should accelerate a human decision. Crosswalk evaluation is firmly the second category.
>
>  
>
> A FEMA compliance verdict requires contextual judgment — the agency's local hazard profile, FEMA's current assessment priorities, the jurisdiction's history. The LLM has none of that. It has the document and the guideline text.
>
>  
>
> The right division of labor:
>
>   
> - LLM does: read 2000 pages, match 111 guidelines, extract evidence quotes, flag gaps. Days of work done in minutes. 
> - Human does: decide whether the evidence is sufficient for this agency's specific situation. That judgment cannot be automated.  
>
> The system enforces this:
>
>   
> - INCONCLUSIVE cannot be submitted without human resolution — no bypass 
> - Evidence quotes are verbatim, not paraphrased — human can verify in 5 seconds 
> - Human overrides stored alongside LLM verdicts — full audit trail 
> - Confidence scores surface low-confidence PASS verdicts — the system is honest about uncertainty  
>
> How it evolves over time: As the system accumulates history of LLM verdicts that match human decisions for stable plan sections, high-confidence PASSes on unchanged sections become one-click approvals. The loop gets shorter for routine cases. Human is still in the loop — just less friction.
>
>  
>
> The Samay parallel: The automated control testing system generated evidence and score; the compliance auditor reviewed and signed off. The LLM is a first reviewer, not the final one. Same principle.
>
>   
>
> ### 2C: RETRIEVAL FROM LARGE DOCUMENTS 
>
>   
>
> 2000-page plans + 111 guidelines = retrieval precision is everything.
>
>   
>
> Three problems with naive token chunking on a 2000-page plan:
>
>   
> - Context loss — a chunk has no idea it came from "Section 4: Resource Management" 
> - Citation imprecision — "somewhere in the plan" is useless; "Page 91, Section 4.2" is what Smart References needs 
> - Retrieval noise — top-5 chunks by pure vector similarity may be from totally different sections  
>
> How to handle it:
>
>  
>
> Structure-aware parsing first. Extract section map before embedding: section number → heading → page range. This is the load-bearing step. At Samay I faced this with multi-format policy docs (docx, PDF, RTF) — metadata preservation during ingestion matters more than the chunking strategy itself.
>
>  
>
> Two-level indexing. Section summaries (~500 tokens) for coarse navigation. Paragraph chunks (~150-200 tokens with overlap) for precision. Both indexed.
>
>  
>
> Hierarchical retrieval. For each guideline: query section summaries → find the 2-3 most relevant sections → retrieve paragraph chunks from within those sections only. Same principle as a book index — find the chapter, then find the paragraph.
>
>  
>
> Contextual chunk enrichment. Every chunk carries full provenance: {doc_title, version, section, heading, page, paragraph_index}. LLM receives this metadata alongside the text. The Smart References citation is assembled from the metadata — not extracted from LLM output.
>
>   
>
> ### 2D: DECONFLICT ARCHITECTURE 
>
>   
>
> Cross-plan contradiction detection — a harder problem than it looks.
>
>   
>
> Two sections can be semantically similar but logically contradictory: "The EOC is activated by the Director" and "The Deputy Director activates the EOC" are close embeddings that directly conflict. Vector similarity won't catch this.
>
>  
>
> Three-phase approach:
>
>  
>
> Phase 1 — Topic clustering. For all plans belonging to an agency, group sections by topic across plans: "all sections across EOP, HMP, and COOP that address EOC activation." This creates candidate groups for contradiction analysis without comparing every pair (which is O(n²) across a large corpus).
>
>  
>
> Phase 2 — Pairwise LLM contradiction detection within clusters. For each cluster: "Given these two sections from different plans, do they give conflicting guidance on the same subject?" Structured output: {contradicts: bool, topic: str, plan_a_section: {...}, plan_b_section: {...}, conflict_description: str}.
>
>  
>
> Phase 3 — Conflict store. {agency_id, topic, plan_a_id, plan_a_section, plan_b_id, plan_b_section, conflict_description, status: open|resolved}. This is the data model for the Deconflict UI — unresolved contradictions surfaced, resolved ones tracked.
>
>  
>
> Where graph fits: Model the corpus as a graph — sections as nodes, addresses_same_topic_as and contradicts as edges. Queries like "all unresolved contradictions involving EOC activation across active plans" become trivial traversals. This is the same pattern as the Samay identity graph — Neo4j is the right tool when the important queries are relationship traversals.
>
>   
>
> ### 2E: AAR PIPELINE & REVIEW SKILL 
>
>   
>
> AARs are part of E03 knowledge base + the upcoming agent skills direction.
>
>   
>
> What makes AARs architecturally different from plans:
>
>   
> - Unstructured narrative (no fixed section schema like a compliant EOP) 
> - Incident-typed — a wildfire AAR is relevant to wildfire planners, irrelevant for active shooter 
> - Lessons-first — the valuable content is "what we learned / what we'd do differently" 
> - Cross-shareable (with consent) — other agencies' AARs are valuable learning material  
>
> Ingestion pipeline: Upload → S3 → structure-aware parsing (look for section markers: "Lessons Learned," "Recommendations," "What Worked," "What Didn't Work") → chunk + embed → knowledge base.
>
>  
>
> Key metadata difference from plans: Every AAR chunk tagged with incident_type (extracted by a classification LLM call or selected at upload), section_type (lessons_learned | recommendations | timeline | other), incident_date, source_agency_id. Without incident tagging, retrieval is noisy across all incident types.
>
>  
>
> Two retrieval use cases:
>
>   
> - E03 Chat: "What have agencies learned from active shooter responses?" → filter incident_type: active_shooter, section_type: lessons_learned → retrieve top-k 
> - Plan improvement workflow: after a crosswalk flags PARTIAL on EOC activation, surface AARs from similar agencies who had the same gap and how they resolved it  
>
> The AAR review skill (stateful LangGraph agent): When an agency finishes an incident and needs to write their AAR, the agent guides them through it step by step — timeline collection (structured form), what worked, what didn't, recommendations. Each step retrieves relevant peer AARs as examples. Final step: draft generation from the structured inputs. State persists across sessions — the user can stop and resume. This is a stateful multi-step workflow agent, not a Q&A agent.
>
>  
>
> Cross-sharing governance: Explicit consent flag per document: {is_shared: bool, anonymize_agency: bool, shared_incident_types: [...]}. Agencies opt in per AAR.
>
>   
>
> ### 2F: AGENT SKILLS ARCHITECTURE 
>
>   
>
> New product direction: E03 evolves from Q&A to guided multi-step workflows.
>
>   
>
> The shift: From reactive stateless Q&A (user asks, agent answers) to stateful conversation with a workflow graph (agent guides user through a structured process with memory across turns).
>
>  
>
> Four components:
>
>  
>
> State schema. Each skill has a state object persisting across the conversation: where the user is, what's been collected, what's still needed. For plan creation: {current_section: "hazard_identification", completed_sections: [...], draft_content: {...}, gaps: [...]}. State lives in the session (PostgreSQL), not in the context window.
>
>  
>
> Workflow graph. Each skill is a directed graph of steps. Nodes = stages (gather jurisdiction info, identify hazards, draft mitigation actions). Edges = transitions triggered by user response or tool result. LangGraph provides this natively — I built LangGraph-based agentic workflows at Epik for security triage pipelines with branching logic. Same pattern.
>
>  
>
> Scoped tool access per step. At each node, the agent has access to only the tools relevant to that step. For "hazard identification": retrieve peer agency hazard sections from library, query FEMA doctrine for that hazard type, check agency's existing plan. Not all tools — just the relevant ones. Keeps the agent focused and reduces noise.
>
>  
>
> Persistence and resumability. A plan creation workflow is not done in one session. State persisted to PostgreSQL keyed on (agency_id, skill_type, workflow_instance_id). User returns → load state → resume.
>
>  
>
> Build order: Start with the simplest possible skill — single-step, no branching, no resumability. Prove the pattern end-to-end. Then add persistence, then multi-step, then branching. The ugly single-step version first is the same discipline as Samay — ugly scripts before architecture.
>
>   
>
> ## PART 3 — TECHNICAL DEEP-DIVES 
>
>   
>
> Study Tuesday AM. Be ready to go narrow and deep on any of these.
>
>    
>
> ### 3A: GRAPH-RAG — THE 1-MINUTE ANSWER 
>
>   
>
> They'll say "Graph-RAG" — be able to position it without overselling.
>
>   
>
> The honest take: Graph-RAG is a specific solution to a specific problem — answering questions that require multi-hop relationship traversal across documents. For the main E01 crosswalk (one plan, 111 guidelines), it is overkill. Dense vector retrieval on well-structured chunks is faster, cheaper, and simpler.
>
>  
>
> Where it actually earns its cost:
>
>   
> - "Which other agencies in our region have mitigation strategies that address our highest-risk hazards?" — cross-agency, cross-hazard, cross-section traversal. That's a graph query. 
> - Deconflict cross-reference graph — sections as nodes, contradiction/alignment as edges, queries like "all unresolved contradictions involving EOC activation" 
> - Doctrine dependency chains — "this guideline references that standard which requires this other certification" — that is a graph by definition  
>
> Decision rule (what I applied at Samay): If the critical queries are "find the most semantically similar content to this text" → vector. If the critical queries are "traverse relationships between named entities across documents" → graph. If the system needs both → dual store with explicit routing at query time.
>
>  
>
> What I'd propose for EM1: Vector (pgvector) as the primary retrieval layer for all single-plan queries. Knowledge graph (lightweight, possibly in PostgreSQL itself as an adjacency model) for cross-plan deconflict and inter-agency queries. Add Neo4j when the cross-document relationship traversal earns its operational overhead.
>
>   
>
> ### 3B: ASYNC JOB ARCHITECTURE 
>
>   
>
> They'll want to understand how you handle long-running operations. This is the design.
>
>   
>
> Why async is mandatory: At 111 LLM calls × 1-3 seconds each → 2-5 minutes per evaluation. A synchronous HTTP request will time out. The only right answer is async + polling/webhook.
>
>  
>
> The pattern:
>
>   
> -  
>
> POST /evaluations — validates input, writes job record with status QUEUED, publishes to SQS, returns {job_id, status: "QUEUED"} immediately. HTTP response is fast (< 200ms).
>
>   
> -  
>
> SQS queue → ECS worker picks up job. Worker updates status PROCESSING, runs the evaluation loop, writes results per guideline, updates progress counter (progress_counter column, incremented after each guideline completion).
>
>   
> -  
>
> Client polls GET /evaluations/{job_id} every 5 seconds: status + {completed: 45, total: 111} — progress bar is live. Or: webhook callback registered at job creation.
>
>   
> -  
>
> Worker completes → status COMPLETED, final report written. Or FAILED with error_message.
>
>    
>
> Schema:
>
>  
>
> ```text
> evaluation_jobs(id, agency_id, plan_id, guideline_set_id, status, progress_counter, total_guidelines, created_at, completed_at, error_message)
> evaluation_results(id, job_id, guideline_id, verdict, evidence_quote, page_reference, gaps, cached_from_job_id)
>
> ```
>
> Idempotency: Unique constraint on (agency_id, plan_file_hash, guideline_set_id). If the same plan+guidelines are submitted again, return the existing job_id, don't requeue.
>
>  
>
> Cache hit logic: Before running a guideline, check if (guideline_id, chunk_hash) has a result from a prior run. If yes — copy result with cached_from_job_id reference. Skip the LLM call. Repeat evaluations can be 60-70% cheaper.
>
>   
>
> ### 3C: SCALABILITY + LLM COST 
>
>   
>
> The 111 × 60 = 6,600 call math. He knows the numbers — show you do too.
>
>   
>
> Current scale: 111 guidelines × 60 agencies = 6,600 LLM calls per full evaluation cycle. If agencies run evaluations monthly: 6,600/month. At 10x growth: ~66,000/month.
>
>  
>
> Cost breakdown (rough):
>
>   
> - GPT-4o at ~5/1Moutputtokens, 1,000tokensoutputpercall→ 5/1M output tokens, ~1,000 tokens output per call → ~5/1Moutputtokens, 1,000tokensoutputpercall→ 0.005/call 
> - 111 calls × 0.005=0.005 =0.005=0.55 per evaluation. Fine at 60 agencies. Fine at 600 agencies ($330/month). 
> - The cost problem isn't the per-evaluation price — it's inefficiency from re-running unchanged plan sections.  
>
> Three levers:
>
>  
>
> Lever 1 — Result caching (biggest win). Key: {guideline_id, chunk_hash}. If plan section hasn't changed since last evaluation, cache hit, skip LLM. Plans are mostly stable — an agency might update 10-15% of sections between evaluations. Caching can eliminate 60-80% of calls on re-evaluations.
>
>  
>
> Lever 2 — Model tiering. Not all 111 guidelines need GPT-4o reasoning. Simple structural checks ("Does the plan have a resource management section?") → fast, cheap model (GPT-4o-mini, Haiku). Complex judgment calls ("Is the mitigation strategy adequately specific?") → full model. Route at inference time. Rough split: 30-40% of guidelines are structural → 35% cost reduction with no quality loss.
>
>  
>
> Lever 3 — Hierarchical retrieval reduces tokens. Better retrieval = smaller, more precise context = fewer tokens in = lower cost. Every improvement to retrieval precision has a direct cost payoff.
>
>  
>
> The architecture implication: Cost at scale is mostly a retrieval quality problem and a caching problem, not a model size problem.
>
>   
>
> ### 3D: HALLUCINATION PREVENTION 
>
>   
>
> EM1 is a domain where wrong answers have real stakes. This matters.
>
>   
>
> The risk: LLM returns verdict: PASS with a plausible-sounding evidence quote that doesn't actually exist in the plan. Agency submits to FEMA. FEMA assessment fails.
>
>  
>
> Four-layer defense:
>
>  
>
> Layer 1 — Evidence gating (the core constraint). Pydantic output schema requires evidence_quote: str. Post-processing: verify the quote exists verbatim in the retrieved context. If not: force verdict = INCONCLUSIVE. The LLM cannot hallucinate a PASS — missing evidence means the system doesn't have enough confidence to emit a verdict. This is the same pattern I built at Samay: no quote → no PASS verdict.
>
>  
>
> Layer 2 — Quote-then-reason prompting. Prompt structure: "First, copy the exact sentence from the context that addresses this guideline. Then, based solely on that sentence, assign a verdict." Forces the LLM to ground in source material before reasoning. Reduces confabulation significantly vs. open-ended prompts.
>
>  
>
> Layer 3 — Post-processing reconciliation. Pipeline step after LLM response: check evidence quote exists in chunks, check page reference exists in doc metadata, check no verdict contradicts the evidence quote. Flag inconsistencies for mandatory review. This catches cases where the LLM is inconsistent with itself.
>
>  
>
> Layer 4 — Eval harness. Golden test set: 20-30 known evaluations (manual expert assessments) checked against the pipeline nightly. Track precision by guideline type, precision by doc structure complexity. I built this at Epik with Langfuse — the infra is straightforward, the discipline is making sure the golden set stays current. If evaluation quality drifts, you catch it before a customer does.
>
>   
>
> ### 3E: MULTI-TENANT ARCHITECTURE 
>
>   
>
> 60+ agencies. Each one's data cannot leak to another.
>
>   
>
> Three layers of isolation:
>
>  
>
> Layer 1 — Request-level. JWT contains agency_id. API middleware extracts it, validates it against the session, sets it in request context. Every downstream call to the database or vector store receives agency_id explicitly. No request can operate on data without an agency_id in its context.
>
>  
>
> Layer 2 — Database-level (PostgreSQL). agency_id foreign key on every data table. Row-level security policies: CREATE POLICY tenant_isolation ON evaluation_jobs USING (agency_id = current_setting('app.current_agency_id')::UUID). Even if application code has a bug and forgets to filter, the database enforces it.
>
>  
>
> Layer 3 — Vector store namespace isolation. pgvector: filter condition agency_id = $1 on every retrieval query. If using Pinecone: namespace per agency. No cross-tenant vector retrieval is structurally possible at the query layer.
>
>  
>
> Guideline store multi-tenancy: System guidelines (agency_id IS NULL) are shared read-only. Agency custom guidelines have agency_id set. Retrieval query: WHERE agency_id = $1 OR agency_id IS NULL. Agencies cannot read each other's custom guidelines.
>
>  
>
> The Samay parallel: Per-tenant S3 buckets, per-tenant Neo4j databases, per-tenant RDS schema. The model was total physical isolation. For EM1 at this scale, logical isolation (RLS + namespace filtering) is the right tradeoff — lower cost, same security properties when implemented correctly.
>
>   
>
> ### 3F: POSTGRESQL SCHEMA + PGVECTOR 
>
>   
>
> The core data store. Be ready for schema-level questions.
>
>   
>
> Core tables:
>
>  
>
> ```text
> agencies(id, name, state, plan_count, created_at)
> plans(id, agency_id, type[EOP|HMP|COOP|IAP|AAR], version, file_hash, s3_key, ingested_at)
> plan_sections(id, plan_id, section_number, heading, page_start, page_end)
> plan_chunks(id, plan_id, section_id, text, chunk_index, embedding vector(1536), page)
> guidelines(id, agency_id NULLABLE, title, text, source, category)
> evaluation_jobs(id, agency_id, plan_id, guideline_set_id, status, progress_counter, total_guidelines, ...)
> evaluation_results(id, job_id, guideline_id, verdict, evidence_quote, page_reference, gaps, cached_from_job_id)
>
> ```
>
> Indexes that matter:
>
>   
> - CREATE INDEX ON plan_chunks USING ivfflat (embedding vector_cosine_ops) — ANN index for pgvector 
> - CREATE INDEX ON plan_chunks (plan_id, section_id) — hierarchical retrieval by section 
> - CREATE INDEX ON evaluation_results (job_id, guideline_id) — fast job result aggregation 
> - CREATE INDEX ON evaluation_jobs (agency_id, status) — dashboard queries per agency  
>
> pgvector vs Pinecone decision: pgvector when: data is already in PostgreSQL, retrieval needs joins with structured metadata (e.g., filter by plan_id AND section_id), scale doesn't require horizontal vector scaling. Pinecone when: retrieval is pure semantic similarity at millions of vectors with no join requirements, latency SLA is < 10ms. For EM1 at current scale: pgvector is the right call — one less operational system, metadata joins come for free.
>
>   
>
> ### 3G: TESTING + OBSERVABILITY 
>
>   
>
> How you'd keep the AI pipeline honest in production.
>
>   
>
> Two categories of tests:
>
>  
>
> Deterministic tests (straightforward): API contract tests, schema validation (does the Pydantic model parse?), business logic (does the result cache logic correctly skip LLM when chunk_hash matches?), idempotency (double-submit returns existing job_id). These are unit/integration tests, fast, run in CI.
>
>  
>
> AI behavior tests (different problem): The LLM output is probabilistic. Standard unit tests cannot assert exact outputs. The right approach:
>
>   
> - Schema contract tests: Does the response always have verdict, evidence_quote, page_reference? These pass/fail deterministically even though the content is probabilistic. 
> - Golden set evaluation: 20-30 labeled examples (guideline + plan section + expected verdict). Run nightly. Track precision@k and recall@k per guideline category. Not pass/fail — drift detection. 
> - Tracing + span logging: Every LLM call gets a run_id. Log: input prompt hash, retrieved chunk IDs, model version, latency, token counts, output schema validation result. This is what Langfuse or LangSmith provides — I built this at Epik. When a user files a bug on a specific evaluation, you can replay the exact run.  
>
> Monitoring in production:
>
>   
> - INCONCLUSIVE rate per guideline: sudden spike = retrieval quality problem or guideline text change 
> - Cache hit rate: dropping cache hits = plans changing more than expected, or cache key logic broken 
> - p99 latency per evaluation: early warning of slow workers or SQS queue backup 
> - Evidence quote verification failure rate: leading indicator of hallucination pressure   
>
> ## PART 4 — STACK-SPECIFIC 
>
>   
>
> Study Tuesday PM. EM1 is TypeScript/Next.js/Terraform — be confident, not defensive.
>
>    
>
> ### 4A: TYPESCRIPT DEPTH 
>
>   
>
> They will probe whether you actually write TypeScript or just "use" it.
>
>   
>
> The foundation is solid: TypeScript is the language of every modern frontend I've built — React UIs at Samay, Epik, TrustX. The discipline I care about:
>
>  
>
> Shared domain types. Define once, use everywhere. For EM1:
>
>  
>
> ```text
> // Defined in @em1/types, imported by API handler, database layer, and UI component
> type EvaluationVerdict = 'PASS' | 'PARTIAL' | 'FAIL' | 'INCONCLUSIVE';
>
> interface EvaluationResult {
>   guidelineId: string;
>   verdict: EvaluationVerdict;
>   evidenceQuote: string;         // never undefined — required by schema
>   pageReference: string;
>   gaps: string[];
>   cachedFromJobId: string | null;
> }
>
> ```
>
> If the LLM response doesn't match EvaluationResult, the Zod parse throws before it reaches any business logic.
>
>  
>
> Discriminated unions for job status: Instead of status: string, use:
>
>  
>
> ```text
> type EvaluationJob =
>   | { status: 'QUEUED'; queuedAt: Date }
>   | { status: 'PROCESSING'; startedAt: Date; progress: number; total: number }
>   | { status: 'COMPLETED'; completedAt: Date; resultId: string }
>   | { status: 'FAILED'; failedAt: Date; error: string };
>
> ```
>
> The UI component that renders status can exhaustively switch — TypeScript will warn if you add a new status and forget to handle it.
>
>  
>
> Zod for LLM response parsing. The boundary where TypeScript type safety is most important is exactly where you have the least control — the LLM response. Parse it with Zod at the edge:
>
>  
>
> ```text
> const EvaluationResultSchema = z.object({
>   verdict: z.enum(['PASS', 'PARTIAL', 'FAIL', 'INCONCLUSIVE']),
>   evidence_quote: z.string().min(1),
>   page_reference: z.string(),
>   gaps: z.array(z.string()),
> });
> // If this throws, the pipeline writes INCONCLUSIVE — no untyped data downstream
> const parsed = EvaluationResultSchema.parse(llmResponse);
>
> ```
>
> RSC boundary consideration in Next.js App Router. Server Components cannot pass non-serializable objects to Client Components as props. When designing the eval results page: fetch data in a Server Component, serialize to primitives (not class instances), pass as props. This is the main footgun in RSC — you hit it once and understand the model immediately.
>
>  
>
> Ramp timeline: The App Router mental model is a 2-3 day adjustment for a React developer. The type fundamentals (union types, generics, Zod patterns) are already there from Samay + Epik. Contributing productively within a week.
>
>   
>
> ### 4B: TERRAFORM vs. CDK — HONEST POSITIONING 
>
>   
>
> Gunnar will likely probe this. Don't oversell. He's worked at real infra companies.
>
>   
>
> What I've actually built:
>
>   
> - AWS CDK (TypeScript): 15+ stacks at Samay — VPC, ECS, Lambda, RDS PostgreSQL, Neo4j on EC2, S3, Secrets Manager, Step Functions, AppRunner. Wrote, deployed, debugged. 
> - Terraform: Used for Azure infrastructure at Samay (AKS, managed Postgres, storage). Worked in an existing Terraform codebase, added resources, understood provider patterns.  
>
> The honest positioning: CDK is production depth, Terraform is working proficiency. The discipline is the same — both are infra-as-code with state management, both require understanding provider APIs and how changes are planned before applied. The syntax difference is real but not the hard part; understanding AWS resource relationships is the hard part, and that's what I have.
>
>  
>
> For EM1's stack: If EM1 uses Terraform, I'm contributing to existing modules within a sprint. If there are new modules to write, I'd be referencing provider docs alongside Gunnar the first time — that's honest. What I'd bring is the CDK depth that maps directly: I've debugged circular dependency errors between stacks, written custom constructs, handled secret injection to Lambda from Secrets Manager, done blue/green deploys with CodePipeline.
>
>  
>
> The answer to "have you used Terraform?" is yes, not no. The answer to "Terraform depth = CDK depth?" is no — and that honesty builds more trust than overclaiming.
>
>   
>
> ### 4C: NEXT.JS APP ROUTER 
>
>   
>
> Be specific. Not "I know React" — know the App Router model.
>
>   
>
> The App Router shift: The main conceptual change from Pages Router is the server/client boundary. Components are Server Components by default — they run on the server, have direct access to the database/secrets, don't ship JavaScript to the client. Client Components are explicitly opted in with 'use client'.
>
>  
>
> What this means for EM1's UI:
>
>   
> - The evaluation results page: Server Component fetches the job and results from the database directly (no API route needed), renders the list, passes serialized data to a Client Component that handles expand/collapse interactions. 
> - The intake form: Client Component (interactive), but form submission goes to a Server Action or API route. 
> - The progress polling during evaluation: Client Component with useState + useEffect for the polling interval, or Server-Sent Events.  
>
> RSC mental model: Think of the component tree as a waterfall — Server Components at the top (data fetching, layout, no interactivity), Client Components at the leaves (buttons, forms, real-time updates). The mistake people make is adding 'use client' to everything — that defeats the purpose.
>
>  
>
> Where I am: React is deep, TypeScript is deep, the RSC mental model is the 2-3 day ramp. I've read the App Router docs and the RSC RFC. The honest answer is: I'd be confident with the patterns within a week of first commit.
>
>   
>
> ### 4D: FULL-STACK SHIPPING STORY 
>
>   
>
> A concrete example of owning a feature end-to-end. Use this when they ask about scope of ownership.
>
>   
>
> The story (TrustX at Samay):
>
>  
>
> The compliance team needed a "Test Control" button in the React dashboard — click it, and the system runs the automated evidence collection and LLM evaluation for a single control, showing the result in real-time. The scope of that one button:
>
>   
> - React UI: New button component in the controls dashboard. Loading state, error state, result display (verdict badge, evidence quote, confidence score). 
> - API layer (Flask/Python): POST /controls/{id}/test endpoint. Validates the control exists and belongs to the tenant. Publishes to the job queue. Returns job_id. 
> - Worker logic (Lambda): Pulled evidence from 6 sources (GitHub, Jira, AWS Config, Confluence, Slack, file uploads). Assembled context. Called Bedrock (Llama 3.3 70B) with Pydantic output schema. Wrote result to RDS. 
> - Infrastructure (CDK): New SQS queue for on-demand test jobs (separate from the nightly batch queue). Lambda trigger. IAM permissions. Secret mounting for the 6 source integrations.  
>
> All four layers in one sprint. No handoffs — I wrote the React, the Flask endpoint, the Lambda, and the CDK stack. That's what "full-stack ownership" means in practice, not just "I've done frontend and backend."
>
>   
>
> ## PART 5 — BEHAVIORAL & CULTURE 
>
>   
>
> Study Tuesday PM — out loud. Practice the stories, don't just read them.
>  Format: STAR (Situation, Task, Action, Result). Max 2 minutes per story.
>
>    
>
> ### 5A: OWNERSHIP — SOLO FOUNDING ENGINEER 
>
>   
>
> "Tell me about a time you owned something end-to-end."
>
>   
>
> S/T: At Samay I was hired as the sole engineer to build TrustX — a compliance automation SaaS. No existing codebase, no architecture, no other engineers. The founders had a product vision and customers lined up. Everything from infrastructure to UI was my decision and my responsibility.
>
>  
>
> A: I started with the ugliest version that could demonstrate the value — manual evidence collection scripts, hard-coded output, no UI. Showed it to the first customer. They got it. Then I built infrastructure: 15+ CDK stacks, per-tenant S3/RDS/Neo4j isolation, Lambda suite for evidence collection. Then the AI layer: Bedrock integration, Pydantic output schema, evidence-gating logic. Then the React dashboard. Shipped to 3 customers.
>
>  
>
> R: Three paying B2B customers on a platform I designed and built alone. Every architectural decision — multi-tenant isolation model, async job pattern, graph DB for identity relationships — was mine to make and mine to defend. That's the context I work best in.
>
>  
>
> Bridge: "That's the context I'm looking for at EM1 — small team, big ownership, high-stakes domain where the engineering decisions matter."
>
>   
>
> ### 5B: WORKING WITH DOMAIN EXPERTS (EM OPERATORS) 
>
>   
>
> "How do you work with non-technical stakeholders?"
>
>   
>
> The principle: Before writing a line of code, watch the person doing the work manually. The first week on a new domain I am an observer, not a builder.
>
>  
>
> S/T: At Samay, the compliance auditor (the domain expert) was manually running the compliance checks: reading through control frameworks, cross-referencing AWS Config output, writing assessment summaries in Word. She knew every edge case, every ambiguity, every place the framework language was vague. I didn't.
>
>  
>
> A: I shadowed her for two full sessions before designing anything. I asked: "Which step takes the longest?" (Reading evidence from 6 sources). "Where do you still have to use judgment?" (Is this GitHub commit actually evidence for this control, or just adjacent?). "What would you never trust a tool to decide without reviewing?" (Any PASS verdict on a high-risk control). Those three answers shaped the architecture: automate the multi-source collection, preserve judgment on verdicts, make INCONCLUSIVE mandatory review.
>
>  
>
> R: The final system matched her mental model — she trusted it because it didn't try to replace her judgment, it accelerated her review. She signed off on PASS verdicts for routine controls in 30 seconds instead of 10 minutes.
>
>  
>
> For EM operators: Same principle. Before designing the intake form or the review UI, I'd want to watch an EM coordinator run a FEMA evaluation manually. What's tedious? What requires contextual judgment they'd never delegate? The answers drive the design.
>
>   
>
> ### 5C: MENTORING JUNIOR ENGINEERS 
>
>   
>
> "How do you work with early-career engineers?"
>
>   
>
> Two examples:
>
>  
>
> OSU (GTA): Taught discrete math and mobile app development. The gap between "understanding the concept yourself" and "teaching it clearly" is large. I learned to give students the smallest working example first, then generalize — not the theorem, then the example. Same approach in code reviews.
>
>  
>
> Zemoso: A junior engineer was struggling with test coverage — writing tests that tested implementation rather than behavior, tests that broke whenever internals changed. Instead of flagging it in review comments, I wrote one example test alongside his code: same feature, behavior-focused, no knowledge of internals. Showed the difference in a 20-minute pairing session. Coverage improved. He understood the principle, not just the fix.
>
>  
>
> The pattern I follow:
>
>   
> - Code reviews that explain the "why" behind the feedback, not just "change this to that" 
> - One pairing session beats five rounds of async review comments 
> - Never fix a junior's bug for them unless time is genuinely critical — walk through the debugging process together 
> - Pick up coverage for things they're struggling with quietly — don't let it become a pressure issue, just get the team unblocked  
>
> For EM1's 2 early-career engineers: First thing I'd do is understand what they're working on and where they feel uncertain. Then invest in the pairing, not the code review.
>
>   
>
> ### 5D: HARD ARCHITECTURAL DECISION 
>
>   
>
> "Tell me about a difficult technical decision you made."
>
>   
>
> S/T: At Samay, I needed to decide whether to use Neo4j (graph database) or extend PostgreSQL for the identity relationship graph — the system that tracked multi-hop relationships between users, roles, permissions, and AWS resources across multi-tenant compliance evidence.
>
>  
>
> A: The case for PostgreSQL: already in the stack, team knows it, one less operational system. The case for Neo4j: the queries I needed were 4-6 hop traversals ("find all AWS resources accessible by this user through role chains, across accounts, given this permission delegation"). I wrote both implementations for the simplest version of the query. The PostgreSQL recursive CTE was correct but took 800ms. The Neo4j traversal was 20ms.
>
>  
>
> R: Used Neo4j for the identity graph layer only. PostgreSQL for everything else. Per-tenant Neo4j databases for isolation. Added operational complexity — I had to learn Neo4j deployment, backup, the Cypher query language. The first two weeks were slower. But the query performance was non-negotiable for the use case.
>
>  
>
> What I'd say to Gunnar: "I don't add architectural complexity unless I've seen the simple version fail. I added Neo4j after writing the PostgreSQL version and seeing it wasn't fast enough. That's the order to approach it."
>
>   
>
> ### 5E: MOTIVATION — WHY EM1, WHY NOW 
>
>   
>
> "Why are you interested in this role?"
>
>   
>
> Three honest reasons:
>
>  
>
> 1. The problem has real stakes. At Samay, I built compliance automation for SOC2/NIST frameworks — the same pattern as FEMA crosswalk evaluation. What drew me there was that a wrong answer had real consequences: a company gets a compliance finding, a customer's data protection is incomplete. EM1 raises the stakes further — a plan with an unaddressed gap in an actual disaster has different consequences. That matters to me as an engineer. I want the work to matter.
>
>  
>
> 2. The architecture is the right level of hard. RAG on 2000-page documents with citation accountability, multi-tenant isolation, async job pipelines, agent skills — this is the class of problems I've been solving for two years. It's not trivially easy (interesting) and it's not research (achievable). It's applied AI engineering with clear production requirements.
>
>  
>
> 3. Small team, full ownership. I've worked in large microservices teams (Zemoso) where my scope was one service out of twelve. I've worked solo (Samay). I strongly prefer the solo/small-team context — decisions are faster, ownership is clearer, the engineering judgment that matters is yours. A 4-engineer team where each person has real scope is the right environment for the kind of engineering I want to do.
>
>   
>
> ### 5F: PRODUCTION FAILURE STORY 
>
>   
>
> "Tell me about a time something broke in production."
>
>   
>
> S/T: At Epik, we had a multi-stage data preprocessing pipeline for AI agent training data. One stage used Spark for distributed processing. In production, Spark was silently dropping records that failed schema validation — not raising an error, just filtering them out. We didn't know until a downstream model evaluation showed degraded performance on edge case inputs.
>
>  
>
> A: Diagnosed by adding a reconciliation check at the end of the pipeline: count records in → count records out → alert if out < in × 0.99. Found the drop immediately. Then traced: Spark's default behavior on malformed records in a DataFrame is to drop and continue, not fail. Added explicit schema enforcement at the read step with mode='FAILFAST' — fail loudly if any record doesn't match the schema. Also added logging of the error records to a dead-letter S3 prefix so nothing is silently lost.
>
>  
>
> R: The silent drop had been running for 3 sprints. The reconciliation check caught it permanently going forward. The lesson: in data pipelines, "it ran without errors" is not the same as "it ran correctly." You need explicit output validation, not just absence of exceptions.
>
>  
>
> Bridge to EM1: The INCONCLUSIVE verdict + mandatory review is the same principle. Don't let the system silently fail into a wrong answer. Make the failure loud and require a human to handle it.
>
>   
>
> ### 5G: CHANGING REQUIREMENTS 
>
>   
>
> "Tell me about a time requirements changed mid-project."
>
>   
>
> S/T: At Samay, the initial spec for TrustX was to track controls against SOC2 only. Three weeks into development, the customer asked if we could also support NIST 800-53. Different framework, different control numbering system, different evidence categories.
>
>  
>
> A: The original design had the control framework baked in — hardcoded SOC2 categories, hardcoded control IDs in the schema. Extending to NIST would have required schema migration and code changes in 12 places. I stopped, reviewed the schema, and extracted the framework as a first-class entity: frameworks(id, name, version), controls(id, framework_id, control_number, title, description). Two days of refactoring. Then adding NIST was a data import, not a code change.
>
>  
>
> R: SOC2 + NIST shipped two weeks after the pivot. ISO 27001 was added the following month with zero code changes — just data. The pivot to a framework-agnostic model was the right call, and the two-day investment paid back within the same month.
>
>  
>
> Bridge: This maps directly to EM1's custom evaluation feature — agencies build their own guideline libraries. Same design: guidelines as a first-class entity, not hardcoded to FEMA. The architecture was correct because requirements changed and we'd anticipated that.
>
>   
>
> ### 5H: DOMAIN ONBOARDING (NEW DOMAIN) 
>
>   
>
> "How do you get up to speed on a new domain?"
>
>   
>
> The process:
>
>   
> - Watch the person doing the work manually. Not "explain the domain to me" — sit with them while they do the actual task. 
> - Build the ugliest possible version of the core workflow. Not the full product — the 30-minute script that demonstrates value. Breaking it is how you learn where the real complexity lives. 
> - Talk to the customers directly, early. Not feature requests — "what's the worst part of your current process?" The answer to that is the product.  
>
> Emergency management specifically: I've spent serious time on EM1's public docs and the FEMA National Preparedness Goal since the first-round conversation. The planning cycle (EOP → HMP → COOP → AAR), the FEMA assessment process, the doctrine hierarchy — these are the vocabulary I'd need to be useful. The gap is I haven't worked with EM coordinators directly. The first thing I'd want to do after joining is shadow one evaluation review session — watch a coordinator actually go through a FEMA assessment, see where the friction is, understand what "good enough" means in practice for this domain.
>
>   
>
> ## PART 6 — QUICK-FIRE ANSWERS 
>
>   
>
> Wednesday morning only. Short, confident, no rambling.
>
>    
>
> Q: How do you know when something is done?
>
>   
>
> "Deployed, monitored for one business day, and the person who asked for it has used it and confirmed it solves the problem. Not 'the PR is merged' — the thing actually works."
>
>   
>
> Q: How do you think about technical debt?
>
>   
>
> "There's debt that costs a little now and a lot later — I don't take that on. There's debt that costs a little now and a predictable, manageable amount later — that's called a trade-off, and it's fine. The 'ugly scripts before architecture' principle I used at Samay: build the prototype that proves the value, then build it properly when you know the shape of the problem."
>
>   
>
> Q: What makes a good API?
>
>   
>
> "It doesn't surprise you. The resource model is consistent, the error responses are structured and actionable, the async operations return job IDs with a status polling contract. The test for a good API is: can a developer integrate against it using only the response bodies, without reading docs?"
>
>   
>
> Q: Tell me about a time you pushed back on a technical decision.
>
>   
>
> "At Monarch Tractor, the team wanted to use Workato (a third-party integration platform) for the HR system sync — UKG to JumpCloud to Azure AD. My pushback: Workato added $20K/year in licensing, required a vendor dependency for infrastructure that was core to employee onboarding, and the same workflow was straightforward AWS Lambda + EventBridge for pennies. I built a working proof-of-concept over a weekend. That became the production system. The pushback wasn't 'this is wrong' — it was 'here's the alternative, let me show you.' Evidence, not opinion."
>
>   
>
> Q: When do you ship fast vs. when do you slow down?
>
>   
>
> "Fast: prototypes that prove the concept, internal tools, features with an obvious rollback path. Slow: anything that handles multi-tenant data isolation, anything that writes to customer records in production, anything that touches auth or permissions. The rule: if a bug here means a customer sees another customer's data, or a compliance report is wrong, that gets extra review. If a bug here means a UI element is in the wrong color, ship it and fix it."
>
>    
>
> ## PART 7 — CLOSE OUT 
>
>   
>
> Read Wednesday morning after Part 0. Then close the doc.
>
>    
>
> ### 7A: QUESTIONS TO ASK GUNNAR (pick 3, not all 5) 
>
>   
>
> Always ask about the technical work first — shows you care about the problems, not just the role.
>
>    
> -  
>
> Technical / product:
>
>   
>
> "The crosswalk — how are you chunking the plans right now? Structurally by section or by token count? I'd expect section-aware parsing to be the hard part for citation precision."
>
>    
> -  
>
> Technical / future:
>
>   
>
> "For Deconflict — are you doing the cross-document contradiction detection today, or is that upcoming? Curious whether you're modeling it as a graph problem internally."
>
>    
> -  
>
> Team / growth:
>
>   
>
> "The 2 early-career engineers — how do you think about the mentoring dynamic in a team this small? I want to understand what being genuinely helpful to them looks like from day one."
>
>    
> -  
>
> Engineering culture:
>
>   
>
> "Coming from OpenSesame and Olo — what engineering habits or standards from those places are you deliberately bringing to EM1? And what are you intentionally leaving behind?"
>
>    
> -  
>
> Ownership / trajectory:
>
>   
>
> "If I joined and was fully up to speed in 60 days — what would you want me to own that you don't have enough bandwidth for right now?"
>
>      
>
> ### 7B: OPENING LINE (say this in the first 90 seconds) 
>
>   
>
> "I'm Neel — six years full-stack, last two deep in AI systems. The most relevant thing I've built is TrustX at Samay — compliance automation platform where the core was: collect evidence from multiple sources, assemble grounded context, run LLM evaluation with citation enforcement. When you describe the Evaluate module — automated FEMA crosswalk, Smart References — that's the same architecture in a different domain. Looking forward to getting into the specifics."
>
>   
>
> ### 7C: CLOSING LINE 
>
>   
>
> "This has been exactly the kind of technical conversation I was hoping for. What you're building — grounded AI with citation accountability in a domain where wrong answers have real stakes — is the problem I care about. I'd love to keep moving forward."
>
>    
>
> ### 7D: STUDY SCHEDULE (2 days) 
>
>    
>
>   | Day  | Focus  | Goal 
>
>    
>
>   | Monday  | Parts 1 + 2  | Know the company cold. Know the E2E flow and human-in-the-loop philosophy cold. 
>
>  
>
>   | Tuesday AM  | Part 3  | Be ready for technical deep-dives on retrieval, async jobs, hallucination, multi-tenant 
>
>  
>
>   | Tuesday PM  | Parts 4 + 5  | TypeScript/Terraform honest positioning. Practice behavioral stories out loud. 
>
>  
>
>   | Wednesday AM  | Part 0 only  | Cheat sheet. One read. Then close the doc. 
>
>     
>
> ### 7E: ENERGY + MINDSET 
>
>  
>
> The tone that works with Gunnar: He's a CTO who came from high-scale engineering orgs. He respects precision and dislikes vagueness. The right register is: confident, specific, honest about gaps, curious about their problems.
>
>  
>
> When you don't know something: Don't bluff. The right answer is: "I haven't worked with that specific tool directly, but here's how I'd think through it..." or "I know the adjacent thing — let me trace how it maps." He knows what he's hiring; he's not looking for encyclopedic knowledge, he's looking for engineering judgment.
>
>  
>
> The numbers rule: When you can use a number, use it. "~111 guidelines", "500-2000 pages", "60+ agencies", "4-engineer team." Numbers signal you did the homework.
>
>  
>
> The bridge rule: At the end of every technical answer, connect to a specific thing you built. Not "I understand this pattern" — "I built this pattern at Samay, here's what it looked like."
>
>  
>
> On Terraform/Next.js gaps: Acknowledge them cleanly, don't over-explain. "CDK is deep, Terraform is working proficiency — contributing within a sprint" is better than three sentences justifying why that's okay. Say it once, move on.
>
>   
>
> ### 7F: LOGISTICS 
>
>   
> - Format: 60-90 min conversation. Likely technical architecture first, then behavioral, then questions. May overlap throughout. 
> - Prep done by: Monday (Parts 1-2), Tuesday (Parts 3-5), Wednesday AM (Part 0 only) 
> - The old doc: Round2_Interview_Prep.md — 588 lines, full reference. If you want to check a specific answer in more detail, it is there.   
>
> Built: June 8, 2026 | Interview: June 10, 2026 | Role: Software Engineer, EM1

## Source provenance

- [Original HTML](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Interview%20Prep%20company%20prep%20docs/EM1/Round2_Prep_v2.html) · Interview Prep company prep docs/EM1/Round2_Prep_v2.html
- [Original MD](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Interview%20Prep%20company%20prep%20docs/EM1/Round2_Prep_v2.md) · Interview Prep company prep docs/EM1/Round2_Prep_v2.md

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
