---
kind: "company-prep"
title: "Round2 Interview Prep"
collection: "EM1"
topic: "Interview Prep"
imported: "2026-10-13"
source_files: ["Interview Prep company prep docs/EM1/Round2_Interview_Prep.html","Interview Prep company prep docs/EM1/Round2_Interview_Prep.md"]
tags: ["career/library"]
source_status: "source-claims-not-verified"
---

# Round2 Interview Prep

[[The Climb/Career Library/Career Library]]

> [!info] Source context
> Historical preparation or source notes. First-person stories and numeric outcomes remain source claims until confirmed; this import does not verify them.

# EM1 — Round 2 Interview Prep (60–90 min Technical + Culture)
### With Gunnar Holwerda, CTO / Co-Founder
**Date:** Wednesday June 10, 2026
**Format:** High-level tech concepts + culture fit. ~40-50 min technical, ~30-40 min behavioral.

---

## CRITICAL FRAMING BEFORE YOU START

Gunnar came from OpenSesame and Olo — real B2B SaaS at scale. He knows what "architected a system" looks like vs. "implemented tickets." He is hiring someone to hold architecture on a 4-engineer team that includes 2 early-career engineers.

You don't have "Staff Engineer" on your resume. That's fine. What you DO have is:
- Solo-designed and delivered a compliance automation platform from zero (Samay)
- Reasoned about multi-tenant isolation, graph vs. vector trade-offs, and LLM grounding in production
- Owned CDK infrastructure end-to-end — not just code, but the whole system

The move: **articulate the WHY behind every decision you made.** That's what separates someone who built something from someone who architected it. He will hear the difference.

---

## THE PRODUCT YOU ARE JOINING (Keep This Crisp)

| Module | What It Does |
|---|---|
| **Evaluate (E01)** | Automated FEMA crosswalk — evaluates each EOP/HMP section against FEMA guidelines; Smart References maps each guideline to the exact plan page answering it |
| **Improve (E02)** | Plan Library + Peer Docs (compare to peer agencies) + Deconflict (find contradictions ACROSS plans) |
| **Operationalize (E03)** | Custom knowledge base from uploaded docs + real-time answer engine with sentence-level citations |
| **Near-term focus** | Vanta-style compliance module: form-based plan intake → automated crosswalk validation → scored output |

**Plan types:** EOPs (master response plans), HMPs (FEMA-required mitigation plans), COOPs (continuity plans), IAPs (per-incident plans), AARs (post-incident lessons).
**The hard part:** Plans are 500–2000 pages. Agencies have multiple conflicting plans. LLM citations must be accurate — a wrong citation in an EOP is a liability.

---

## SECTION 1: SYSTEM DESIGN — The Crosswalk Module

> **This is the highest-risk question. He will ask this. You built this at Samay. Translate it.**

### The Question (several forms it can take):
- "How would you think about architecting the Vanta-style compliance module?"
- "Walk me through how you'd build the automated plan evaluation system."
- "If you were to design the crosswalk workflow from scratch, where would you start?"

### The Samay ↔ EM1 Translation

