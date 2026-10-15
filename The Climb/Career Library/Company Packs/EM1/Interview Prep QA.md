---
kind: "company-prep"
title: "Interview Prep QA"
collection: "EM1"
topic: "Interview Prep"
imported: "2026-10-13"
source_files: ["Interview Prep company prep docs/EM1/Interview_Prep_QA.md"]
tags: ["career/library"]
source_status: "source-claims-not-verified"
---

# Interview Prep QA

[[The Climb/Career Library/Career Library]]

> [!info] Source context
> Historical preparation or source notes. First-person stories and numeric outcomes remain source claims until confirmed; this import does not verify them.

# EM1 Interview Prep — Neel Gali
### 30-Minute Intro Chat with Gunnar (Co-founder & CTO)
**Format:** Casual conversation — Gunnar wants to learn your background, what motivates you, and tell you about EM1.
**Date:** June 2026 | **Role:** Full Stack Software Engineer ($150k–200k, fully remote)

---

## The Company at a Glance

| | |
|---|---|
| **Tagline** | "The first AI-powered co-pilot for Emergency Management" — safe, trustworthy AI tools for Emergency Managers |
| **Product** | Three-module platform: **Evaluate (E01)**, **Improve (E02)**, **Operationalize/Chat (E03)** |
| **Plan types supported** | EOPs (Emergency Operations Plans), HMPs (Hazard Mitigation Plans), COOPs (Continuity of Operations Plans) |
| **E01 — Evaluate** | Automated crosswalk of plans against FEMA or State guidelines; unlimited evals; **Smart References** (maps each guideline to the exact page in the plan that answers it); accelerates HMP compliance pass rates |
| **E02 — Improve** | Plan Library of industry best practices; **Peer Docs** (compare your plan to peer agency plans); **Deconflict** (instantly surface and resolve contradictions across plans) |
| **E03 — Operationalize** | Custom knowledge base (upload EOPs, IAPs, AARs, any doc); Fed + State Library; **real-time answer engine** — type a question, get an instant answer cited to your docs |
| **AI Differentiator** | LLM grounded directly in doctrine + After Action Reports; **sentence-level citations** back to source pages; human-in-the-loop by design — not autopilot |
| **Traction** | 40+ agency customers across the US |
| **Team** | Small — software engineers + experienced emergency management operators |
| **Stack** | Next.js, TypeScript, PostgreSQL, AWS, Terraform, LLM workflows |

### The Founders

| | |
|---|---|
| **Tyler Felous** (CEO) | 15 years building software and companies; previously co-founded, built, and **sold Wisely** (fintech/wage access); driven by family and climate resilience to build for emergency management |
| **Gunnar Holwerda** (CTO) | Engineering leader who **architected systems and grew teams at OpenSesame** (enterprise B2B SaaS, HR/learning platform) **and Olo** (restaurant tech platform, high-scale B2B SaaS); mission: enable a more effective world through software and develop the next generation of Emergency Managers |

**What this tells you about Gunnar:** He's been on scaling teams at real SaaS companies — OpenSesame and Olo are both growth-stage/mature B2B platforms. He knows what production engineering at scale looks like. He'll respect concrete, production-grade stories over buzzwords. He's also mission-driven, not just technical — he cares about enabling the next gen of Emergency Managers. Mirror that energy.

### Domain Terminology Cheatsheet

| Term | Meaning |
|---|---|
| **EOP** | Emergency Operations Plan — the master plan for responding to disasters |
| **HMP** | Hazard Mitigation Plan — FEMA-required plan to reduce disaster risks; must pass periodic assessments |
| **COOP** | Continuity of Operations Plan — how an agency keeps functioning during a disaster |
| **IAP** | Incident Action Plan — operational plan for a specific incident |
| **AAR** | After Action Report — post-incident analysis of what worked and what didn't |
| **EOC** | Emergency Operations Center — command and coordination hub during a disaster |
| **FEMA** | Federal Emergency Management Agency — sets national doctrine; EM1 evaluates plans against FEMA guidelines |
| **Doctrine** | The authoritative federal/state guidance EM managers are required to follow |

---

## Section 1: The Core Stories

> These are your anchors. Know them cold and reference them naturally.

### Story A — TrustX ATAP (Samay Systems): The AI Compliance Platform
The most directly relevant project. You built an end-to-end automated compliance testing system for a B2B SaaS product.

