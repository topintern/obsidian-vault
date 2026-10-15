---
kind: "company-prep"
title: "EM1 Cheatsheet"
collection: "EM1"
topic: "Interview Prep"
imported: "2026-10-13"
source_files: ["Interview Prep company prep docs/EM1/EM1_Cheatsheet.md"]
tags: ["career/library"]
source_status: "source-claims-not-verified"
---

# EM1 Cheatsheet

[[The Climb/Career Library/Career Library]]

> [!info] Source context
> Historical preparation or source notes. First-person stories and numeric outcomes remain source claims until confirmed; this import does not verify them.

# EM1 — Day-of Cheat Sheet
### Gunnar Holwerda, CTO | Wednesday June 10, 2026 | 60–90 min
> **One read Wednesday morning. Then close it.**

---

## KEY NUMBERS
| Signal | Number |
|---|---|
| Agencies on platform | 60+ (state, county, city) |
| Guidelines per HMP evaluation | 111 |
| Plan size | 500–2,000 pages |
| LLM calls at current scale | ~6,600/month (111 × 60) |
| At 10x growth | ~66,000/month |
| Team size | 4 engineers incl. Gunnar |
| Modules | E01 Evaluate, E02 Improve, E03 Operationalize/Chat |
| Near-term focus | Vanta-style intake — replace email + manual trigger |

---

## COMPANY CONTEXT (30-second version)
- **E01 Evaluate:** Automated FEMA crosswalk — 111 guidelines matched against a plan. Smart References = which page answers which guideline.
- **E02 Improve:** Plan Library + Peer Docs + **Deconflict** (cross-plan contradiction detection)
- **E03 Operationalize:** Custom knowledge base + real-time chat Q&A
- **What you're building:** The self-serve intake form + async evaluation pipeline that replaces the current email/manual flow. Plus extending the RAG and contributing to agent skills.
- **Stack:** Next.js, TypeScript, PostgreSQL, AWS, Terraform

---

## ALIGNMENT TABLE (one-liner per question)
| If he says... | You say... |
|---|---|
| "Vanta-style module" | "I built this at Samay — SOC2 controls → FEMA guidelines is a configuration change, architecture is identical" |
| "Sentence-level citations / Smart References" | "Evidence-gating pattern — Pydantic schema forces verbatim quote, no quote = INCONCLUSIVE, no hallucination path to PASS" |
| "Human in the loop" | "Automate the tedious reading, preserve the judgment — LLM does 2000-page scan, human signs off on verdict" |
| "Graph-RAG" | "Right for multi-hop cross-doc traversal; overkill for single-plan crosswalk — used Neo4j at Samay exactly where it earns its complexity" |
| "Full-stack ownership" | "CDK infrastructure + Lambda + API + React UI — all of it, no handoffs. Test Control button story." |
| "Small team / 4 engineers" | "Samay was effectively solo founding engineer — that context is where I work best" |
| "Next.js" | "React + TypeScript is the base — App Router / RSC model is the 2-3 day ramp, productive in a week" |
| "Terraform" | "Deep CDK (same discipline), Terraform working proficiency — contributing to existing codebase within a sprint" |
| "Mentor juniors" | "OSU GTA, Zemoso test coverage story — reviews that teach the why, pairing over async comments" |

---

## OPENING LINE (first 90 seconds)
> "I'm Neel — six years full-stack, last two building AI systems. The most directly relevant thing I've built is TrustX at Samay — compliance automation where the core was: collect evidence across sources, assemble grounded context, run LLM evaluation with citation enforcement. When you describe the Evaluate module — automated FEMA crosswalk, Smart References — that's the same architecture in a different domain. Looking forward to getting into the specifics."

## CLOSING LINE
> "This has been exactly the kind of conversation I was hoping for. Grounded AI with citation accountability, in a domain where wrong answers have real stakes — that's the problem I care about. I'd love to keep moving forward."

---

## QUESTIONS TO ASK (pick 3)
1. **[Technical — lead with this]** "The crosswalk — are you chunking plans structurally by section, or by token count? I'd expect section-aware parsing to be the hard part for citation precision."
2. **[Technical / future]** "Deconflict — doing cross-document contradiction detection today, or is that upcoming? Curious if you're modeling it as a graph problem."
3. **[Team]** "The 2 early-career engineers — how do you think about the mentoring dynamic on a 4-person team? Want to understand what being genuinely useful to them looks like from day one."
4. **[Engineering culture]** "Coming from OpenSesame and Olo — what habits are you deliberately bringing to EM1, and what are you leaving behind?"
5. **[Ownership]** "If I'm fully up to speed in 60 days — what's something you'd want me to own that you don't have bandwidth for right now?"

---

## STUDY SCHEDULE
| Day | Read | Goal |
|---|---|---|
| **Monday** | EM1_System_Design.md | Know E2E flow + human-in-the-loop cold |
| **Tuesday AM** | EM1_System_Design.md (deep dives) | Ready for technical architecture questions |
| **Tuesday PM** | EM1_Experience_Dives.md (behavioral out loud) | Stories internalized, not read |
| **Wednesday AM** | This file only | Cheat sheet. One read. Trust the prep. |

---

## DOMAIN TERMS (use naturally)
**EOP** = Emergency Operations Plan | **HMP** = Hazard Mitigation Plan (FEMA-required) | **COOP** = Continuity of Operations | **IAP** = Incident Action Plan | **AAR** = After Action Report | **EOC** = Emergency Operations Center

---

## MINDSET
- Use numbers when you can — signal you did the homework
- End every technical answer with a bridge to something you built: "I built this pattern at Samay — here's what it looked like"
- On Next.js/Terraform gaps: say it once, cleanly, move on. Don't over-explain.
- When you don't know: "Haven't used X directly but here's how I'd think through it..." not silence, not bluff
- He respects precision, dislikes vagueness. Specific > comprehensive.



## Source provenance

- [Original MD](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Interview%20Prep%20company%20prep%20docs/EM1/EM1_Cheatsheet.md) · Interview Prep company prep docs/EM1/EM1_Cheatsheet.md

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