| Samay (what you built) | EM1 (what you're describing) |
|---|---|
| SOC2/NIST/ISO27001 controls | FEMA guidelines |
| AWS infra metadata + GitHub/Jira data | Emergency plan document sections (EOP, HMP) |
| Evidence collection Lambda (6 sources) | Document parsing + chunking pipeline |
| LLM compliance scoring (Bedrock) | Guideline crosswalk evaluation (LLM) |
| Structured output with evidence quotes | Smart References (guideline → exact page) |
| Controls dashboard (React) | Evaluate module UI |
| Per-tenant S3 / schema isolation | Per-agency document isolation |

### How to Answer (structured, ~4-5 minutes)

**"I'd think about this in four layers."**

**Layer 1 — Document Ingestion & Parsing**
The hardest part isn't the AI — it's ingestion. A 2000-page EOP is structured: it has a table of contents, numbered sections, annexes, appendices. If you treat it as a flat blob and chunk naively, your retrieval will be garbage — you'll get fragments without context, sections split mid-sentence across chunk boundaries.

What I'd do: parse structure first. Extract section headings, section numbers, and page ranges as metadata before chunking content. Build a structural map: Section 4 → pages 84–112 → "Resource Management." That way every chunk I store carries: `{section: "4.2", heading: "EOC Activation Procedures", page: 91, doc_id: "EOP-v3"}`. That metadata is what makes sentence-level citations possible later.

At Samay I faced a version of this with multi-format policy documents — docx, PDF, RTF — where you lose structural context in conversion. The lesson was: metadata preservation during ingestion is more important than the chunking strategy itself.

**Layer 2 — Dual Indexing: Vector + Structural**
Two indexes, not one.

First: vector embeddings per chunk (using pgvector in PostgreSQL or a dedicated store). These enable semantic retrieval — "find all content related to hazard identification" even if those exact words aren't present.

Second: a structured metadata layer in PostgreSQL — one row per chunk with section, page, heading, doc version, agency ID. This enables non-semantic queries: "give me all chunks from Section 4 of this EOP" for cases where you already know what section the guideline maps to.

You need both. Vector-only retrieval misses structural queries. Structured-only misses the semantic ones. The crosswalk workflow will use both: broad semantic search to find candidate sections, then page/section metadata to form the citation.

**Layer 3 — Guideline Store & Crosswalk Logic**
FEMA guidelines are a structured artifact — they have IDs, required elements, plain-text descriptions. I'd store them as structured records: `{guideline_id: "FEMA-HMP-4.2.1", text: "...", category: "Hazard Identification", required_elements: [...]}`.

The crosswalk loop is: for each guideline → retrieve top-k chunks from the plan → LLM evaluation prompt: "Given this FEMA guideline and these sections from the plan, does the plan satisfy this requirement? Return: verdict (PASS/PARTIAL/FAIL), evidence_quote (verbatim from plan), page_reference, gaps (if any)."

Critically, I'd use a **Pydantic output schema** for this — not free-text LLM output. The model must populate `evidence_quote`, `page_reference`, and `verdict` as structured fields. If it can't populate `evidence_quote`, the verdict is INCONCLUSIVE — not hallucinated. This is the same evidence-gating pattern I used in the take-home project and at Samay. The LLM can't assert a finding it didn't retrieve evidence for.

**Layer 4 — Agency Isolation & Results Storage**
Multi-tenant from day one. Agency A's plans never appear in Agency B's retrieval. I'd use:
- Filtered metadata on every vector query: `WHERE agency_id = ?` — no cross-agency leakage at the retrieval layer
- Per-agency row-level security (RLS) in PostgreSQL on the results tables — defense in depth
- Evaluation results written to a `control_evaluations` table with `agency_id`, `guideline_id`, `verdict`, `evidence_quote`, `page_ref`, `run_timestamp`

That last piece — storing structured evaluation history — is what enables the UI to show "you improved from 68% to 84% compliance since your last submission" and lets agencies track progress over time.

**The UI layer** I've already built at Samay: controls dashboard (list view, aggregate score per framework section), detail page per guideline (verdict, evidence quote, gaps), status update, comments for human review. That translates directly to the Evaluate module.

---

### Follow-up: "What would you do differently than Samay?"

Two things:

1. **Hierarchical retrieval** — at Samay the document corpus was smaller. For 2000-page plans I'd add a coarse-to-fine retrieval step: first retrieve section-level summaries to find the right section, then fine-grained chunk retrieval within that section. This cuts down irrelevant context and improves citation precision.

2. **Guideline dependency graph** — FEMA guidelines have dependencies: "Section 4.2 is only applicable if hazard X was identified in Section 3." At Samay the controls were independent. For a proper crosswalk you want to model those dependencies so the evaluation order is correct. That's a natural place for a lightweight graph — nodes are guidelines, edges are "must satisfy before."

---

## SECTION 2: GRAPH-RAG — CRISP 1-MINUTE ANSWER

> This was explicitly flagged as weak from the phone screen. Have this cold.

### The Question:
"You mentioned graph-RAG. Walk me through the trade-off — when is it worth the overhead vs. plain vector RAG?"

### The Answer:

Vector RAG and graph RAG answer different question types, and the mistake is trying to use one for both.

**Vector RAG** is the right default when the query is: "find content semantically similar to this." Single-hop. "What does this plan say about resource management?" Vector search is fast, straightforward to maintain, and well-supported.

**Graph RAG** earns its complexity when the query is multi-hop or relationship-centric: "which users had their permissions changed in the 30 days before this access event?" At Samay, that question can't be answered by semantic similarity — it requires traversal: User node → HAS_ACCESS_TO → Repository node → filtered by timestamp. Vector can't do that. Graph can.

For EM1 specifically: **single-plan retrieval → vector is right.** "Does Section 4.2 of this EOP satisfy FEMA guideline HMP-4.2.1?" That's semantic similarity within one document. Fast, cheap, works.

**Cross-plan reasoning → this is where graph adds value.** The Deconflict feature — "find contradictions across the EOP, HMP, and COOP" — is inherently relational. You're asking: "which sections across multiple plans address the same topic and give conflicting guidance?" That's a multi-hop traversal: Plan A Section 4 → addresses_topic → EOC Activation → addressed_by → Plan B Section 7 → contradicts → Plan A Section 4. Graph traversal makes that query clean. Trying to do it with vectors and pairwise similarity comparison across every chunk combination is $O(n^2)$ and noise-prone.

At Samay I used Neo4j for exactly this pattern — identity events as nodes, typed relationships, LangChain translating natural language questions into Cypher. The graph was the right shape because the queries were about multi-hop access chains, not document similarity.

**The cost of graph:** You need to maintain the graph as a separate store, keep it in sync with source data, and your engineers need to know Cypher. For plain Q&A over static documents, that's not worth it. For cross-document relationship reasoning at EM1's scale — it is.

**My recommendation for EM1:** Start vector-only for the crosswalk module (right tool, lower complexity). Build toward graph for Deconflict as the document corpus and cross-reference patterns mature. Don't add graph complexity before you've validated the query patterns that need it.

---

## SECTION 3: RETRIEVAL FROM 500–2000 PAGE PLANS

### The Question:
"How would you handle the retrieval challenge when the document is 2000 pages?"

### The Answer:

Three problems with naive fixed-size chunking on a 2000-page plan:

1. **Context loss**: a 512-token chunk cut in the middle of a section has no idea it's in "Section 4: Resource Management." The LLM receiving that chunk doesn't know what part of the plan it came from.

2. **Citation imprecision**: "somewhere in the plan" is useless. "Page 91, Section 4.2" is what the Evaluate module needs.

3. **Retrieval noise**: top-5 chunks from a 2000-page doc by pure vector similarity may all be from different sections with tangential relevance. You need structural coherence in what you pass to the LLM.

**How I'd handle it:**

**Step 1 — Structure-aware parsing.** Before embedding, parse the document structure: identify section headers, extract section boundaries (which pages each section spans), flag annexes and appendices as separate logical units. Store this as a structural map alongside the document.

**Step 2 — Two-level indexing.** Index at section level (section summaries, ~500 tokens each) AND at paragraph level (fine-grained chunks, ~150-200 tokens with overlap). Section summaries give you coarse navigation; paragraphs give you precision.

**Step 3 — Hierarchical retrieval.** For a given guideline: first query section summaries to identify the 2-3 most relevant sections. Then restrict fine-grained retrieval to chunks within those sections. This is the same principle as indexing a book — you find the chapter, then you find the paragraph. You don't scan every paragraph in the whole book.

**Step 4 — Contextual chunk enrichment.** Every chunk I store carries its full provenance: document title, version, section number, section heading, page number, paragraph index. When the LLM receives the chunk, it receives that metadata too. This is what makes the Smart References feature possible — the citation is assembled from the metadata, not extracted from LLM output.

I built this metadata-preservation pattern at Samay for policy documents — the structural integrity of the evidence is what makes it auditable. Same principle here, bigger documents.

---

## SECTION 4: DECONFLICT — ARCHITECTURE

### The Question:
"How would you think about the Deconflict feature — detecting contradictions across multiple plans?"

### The Answer:

This is one of the harder problems in the product because contradiction isn't just semantic distance — two sections can be semantically similar but logically contradictory. "The EOC is activated by the Director" and "The Deputy Director activates the EOC" are highly similar sentences that directly conflict.

**My approach:**

**Phase 1 — Topic clustering.** Extract all sections from all plans for an agency. For each section, generate a topic label or embedding. Cluster sections by topic across plans: "All sections across EOP, HMP, and COOP that address EOC activation." This gives you candidate groups for contradiction analysis.

**Phase 2 — Pairwise contradiction detection within clusters.** For each cluster (sections across different plans on the same topic), run an LLM comparison: "Given these two sections from different plans, do they give conflicting guidance on the same subject? If yes, describe the contradiction." Structured output: `{contradicts: true, topic: "EOC activation authority", plan_a: {...}, plan_b: {...}, conflict_description: "..."}`.

**Phase 3 — Conflict store.** Write flagged contradictions to a structured table: `agency_id, topic, plan_a_id, plan_a_section, plan_b_id, plan_b_section, conflict_description, status (open/resolved)`. This is the data model for the Deconflict UI.

**Where graph fits here:** You can model the full corpus as a graph — nodes are plan sections, edges are "addresses_same_topic_as" (from clustering) and "contradicts" (from detection). Neo4j makes queries like "find all unresolved contradictions involving EOC activation across all active plans" trivial. At Samay I modeled identity events as a graph for exactly this reason — the relationship queries that matter don't fit a relational table.

**Practical concern:** Pairwise comparison across all section pairs is expensive at scale — if an agency has 5 plans of 200 sections each, that's 1000 sections and potentially 499,500 pairs. The clustering step is load-bearing — it's what keeps the comparison set tractable. Good topic clustering reduces that to maybe 20–30 pairs per topic cluster.

---

## SECTION 5: HALLUCINATION PREVENTION AT CITATION LEVEL

### The Question:
"How do you make sure the LLM citations in the Evaluate module are accurate? How do you prevent hallucination?"

### The Answer:

I don't try to prevent hallucinations at the model level — that's a losing battle. I change the system architecture so hallucinations can't reach the output unchallenged.

**Three mechanisms:**

**1. Evidence-gated output schema.** The LLM must return a Pydantic model with `evidence_quote: str` (verbatim text from the plan), `page_reference: str`, and `verdict: Literal["PASS", "PARTIAL", "FAIL", "INCONCLUSIVE"]`. If the model can't provide a verbatim quote from the retrieved context, it must return `INCONCLUSIVE` — not a fabricated verdict. The schema enforces this contract. I used this exact pattern in the take-home project: the agent can't write a section of the brief without retrieved data to support it.

**2. Quote-then-reason prompting.** The system prompt instructs: "First, copy the exact sentence(s) from the provided plan text that are relevant to this guideline. Then evaluate whether that text satisfies the requirement." Forcing the quote-first behavior dramatically reduces confabulation — the model anchors on actual text before reasoning about it.

**3. Post-processing reconciliation.** After the LLM returns its structured output, a deterministic check verifies: is the `evidence_quote` a substring (or near-match via fuzzy string matching) of one of the retrieved chunks? If not, the verdict is flagged for human review rather than accepted. This catches cases where the model paraphrased or subtly altered the quote.

**Eval harness:** At Epik I built eval pipelines with Langfuse and golden datasets — known plan/guideline pairs with human-verified verdicts. Before every deploy, run the pipeline against the golden set and alert if citation accuracy drops below threshold. EM1 should have this from day one given the liability stakes — a wrong citation in a preparedness plan isn't a UX bug.

The underlying principle: **trust the retrieval, verify the assertion.** The retrieved chunks are ground truth. The LLM is only allowed to reason about what's in those chunks.

---

## SECTION 6: MULTI-TENANT ARCHITECTURE FOR EM1

### The Question (implicit — he'll probe this if you describe the system design):
"How would you handle data isolation between agencies?"

### The Answer:

I built multi-tenant compliance infrastructure at Samay and the pattern maps directly.

**Three layers of isolation:**

**Layer 1 — Tenant resolution.** Every request carries an agency JWT. The backend resolves `agency_id` from the token, looks up that agency's configuration in a PostgreSQL control-plane table — which S3 prefix, which vector namespace, which schema. No request proceeds without this resolution step. No agency ID → no data access.

**Layer 2 — Row-level security in PostgreSQL.** All evaluation results, guideline scores, and plan metadata tables have `agency_id` as a column with RLS policies that enforce it at the database level. Even if application code had a bug and forgot to filter, the DB enforces isolation.

**Layer 3 — Vector namespace isolation.** For the vector store (whether pgvector in PostgreSQL or an external store like Pinecone), every embedding carries an `agency_id` metadata tag and every query applies a metadata filter. An agency can only retrieve their own document chunks. Cross-agency retrieval is impossible by construction.

**At Samay** the per-tenant isolation was more complex — per-tenant Neo4j instances, per-tenant S3 buckets, per-tenant credentials in Secrets Manager under `neo4j/tenant-{id}` paths, IAM policies scoped to the pattern. EM1 probably doesn't need separate databases per agency — filtered namespaces and RLS are sufficient and much simpler to operate.

---

## SECTION 7: POSTGRESQL AT THIS SCALE

### The Question:
"Talk me through your PostgreSQL experience. Any performance or design considerations for this kind of system?"

### The Answer:

Production usage across three roles. The design considerations I'd apply at EM1:

**Schema design for the evaluation results table:** Avoid storing large text in PostgreSQL — evidence quotes and chunk text belong in S3 or a dedicated store, with a reference key in the row. PostgreSQL should own structured metadata: `guideline_id`, `verdict`, `agency_id`, `page_ref`, `run_id`, `created_at`. Fast OLTP queries, not a blob store.

**Indexing:** Composite index on `(agency_id, guideline_id, run_id)` for the most common query pattern — "show me all results for this agency's latest evaluation run." GIN index for full-text search on guideline text if you're doing in-DB search. EXPLAIN ANALYZE before any production query that's running against a large table.

**pgvector for embeddings:** PostgreSQL with pgvector is a reasonable choice for EM1's scale — you don't need Pinecone until you're at tens of millions of vectors. It keeps the operational footprint simple (one database) and the filtering story is native SQL. The tradeoff is that pgvector approximate nearest neighbor (IVFFlat or HNSW index) needs tuning — you configure the number of lists/clusters at build time and re-index when the dataset grows significantly.

**Multi-tenant schema strategy:** At Samay I used per-tenant PostgreSQL schemas. For EM1 I'd recommend a single schema with `agency_id` columns and RLS over per-tenant schemas — simpler to query, simpler to migrate, Postgres RLS handles the isolation cleanly.

---

## SECTION 8: NEXT.JS — HONEST, CONFIDENT ANSWER

### The Question:
"Your resume shows React. We're on Next.js. How quickly can you ramp?"

### The Answer:

My frontend work has been React and TypeScript throughout — that's the foundation Next.js is built on. The component model, hooks, state management, the TypeScript patterns — that's all the same.

The specific Next.js concepts I'd ramp on: the App Router (current direction — server components by default, layouts, nested routing), the server/client component boundary (which component needs client-side interactivity vs. which can be a server component), and the data fetching model with async server components replacing getServerSideProps.

I've also built forms, dashboards, evidence management UIs, and document management interfaces in React — all of which map directly to the compliance module UI they're building. The form-based plan intake, guideline-by-guideline results views, expandable evidence sections — I built all of those patterns at Samay. They were in React; translating to Next.js App Router is a framework migration, not a paradigm shift.

Honest ramp estimate: productive in the codebase within a week, fully comfortable in 3-4 weeks.

---

## SECTION 9: BEHAVIORAL / CULTURE FIT

### Q: Tell me about a time you owned something truly end-to-end.

TrustX ATAP at Samay. I came in as the sole engineer on a compliance platform for B2B SaaS customers. There was no dedicated DevOps, no dedicated frontend, no dedicated DBA. I owned everything: CDK infrastructure (15+ stacks — VPC, RDS, Lambda suite, Step Functions, AppRunner, ECS Fargate), the data pipelines, the LLM integration layer, and the React frontend with controls dashboards, evidence management, document editor.

When the infrastructure existed as click-ops with no IaC — dev had drifted from staging, nobody knew what was where — I migrated everything to CDK incrementally, stack by stack, until one `cdk deploy --all` stood up a clean environment. That's the kind of work that's invisible if you do it right and very visible if you don't.

The multi-tenant architecture was entirely my design: RDS as the control plane for tenant resolution, per-tenant Neo4j instances with credentials in Secrets Manager, per-tenant S3 buckets, Step Functions fanning out per tenant. I made those decisions, reasoned about the trade-offs (separate DBs vs. schemas, graph vs. vector for access traversal), and implemented them.

What end-to-end ownership meant practically: I filed bugs I found in adjacent systems. I flagged when a schema decision in week two was going to cause pain in week eight. I knew the whole system well enough to debug it at 2pm on a Friday without a runbook.

---

### Q: How do you work with junior engineers? What does that look like in practice?

Two angles: code reviews and knowledge transfer.

On code reviews: I try to give the "why," not just the "what." Saying "use a Pydantic model here instead of a raw dict" without explaining why is just a style vote. Saying "if you use a raw dict here, the Lambda returns a 200 even when the field is missing — Pydantic validation catches that at the boundary" is teaching something that will stick past this PR.

I also have a rule about code reviews: if I'm leaving more than 3 blocking comments, I ask for a sync call instead of a comment thread. Long async comment chains are demoralizing for junior engineers and slow.

On knowledge transfer: at OSU when I was a GTA for discrete math and mobile app development, I learned that students don't always need the answer — they need the frame for thinking about the problem. The same is true for junior engineers. When someone is stuck, I try to ask "what have you tried and what was the result?" before giving the answer. That forces them to articulate their own mental model, which usually reveals where it's broken.

Concretely at Zemoso: a junior developer was behind on test coverage near sprint end on a complex feature in the Strateos codebase — dozens of interrelated models, hard to understand without context. I picked up the test cases without being asked. Not as a favor — because writing tests on someone else's unfamiliar code when you're still building your mental model of a system is genuinely harder than writing tests for your own code. I had more context; it was the right move.

---

### Q: Walk me through a hard architectural decision and what you gave up.

The decision to use Neo4j for the identity access graph at Samay rather than staying in PostgreSQL.

The case for PostgreSQL: it was already there, the team knew it, you can do multi-hop queries with recursive CTEs. Simpler operational footprint.

The case for Neo4j: the queries that mattered to compliance auditors were multi-hop traversals — "which users have access to this repository, what's their org, and what changed in the last 30 days?" In PostgreSQL that's 3-4 JOINs with recursive CTEs that become hard to read and hard to optimize as the graph depth grows. In Cypher it's a single readable query. And the LangChain NL→Cypher translation worked well because Cypher's traversal patterns map cleanly to how auditors described their questions.

What I gave up: operational simplicity. A separate Neo4j instance per tenant adds infrastructure overhead — provisioning, credentials in Secrets Manager, VPC configuration, monitoring. I had to own all of that.

Was it right? For the access intelligence use case, yes — the query expressiveness and the NL→Cypher translation quality justified the overhead. For simpler relationship queries I'd have stayed in PostgreSQL. The rule: add a graph store when the most important queries are relationship traversals, not when you can do it with JOINs.

---

### Q: What motivates you? Why are you looking now?

Two things have driven my best work: a tight feedback loop between what I build and real outcomes, and the challenge of making AI systems genuinely reliable in production rather than demo-ready.

The LLM space is full of prototypes that don't survive contact with real users — hallucinations, bad citations, outputs that look good but can't be trusted. I'm motivated by closing that gap: the eval harnesses, the grounding mechanisms, the evidence trails that make an AI feature trustworthy enough to put in front of practitioners who depend on it.

EM1 is exactly that problem in a domain where the stakes are real. When an Emergency Manager's EOP has a flaw that EM1's Evaluate module missed, the downstream effect is real preparedness. When the system surfaces a contradiction between two plans that would have caused confusion during an actual incident, that's impact that doesn't come from most engineering jobs.

On timing: I've been building at Epik and learned a lot, but I want to be on a smaller team where I'm shaping the product and architecture from close to the beginning — not implementing into a mature codebase. EM1 at 12 people, 40+ real customers, with the compliance module as the near-term focus — that's the moment to join.

---

### Q: Tell me about a time something broke in production that was your fault.

At Samay, the identity event ingestion pipeline was silently dropping events under load. No errors, no alerts — the pipeline looked healthy. We found it because an auditor noticed that a user's access history had gaps in a compliance review. That's not how you want to discover a bug.

The root cause: a Spark job hitting memory limits was silently discarding overflow batches instead of failing noisily. The error handling was too defensive — catch-all that logged and continued. My fault for writing that error handling pattern without thinking through what "continue" meant at the pipeline level.

Fix: reduce batch size, change the catch to re-raise memory errors so they're loud, add end-of-pipeline reconciliation that counted events at ingestion vs. output and paged if they didn't match.

The more important fix: I added the reconciliation pattern across other pipelines too. If one could fail silently, others could. That's the lesson I actually needed — silent failures erode trust slowly and get discovered at the worst time. Loud failures are better. Make your systems fail visibly.

---

### Q: How do you handle unclear or changing requirements?

Short version: I build the smallest thing that generates real feedback, and I hold the architecture flexible around the parts I expect to change.

At Samay, when the client changed the priority control set mid-build, I was frustrated initially — I had three controls working, was mid-build on generalizing the Lambda. But because I had structured the data collectors as independent modules (`aws_collector.py`, `integration_collector.py`) and the LLM analysis as a function that took a control ID + data payload, the architecture was already generic. Swapping which controls were tested was mostly a prompt change and a collector configuration update — not a rewrite.

The practice: when I'm building something, I try to identify which parts are likely to change (control IDs, prompt language, which data sources) vs. stable (the Lambda invocation pattern, the Step Functions orchestration, the Pydantic output schema). I hold the stable parts firm and build the changeable parts to be easy to swap. Requirements don't change because people are irrational — they change because you learn things in production you couldn't know from a spec. Building for that is just realistic.

---

### Q: What does good code review look like to you?

Good code review teaches something, catches something real, and doesn't waste the author's time on style votes.

What I look for: boundary errors (missing validation at API inputs, edge cases the author didn't see), security patterns (secrets in environment variables, SQL query construction), the schema decisions that will be expensive later, and places where the code works but will be confusing to the next engineer in it.

What I don't use code review for: formatting, naming conventions that don't affect readability, or anything a linter should catch. Those should be automated out of the review process.

One concrete habit: I leave a comment ratio in mind — if a PR has more than 3-4 blocking comments from me, I ask for a sync call instead of building up a thread. Long comment chains slow down junior engineers and create adversarial energy. A 20-minute call resolves more, faster, and leaves people feeling helped not criticized.

At Epik I led code reviews for a 6-engineer team. The goal I held: a developer should be able to read a review comment I left 6 months ago and understand not just what I wanted changed but why.

---

### Q: How do you think about the Deconflict feature?

*(See Section 4 above — have that answer ready. This is a product-thinking question, not just technical.)*

The product framing: agencies with multiple plans often wrote them at different times, with different authors, without a systematic cross-check. The EOP says the Director activates the EOC. The COOP says the Deputy Director does. Both documents passed their individual reviews. Neither individual reviewer knew about the conflict.

This is a problem that's invisible without automated cross-document analysis. It's also a problem where the stakes are real — during an actual disaster, a first responder reading the wrong plan could take the wrong action. Surfacing these contradictions during the planning phase, not the incident phase, is the value.

The engineering challenge is making the detection precise enough to be useful and not noisy. Generating false-positive contradictions ("Section 3 says 'notify staff' and Section 7 says 'alert personnel' — contradiction!") would undermine trust in the feature quickly. The topic clustering step is load-bearing for precision.

---

## SECTION 10: QUESTIONS TO ASK GUNNAR

> Ask 3-5. These signal you've thought about their specific hard problems.

**Architecture & Product:**
1. "The crosswalk module — are you chunking plans structurally (section-level) or naively by token count? I'd expect structural parsing to be the harder part of making the citations trustworthy."
2. "For Deconflict — are you doing cross-document contradiction detection today or is that upcoming? I'm curious whether you're modeling section relationships as a graph or doing pairwise LLM comparison."
3. "The 500-2000 page plans — how are you handling the retrieval precision problem? I'm thinking about hierarchical indexing, but curious what you've found works at your doc sizes."

**Team & Engineering:**
4. "You mentioned 2 early-career engineers. How do you think about mentoring on a small team — is that structured or organic? I want to understand what supporting them well would look like."
5. "Coming from OpenSesame and Olo — both real production B2B SaaS at scale — what engineering habits from those environments are you deliberately bringing to EM1, and what are you leaving behind?"

**Domain & Roadmap:**
6. "The AAR corpus — agencies generate After Action Reports after incidents. Is the ingestion of AARs into the knowledge base self-serve today, or is that curated by your team?"
7. "What's the biggest technical problem on the roadmap that an engineer joining now would own end-to-end?"

---

## SECTION 11: RAPID-FIRE ALIGNMENT TABLE

| What Gunnar Said / Needs | Your Angle |
|---|---|
| "Vanta-style compliance module" | "I built this at Samay — control scoring, evidence collection, LLM-grounded verdicts, controls dashboard. The mapping to FEMA guidelines instead of SOC2 controls is a configuration change." |
| "Graph-RAG" | "I built the graph layer at Samay — Neo4j for identity traversal, NL→Cypher via LangChain. My take: right for multi-hop queries, overkill for single-doc retrieval." |
| "Sentence-level citations" | "That's the evidence-gating pattern — LLM must quote the source, schema-validated. I used this at Samay and in the take-home project." |
| "Human in the loop" | "Correct call for high-stakes domains. I built compliance systems where auditors verify every LLM output. Same principle." |
| "4 engineers including founder" | "Samay was effectively solo. I owned CDK, pipelines, frontend, and LLM layer. That's the environment I built in and prefer." |
| "Mentor junior engineers" | "OSU GTA for a year, picked up test coverage for struggling junior at Zemoso, code review discipline that teaches not just flags." |
| "Full-stack ownership" | "Not 'I own the backend.' I own the CDK stack, the Lambda suite, the API, and the React UI. All of it." |

---

## SECTION 12: OPENING & CLOSING

### Opening (if he asks you to go first):
"Happy to. I'm Neel — six years full-stack, last two deep in AI systems. The most directly relevant work is at Samay Systems where I was effectively the sole engineer on a compliance automation platform. The core of it was: collect evidence from multiple data sources, assemble it into a grounded context, send it to an LLM to generate a scored compliance verdict with citations. When you describe the EM1 Evaluate module — automated FEMA crosswalk, Smart References to specific plan pages — that's the same system design in a different domain. I've been curious about this conversation since the first call."

### Closing:
"This has been exactly the kind of technical conversation I was hoping for. What you're building — grounded AI with citation accountability in a domain where wrong answers have real stakes — is the problem I care about. I'd love to keep moving forward."

---

## SECTION 13: LOGISTICS & MINDSET

- **Length:** 60-90 min. Give concise answers first, expand when he follows up. Don't monologue.
- **Energy:** Direct, confident, concrete. Skip hedging ("I think maybe..."). Gunnar is a CTO — talk to him as a peer.
- **When you don't know something:** "I haven't worked with that specifically, but here's how I'd think about it..." is always better than a gap or a bluff.
- **The junior engineers question:** Don't skip this. It's a proxy for "will you slow our team down or accelerate it."
- **Timing:** Wed June 10. 3 days. Read this twice on Monday, read only the answers you feel weakest on Tuesday, skim the full doc Wednesday morning.

---

*Generated June 7, 2026 — EM1 Round 2 Prep*

---

## SECTION 14: ASYNC JOB ARCHITECTURE

> **High-probability question.** Gunnar shipped at Olo — async-first architecture for restaurant orders. He knows a 2000-page plan crosswalk is not a synchronous request.

### The Question (several forms):
- "How would you handle a plan evaluation that takes 5 minutes? You can't block an HTTP request for that."
- "Walk me through the request lifecycle for triggering a crosswalk evaluation."
- "What happens if an evaluation job fails halfway through?"

### The Answer:

The crosswalk evaluation is a long-running background job, not a synchronous API call. Here is the architecture I would use:

**Request / Response split:**
The frontend submits a plan evaluation request — `POST /evaluations` — and gets back immediately with a job ID and status `QUEUED`. No waiting. The client either polls `GET /evaluations/{id}` on an interval, or we push progress via a WebSocket or SSE stream as each guideline completes. I have built the streaming side of this — at Epik the real-time triage dashboard used WebSockets to push results as the pipeline processed events. Same pattern.

**Job queue:**
The API handler writes a job record to PostgreSQL (`evaluation_jobs` table: `id`, `agency_id`, `plan_id`, `status`, `created_at`, `updated_at`) and publishes a message to SQS. A worker (Lambda or ECS task, depending on duration) consumes from SQS and processes the job. SQS gives you durability — if the worker crashes, the message is not lost, it reappears after the visibility timeout and another worker picks it up.

**Granular progress:**
The job processes one guideline at a time and writes each result to the `evaluation_results` table as it completes. The polling endpoint returns both the overall status AND the count of completed vs. total guidelines. That way the UI can show a real progress bar: "47 of 150 guidelines evaluated" rather than a spinner. This matters for a 5-minute job — users need to know something is happening.

**Failure handling:**
At the job level: three retries with exponential backoff for transient failures (LLM API timeout, S3 read error). If all three fail, status → `FAILED`, error reason stored, agency notified.
At the guideline level: a failure on one guideline should not fail the entire evaluation. Write `INCONCLUSIVE` for that guideline with the error, continue. The evaluation completes with a note: "3 guidelines could not be evaluated — review manually."

**Idempotency:**
If an agency triggers the same plan evaluation twice (double-click, retry), the second request should detect an in-flight job for the same plan version and return the existing job ID rather than starting a duplicate run. Cheapest implementation: unique constraint on `(agency_id, plan_id, plan_version_hash)` in the jobs table.

At Samay, the Step Functions orchestration handled exactly this pattern for the compliance pipeline — fan out per tenant, each execution independent, failed executions visible in the Step Functions console without affecting others. SQS + worker is simpler at EM1's current scale, with Step Functions as the natural migration when you need more complex branching logic.

---

## SECTION 15: SCALABILITY & LLM COST MANAGEMENT

> **Gunnar came from scale. He is hiring for someone who thinks ahead, not someone who scales on fire.**

### The Question:
- "What breaks first if EM1 goes from 40 agencies to 400?"
- "A full crosswalk on a 2000-page plan triggers 150 LLM calls. How do you think about cost?"
- "How does the system perform as the document corpus grows?"

### The Answer (think in layers — compute, storage, cost):

**What breaks first at 10x scale:**

*Embedding compute:* Every new plan upload needs to be chunked and embedded. At 40 agencies this is sporadic. At 400 it becomes a sustained background workload. The fix: async embedding pipeline (SQS → worker), not synchronous on upload. Embedding jobs queue independently of the user-facing API. Already the right pattern — just needs to be designed for it from the start.

*pgvector query performance:* Approximate nearest neighbor search with IVFFlat in pgvector degrades as the vector count grows — the index needs to be rebuilt periodically as data volume increases, and the number of lists configured at index creation time becomes a tuning concern. At 400 agencies with large corpora, you would monitor query time and either tune the HNSW index parameters or migrate to a dedicated vector store like Pinecone. The schema is the same — swapping the retrieval backend is a contained change if you have an abstraction layer.

*LLM cost — the real concern:* A full crosswalk on a 2000-page plan against 150 FEMA guidelines = 150 LLM calls per evaluation run. If 400 agencies each run one evaluation per month, that is 60,000 LLM calls per month — significant cost, especially with a large model.

Three levers I would pull:

1. **Caching at the guideline level.** FEMA guidelines are stable — they do not change week to week. If a plan section has not changed since the last evaluation, there is no reason to re-run the LLM evaluation for that guideline. Cache the result keyed on `(guideline_id, chunk_hash)`. On re-evaluation, only run the LLM for guideline/section pairs where the content has changed. This alone could reduce repeat evaluation costs by 60–70%.

2. **Model tiering.** Not every step needs a frontier model. Classification (which section is relevant to this guideline?) can run on a small, fast, cheap model — Llama 3 8B via Groq, for example. The synthesis step (evaluate and write the verdict with evidence quote) needs more reasoning capacity — Claude Haiku or GPT-4o-mini. The final narrative summary for the agency report might warrant a larger model. I used this exact tiering at Samay: classification prompt vs. full analysis prompt were different model calls.

3. **Batch evaluation scheduling.** Not all agencies need real-time evaluation. A "scheduled monthly evaluation" workload can be batched during off-peak hours at lower cost than on-demand real-time.

**Storage at scale:** Plans are large PDFs. Store raw documents in S3, metadata in PostgreSQL. Never put binary content in PostgreSQL — it is not a blob store. S3 with lifecycle policies (move old plan versions to Glacier after 90 days) keeps storage costs reasonable. At Samay every document went to tenant-specific S3 buckets with metadata in PostgreSQL; same pattern here.

---

## SECTION 16: TESTING STRATEGY & OBSERVABILITY

> **4-person team, no dedicated QA. He needs to know you think about quality without process overhead.**

### The Question:
- "How do you maintain test coverage on a small team moving fast?"
- "How do you know the crosswalk system is working correctly in production?"
- "How do you test an LLM system? You can not unit test an LLM."

### Testing Strategy Answer:

I split testing into three layers for an LLM-integrated system, and I think about the cost/value of each layer explicitly on a small team:

**Layer 1 — Deterministic unit tests (fast, cheap, always run):**
Everything that is NOT the LLM call is deterministic and should be unit tested. Chunk metadata extraction — does this parser correctly identify Section 4.2 as starting on page 91? Pydantic schema validation — does the output model reject a missing `evidence_quote`? Guideline store CRUD — does the right guideline get retrieved by ID? These are fast, cheap, and catch regressions. I write these by default.

**Layer 2 — Integration tests against a fixture LLM (slower, run on merge):**
Mock the LLM call with a fixture response. Test the full evaluation pipeline end-to-end with a small test plan document and a small test guideline set. Validates the orchestration logic — job creation, chunk retrieval, result writing, status updates — without burning real LLM API tokens on every test run. At Samay I used a local fixture server for MCP tool calls in the take-home project for exactly this reason.

**Layer 3 — Eval harness with golden dataset (periodic, production-grade):**
A set of known plan/guideline pairs with human-verified correct verdicts. Run the full LLM pipeline against this set and track: citation accuracy (is the evidence quote actually in the plan?), verdict accuracy (does PASS/FAIL match human judgment?), hallucination rate (does the model assert findings not in the retrieved context?). Run this before every significant prompt change or model upgrade, not on every commit. I built this at Epik with Langfuse — dashboard plus regression alerts. This is what gives you confidence that a prompt change improved things vs. broke them.

**What I do NOT test exhaustively on a small team:** every edge case in the LLM's reasoning. The LLM is non-deterministic — you test the system around it, not the model itself.

### Observability Answer:

For an LLM-integrated system, standard APM is necessary but not sufficient. I instrument three things:

**System health (standard):** Request latency, error rates, job queue depth, worker throughput — standard CloudWatch or Datadog. An alert if the job queue is growing and workers are not draining it.

**LLM pipeline health (custom):** Per-evaluation-run metrics: total guidelines evaluated, PASS/PARTIAL/FAIL/INCONCLUSIVE counts, average evaluation latency per guideline, total token usage and estimated cost. Written to the `evaluation_runs` table and visible in a simple internal dashboard. At Samay the equivalent was reconciliation counters at each pipeline stage — events in vs. events out, alerting on mismatch. The principle is the same: make the pipeline's behavior numerically observable, not just pass/fail.

**Citation quality drift (hardest, most important):** Run a sample of production evaluations weekly through the golden dataset comparison. If citation accuracy starts drifting — even if the system looks healthy by latency/error metrics — you catch it before customers notice. This is the silent failure mode: the system keeps running and returning results, but the results are getting worse. At Samay the equivalent was a compliance auditor noticing access history gaps — that is the worst way to discover a quality regression. Proactive quality monitoring catches it first.

---

## SECTION 17: DOMAIN ONBOARDING — EMERGENCY MANAGEMENT

> **This question is certain. You have zero EM domain experience. He knows this and will ask about it. The right answer is not "I'll read FEMA's website" — it is a specific, credible onboarding strategy.**

### The Question:
- "You have not built for emergency management before. How would you approach learning this domain?"
- "The team has EM operators alongside engineers. How do you work with domain experts to close that gap?"

### The Answer:

I have been in this situation before — at Samay I came in with zero compliance domain knowledge. SOC2, NIST, ISO27001 controls were not familiar territory. The way I closed it was not by reading documentation in isolation — it was by sitting with the people doing the actual work and asking the right questions.

The most useful question I asked the compliance auditor at Samay was not "what data do you need?" It was: "Walk me through a real audit, step by step, as if I am a new auditor learning the job." That session gave me the mental model I needed to design the data collection pipeline correctly. No requirements doc would have given me that.

I would apply the same approach at EM1. Concretely:

**Week 1:** Sit with one of the EM operators on your team and ask them to walk me through a real plan review — how they read an EOP, what they look for in each section, how they use the Evaluate module today, where it falls short. Shadow a customer call if possible. I am not trying to become an EM expert in a week — I am trying to understand the workflow well enough to build for it correctly.

**Early artifacts I would read:** One real EOP (even a public one), the FEMA Comprehensive Preparedness Guide, one After Action Report. Not to memorize — to have the vocabulary and understand the document structure before I start building the ingestion pipeline.

**Ongoing:** I would ask your EM operators to review any feature I build that touches the evaluation output before it ships. The engineer can build the right system; the domain expert tells you if the system is asking the right question. That is the division I had at Samay with the compliance auditors and it made the product significantly better than what I would have designed alone.

The short version: I close domain gaps by getting close to the people who live in the domain, not by reading about it in isolation. I have done this in compliance and it worked. I would do it the same way here.

---

## SECTION 18: SHORTER QUICK-FIRE ANSWERS

### Q: What does "done" mean to you?

Done means it is in production, tested, monitored, and I could explain it to the next engineer who has to touch it. Not done means: works on my machine, works in staging, deployed but not observed. Done is the version that can break at 2pm on a Friday and I can diagnose it without a runbook.

On a small team, I also include: does the person who will maintain this have what they need to do so? If I shipped a feature with no tests and no documentation and left the team, that feature is not done — I just moved the cost.

---

### Q: How do you approach technical debt on a small team moving fast?

Debt falls into two categories and I treat them differently.

**Load-bearing debt** — infrastructure that is creaking, schema decisions that are starting to hurt, the click-ops AWS setup that has no IaC — this accrues compound interest. At Samay I migrated the entire infrastructure to CDK stack by stack specifically because not having IaC was starting to cost more time every sprint than the migration would take. I identify this kind of debt early and make the case for addressing it before it becomes an emergency.

**Cosmetic debt** — ugly but functional code, imperfect naming, tests that could be better structured — I leave this alone when velocity matters. A small team shipping fast cannot gold-plate everything. The discipline is knowing the difference between debt that is getting more expensive over time and debt that is just aesthetically unpleasant.

The honest signal I use: if I am explaining the same piece of code or architecture to a new person for the second time and they look confused, that is debt that needs to be fixed — it is actively slowing the team down.

---

### Q: What does a good API look like to you?

Three things: predictable, honest about failures, and versioned from day one.

Predictable: consistent naming, consistent response shapes, consistent error codes. If `GET /evaluations/{id}` returns `{status, created_at, results}`, then `GET /plans/{id}` should follow the same envelope. A developer should be able to guess your API without reading docs.

Honest about failures: `400` for bad input the caller can fix, `422` for validation errors with field-level detail, `500` for things we broke, never a `200` wrapping an error. I have debugged too many systems where a `200 {"error": "something failed"}` pattern hid production failures from monitoring.

Versioned from day one: a `/v1/` prefix costs nothing to add at the start and is very expensive to retrofit when you have 40 agency customers relying on an unversioned API. At EM1 specifically, agencies may have their own tooling or integrations — changing API shapes without a version is a support incident waiting to happen.

---

### Q: Tell me about a time you pushed back on a technical direction with leadership.

At Monarch Tractor, the decision was between Workato, Boomi, and AWS native for the HRMS sync workflow. I had calls with all three vendors. Coming out of those conversations, my recommendation was Workato — it was purpose-built for multi-system HRMS integrations, the error handling was mature, and I could see exactly what I would be building from scratch with AWS Lambda that Workato had already solved.

Leadership picked AWS. Budget.

My first reaction was that we would spend more engineering hours building what Workato had already solved. I said that explicitly, with specifics: "the Lambda layer dependency issues alone will cost us a week." And parts of that were true — I had to containerize just to run PowerShell, I wrote custom error handling from scratch, the UKG API bug required a vendor ticket to resolve.

But I came to understand why the decision was right in context. The team already had AWS expertise and infrastructure. The CloudWatch and EventBridge audit trail was actually better for an HR system's compliance requirements than Workato's logs would have been. When you are managing employee onboarding and offboarding, you want every operation logged in a system your security team already audits. I had not fully weighed that when I pushed back.

What I took from it: my analysis was technically correct and contextually incomplete. Leadership had constraints — budget, team skills, existing infra, compliance requirements — that I did not have full visibility into. Pushing back clearly was right. Accepting the decision and building it well was also right.

---

### Q: How do you balance shipping fast with not breaking things?

I think about this as: move fast on the parts that are easy to change, be deliberate on the parts that are hard to undo.

Schema decisions, API contracts, and infrastructure choices are hard to undo — especially with 40+ real customers on the platform. I slow down on those and make sure the decision is right before committing. I will ask an extra question, propose two options to Gunnar, or write a short DECISIONS.md entry before building. That 30-minute investment is cheap relative to a migration later.

Feature implementation — the actual code inside a well-designed API — is easy to change. I move fast here. Ship something that works, get feedback from a real user, iterate. The Samay compliance testing system started as a single-control proof of concept that ran in a notebook. It was ugly. It told us whether the approach was right before we invested in production architecture. That is the sequence I try to follow.

The summary: nail the contracts, move fast on the implementation.

---

*Appended June 7, 2026 — Sections 14–18: Async, Scalability, Testing/Observability, Domain Onboarding, Quick-Fire*

---

## SECTION 19: UPDATED CONTEXT — WHAT'S ACTUALLY BUILT VS. WHAT YOU'RE BUILDING

> **Read this before anything else. It reframes several answers.**

### The current state (what exists today):

| Component | Current Reality |
|---|---|
| Core AI | A "simple RAG" — indexes large EM PDFs (500–2000 pages), retrieves relevant passages in the EM domain |
| Document library | Aggregates public plans + customer-contributed docs; agencies can cross-share non-competing incident docs |
| Compliance crosswalk | A SEPARATE product — breaks FEMA requirements into checklists, validates plan against them |
| Current intake | Plans submitted via **email or manual upload**; compliance checks only run after a **human manually triggers** them |
| Customer base | **60+ agencies** (state, county, city) — update any mention of "40" |
| Evaluation scale | ~111 guidelines per evaluation run (website shows All: 111, Passed: 24, Needs Attention: 39) |

### What this role is building:

| Feature | What It Actually Is |
|---|---|
| Vanta-style compliance module | **Self-serve form intake replacing the current email/manual flow** → automated trigger → async evaluation → scored results dashboard |
| Agent "skills" | Workflow-specific guided capabilities for the AI agent: e.g., walk a user through plan creation, guide an AAR review — multi-step structured conversation with state, not just Q&A |
| RAG improvements | Extend and improve the existing "simple RAG" — better retrieval precision, structural awareness, cross-doc reasoning |
| Library enhancements | Better cross-sharing, search, and integration between library and agent |

### How this sharpens existing answers:

**Crosswalk system design (Section 1):** You are not designing from scratch — you are replacing a human-in-the-loop manual process. The intake step (the form) is the first thing to build. The trigger is currently human; you are automating it. This is the framing Gunnar wants to hear: "I understand the current flow is email/manual trigger, and the module is replacing that with self-serve intake + automated trigger + async evaluation pipeline."

**Async job architecture (Section 14):** Even more important now. The current system only runs when a human clicks a button. The new system needs to handle concurrent submissions from 60+ agencies without a human coordinating. Job queue is not optional — it is the core architectural change from the current model.

**LLM cost (Section 15):** With 111 guidelines per run, 60+ agencies, and monthly evaluation cadence, that is 6,600+ LLM calls per month at current scale, scaling to 66,000+ at 10x. The caching strategy (skip re-evaluation if plan section + guideline pair has not changed) is the primary cost lever.

---

## SECTION 20: AGENT SKILLS ARCHITECTURE

> **New product direction — not covered anywhere in current prep. High probability he mentions this.**

### The Question (likely form):
- "We want to add workflow-specific skills to the AI agent — things like guiding an EM through plan creation or an AAR review. How would you think about building that?"
- "How do you go from a pure Q&A RAG agent to a guided multi-step workflow agent?"

### The Answer:

The distinction here is between a **reactive agent** (user asks a question, agent answers) and a **proactive workflow agent** (agent guides a user through a structured process with multiple steps, memory across turns, and different tool calls at each stage).

The architecture shift is from stateless Q&A to **stateful conversation with a workflow graph.**

**How I would structure it:**

**State schema first.** Each "skill" has a state object that persists across the conversation: where the user is in the workflow, what has been collected so far, what is still needed. For a plan creation skill, that state might be: `{current_section: "hazard_identification", completed_sections: [...], draft_content: {...}, gaps: [...]}`. This state lives in the session, not in the LLM's context window.

**Workflow graph.** Each skill is a directed graph of steps. A node is a stage in the workflow (e.g., "gather jurisdiction info," "identify hazards," "draft mitigation actions"). An edge represents a transition triggered by the user's response or a tool call result. This is exactly what LangGraph provides — I built LangGraph-based agentic workflows at Epik for security triage pipelines that had branching logic based on alert classification. Same pattern applies here.

**Tool calls per step.** At each node the agent has access to a specific, scoped set of tools relevant to that step — not every tool the agent has. For the "hazard identification" step: retrieve relevant peer agency hazard sections from the library, query FEMA doctrine for that hazard type, check the agency's existing plan for what they already have. For the "mitigation actions" step: different tools, different retrieval context. Scoping tool access per step keeps the agent focused and reduces noise.

**Persistence and resumability.** A plan creation workflow is not done in one session. The user will come back. State needs to be persisted to PostgreSQL between sessions, keyed on `(agency_id, skill_type, workflow_instance_id)`. When the user returns, load the state and resume. This is a meaningful architectural requirement that a stateless Q&A agent does not have.

**At Samay** I built n8n agentic workflows for daily compliance summary reports — multi-step, MCP-based tool calling, state across steps. The concept is identical; LangGraph is a more developer-native implementation of the same pattern for code-first teams.

**The practical build order:** Start with the simplest possible skill — single-step, no branching, no resumability. Prove the pattern works end-to-end (user input → structured state → targeted retrieval → guided response). Then add persistence and multi-step flow. Then add branching. This is the same "ugly scripts first, architecture second" progression that worked at Samay.

---

## SECTION 21: PRODUCT KNOWLEDGE ADDITIONS

> Update your mental model of the product with these specifics from website + conversation.

**Custom evaluations:** Agencies are not limited to the FEMA library. They can build their own crosswalk checklists — custom guidelines for state-specific requirements, local ordinances, or agency internal standards. This means the guideline store is not a static FEMA dataset; it is a multi-tenant, user-editable store. Architectural implication: guidelines need an `owner` field (system vs. agency), and the crosswalk engine needs to run against the right guideline set per agency.

**Smart References UI:** The Evaluate module shows exactly which page in the plan answers which FEMA guideline. This is the customer-facing display of the `page_reference` field in the evaluation result. When you talk about citation grounding and evidence-gated output, this is the UI it surfaces into.

**The free evaluation entry point:** On the website, agencies can submit a plan for a free evaluation (drag-and-drop, max 25 MB). This is the top-of-funnel acquisition flow — it also tells you the file size constraint the ingestion pipeline needs to handle.

**E03 is called "Chat" in the nav:** The Operationalize module is surfaced to users as a chat interface — real-time Q&A over their uploaded documents. This is the module that the agent skills are extending.

**Updated traction:** 60+ agencies, not 40. Use this number.

---

*Appended June 8, 2026 — Sections 19–21: Current state context, agent skills architecture, product knowledge updates*

---

## SECTION 22: FULL END-TO-END SYSTEM DESIGN — VANTA-STYLE COMPLIANCE MODULE

> **This is the master answer. Section 1 covers the AI/data layer. This covers the FULL system from intake form to human approval. Know both — he may ask either version.**

### The Question:
- "Walk me through the full flow — from an agency uploading a plan to them seeing a scored evaluation."
- "How would you replace the current email/manual trigger process end-to-end?"
- "How would you build the Vanta-style compliance module from scratch?"

### Critical framing first:

> "The current flow is: plan arrives by email, a human manually uploads it and manually triggers the compliance check. The Vanta module automates everything from intake to results — the human only re-enters at the review and approval step. That is the right place for them to be."

That one sentence tells Gunnar you understood the problem, not just the technology.

---

### The Full 6-Stage Flow:

**Stage 1 — Self-Serve Intake Form (Frontend)**

The form is the entry point that replaces email. It collects:
- Plan type (EOP / HMP / COOP / IAP / other)
- Jurisdiction and agency name (pre-populated from account)
- Plan version / effective date
- File upload (PDF, max 25MB based on current site — use presigned S3 URL for direct browser-to-S3 upload, not routing large files through the API server)
- Guideline library selection: FEMA standard, state-specific, or a custom evaluation the agency has built

The presigned URL pattern matters: for a 25MB PDF, you do not want that file moving through your API server on every upload. Issue a presigned S3 PUT URL from the backend, upload directly from the browser to S3, then the backend receives a callback/confirmation with the S3 key. This is standard and keeps the API layer thin.

On submit: `POST /evaluations` returns `{job_id, status: "QUEUED"}` immediately. The user sees a confirmation screen: "Your plan has been submitted. You will be notified when the evaluation is complete."

**Stage 2 — Async Job Queue**

The API handler writes to `evaluation_jobs`: `{id, agency_id, plan_id, plan_s3_key, guideline_library_id, status: QUEUED, created_at}` and publishes to SQS. Worker picks it up. If the agency submits the same plan twice (double-click, race condition), a unique constraint on `(agency_id, plan_s3_key_hash)` catches it and returns the existing job.

**Stage 3 — Document Ingestion (if not already indexed)**

Worker checks: has this exact plan version been indexed before (matched on file hash)? If yes, skip ingestion, reuse the existing chunk index. If no:

1. Download PDF from S3
2. Structure-aware parsing: extract section map (section number → heading → page range), not naive fixed-size chunks
3. Generate chunks at two levels: section summaries (~500 tokens) and paragraph-level chunks (~150-200 tokens with overlap), each tagged with provenance metadata: `{agency_id, doc_id, section, heading, page, chunk_index}`
4. Embed all chunks, write to pgvector (or Pinecone at scale), write chunk metadata to PostgreSQL
5. Write document record to `plans` table: `{id, agency_id, s3_key, file_hash, version, plan_type, indexed_at}`

**Stage 4 — Crosswalk Evaluation Loop**

For each guideline in the selected library (111 for standard FEMA HMP):

1. Retrieve top-k chunks: first query section summaries to find the 2-3 most relevant sections, then retrieve paragraph-level chunks from within those sections only (hierarchical retrieval)
2. LLM evaluation call with Pydantic output schema:
   - Input: guideline text + retrieved chunks with metadata
   - Output: `{verdict: PASS|PARTIAL|FAIL|INCONCLUSIVE, evidence_quote: str, page_reference: str, gaps: list[str], confidence: float}`
3. Evidence gate: if `evidence_quote` is empty or not a substring of the retrieved context → override verdict to `INCONCLUSIVE`, flag for mandatory human review
4. Write result to `evaluation_results`: one row per guideline
5. Update job progress counter: `completed_guidelines += 1`
6. Update job status to `COMPLETE` when all guidelines are done; `FAILED` if unrecoverable error

LLM cost optimization: if the same `(guideline_id, chunk_hash)` pair was evaluated in a previous run with the same plan version, reuse the cached result. Only run LLM for guideline/section pairs where content has changed. This is the primary cost lever — repeat evaluations should be 60-70% cheaper than first-time runs.

**Stage 5 — Human-in-the-Loop Review (The Right Bottleneck)**

This is not optional and is not a concession to uncertainty — it is a deliberate design choice for a high-stakes domain. The output of Stage 4 is the LLM's assessment, not the final verdict.

The review UI surfaces:
- **PASS with high-confidence evidence** → shown clearly, minimal friction. EM can accept with one click.
- **PARTIAL / NEEDS ATTENTION** → highlighted, evidence quote shown, gaps listed, EM reviews and can: accept LLM assessment, override with their own judgment + annotation, or flag for more context
- **INCONCLUSIVE** → mandatory review, cannot be submitted without human resolution. Either the section exists and the LLM couldn't find it (retrieval gap) or the section is genuinely missing.
- **FAIL** → shown with specific gaps from the LLM, EM reviews what is missing

The principle: **automate the tedious, preserve the judgment.** Finding which sections of a 2000-page plan might satisfy 111 guidelines and pre-populating evidence quotes is the tedious part. Deciding whether the agency's specific context meets the requirement is the judgment part. The LLM handles the first; the human owns the second.

At Samay this was the same model — the automated control testing system generated the evidence and score, but the compliance auditor reviewed and signed off before it went into a compliance report. The LLM is a first reviewer, not the final one.

**Stage 6 — Report Generation & Submission**

Once the EM has reviewed and resolved all PARTIAL/INCONCLUSIVE items:
- Generate a structured scorecard: overall pass rate, section-by-section breakdown, guideline-by-guideline results with evidence quotes and page references
- Export to PDF for FEMA submission (or whatever the agency's compliance body requires)
- Store evaluation history: `{agency_id, plan_id, run_id, overall_score, run_date}` — enables the "you improved from 68% to 84% since last submission" trend view
- Optionally: notify the agency via email/webhook when the evaluation is ready for review

---

## SECTION 23: HUMAN-IN-THE-LOOP — DESIGN PHILOSOPHY

> **EM1's core product philosophy is "human in the loop." He WILL ask about this. Have a principled answer, not a vague one.**

### The Question:
- "How do you think about the role of human review in an AI system like this?"
- "How do you decide what the AI does vs. what the human does?"
- "How do you prevent the LLM from making decisions it shouldn't?"

### The Answer:

Human-in-the-loop is not a risk mitigation — it is a product design choice based on the nature of the task.

The relevant distinction is between **tasks where the AI can be the final decision-maker** and **tasks where the AI should be a first-pass reviewer that accelerates a human decision.** The crosswalk evaluation sits firmly in the second category. Here is why:

A FEMA compliance verdict is not just a logical inference from text — it is a professional judgment about whether a plan meets a requirement in context. "Does this EOP address hazard identification adequately?" requires understanding the jurisdiction, the local hazard profile, the agency's history, and FEMA's current assessment priorities. An LLM has none of that context. It has the document and the guideline text.

So the architecture I design for is: **the LLM does the work that would take a human expert days (reading 2000 pages, matching each section to 111 guidelines, extracting evidence quotes), and the human does the work that requires contextual judgment (deciding whether the evidence is sufficient for this specific agency's situation).** The human is still doing meaningful work — just not the mechanical, tedious part.

The specific design decisions that enforce this:
1. `INCONCLUSIVE` verdict cannot be submitted without human resolution — no bypass
2. Evidence quotes are surfaced verbatim from the plan, not paraphrased — human can verify in 5 seconds by checking the page reference
3. Human annotations and overrides are stored alongside LLM verdicts — the final record shows what the LLM said AND what the human decided. That audit trail is important if an agency is submitting to FEMA.
4. Confidence scores flag low-confidence verdicts even when they are PASS — the system is honest about uncertainty

**When to reduce human review over time:** As the system accumulates a history of LLM verdicts that match human review decisions for a specific agency's plan type, you can surface confidence levels that reflect that calibration. High-confidence PASS verdicts on stable sections that have not changed from the last accepted evaluation can reasonably become one-click approvals. The human is still in the loop; the loop is just shorter for routine cases.

---

## SECTION 24: AFTER ACTION REVIEW (AAR) PIPELINE

> **AARs are explicitly part of the product (E03 knowledge base, agent skills roadmap). If he asks about system design beyond the crosswalk, AAR pipeline is the next most likely topic.**

### The Question:
- "How would you think about the AAR ingestion and retrieval pipeline?"
- "How would you build the after-action review skill for the agent?"
- "AARs are key to how agencies learn — how does that feed back into the system?"

### What AARs Are (and why they're architecturally interesting):

An After Action Report is written after an incident — it documents what happened, what worked, what didn't, and what should be improved. AARs are:
- **Unstructured narrative** — unlike plans which have defined sections, AARs vary widely in format
- **Incident-typed** — an AAR from a flood response is relevant to other agencies planning flood response; irrelevant to an active shooter scenario
- **Lessons-first** — the most valuable content is the "what we learned / what we'd do differently" sections, not the incident timeline
- **Sharable across agencies** (with consent) — non-competing agencies' AARs are valuable learning material; EM1's library feature already enables this

### Pipeline Design:

**Ingestion (same base as plan ingestion, different metadata):**

AAR upload → S3 → structure-aware parsing (but AARs are less structured — look for section markers like "Lessons Learned," "Recommendations," "What Worked," "What Didn't Work" rather than numbered compliance sections) → chunk and embed → store in the knowledge base.

Key metadata difference: every AAR chunk is tagged with:
- `incident_type` (flood, wildfire, active shooter, public health, etc.) — either extracted by a classification LLM call or selected during upload
- `jurisdiction` (optional — for privacy/cross-share decisions)
- `incident_date`
- `source_agency_id`
- `section_type` (lessons_learned | recommendations | timeline | other) — extracted from section heading

This tagging is what makes AAR retrieval useful. "What did agencies learn from wildfire response?" → filter by `incident_type: wildfire`, `section_type: lessons_learned` → retrieve top-k. Without incident tagging, you get retrieval noise across all incident types.

**Two use cases, two retrieval patterns:**

**Use case 1 — E03 Chat:** User asks "What have agencies learned from active shooter responses?" The chat agent retrieves AAR lessons-learned chunks filtered by incident type. The answer is grounded in real post-incident reports, not training data. Citations point to specific AAR documents (agency name if shared, anonymized if not).

**Use case 2 — Plan improvement (agent skill):** After an agency runs a crosswalk evaluation and gets PARTIAL/FAIL verdicts, the plan improvement workflow can retrieve relevant AARs: "Here are lessons from similar agencies who had the same gap in their EOC activation section — how did they address it?" This turns the improvement workflow from a blank-page problem into a reference-guided one.

**The AAR review skill (stateful agent workflow):**

When an agency finishes an incident and needs to write their AAR, the agent can guide them through it:
- Step 1: Gather incident timeline (structured form — date, incident type, agencies involved, duration)
- Step 2: What worked — agent retrieves similar AARs' "what worked" sections as prompts/examples
- Step 3: What didn't work — same pattern, different filter
- Step 4: Recommendations — agent surfaces relevant doctrine and peer recommendations for the gaps identified
- Step 5: Draft generation — agent assembles a draft AAR from the collected structured inputs, formatted to standard AAR template

This is a stateful, multi-step workflow agent (LangGraph) — not a Q&A agent. State persists across the session. Each step has a targeted retrieval context (incident-type-filtered AARs, relevant doctrine sections). The human fills in what they actually experienced; the agent provides structure, examples, and draft language.

**Cross-sharing governance:**

AARs can contain sensitive incident details. The library cross-share model needs an explicit consent flag per document: `{is_shared: bool, anonymize_agency: bool, shared_incident_types: [...]}`. An agency opts in to sharing specific AARs with specific peer agencies or the whole platform. This is the same governance model as the existing document library but more granular because AARs may contain sensitive operational details.

---

*Appended June 8, 2026 — Sections 22–24: Full E2E system design, human-in-the-loop philosophy, AAR pipeline*

---

## SECTION 25: TYPESCRIPT — DEPTH ANSWER

> **EM1's entire stack is TypeScript — Next.js frontend, CDK infrastructure, likely shared types. If you say "I use TypeScript" and stop there, that's a gap.**

### The Question:
- "Walk me through your TypeScript experience."
- "How do you handle typing in a full-stack system where the frontend and backend share data shapes?"
- "How do you type LLM responses that are inherently dynamic?"

### The Answer:

TypeScript has been my default for the last two-plus years — CDK infrastructure at Samay was TypeScript, React frontends at Samay and Epik were TypeScript, and the take-home project's agent backend was Python but the frontend and tooling layer was TypeScript.

**The patterns I rely on in production:**

**Shared types across layers.** In a full-stack TypeScript system, the most expensive bugs come from the API contract drifting between frontend and backend — the backend returns `evidence_quote` and the frontend expects `evidenceQuote`, nobody notices until a user sees an empty field. The fix is a shared types package: one `types/` directory (or a monorepo package) that both the Next.js frontend and the API layer import from. One change to the type propagates everywhere. If EM1 doesn't have this already, it's an early contribution I'd want to make.

**Discriminated unions for state.** A compliance evaluation result has multiple states — `PASS`, `PARTIAL`, `FAIL`, `INCONCLUSIVE` — and each state has different fields (FAIL has `gaps`, INCONCLUSIVE has a `review_required` flag). A discriminated union models this correctly:
```ts
type EvaluationResult =
  | { verdict: "PASS"; evidence_quote: string; page_ref: string }
  | { verdict: "FAIL"; evidence_quote: string; page_ref: string; gaps: string[] }
  | { verdict: "INCONCLUSIVE"; reason: string; review_required: true }
```
Now the compiler catches every place you handle `FAIL` but forgot to handle `INCONCLUSIVE`. That's a whole class of runtime bugs eliminated.

**Typing LLM responses.** LLM output is inherently dynamic — you can't trust its shape at the TypeScript layer directly. The pattern I use: Zod schema at the API boundary that validates and types the LLM response. The schema is the source of truth; the TypeScript type is inferred from it (`z.infer<typeof evaluationResultSchema>`). If the LLM returns an unexpected shape, Zod throws at the boundary — the error is caught and handled, not silently propagated as `undefined` into the UI. This is the TypeScript equivalent of the Pydantic output schema pattern I use on the Python side.

**Strict mode.** I always enable `strict: true` in `tsconfig.json`. It forces explicit null handling — `string | null` can't be used as `string` without a guard — which surfaces the "what happens when this field is missing?" question at compile time rather than at 2am in production.

**In a Next.js App Router context specifically:** The server/client component boundary creates a type safety concern — you can't pass non-serializable values (functions, class instances) from server components to client components as props. TypeScript doesn't catch this by default; it's a runtime error. The habit is: keep server component props to plain serializable types, use `use client` boundary components as the adapters that receive server data and attach event handlers.

---

## SECTION 26: TERRAFORM vs CDK — DIRECT ANSWER

> **JD says Terraform. You have CDK. This will come up. Don't be defensive — be direct.**

### The Question:
- "We use Terraform. You have CDK experience. Is that a gap?"
- "What's your take on Terraform vs CDK? Do you have a preference?"

### The Answer:

CDK and Terraform solve the same problem — infrastructure as code — and the mental model transfers almost entirely. The syntax is different, the state management is different, the provider story is different. The underlying discipline — every resource in code, every environment reproducible, no click-ops — is the same.

My CDK experience is deep: 15+ stacks at Samay covering VPC, RDS, Lambda, Step Functions, AppRunner, ECS Fargate, Secrets Manager, S3. I've reasoned about dependency ordering between stacks, parameterized environments with context flags (`--context env=staging`), managed circular dependency problems between stacks, and debugged CloudFormation rollback failures. That reasoning process is the same in Terraform — HCL is a thinner layer over the same concepts.

**The real differences I'd be ramping on:**

Terraform's state management is explicit — the `terraform.tfstate` file (local or remote in S3/Terraform Cloud) is something you manage. CDK delegates state to CloudFormation behind the scenes. Understanding remote state backends, state locking (especially in a team context), and `terraform import` for existing resources are the Terraform-specific skills I'd build quickly.

Terraform's provider ecosystem is broader — it's cloud-agnostic, which matters when you're managing AWS and have future plans for any other cloud. CDK is AWS-native (though CDK for Terraform exists). For a company that's all-in on AWS, this is a minor consideration.

I've also written Terraform for Azure services at Samay — provisioned Azure resources alongside the AWS CDK stacks. Not deep Terraform experience, but enough to know the syntax and workflow.

**Honest ramp:** reading an existing Terraform codebase and contributing to it within a sprint. Independently writing new modules within 2-3 weeks with the existing codebase as reference.

---

## SECTION 27: FULL-STACK SHIPPING — DAY-TO-DAY ACROSS LAYERS

> **"Own and ship multiple small-to-mid-size features" — this is the role description. He wants evidence you can context-switch across backend/infra/frontend inside a normal sprint, not just one big project.**

### The Question:
- "Walk me through how you actually work across the stack day to day."
- "Give me an example of a feature you shipped end-to-end — frontend to infra."

### The Answer (Feature Story: Automated Control Testing at Samay):

The clearest example is the automated control testing feature at Samay — from the "Test Control" button in the UI down to the CDK stack that deployed the Lambda.

**The frontend slice:** I built the `FocusAreaDetail.jsx` component — the control detail page. It had a "Test Control" button that needed to trigger the Lambda, show a loading state while the job ran, then display the returned compliance score, evidence quote, and gaps inline on the page. That's a React component with async state management, optimistic UI for the loading case, and error handling for Lambda timeout.

**The API slice:** The Next.js equivalent (in our case a FastAPI backend) needed a `POST /controls/{id}/test` endpoint that accepted the control ID, invoked the Lambda asynchronously, and returned a job ID. The Lambda result was written to S3 and the frontend polled for it.

**The Lambda slice:** Python Lambda function that collected from six data sources — AWS CloudTrail, Inspector, Security Hub, EntraID, GitHub, document embeddings — assembled the payload, called AWS Bedrock, structured the output as a Pydantic model, wrote to S3.

**The CDK slice:** The Lambda's IAM role needed permissions for all six sources — CloudTrail read, Inspector read, Secrets Manager access for Neo4j credentials, S3 write for results. I wrote the CDK construct, wired the execution role, added the environment variables, and deployed. When the IAM policy was wrong, CloudWatch had the error; I fixed the policy in CDK and redeployed.

The whole feature touched four layers in four different languages and runtimes. The discipline was: understand the full data flow before writing any code in any layer, so the interfaces between layers are correct from the start. Changing an interface after you've already built both sides costs double.

**The pattern I bring to EM1:** When picking up a feature ticket, I read the full system diagram first — what touches what. I don't start at the frontend and discover the Lambda needs a new permission three days later. I trace the request all the way through, identify the changes needed at each layer, and sequence them backend-first (so the API is testable before the UI exists).

---

## SECTION 28: STAKEHOLDER INTERACTION & PRODUCT ROADMAP CONTRIBUTION

> **12-person company. Engineers talk to customers and EM operators directly. "Help shape the product roadmap" is in the role description. No stories existed for this.**

### Q: How do you work with non-technical domain experts like the EM operators on the team?

The closest parallel I have is Samay, where I worked alongside a compliance domain expert with no engineering background to design and build the automated control testing system. She thought in audit procedures and control narratives. I thought in APIs, schemas, and Lambda functions. Early on, that gap caused real friction — I'd come out of a meeting thinking I understood what she needed and build something. She'd look at it and say "that's not what I meant."

The fix was simple but took a few cycles to land on: I stopped translating her language into mine during the conversation. I asked her to walk me through a real audit, step by step, as if I was a new auditor learning the job. I took notes in her language — "we need to see that config changes were tracked and reviewed," not "CloudTrail events." Then I did the translation afterward, alone.

The six-source data model for the automated testing system came entirely out of that session. She had never heard of CloudTrail. She knew she needed to see that config changes were tracked. Those are the same thing — but only once you've done the translation carefully.

At EM1 the equivalent is the EM operators on your team. They know what Emergency Managers need; I know how to build the system. The interface between those two things is the most important relationship to get right. I'd approach it the same way: watch them use the current product before writing any code for the next feature. Ask "what's the worst part of this?" before asking "what do you want to build?"

---

### Q: Have you ever contributed to product direction, not just implementation?

At Samay, by the time I was 2-3 months in, I was the person in the room with the most context on what the system could and couldn't do. That put me in product conversations by default — not because I had a PM title, but because nobody else knew the technical constraints well enough to reason about trade-offs.

The clearest example: the team was considering adding a real-time alert feature for compliance score drops — an agency's score changes and they get notified immediately. My contribution to that conversation was: "real-time means we're re-running 111 LLM evaluations every time any plan section changes. Here's the cost implication at our current scale. Here's an alternative: delta-only re-evaluation — only re-run the guidelines whose source sections changed — which gets you 80% of the value at 15% of the cost." That's not a PM decision or a pure engineering decision — it's the place where cost, architecture, and product behavior intersect, and it requires someone who understands all three.

That's the kind of input I want to bring to EM1's roadmap discussions. Not "here's what I want to build" — but "here's what this feature actually costs to operate, here's the architectural implication of that choice, here's an alternative that might serve the same user need with less complexity." Engineers who can reason that way make product teams better.

---

### Q: Tell me about a time you had to simplify a complex technical constraint for a non-technical person.

At Epik, a senior stakeholder wanted the AI incident triage pipeline to switch to autonomous mode immediately — it was performing well in testing, why wait?

The real constraint was: in testing, the false positive rate was acceptable but not production-calibrated. In production, a false positive meant a real analyst ignoring a real threat because the system had cried wolf. That's not a UX bug — it's a security gap.

I didn't explain false positive rates or precision-recall trade-offs. I said: "Think of it like a new hire. They passed the interview — they're clearly capable. But you wouldn't let them make final calls on major incidents on day one without anyone checking their work. The two-week shadow period is the same thing — we watch what it recommends, compare it to what experienced analysts would do, and calibrate where it's overconfident before we let it act alone."

She understood immediately. The two-week shadow period became part of the plan with no further argument.

The principle: technical constraints land when they're translated into human dynamics the other person already understands. Almost everyone knows what it means to ramp up a new team member. Almost no one knows what precision-recall calibration means in a production classifier.

---

### Q: How do you think about contributing to the product roadmap as an engineer?

I think the most useful thing an engineer can bring to a product conversation is: "here's what this feature would actually cost to build and operate, and here's what the architecture would need to support it."

Most feature ideas are good in the abstract. The engineering contribution is grounding them in reality — not as a blocker, but as a constraint that shapes the design. "We could build real-time plan monitoring, but here's what that means for our LLM API bill and our infrastructure. Here's a version that gives the customer most of the value with a quarter of the complexity."

At Samay I was in those conversations regularly because I had the full-stack context no one else had. At EM1 I'd want to be in them too — especially on the compliance module roadmap and the agent skills direction, where the technical decisions have product implications that might not be visible until you've tried to build it.

The other angle: I pay attention to what's painful in what I'm building. If I'm implementing a feature and the data model is fighting me, that's signal — either the model is wrong or the feature is more complex than it appears. I surface that early rather than absorbing it silently.

---

### Q: You'd be working with EM operators who are domain experts, not engineers. What does that collaboration look like day-to-day?

The honest dynamic: they know more about the domain than I ever will. I know more about the system than they ever need to. The useful overlap is: they can tell me whether a feature is solving the right problem; I can tell them whether the solution is feasible and what it costs.

Day-to-day, that means: before I spec out a feature, I want to understand the current manual process it's replacing — not from a requirements doc, from watching someone do it. After I build something, I want to get it in front of an EM operator before it ships to customers — not for QA, for "does this match how you actually think about the problem?"

The risk I try to avoid: building technically correct features that miss the domain nuance. At Samay, the compliance chatbot I built gave technically accurate answers about access relationships — but compliance auditors didn't care about raw access data, they cared about whether the access pattern satisfied a specific control narrative. That's a domain nuance no amount of engineering can substitute for. Getting it requires being close to the people who live in it.

---

*Appended June 8, 2026 — Sections 25–28: TypeScript depth, Terraform vs CDK, full-stack shipping story, stakeholder interaction + roadmap contribution*


> [!example]- Alternate source version (html)
> ## EM1 — Round 2 Interview Prep (60–90 min Technical + Culture) 
>
>  
>
> #### With Gunnar Holwerda, CTO / Co-Founder 
>
>  
>
> Date: Wednesday June 10, 2026
>  Format: High-level tech concepts + culture fit. ~40-50 min technical, ~30-40 min behavioral.
>
>   
>
> ### CRITICAL FRAMING BEFORE YOU START 
>
>  
>
> Gunnar came from OpenSesame and Olo — real B2B SaaS at scale. He knows what "architected a system" looks like vs. "implemented tickets." He is hiring someone to hold architecture on a 4-engineer team that includes 2 early-career engineers.
>
>  
>
> You don't have "Staff Engineer" on your resume. That's fine. What you DO have is:
>
>   
> - Solo-designed and delivered a compliance automation platform from zero (Samay) 
> - Reasoned about multi-tenant isolation, graph vs. vector trade-offs, and LLM grounding in production 
> - Owned CDK infrastructure end-to-end — not just code, but the whole system  
>
> The move: articulate the WHY behind every decision you made. That's what separates someone who built something from someone who architected it. He will hear the difference.
>
>   
>
> ### THE PRODUCT YOU ARE JOINING (Keep This Crisp) 
>
>    
>
>   | Module  | What It Does 
>
>    
>
>   | Evaluate (E01)  | Automated FEMA crosswalk — evaluates each EOP/HMP section against FEMA guidelines; Smart References maps each guideline to the exact plan page answering it 
>
>  
>
>   | Improve (E02)  | Plan Library + Peer Docs (compare to peer agencies) + Deconflict (find contradictions ACROSS plans) 
>
>  
>
>   | Operationalize (E03)  | Custom knowledge base from uploaded docs + real-time answer engine with sentence-level citations 
>
>  
>
>   | Near-term focus  | Vanta-style compliance module: form-based plan intake → automated crosswalk validation → scored output 
>
>    
>
> Plan types: EOPs (master response plans), HMPs (FEMA-required mitigation plans), COOPs (continuity plans), IAPs (per-incident plans), AARs (post-incident lessons).
>  The hard part: Plans are 500–2000 pages. Agencies have multiple conflicting plans. LLM citations must be accurate — a wrong citation in an EOP is a liability.
>
>   
>
> ### SECTION 1: SYSTEM DESIGN — The Crosswalk Module 
>
>   
>
> This is the highest-risk question. He will ask this. You built this at Samay. Translate it.
>
>   
>
> #### The Question (several forms it can take): 
>
>   
> - "How would you think about architecting the Vanta-style compliance module?" 
> - "Walk me through how you'd build the automated plan evaluation system." 
> - "If you were to design the crosswalk workflow from scratch, where would you start?"  
>
> #### The Samay ↔ EM1 Translation 
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
>   | AWS infra metadata + GitHub/Jira data  | Emergency plan document sections (EOP, HMP) 
>
>  
>
>   | Evidence collection Lambda (6 sources)  | Document parsing + chunking pipeline 
>
>  
>
>   | LLM compliance scoring (Bedrock)  | Guideline crosswalk evaluation (LLM) 
>
>  
>
>   | Structured output with evidence quotes  | Smart References (guideline → exact page) 
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
> #### How to Answer (structured, ~4-5 minutes) 
>
>  
>
> "I'd think about this in four layers."
>
>  
>
> Layer 1 — Document Ingestion & Parsing
>  The hardest part isn't the AI — it's ingestion. A 2000-page EOP is structured: it has a table of contents, numbered sections, annexes, appendices. If you treat it as a flat blob and chunk naively, your retrieval will be garbage — you'll get fragments without context, sections split mid-sentence across chunk boundaries.
>
>  
>
> What I'd do: parse structure first. Extract section headings, section numbers, and page ranges as metadata before chunking content. Build a structural map: Section 4 → pages 84–112 → "Resource Management." That way every chunk I store carries: {section: "4.2", heading: "EOC Activation Procedures", page: 91, doc_id: "EOP-v3"}. That metadata is what makes sentence-level citations possible later.
>
>  
>
> At Samay I faced a version of this with multi-format policy documents — docx, PDF, RTF — where you lose structural context in conversion. The lesson was: metadata preservation during ingestion is more important than the chunking strategy itself.
>
>  
>
> Layer 2 — Dual Indexing: Vector + Structural
>  Two indexes, not one.
>
>  
>
> First: vector embeddings per chunk (using pgvector in PostgreSQL or a dedicated store). These enable semantic retrieval — "find all content related to hazard identification" even if those exact words aren't present.
>
>  
>
> Second: a structured metadata layer in PostgreSQL — one row per chunk with section, page, heading, doc version, agency ID. This enables non-semantic queries: "give me all chunks from Section 4 of this EOP" for cases where you already know what section the guideline maps to.
>
>  
>
> You need both. Vector-only retrieval misses structural queries. Structured-only misses the semantic ones. The crosswalk workflow will use both: broad semantic search to find candidate sections, then page/section metadata to form the citation.
>
>  
>
> Layer 3 — Guideline Store & Crosswalk Logic
>  FEMA guidelines are a structured artifact — they have IDs, required elements, plain-text descriptions. I'd store them as structured records: {guideline_id: "FEMA-HMP-4.2.1", text: "...", category: "Hazard Identification", required_elements: [...]}.
>
>  
>
> The crosswalk loop is: for each guideline → retrieve top-k chunks from the plan → LLM evaluation prompt: "Given this FEMA guideline and these sections from the plan, does the plan satisfy this requirement? Return: verdict (PASS/PARTIAL/FAIL), evidence_quote (verbatim from plan), page_reference, gaps (if any)."
>
>  
>
> Critically, I'd use a Pydantic output schema for this — not free-text LLM output. The model must populate evidence_quote, page_reference, and verdict as structured fields. If it can't populate evidence_quote, the verdict is INCONCLUSIVE — not hallucinated. This is the same evidence-gating pattern I used in the take-home project and at Samay. The LLM can't assert a finding it didn't retrieve evidence for.
>
>  
>
> Layer 4 — Agency Isolation & Results Storage
>  Multi-tenant from day one. Agency A's plans never appear in Agency B's retrieval. I'd use:
>
>   
> - Filtered metadata on every vector query: WHERE agency_id = ? — no cross-agency leakage at the retrieval layer 
> - Per-agency row-level security (RLS) in PostgreSQL on the results tables — defense in depth 
> - Evaluation results written to a control_evaluations table with agency_id, guideline_id, verdict, evidence_quote, page_ref, run_timestamp  
>
> That last piece — storing structured evaluation history — is what enables the UI to show "you improved from 68% to 84% compliance since your last submission" and lets agencies track progress over time.
>
>  
>
> The UI layer I've already built at Samay: controls dashboard (list view, aggregate score per framework section), detail page per guideline (verdict, evidence quote, gaps), status update, comments for human review. That translates directly to the Evaluate module.
>
>   
>
> #### Follow-up: "What would you do differently than Samay?" 
>
>  
>
> Two things:
>
>   
> -  
>
> Hierarchical retrieval — at Samay the document corpus was smaller. For 2000-page plans I'd add a coarse-to-fine retrieval step: first retrieve section-level summaries to find the right section, then fine-grained chunk retrieval within that section. This cuts down irrelevant context and improves citation precision.
>
>   
> -  
>
> Guideline dependency graph — FEMA guidelines have dependencies: "Section 4.2 is only applicable if hazard X was identified in Section 3." At Samay the controls were independent. For a proper crosswalk you want to model those dependencies so the evaluation order is correct. That's a natural place for a lightweight graph — nodes are guidelines, edges are "must satisfy before."
>
>     
>
> ### SECTION 2: GRAPH-RAG — CRISP 1-MINUTE ANSWER 
>
>   
>
> This was explicitly flagged as weak from the phone screen. Have this cold.
>
>   
>
> #### The Question: 
>
>  
>
> "You mentioned graph-RAG. Walk me through the trade-off — when is it worth the overhead vs. plain vector RAG?"
>
>  
>
> #### The Answer: 
>
>  
>
> Vector RAG and graph RAG answer different question types, and the mistake is trying to use one for both.
>
>  
>
> Vector RAG is the right default when the query is: "find content semantically similar to this." Single-hop. "What does this plan say about resource management?" Vector search is fast, straightforward to maintain, and well-supported.
>
>  
>
> Graph RAG earns its complexity when the query is multi-hop or relationship-centric: "which users had their permissions changed in the 30 days before this access event?" At Samay, that question can't be answered by semantic similarity — it requires traversal: User node → HAS_ACCESS_TO → Repository node → filtered by timestamp. Vector can't do that. Graph can.
>
>  
>
> For EM1 specifically: single-plan retrieval → vector is right. "Does Section 4.2 of this EOP satisfy FEMA guideline HMP-4.2.1?" That's semantic similarity within one document. Fast, cheap, works.
>
>  
>
> Cross-plan reasoning → this is where graph adds value. The Deconflict feature — "find contradictions across the EOP, HMP, and COOP" — is inherently relational. You're asking: "which sections across multiple plans address the same topic and give conflicting guidance?" That's a multi-hop traversal: Plan A Section 4 → addresses_topic → EOC Activation → addressed_by → Plan B Section 7 → contradicts → Plan A Section 4. Graph traversal makes that query clean. Trying to do it with vectors and pairwise similarity comparison across every chunk combination is O(n2)O(n^2)O(n2) and noise-prone.
>
>  
>
> At Samay I used Neo4j for exactly this pattern — identity events as nodes, typed relationships, LangChain translating natural language questions into Cypher. The graph was the right shape because the queries were about multi-hop access chains, not document similarity.
>
>  
>
> The cost of graph: You need to maintain the graph as a separate store, keep it in sync with source data, and your engineers need to know Cypher. For plain Q&A over static documents, that's not worth it. For cross-document relationship reasoning at EM1's scale — it is.
>
>  
>
> My recommendation for EM1: Start vector-only for the crosswalk module (right tool, lower complexity). Build toward graph for Deconflict as the document corpus and cross-reference patterns mature. Don't add graph complexity before you've validated the query patterns that need it.
>
>   
>
> ### SECTION 3: RETRIEVAL FROM 500–2000 PAGE PLANS 
>
>  
>
> #### The Question: 
>
>  
>
> "How would you handle the retrieval challenge when the document is 2000 pages?"
>
>  
>
> #### The Answer: 
>
>  
>
> Three problems with naive fixed-size chunking on a 2000-page plan:
>
>   
> -  
>
> Context loss: a 512-token chunk cut in the middle of a section has no idea it's in "Section 4: Resource Management." The LLM receiving that chunk doesn't know what part of the plan it came from.
>
>   
> -  
>
> Citation imprecision: "somewhere in the plan" is useless. "Page 91, Section 4.2" is what the Evaluate module needs.
>
>   
> -  
>
> Retrieval noise: top-5 chunks from a 2000-page doc by pure vector similarity may all be from different sections with tangential relevance. You need structural coherence in what you pass to the LLM.
>
>    
>
> How I'd handle it:
>
>  
>
> Step 1 — Structure-aware parsing. Before embedding, parse the document structure: identify section headers, extract section boundaries (which pages each section spans), flag annexes and appendices as separate logical units. Store this as a structural map alongside the document.
>
>  
>
> Step 2 — Two-level indexing. Index at section level (section summaries, ~500 tokens each) AND at paragraph level (fine-grained chunks, ~150-200 tokens with overlap). Section summaries give you coarse navigation; paragraphs give you precision.
>
>  
>
> Step 3 — Hierarchical retrieval. For a given guideline: first query section summaries to identify the 2-3 most relevant sections. Then restrict fine-grained retrieval to chunks within those sections. This is the same principle as indexing a book — you find the chapter, then you find the paragraph. You don't scan every paragraph in the whole book.
>
>  
>
> Step 4 — Contextual chunk enrichment. Every chunk I store carries its full provenance: document title, version, section number, section heading, page number, paragraph index. When the LLM receives the chunk, it receives that metadata too. This is what makes the Smart References feature possible — the citation is assembled from the metadata, not extracted from LLM output.
>
>  
>
> I built this metadata-preservation pattern at Samay for policy documents — the structural integrity of the evidence is what makes it auditable. Same principle here, bigger documents.
>
>   
>
> ### SECTION 4: DECONFLICT — ARCHITECTURE 
>
>  
>
> #### The Question: 
>
>  
>
> "How would you think about the Deconflict feature — detecting contradictions across multiple plans?"
>
>  
>
> #### The Answer: 
>
>  
>
> This is one of the harder problems in the product because contradiction isn't just semantic distance — two sections can be semantically similar but logically contradictory. "The EOC is activated by the Director" and "The Deputy Director activates the EOC" are highly similar sentences that directly conflict.
>
>  
>
> My approach:
>
>  
>
> Phase 1 — Topic clustering. Extract all sections from all plans for an agency. For each section, generate a topic label or embedding. Cluster sections by topic across plans: "All sections across EOP, HMP, and COOP that address EOC activation." This gives you candidate groups for contradiction analysis.
>
>  
>
> Phase 2 — Pairwise contradiction detection within clusters. For each cluster (sections across different plans on the same topic), run an LLM comparison: "Given these two sections from different plans, do they give conflicting guidance on the same subject? If yes, describe the contradiction." Structured output: {contradicts: true, topic: "EOC activation authority", plan_a: {...}, plan_b: {...}, conflict_description: "..."}.
>
>  
>
> Phase 3 — Conflict store. Write flagged contradictions to a structured table: agency_id, topic, plan_a_id, plan_a_section, plan_b_id, plan_b_section, conflict_description, status (open/resolved). This is the data model for the Deconflict UI.
>
>  
>
> Where graph fits here: You can model the full corpus as a graph — nodes are plan sections, edges are "addresses_same_topic_as" (from clustering) and "contradicts" (from detection). Neo4j makes queries like "find all unresolved contradictions involving EOC activation across all active plans" trivial. At Samay I modeled identity events as a graph for exactly this reason — the relationship queries that matter don't fit a relational table.
>
>  
>
> Practical concern: Pairwise comparison across all section pairs is expensive at scale — if an agency has 5 plans of 200 sections each, that's 1000 sections and potentially 499,500 pairs. The clustering step is load-bearing — it's what keeps the comparison set tractable. Good topic clustering reduces that to maybe 20–30 pairs per topic cluster.
>
>   
>
> ### SECTION 5: HALLUCINATION PREVENTION AT CITATION LEVEL 
>
>  
>
> #### The Question: 
>
>  
>
> "How do you make sure the LLM citations in the Evaluate module are accurate? How do you prevent hallucination?"
>
>  
>
> #### The Answer: 
>
>  
>
> I don't try to prevent hallucinations at the model level — that's a losing battle. I change the system architecture so hallucinations can't reach the output unchallenged.
>
>  
>
> Three mechanisms:
>
>  
>
> 1. Evidence-gated output schema. The LLM must return a Pydantic model with evidence_quote: str (verbatim text from the plan), page_reference: str, and verdict: Literal["PASS", "PARTIAL", "FAIL", "INCONCLUSIVE"]. If the model can't provide a verbatim quote from the retrieved context, it must return INCONCLUSIVE — not a fabricated verdict. The schema enforces this contract. I used this exact pattern in the take-home project: the agent can't write a section of the brief without retrieved data to support it.
>
>  
>
> 2. Quote-then-reason prompting. The system prompt instructs: "First, copy the exact sentence(s) from the provided plan text that are relevant to this guideline. Then evaluate whether that text satisfies the requirement." Forcing the quote-first behavior dramatically reduces confabulation — the model anchors on actual text before reasoning about it.
>
>  
>
> 3. Post-processing reconciliation. After the LLM returns its structured output, a deterministic check verifies: is the evidence_quote a substring (or near-match via fuzzy string matching) of one of the retrieved chunks? If not, the verdict is flagged for human review rather than accepted. This catches cases where the model paraphrased or subtly altered the quote.
>
>  
>
> Eval harness: At Epik I built eval pipelines with Langfuse and golden datasets — known plan/guideline pairs with human-verified verdicts. Before every deploy, run the pipeline against the golden set and alert if citation accuracy drops below threshold. EM1 should have this from day one given the liability stakes — a wrong citation in a preparedness plan isn't a UX bug.
>
>  
>
> The underlying principle: trust the retrieval, verify the assertion. The retrieved chunks are ground truth. The LLM is only allowed to reason about what's in those chunks.
>
>   
>
> ### SECTION 6: MULTI-TENANT ARCHITECTURE FOR EM1 
>
>  
>
> #### The Question (implicit — he'll probe this if you describe the system design): 
>
>  
>
> "How would you handle data isolation between agencies?"
>
>  
>
> #### The Answer: 
>
>  
>
> I built multi-tenant compliance infrastructure at Samay and the pattern maps directly.
>
>  
>
> Three layers of isolation:
>
>  
>
> Layer 1 — Tenant resolution. Every request carries an agency JWT. The backend resolves agency_id from the token, looks up that agency's configuration in a PostgreSQL control-plane table — which S3 prefix, which vector namespace, which schema. No request proceeds without this resolution step. No agency ID → no data access.
>
>  
>
> Layer 2 — Row-level security in PostgreSQL. All evaluation results, guideline scores, and plan metadata tables have agency_id as a column with RLS policies that enforce it at the database level. Even if application code had a bug and forgot to filter, the DB enforces isolation.
>
>  
>
> Layer 3 — Vector namespace isolation. For the vector store (whether pgvector in PostgreSQL or an external store like Pinecone), every embedding carries an agency_id metadata tag and every query applies a metadata filter. An agency can only retrieve their own document chunks. Cross-agency retrieval is impossible by construction.
>
>  
>
> At Samay the per-tenant isolation was more complex — per-tenant Neo4j instances, per-tenant S3 buckets, per-tenant credentials in Secrets Manager under neo4j/tenant-{id} paths, IAM policies scoped to the pattern. EM1 probably doesn't need separate databases per agency — filtered namespaces and RLS are sufficient and much simpler to operate.
>
>   
>
> ### SECTION 7: POSTGRESQL AT THIS SCALE 
>
>  
>
> #### The Question: 
>
>  
>
> "Talk me through your PostgreSQL experience. Any performance or design considerations for this kind of system?"
>
>  
>
> #### The Answer: 
>
>  
>
> Production usage across three roles. The design considerations I'd apply at EM1:
>
>  
>
> Schema design for the evaluation results table: Avoid storing large text in PostgreSQL — evidence quotes and chunk text belong in S3 or a dedicated store, with a reference key in the row. PostgreSQL should own structured metadata: guideline_id, verdict, agency_id, page_ref, run_id, created_at. Fast OLTP queries, not a blob store.
>
>  
>
> Indexing: Composite index on (agency_id, guideline_id, run_id) for the most common query pattern — "show me all results for this agency's latest evaluation run." GIN index for full-text search on guideline text if you're doing in-DB search. EXPLAIN ANALYZE before any production query that's running against a large table.
>
>  
>
> pgvector for embeddings: PostgreSQL with pgvector is a reasonable choice for EM1's scale — you don't need Pinecone until you're at tens of millions of vectors. It keeps the operational footprint simple (one database) and the filtering story is native SQL. The tradeoff is that pgvector approximate nearest neighbor (IVFFlat or HNSW index) needs tuning — you configure the number of lists/clusters at build time and re-index when the dataset grows significantly.
>
>  
>
> Multi-tenant schema strategy: At Samay I used per-tenant PostgreSQL schemas. For EM1 I'd recommend a single schema with agency_id columns and RLS over per-tenant schemas — simpler to query, simpler to migrate, Postgres RLS handles the isolation cleanly.
>
>   
>
> ### SECTION 8: NEXT.JS — HONEST, CONFIDENT ANSWER 
>
>  
>
> #### The Question: 
>
>  
>
> "Your resume shows React. We're on Next.js. How quickly can you ramp?"
>
>  
>
> #### The Answer: 
>
>  
>
> My frontend work has been React and TypeScript throughout — that's the foundation Next.js is built on. The component model, hooks, state management, the TypeScript patterns — that's all the same.
>
>  
>
> The specific Next.js concepts I'd ramp on: the App Router (current direction — server components by default, layouts, nested routing), the server/client component boundary (which component needs client-side interactivity vs. which can be a server component), and the data fetching model with async server components replacing getServerSideProps.
>
>  
>
> I've also built forms, dashboards, evidence management UIs, and document management interfaces in React — all of which map directly to the compliance module UI they're building. The form-based plan intake, guideline-by-guideline results views, expandable evidence sections — I built all of those patterns at Samay. They were in React; translating to Next.js App Router is a framework migration, not a paradigm shift.
>
>  
>
> Honest ramp estimate: productive in the codebase within a week, fully comfortable in 3-4 weeks.
>
>   
>
> ### SECTION 9: BEHAVIORAL / CULTURE FIT 
>
>  
>
> #### Q: Tell me about a time you owned something truly end-to-end. 
>
>  
>
> TrustX ATAP at Samay. I came in as the sole engineer on a compliance platform for B2B SaaS customers. There was no dedicated DevOps, no dedicated frontend, no dedicated DBA. I owned everything: CDK infrastructure (15+ stacks — VPC, RDS, Lambda suite, Step Functions, AppRunner, ECS Fargate), the data pipelines, the LLM integration layer, and the React frontend with controls dashboards, evidence management, document editor.
>
>  
>
> When the infrastructure existed as click-ops with no IaC — dev had drifted from staging, nobody knew what was where — I migrated everything to CDK incrementally, stack by stack, until one cdk deploy --all stood up a clean environment. That's the kind of work that's invisible if you do it right and very visible if you don't.
>
>  
>
> The multi-tenant architecture was entirely my design: RDS as the control plane for tenant resolution, per-tenant Neo4j instances with credentials in Secrets Manager, per-tenant S3 buckets, Step Functions fanning out per tenant. I made those decisions, reasoned about the trade-offs (separate DBs vs. schemas, graph vs. vector for access traversal), and implemented them.
>
>  
>
> What end-to-end ownership meant practically: I filed bugs I found in adjacent systems. I flagged when a schema decision in week two was going to cause pain in week eight. I knew the whole system well enough to debug it at 2pm on a Friday without a runbook.
>
>   
>
> #### Q: How do you work with junior engineers? What does that look like in practice? 
>
>  
>
> Two angles: code reviews and knowledge transfer.
>
>  
>
> On code reviews: I try to give the "why," not just the "what." Saying "use a Pydantic model here instead of a raw dict" without explaining why is just a style vote. Saying "if you use a raw dict here, the Lambda returns a 200 even when the field is missing — Pydantic validation catches that at the boundary" is teaching something that will stick past this PR.
>
>  
>
> I also have a rule about code reviews: if I'm leaving more than 3 blocking comments, I ask for a sync call instead of a comment thread. Long async comment chains are demoralizing for junior engineers and slow.
>
>  
>
> On knowledge transfer: at OSU when I was a GTA for discrete math and mobile app development, I learned that students don't always need the answer — they need the frame for thinking about the problem. The same is true for junior engineers. When someone is stuck, I try to ask "what have you tried and what was the result?" before giving the answer. That forces them to articulate their own mental model, which usually reveals where it's broken.
>
>  
>
> Concretely at Zemoso: a junior developer was behind on test coverage near sprint end on a complex feature in the Strateos codebase — dozens of interrelated models, hard to understand without context. I picked up the test cases without being asked. Not as a favor — because writing tests on someone else's unfamiliar code when you're still building your mental model of a system is genuinely harder than writing tests for your own code. I had more context; it was the right move.
>
>   
>
> #### Q: Walk me through a hard architectural decision and what you gave up. 
>
>  
>
> The decision to use Neo4j for the identity access graph at Samay rather than staying in PostgreSQL.
>
>  
>
> The case for PostgreSQL: it was already there, the team knew it, you can do multi-hop queries with recursive CTEs. Simpler operational footprint.
>
>  
>
> The case for Neo4j: the queries that mattered to compliance auditors were multi-hop traversals — "which users have access to this repository, what's their org, and what changed in the last 30 days?" In PostgreSQL that's 3-4 JOINs with recursive CTEs that become hard to read and hard to optimize as the graph depth grows. In Cypher it's a single readable query. And the LangChain NL→Cypher translation worked well because Cypher's traversal patterns map cleanly to how auditors described their questions.
>
>  
>
> What I gave up: operational simplicity. A separate Neo4j instance per tenant adds infrastructure overhead — provisioning, credentials in Secrets Manager, VPC configuration, monitoring. I had to own all of that.
>
>  
>
> Was it right? For the access intelligence use case, yes — the query expressiveness and the NL→Cypher translation quality justified the overhead. For simpler relationship queries I'd have stayed in PostgreSQL. The rule: add a graph store when the most important queries are relationship traversals, not when you can do it with JOINs.
>
>   
>
> #### Q: What motivates you? Why are you looking now? 
>
>  
>
> Two things have driven my best work: a tight feedback loop between what I build and real outcomes, and the challenge of making AI systems genuinely reliable in production rather than demo-ready.
>
>  
>
> The LLM space is full of prototypes that don't survive contact with real users — hallucinations, bad citations, outputs that look good but can't be trusted. I'm motivated by closing that gap: the eval harnesses, the grounding mechanisms, the evidence trails that make an AI feature trustworthy enough to put in front of practitioners who depend on it.
>
>  
>
> EM1 is exactly that problem in a domain where the stakes are real. When an Emergency Manager's EOP has a flaw that EM1's Evaluate module missed, the downstream effect is real preparedness. When the system surfaces a contradiction between two plans that would have caused confusion during an actual incident, that's impact that doesn't come from most engineering jobs.
>
>  
>
> On timing: I've been building at Epik and learned a lot, but I want to be on a smaller team where I'm shaping the product and architecture from close to the beginning — not implementing into a mature codebase. EM1 at 12 people, 40+ real customers, with the compliance module as the near-term focus — that's the moment to join.
>
>   
>
> #### Q: Tell me about a time something broke in production that was your fault. 
>
>  
>
> At Samay, the identity event ingestion pipeline was silently dropping events under load. No errors, no alerts — the pipeline looked healthy. We found it because an auditor noticed that a user's access history had gaps in a compliance review. That's not how you want to discover a bug.
>
>  
>
> The root cause: a Spark job hitting memory limits was silently discarding overflow batches instead of failing noisily. The error handling was too defensive — catch-all that logged and continued. My fault for writing that error handling pattern without thinking through what "continue" meant at the pipeline level.
>
>  
>
> Fix: reduce batch size, change the catch to re-raise memory errors so they're loud, add end-of-pipeline reconciliation that counted events at ingestion vs. output and paged if they didn't match.
>
>  
>
> The more important fix: I added the reconciliation pattern across other pipelines too. If one could fail silently, others could. That's the lesson I actually needed — silent failures erode trust slowly and get discovered at the worst time. Loud failures are better. Make your systems fail visibly.
>
>   
>
> #### Q: How do you handle unclear or changing requirements? 
>
>  
>
> Short version: I build the smallest thing that generates real feedback, and I hold the architecture flexible around the parts I expect to change.
>
>  
>
> At Samay, when the client changed the priority control set mid-build, I was frustrated initially — I had three controls working, was mid-build on generalizing the Lambda. But because I had structured the data collectors as independent modules (aws_collector.py, integration_collector.py) and the LLM analysis as a function that took a control ID + data payload, the architecture was already generic. Swapping which controls were tested was mostly a prompt change and a collector configuration update — not a rewrite.
>
>  
>
> The practice: when I'm building something, I try to identify which parts are likely to change (control IDs, prompt language, which data sources) vs. stable (the Lambda invocation pattern, the Step Functions orchestration, the Pydantic output schema). I hold the stable parts firm and build the changeable parts to be easy to swap. Requirements don't change because people are irrational — they change because you learn things in production you couldn't know from a spec. Building for that is just realistic.
>
>   
>
> #### Q: What does good code review look like to you? 
>
>  
>
> Good code review teaches something, catches something real, and doesn't waste the author's time on style votes.
>
>  
>
> What I look for: boundary errors (missing validation at API inputs, edge cases the author didn't see), security patterns (secrets in environment variables, SQL query construction), the schema decisions that will be expensive later, and places where the code works but will be confusing to the next engineer in it.
>
>  
>
> What I don't use code review for: formatting, naming conventions that don't affect readability, or anything a linter should catch. Those should be automated out of the review process.
>
>  
>
> One concrete habit: I leave a comment ratio in mind — if a PR has more than 3-4 blocking comments from me, I ask for a sync call instead of building up a thread. Long comment chains slow down junior engineers and create adversarial energy. A 20-minute call resolves more, faster, and leaves people feeling helped not criticized.
>
>  
>
> At Epik I led code reviews for a 6-engineer team. The goal I held: a developer should be able to read a review comment I left 6 months ago and understand not just what I wanted changed but why.
>
>   
>
> #### Q: How do you think about the Deconflict feature? 
>
>  
>
> (See Section 4 above — have that answer ready. This is a product-thinking question, not just technical.)
>
>  
>
> The product framing: agencies with multiple plans often wrote them at different times, with different authors, without a systematic cross-check. The EOP says the Director activates the EOC. The COOP says the Deputy Director does. Both documents passed their individual reviews. Neither individual reviewer knew about the conflict.
>
>  
>
> This is a problem that's invisible without automated cross-document analysis. It's also a problem where the stakes are real — during an actual disaster, a first responder reading the wrong plan could take the wrong action. Surfacing these contradictions during the planning phase, not the incident phase, is the value.
>
>  
>
> The engineering challenge is making the detection precise enough to be useful and not noisy. Generating false-positive contradictions ("Section 3 says 'notify staff' and Section 7 says 'alert personnel' — contradiction!") would undermine trust in the feature quickly. The topic clustering step is load-bearing for precision.
>
>   
>
> ### SECTION 10: QUESTIONS TO ASK GUNNAR 
>
>   
>
> Ask 3-5. These signal you've thought about their specific hard problems.
>
>   
>
> Architecture & Product:
>
>   
> - "The crosswalk module — are you chunking plans structurally (section-level) or naively by token count? I'd expect structural parsing to be the harder part of making the citations trustworthy." 
> - "For Deconflict — are you doing cross-document contradiction detection today or is that upcoming? I'm curious whether you're modeling section relationships as a graph or doing pairwise LLM comparison." 
> - "The 500-2000 page plans — how are you handling the retrieval precision problem? I'm thinking about hierarchical indexing, but curious what you've found works at your doc sizes."  
>
> Team & Engineering:
>  4. "You mentioned 2 early-career engineers. How do you think about mentoring on a small team — is that structured or organic? I want to understand what supporting them well would look like."
>  5. "Coming from OpenSesame and Olo — both real production B2B SaaS at scale — what engineering habits from those environments are you deliberately bringing to EM1, and what are you leaving behind?"
>
>  
>
> Domain & Roadmap:
>  6. "The AAR corpus — agencies generate After Action Reports after incidents. Is the ingestion of AARs into the knowledge base self-serve today, or is that curated by your team?"
>  7. "What's the biggest technical problem on the roadmap that an engineer joining now would own end-to-end?"
>
>   
>
> ### SECTION 11: RAPID-FIRE ALIGNMENT TABLE 
>
>    
>
>   | What Gunnar Said / Needs  | Your Angle 
>
>    
>
>   | "Vanta-style compliance module"  | "I built this at Samay — control scoring, evidence collection, LLM-grounded verdicts, controls dashboard. The mapping to FEMA guidelines instead of SOC2 controls is a configuration change." 
>
>  
>
>   | "Graph-RAG"  | "I built the graph layer at Samay — Neo4j for identity traversal, NL→Cypher via LangChain. My take: right for multi-hop queries, overkill for single-doc retrieval." 
>
>  
>
>   | "Sentence-level citations"  | "That's the evidence-gating pattern — LLM must quote the source, schema-validated. I used this at Samay and in the take-home project." 
>
>  
>
>   | "Human in the loop"  | "Correct call for high-stakes domains. I built compliance systems where auditors verify every LLM output. Same principle." 
>
>  
>
>   | "4 engineers including founder"  | "Samay was effectively solo. I owned CDK, pipelines, frontend, and LLM layer. That's the environment I built in and prefer." 
>
>  
>
>   | "Mentor junior engineers"  | "OSU GTA for a year, picked up test coverage for struggling junior at Zemoso, code review discipline that teaches not just flags." 
>
>  
>
>   | "Full-stack ownership"  | "Not 'I own the backend.' I own the CDK stack, the Lambda suite, the API, and the React UI. All of it." 
>
>     
>
> ### SECTION 12: OPENING & CLOSING 
>
>  
>
> #### Opening (if he asks you to go first): 
>
>  
>
> "Happy to. I'm Neel — six years full-stack, last two deep in AI systems. The most directly relevant work is at Samay Systems where I was effectively the sole engineer on a compliance automation platform. The core of it was: collect evidence from multiple data sources, assemble it into a grounded context, send it to an LLM to generate a scored compliance verdict with citations. When you describe the EM1 Evaluate module — automated FEMA crosswalk, Smart References to specific plan pages — that's the same system design in a different domain. I've been curious about this conversation since the first call."
>
>  
>
> #### Closing: 
>
>  
>
> "This has been exactly the kind of technical conversation I was hoping for. What you're building — grounded AI with citation accountability in a domain where wrong answers have real stakes — is the problem I care about. I'd love to keep moving forward."
>
>   
>
> ### SECTION 13: LOGISTICS & MINDSET 
>
>   
> - Length: 60-90 min. Give concise answers first, expand when he follows up. Don't monologue. 
> - Energy: Direct, confident, concrete. Skip hedging ("I think maybe..."). Gunnar is a CTO — talk to him as a peer. 
> - When you don't know something: "I haven't worked with that specifically, but here's how I'd think about it..." is always better than a gap or a bluff. 
> - The junior engineers question: Don't skip this. It's a proxy for "will you slow our team down or accelerate it." 
> - Timing: Wed June 10. 3 days. Read this twice on Monday, read only the answers you feel weakest on Tuesday, skim the full doc Wednesday morning.   
>
> Generated June 7, 2026 — EM1 Round 2 Prep
>
>   
>
> ### SECTION 14: ASYNC JOB ARCHITECTURE 
>
>   
>
> High-probability question. Gunnar shipped at Olo — async-first architecture for restaurant orders. He knows a 2000-page plan crosswalk is not a synchronous request.
>
>   
>
> #### The Question (several forms): 
>
>   
> - "How would you handle a plan evaluation that takes 5 minutes? You can't block an HTTP request for that." 
> - "Walk me through the request lifecycle for triggering a crosswalk evaluation." 
> - "What happens if an evaluation job fails halfway through?"  
>
> #### The Answer: 
>
>  
>
> The crosswalk evaluation is a long-running background job, not a synchronous API call. Here is the architecture I would use:
>
>  
>
> Request / Response split:
>  The frontend submits a plan evaluation request — POST /evaluations — and gets back immediately with a job ID and status QUEUED. No waiting. The client either polls GET /evaluations/{id} on an interval, or we push progress via a WebSocket or SSE stream as each guideline completes. I have built the streaming side of this — at Epik the real-time triage dashboard used WebSockets to push results as the pipeline processed events. Same pattern.
>
>  
>
> Job queue:
>  The API handler writes a job record to PostgreSQL (evaluation_jobs table: id, agency_id, plan_id, status, created_at, updated_at) and publishes a message to SQS. A worker (Lambda or ECS task, depending on duration) consumes from SQS and processes the job. SQS gives you durability — if the worker crashes, the message is not lost, it reappears after the visibility timeout and another worker picks it up.
>
>  
>
> Granular progress:
>  The job processes one guideline at a time and writes each result to the evaluation_results table as it completes. The polling endpoint returns both the overall status AND the count of completed vs. total guidelines. That way the UI can show a real progress bar: "47 of 150 guidelines evaluated" rather than a spinner. This matters for a 5-minute job — users need to know something is happening.
>
>  
>
> Failure handling:
>  At the job level: three retries with exponential backoff for transient failures (LLM API timeout, S3 read error). If all three fail, status → FAILED, error reason stored, agency notified.
>  At the guideline level: a failure on one guideline should not fail the entire evaluation. Write INCONCLUSIVE for that guideline with the error, continue. The evaluation completes with a note: "3 guidelines could not be evaluated — review manually."
>
>  
>
> Idempotency:
>  If an agency triggers the same plan evaluation twice (double-click, retry), the second request should detect an in-flight job for the same plan version and return the existing job ID rather than starting a duplicate run. Cheapest implementation: unique constraint on (agency_id, plan_id, plan_version_hash) in the jobs table.
>
>  
>
> At Samay, the Step Functions orchestration handled exactly this pattern for the compliance pipeline — fan out per tenant, each execution independent, failed executions visible in the Step Functions console without affecting others. SQS + worker is simpler at EM1's current scale, with Step Functions as the natural migration when you need more complex branching logic.
>
>   
>
> ### SECTION 15: SCALABILITY & LLM COST MANAGEMENT 
>
>   
>
> Gunnar came from scale. He is hiring for someone who thinks ahead, not someone who scales on fire.
>
>   
>
> #### The Question: 
>
>   
> - "What breaks first if EM1 goes from 40 agencies to 400?" 
> - "A full crosswalk on a 2000-page plan triggers 150 LLM calls. How do you think about cost?" 
> - "How does the system perform as the document corpus grows?"  
>
> #### The Answer (think in layers — compute, storage, cost): 
>
>  
>
> What breaks first at 10x scale:
>
>  
>
> Embedding compute: Every new plan upload needs to be chunked and embedded. At 40 agencies this is sporadic. At 400 it becomes a sustained background workload. The fix: async embedding pipeline (SQS → worker), not synchronous on upload. Embedding jobs queue independently of the user-facing API. Already the right pattern — just needs to be designed for it from the start.
>
>  
>
> pgvector query performance: Approximate nearest neighbor search with IVFFlat in pgvector degrades as the vector count grows — the index needs to be rebuilt periodically as data volume increases, and the number of lists configured at index creation time becomes a tuning concern. At 400 agencies with large corpora, you would monitor query time and either tune the HNSW index parameters or migrate to a dedicated vector store like Pinecone. The schema is the same — swapping the retrieval backend is a contained change if you have an abstraction layer.
>
>  
>
> LLM cost — the real concern: A full crosswalk on a 2000-page plan against 150 FEMA guidelines = 150 LLM calls per evaluation run. If 400 agencies each run one evaluation per month, that is 60,000 LLM calls per month — significant cost, especially with a large model.
>
>  
>
> Three levers I would pull:
>
>   
> -  
>
> Caching at the guideline level. FEMA guidelines are stable — they do not change week to week. If a plan section has not changed since the last evaluation, there is no reason to re-run the LLM evaluation for that guideline. Cache the result keyed on (guideline_id, chunk_hash). On re-evaluation, only run the LLM for guideline/section pairs where the content has changed. This alone could reduce repeat evaluation costs by 60–70%.
>
>   
> -  
>
> Model tiering. Not every step needs a frontier model. Classification (which section is relevant to this guideline?) can run on a small, fast, cheap model — Llama 3 8B via Groq, for example. The synthesis step (evaluate and write the verdict with evidence quote) needs more reasoning capacity — Claude Haiku or GPT-4o-mini. The final narrative summary for the agency report might warrant a larger model. I used this exact tiering at Samay: classification prompt vs. full analysis prompt were different model calls.
>
>   
> -  
>
> Batch evaluation scheduling. Not all agencies need real-time evaluation. A "scheduled monthly evaluation" workload can be batched during off-peak hours at lower cost than on-demand real-time.
>
>    
>
> Storage at scale: Plans are large PDFs. Store raw documents in S3, metadata in PostgreSQL. Never put binary content in PostgreSQL — it is not a blob store. S3 with lifecycle policies (move old plan versions to Glacier after 90 days) keeps storage costs reasonable. At Samay every document went to tenant-specific S3 buckets with metadata in PostgreSQL; same pattern here.
>
>   
>
> ### SECTION 16: TESTING STRATEGY & OBSERVABILITY 
>
>   
>
> 4-person team, no dedicated QA. He needs to know you think about quality without process overhead.
>
>   
>
> #### The Question: 
>
>   
> - "How do you maintain test coverage on a small team moving fast?" 
> - "How do you know the crosswalk system is working correctly in production?" 
> - "How do you test an LLM system? You can not unit test an LLM."  
>
> #### Testing Strategy Answer: 
>
>  
>
> I split testing into three layers for an LLM-integrated system, and I think about the cost/value of each layer explicitly on a small team:
>
>  
>
> Layer 1 — Deterministic unit tests (fast, cheap, always run):
>  Everything that is NOT the LLM call is deterministic and should be unit tested. Chunk metadata extraction — does this parser correctly identify Section 4.2 as starting on page 91? Pydantic schema validation — does the output model reject a missing evidence_quote? Guideline store CRUD — does the right guideline get retrieved by ID? These are fast, cheap, and catch regressions. I write these by default.
>
>  
>
> Layer 2 — Integration tests against a fixture LLM (slower, run on merge):
>  Mock the LLM call with a fixture response. Test the full evaluation pipeline end-to-end with a small test plan document and a small test guideline set. Validates the orchestration logic — job creation, chunk retrieval, result writing, status updates — without burning real LLM API tokens on every test run. At Samay I used a local fixture server for MCP tool calls in the take-home project for exactly this reason.
>
>  
>
> Layer 3 — Eval harness with golden dataset (periodic, production-grade):
>  A set of known plan/guideline pairs with human-verified correct verdicts. Run the full LLM pipeline against this set and track: citation accuracy (is the evidence quote actually in the plan?), verdict accuracy (does PASS/FAIL match human judgment?), hallucination rate (does the model assert findings not in the retrieved context?). Run this before every significant prompt change or model upgrade, not on every commit. I built this at Epik with Langfuse — dashboard plus regression alerts. This is what gives you confidence that a prompt change improved things vs. broke them.
>
>  
>
> What I do NOT test exhaustively on a small team: every edge case in the LLM's reasoning. The LLM is non-deterministic — you test the system around it, not the model itself.
>
>  
>
> #### Observability Answer: 
>
>  
>
> For an LLM-integrated system, standard APM is necessary but not sufficient. I instrument three things:
>
>  
>
> System health (standard): Request latency, error rates, job queue depth, worker throughput — standard CloudWatch or Datadog. An alert if the job queue is growing and workers are not draining it.
>
>  
>
> LLM pipeline health (custom): Per-evaluation-run metrics: total guidelines evaluated, PASS/PARTIAL/FAIL/INCONCLUSIVE counts, average evaluation latency per guideline, total token usage and estimated cost. Written to the evaluation_runs table and visible in a simple internal dashboard. At Samay the equivalent was reconciliation counters at each pipeline stage — events in vs. events out, alerting on mismatch. The principle is the same: make the pipeline's behavior numerically observable, not just pass/fail.
>
>  
>
> Citation quality drift (hardest, most important): Run a sample of production evaluations weekly through the golden dataset comparison. If citation accuracy starts drifting — even if the system looks healthy by latency/error metrics — you catch it before customers notice. This is the silent failure mode: the system keeps running and returning results, but the results are getting worse. At Samay the equivalent was a compliance auditor noticing access history gaps — that is the worst way to discover a quality regression. Proactive quality monitoring catches it first.
>
>   
>
> ### SECTION 17: DOMAIN ONBOARDING — EMERGENCY MANAGEMENT 
>
>   
>
> This question is certain. You have zero EM domain experience. He knows this and will ask about it. The right answer is not "I'll read FEMA's website" — it is a specific, credible onboarding strategy.
>
>   
>
> #### The Question: 
>
>   
> - "You have not built for emergency management before. How would you approach learning this domain?" 
> - "The team has EM operators alongside engineers. How do you work with domain experts to close that gap?"  
>
> #### The Answer: 
>
>  
>
> I have been in this situation before — at Samay I came in with zero compliance domain knowledge. SOC2, NIST, ISO27001 controls were not familiar territory. The way I closed it was not by reading documentation in isolation — it was by sitting with the people doing the actual work and asking the right questions.
>
>  
>
> The most useful question I asked the compliance auditor at Samay was not "what data do you need?" It was: "Walk me through a real audit, step by step, as if I am a new auditor learning the job." That session gave me the mental model I needed to design the data collection pipeline correctly. No requirements doc would have given me that.
>
>  
>
> I would apply the same approach at EM1. Concretely:
>
>  
>
> Week 1: Sit with one of the EM operators on your team and ask them to walk me through a real plan review — how they read an EOP, what they look for in each section, how they use the Evaluate module today, where it falls short. Shadow a customer call if possible. I am not trying to become an EM expert in a week — I am trying to understand the workflow well enough to build for it correctly.
>
>  
>
> Early artifacts I would read: One real EOP (even a public one), the FEMA Comprehensive Preparedness Guide, one After Action Report. Not to memorize — to have the vocabulary and understand the document structure before I start building the ingestion pipeline.
>
>  
>
> Ongoing: I would ask your EM operators to review any feature I build that touches the evaluation output before it ships. The engineer can build the right system; the domain expert tells you if the system is asking the right question. That is the division I had at Samay with the compliance auditors and it made the product significantly better than what I would have designed alone.
>
>  
>
> The short version: I close domain gaps by getting close to the people who live in the domain, not by reading about it in isolation. I have done this in compliance and it worked. I would do it the same way here.
>
>   
>
> ### SECTION 18: SHORTER QUICK-FIRE ANSWERS 
>
>  
>
> #### Q: What does "done" mean to you? 
>
>  
>
> Done means it is in production, tested, monitored, and I could explain it to the next engineer who has to touch it. Not done means: works on my machine, works in staging, deployed but not observed. Done is the version that can break at 2pm on a Friday and I can diagnose it without a runbook.
>
>  
>
> On a small team, I also include: does the person who will maintain this have what they need to do so? If I shipped a feature with no tests and no documentation and left the team, that feature is not done — I just moved the cost.
>
>   
>
> #### Q: How do you approach technical debt on a small team moving fast? 
>
>  
>
> Debt falls into two categories and I treat them differently.
>
>  
>
> Load-bearing debt — infrastructure that is creaking, schema decisions that are starting to hurt, the click-ops AWS setup that has no IaC — this accrues compound interest. At Samay I migrated the entire infrastructure to CDK stack by stack specifically because not having IaC was starting to cost more time every sprint than the migration would take. I identify this kind of debt early and make the case for addressing it before it becomes an emergency.
>
>  
>
> Cosmetic debt — ugly but functional code, imperfect naming, tests that could be better structured — I leave this alone when velocity matters. A small team shipping fast cannot gold-plate everything. The discipline is knowing the difference between debt that is getting more expensive over time and debt that is just aesthetically unpleasant.
>
>  
>
> The honest signal I use: if I am explaining the same piece of code or architecture to a new person for the second time and they look confused, that is debt that needs to be fixed — it is actively slowing the team down.
>
>   
>
> #### Q: What does a good API look like to you? 
>
>  
>
> Three things: predictable, honest about failures, and versioned from day one.
>
>  
>
> Predictable: consistent naming, consistent response shapes, consistent error codes. If GET /evaluations/{id} returns {status, created_at, results}, then GET /plans/{id} should follow the same envelope. A developer should be able to guess your API without reading docs.
>
>  
>
> Honest about failures: 400 for bad input the caller can fix, 422 for validation errors with field-level detail, 500 for things we broke, never a 200 wrapping an error. I have debugged too many systems where a 200 {"error": "something failed"} pattern hid production failures from monitoring.
>
>  
>
> Versioned from day one: a /v1/ prefix costs nothing to add at the start and is very expensive to retrofit when you have 40 agency customers relying on an unversioned API. At EM1 specifically, agencies may have their own tooling or integrations — changing API shapes without a version is a support incident waiting to happen.
>
>   
>
> #### Q: Tell me about a time you pushed back on a technical direction with leadership. 
>
>  
>
> At Monarch Tractor, the decision was between Workato, Boomi, and AWS native for the HRMS sync workflow. I had calls with all three vendors. Coming out of those conversations, my recommendation was Workato — it was purpose-built for multi-system HRMS integrations, the error handling was mature, and I could see exactly what I would be building from scratch with AWS Lambda that Workato had already solved.
>
>  
>
> Leadership picked AWS. Budget.
>
>  
>
> My first reaction was that we would spend more engineering hours building what Workato had already solved. I said that explicitly, with specifics: "the Lambda layer dependency issues alone will cost us a week." And parts of that were true — I had to containerize just to run PowerShell, I wrote custom error handling from scratch, the UKG API bug required a vendor ticket to resolve.
>
>  
>
> But I came to understand why the decision was right in context. The team already had AWS expertise and infrastructure. The CloudWatch and EventBridge audit trail was actually better for an HR system's compliance requirements than Workato's logs would have been. When you are managing employee onboarding and offboarding, you want every operation logged in a system your security team already audits. I had not fully weighed that when I pushed back.
>
>  
>
> What I took from it: my analysis was technically correct and contextually incomplete. Leadership had constraints — budget, team skills, existing infra, compliance requirements — that I did not have full visibility into. Pushing back clearly was right. Accepting the decision and building it well was also right.
>
>   
>
> #### Q: How do you balance shipping fast with not breaking things? 
>
>  
>
> I think about this as: move fast on the parts that are easy to change, be deliberate on the parts that are hard to undo.
>
>  
>
> Schema decisions, API contracts, and infrastructure choices are hard to undo — especially with 40+ real customers on the platform. I slow down on those and make sure the decision is right before committing. I will ask an extra question, propose two options to Gunnar, or write a short DECISIONS.md entry before building. That 30-minute investment is cheap relative to a migration later.
>
>  
>
> Feature implementation — the actual code inside a well-designed API — is easy to change. I move fast here. Ship something that works, get feedback from a real user, iterate. The Samay compliance testing system started as a single-control proof of concept that ran in a notebook. It was ugly. It told us whether the approach was right before we invested in production architecture. That is the sequence I try to follow.
>
>  
>
> The summary: nail the contracts, move fast on the implementation.
>
>   
>
> Appended June 7, 2026 — Sections 14–18: Async, Scalability, Testing/Observability, Domain Onboarding, Quick-Fire
>
>   
>
> ### SECTION 19: UPDATED CONTEXT — WHAT'S ACTUALLY BUILT VS. WHAT YOU'RE BUILDING 
>
>   
>
> Read this before anything else. It reframes several answers.
>
>   
>
> #### The current state (what exists today): 
>
>    
>
>   | Component  | Current Reality 
>
>    
>
>   | Core AI  | A "simple RAG" — indexes large EM PDFs (500–2000 pages), retrieves relevant passages in the EM domain 
>
>  
>
>   | Document library  | Aggregates public plans + customer-contributed docs; agencies can cross-share non-competing incident docs 
>
>  
>
>   | Compliance crosswalk  | A SEPARATE product — breaks FEMA requirements into checklists, validates plan against them 
>
>  
>
>   | Current intake  | Plans submitted via email or manual upload; compliance checks only run after a human manually triggers them 
>
>  
>
>   | Customer base  | 60+ agencies (state, county, city) — update any mention of "40" 
>
>  
>
>   | Evaluation scale  | ~111 guidelines per evaluation run (website shows All: 111, Passed: 24, Needs Attention: 39) 
>
>    
>
> #### What this role is building: 
>
>    
>
>   | Feature  | What It Actually Is 
>
>    
>
>   | Vanta-style compliance module  | Self-serve form intake replacing the current email/manual flow → automated trigger → async evaluation → scored results dashboard 
>
>  
>
>   | Agent "skills"  | Workflow-specific guided capabilities for the AI agent: e.g., walk a user through plan creation, guide an AAR review — multi-step structured conversation with state, not just Q&A 
>
>  
>
>   | RAG improvements  | Extend and improve the existing "simple RAG" — better retrieval precision, structural awareness, cross-doc reasoning 
>
>  
>
>   | Library enhancements  | Better cross-sharing, search, and integration between library and agent 
>
>    
>
> #### How this sharpens existing answers: 
>
>  
>
> Crosswalk system design (Section 1): You are not designing from scratch — you are replacing a human-in-the-loop manual process. The intake step (the form) is the first thing to build. The trigger is currently human; you are automating it. This is the framing Gunnar wants to hear: "I understand the current flow is email/manual trigger, and the module is replacing that with self-serve intake + automated trigger + async evaluation pipeline."
>
>  
>
> Async job architecture (Section 14): Even more important now. The current system only runs when a human clicks a button. The new system needs to handle concurrent submissions from 60+ agencies without a human coordinating. Job queue is not optional — it is the core architectural change from the current model.
>
>  
>
> LLM cost (Section 15): With 111 guidelines per run, 60+ agencies, and monthly evaluation cadence, that is 6,600+ LLM calls per month at current scale, scaling to 66,000+ at 10x. The caching strategy (skip re-evaluation if plan section + guideline pair has not changed) is the primary cost lever.
>
>   
>
> ### SECTION 20: AGENT SKILLS ARCHITECTURE 
>
>   
>
> New product direction — not covered anywhere in current prep. High probability he mentions this.
>
>   
>
> #### The Question (likely form): 
>
>   
> - "We want to add workflow-specific skills to the AI agent — things like guiding an EM through plan creation or an AAR review. How would you think about building that?" 
> - "How do you go from a pure Q&A RAG agent to a guided multi-step workflow agent?"  
>
> #### The Answer: 
>
>  
>
> The distinction here is between a reactive agent (user asks a question, agent answers) and a proactive workflow agent (agent guides a user through a structured process with multiple steps, memory across turns, and different tool calls at each stage).
>
>  
>
> The architecture shift is from stateless Q&A to stateful conversation with a workflow graph.
>
>  
>
> How I would structure it:
>
>  
>
> State schema first. Each "skill" has a state object that persists across the conversation: where the user is in the workflow, what has been collected so far, what is still needed. For a plan creation skill, that state might be: {current_section: "hazard_identification", completed_sections: [...], draft_content: {...}, gaps: [...]}. This state lives in the session, not in the LLM's context window.
>
>  
>
> Workflow graph. Each skill is a directed graph of steps. A node is a stage in the workflow (e.g., "gather jurisdiction info," "identify hazards," "draft mitigation actions"). An edge represents a transition triggered by the user's response or a tool call result. This is exactly what LangGraph provides — I built LangGraph-based agentic workflows at Epik for security triage pipelines that had branching logic based on alert classification. Same pattern applies here.
>
>  
>
> Tool calls per step. At each node the agent has access to a specific, scoped set of tools relevant to that step — not every tool the agent has. For the "hazard identification" step: retrieve relevant peer agency hazard sections from the library, query FEMA doctrine for that hazard type, check the agency's existing plan for what they already have. For the "mitigation actions" step: different tools, different retrieval context. Scoping tool access per step keeps the agent focused and reduces noise.
>
>  
>
> Persistence and resumability. A plan creation workflow is not done in one session. The user will come back. State needs to be persisted to PostgreSQL between sessions, keyed on (agency_id, skill_type, workflow_instance_id). When the user returns, load the state and resume. This is a meaningful architectural requirement that a stateless Q&A agent does not have.
>
>  
>
> At Samay I built n8n agentic workflows for daily compliance summary reports — multi-step, MCP-based tool calling, state across steps. The concept is identical; LangGraph is a more developer-native implementation of the same pattern for code-first teams.
>
>  
>
> The practical build order: Start with the simplest possible skill — single-step, no branching, no resumability. Prove the pattern works end-to-end (user input → structured state → targeted retrieval → guided response). Then add persistence and multi-step flow. Then add branching. This is the same "ugly scripts first, architecture second" progression that worked at Samay.
>
>   
>
> ### SECTION 21: PRODUCT KNOWLEDGE ADDITIONS 
>
>   
>
> Update your mental model of the product with these specifics from website + conversation.
>
>   
>
> Custom evaluations: Agencies are not limited to the FEMA library. They can build their own crosswalk checklists — custom guidelines for state-specific requirements, local ordinances, or agency internal standards. This means the guideline store is not a static FEMA dataset; it is a multi-tenant, user-editable store. Architectural implication: guidelines need an owner field (system vs. agency), and the crosswalk engine needs to run against the right guideline set per agency.
>
>  
>
> Smart References UI: The Evaluate module shows exactly which page in the plan answers which FEMA guideline. This is the customer-facing display of the page_reference field in the evaluation result. When you talk about citation grounding and evidence-gated output, this is the UI it surfaces into.
>
>  
>
> The free evaluation entry point: On the website, agencies can submit a plan for a free evaluation (drag-and-drop, max 25 MB). This is the top-of-funnel acquisition flow — it also tells you the file size constraint the ingestion pipeline needs to handle.
>
>  
>
> E03 is called "Chat" in the nav: The Operationalize module is surfaced to users as a chat interface — real-time Q&A over their uploaded documents. This is the module that the agent skills are extending.
>
>  
>
> Updated traction: 60+ agencies, not 40. Use this number.
>
>   
>
> Appended June 8, 2026 — Sections 19–21: Current state context, agent skills architecture, product knowledge updates
>
>   
>
> ### SECTION 22: FULL END-TO-END SYSTEM DESIGN — VANTA-STYLE COMPLIANCE MODULE 
>
>   
>
> This is the master answer. Section 1 covers the AI/data layer. This covers the FULL system from intake form to human approval. Know both — he may ask either version.
>
>   
>
> #### The Question: 
>
>   
> - "Walk me through the full flow — from an agency uploading a plan to them seeing a scored evaluation." 
> - "How would you replace the current email/manual trigger process end-to-end?" 
> - "How would you build the Vanta-style compliance module from scratch?"  
>
> #### Critical framing first: 
>
>   
>
> "The current flow is: plan arrives by email, a human manually uploads it and manually triggers the compliance check. The Vanta module automates everything from intake to results — the human only re-enters at the review and approval step. That is the right place for them to be."
>
>   
>
> That one sentence tells Gunnar you understood the problem, not just the technology.
>
>   
>
> #### The Full 6-Stage Flow: 
>
>  
>
> Stage 1 — Self-Serve Intake Form (Frontend)
>
>  
>
> The form is the entry point that replaces email. It collects:
>
>   
> - Plan type (EOP / HMP / COOP / IAP / other) 
> - Jurisdiction and agency name (pre-populated from account) 
> - Plan version / effective date 
> - File upload (PDF, max 25MB based on current site — use presigned S3 URL for direct browser-to-S3 upload, not routing large files through the API server) 
> - Guideline library selection: FEMA standard, state-specific, or a custom evaluation the agency has built  
>
> The presigned URL pattern matters: for a 25MB PDF, you do not want that file moving through your API server on every upload. Issue a presigned S3 PUT URL from the backend, upload directly from the browser to S3, then the backend receives a callback/confirmation with the S3 key. This is standard and keeps the API layer thin.
>
>  
>
> On submit: POST /evaluations returns {job_id, status: "QUEUED"} immediately. The user sees a confirmation screen: "Your plan has been submitted. You will be notified when the evaluation is complete."
>
>  
>
> Stage 2 — Async Job Queue
>
>  
>
> The API handler writes to evaluation_jobs: {id, agency_id, plan_id, plan_s3_key, guideline_library_id, status: QUEUED, created_at} and publishes to SQS. Worker picks it up. If the agency submits the same plan twice (double-click, race condition), a unique constraint on (agency_id, plan_s3_key_hash) catches it and returns the existing job.
>
>  
>
> Stage 3 — Document Ingestion (if not already indexed)
>
>  
>
> Worker checks: has this exact plan version been indexed before (matched on file hash)? If yes, skip ingestion, reuse the existing chunk index. If no:
>
>   
> - Download PDF from S3 
> - Structure-aware parsing: extract section map (section number → heading → page range), not naive fixed-size chunks 
> - Generate chunks at two levels: section summaries (~500 tokens) and paragraph-level chunks (~150-200 tokens with overlap), each tagged with provenance metadata: {agency_id, doc_id, section, heading, page, chunk_index} 
> - Embed all chunks, write to pgvector (or Pinecone at scale), write chunk metadata to PostgreSQL 
> - Write document record to plans table: {id, agency_id, s3_key, file_hash, version, plan_type, indexed_at}  
>
> Stage 4 — Crosswalk Evaluation Loop
>
>  
>
> For each guideline in the selected library (111 for standard FEMA HMP):
>
>   
> - Retrieve top-k chunks: first query section summaries to find the 2-3 most relevant sections, then retrieve paragraph-level chunks from within those sections only (hierarchical retrieval) 
> - LLM evaluation call with Pydantic output schema:  
> - Input: guideline text + retrieved chunks with metadata 
> - Output: {verdict: PASS|PARTIAL|FAIL|INCONCLUSIVE, evidence_quote: str, page_reference: str, gaps: list[str], confidence: float}   
> - Evidence gate: if evidence_quote is empty or not a substring of the retrieved context → override verdict to INCONCLUSIVE, flag for mandatory human review 
> - Write result to evaluation_results: one row per guideline 
> - Update job progress counter: completed_guidelines += 1 
> - Update job status to COMPLETE when all guidelines are done; FAILED if unrecoverable error  
>
> LLM cost optimization: if the same (guideline_id, chunk_hash) pair was evaluated in a previous run with the same plan version, reuse the cached result. Only run LLM for guideline/section pairs where content has changed. This is the primary cost lever — repeat evaluations should be 60-70% cheaper than first-time runs.
>
>  
>
> Stage 5 — Human-in-the-Loop Review (The Right Bottleneck)
>
>  
>
> This is not optional and is not a concession to uncertainty — it is a deliberate design choice for a high-stakes domain. The output of Stage 4 is the LLM's assessment, not the final verdict.
>
>  
>
> The review UI surfaces:
>
>   
> - PASS with high-confidence evidence → shown clearly, minimal friction. EM can accept with one click. 
> - PARTIAL / NEEDS ATTENTION → highlighted, evidence quote shown, gaps listed, EM reviews and can: accept LLM assessment, override with their own judgment + annotation, or flag for more context 
> - INCONCLUSIVE → mandatory review, cannot be submitted without human resolution. Either the section exists and the LLM couldn't find it (retrieval gap) or the section is genuinely missing. 
> - FAIL → shown with specific gaps from the LLM, EM reviews what is missing  
>
> The principle: automate the tedious, preserve the judgment. Finding which sections of a 2000-page plan might satisfy 111 guidelines and pre-populating evidence quotes is the tedious part. Deciding whether the agency's specific context meets the requirement is the judgment part. The LLM handles the first; the human owns the second.
>
>  
>
> At Samay this was the same model — the automated control testing system generated the evidence and score, but the compliance auditor reviewed and signed off before it went into a compliance report. The LLM is a first reviewer, not the final one.
>
>  
>
> Stage 6 — Report Generation & Submission
>
>  
>
> Once the EM has reviewed and resolved all PARTIAL/INCONCLUSIVE items:
>
>   
> - Generate a structured scorecard: overall pass rate, section-by-section breakdown, guideline-by-guideline results with evidence quotes and page references 
> - Export to PDF for FEMA submission (or whatever the agency's compliance body requires) 
> - Store evaluation history: {agency_id, plan_id, run_id, overall_score, run_date} — enables the "you improved from 68% to 84% since last submission" trend view 
> - Optionally: notify the agency via email/webhook when the evaluation is ready for review   
>
> ### SECTION 23: HUMAN-IN-THE-LOOP — DESIGN PHILOSOPHY 
>
>   
>
> EM1's core product philosophy is "human in the loop." He WILL ask about this. Have a principled answer, not a vague one.
>
>   
>
> #### The Question: 
>
>   
> - "How do you think about the role of human review in an AI system like this?" 
> - "How do you decide what the AI does vs. what the human does?" 
> - "How do you prevent the LLM from making decisions it shouldn't?"  
>
> #### The Answer: 
>
>  
>
> Human-in-the-loop is not a risk mitigation — it is a product design choice based on the nature of the task.
>
>  
>
> The relevant distinction is between tasks where the AI can be the final decision-maker and tasks where the AI should be a first-pass reviewer that accelerates a human decision. The crosswalk evaluation sits firmly in the second category. Here is why:
>
>  
>
> A FEMA compliance verdict is not just a logical inference from text — it is a professional judgment about whether a plan meets a requirement in context. "Does this EOP address hazard identification adequately?" requires understanding the jurisdiction, the local hazard profile, the agency's history, and FEMA's current assessment priorities. An LLM has none of that context. It has the document and the guideline text.
>
>  
>
> So the architecture I design for is: the LLM does the work that would take a human expert days (reading 2000 pages, matching each section to 111 guidelines, extracting evidence quotes), and the human does the work that requires contextual judgment (deciding whether the evidence is sufficient for this specific agency's situation). The human is still doing meaningful work — just not the mechanical, tedious part.
>
>  
>
> The specific design decisions that enforce this:
>
>   
> - INCONCLUSIVE verdict cannot be submitted without human resolution — no bypass 
> - Evidence quotes are surfaced verbatim from the plan, not paraphrased — human can verify in 5 seconds by checking the page reference 
> - Human annotations and overrides are stored alongside LLM verdicts — the final record shows what the LLM said AND what the human decided. That audit trail is important if an agency is submitting to FEMA. 
> - Confidence scores flag low-confidence verdicts even when they are PASS — the system is honest about uncertainty  
>
> When to reduce human review over time: As the system accumulates a history of LLM verdicts that match human review decisions for a specific agency's plan type, you can surface confidence levels that reflect that calibration. High-confidence PASS verdicts on stable sections that have not changed from the last accepted evaluation can reasonably become one-click approvals. The human is still in the loop; the loop is just shorter for routine cases.
>
>   
>
> ### SECTION 24: AFTER ACTION REVIEW (AAR) PIPELINE 
>
>   
>
> AARs are explicitly part of the product (E03 knowledge base, agent skills roadmap). If he asks about system design beyond the crosswalk, AAR pipeline is the next most likely topic.
>
>   
>
> #### The Question: 
>
>   
> - "How would you think about the AAR ingestion and retrieval pipeline?" 
> - "How would you build the after-action review skill for the agent?" 
> - "AARs are key to how agencies learn — how does that feed back into the system?"  
>
> #### What AARs Are (and why they're architecturally interesting): 
>
>  
>
> An After Action Report is written after an incident — it documents what happened, what worked, what didn't, and what should be improved. AARs are:
>
>   
> - Unstructured narrative — unlike plans which have defined sections, AARs vary widely in format 
> - Incident-typed — an AAR from a flood response is relevant to other agencies planning flood response; irrelevant to an active shooter scenario 
> - Lessons-first — the most valuable content is the "what we learned / what we'd do differently" sections, not the incident timeline 
> - Sharable across agencies (with consent) — non-competing agencies' AARs are valuable learning material; EM1's library feature already enables this  
>
> #### Pipeline Design: 
>
>  
>
> Ingestion (same base as plan ingestion, different metadata):
>
>  
>
> AAR upload → S3 → structure-aware parsing (but AARs are less structured — look for section markers like "Lessons Learned," "Recommendations," "What Worked," "What Didn't Work" rather than numbered compliance sections) → chunk and embed → store in the knowledge base.
>
>  
>
> Key metadata difference: every AAR chunk is tagged with:
>
>   
> - incident_type (flood, wildfire, active shooter, public health, etc.) — either extracted by a classification LLM call or selected during upload 
> - jurisdiction (optional — for privacy/cross-share decisions) 
> - incident_date 
> - source_agency_id 
> - section_type (lessons_learned | recommendations | timeline | other) — extracted from section heading  
>
> This tagging is what makes AAR retrieval useful. "What did agencies learn from wildfire response?" → filter by incident_type: wildfire, section_type: lessons_learned → retrieve top-k. Without incident tagging, you get retrieval noise across all incident types.
>
>  
>
> Two use cases, two retrieval patterns:
>
>  
>
> Use case 1 — E03 Chat: User asks "What have agencies learned from active shooter responses?" The chat agent retrieves AAR lessons-learned chunks filtered by incident type. The answer is grounded in real post-incident reports, not training data. Citations point to specific AAR documents (agency name if shared, anonymized if not).
>
>  
>
> Use case 2 — Plan improvement (agent skill): After an agency runs a crosswalk evaluation and gets PARTIAL/FAIL verdicts, the plan improvement workflow can retrieve relevant AARs: "Here are lessons from similar agencies who had the same gap in their EOC activation section — how did they address it?" This turns the improvement workflow from a blank-page problem into a reference-guided one.
>
>  
>
> The AAR review skill (stateful agent workflow):
>
>  
>
> When an agency finishes an incident and needs to write their AAR, the agent can guide them through it:
>
>   
> - Step 1: Gather incident timeline (structured form — date, incident type, agencies involved, duration) 
> - Step 2: What worked — agent retrieves similar AARs' "what worked" sections as prompts/examples 
> - Step 3: What didn't work — same pattern, different filter 
> - Step 4: Recommendations — agent surfaces relevant doctrine and peer recommendations for the gaps identified 
> - Step 5: Draft generation — agent assembles a draft AAR from the collected structured inputs, formatted to standard AAR template  
>
> This is a stateful, multi-step workflow agent (LangGraph) — not a Q&A agent. State persists across the session. Each step has a targeted retrieval context (incident-type-filtered AARs, relevant doctrine sections). The human fills in what they actually experienced; the agent provides structure, examples, and draft language.
>
>  
>
> Cross-sharing governance:
>
>  
>
> AARs can contain sensitive incident details. The library cross-share model needs an explicit consent flag per document: {is_shared: bool, anonymize_agency: bool, shared_incident_types: [...]}. An agency opts in to sharing specific AARs with specific peer agencies or the whole platform. This is the same governance model as the existing document library but more granular because AARs may contain sensitive operational details.
>
>   
>
> Appended June 8, 2026 — Sections 22–24: Full E2E system design, human-in-the-loop philosophy, AAR pipeline
>
>   
>
> ### SECTION 25: TYPESCRIPT — DEPTH ANSWER 
>
>   
>
> EM1's entire stack is TypeScript — Next.js frontend, CDK infrastructure, likely shared types. If you say "I use TypeScript" and stop there, that's a gap.
>
>   
>
> #### The Question: 
>
>   
> - "Walk me through your TypeScript experience." 
> - "How do you handle typing in a full-stack system where the frontend and backend share data shapes?" 
> - "How do you type LLM responses that are inherently dynamic?"  
>
> #### The Answer: 
>
>  
>
> TypeScript has been my default for the last two-plus years — CDK infrastructure at Samay was TypeScript, React frontends at Samay and Epik were TypeScript, and the take-home project's agent backend was Python but the frontend and tooling layer was TypeScript.
>
>  
>
> The patterns I rely on in production:
>
>  
>
> Shared types across layers. In a full-stack TypeScript system, the most expensive bugs come from the API contract drifting between frontend and backend — the backend returns evidence_quote and the frontend expects evidenceQuote, nobody notices until a user sees an empty field. The fix is a shared types package: one types/ directory (or a monorepo package) that both the Next.js frontend and the API layer import from. One change to the type propagates everywhere. If EM1 doesn't have this already, it's an early contribution I'd want to make.
>
>  
>
> Discriminated unions for state. A compliance evaluation result has multiple states — PASS, PARTIAL, FAIL, INCONCLUSIVE — and each state has different fields (FAIL has gaps, INCONCLUSIVE has a review_required flag). A discriminated union models this correctly:
>
>  
>
> ```text
> type EvaluationResult =
>   | { verdict: "PASS"; evidence_quote: string; page_ref: string }
>   | { verdict: "FAIL"; evidence_quote: string; page_ref: string; gaps: string[] }
>   | { verdict: "INCONCLUSIVE"; reason: string; review_required: true }
>
> ```
>
> Now the compiler catches every place you handle FAIL but forgot to handle INCONCLUSIVE. That's a whole class of runtime bugs eliminated.
>
>  
>
> Typing LLM responses. LLM output is inherently dynamic — you can't trust its shape at the TypeScript layer directly. The pattern I use: Zod schema at the API boundary that validates and types the LLM response. The schema is the source of truth; the TypeScript type is inferred from it (z.infer<typeof evaluationResultSchema>). If the LLM returns an unexpected shape, Zod throws at the boundary — the error is caught and handled, not silently propagated as undefined into the UI. This is the TypeScript equivalent of the Pydantic output schema pattern I use on the Python side.
>
>  
>
> Strict mode. I always enable strict: true in tsconfig.json. It forces explicit null handling — string | null can't be used as string without a guard — which surfaces the "what happens when this field is missing?" question at compile time rather than at 2am in production.
>
>  
>
> In a Next.js App Router context specifically: The server/client component boundary creates a type safety concern — you can't pass non-serializable values (functions, class instances) from server components to client components as props. TypeScript doesn't catch this by default; it's a runtime error. The habit is: keep server component props to plain serializable types, use use client boundary components as the adapters that receive server data and attach event handlers.
>
>   
>
> ### SECTION 26: TERRAFORM vs CDK — DIRECT ANSWER 
>
>   
>
> JD says Terraform. You have CDK. This will come up. Don't be defensive — be direct.
>
>   
>
> #### The Question: 
>
>   
> - "We use Terraform. You have CDK experience. Is that a gap?" 
> - "What's your take on Terraform vs CDK? Do you have a preference?"  
>
> #### The Answer: 
>
>  
>
> CDK and Terraform solve the same problem — infrastructure as code — and the mental model transfers almost entirely. The syntax is different, the state management is different, the provider story is different. The underlying discipline — every resource in code, every environment reproducible, no click-ops — is the same.
>
>  
>
> My CDK experience is deep: 15+ stacks at Samay covering VPC, RDS, Lambda, Step Functions, AppRunner, ECS Fargate, Secrets Manager, S3. I've reasoned about dependency ordering between stacks, parameterized environments with context flags (--context env=staging), managed circular dependency problems between stacks, and debugged CloudFormation rollback failures. That reasoning process is the same in Terraform — HCL is a thinner layer over the same concepts.
>
>  
>
> The real differences I'd be ramping on:
>
>  
>
> Terraform's state management is explicit — the terraform.tfstate file (local or remote in S3/Terraform Cloud) is something you manage. CDK delegates state to CloudFormation behind the scenes. Understanding remote state backends, state locking (especially in a team context), and terraform import for existing resources are the Terraform-specific skills I'd build quickly.
>
>  
>
> Terraform's provider ecosystem is broader — it's cloud-agnostic, which matters when you're managing AWS and have future plans for any other cloud. CDK is AWS-native (though CDK for Terraform exists). For a company that's all-in on AWS, this is a minor consideration.
>
>  
>
> I've also written Terraform for Azure services at Samay — provisioned Azure resources alongside the AWS CDK stacks. Not deep Terraform experience, but enough to know the syntax and workflow.
>
>  
>
> Honest ramp: reading an existing Terraform codebase and contributing to it within a sprint. Independently writing new modules within 2-3 weeks with the existing codebase as reference.
>
>   
>
> ### SECTION 27: FULL-STACK SHIPPING — DAY-TO-DAY ACROSS LAYERS 
>
>   
>
> "Own and ship multiple small-to-mid-size features" — this is the role description. He wants evidence you can context-switch across backend/infra/frontend inside a normal sprint, not just one big project.
>
>   
>
> #### The Question: 
>
>   
> - "Walk me through how you actually work across the stack day to day." 
> - "Give me an example of a feature you shipped end-to-end — frontend to infra."  
>
> #### The Answer (Feature Story: Automated Control Testing at Samay): 
>
>  
>
> The clearest example is the automated control testing feature at Samay — from the "Test Control" button in the UI down to the CDK stack that deployed the Lambda.
>
>  
>
> The frontend slice: I built the FocusAreaDetail.jsx component — the control detail page. It had a "Test Control" button that needed to trigger the Lambda, show a loading state while the job ran, then display the returned compliance score, evidence quote, and gaps inline on the page. That's a React component with async state management, optimistic UI for the loading case, and error handling for Lambda timeout.
>
>  
>
> The API slice: The Next.js equivalent (in our case a FastAPI backend) needed a POST /controls/{id}/test endpoint that accepted the control ID, invoked the Lambda asynchronously, and returned a job ID. The Lambda result was written to S3 and the frontend polled for it.
>
>  
>
> The Lambda slice: Python Lambda function that collected from six data sources — AWS CloudTrail, Inspector, Security Hub, EntraID, GitHub, document embeddings — assembled the payload, called AWS Bedrock, structured the output as a Pydantic model, wrote to S3.
>
>  
>
> The CDK slice: The Lambda's IAM role needed permissions for all six sources — CloudTrail read, Inspector read, Secrets Manager access for Neo4j credentials, S3 write for results. I wrote the CDK construct, wired the execution role, added the environment variables, and deployed. When the IAM policy was wrong, CloudWatch had the error; I fixed the policy in CDK and redeployed.
>
>  
>
> The whole feature touched four layers in four different languages and runtimes. The discipline was: understand the full data flow before writing any code in any layer, so the interfaces between layers are correct from the start. Changing an interface after you've already built both sides costs double.
>
>  
>
> The pattern I bring to EM1: When picking up a feature ticket, I read the full system diagram first — what touches what. I don't start at the frontend and discover the Lambda needs a new permission three days later. I trace the request all the way through, identify the changes needed at each layer, and sequence them backend-first (so the API is testable before the UI exists).
>
>   
>
> ### SECTION 28: STAKEHOLDER INTERACTION & PRODUCT ROADMAP CONTRIBUTION 
>
>   
>
> 12-person company. Engineers talk to customers and EM operators directly. "Help shape the product roadmap" is in the role description. No stories existed for this.
>
>   
>
> #### Q: How do you work with non-technical domain experts like the EM operators on the team? 
>
>  
>
> The closest parallel I have is Samay, where I worked alongside a compliance domain expert with no engineering background to design and build the automated control testing system. She thought in audit procedures and control narratives. I thought in APIs, schemas, and Lambda functions. Early on, that gap caused real friction — I'd come out of a meeting thinking I understood what she needed and build something. She'd look at it and say "that's not what I meant."
>
>  
>
> The fix was simple but took a few cycles to land on: I stopped translating her language into mine during the conversation. I asked her to walk me through a real audit, step by step, as if I was a new auditor learning the job. I took notes in her language — "we need to see that config changes were tracked and reviewed," not "CloudTrail events." Then I did the translation afterward, alone.
>
>  
>
> The six-source data model for the automated testing system came entirely out of that session. She had never heard of CloudTrail. She knew she needed to see that config changes were tracked. Those are the same thing — but only once you've done the translation carefully.
>
>  
>
> At EM1 the equivalent is the EM operators on your team. They know what Emergency Managers need; I know how to build the system. The interface between those two things is the most important relationship to get right. I'd approach it the same way: watch them use the current product before writing any code for the next feature. Ask "what's the worst part of this?" before asking "what do you want to build?"
>
>   
>
> #### Q: Have you ever contributed to product direction, not just implementation? 
>
>  
>
> At Samay, by the time I was 2-3 months in, I was the person in the room with the most context on what the system could and couldn't do. That put me in product conversations by default — not because I had a PM title, but because nobody else knew the technical constraints well enough to reason about trade-offs.
>
>  
>
> The clearest example: the team was considering adding a real-time alert feature for compliance score drops — an agency's score changes and they get notified immediately. My contribution to that conversation was: "real-time means we're re-running 111 LLM evaluations every time any plan section changes. Here's the cost implication at our current scale. Here's an alternative: delta-only re-evaluation — only re-run the guidelines whose source sections changed — which gets you 80% of the value at 15% of the cost." That's not a PM decision or a pure engineering decision — it's the place where cost, architecture, and product behavior intersect, and it requires someone who understands all three.
>
>  
>
> That's the kind of input I want to bring to EM1's roadmap discussions. Not "here's what I want to build" — but "here's what this feature actually costs to operate, here's the architectural implication of that choice, here's an alternative that might serve the same user need with less complexity." Engineers who can reason that way make product teams better.
>
>   
>
> #### Q: Tell me about a time you had to simplify a complex technical constraint for a non-technical person. 
>
>  
>
> At Epik, a senior stakeholder wanted the AI incident triage pipeline to switch to autonomous mode immediately — it was performing well in testing, why wait?
>
>  
>
> The real constraint was: in testing, the false positive rate was acceptable but not production-calibrated. In production, a false positive meant a real analyst ignoring a real threat because the system had cried wolf. That's not a UX bug — it's a security gap.
>
>  
>
> I didn't explain false positive rates or precision-recall trade-offs. I said: "Think of it like a new hire. They passed the interview — they're clearly capable. But you wouldn't let them make final calls on major incidents on day one without anyone checking their work. The two-week shadow period is the same thing — we watch what it recommends, compare it to what experienced analysts would do, and calibrate where it's overconfident before we let it act alone."
>
>  
>
> She understood immediately. The two-week shadow period became part of the plan with no further argument.
>
>  
>
> The principle: technical constraints land when they're translated into human dynamics the other person already understands. Almost everyone knows what it means to ramp up a new team member. Almost no one knows what precision-recall calibration means in a production classifier.
>
>   
>
> #### Q: How do you think about contributing to the product roadmap as an engineer? 
>
>  
>
> I think the most useful thing an engineer can bring to a product conversation is: "here's what this feature would actually cost to build and operate, and here's what the architecture would need to support it."
>
>  
>
> Most feature ideas are good in the abstract. The engineering contribution is grounding them in reality — not as a blocker, but as a constraint that shapes the design. "We could build real-time plan monitoring, but here's what that means for our LLM API bill and our infrastructure. Here's a version that gives the customer most of the value with a quarter of the complexity."
>
>  
>
> At Samay I was in those conversations regularly because I had the full-stack context no one else had. At EM1 I'd want to be in them too — especially on the compliance module roadmap and the agent skills direction, where the technical decisions have product implications that might not be visible until you've tried to build it.
>
>  
>
> The other angle: I pay attention to what's painful in what I'm building. If I'm implementing a feature and the data model is fighting me, that's signal — either the model is wrong or the feature is more complex than it appears. I surface that early rather than absorbing it silently.
>
>   
>
> #### Q: You'd be working with EM operators who are domain experts, not engineers. What does that collaboration look like day-to-day? 
>
>  
>
> The honest dynamic: they know more about the domain than I ever will. I know more about the system than they ever need to. The useful overlap is: they can tell me whether a feature is solving the right problem; I can tell them whether the solution is feasible and what it costs.
>
>  
>
> Day-to-day, that means: before I spec out a feature, I want to understand the current manual process it's replacing — not from a requirements doc, from watching someone do it. After I build something, I want to get it in front of an EM operator before it ships to customers — not for QA, for "does this match how you actually think about the problem?"
>
>  
>
> The risk I try to avoid: building technically correct features that miss the domain nuance. At Samay, the compliance chatbot I built gave technically accurate answers about access relationships — but compliance auditors didn't care about raw access data, they cared about whether the access pattern satisfied a specific control narrative. That's a domain nuance no amount of engineering can substitute for. Getting it requires being close to the people who live in it.
>
>   
>
> Appended June 8, 2026 — Sections 25–28: TypeScript depth, Terraform vs CDK, full-stack shipping story, stakeholder interaction + roadmap contribution

## Source provenance

- [Original HTML](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Interview%20Prep%20company%20prep%20docs/EM1/Round2_Interview_Prep.html) · Interview Prep company prep docs/EM1/Round2_Interview_Prep.html
- [Original MD](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Interview%20Prep%20company%20prep%20docs/EM1/Round2_Interview_Prep.md) · Interview Prep company prep docs/EM1/Round2_Interview_Prep.md

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