**What you built:**
- **Profile-360 Pipeline** — AWS Lambda + Step Functions orchestration pulling data from GitHub, Jira, and EntraID into Neo4j graph databases for LLM-powered compliance analysis
- **Automated Control Testing** — Lambda workflow that collects AWS infra data, runs document embedding lookups, then uses an LLM to auto-generate compliance scores and evidence for controls (e.g., TX-MON04.01)
- **Multi-tenant Architecture** — Dynamic tenant resolution from RDS PostgreSQL, per-tenant S3 buckets, per-tenant Neo4j instances — all fully isolated
- **AppRunner AI Query Service** — Containerized Flask API for natural language → Cypher query processing, integrated with LangChain `.invoke()`, VPC-connected
- **React Frontend** — Controls dashboard, detail pages, evidence management, comments system, document editor

**Key analogy to EM1:** EM1 uses an LLM agent to draft plan updates citing AARs and doctrine. You built an LLM agent that tests compliance controls by citing AWS infra data and document embeddings. It's the same pattern: grounded AI → structured evidence → human-in-the-loop review.

---

### Story B — Full Stack at Epik Solutions: AI-Powered Enterprise Platform
- LangGraph-based agentic workflows (automated alert triage, structured outputs from GPT-4o)
- RAG pipelines using Pinecone + LangChain over enterprise corpora
- React.js real-time streaming UI with WebSockets
- AWS ECS/Lambda/S3/SQS, Docker, Kubernetes, GitHub Actions CI/CD
- Led sprint planning and code reviews for a 6-engineer team

---

### Story C — Zemoso Technologies: Foundation
- Full-stack Spring Boot + React.js + PostgreSQL for a LabOps platform
- Built TypeScript React component libraries, normalized PostgreSQL schemas
- Spring Security RBAC, JUnit + Jest testing discipline

---

## Section 2: Expected Questions & Strong Answers

---

### Q: Tell me about yourself / Walk me through your background.

**Answer:**
> "Sure — I started at Zemoso Technologies building full-stack SaaS products on Spring Boot, React, and PostgreSQL. That gave me a strong foundation across the entire stack. From there I moved to Samay Systems, which is where my work got much more interesting from an AI standpoint. I was building a compliance automation platform — essentially using LLMs to automatically test compliance controls by collecting data from AWS infrastructure, integrations, and document embeddings, then generating scored evidence reports. That's where I really got deep into RAG, Lambda orchestration, and multi-tenant architecture on AWS.
>
> Most recently at Epik Solutions I've been doing more agentic work — LangGraph workflows, real-time streaming frontends with WebSockets, and more structured LLM output pipelines. In terms of ownership, at Samay I wasn't just implementing tickets — I architected the CDK stacks, owned the Lambda suite end-to-end, and built out the React frontend controls UI from scratch. I like that kind of full-spectrum ownership."

**Key beats:** Zemoso (foundation) → Samay (LLM compliance, real ownership) → Epik (agentic, production AI). End with ownership.

---

### Q: What do you know about EM1 / what do you know about what we're building?

> *(This is Gunnar checking if you actually dug. Have this ready.)*

**Answer:**
> "Yeah, I spent some time on the site and found the three-module structure really clearly thought out. You have Evaluate — the automated FEMA crosswalk that tells an agency exactly which guidelines they pass or need to fix, with Smart References mapping each requirement to the specific page in their plan. Then Improve — the Plan Library and Peer Docs features so agencies can see how comparable agencies handled a section they're weak on. And then Operationalize — turning the entire document corpus, including AARs and IAPs, into a real-time answer engine.
>
> What clicked for me was the Deconflict feature in Improve — agencies have multiple plans that can contradict each other, like an EOP and a COOP saying different things about who activates the EOC. That's a subtle problem that would be invisible without automated detection across the full doc set.
>
> The agent that works across those tools to draft plan updates — citing best practices from other agencies and lessons from AARs — is where the sentence-level citation design makes or breaks the product. A wrong citation in a preparedness plan isn't a UX bug, it's a liability. Getting that grounding right is the hard part.
>
> And I noticed you're specifically targeting HMP compliance — getting Hazard Mitigation Plans to pass their FEMA assessment on the first submission is a real pain point because those assessments are expensive and time-consuming to redo."

---

### Q: What excites you about EM1 specifically?

**Answer:**
> "A few things. The problem is genuinely high-stakes — when the software helps an agency build a better EOP or HMP, that's not a product metric, that's preparedness that affects real disaster outcomes. That feedback loop is rare.
>
> The architecture matches work I've actually done. At Samay I built an LLM system that automatically tested compliance controls — collected data from multiple sources, assembled context, passed it to an LLM, generated a scored evidence report with citations. Your Evaluate module and the AAR-citing agent are the same pattern: ground the model in the right corpus, retrieve precisely, show your work. I care a lot about getting that part right.
>
> And the scale and ownership. Small team, 40+ real customers, co-founders who came from OpenSesame and Olo — that's not a side project, that's a real SaaS business being built by people who know how to scale engineering. I want to be in that environment and help shape it, not just take tickets."

