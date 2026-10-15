---
kind: "company-prep"
title: "Casca Interview Prep"
collection: "Casca"
topic: "Interview Prep"
imported: "2026-10-13"
source_files: ["Interview Prep company prep docs/Casca/Casca_Interview_Prep.html","Interview Prep company prep docs/Casca/Casca_Interview_Prep.md"]
tags: ["career/library"]
source_status: "source-claims-not-verified"
---

# Casca Interview Prep

[[The Climb/Career Library/Career Library]]

> [!info] Source context
> Historical preparation or source notes. First-person stories and numeric outcomes remain source claims until confirmed; this import does not verify them.

# Casca — Forward Deployed Engineer: Interview Prep

> **Role:** Forward Deployed Engineer (FDE) — Casca  
> **Stack they want:** TypeScript, React, Next.js (must-haves) + Postgres/Prisma, Python, AWS  
> **Phone screen with:** Samantha Harvey Fleeman (LinkedIn Full Service Hiring)  
> **Format:** Phone screen — behavioral + fit, ~30 min. No deep technical yet.

---

## TABLE OF CONTENTS
1. [Phone Screen — Recruiter Questions](#1-phone-screen--recruiter-questions)
2. [Behavioral / FDE Mindset](#2-behavioral--fde-mindset)
3. [Technical — Surface Level](#3-technical--surface-level)
4. [Casca-Specific / Domain Knowledge](#4-casca-specific--domain-knowledge)
5. [Culture / Startup Fit](#5-culture--startup-fit)
6. [Quick Reference](#6-quick-reference)

---

## 1. PHONE SCREEN — RECRUITER QUESTIONS

---

### Q1: Walk me through your background briefly.

I'm a full-stack software engineer with about four years of experience. The last two years have been almost entirely in AI-augmented production systems — LLM pipelines, agentic workflows, and automation tools built for real enterprise users.

At **Epik Solutions**, my current role, I'm embedded with enterprise security teams building AI-driven triage pipelines on top of Azure OpenAI. We process over a thousand security events a day and cut analyst workload by 30%. The key work there was designing and shipping a LangGraph-based agent that automatically pivots across multiple internal security tools — something SOC teams previously had to do manually for every alert.

Before that, at **Samay Systems**, I was the founding engineer on TrustX — a compliance automation SaaS. I was the sole engineer. I built the entire product from zero: 15+ AWS CDK stacks, a React TypeScript dashboard, an LLM evaluation pipeline on AWS Bedrock, a Neo4j identity graph, and an MCP-based AI chatbot. We went from a blank repo to 3 paying B2B enterprise customers. Compliance officers using the platform cut their manual evidence review time by 45%.

The thread across both: I've always worked close to the people who use the software. At Epik, that's SOC analysts. At Samay, it was compliance officers. I sit in on their workflows, understand what's actually tedious, and then build automation that targets those exact friction points. That's exactly what forward deployed engineering is — and it's the model I want to double down on at Casca.

---

### Q2: Where have you had the most direct exposure to customers or end users influencing what you built?

Two clear examples — one at each company.

**At Epik Solutions (SOC teams):** I regularly did shared-screen shadowing sessions with security analysts. I'd watch them handle a live critical alert — and what I saw was that a single alert required them to manually query three different internal tools just to get enough context to make a triage decision: check the asset inventory, query the threat intelligence feed, look up the user's recent access logs. That wasn't a complaint they'd ever written down in a ticket. I only saw it by watching. I took that workflow and directly mapped it to what the LangGraph agent would automate — those three pivoting steps became three agent tool calls. The agent now does in 4 seconds what took an analyst 8-10 minutes of context switching.

**At Samay Systems (compliance officers):** During early tenant onboarding I sat down with compliance managers and watched them work. They'd manually open hundreds of vendor PDFs, hunt for specific clause language — things like data retention policies, encryption standards — and log it all in a spreadsheet. The part that struck me wasn't the volume; it was the cognitive load of holding three different framework requirements in their head at once while reading. That specific observation shaped how I built the LLM evidence evaluation — I designed the output schema to surface a verdict, a verbatim evidence quote, and a source reference in one card, so the auditor only needs to confirm, not re-derive. Direct workflow observation drove direct design decisions.

---

### Q3: At Samay Systems — what did "owned end-to-end modules" actually look like in practice? Were those tied to live product usage?

Absolutely live product — 15 enterprise tenants in production.

"End-to-end" at Samay meant: I took a feature from conversation with the founders all the way to a customer using it in production, with no other engineer involved.

A specific example is the automated control testing pipeline. The compliance officer would log in, click "Run Test" on a control — say CC7.1 (System Monitoring) — and within a few minutes the platform had: collected evidence from GitHub, Jira, AWS Config, and AWS Inspector; run an LLM evaluation on AWS Bedrock with a structured Pydantic schema; applied an evidence-gating check (if the quote wasn't verbatim in the retrieved context, the verdict flipped to INCONCLUSIVE instead of hallucinating a PASS); and surfaced the result with a color-coded verdict, evidence quote, and source reference.

I owned every layer of that: the Lambda evidence collectors, the Step Functions orchestration, the Bedrock LLM evaluation, the Flask API endpoint, the React UI components, the CDK infrastructure (IAM roles, SQS queues, S3 buckets), and the test suite. Real compliance officers used it. When the founders demoed it to a prospect and the customer asked "can you run this for access controls too?" — I shipped the generic version in two days because I understood every part of the system.

---

### Q4: How much of your experience has followed the loop — understand workflow → build quickly → iterate?

It's been the primary loop in both roles. The clearest example:

At Samay, after I watched compliance officers struggling with the PDF review workflow, I didn't go back and spec out a six-week project. I built a single-control proof of concept in a week: collect evidence from one source (GitHub), run it through a prompt, return a verdict. Showed it to the founders and the first paying customer in the same meeting. Their feedback that session: "It works, but if the confidence is below 80%, I want it flagged for human review, not auto-passed." I had that change live by the next day. The second iteration feedback: "I need to see exactly which line of which document you used." That forced the evidence-gating architecture — not because I thought of it upfront, but because real users told me what trust actually required.

At Epik, the same loop: I ran the LangGraph triage agent past SOC leads every two weeks with new capabilities. They'd run it against real historical alerts and tell me which tools it was calling unnecessarily and which it was missing. That feedback shaped the tool selection logic directly.

The loop you're describing — understand, build, iterate with real users — isn't a methodology I read about. It's just how I've always worked.

---

### Q5: Why Casca specifically? Why forward deployed over a traditional eng role?

Three things make Casca specifically interesting.

First, the problem is real and underserved. Small business lending taking 90 days is not a UI problem or a process problem — it's a structural automation deficit. Banks have decade-old systems, and the manual work is genuinely painful. That's the kind of problem where AI actually earns its value rather than being bolted on for appearances.

Second, the model is right. Most AI in fintech is advisory — "here's a recommendation, a human will decide." Casca is actually automating the workflow. That requires the kind of deep operator understanding you only get by sitting with them on-site. The forward deployed model is the only way to build software that actually changes how an underwriter works, not just how they get a dashboard update.

Third, it matches how I already work best. At Samay and Epik, my best engineering came from being in the room with the people using the software. Traditional sprint-based product roles put distance between me and that feedback. The FDE structure removes that distance by design, and that's where I know I do my best work.

---

### Q6: Are you open to roughly one week per month travel on-site with bank customers?

Yes — that's not a constraint, that's the draw. The on-site time is where you get the signal that no amount of Slack or Jira can replicate. Watching someone work in their actual environment tells you things they can't articulate in a requirements doc. One week per month on-site is very workable, and for the right deployment I'd be comfortable with extended time if that's what the customer situation calls for.

---

### Q7: What are your compensation expectations?

I'm targeting a base in the $135K–$155K range depending on the overall package and equity structure. I'm flexible on the mix — meaningful equity at a YC-backed company at Casca's stage is part of the comp story, and I take that seriously. Happy to talk specifics once we move forward.

---

### Q8: Are you open to relocation?

Yes. If the team and role are the right fit, relocation is on the table. I saw that you offer relocation support, which I appreciate — it removes the logistics barrier. Where is the team primarily based?

---

## 2. BEHAVIORAL / FDE MINDSET

---

### Q9: Tell me about a time you sat with a user and discovered something that changed what you built.

At Epik I had a moment that completely reframed what I was building. I was in a screen-share with a senior SOC analyst reviewing how she handled a P1 alert. I expected her to demonstrate the tool usage flow I'd designed — query asset inventory, cross-reference threat intel, triage. Instead, she spent the first four minutes figuring out *which system* had the asset record she needed, because asset ownership in the organization was split across three tools depending on whether the asset was cloud, on-prem, or a SaaS vendor.

I had built the agent assuming one asset inventory source. The discovery changed the architecture: the agent now runs three parallel lookups against all three sources and merges the results. That parallel call pattern added two weeks of engineering time but it's why the agent actually works in production — because I watched the reality, not the theory.

---

### Q10: Give me an example where you had to build fast and ship something imperfect. How did you handle the tradeoff?

At Samay, document management for compliance artifacts. We needed to support PDF and DOCX uploads — compliance teams have existing documentation. I evaluated four conversion approaches and all of them had problems: `python-docx` had 15–20% formatting loss on round-trips, LibreOffice headless ballooned the Lambda package to 250MB (at the architectural limit), a dedicated conversion service was 2+ weeks off-roadmap.

I shipped with a known limitation: uploaded DOCX/PDF files are stored as binary in S3 with a `readonly` flag — users can view them in an embedded viewer but not edit them in the platform. Documents created natively in the platform work with full fidelity and full editing. I documented this explicitly: "Uploaded DOCX/PDF are view-only. Create compliance documents in-platform for full editing."

Why it was the right call: compliance teams' working documents were already being created natively. Legacy uploads were reference material, not documents they actively edited. Shipping a known, explicit limitation is better than shipping a feature that silently corrupts compliance documents — especially in a context where document integrity has legal weight. I also put the recommended fix in the engineering handoff with an effort estimate so the path forward was concrete, not just punted.

---

### Q11: Describe a time you owned something end-to-end. What broke and how did you fix it?

TrustX at Samay was end-to-end ownership by necessity — I was the only engineer. The clearest "something broke" story: a production incident the day after deploying the multi-tenant nightly pipeline.

Step Functions ran three Neo4j ingestion Lambdas in parallel for each tenant. In dev, with 1-2 tenants triggered manually, it ran fine. In production, with EventBridge firing all tenant executions simultaneously at 2 AM: `ServiceUnavailable: Connection pool size of 50 exceeded`. Three Lambdas at default 50 connections each, times three concurrent tenant executions, equals 450 simultaneous Neo4j connections against instances sized for 50. Zero warnings in dev; deterministic failure in production.

Diagnostic in CloudWatch: all errors started at exactly 2:00:03 AM — the trigger time. The concurrency pattern was invisible in development.

Two-part fix: short-term, a dispatcher Lambda that staggers tenant execution starts by 30 seconds each. Long-term, set `max_connection_pool_size = 5` in the Neo4j driver config for each Lambda — the default of 50 assumes a long-running service, not a Lambda that handles one request and exits.

Lesson: think about concurrency not just within a single execution, but across simultaneous executions. Identical cron expressions fire simultaneously by design.

---

### Q12: Tell me about a time you worked in a highly ambiguous environment. How did you create structure?

TrustX started as a vague brief: "automate compliance for SOC2." No spec, no prior codebase, no design documents. Just the founders, me, and a whiteboard.

My first move was to define the data model before writing any application code. What is a "tenant"? What is a "control"? What is a "test result"? What is "evidence"? I spent two days getting the domain entities right — writing them as TypeScript interfaces and Pydantic schemas before touching AWS or React. Once those were stable, the rest of the architecture followed from them. Every CDK stack, every API endpoint, every React component was just an expression of those data relationships.

The second thing I did was time-box uncertainty. For any design question I couldn't answer definitively in an hour — like "should we use logical or physical multi-tenant isolation?" — I wrote a short decision record: options, tradeoffs, decision made, rationale, what would change this decision. This gave me a way to move forward without being blocked and gave the founders visibility into what we were betting on and why.

Ambiguity is manageable. The mistake is treating it as a blocker. My approach: fix the data model first, time-box design questions, write decisions down so you can move.

---

### Q13: Have you ever pushed back on a user's stated requirement? What happened?

At Samay, the founders' initial requirement for the document editor was: "upload a DOCX, edit it in the browser, download it back as DOCX with no formatting loss." Clean requirement in theory; physically impossible with available tooling at Lambda package size limits.

I came back with the data: LibreOffice headless (best quality) = 250MB+ Lambda package, at the architectural limit. python-docx = 15–20% formatting loss on round-trip (tables, list nesting, fonts). I proposed the alternative: native document creation in a rich-text editor with version control, full fidelity. Legacy DOCX files uploaded as view-only references.

The pushback was: "But customers expect DOCX compatibility." My response: "They expect their compliance documentation to be reliable. A view-only legacy document is better than an edited document that silently corrupts the formatting. The documents they're creating going forward — that's where fidelity matters, and that's where we're perfect." They agreed. Three customers later, no one has asked for DOCX round-trip editing. They create documents in-platform.

Pushing back on a stated requirement only works if you bring an alternative and the data. Opinion alone doesn't move the conversation.

---

### Q14: Tell me about the most complex production system you've shipped solo or near-solo.

TrustX. 15+ AWS CDK stacks: VPC, ECS Fargate, Lambda suite (6 evidence collectors), RDS PostgreSQL with per-tenant schema isolation and Row Level Security, Neo4j graph DB with per-tenant physical isolation on EC2, Step Functions pipeline, AppRunner Flask API, S3 + CloudFront frontend, Secrets Manager with rotation. All provisioned as code, all in production.

The AI layer: AWS Bedrock (Llama 3.3 70B) for LLM control evaluation with evidence-gating post-processing, Pydantic structured output schema, LangChain for NL-to-Cypher translation, MCP-based tool calling for daily compliance report assembly via n8n.

Frontend: React TypeScript dashboard — controls list with framework compliance scores, control detail pages with evidence management, live test execution with job polling, Quill.js document editor with version control, Neo4j graph visualization for identity relationship queries.

The full system went from blank repo to 3 paying enterprise customers over about 10 months. The architectural decisions I'm most proud of: evidence-gating (an LLM cannot hallucinate a PASS verdict in a compliance context — INCONCLUSIVE is the honest answer) and physical multi-tenant isolation (a code bug cannot cause cross-tenant data exposure because infrastructure enforces the boundary before application logic runs).

---

## 3. TECHNICAL — SURFACE LEVEL

---

### Q15: How comfortable are you with TypeScript and React?

TypeScript is my primary infrastructure language — I wrote 15+ AWS CDK stacks in TypeScript at Samay. It's where I do my heaviest architectural work because the type system catches class-level design mistakes before runtime. React I've shipped in production for two years: the full TrustX dashboard is React TypeScript — controls list, evidence management, document editor, live job polling, compliance score visualizations.

Where I'm thin: Next.js specifically. The React fundamentals transfer directly, and I've built server-rendered patterns in other contexts. I'd spend a week getting solid on Next.js routing, server components, and the App Router patterns before deploying anything. I learn framework layers fast when the underlying primitives are already solid.

---

### Q16: Have you built anything on Next.js?

Honest answer: my React work at Samay was a traditional SPA (React Router, no SSR). I haven't shipped a Next.js project in production. The React TypeScript fundamentals, state management patterns, and component architecture are all transferable — the framework-specific additions like file-based routing, server components, API routes, and the App Router model I'd ramp on deliberately in the first few weeks. I don't learn frameworks by reading docs in isolation; I learn by building something real within the first week on the job.

---

### Q17: Walk me through an AI/LLM system you've built — architecture, tradeoffs, what broke in prod.

The TrustX evidence evaluation pipeline.

**Architecture:** AWS EventBridge fires a nightly Step Functions state machine. Stage 1: two parallel Lambdas format data from Entra ID and Jira. Stage 2: three parallel Lambdas write to each tenant's Neo4j graph. A separate on-demand path triggers from the React UI via SQS for interactive test runs. The evaluation Lambda calls AWS Bedrock (Llama 3.3 70B) with a structured Pydantic schema output.

**The key design decision — evidence gating:** The LLM can only return PASS, PARTIAL, FAIL, or INCONCLUSIVE. Post-processing runs before any DB write: if the evidence quote is empty or not verbatim in the retrieved context, the verdict flips to INCONCLUSIVE regardless of what the LLM returned. In compliance, a hallucinated PASS is worse than no answer. Auditors trust the system because it admits uncertainty rather than manufacturing confidence.

**What broke in prod:** The concurrency bug described above — parallel Lambda executions exhausting Neo4j connection pools. Also: a psycopg2 architecture mismatch where a Lambda-compiled `.so` file ended up on the AppRunner import path and caused 503s only on the first real DB operation — appeared healthy through health checks. Both were caught via CloudWatch pattern analysis, not application-level error handling — which taught me that distributed system bugs require log correlation, not just exception catching.

---

### Q18: How do you approach debugging a workflow that's failing silently in production?

Three-step discipline I developed at Samay.

First: **establish a timeline.** CloudWatch Logs with timestamps across all services involved. When did failures start exactly? What changed at or before that time? The concurrency bug's exact 2:00:03 AM timestamp was the key signal.

Second: **follow the data path.** Pick one failing request and trace it through every service boundary — input, transformation, output, errors. Don't hypothesize; trace. The psycopg2 bug was found by looking at `sys.path` in a startup log, not by guessing.

Third: **look for correlated signals, not isolated errors.** A single Lambda failing is a bug. All Lambdas for all tenants failing at the same time is an infrastructure or concurrency pattern. The shape of the failure tells you where to look.

Silent failures specifically: I added structured logging with correlation IDs at every service boundary after the concurrency bug. Every Step Functions execution writes a structured log line at each state transition. A silent failure now shows up as a missing log line, not a missing exception.

---

### Q19: How have you handled scaling issues or reliability problems in a system you owned?

The connection pool exhaustion at Samay is the clearest example (Q11 above). Beyond that: the AppRunner cold-start problem.

Initial TrustX implementation loaded all tenant mappings at `create_app()` time — a single RDS query that took 3-4 seconds and blocked AppRunner initialization. AppRunner health checks were timing out and the service was restarting in a loop.

Fix: lazy loading with a `_tenant_mappings_loaded` flag. The first incoming request triggers the RDS load; subsequent requests hit an in-memory cache. App startup went from 3-4 seconds to under 500ms. Health checks cleared immediately.

Principle I apply: don't pay startup costs for runtime operations. AppRunner's health check timeout is designed for a service that's ready quickly, not one that's pre-loading data. Defer expensive initialization to first use.

---

## 4. CASCA-SPECIFIC / DOMAIN KNOWLEDGE

---

### Q20: What do you know about how small business lending actually works today?

The core problem is that lending is a document-intensive, human-judgment-heavy process with almost no real-time data feedback loops.

A small business applies for a loan. The bank's underwriting team collects: business financial statements (2-3 years of tax returns, P&L, balance sheet), personal financial statements, business documentation (articles of incorporation, licenses, existing debt schedules), and industry context. An underwriter manually reviews all of this against the bank's credit policy — itself a document, often 50-100 pages of rules, ratios, and exception procedures.

The bottleneck isn't decision quality — it's the collection, organization, and cross-referencing of documents that arrive in different formats, at different times, from different sources. A loan that should take a week of actual analysis time takes 90 days because documents are trickling in, manually tracked in email threads, being re-requested because the initial submission was incomplete, and waiting in a human review queue.

Where AI earns its keep: document ingestion and structuring (extract the financial ratios automatically), completeness checking (identify what's missing before the underwriter even starts), policy cross-referencing (flag which credit policy rules apply and whether the application clears them), and workflow orchestration (route the right tasks to the right people at the right time instead of relying on email coordination).

---

### Q21: Why do you think the process takes 90 days? What would you automate first?

The 90 days are almost entirely coordination overhead and wait time, not analysis time. The underwriter might spend 8 active hours on a loan that takes 90 calendar days to close.

If I were attacking this, I'd automate document completeness first. Not the credit decision — the checklist. Before an underwriter touches the application, automated extraction determines: which documents were submitted, which required fields are present in each document, and which items are missing. The first call with the applicant is then a targeted list of exactly what's needed, not "we'll review and get back to you." That alone probably cuts 2-3 weeks of back-and-forth from the cycle.

Second: financial spreading. Extracting standardized financial ratios from uploaded tax returns and P&Ls into a structured format the underwriter can immediately work with, rather than manually transcribing numbers from PDFs into a spreadsheet. Not making the credit decision — just doing the data transformation so the human can focus on judgment.

Third, eventually: policy pre-screening. Given the extracted financials, which credit policy rules clearly clear, which clearly fail, and which require human judgment? The underwriter reviews only the exceptions, not the entire policy book.

This is very close to what I built at Samay — evidence collection, structured extraction, LLM scoring against policy rules, human review of INCONCLUSIVE verdicts. The domain is different but the automation pattern is identical.

---

### Q22: How would you approach getting a bank operator to trust an AI-driven workflow?

The same way I approached it with compliance officers at Samay: make the AI's reasoning visible and make its uncertainty explicit.

An operator doesn't trust a black box. They trust a system that shows its work. When the TrustX compliance evaluation returned a result, it didn't just say PASS — it showed the exact quote from the source document it used, the document reference, and a confidence score. The auditor could verify the quote in the original document in 10 seconds. That verifiability is what builds trust.

Equally important: the INCONCLUSIVE verdict. A system that admits "I don't have enough evidence to answer this" is more trustworthy than one that always returns an answer. Banks have seen too many demos where the AI confidently says wrong things. Showing them that your system knows when to escalate to a human — and does it reliably — is more valuable than higher accuracy scores.

Practical approach for Casca: start with a workflow the operator currently does manually, have the AI run it in parallel for 2-3 weeks without acting on the results, then compare AI outputs against what the human did. When the operator can see that the AI would have reached the same conclusion on 85% of cases and escalated the other 15% for exactly the right reasons, they start trusting it. You earn that trust with evidence, not a pitch.

---

### Q23: What's your mental model for when to automate vs. keep a human in the loop?

Three factors: consequence of error, verifiability of the AI output, and frequency of the task.

**Automate fully** when errors are reversible or low-stakes, the AI output is verifiable by the downstream system (not just by a human), and the task is high-frequency/low-variance. Evidence collection at Samay is an example — pulling structured data from GitHub or Jira has low error consequence and the output is verifiable against source data.

**Automate with human confirmation** when errors have meaningful consequences but the AI's reasoning can be shown to the human quickly enough that review doesn't create a bottleneck. LLM control scoring at Samay is an example — the auditor sees the AI's verdict, the evidence quote, and the source reference, and clicks confirm or override. The human is in the loop but the cognitive load is "verify," not "derive."

**Keep fully human** when the AI cannot show its reasoning in a form the human can verify, or the error consequence is severe enough that the risk of a confident wrong answer outweighs the efficiency gain. Credit decisions in banking probably stay in this bucket for a while — not because AI can't get close, but because the regulatory and liability framework requires a human accountable decision-maker.

At Casca, I'd expect most early deployments to be in the middle bucket: AI does the extraction and structuring, human confirms before it moves to the next stage. That's still a massive time reduction even without full automation.

---

## 5. CULTURE / STARTUP FIT

---

### Q24: What kind of environment brings out your best work?

One where I'm close to the problem and have permission to move. At Samay, I was the sole engineer. The founders would describe a customer complaint at 9 AM; by 3 PM I'd have a prototype in staging for them to react to. That speed was possible because there was no translation layer between understanding the problem and writing the code.

I do worse in environments where the cycle is: PM writes a ticket, designer creates a mockup, ticket goes to the engineering queue, engineer builds it without customer context, ships it, and product wonders why users don't engage with it. The distance between problem and solution is where quality dies.

What specifically helps me: direct access to the people using the software, authority to make technical tradeoffs without a three-meeting approval process, and a team that treats "I shipped it and it didn't work, here's what I learned" as progress rather than failure.

---

### Q25: What's the most impactful thing you've shipped, and how do you measure impact?

The automated control testing pipeline at TrustX. Compliance auditors went from spending 4-6 hours manually compiling evidence for a single control evaluation to reviewing an AI-generated assessment in 15 minutes. That's roughly a 20x reduction in the time cost of answering "does this organization satisfy this control?"

I measure impact in terms of what the user no longer has to do. "Reduced manual effort by 45%" is the metric, but the experience is: an auditor who used to dread quarter-end evidence collection now clicks a button. That's the real outcome.

At Epik, the equivalent: SOC analysts who used to spend 8-10 minutes per critical alert doing manual context pivoting now spend 90 seconds reviewing the AI's consolidated triage output and making the call. The metric is 40% MTTR reduction; the experience is that a 2 AM P1 alert doesn't require waking up three people to gather context before anyone can act.

---

### Q26: What do you want to be doing in 2 years?

Owning more of the product surface and having more autonomy in shaping what gets built. The forward deployed model appeals to me because it puts engineers at the intersection of customer reality and product direction — the people who see the workflows firsthand have the most context to make good product decisions.

In two years I'd want to be the person who knows a particular bank's lending workflow better than almost anyone — and to have that knowledge reflected in the platform in a way that helps every future deployment. The "feed what you learn in the field back into the platform" piece in the JD is what I want to be doing at scale.

---

### Q27: Why are you open to new opportunities right now?

Epik is good work, but it's consulting-adjacent — the AI systems I build stay within the client's environment and don't feed into a product that compounds over time. I want to build software that gets better with every deployment, where what I learn on-site with customer 3 makes the experience better for customers 4, 5, and 10. TrustX gave me a taste of that compound building. Casca is the version of that at real scale, in a domain where the problem is genuinely important.

---

## 6. QUICK REFERENCE

### Key Metrics

| Metric | Source | Context |
|--------|--------|---------|
| 40% MTTR reduction | Epik Solutions | LangGraph SOC triage agent |
| 30% analyst workload cut | Epik Solutions | Azure OpenAI alert processing |
| 1,000+ events/day | Epik Solutions | Pipeline throughput |
| 45% manual review reduction | Samay / TrustX | LLM compliance evaluation |
| 15 enterprise tenants | Samay / TrustX | Live production |
| 0 → 3 paying customers | Samay / TrustX | Sole engineer, ~10 months |
| 15+ CDK stacks | Samay / TrustX | AWS infrastructure |

### Stories Mapped to Themes

| Theme | Story to use |
|-------|-------------|
| User observation changed design | SOC pivot tool discovery (Epik); compliance officer PDF cognitive load (Samay) |
| Ship imperfect with clarity | Document editor DOCX — shipped as view-only with explicit docs and a fix path |
| Production incident ownership | psycopg2 architecture mismatch; Neo4j connection pool exhaustion |
| Ambiguity → structure | TrustX from blank repo — data model first, decision records |
| Pushed back on a requirement | DOCX round-trip editing — proposed view-only alternative with data |
| Refactor unlocked velocity | Generic ControlTester — hardcoded CC7.1 → any control as a data operation |
| End-to-end ownership | TrustX entire product — infra, AI, API, UI, CI/CD, tests |
| Domain knowledge (Casca-relevant) | Evidence-gating → document completeness automation analogy |


> [!example]- Alternate source version (html)
> ## Casca — Forward Deployed Engineer: Interview Prep 
>
>   
>
> Role: Forward Deployed Engineer (FDE) — Casca
>  Stack they want: TypeScript, React, Next.js (must-haves) + Postgres/Prisma, Python, AWS
>  Phone screen with: Samantha Harvey Fleeman (LinkedIn Full Service Hiring)
>  Format: Phone screen — behavioral + fit, ~30 min. No deep technical yet.
>
>    
>
> ### TABLE OF CONTENTS 
>
>   
> - Phone Screen — Recruiter Questions 
> - Behavioral / FDE Mindset 
> - Technical — Surface Level 
> - Casca-Specific / Domain Knowledge 
> - Culture / Startup Fit 
> - Quick Reference   
>
> ### 1. PHONE SCREEN — RECRUITER QUESTIONS 
>
>   
>
> #### Q1: Walk me through your background briefly. 
>
>  
>
> I'm a full-stack software engineer with about four years of experience. The last two years have been almost entirely in AI-augmented production systems — LLM pipelines, agentic workflows, and automation tools built for real enterprise users.
>
>  
>
> At Epik Solutions, my current role, I'm embedded with enterprise security teams building AI-driven triage pipelines on top of Azure OpenAI. We process over a thousand security events a day and cut analyst workload by 30%. The key work there was designing and shipping a LangGraph-based agent that automatically pivots across multiple internal security tools — something SOC teams previously had to do manually for every alert.
>
>  
>
> Before that, at Samay Systems, I was the founding engineer on TrustX — a compliance automation SaaS. I was the sole engineer. I built the entire product from zero: 15+ AWS CDK stacks, a React TypeScript dashboard, an LLM evaluation pipeline on AWS Bedrock, a Neo4j identity graph, and an MCP-based AI chatbot. We went from a blank repo to 3 paying B2B enterprise customers. Compliance officers using the platform cut their manual evidence review time by 45%.
>
>  
>
> The thread across both: I've always worked close to the people who use the software. At Epik, that's SOC analysts. At Samay, it was compliance officers. I sit in on their workflows, understand what's actually tedious, and then build automation that targets those exact friction points. That's exactly what forward deployed engineering is — and it's the model I want to double down on at Casca.
>
>   
>
> #### Q2: Where have you had the most direct exposure to customers or end users influencing what you built? 
>
>  
>
> Two clear examples — one at each company.
>
>  
>
> At Epik Solutions (SOC teams): I regularly did shared-screen shadowing sessions with security analysts. I'd watch them handle a live critical alert — and what I saw was that a single alert required them to manually query three different internal tools just to get enough context to make a triage decision: check the asset inventory, query the threat intelligence feed, look up the user's recent access logs. That wasn't a complaint they'd ever written down in a ticket. I only saw it by watching. I took that workflow and directly mapped it to what the LangGraph agent would automate — those three pivoting steps became three agent tool calls. The agent now does in 4 seconds what took an analyst 8-10 minutes of context switching.
>
>  
>
> At Samay Systems (compliance officers): During early tenant onboarding I sat down with compliance managers and watched them work. They'd manually open hundreds of vendor PDFs, hunt for specific clause language — things like data retention policies, encryption standards — and log it all in a spreadsheet. The part that struck me wasn't the volume; it was the cognitive load of holding three different framework requirements in their head at once while reading. That specific observation shaped how I built the LLM evidence evaluation — I designed the output schema to surface a verdict, a verbatim evidence quote, and a source reference in one card, so the auditor only needs to confirm, not re-derive. Direct workflow observation drove direct design decisions.
>
>   
>
> #### Q3: At Samay Systems — what did "owned end-to-end modules" actually look like in practice? Were those tied to live product usage? 
>
>  
>
> Absolutely live product — 15 enterprise tenants in production.
>
>  
>
> "End-to-end" at Samay meant: I took a feature from conversation with the founders all the way to a customer using it in production, with no other engineer involved.
>
>  
>
> A specific example is the automated control testing pipeline. The compliance officer would log in, click "Run Test" on a control — say CC7.1 (System Monitoring) — and within a few minutes the platform had: collected evidence from GitHub, Jira, AWS Config, and AWS Inspector; run an LLM evaluation on AWS Bedrock with a structured Pydantic schema; applied an evidence-gating check (if the quote wasn't verbatim in the retrieved context, the verdict flipped to INCONCLUSIVE instead of hallucinating a PASS); and surfaced the result with a color-coded verdict, evidence quote, and source reference.
>
>  
>
> I owned every layer of that: the Lambda evidence collectors, the Step Functions orchestration, the Bedrock LLM evaluation, the Flask API endpoint, the React UI components, the CDK infrastructure (IAM roles, SQS queues, S3 buckets), and the test suite. Real compliance officers used it. When the founders demoed it to a prospect and the customer asked "can you run this for access controls too?" — I shipped the generic version in two days because I understood every part of the system.
>
>   
>
> #### Q4: How much of your experience has followed the loop — understand workflow → build quickly → iterate? 
>
>  
>
> It's been the primary loop in both roles. The clearest example:
>
>  
>
> At Samay, after I watched compliance officers struggling with the PDF review workflow, I didn't go back and spec out a six-week project. I built a single-control proof of concept in a week: collect evidence from one source (GitHub), run it through a prompt, return a verdict. Showed it to the founders and the first paying customer in the same meeting. Their feedback that session: "It works, but if the confidence is below 80%, I want it flagged for human review, not auto-passed." I had that change live by the next day. The second iteration feedback: "I need to see exactly which line of which document you used." That forced the evidence-gating architecture — not because I thought of it upfront, but because real users told me what trust actually required.
>
>  
>
> At Epik, the same loop: I ran the LangGraph triage agent past SOC leads every two weeks with new capabilities. They'd run it against real historical alerts and tell me which tools it was calling unnecessarily and which it was missing. That feedback shaped the tool selection logic directly.
>
>  
>
> The loop you're describing — understand, build, iterate with real users — isn't a methodology I read about. It's just how I've always worked.
>
>   
>
> #### Q5: Why Casca specifically? Why forward deployed over a traditional eng role? 
>
>  
>
> Three things make Casca specifically interesting.
>
>  
>
> First, the problem is real and underserved. Small business lending taking 90 days is not a UI problem or a process problem — it's a structural automation deficit. Banks have decade-old systems, and the manual work is genuinely painful. That's the kind of problem where AI actually earns its value rather than being bolted on for appearances.
>
>  
>
> Second, the model is right. Most AI in fintech is advisory — "here's a recommendation, a human will decide." Casca is actually automating the workflow. That requires the kind of deep operator understanding you only get by sitting with them on-site. The forward deployed model is the only way to build software that actually changes how an underwriter works, not just how they get a dashboard update.
>
>  
>
> Third, it matches how I already work best. At Samay and Epik, my best engineering came from being in the room with the people using the software. Traditional sprint-based product roles put distance between me and that feedback. The FDE structure removes that distance by design, and that's where I know I do my best work.
>
>   
>
> #### Q6: Are you open to roughly one week per month travel on-site with bank customers? 
>
>  
>
> Yes — that's not a constraint, that's the draw. The on-site time is where you get the signal that no amount of Slack or Jira can replicate. Watching someone work in their actual environment tells you things they can't articulate in a requirements doc. One week per month on-site is very workable, and for the right deployment I'd be comfortable with extended time if that's what the customer situation calls for.
>
>   
>
> #### Q7: What are your compensation expectations? 
>
>  
>
> I'm targeting a base in the 135K–135K–135K–155K range depending on the overall package and equity structure. I'm flexible on the mix — meaningful equity at a YC-backed company at Casca's stage is part of the comp story, and I take that seriously. Happy to talk specifics once we move forward.
>
>   
>
> #### Q8: Are you open to relocation? 
>
>  
>
> Yes. If the team and role are the right fit, relocation is on the table. I saw that you offer relocation support, which I appreciate — it removes the logistics barrier. Where is the team primarily based?
>
>   
>
> ### 2. BEHAVIORAL / FDE MINDSET 
>
>   
>
> #### Q9: Tell me about a time you sat with a user and discovered something that changed what you built. 
>
>  
>
> At Epik I had a moment that completely reframed what I was building. I was in a screen-share with a senior SOC analyst reviewing how she handled a P1 alert. I expected her to demonstrate the tool usage flow I'd designed — query asset inventory, cross-reference threat intel, triage. Instead, she spent the first four minutes figuring out which system had the asset record she needed, because asset ownership in the organization was split across three tools depending on whether the asset was cloud, on-prem, or a SaaS vendor.
>
>  
>
> I had built the agent assuming one asset inventory source. The discovery changed the architecture: the agent now runs three parallel lookups against all three sources and merges the results. That parallel call pattern added two weeks of engineering time but it's why the agent actually works in production — because I watched the reality, not the theory.
>
>   
>
> #### Q10: Give me an example where you had to build fast and ship something imperfect. How did you handle the tradeoff? 
>
>  
>
> At Samay, document management for compliance artifacts. We needed to support PDF and DOCX uploads — compliance teams have existing documentation. I evaluated four conversion approaches and all of them had problems: python-docx had 15–20% formatting loss on round-trips, LibreOffice headless ballooned the Lambda package to 250MB (at the architectural limit), a dedicated conversion service was 2+ weeks off-roadmap.
>
>  
>
> I shipped with a known limitation: uploaded DOCX/PDF files are stored as binary in S3 with a readonly flag — users can view them in an embedded viewer but not edit them in the platform. Documents created natively in the platform work with full fidelity and full editing. I documented this explicitly: "Uploaded DOCX/PDF are view-only. Create compliance documents in-platform for full editing."
>
>  
>
> Why it was the right call: compliance teams' working documents were already being created natively. Legacy uploads were reference material, not documents they actively edited. Shipping a known, explicit limitation is better than shipping a feature that silently corrupts compliance documents — especially in a context where document integrity has legal weight. I also put the recommended fix in the engineering handoff with an effort estimate so the path forward was concrete, not just punted.
>
>   
>
> #### Q11: Describe a time you owned something end-to-end. What broke and how did you fix it? 
>
>  
>
> TrustX at Samay was end-to-end ownership by necessity — I was the only engineer. The clearest "something broke" story: a production incident the day after deploying the multi-tenant nightly pipeline.
>
>  
>
> Step Functions ran three Neo4j ingestion Lambdas in parallel for each tenant. In dev, with 1-2 tenants triggered manually, it ran fine. In production, with EventBridge firing all tenant executions simultaneously at 2 AM: ServiceUnavailable: Connection pool size of 50 exceeded. Three Lambdas at default 50 connections each, times three concurrent tenant executions, equals 450 simultaneous Neo4j connections against instances sized for 50. Zero warnings in dev; deterministic failure in production.
>
>  
>
> Diagnostic in CloudWatch: all errors started at exactly 2:00:03 AM — the trigger time. The concurrency pattern was invisible in development.
>
>  
>
> Two-part fix: short-term, a dispatcher Lambda that staggers tenant execution starts by 30 seconds each. Long-term, set max_connection_pool_size = 5 in the Neo4j driver config for each Lambda — the default of 50 assumes a long-running service, not a Lambda that handles one request and exits.
>
>  
>
> Lesson: think about concurrency not just within a single execution, but across simultaneous executions. Identical cron expressions fire simultaneously by design.
>
>   
>
> #### Q12: Tell me about a time you worked in a highly ambiguous environment. How did you create structure? 
>
>  
>
> TrustX started as a vague brief: "automate compliance for SOC2." No spec, no prior codebase, no design documents. Just the founders, me, and a whiteboard.
>
>  
>
> My first move was to define the data model before writing any application code. What is a "tenant"? What is a "control"? What is a "test result"? What is "evidence"? I spent two days getting the domain entities right — writing them as TypeScript interfaces and Pydantic schemas before touching AWS or React. Once those were stable, the rest of the architecture followed from them. Every CDK stack, every API endpoint, every React component was just an expression of those data relationships.
>
>  
>
> The second thing I did was time-box uncertainty. For any design question I couldn't answer definitively in an hour — like "should we use logical or physical multi-tenant isolation?" — I wrote a short decision record: options, tradeoffs, decision made, rationale, what would change this decision. This gave me a way to move forward without being blocked and gave the founders visibility into what we were betting on and why.
>
>  
>
> Ambiguity is manageable. The mistake is treating it as a blocker. My approach: fix the data model first, time-box design questions, write decisions down so you can move.
>
>   
>
> #### Q13: Have you ever pushed back on a user's stated requirement? What happened? 
>
>  
>
> At Samay, the founders' initial requirement for the document editor was: "upload a DOCX, edit it in the browser, download it back as DOCX with no formatting loss." Clean requirement in theory; physically impossible with available tooling at Lambda package size limits.
>
>  
>
> I came back with the data: LibreOffice headless (best quality) = 250MB+ Lambda package, at the architectural limit. python-docx = 15–20% formatting loss on round-trip (tables, list nesting, fonts). I proposed the alternative: native document creation in a rich-text editor with version control, full fidelity. Legacy DOCX files uploaded as view-only references.
>
>  
>
> The pushback was: "But customers expect DOCX compatibility." My response: "They expect their compliance documentation to be reliable. A view-only legacy document is better than an edited document that silently corrupts the formatting. The documents they're creating going forward — that's where fidelity matters, and that's where we're perfect." They agreed. Three customers later, no one has asked for DOCX round-trip editing. They create documents in-platform.
>
>  
>
> Pushing back on a stated requirement only works if you bring an alternative and the data. Opinion alone doesn't move the conversation.
>
>   
>
> #### Q14: Tell me about the most complex production system you've shipped solo or near-solo. 
>
>  
>
> TrustX. 15+ AWS CDK stacks: VPC, ECS Fargate, Lambda suite (6 evidence collectors), RDS PostgreSQL with per-tenant schema isolation and Row Level Security, Neo4j graph DB with per-tenant physical isolation on EC2, Step Functions pipeline, AppRunner Flask API, S3 + CloudFront frontend, Secrets Manager with rotation. All provisioned as code, all in production.
>
>  
>
> The AI layer: AWS Bedrock (Llama 3.3 70B) for LLM control evaluation with evidence-gating post-processing, Pydantic structured output schema, LangChain for NL-to-Cypher translation, MCP-based tool calling for daily compliance report assembly via n8n.
>
>  
>
> Frontend: React TypeScript dashboard — controls list with framework compliance scores, control detail pages with evidence management, live test execution with job polling, Quill.js document editor with version control, Neo4j graph visualization for identity relationship queries.
>
>  
>
> The full system went from blank repo to 3 paying enterprise customers over about 10 months. The architectural decisions I'm most proud of: evidence-gating (an LLM cannot hallucinate a PASS verdict in a compliance context — INCONCLUSIVE is the honest answer) and physical multi-tenant isolation (a code bug cannot cause cross-tenant data exposure because infrastructure enforces the boundary before application logic runs).
>
>   
>
> ### 3. TECHNICAL — SURFACE LEVEL 
>
>   
>
> #### Q15: How comfortable are you with TypeScript and React? 
>
>  
>
> TypeScript is my primary infrastructure language — I wrote 15+ AWS CDK stacks in TypeScript at Samay. It's where I do my heaviest architectural work because the type system catches class-level design mistakes before runtime. React I've shipped in production for two years: the full TrustX dashboard is React TypeScript — controls list, evidence management, document editor, live job polling, compliance score visualizations.
>
>  
>
> Where I'm thin: Next.js specifically. The React fundamentals transfer directly, and I've built server-rendered patterns in other contexts. I'd spend a week getting solid on Next.js routing, server components, and the App Router patterns before deploying anything. I learn framework layers fast when the underlying primitives are already solid.
>
>   
>
> #### Q16: Have you built anything on Next.js? 
>
>  
>
> Honest answer: my React work at Samay was a traditional SPA (React Router, no SSR). I haven't shipped a Next.js project in production. The React TypeScript fundamentals, state management patterns, and component architecture are all transferable — the framework-specific additions like file-based routing, server components, API routes, and the App Router model I'd ramp on deliberately in the first few weeks. I don't learn frameworks by reading docs in isolation; I learn by building something real within the first week on the job.
>
>   
>
> #### Q17: Walk me through an AI/LLM system you've built — architecture, tradeoffs, what broke in prod. 
>
>  
>
> The TrustX evidence evaluation pipeline.
>
>  
>
> Architecture: AWS EventBridge fires a nightly Step Functions state machine. Stage 1: two parallel Lambdas format data from Entra ID and Jira. Stage 2: three parallel Lambdas write to each tenant's Neo4j graph. A separate on-demand path triggers from the React UI via SQS for interactive test runs. The evaluation Lambda calls AWS Bedrock (Llama 3.3 70B) with a structured Pydantic schema output.
>
>  
>
> The key design decision — evidence gating: The LLM can only return PASS, PARTIAL, FAIL, or INCONCLUSIVE. Post-processing runs before any DB write: if the evidence quote is empty or not verbatim in the retrieved context, the verdict flips to INCONCLUSIVE regardless of what the LLM returned. In compliance, a hallucinated PASS is worse than no answer. Auditors trust the system because it admits uncertainty rather than manufacturing confidence.
>
>  
>
> What broke in prod: The concurrency bug described above — parallel Lambda executions exhausting Neo4j connection pools. Also: a psycopg2 architecture mismatch where a Lambda-compiled .so file ended up on the AppRunner import path and caused 503s only on the first real DB operation — appeared healthy through health checks. Both were caught via CloudWatch pattern analysis, not application-level error handling — which taught me that distributed system bugs require log correlation, not just exception catching.
>
>   
>
> #### Q18: How do you approach debugging a workflow that's failing silently in production? 
>
>  
>
> Three-step discipline I developed at Samay.
>
>  
>
> First: establish a timeline. CloudWatch Logs with timestamps across all services involved. When did failures start exactly? What changed at or before that time? The concurrency bug's exact 2:00:03 AM timestamp was the key signal.
>
>  
>
> Second: follow the data path. Pick one failing request and trace it through every service boundary — input, transformation, output, errors. Don't hypothesize; trace. The psycopg2 bug was found by looking at sys.path in a startup log, not by guessing.
>
>  
>
> Third: look for correlated signals, not isolated errors. A single Lambda failing is a bug. All Lambdas for all tenants failing at the same time is an infrastructure or concurrency pattern. The shape of the failure tells you where to look.
>
>  
>
> Silent failures specifically: I added structured logging with correlation IDs at every service boundary after the concurrency bug. Every Step Functions execution writes a structured log line at each state transition. A silent failure now shows up as a missing log line, not a missing exception.
>
>   
>
> #### Q19: How have you handled scaling issues or reliability problems in a system you owned? 
>
>  
>
> The connection pool exhaustion at Samay is the clearest example (Q11 above). Beyond that: the AppRunner cold-start problem.
>
>  
>
> Initial TrustX implementation loaded all tenant mappings at create_app() time — a single RDS query that took 3-4 seconds and blocked AppRunner initialization. AppRunner health checks were timing out and the service was restarting in a loop.
>
>  
>
> Fix: lazy loading with a _tenant_mappings_loaded flag. The first incoming request triggers the RDS load; subsequent requests hit an in-memory cache. App startup went from 3-4 seconds to under 500ms. Health checks cleared immediately.
>
>  
>
> Principle I apply: don't pay startup costs for runtime operations. AppRunner's health check timeout is designed for a service that's ready quickly, not one that's pre-loading data. Defer expensive initialization to first use.
>
>   
>
> ### 4. CASCA-SPECIFIC / DOMAIN KNOWLEDGE 
>
>   
>
> #### Q20: What do you know about how small business lending actually works today? 
>
>  
>
> The core problem is that lending is a document-intensive, human-judgment-heavy process with almost no real-time data feedback loops.
>
>  
>
> A small business applies for a loan. The bank's underwriting team collects: business financial statements (2-3 years of tax returns, P&L, balance sheet), personal financial statements, business documentation (articles of incorporation, licenses, existing debt schedules), and industry context. An underwriter manually reviews all of this against the bank's credit policy — itself a document, often 50-100 pages of rules, ratios, and exception procedures.
>
>  
>
> The bottleneck isn't decision quality — it's the collection, organization, and cross-referencing of documents that arrive in different formats, at different times, from different sources. A loan that should take a week of actual analysis time takes 90 days because documents are trickling in, manually tracked in email threads, being re-requested because the initial submission was incomplete, and waiting in a human review queue.
>
>  
>
> Where AI earns its keep: document ingestion and structuring (extract the financial ratios automatically), completeness checking (identify what's missing before the underwriter even starts), policy cross-referencing (flag which credit policy rules apply and whether the application clears them), and workflow orchestration (route the right tasks to the right people at the right time instead of relying on email coordination).
>
>   
>
> #### Q21: Why do you think the process takes 90 days? What would you automate first? 
>
>  
>
> The 90 days are almost entirely coordination overhead and wait time, not analysis time. The underwriter might spend 8 active hours on a loan that takes 90 calendar days to close.
>
>  
>
> If I were attacking this, I'd automate document completeness first. Not the credit decision — the checklist. Before an underwriter touches the application, automated extraction determines: which documents were submitted, which required fields are present in each document, and which items are missing. The first call with the applicant is then a targeted list of exactly what's needed, not "we'll review and get back to you." That alone probably cuts 2-3 weeks of back-and-forth from the cycle.
>
>  
>
> Second: financial spreading. Extracting standardized financial ratios from uploaded tax returns and P&Ls into a structured format the underwriter can immediately work with, rather than manually transcribing numbers from PDFs into a spreadsheet. Not making the credit decision — just doing the data transformation so the human can focus on judgment.
>
>  
>
> Third, eventually: policy pre-screening. Given the extracted financials, which credit policy rules clearly clear, which clearly fail, and which require human judgment? The underwriter reviews only the exceptions, not the entire policy book.
>
>  
>
> This is very close to what I built at Samay — evidence collection, structured extraction, LLM scoring against policy rules, human review of INCONCLUSIVE verdicts. The domain is different but the automation pattern is identical.
>
>   
>
> #### Q22: How would you approach getting a bank operator to trust an AI-driven workflow? 
>
>  
>
> The same way I approached it with compliance officers at Samay: make the AI's reasoning visible and make its uncertainty explicit.
>
>  
>
> An operator doesn't trust a black box. They trust a system that shows its work. When the TrustX compliance evaluation returned a result, it didn't just say PASS — it showed the exact quote from the source document it used, the document reference, and a confidence score. The auditor could verify the quote in the original document in 10 seconds. That verifiability is what builds trust.
>
>  
>
> Equally important: the INCONCLUSIVE verdict. A system that admits "I don't have enough evidence to answer this" is more trustworthy than one that always returns an answer. Banks have seen too many demos where the AI confidently says wrong things. Showing them that your system knows when to escalate to a human — and does it reliably — is more valuable than higher accuracy scores.
>
>  
>
> Practical approach for Casca: start with a workflow the operator currently does manually, have the AI run it in parallel for 2-3 weeks without acting on the results, then compare AI outputs against what the human did. When the operator can see that the AI would have reached the same conclusion on 85% of cases and escalated the other 15% for exactly the right reasons, they start trusting it. You earn that trust with evidence, not a pitch.
>
>   
>
> #### Q23: What's your mental model for when to automate vs. keep a human in the loop? 
>
>  
>
> Three factors: consequence of error, verifiability of the AI output, and frequency of the task.
>
>  
>
> Automate fully when errors are reversible or low-stakes, the AI output is verifiable by the downstream system (not just by a human), and the task is high-frequency/low-variance. Evidence collection at Samay is an example — pulling structured data from GitHub or Jira has low error consequence and the output is verifiable against source data.
>
>  
>
> Automate with human confirmation when errors have meaningful consequences but the AI's reasoning can be shown to the human quickly enough that review doesn't create a bottleneck. LLM control scoring at Samay is an example — the auditor sees the AI's verdict, the evidence quote, and the source reference, and clicks confirm or override. The human is in the loop but the cognitive load is "verify," not "derive."
>
>  
>
> Keep fully human when the AI cannot show its reasoning in a form the human can verify, or the error consequence is severe enough that the risk of a confident wrong answer outweighs the efficiency gain. Credit decisions in banking probably stay in this bucket for a while — not because AI can't get close, but because the regulatory and liability framework requires a human accountable decision-maker.
>
>  
>
> At Casca, I'd expect most early deployments to be in the middle bucket: AI does the extraction and structuring, human confirms before it moves to the next stage. That's still a massive time reduction even without full automation.
>
>   
>
> ### 5. CULTURE / STARTUP FIT 
>
>   
>
> #### Q24: What kind of environment brings out your best work? 
>
>  
>
> One where I'm close to the problem and have permission to move. At Samay, I was the sole engineer. The founders would describe a customer complaint at 9 AM; by 3 PM I'd have a prototype in staging for them to react to. That speed was possible because there was no translation layer between understanding the problem and writing the code.
>
>  
>
> I do worse in environments where the cycle is: PM writes a ticket, designer creates a mockup, ticket goes to the engineering queue, engineer builds it without customer context, ships it, and product wonders why users don't engage with it. The distance between problem and solution is where quality dies.
>
>  
>
> What specifically helps me: direct access to the people using the software, authority to make technical tradeoffs without a three-meeting approval process, and a team that treats "I shipped it and it didn't work, here's what I learned" as progress rather than failure.
>
>   
>
> #### Q25: What's the most impactful thing you've shipped, and how do you measure impact? 
>
>  
>
> The automated control testing pipeline at TrustX. Compliance auditors went from spending 4-6 hours manually compiling evidence for a single control evaluation to reviewing an AI-generated assessment in 15 minutes. That's roughly a 20x reduction in the time cost of answering "does this organization satisfy this control?"
>
>  
>
> I measure impact in terms of what the user no longer has to do. "Reduced manual effort by 45%" is the metric, but the experience is: an auditor who used to dread quarter-end evidence collection now clicks a button. That's the real outcome.
>
>  
>
> At Epik, the equivalent: SOC analysts who used to spend 8-10 minutes per critical alert doing manual context pivoting now spend 90 seconds reviewing the AI's consolidated triage output and making the call. The metric is 40% MTTR reduction; the experience is that a 2 AM P1 alert doesn't require waking up three people to gather context before anyone can act.
>
>   
>
> #### Q26: What do you want to be doing in 2 years? 
>
>  
>
> Owning more of the product surface and having more autonomy in shaping what gets built. The forward deployed model appeals to me because it puts engineers at the intersection of customer reality and product direction — the people who see the workflows firsthand have the most context to make good product decisions.
>
>  
>
> In two years I'd want to be the person who knows a particular bank's lending workflow better than almost anyone — and to have that knowledge reflected in the platform in a way that helps every future deployment. The "feed what you learn in the field back into the platform" piece in the JD is what I want to be doing at scale.
>
>   
>
> #### Q27: Why are you open to new opportunities right now? 
>
>  
>
> Epik is good work, but it's consulting-adjacent — the AI systems I build stay within the client's environment and don't feed into a product that compounds over time. I want to build software that gets better with every deployment, where what I learn on-site with customer 3 makes the experience better for customers 4, 5, and 10. TrustX gave me a taste of that compound building. Casca is the version of that at real scale, in a domain where the problem is genuinely important.
>
>   
>
> ### 6. QUICK REFERENCE 
>
>  
>
> #### Key Metrics 
>
>    
>
>   | Metric  | Source  | Context 
>
>    
>
>   | 40% MTTR reduction  | Epik Solutions  | LangGraph SOC triage agent 
>
>  
>
>   | 30% analyst workload cut  | Epik Solutions  | Azure OpenAI alert processing 
>
>  
>
>   | 1,000+ events/day  | Epik Solutions  | Pipeline throughput 
>
>  
>
>   | 45% manual review reduction  | Samay / TrustX  | LLM compliance evaluation 
>
>  
>
>   | 15 enterprise tenants  | Samay / TrustX  | Live production 
>
>  
>
>   | 0 → 3 paying customers  | Samay / TrustX  | Sole engineer, ~10 months 
>
>  
>
>   | 15+ CDK stacks  | Samay / TrustX  | AWS infrastructure 
>
>    
>
> #### Stories Mapped to Themes 
>
>    
>
>   | Theme  | Story to use 
>
>    
>
>   | User observation changed design  | SOC pivot tool discovery (Epik); compliance officer PDF cognitive load (Samay) 
>
>  
>
>   | Ship imperfect with clarity  | Document editor DOCX — shipped as view-only with explicit docs and a fix path 
>
>  
>
>   | Production incident ownership  | psycopg2 architecture mismatch; Neo4j connection pool exhaustion 
>
>  
>
>   | Ambiguity → structure  | TrustX from blank repo — data model first, decision records 
>
>  
>
>   | Pushed back on a requirement  | DOCX round-trip editing — proposed view-only alternative with data 
>
>  
>
>   | Refactor unlocked velocity  | Generic ControlTester — hardcoded CC7.1 → any control as a data operation 
>
>  
>
>   | End-to-end ownership  | TrustX entire product — infra, AI, API, UI, CI/CD, tests 
>
>  
>
>   | Domain knowledge (Casca-relevant)  | Evidence-gating → document completeness automation analogy

## Source provenance

- [Original HTML](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Interview%20Prep%20company%20prep%20docs/Casca/Casca_Interview_Prep.html) · Interview Prep company prep docs/Casca/Casca_Interview_Prep.html
- [Original MD](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Interview%20Prep%20company%20prep%20docs/Casca/Casca_Interview_Prep.md) · Interview Prep company prep docs/Casca/Casca_Interview_Prep.md

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
