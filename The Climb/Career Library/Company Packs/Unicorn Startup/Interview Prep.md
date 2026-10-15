---
kind: "company-prep"
title: "Interview Prep"
collection: "Unicorn Startup"
topic: "Interview Prep"
imported: "2026-10-13"
source_files: ["Unicorn startup reachout brendon corfee/Interview Prep.md"]
tags: ["career/library"]
source_status: "source-claims-not-verified"
---

# Interview Prep

[[The Climb/Career Library/Career Library]]

> [!info] Source context
> Historical preparation or source notes. First-person stories and numeric outcomes remain source claims until confirmed; this import does not verify them.

# 🔋 Interview Prep — Sr. Backend Engineer
## Unicorn Startup (Energy/Climate Tech) | Austin, TX
### Round: Casual Recruiter Screen with Brenden Corfee

> **Company snapshot:** Series C unicorn, ~$1B raised late 2025. Builds a proprietary OS that coordinates thousands of distributed batteries to stabilize power grids and deliver low-cost electricity at scale.
> **Stack:** Go / Python · DevOps/SRE · Security Infrastructure · Ground-up + migration work
> **Logistics:** Onsite 5×/week in downtown Austin (just south of Colorado River)

---

## 📋 Table of Contents
1. [Opening — Tell Me About Yourself](#1-opening)
2. [Why This Role / Why Now](#2-why-this-role--why-now)
3. [Go & Python Background](#3-go--python-background)
4. [DevOps / SRE Experience](#4-devops--sre-experience)
5. [Security Infrastructure](#5-security-infrastructure)
6. [Distributed Systems & Scale](#6-distributed-systems--scale)
7. [Speed vs. Quality — Shipping Culture](#7-speed-vs-quality--shipping-culture)
8. [Ground-Up & Migration Experience](#8-ground-up--migration-experience)
9. [Behavioral / Fit Questions](#9-behavioral--fit-questions)
10. [Logistics & Compensation](#10-logistics--compensation)
11. [Your Questions for Brenden](#11-your-questions-for-brenden)
12. [Key Talking Points Cheat Sheet](#12-key-talking-points-cheat-sheet)

---

## 1. Opening

### Q: "Walk me through your background."

**Framework:** Now → Back → Why here

> Lead with your current role and biggest impact in 1-2 sentences. Walk back through the thread of backend + infrastructure work. Land on *why distributed energy systems is a natural next step.*

**Key beats to hit:**
- Years of backend experience (Go/Python emphasis if applicable)
- Scale/infrastructure work — systems you owned end-to-end
- Rapid delivery in fast-paced environments
- Any exposure to hardware/IoT/edge systems is a bonus talking point
- Close with genuine energy about the mission

**Example close:**
> "What draws me to this specifically is the intersection of large-scale distributed systems and real-world physical infrastructure — coordinating thousands of battery nodes is a genuinely hard engineering problem, and the climate angle makes it meaningful work."

---

### Q: "What are you looking for in your next role?"

> "I want to be somewhere I can own things end-to-end — not just write features but actually shape how systems are built, scaled, and hardened. A place that moves fast but respects craft. This role checks both: greenfield development plus the SRE/security dimension means I'm solving across the full stack of concerns, not just application code."

---

## 2. Why This Role / Why Now

### Q: "Why are you interested in energy/climate tech?"

> "Power grid reliability is one of the most concrete, consequential engineering problems of the next decade. Battery storage is the fulcrum — it's what turns intermittent renewables into a dependable grid. When I read that this company has a proprietary OS coordinating thousands of distributed batteries at scale, that's a distributed systems problem with real physical stakes. That's rare."

### Q: "What do you know about what we're building?"

**Be ready to say:**
- Proprietary OS that orchestrates thousands of distributed battery nodes
- Transforms fragile grid infrastructure into resilient, fault-tolerant systems
- Enables low-cost electricity delivery at scale
- Series C — $1B raised late 2025 — still building, not just maintaining
- Austin HQ, onsite culture suggests tight collaboration and rapid iteration

---

## 3. Go & Python Background

### Q: "How much Go have you written in production?"

**Talking points:**
- Specific services/APIs you built in Go (gRPC, REST, event-driven)
- Concurrency patterns you've used: goroutines, channels, context cancellation
- Go's strengths you appreciate: fast compile, static binaries, simple deployment
- Libraries you've worked with (e.g., `gin`, `echo`, `chi`, `grpc-go`, `pgx`, `cobra`)

### Q: "How do you decide between Go and Python for a given service?"

> "Go for latency-sensitive, high-throughput services where you want predictable performance and easy deployment — single binary, low memory, great concurrency primitives. Python where development velocity matters more than raw throughput, especially for data pipelines, ML inference wrappers, scripting, or internal tooling. In a team doing rapid iteration, having both is powerful — right tool per workload."

### Q: "Tell me about a Go service you built under tight deadlines."

**Structure:** Situation → constraint → decision → outcome
- What the service did, what the performance/scale requirements were
- Key design decisions (async, queue-backed, stateless, etc.)
- How you shipped fast without tech debt piling up
- Lessons learned

---

## 4. DevOps / SRE Experience

### Q: "How hands-on are you on the infrastructure side?"

**Areas to cover:**
- Container orchestration (Kubernetes, ECS, or similar)
- CI/CD pipeline ownership (GitHub Actions, ArgoCD, Buildkite, etc.)
- Observability stack: metrics (Prometheus/Grafana), tracing (Jaeger/OTEL), logging (ELK/Loki)
- On-call experience — how you've handled incidents, runbooks, postmortems
- Infrastructure-as-Code: Terraform, Pulumi, Helm

### Q: "Describe your approach to reliability for a distributed system."

> "I think in layers: design the service to fail gracefully first (circuit breakers, retries with backoff, bulkheads), instrument everything before you need it (SLOs/SLIs over ad-hoc alerting), and make the runbook so clear that someone paged at 2am can resolve it without heroics. Postmortems blameless and actionable — every incident is a system design feedback loop."

### Q: "Have you worked with edge/embedded infrastructure or anything close to hardware?"

- Mention any IoT, edge computing, or telemetry ingestion pipelines if applicable
- Even high-throughput sensor data processing is relevant — battery nodes are essentially IoT endpoints reporting state

---

## 5. Security Infrastructure

### Q: "What's your security background on the infrastructure side?"

**Topics to be ready for:**
- Secret management (Vault, AWS Secrets Manager, SOPS)
- Network security: VPCs, mTLS, zero-trust networking, firewall rules
- Identity & access: RBAC, IAM policies, service mesh auth (Istio, Linkerd)
- Vulnerability scanning: Trivy, Snyk, Dependabot in CI/CD
- Compliance/hardening experience (SOC 2, CIS benchmarks)
- Incident response to security events

### Q: "How do you think about securing a distributed system where nodes are physical hardware in the field?"

> "Physical nodes are a different threat surface — you have to assume any node can be compromised or tampered with. That pushes you toward zero-trust: mutual TLS between every node and the control plane, signed firmware/config payloads, short-lived credentials rotated automatically, and anomaly detection on telemetry streams so a compromised node gets isolated before it poisons the mesh. Defense in depth from the hardware attestation layer up."

---

## 6. Distributed Systems & Scale

### Q: "Walk me through a distributed system you've designed or significantly contributed to."

**Dimensions to address:**
- Scale: requests/sec, data volume, number of nodes/services
- Consistency vs. availability trade-offs you made (CAP theorem in practice)
- How you handled partial failures
- Communication pattern: event-driven, pub/sub, RPC, or hybrid
- How it's observable and how you'd diagnose a silent failure

### Q: "How would you think about coordinating thousands of battery nodes from a software architecture standpoint?"

> "Conceptually this looks like a large-scale IoT control plane. Each battery node is a stateful agent with local autonomy — it needs to function in degraded-connectivity scenarios. The control plane aggregates telemetry, runs optimization algorithms (charge/discharge scheduling), and pushes configuration. I'd think about: event sourcing for state changes so the system has a reliable audit trail, a gossip/heartbeat layer for node health, CQRS-style separation of the command plane from the read/analytics path, and strong idempotency on all command delivery so retries don't cause dangerous double-commands on physical hardware."

---

## 7. Speed vs. Quality — Shipping Culture

### Q: "The JD says you won't spend more than 8 months on a project. How do you stay high-quality under that kind of velocity?"

> "Velocity and quality aren't opposites if you invest in the right defaults: good test coverage for the core paths (not 100% — triage what breaks the user), observability baked in from day one so you know when something goes wrong after shipping, feature flags so you can ship dark and turn on gradually, and strong code review culture that finds design issues before they calcify. The 8-month cycle actually forces good architecture — you're handing off, so you write for the next person."

### Q: "Tell me about a time you had to ship something fast and still made it maintainable."

- Specific project, specific constraint (deadline, team size, scope)
- Decisions you made to cut scope intelligently vs. cut quality
- How the system held up post-launch
- What you'd do differently

---

## 8. Ground-Up & Migration Experience

### Q: "Have you done greenfield development at scale? What's your approach?"

> "Greenfield is exciting but the trap is over-engineering early. My approach: start with the simplest thing that works at the current scale, make strong interface contracts between modules early so you can swap internals later, and be disciplined about documenting why architectural decisions were made — ADRs (Architecture Decision Records) are lightweight but invaluable when the team grows. Get real traffic on it as early as possible; prod data reveals assumptions that design reviews miss."

### Q: "How have you handled large migrations without downtime?"

**Patterns to mention:**
- Strangler fig / parallel-run pattern
- Dual writes during migration window
- Feature flags to control traffic cutover
- Rollback-first mindset: define the rollback plan before writing the migration plan
- Dark launching and shadow traffic

---

## 9. Behavioral / Fit Questions

### Q: "Tell me about a time you disagreed with a technical direction and how you handled it."

**STAR structure:**
- Specific technical disagreement (architectural choice, tech selection, process)
- How you made the case (data, prototypes, written RFC)
- Outcome: whether you won or lost, and what you learned either way
- Show you can commit and execute even when overruled

### Q: "Describe a production incident you led. What happened and how did you run it?"

- Incident type, blast radius, how you were paged
- Immediate triage: isolate, communicate status, stop the bleeding
- Root cause discovery process
- Fix vs. mitigation decision
- Postmortem and what changed structurally afterward

### Q: "What's your ideal team dynamic?"

> "Small, senior, high-trust. I like teams where you can propose something in a Slack thread, get two colleagues to poke holes in it, and ship a PR by end of day. Not no-process, but lightweight process. Ownership is clear, on-call rotation is fair, and people give code review feedback that makes the code better — not just stylistic nitpicks."

### Q: "Why are you considering leaving your current role?"

**Honest, positive framing:**
- Frame around what you're moving *toward* (not fleeing)
- Growth ceiling / desire for more ownership / mission alignment
- The scale/impact of what this company is building vs. current trajectory

---

## 10. Logistics & Compensation

### Q: "Are you open to onsite 5 days a week in Austin?"

- Be clear and direct about your situation
- If you're in Austin or willing to relocate: confirm enthusiasm
- If relocation needed: "I'm open to relocation for the right opportunity — this one qualifies"

### Q: "What are your comp expectations?"

**Strategy for a recruiter screen:**
> "I'd rather let the leveling conversation inform that — I understand the comp is tied to where I level with the team, which I appreciate. Based on my experience and the scope of this role, I'm targeting [X range] in base, but I'm genuinely interested in the equity story at Series C too. What does the band look like at the senior level?"

- Get them to share ranges before anchoring too hard
- Ask about equity: strike price, vesting schedule, last 409A, preferred vs. common shares outstanding
- Ask about refresh grants

### Equity due diligence questions to ask:
- What's the fully diluted share count?
- What was the valuation at last 409A?
- What's the current preferred share price (post Series C)?
- What's the standard vesting schedule and cliff?
- Do you do refresh grants?

---

## 11. Your Questions for Brenden

> These signal preparation, genuine interest, and seniority. Pick 4-6.

### About the Role
1. "What does the first 90 days look like — is there a ramp period or do engineers ship quickly from day one?"
2. "You mentioned both migration and ground-up work — what's the current ratio, and how does that shift over time?"
3. "What does the on-call culture look like? How many engineers share the rotation, and what's the typical incident frequency?"
4. "The JD mentions security infrastructure as a concentration area — is there a dedicated security team, or is this embedded within the backend engineering org?"

### About the Team & Company
5. "How big is the backend engineering team today, and what's the growth plan over the next 12 months?"
6. "What does the tech stack look like in terms of infrastructure — are you primarily cloud-hosted, on-prem, or hybrid given the physical hardware component?"
7. "Who would I be working most closely with day-to-day, and what does seniority distribution on the team look like?"
8. "How does the company think about technical autonomy for senior engineers — is there an RFC/proposal process, or is it more informal?"

### About the Business
9. "The $1B Series C is a big milestone — what does the deployment roadmap look like for the battery network over the next 2 years?"
10. "What are the biggest engineering challenges standing between where you are today and the next inflection point in scale?"

---

## 12. Key Talking Points Cheat Sheet

| Theme | Your Hook |
|---|---|
| **Go experience** | Production services, concurrency, binary deployments |
| **Python** | Data pipelines, scripting, ML-adjacent tooling |
| **SRE** | On-call, SLOs, observability, postmortems |
| **Security** | Zero-trust, secrets management, network hardening |
| **Distributed systems** | Fault tolerance, CAP trade-offs, event-driven |
| **Shipping velocity** | Feature flags, good defaults, scope triage |
| **Greenfield** | ADRs, interface contracts, get real traffic early |
| **Mission** | Grid resilience is a hard, consequential systems problem |
| **Culture fit** | Small, senior, high-trust, clear ownership |

---

## ⚡ Pre-Call Checklist

- [ ] Research the company name (ask Brenden if he'll share it pre-call — it's listed as unnamed unicorn)
- [ ] Look up recent news on Austin-based energy storage unicorns (likely [Nuvve / Geli / Form Energy / similar] — $1B Series C late 2025 is identifiable)
- [ ] Have your resume open in front of you
- [ ] Have a number in mind for base comp + equity expectations
- [ ] Know your current notice period / availability start date
- [ ] Confirm Austin logistics (are you there now, or is relocation involved?)
- [ ] Keep answers to 90 seconds max — this is a conversation, not a presentation

---

*Generated June 2, 2026 · Brenden Corfee recruiter screen prep*


## Source provenance

- [Original MD](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Unicorn%20startup%20reachout%20brendon%20corfee/Interview%20Prep.md) · Unicorn startup reachout brendon corfee/Interview Prep.md

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