---

### Q: What's your experience with LLMs and RAG?

**Answer:**
> "Hands-on and production-grade. At Samay, I built a RAG-adjacent system where Lambda functions would collect data from multiple sources — AWS infra metadata, GitHub/Jira integration data, and document embeddings stored in PostgreSQL — then pass that assembled context to an LLM to generate a compliance verdict. The embedding + retrieval part was backed by PostgreSQL and S3, with Neo4j for graph traversal.
>
> At Epik I built more classical RAG with Pinecone as the vector store and LangChain retrieval chains. I also built eval harnesses using Langfuse with golden datasets to track retrieval precision, hallucination risk, and latency regressions before every production rollout.
>
> I care a lot about the grounding problem — making sure LLMs answer from the right sources, not from hallucination. Given that EM1 does sentence-level citations from doctrine and AARs, that resonates directly with work I've done."

---

### Q: Have you worked on Next.js? (It's in their stack but not prominently in your resume)

**Answer:**
> "My frontend work has primarily been React and TypeScript, which Next.js is built on — so I'd pick it up very quickly. I've built real-time streaming UIs, role-based dashboards, multi-step form workflows, and complex data grid components in React and TypeScript. The App Router, server components, and RSC model are the main new concepts, but the fundamentals are the same. I've shipped production React at all three companies."

**Tip:** Don't oversell Next.js — be honest but frame it as a fast ramp from solid React/TS experience.

---

### Q: What's your Terraform / AWS / infrastructure experience?

**Answer:**
> "At Samay I provisioned the full AWS infrastructure using CDK (which is the TypeScript-based IaC tool in the same family as Terraform). I owned CDK stacks for Lambda functions, Step Functions orchestration, AppRunner services, RDS PostgreSQL, S3 buckets with per-tenant isolation, and Secrets Manager. I also provisioned some Azure services with Terraform.
>
> On the AWS side specifically: Lambda, Step Functions, AppRunner, ECS, RDS, S3, SQS, Secrets Manager — all production usage. I'm comfortable with VPC configuration, IAM policies, and environment parity across dev/staging/prod."

---

### Q: What does ownership mean to you in practice?

**Answer:**
> "To me ownership means you care about the outcome, not just your slice of the ticket. At Samay, when we were building the automated control testing system, I wasn't just implementing the Lambda function — I was thinking about how the CDK stack should be structured, what happens when a tenant's Neo4j credentials rotate in Secrets Manager, how the front-end React component should display partial evidence results. I filed the bugs I found in adjacent systems. I proactively flagged when a database schema decision in week two was going to cause pain in week eight.
>
> It also means being the person who knows the system well enough that when something breaks at 2pm on a Friday, you can diagnose it without a runbook."

---

### Q: Tell me about a time you worked across the full stack end-to-end.

**Answer (STAR format):**
> "The TrustX Automated Control Testing feature is the cleanest example. The goal was: given a compliance control like TX-MON04.01, automatically collect all evidence, score it, and present it to a compliance officer.
>
> **Situation:** Manual compliance reviews were slow and inconsistent — reviewers were manually pulling AWS config data, Jira tickets, and policy documents to build a case.
>
> **Task:** I owned the entire end-to-end build — AWS infrastructure, data pipeline, LLM integration, and the React frontend.
>
> **Action:** I built Lambda functions that collect AWS infra data, integration data from GitHub and Jira, and document embeddings from PostgreSQL. Those get assembled into a context payload that gets sent to an LLM which generates a compliance score and evidence summary. The results flow back through the Step Functions pipeline and get surfaced in a React controls detail page I built, with comments, evidence management, and status updates.
>
> **Result:** Reduced manual evidence review by 45% across monthly compliance cycles. Fully tested TX-MON04.01 and architected it to be generic enough to expand to any control."

---

### Q: You've worked in compliance — what do you know about the emergency management / public safety domain?

**Answer:**
> "Not a domain expert, and I'd lean on the operators on your team to close that gap fast. But I've done my homework. The core workflow is: agencies manage multiple plan types — EOPs for response, HMPs for mitigation, COOPs for continuity — and those plans have to pass periodic FEMA assessments and stay aligned with current doctrine. The challenge is the plans are long, they reference each other, they go stale after incidents, and Emergency Managers are often understaffed relative to the volume of plans they're responsible for.
>
> The AAR piece is particularly interesting to me — after an incident, agencies produce After Action Reports that capture lessons learned, but that institutional knowledge usually just sits in a document somewhere. Turning AARs into a retrieval layer that gets cited when drafting plan updates is genuinely smart. It's like giving every new Emergency Manager access to the lessons of every incident that came before them.
>
> On the AI side, the compliance analogy is tight — I built systems where auditors can't accept an LLM verdict without seeing the evidence trail. Same deal here: an Emergency Manager can't update their EOP based on an AI suggestion they can't verify. The sentence-level citation design is the right answer for this domain."

---

### Q: Why do you want to leave your current role?

**Answer:**
> "Epik is a good team and I've learned a lot building AI features there. But I'm ready for something where I have more direct influence on product direction and where the domain itself matters more. At a company like EM1 — small team, real users in public safety, building something from the ground up — every architectural decision I make has visible impact. That's the environment I want to be in for the next phase."

---

### Q: What motivates you as an engineer?

**Answer:**
> "Two things: the feedback loop between what I build and real outcomes, and the challenge of making AI systems actually reliable in production. The LLM space is full of demos that don't survive contact with real users. I'm motivated by closing that gap — building the eval harnesses, the grounding mechanisms, the observability pipelines that make an AI feature trustworthy enough to put in front of practitioners who depend on it. EM1's emphasis on keeping humans in the loop and citing doctrine is exactly that philosophy."

---

### Q: What's your experience working on a small team?

**Answer:**
> "At Samay I was effectively the sole engineer on the TrustX compliance platform — I owned the CDK infrastructure, Lambda suite, AppRunner services, and the React frontend. There was no dedicated DevOps, no dedicated frontend engineer — you just figure it out or the feature doesn't ship. I prefer that. I like having context across the whole system because it makes you a better architect. You know where the bodies are buried."

---

## Section 3: Technical Quick-Fire

| Question | Strong Answer |
|---|---|
| **What is RAG and when do you use it?** | Retrieval Augmented Generation — retrieve relevant context from a vector store or structured DB and inject it into the LLM prompt instead of relying on parametric memory. Use it when the knowledge is domain-specific, changes frequently, or needs to be cited. |
| **How do you evaluate LLM quality in production?** | Eval harnesses with golden datasets; track retrieval precision (are the right chunks retrieved?), faithfulness (does the answer match the context?), hallucination rate, and latency. I've used Langfuse for this — dashboards + regression alerts on every deploy. |
| **PostgreSQL — any performance work?** | Index design (GIN for full-text, B-tree for FK lookups), query plan analysis with EXPLAIN ANALYZE, normalized schema design to avoid N+1 patterns, schema migrations with zero-downtime via additive changes first. |
| **Terraform vs CDK?** | Same IaC philosophy, different syntax layer. Terraform is provider-agnostic HCL; CDK is TypeScript/Python with CloudFormation underneath. I've used CDK for AWS heavily — prefer it for TypeScript shops because the type safety is excellent. Terraform experience on mixed AWS + Azure environments. |
| **What's a Lambda cold start and how do you mitigate it?** | First invocation after idle period — container initialization latency. Mitigations: provisioned concurrency for latency-critical paths, keep handler lightweight (lazy imports), use Lambda layers for large dependencies. |
| **How would you approach multi-tenant data isolation?** | Dynamic tenant resolution (JWT → tenant ID → lookup in control plane DB), tenant-specific schemas or row-level security in PostgreSQL, separate S3 prefixes or buckets per tenant, tenant-scoped Secrets Manager keys. This is exactly what I built at Samay/TrustX. |
| **Next.js App Router vs Pages Router?** | App Router is the current direction — server components by default, layouts, streaming, and nested routing. Pages Router is the legacy model with getServerSideProps / getStaticProps. I'd ramp on App Router; the React mental model is the same. |

---

## Section 4: Questions to Ask Gunnar

> Ask 3–5 of these. Pick ones that flow naturally from the conversation. The starred ones ⭐ are highest signal — they show you read the product carefully.

### About the Product
1. ⭐ **"The Deconflict feature — detecting contradictions across multiple plans — is really interesting architecturally. Are you doing that with LLM reasoning over the full doc set, or more of a structured semantic similarity approach?"**
2. ⭐ **"For the real-time answer engine in the Operationalize module — when an EM asks 'who activates the EOC?' and there are multiple plans in the knowledge base that answer differently, how does the system handle that conflict in the response?"**
3. **"The sentence-level citations — are you chunking AARs and doctrine into a vector store for retrieval, or is the grounding more structured than classical RAG?"**
4. **"When the agent drafts plan updates citing peer agency best practices — is that pulling from a curated EM1 library you maintain, or are agencies able to upload peer docs and reference them directly? I saw the Peer Docs feature but curious how deep that goes into the agentic side."**

### About Engineering Culture
5. **"You came from OpenSesame and Olo — both real B2B SaaS companies at scale. What engineering habits from those environments are you deliberately bringing into EM1, and what are you leaving behind?"**
6. **"What does a typical sprint or release cycle look like right now — how often are you shipping to the 40+ customers?"**

### About Growth & Domain
7. **"The team combines software engineers with EM operators. How does the domain knowledge transfer work day-to-day — do engineers sit in on customer sessions or read AARs as part of onboarding?"**
8. **"What's the biggest technical problem on the roadmap right now — something an engineer joining in the next few months would own end-to-end?"**

### About the Role
9. **"What does success look like at 3 months and 12 months for this role?"**

---

## Section 5: Rapid-Fire Alignment Points

Use these to weave into conversation naturally — they show you've read the JD carefully.

| EM1 Says | Your Angle |
|---|---|
| *"Engineers who take ownership"* | "At Samay I owned the entire TrustX platform — CDK, Lambda suite, React frontend, no handoffs" |
| *"Human-in-the-loop for a human-centric industry"* | "That's the right call. I built compliance systems where auditors need to verify every LLM output — citation + evidence trails are non-negotiable" |
| *"Grounded in doctrine, sentence-level citations"* | "That solves the hallucination problem for high-stakes domains. I've built similar grounding in compliance — LLM cites specific document passages, not general knowledge" |
| *"Small team, software engineers + EM operators"* | "Best learning environment — you build with more context and ship with more care" |
| *"Ship quickly in Next.js, TypeScript, PostgreSQL, AWS, Terraform"* | "That's my stack. PostgreSQL + AWS + IaC + TypeScript full-stack is exactly what I've been doing" |
| *"40+ customers across the country"* | "Real product, real users, real urgency — not a prototype" |

---

## Section 6: Opening & Closing Moves

### Opening (if Gunnar asks you to go first)
> "Happy to. I'm Neel — I've been a full-stack software engineer for about 6 years, most recently building AI-powered compliance automation at Samay Systems and then production LLM features at Epik Solutions. The TrustX work I did at Samay is probably the most directly relevant to EM1 — I was building an LLM agent that automatically tested compliance controls by assembling evidence from multiple data sources and generating a grounded, cited verdict. When I read about what EM1 is doing — grounding the model in doctrine and AARs, sentence-level citations, keeping Emergency Managers in the loop — it felt like a natural next step in the same direction, in a domain that has real stakes."

### Closing (end of 30 minutes)
> "Thanks Gunnar — I really appreciated you explaining the product in more depth, especially the [something specific they mentioned]. I'm genuinely excited about this one — the combination of real ownership, an AI stack I've been working in, and a domain where the software can affect actual emergency outcomes is rare. I'd love to stay in the conversation."

---

## Section 7: Logistics & Mindset

- **Length:** 30 minutes. Don't over-explain. Give 2–3 sentence answers and let Gunnar follow up.
- **Energy:** Gunnar is a co-founder/CTO hiring for ownership. Be direct, confident, and concrete. Skip hedging.
- **Tone:** This is a conversation, not an interrogation. Ask back. Show genuine curiosity about EM1's architecture.
- **Gunnar's background:** He was an engineering leader at **OpenSesame** (enterprise learning/HR SaaS) and **Olo** (restaurant tech platform). Both are real B2B SaaS companies — he knows what a professional engineering org looks like. Concrete, production numbers will land well with him.
- **Tyler Felous (CEO)** built and sold **Wisely** (fintech). You likely won't talk to Tyler in round 1 but good to know.
- **The "Cardinal Health" mention:** Gunnar's email references "Cardinal Health" — if he brings this up, just confirm and speak to the PostgreSQL/AWS/Terraform work at Samay Systems (your compliance platform work covers all of this). Don't let a company name discrepancy throw you.
- **Red flags to avoid:** Vague answers ("I've done some LLM work"), underselling ownership ("I mostly implemented what was scoped"), or being passive about motivation ("It seems like a good opportunity").

---

*Generated June 2, 2026 — EM1 Intro Call with Gunnar*


## Source provenance

- [Original MD](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Interview%20Prep%20company%20prep%20docs/EM1/Interview_Prep_QA.md) · Interview Prep company prep docs/EM1/Interview_Prep_QA.md

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
