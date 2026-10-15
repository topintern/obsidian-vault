---
kind: "company-prep"
title: "Wei Tang Round Prep"
collection: "InMarket"
topic: "Interview Prep"
imported: "2026-10-13"
source_files: ["AI Builder/InMarket JD and Resume, interview round info/Wei_Tang_Round_Prep.html","AI Builder/InMarket JD and Resume, interview round info/Wei_Tang_Round_Prep.md","Interview Prep company prep docs/AI Builder/InMarket JD and Resume, interview round info/Wei_Tang_Round_Prep.html","Interview Prep company prep docs/AI Builder/InMarket JD and Resume, interview round info/Wei_Tang_Round_Prep.md"]
tags: ["career/library"]
source_status: "source-claims-not-verified"
---

# Wei Tang Round Prep

[[The Climb/Career Library/Career Library]]

> [!info] Source context
> Historical preparation or source notes. First-person stories and numeric outcomes remain source claims until confirmed; this import does not verify them.

# InMarket — Wei Tang Round Prep

> **Format:** Culture + collaboration + product thinking, ~45–60 min.
> **Interviewer:** Wei Tang — Principal Product Designer, 5 years at InMarket. Owns GeoLink end-to-end. Built InMarKit design system. Came from Perkins&Will where she built internal tools that saved 5,000+ labor hours/year. She measures everything with SUS scores, retention, and revenue impact.
> **Your posture:** Collaborative builder who is genuinely curious about the user, the product, and the people doing the work — not just the technology. Engineer who thinks like a product person.

---

## InMarket Context You Need to Know

**The company:** Real-time marketing and measurement platform, 15+ years old, 300+ people, 35+ industry awards. Core thesis: right person, right message, right moment. Revenue model is B2B SaaS + managed campaigns for major brands (Danone, Bayer, Dunkin', Albertsons, Coors Light).

**The product stack (external-facing):**
- **GeoLink** — self-serve ad platform. Location-based audience targeting, GeoFences, GeoRetargeting, CTV/mobile/desktop. 200M+ mobile devices. This is where Wei has spent 5 years. Campaign setup used to take 49 minutes; she shipped Async Avails and got it to 16 minutes. That single feature retained $6.7M in client spend.
- **LCI® (Lift, Conversion & Incrementality)** — AI-powered measurement and optimization engine. Closed-loop attribution against $2.5T+ in retail sales data, 127B+ receipt transactions. Agencies use LCI to prove ROI to their clients. Dunkin', WPP, Reddit all on it.
- **Activation** — Preceptivity (AI-driven predictive audiences), Moments (InStore/InHome/InPath/InHand push experiences, 6x industry engagement benchmark).
- **InSights** — analytics layer for agencies and brands.
- **Unified Platform** — bringing GeoLink, Ventura, LCI, and InSights together.

**The internal pain (what Roj told you):** Heavy data pipelines, many manual handoffs, headless browsers, Playwright — these are the internal ops problems the AI Builder role is solving. Think: campaign operations teams doing things by hand that should be automated, reporting workflows that require scraping or headloading data between systems, maybe internal tooling that bridges GeoLink/LCI data to agency reporting.

**Wei's specific work that matters for your conversation:**
- GeoLink Async Avails: 49 min → 16 min campaign setup, $6.7M retained
- GeoLink Reports: SUS 72.5 → 91.25 (above-average → excellent)
- InMarKit design system: 30% faster prototyping, 40% faster front-end implementation
- LCI Sales Attribution by Dimension: 83% revenue increase YOY
- She thinks in SUS scores, time-on-task, revenue retained, and YOY comparisons — speak her language

---

## Table of Contents
1. [Tell Me About Yourself](#1-tell-me-about-yourself)
2. [Collaboration Across Working Styles](#2-collaboration-across-working-styles)
3. [Navigating Disagreement & Changing Direction](#3-navigating-disagreement--changing-direction)
4. [Showing Up When Things Get Hard](#4-showing-up-when-things-get-hard)
5. [Genuine Curiosity About Work and People](#5-genuine-curiosity-about-work-and-people)
6. [Building for Real Users](#6-building-for-real-users)
7. [InMarket-Specific & Product Thinking](#7-inmarket-specific--product-thinking)
8. [Questions to Ask Wei](#8-questions-to-ask-wei)

---

## 1. Tell Me About Yourself

---

### Q: Walk me through who you are and why you're here.

I'm a software engineer who's spent the last couple of years building AI-powered internal tools — pipelines, automation systems, compliance platforms. The consistent thread is: I don't just build what the spec says. I try to understand who's actually using the thing and what's making their day harder than it needs to be.

The most satisfying work I've done is when something I built made a manual, tedious process disappear for people who weren't engineers — security analysts who stopped spending their mornings triaging noise, compliance auditors who stopped spending days pulling evidence by hand.

I'm here because InMarket has a real internal ops problem that maps to exactly what I've been building. You've got heavy data pipelines, manual handoffs between teams, operational workflows that were designed before AI was practical. That's the gap I want to work in.

I also looked at what Wei has shipped here — taking GeoLink campaign setup from 49 minutes to 16 with Async Avails, getting the GeoLink Reports SUS score from 72 to 91 — and that kind of measurable, user-centered product thinking is the environment I want to be building in. When the people around you are measuring impact with SUS scores and revenue retained, it raises the bar for everybody.

---

### Q: You're an engineer interviewing with a product designer. Why should that conversation be interesting?

Because I think like a product person when I build. The first thing I ask about any feature isn't "what's the schema?" — it's "who is the person doing this today without the tool, and what does their day look like?"

At Epik, I sat with security analysts for two hours before writing a line of code — just watching their morning triage routine. At Samay, I spent time with compliance auditors doing a live walkthrough of a real audit before building any data model. In both cases, the thing I would have built from a spec alone would have been technically correct and practically useless.

I think that's the overlap between design and engineering at its best: you're both trying to understand the user deeply enough to build the right thing. The implementation language is different but the process has to be the same.

---

## 2. Collaboration Across Working Styles

---

### Q: Tell me about a time you had to collaborate closely with someone who worked very differently from you.

At Samay, I worked closely with a compliance domain expert who thought in legal frameworks and audit trails — not systems or data models. Her mental model of "evidence" was nothing like mine. She described what she needed in terms of audit procedures and control narratives. I was trying to map that to APIs, schemas, and Lambda functions.

Early on I'd come out of meetings with notes that I thought were clear and build something based on them. She'd look at it and say "that's not what I meant." Not because she was wrong — because I had translated her language into my language and lost something in the process.

The fix was: I stopped translating. I asked her to walk me through a real audit, step by step, as if I was a new auditor learning the job. I took notes in her language, not mine. "We look at whether config changes were tracked and reviewed" — I wrote that down exactly as she said it, then I did the translation afterward. The 6-source data model that the automated testing system ran on came entirely from that session. She didn't know what CloudTrail was. She knew she needed to see that config changes were tracked and reviewed. Those are the same thing, but only once you've done the translation carefully.

The working-style difference that almost caused the most friction wasn't expertise — it was pace. I wanted to iterate fast and show her something. She needed more certainty before she'd give feedback. The compromise was: I showed her something I explicitly labeled as 30% done with specific questions attached — "I'm not asking if this is right, I'm asking if the data I'm collecting matches what you actually look at." That unlocked the feedback loop.

---

### Q: How do you work with designers? What does that relationship look like when it's going well vs. when it's not?

When it goes well, the designer and I are solving the same problem from different angles and the answers converge. The designer is asking "what does this person need to understand at a glance?" and I'm asking "what does the system need to do to produce that?" We're checking each other's assumptions constantly.

The clearest example I have is from Epik — the C-suite dashboards. The first version I built was data-rich and technically complete. It aggregated telemetry from 15+ systems, every metric was accurate. The executives used it for a week and stopped. When I asked why: "we don't know what to do with this."

I rebuilt it around one question: what should I do right now? That's a design question, not an engineering question. Traffic-light status for each system, a "needs attention" list with plain-English explanations, week-over-week trend line. Everything else was a click-through. That version got used every day.

What I wish I had in that situation was a designer early — someone asking "what decision is this person making when they look at this screen?" before I built anything. The rebuild cost three or four days. A half-hour conversation with someone like Wei at the start would have saved it.

The flip side of that: at Zemoso I worked on a proprietary custom UI component library and had to change an expanded table component used across the whole platform. The ask was: add padding and a blue row highlight on expand. Simple on the surface. But I had to trace every place the existing component was used, understand why it was built the way it was, create a new version that didn't break existing consumers while adding the new behavior, cut a library release, then update all the call sites. Multiple review rounds with the onshore team to get the spacing exactly right. Took significantly longer than the surface ask suggested — a component library is load-bearing, you can't change it casually, and you don't really understand that until you've had to trace all its consumers.

When it doesn't go well: usually it's because design and engineering are running in parallel without talking, and the gap gets discovered at implementation. You end up in a negotiation over what gets cut. That's a process failure, not a people failure — it means the handoff happened too late.

---

### Q: What's your hands-on experience with design tools, Figma, and the design-to-engineering process?

I'm on the engineering side of that boundary, not the design side — so let me be honest about what I've actually done.

The most direct experience I have with Figma as a working artifact is from Zemoso/Strateos. The expanded table component task was explicitly framed as "it's not matching the Figma" — the Figma spec was the source of truth, and my job was to understand why the implementation had diverged and fix it. That meant opening the Figma file, reading the annotations, understanding the intended spacing and color behavior, and then tracing whether the component could even produce that output given how it was written. The component couldn't — it was structurally incompatible with some of the required behavior — which meant creating a new version of the component in the custom UI library, not just adjusting values.

The iterative review process that followed was where the real design-engineering dialogue happened. The onshore team had strong opinions about exact pixel values because those values affected how the component sat in different layouts across the platform. Multiple rounds of PR review, each with specific annotated feedback. I'd adjust, they'd review, we'd get on a call when comments weren't capturing the nuance. That back-and-forth is what "implementation matches design intent" actually looks like in practice — it's not a one-pass thing.

Beyond that: at Strateos, one of the four teams was a dedicated UX team. I was in the Chem team. We consumed their output — component specs, interaction patterns, flow documentation. When our work touched their components, we'd loop them in. Watching how they approached a feature request — the questions they asked about use cases before committing to a design direction — was genuinely useful to see up close.

What I understand about good handoff vs. bad handoff: when a Figma spec includes interaction notes, edge case states (empty, loading, error), and annotated rationale for decisions, implementation is fast and confident. When it's just the happy path, you end up making judgment calls at implementation time that should have been design decisions. Those judgment calls are where drift happens.

I also did a serious stretch of HTML/CSS/Bootstrap work during my time at Zemoso's training program — built responsive layouts, worked with grid systems, learned how visual structure maps to code. Enough to read a design spec and understand the structural intent, not just copy coordinates.

---

### Q: You've worked across small startups and larger orgs. How do you adapt?

At Zemoso (Strateos), I was one developer in a Chem team on a four-team project — lab devices, UX, Chem, and a fourth team I didn't overlap with much. The platform was enormous: a scientific experiment system with compounds, batches, runs, inventories, containers, multiple scientist roles with different permissions, dozens of microservices. It took two full days just to get the local environment running — Docker bringing up all services, health checks, the whole chain. The first time I had to write test cases for someone else's code, I needed to fully understand what the existing code was doing, what tests already covered it, and how to add coverage without breaking anything. That's a completely different posture than building from scratch. I had to slow down and be more deliberate than felt natural.

At Samay as founding engineer, the opposite — building from nothing with a 5-person team, fast feedback loops. Ship a Lambda in the morning, show a client in the afternoon, get new requirements the same day.

At Epik, embedded in an established enterprise security team, there were years of existing routing decisions, stakeholder relationships, and tool choices that had reasons behind them even when undocumented. Understanding those reasons before proposing changes was the right move.

The question I answer fast when I start somewhere new: how are decisions actually made here — not on paper, in practice — and who is the person opening this tool every morning?

---

## 3. Navigating Disagreement & Changing Direction

---

### Q: Tell me about a time you pushed back on something and it changed the outcome.

At Epik, a stakeholder wanted the incident triage pipeline to send Slack alerts with full event details — every field, all the context, inline in the message. The intent was good: make the alert as information-dense as possible so analysts had everything they needed without opening a ticket.

The problem I saw: several of those fields contained PII — employee account names, internal system identifiers, things that shouldn't be sitting in Slack channels that ops people share screens from. It was a security problem.

I didn't say "that's not possible" or "that's a security risk, we can't do it." I said: "Here's what that would take, and here's what we'd have to give up. We can send the fields that are safe. The full detail view would need to be a link to the internal ticket system, which is already access-controlled. That also makes the alert itself shorter and more actionable." I showed them what both versions would look like.

They actually preferred the second version once they saw it. Shorter alert, clear link, everything sensitive is one click away behind auth. Better UX and better security.

---

### Q: Tell me about a time requirements changed significantly mid-build. How did you handle it?

At Samay, I was mid-build on the automated compliance testing system — had CC7.1 (system monitoring) working, was generalizing the Lambda to accept any control — when the team lead came back from a client call. The client had changed their priorities. Different compliance controls, different evidence profile needed.

My first reaction was frustration, honestly. I had built something that was working and it felt like we were moving the target.

But when I looked at the actual impact, it was smaller than I expected. Because I had built the data collectors as separate modules — `aws_collector.py`, `integration_collector.py` — and the LLM analysis was a function that took a control ID and a data payload, the core architecture was already generic. Swapping which control was being tested was mostly a prompt change and tweaking which collectors were called. It wasn't a rewrite.

I gave the team lead a realistic assessment: "First of the new controls by end of week, second the week after." Honest, with reasoning. Not defensive, not falsely optimistic.

---

### Q: Tell me about a time you changed direction because someone else was right.

When I built the first version of the security dashboards at Epik, I genuinely believed dense information was better — analysts were smart, they'd know what to do with everything. The executives said they didn't know what to do with the dashboard. My first instinct was to explain it better.

Then I actually watched one of them use it. They scrolled to the bottom, found one number that looked bad, asked someone what it meant, and closed the tab. They hadn't engaged with 80% of what I built.

That's when I understood: the feedback wasn't "explain it better." It was "I don't want all of this." The problem was the paradigm, not the execution. I threw out the UI architecture of the first version — kept the data layer, changed everything about what to surface by default.

In hindsight, I was doing design work without a designer in the room. I had talked to executives about what they wanted, but talking to someone about a tool is different from watching them use it. What I thought I understood from the conversations wasn't what they actually needed in the moment of use. That's the kind of gap a design process catches — I just didn't have one in that situation.

---

### Q: Tell me about a time you disagreed with a peer — not a requirements disagreement, a genuine technical disagreement — and you both had a real case.

At Zemoso, I was reworking the expanded table component in the shared UI library. Multiple PR review rounds with the onshore tech lead. In one specific round, they asked for a reduced left-padding value — their reasoning was consistency with an existing component in the library. I looked at the Figma, traced all the places the table was used, and flagged a collision issue: in narrow-column configurations, their requested value would sit the text too close to the expand chevron. I pushed back on the review comment with a specific counter-proposal: "In narrow-column contexts the Figma shows a larger gap — I'd suggest X instead of Y."

Their response was immediate and not what I expected. They had a layout I hadn't seen — an upcoming feature that used a wider table configuration where their value was actually correct for that context. We got on a call because the comment thread wasn't capturing the nuance. With both layouts on screen at once, the answer was clear: neither of us was wrong, we needed two configurations instead of one value trying to satisfy both. The PR ended up slightly more complex than the original scope, but it was right.

What I noticed: the reviewer who pushes back hardest on something you're confident about is often seeing a context you haven't seen yet. That's the right frame before getting defensive.

---

### Q: Tell me about a time leadership made a call you disagreed with and you had to work within it.

At Monarch Tractor, we shortlisted three vendors for the HRMS automation: Workato, Boomi, and AWS native. I had calls with all three. Coming out of those calls, I thought Workato was the right choice — it was purpose-built for multi-system HRMS integrations, the connectors were mature, and the error handling they demoed was stronger than anything I'd build from scratch in a reasonable timeframe. Leadership picked AWS. Budget.

My honest read at the time: we'd spend more engineering hours building what Workato had already solved. And parts of that were true — the Lambda layer dependency issues, having to containerize just to run PowerShell, the custom error handling I had to write myself. But there were things I hadn't fully weighed when I disagreed: the team already had AWS infrastructure and skills, and the audit trail through CloudWatch and EventBridge was actually better for an HR system's compliance requirements than what Workato's logs would have given us. Once I was deep in the build, I understood better why someone with broader context had made that call.

I didn't formally push back — it was a leadership call made on constraints I didn't have full visibility into. What I did was document the Lambda/container tradeoff explicitly, so whoever touched the system next would understand why it was structured the way it was, not just that it was.

---

### Q: Tell me about a time you pushed back on a direction and lost the argument — and then realized you were wrong.

At Samay, when the team lead came back from the client call with the controls pivot, I pushed back. I had specific evidence: the new control set had a meaningfully different evidence profile, and one of them required a source integration we hadn't built yet. My position was clear: if we build automated testing for incomplete controls, we ship something that looks worse than nothing — the client sees a system that doesn't work rather than a system that works on the old scope. I said this directly to the team lead.

He heard me and overruled me. "Show the client progress on what they actually care about now. Flag the integration gap separately."

He was right. What I had missed: the client's confidence in the platform was the more urgent problem. They had changed their priorities — showing them forward motion on the controls they currently cared about mattered more than having a complete system for controls they'd deprioritized. The integration gap was real and got properly tracked. The client didn't care about the completeness of the old control set. I cared about it because I built it.

Being overruled and then being wrong is a different experience than just being overruled. It's more useful. I understood after that why "show progress on what the client needs right now" is sometimes the right call even when the technical situation isn't clean.

---

### Q: Tell me about a time you were caught between two teams who had a legitimate disagreement about ownership.

At Zemoso, the expanded table component I was reworking was in the shared UI library — documented as "stable, do not change behavior without UX review." The Chem team lead gave me the task without routing through the UX team, reasoning that it was a visual alignment fix, not a behavior change.

The UX team found out mid-review. One of their designers was on the PR and flagged it: this component appears in UX-specified flows across multiple screens — any padding change cascades. They wanted the PR held for a design review. The Chem lead's position: visual spec alignment isn't behavior change, this doesn't require a gate. The UX lead's position: in a shared component library, visual changes are behavior changes.

I was the developer who wrote the change, caught between two team leads in a thread that was going sideways fast.

What I did: I wrote a summary of exactly what the change did — specific, with before/after screenshots, a list of every component in the library that referenced the table, and which layouts were affected. I shared it in the thread without taking a side. I moved the conversation from "who has authority here" to "here's the actual scope, let's decide from this." The UX team signed off with one small adjustment. The review that looked like it was going to take another week happened in a day.

The useful thing I took from that: when two people are disagreeing about ownership, it's often because they don't have the same information about the actual scope. Getting that information on the table — neutral, specific, without editorializing — is almost always the fastest way through.

---

## 4. Showing Up When Things Get Hard

---

### Q: Tell me about a time something you built broke in production. What did you do?

At Samay, we had a distributed identity event ingestion pipeline that was silently dropping events under load. No errors, no alerts — the pipeline looked healthy from the outside, but the event counts were off. An auditor noticed that a user's access history had gaps. That's how we found it — not from a monitoring alert, from a human noticing something wrong in a manual review. The fact that it surfaced that way bothered me more than the bug itself.

I ran it down by adding counters at every stage of the pipeline — events received, events processed, events written — and comparing the deltas. The failure was a Spark job hitting memory limits and silently discarding the overflow batch instead of raising an error. It had been configured with error handling that was too defensive.

Fix: reduce batch size, change the error handling so memory failures raised visibly, and add an end-of-pipeline count reconciliation job that paged if the numbers didn't match.

But the more important fix was: I added the reconciliation job as a pattern across other pipelines too. Not just the one that broke. If one pipeline could fail silently, others could too.

---

### Q: Tell me about a time the project was genuinely hard and you kept going. What made you stay?

The compliance testing automation at Samay had a stretch in month two that was genuinely difficult. We had the core Lambda working but the multi-tenant orchestration wasn't right — Step Functions was sequencing the tenant invocations correctly but the per-tenant credential resolution from Secrets Manager was introducing intermittent failures we couldn't reproduce reliably.

The failures were non-deterministic. They happened 1 in 20 runs, under conditions we couldn't control. I spent a week on it — adding logging at every possible point, trying to isolate the timing window where the failure occurred. It was the kind of debugging where you're not sure you're making progress.

What kept me going: I had shown the auditors a working demo for one tenant. They had changed how they thought about the work based on what they saw. Walking away from the multi-tenant part would have meant they only ever got a single-client system. The gap between "working for one" and "working for all of them" was the actual value.

The fix ended up being a caching layer on the tenant credential resolution — the intermittent failure was a race condition on cold Lambda starts hitting Secrets Manager before the IAM policy propagation had fully completed. Once I understood the root cause, the fix was small. The path to understanding it was long.

---

### Q: How do you handle it when you're stuck and the deadline is real?

I timebox my rabbit holes. If I've been stuck on the same problem for more than two hours and I'm not making progress, I stop and ask someone. Not as a failure — as a tactic.

At Samay, the Secrets Manager race condition (above) — after two days of non-deterministic failures, I brought it to a senior engineer on the team. Not with "I don't know what's happening" but with a full writeup of what I'd tried, what the logs showed, and my current best hypothesis. That conversation led to the caching fix in about 30 minutes.

The thing I've learned: being stuck silently is the expensive choice. The cost of asking is embarrassment you feel for about 10 seconds. The cost of not asking is days.

For deadlines specifically: I communicate early. "I hit a blocker, here's what it is, here's my current plan, here's when I'll know if the plan is working." That gives the person who set the deadline the information they need to decide whether to adjust scope or timeline. It's not my job to absorb deadline pressure silently.

---

### Q: Tell me about a time you showed up for someone else who was struggling — not a technical problem, a person problem.

At Zemoso, there was a stretch near the end of a sprint where another developer on the Chem team had shipped their feature but the test coverage was thin — the kind that would flag in review and stall the PR. We were close to the deadline. I'd already closed my ticket for that sprint.

I picked up the test cases work without being asked. Traced through their code, figured out what was already covered, wrote the missing cases, submitted a PR against their ticket.

They were uncomfortable when they saw it. "You didn't have to do that." My response was: I had the time, they had the gap, the sprint needed both PRs to close. The right move was obvious.

What I understood after: they were also newer to the Strateos codebase than I was at that point. Writing test cases for someone else's feature on a system that complex — dozens of interrelated models, multiple microservices, different user permission layers — is harder than writing them for your own code. You have to reconstruct the intent, not just read the mechanics. When you're still building your mental model of a system and sprint velocity is real, test coverage is the first thing to slip. Not because you don't care — because you're still keeping up.

Picking that up wasn't a favor. It was just what the situation needed.

---

## 5. Genuine Curiosity About Work and People

---

### Q: How do you stay current in this space? What have you been following?

I'm subscribed to a few newsletters — TL;DR AI, a couple of Substacks — but honestly the most current signal I've found is X. Roj actually mentioned this, and it's accurate: the people shipping models and tools are posting about them in real time, before any article gets written. Anthropic's team, the OpenAI research accounts, the Grok/xAI team — you see what's being released and debated before it's been packaged into a think piece.

Recently I've been watching the MCP ecosystem specifically — Anthropic released MCP, then within a month you had n8n adding native MCP support, LangChain wrapping it, companies building public MCP tool registries. That's a real shift in how external tools get composed into agents. I used MCP as an architectural pattern in the take-home project before the SDK even existed, so watching it formalize into a standard is interesting to see play out.

I've also been closely watching the agent reliability work — how do you make an agent that doesn't hallucinate its tool calls, how do you give it memory that doesn't leak between users, how do you make the reasoning auditable. Those are the hard problems that matter for internal tools where the user is trusting the system to do real work on their behalf.

---

### Q: What drew you to ad tech specifically?

Honest answer: Roj drew me in during the first conversation. He described InMarket's problem in specific terms — heavy data pipelines, manual handoffs, Playwright-driven workflows that humans are doing by hand — and that's a pattern I've built automation for before.

But the thing that made it more interesting the more I thought about it: InMarket is a measurement company at its core. LCI processes $2.5 trillion in retail sales data. You're attributing media spend to actual visits and purchases. The data volume and the stakes are real — when a brand like Dunkin' or Bayer is making budget decisions based on LCI output, the internal tooling that produces those reports matters.

That's different from a lot of internal tooling work, where the impact is nice-to-have. Here, if an internal data pipeline breaks silently or a reporting workflow has a manual error, the downstream effect is real money in real campaign budgets. That makes the reliability and trust properties of the system much more interesting to me.

---

### Q: How do you actually get curious about the people you're working with or building for — not the problem, the person?

Work curiosity is easy — there's documentation, a codebase, a spec, something to read. Curiosity about a person takes more deliberate effort because the useful information isn't written anywhere.

At Samay, the most useful question I asked the compliance auditor wasn't "what data do you need?" It was "what's the worst part of audit season?" Not a requirements question — just a genuine question about her experience of the work. She said: "not knowing if we have enough evidence until it's too late to get more." That one answer shaped the design of the whole system in a way that no requirements doc would have captured. The automated collection ran on a continuous schedule specifically because of that answer — so auditors had evidence accumulating before they needed it, not scrambling during the audit window.

The question I've found consistently useful: "what's the worst part of this?" People know what hurts. They don't always know what good would look like. Starting from the pain is almost always more revealing than starting from the wishlist.

A different version of this happened at Epik. During the observation sessions with security analysts, I asked one of them directly: "What's the part of this morning that bothers you the most?" She didn't say volume of alerts. She said: "Nobody believes me when I flag something that looks low-priority but feels wrong." That wasn't a question I could have gotten from a requirements doc, and it wasn't in scope for what I was building. But it told me something important about who she was at work — the frustration wasn't with the tools, it was with not being heard. I kept that in mind every time I designed how the triage pipeline surfaced its confidence levels. The system being calibrated wasn't just for accuracy — it was so that when she flagged something, the tool backed her up.

I notice I'm naturally more curious about people than I sometimes act in professional contexts — there's a tendency to be heads-down on the technical problem. I've had to deliberately build the habit of stopping to ask the person question first, before the technical one.

---

### Q: What question do you wish people asked you more?

"What did you learn from the thing that didn't work?"

The stuff that goes well is usually a combination of preparation and some luck. The stuff that fails teaches you something that doesn't go away.

The most useful failure I've had was the first version of the Epik executive dashboard — the one I built too data-dense. I was genuinely confident it was good. Watching an executive close it after 30 seconds and not come back was a clean signal that confidence without user feedback is just wishful thinking. That's stuck with me. Now I try to get something in front of a real user before I'm confident about it, not after.

---

## 6. Building for Real Users

---

### Q: Tell me about a time you built something for non-technical users. How did you approach it?

Two examples.

**Epik dashboards for the C-suite:** The first version had everything. Every metric from every one of the 15+ security systems we were ingesting. I thought more information was better. After a week, executives stopped using it. I asked one of them directly: "what were you hoping to see when you opened this?" The answer: "am I getting worse or better, and what do I need to act on today?"

I rebuilt the whole UI around those two questions. Traffic-light status per system. A "needs attention" list with plain-English descriptions of what was wrong and what to do. A week-over-week trend line. Everything else was a click-through if they wanted detail. That version got used every day.

**Samay compliance chatbot:** Compliance auditors needed to ask questions like "which users have access to this repository and changed their permissions in the last 30 days?" against a Neo4j knowledge graph. Teaching them Cypher was never going to work. Building a keyword search wasn't going to work either — the questions were too varied and too specific.

I built a Flask service on AppRunner that took their plain language question and translated it to a Cypher graph traversal using LangChain. The UX was a simple text box. The auditors could ask questions in their own language and get structured answers with sources they could cite in their reports. The translation layer was invisible to them.

What I got right there: I kept the interface at the level the user was actually at, not at the level of the underlying technology. The fact that there was a graph database with LangChain-generated queries was completely hidden. They saw a search box and answers. That was the right call.

---

### Q: Talk about a time you had to simplify something complex for a non-technical audience.

At Epik, I had to explain to a senior stakeholder why the AI incident triage pipeline needed a two-week shadow period before we trusted it to act autonomously. She wanted to flip it on immediately — it was working in testing, why wait?

I used an analogy: "Think of it like a new hire. They're clearly capable — they passed the interview. But you wouldn't let them make final calls on major incidents on day one without anyone reviewing their work. The shadow period is the same thing. We're watching what it recommends, comparing it to what our experienced analysts would do, and calibrating where it's over-confident."

She immediately got it. The two-week period became part of the plan without argument.

What I've found: technical constraints land better when they're translated into human dynamics the other person already understands. Everyone knows what it means to ramp up a new team member. Almost nobody knows what false positive rate calibration means in the context of a triage classifier.

---

### Q: If you were embedded in InMarket's internal ops team tomorrow, where would you look first for automation opportunities?

Based on what Roj described: the handoffs. Every time a human has to move data from one system to another manually — copying a report output, triggering a downstream process, verifying that a pipeline completed and then taking an action — that's an automation opportunity.

Specifically:
- Campaign operations workflows in GeoLink that involve human steps between setup and launch — if Async Avails got campaign setup from 49 to 16 minutes by improving the UI, there might be further time to cut on the operational side through automation
- Internal reporting handoffs — if LCI attribution data is being manually pulled and formatted for agency reports, that's a Playwright/headless browser problem that should be a scheduled pipeline
- Cross-system status checks — if someone is manually checking whether a data pipeline completed before triggering downstream work, that's a monitoring and orchestration problem

I'd want to spend time with the ops people first, the same way I do anywhere: watch what they're doing by hand, ask "how long does this take?", ask "how often does it break?", ask "what happens when it breaks?" The answers to those three questions tell you exactly where to start.

---

## 7. InMarket-Specific & Product Thinking

---

### Q: What do you know about InMarket and what stands out to you?

The core positioning is that you're a measurement company more than an ad network — real-time ROI, LCI attribution, iROAS guarantees. That's the bet: brands care about outcomes, not impressions, and InMarket is the one that can prove the connection.

What stands out: the scale of the data layer. $2.5 trillion in retail sales, 127 billion item-level receipt transactions, 200M+ mobile devices. That's not a startup playing with AI on top of small data. The measurement product is credible because the data is real and large enough to be statistically meaningful. When Dunkin' says "InMarket's LCI tool is a staple of our measurement analytics," that's because LCI actually closes the loop — impression to foot traffic to purchase — not just impression to click.

The internal angle that interests me: a platform this data-heavy has a lot of operational surface area. The external product is polished — Wei's SUS scores prove that — but the internal operations that feed it (data ingestion, pipeline monitoring, agency reporting workflows, campaign ops) are probably where the manual toil lives. That's the gap the AI Builder role is plugging.

---

### Q: Wei's work includes things like InMarKit — the design system. What does a design system mean to you as an engineer?

It's a shared contract. When it works, I'm not making UI decisions I'm not qualified to make, and Wei isn't chasing down engineers who went off-spec. The design system is the place where "this is the truth" lives — component behavior, visual language, interaction patterns.

The engineering equivalent is an API contract or a module interface. When it's clear and respected, everyone moves faster because they're not rediscovering decisions that were already made.

Wei's numbers back this up — 40% faster front-end implementation. That's real. When I know exactly what component to use and exactly how it behaves, I'm not hunting through Figma files or making judgment calls about spacing. I'm implementing.

Where I'd want to contribute: the AI-generated components side. LLMs are increasingly good at scaffolding UI code — if you have a design system and the prompt is grounded in it, Copilot can generate a component that's on-spec most of the time. But that only works if the design system is well-documented and has clear usage patterns. Poorly documented design systems produce confidently wrong AI-generated code.

---

### Q: The AI Builder role involves both building new things and modernizing existing workflows. How do you decide which to prioritize?

Modernizing first, usually. New tools built on top of broken processes just fail in different ways.

The example I use: at Epik, I could have built a brand new incident classification AI from scratch. But the actual problem was upstream — the events coming into the triage system weren't consistently formatted, the sources had different schemas, and some of them were missing fields the classifier needed. If I had just trained a better model without fixing the ingestion, I'd have a more sophisticated system producing unreliable output.

I spent the first week standardizing the input pipeline — normalizing event schemas, adding validation, fixing the sources that were sending malformed data. Then I built the classifier on clean input. The classifier was actually the easier part.

At InMarket, I'd want to understand what the internal data flows look like before proposing new AI tooling. If the Playwright workflows Roj mentioned are fragile — brittle selectors, inconsistent page structures — the right first move is probably making them more reliable and observable before adding AI on top.

---

### Q: What would you build first if you had two weeks and full access?

I'd build an internal observability layer before building any automation. The thing Roj described — manual handoffs, headless browsers, pipelines — those are all things I'd want to be able to monitor before I try to automate them.

Concretely: a simple internal dashboard that shows which data pipelines are running, which are delayed, which completed with errors, and what the error was. Something the ops team can look at in the morning and immediately know if they need to intervene, instead of finding out an hour later when someone downstream notices a report is wrong.

At Samay we found a production pipeline failure because an auditor noticed gaps in a user's access history — not from any monitoring we had built. That was a wake-up call about how much I was operating blind. I'd rather know what's actually happening before automating anything on top of it.

That said — InMarket might already have something like this. I'd want to understand what exists before proposing anything new.

After that: automate the most painful handoff first. The one that happens most often, takes the most human time, and breaks most visibly when it fails. That's your highest-leverage starting point.

---

## 8. Questions to Ask Wei

These are conversation-openers, not interrogations. Let her talk.

---

### On her work and the platform:

- "The campaign setup time going from 49 to 16 minutes with Async Avails — what was the hardest thing about shipping that feature? Was it the technical complexity, the stakeholder alignment, or something else entirely?"

- "GeoLink Reports going from SUS 72 to 91 — what was the single biggest change that moved the score? I'm curious if it was one thing or a lot of small things."

- "InMarKit is 4+ years old now — what's the hardest part of maintaining a design system as the product evolves? I imagine the internal tooling is a very different consumer than the external platform."

---

### On the AI Builder role specifically:

- "When you think about where AI tooling is most useful internally — is it more in the ops/pipeline layer that Roj described, or are there product-level tools that design or PM need that engineering hasn't gotten to yet?"

- "The manual handoffs Roj mentioned — do those mostly live in campaign ops, or is there a reporting/agency side to it too? I'm trying to understand the full surface area."

---

### On collaboration and what working there looks like:

- "How does engineering and design work together on something like InMarKit — is it a you-maintain-it, engineers-consume-it model, or is it more of an ongoing collaboration?"

- "What does showing up for the team when things get hard look like here — is there a specific situation you can think of where that mattered?"

---

### On fit:

- "What's the thing that would make you most confident that an AI Builder was going to succeed here in the first 60 days? Not technically — more about how they show up."

---

## Quick Reference

| InMarket Product | Key Stat | What It Means |
|---|---|---|
| GeoLink | Campaign setup: 49 min → 16 min | Wei shipped Async Avails — huge UX/ops win |
| GeoLink Reports | SUS 72.5 → 91.25 | She measures with SUS scores — speak that language |
| InMarKit | 40% faster front-end implementation | Design system = shared contract |
| LCI Sales Attribution by Dimension | +83% revenue YOY | Measurement product drives real revenue |
| LCI data layer | $2.5T retail sales, 127B+ receipt transactions | Scale is real |
| Activation/Moments | 6x industry engagement benchmark | Real-time push ads at point of purchase |
| Company | 300+ people, 15+ years, 35+ awards | Established, not scrappy — culture is process-aware |

---

## Things NOT to Say

- Don't lead with technology in this round — lead with the user or the person doing the work
- Don't say "I can build anything" — be specific about what you'd prioritize and why
- Don't treat Wei as the gatekeeper to the technical round — she's evaluating real collaboration fit, give her real answers
- Don't forget she built internal tools herself at Perkins&Will — she knows what that work actually feels like, don't oversell it
- Don't pitch ideas for GeoLink's external product — focus on the internal ops/tooling layer that's actually the job

---

*Last updated: June 4, 2026 — InMarket Wei Tang round prep*


> [!example]- Alternate source version (html)
> # InMarket — Wei Tang Round Prep
>
>   
>
> Format: Culture + collaboration + product thinking, ~45–60 min.
>  Interviewer: Wei Tang — Principal Product Designer, 5 years at InMarket. Owns GeoLink end-to-end. Built InMarKit design system. Came from Perkins&Will where she built internal tools that saved 5,000+ labor hours/year. She measures everything with SUS scores, retention, and revenue impact.
>  Your posture: Collaborative builder who is genuinely curious about the user, the product, and the people doing the work — not just the technology. Engineer who thinks like a product person.
>
>    
>
> ### InMarket Context You Need to Know 
>
>  
>
> The company: Real-time marketing and measurement platform, 15+ years old, 300+ people, 35+ industry awards. Core thesis: right person, right message, right moment. Revenue model is B2B SaaS + managed campaigns for major brands (Danone, Bayer, Dunkin', Albertsons, Coors Light).
>
>  
>
> The product stack (external-facing):
>
>   
> - GeoLink — self-serve ad platform. Location-based audience targeting, GeoFences, GeoRetargeting, CTV/mobile/desktop. 200M+ mobile devices. This is where Wei has spent 5 years. Campaign setup used to take 49 minutes; she shipped Async Avails and got it to 16 minutes. That single feature retained $6.7M in client spend. 
> - LCI® (Lift, Conversion & Incrementality) — AI-powered measurement and optimization engine. Closed-loop attribution against $2.5T+ in retail sales data, 127B+ receipt transactions. Agencies use LCI to prove ROI to their clients. Dunkin', WPP, Reddit all on it. 
> - Activation — Preceptivity (AI-driven predictive audiences), Moments (InStore/InHome/InPath/InHand push experiences, 6x industry engagement benchmark). 
> - InSights — analytics layer for agencies and brands. 
> - Unified Platform — bringing GeoLink, Ventura, LCI, and InSights together.  
>
> The internal pain (what Roj told you): Heavy data pipelines, many manual handoffs, headless browsers, Playwright — these are the internal ops problems the AI Builder role is solving. Think: campaign operations teams doing things by hand that should be automated, reporting workflows that require scraping or headloading data between systems, maybe internal tooling that bridges GeoLink/LCI data to agency reporting.
>
>  
>
> Wei's specific work that matters for your conversation:
>
>   
> - GeoLink Async Avails: 49 min → 16 min campaign setup, $6.7M retained 
> - GeoLink Reports: SUS 72.5 → 91.25 (above-average → excellent) 
> - InMarKit design system: 30% faster prototyping, 40% faster front-end implementation 
> - LCI Sales Attribution by Dimension: 83% revenue increase YOY 
> - She thinks in SUS scores, time-on-task, revenue retained, and YOY comparisons — speak her language   
>
> ### Table of Contents 
>
>   
> - Tell Me About Yourself 
> - Collaboration Across Working Styles 
> - Navigating Disagreement & Changing Direction 
> - Showing Up When Things Get Hard 
> - Genuine Curiosity About Work and People 
> - Building for Real Users 
> - InMarket-Specific & Product Thinking 
> - Questions to Ask Wei   
>
> ### 1. Tell Me About Yourself 
>
>   
>
> #### Q: Walk me through who you are and why you're here. 
>
>  
>
> I'm a software engineer who's spent the last couple of years building AI-powered internal tools — pipelines, automation systems, compliance platforms. The consistent thread is: I don't just build what the spec says. I try to understand who's actually using the thing and what's making their day harder than it needs to be.
>
>  
>
> The most satisfying work I've done is when something I built made a manual, tedious process disappear for people who weren't engineers — security analysts who stopped spending their mornings triaging noise, compliance auditors who stopped spending days pulling evidence by hand.
>
>  
>
> I'm here because InMarket has a real internal ops problem that maps to exactly what I've been building. You've got heavy data pipelines, manual handoffs between teams, operational workflows that were designed before AI was practical. That's the gap I want to work in.
>
>  
>
> I also looked at what Wei has shipped here — taking GeoLink campaign setup from 49 minutes to 16 with Async Avails, getting the GeoLink Reports SUS score from 72 to 91 — and that kind of measurable, user-centered product thinking is the environment I want to be building in. When the people around you are measuring impact with SUS scores and revenue retained, it raises the bar for everybody.
>
>   
>
> #### Q: You're an engineer interviewing with a product designer. Why should that conversation be interesting? 
>
>  
>
> Because I think like a product person when I build. The first thing I ask about any feature isn't "what's the schema?" — it's "who is the person doing this today without the tool, and what does their day look like?"
>
>  
>
> At Epik, I sat with security analysts for two hours before writing a line of code — just watching their morning triage routine. At Samay, I spent time with compliance auditors doing a live walkthrough of a real audit before building any data model. In both cases, the thing I would have built from a spec alone would have been technically correct and practically useless.
>
>  
>
> I think that's the overlap between design and engineering at its best: you're both trying to understand the user deeply enough to build the right thing. The implementation language is different but the process has to be the same.
>
>   
>
> ### 2. Collaboration Across Working Styles 
>
>   
>
> #### Q: Tell me about a time you had to collaborate closely with someone who worked very differently from you. 
>
>  
>
> At Samay, I worked closely with a compliance domain expert who thought in legal frameworks and audit trails — not systems or data models. Her mental model of "evidence" was nothing like mine. She described what she needed in terms of audit procedures and control narratives. I was trying to map that to APIs, schemas, and Lambda functions.
>
>  
>
> Early on I'd come out of meetings with notes that I thought were clear and build something based on them. She'd look at it and say "that's not what I meant." Not because she was wrong — because I had translated her language into my language and lost something in the process.
>
>  
>
> The fix was: I stopped translating. I asked her to walk me through a real audit, step by step, as if I was a new auditor learning the job. I took notes in her language, not mine. "We look at whether config changes were tracked and reviewed" — I wrote that down exactly as she said it, then I did the translation afterward. The 6-source data model that the automated testing system ran on came entirely from that session. She didn't know what CloudTrail was. She knew she needed to see that config changes were tracked and reviewed. Those are the same thing, but only once you've done the translation carefully.
>
>  
>
> The working-style difference that almost caused the most friction wasn't expertise — it was pace. I wanted to iterate fast and show her something. She needed more certainty before she'd give feedback. The compromise was: I showed her something I explicitly labeled as 30% done with specific questions attached — "I'm not asking if this is right, I'm asking if the data I'm collecting matches what you actually look at." That unlocked the feedback loop.
>
>   
>
> #### Q: How do you work with designers? What does that relationship look like when it's going well vs. when it's not? 
>
>  
>
> When it goes well, the designer and I are solving the same problem from different angles and the answers converge. The designer is asking "what does this person need to understand at a glance?" and I'm asking "what does the system need to do to produce that?" We're checking each other's assumptions constantly.
>
>  
>
> The clearest example I have is from Epik — the C-suite dashboards. The first version I built was data-rich and technically complete. It aggregated telemetry from 15+ systems, every metric was accurate. The executives used it for a week and stopped. When I asked why: "we don't know what to do with this."
>
>  
>
> I rebuilt it around one question: what should I do right now? That's a design question, not an engineering question. Traffic-light status for each system, a "needs attention" list with plain-English explanations, week-over-week trend line. Everything else was a click-through. That version got used every day.
>
>  
>
> What I wish I had in that situation was a designer early — someone asking "what decision is this person making when they look at this screen?" before I built anything. The rebuild cost three or four days. A half-hour conversation with someone like Wei at the start would have saved it.
>
>  
>
> The flip side of that: at Zemoso I worked on a proprietary custom UI component library and had to change an expanded table component used across the whole platform. The ask was: add padding and a blue row highlight on expand. Simple on the surface. But I had to trace every place the existing component was used, understand why it was built the way it was, create a new version that didn't break existing consumers while adding the new behavior, cut a library release, then update all the call sites. Multiple review rounds with the onshore team to get the spacing exactly right. Took significantly longer than the surface ask suggested — a component library is load-bearing, you can't change it casually, and you don't really understand that until you've had to trace all its consumers.
>
>  
>
> When it doesn't go well: usually it's because design and engineering are running in parallel without talking, and the gap gets discovered at implementation. You end up in a negotiation over what gets cut. That's a process failure, not a people failure — it means the handoff happened too late.
>
>   
>
> #### Q: What's your hands-on experience with design tools, Figma, and the design-to-engineering process? 
>
>  
>
> I'm on the engineering side of that boundary, not the design side — so let me be honest about what I've actually done.
>
>  
>
> The most direct experience I have with Figma as a working artifact is from Zemoso/Strateos. The expanded table component task was explicitly framed as "it's not matching the Figma" — the Figma spec was the source of truth, and my job was to understand why the implementation had diverged and fix it. That meant opening the Figma file, reading the annotations, understanding the intended spacing and color behavior, and then tracing whether the component could even produce that output given how it was written. The component couldn't — it was structurally incompatible with some of the required behavior — which meant creating a new version of the component in the custom UI library, not just adjusting values.
>
>  
>
> The iterative review process that followed was where the real design-engineering dialogue happened. The onshore team had strong opinions about exact pixel values because those values affected how the component sat in different layouts across the platform. Multiple rounds of PR review, each with specific annotated feedback. I'd adjust, they'd review, we'd get on a call when comments weren't capturing the nuance. That back-and-forth is what "implementation matches design intent" actually looks like in practice — it's not a one-pass thing.
>
>  
>
> Beyond that: at Strateos, one of the four teams was a dedicated UX team. I was in the Chem team. We consumed their output — component specs, interaction patterns, flow documentation. When our work touched their components, we'd loop them in. Watching how they approached a feature request — the questions they asked about use cases before committing to a design direction — was genuinely useful to see up close.
>
>  
>
> What I understand about good handoff vs. bad handoff: when a Figma spec includes interaction notes, edge case states (empty, loading, error), and annotated rationale for decisions, implementation is fast and confident. When it's just the happy path, you end up making judgment calls at implementation time that should have been design decisions. Those judgment calls are where drift happens.
>
>  
>
> I also did a serious stretch of HTML/CSS/Bootstrap work during my time at Zemoso's training program — built responsive layouts, worked with grid systems, learned how visual structure maps to code. Enough to read a design spec and understand the structural intent, not just copy coordinates.
>
>   
>
> #### Q: You've worked across small startups and larger orgs. How do you adapt? 
>
>  
>
> At Zemoso (Strateos), I was one developer in a Chem team on a four-team project — lab devices, UX, Chem, and a fourth team I didn't overlap with much. The platform was enormous: a scientific experiment system with compounds, batches, runs, inventories, containers, multiple scientist roles with different permissions, dozens of microservices. It took two full days just to get the local environment running — Docker bringing up all services, health checks, the whole chain. The first time I had to write test cases for someone else's code, I needed to fully understand what the existing code was doing, what tests already covered it, and how to add coverage without breaking anything. That's a completely different posture than building from scratch. I had to slow down and be more deliberate than felt natural.
>
>  
>
> At Samay as founding engineer, the opposite — building from nothing with a 5-person team, fast feedback loops. Ship a Lambda in the morning, show a client in the afternoon, get new requirements the same day.
>
>  
>
> At Epik, embedded in an established enterprise security team, there were years of existing routing decisions, stakeholder relationships, and tool choices that had reasons behind them even when undocumented. Understanding those reasons before proposing changes was the right move.
>
>  
>
> The question I answer fast when I start somewhere new: how are decisions actually made here — not on paper, in practice — and who is the person opening this tool every morning?
>
>   
>
> ### 3. Navigating Disagreement & Changing Direction 
>
>   
>
> #### Q: Tell me about a time you pushed back on something and it changed the outcome. 
>
>  
>
> At Epik, a stakeholder wanted the incident triage pipeline to send Slack alerts with full event details — every field, all the context, inline in the message. The intent was good: make the alert as information-dense as possible so analysts had everything they needed without opening a ticket.
>
>  
>
> The problem I saw: several of those fields contained PII — employee account names, internal system identifiers, things that shouldn't be sitting in Slack channels that ops people share screens from. It was a security problem.
>
>  
>
> I didn't say "that's not possible" or "that's a security risk, we can't do it." I said: "Here's what that would take, and here's what we'd have to give up. We can send the fields that are safe. The full detail view would need to be a link to the internal ticket system, which is already access-controlled. That also makes the alert itself shorter and more actionable." I showed them what both versions would look like.
>
>  
>
> They actually preferred the second version once they saw it. Shorter alert, clear link, everything sensitive is one click away behind auth. Better UX and better security.
>
>   
>
> #### Q: Tell me about a time requirements changed significantly mid-build. How did you handle it? 
>
>  
>
> At Samay, I was mid-build on the automated compliance testing system — had CC7.1 (system monitoring) working, was generalizing the Lambda to accept any control — when the team lead came back from a client call. The client had changed their priorities. Different compliance controls, different evidence profile needed.
>
>  
>
> My first reaction was frustration, honestly. I had built something that was working and it felt like we were moving the target.
>
>  
>
> But when I looked at the actual impact, it was smaller than I expected. Because I had built the data collectors as separate modules — aws_collector.py, integration_collector.py — and the LLM analysis was a function that took a control ID and a data payload, the core architecture was already generic. Swapping which control was being tested was mostly a prompt change and tweaking which collectors were called. It wasn't a rewrite.
>
>  
>
> I gave the team lead a realistic assessment: "First of the new controls by end of week, second the week after." Honest, with reasoning. Not defensive, not falsely optimistic.
>
>   
>
> #### Q: Tell me about a time you changed direction because someone else was right. 
>
>  
>
> When I built the first version of the security dashboards at Epik, I genuinely believed dense information was better — analysts were smart, they'd know what to do with everything. The executives said they didn't know what to do with the dashboard. My first instinct was to explain it better.
>
>  
>
> Then I actually watched one of them use it. They scrolled to the bottom, found one number that looked bad, asked someone what it meant, and closed the tab. They hadn't engaged with 80% of what I built.
>
>  
>
> That's when I understood: the feedback wasn't "explain it better." It was "I don't want all of this." The problem was the paradigm, not the execution. I threw out the UI architecture of the first version — kept the data layer, changed everything about what to surface by default.
>
>  
>
> In hindsight, I was doing design work without a designer in the room. I had talked to executives about what they wanted, but talking to someone about a tool is different from watching them use it. What I thought I understood from the conversations wasn't what they actually needed in the moment of use. That's the kind of gap a design process catches — I just didn't have one in that situation.
>
>   
>
> #### Q: Tell me about a time you disagreed with a peer — not a requirements disagreement, a genuine technical disagreement — and you both had a real case. 
>
>  
>
> At Zemoso, I was reworking the expanded table component in the shared UI library. Multiple PR review rounds with the onshore tech lead. In one specific round, they asked for a reduced left-padding value — their reasoning was consistency with an existing component in the library. I looked at the Figma, traced all the places the table was used, and flagged a collision issue: in narrow-column configurations, their requested value would sit the text too close to the expand chevron. I pushed back on the review comment with a specific counter-proposal: "In narrow-column contexts the Figma shows a larger gap — I'd suggest X instead of Y."
>
>  
>
> Their response was immediate and not what I expected. They had a layout I hadn't seen — an upcoming feature that used a wider table configuration where their value was actually correct for that context. We got on a call because the comment thread wasn't capturing the nuance. With both layouts on screen at once, the answer was clear: neither of us was wrong, we needed two configurations instead of one value trying to satisfy both. The PR ended up slightly more complex than the original scope, but it was right.
>
>  
>
> What I noticed: the reviewer who pushes back hardest on something you're confident about is often seeing a context you haven't seen yet. That's the right frame before getting defensive.
>
>   
>
> #### Q: Tell me about a time leadership made a call you disagreed with and you had to work within it. 
>
>  
>
> At Monarch Tractor, we shortlisted three vendors for the HRMS automation: Workato, Boomi, and AWS native. I had calls with all three. Coming out of those calls, I thought Workato was the right choice — it was purpose-built for multi-system HRMS integrations, the connectors were mature, and the error handling they demoed was stronger than anything I'd build from scratch in a reasonable timeframe. Leadership picked AWS. Budget.
>
>  
>
> My honest read at the time: we'd spend more engineering hours building what Workato had already solved. And parts of that were true — the Lambda layer dependency issues, having to containerize just to run PowerShell, the custom error handling I had to write myself. But there were things I hadn't fully weighed when I disagreed: the team already had AWS infrastructure and skills, and the audit trail through CloudWatch and EventBridge was actually better for an HR system's compliance requirements than what Workato's logs would have given us. Once I was deep in the build, I understood better why someone with broader context had made that call.
>
>  
>
> I didn't formally push back — it was a leadership call made on constraints I didn't have full visibility into. What I did was document the Lambda/container tradeoff explicitly, so whoever touched the system next would understand why it was structured the way it was, not just that it was.
>
>   
>
> #### Q: Tell me about a time you pushed back on a direction and lost the argument — and then realized you were wrong. 
>
>  
>
> At Samay, when the team lead came back from the client call with the controls pivot, I pushed back. I had specific evidence: the new control set had a meaningfully different evidence profile, and one of them required a source integration we hadn't built yet. My position was clear: if we build automated testing for incomplete controls, we ship something that looks worse than nothing — the client sees a system that doesn't work rather than a system that works on the old scope. I said this directly to the team lead.
>
>  
>
> He heard me and overruled me. "Show the client progress on what they actually care about now. Flag the integration gap separately."
>
>  
>
> He was right. What I had missed: the client's confidence in the platform was the more urgent problem. They had changed their priorities — showing them forward motion on the controls they currently cared about mattered more than having a complete system for controls they'd deprioritized. The integration gap was real and got properly tracked. The client didn't care about the completeness of the old control set. I cared about it because I built it.
>
>  
>
> Being overruled and then being wrong is a different experience than just being overruled. It's more useful. I understood after that why "show progress on what the client needs right now" is sometimes the right call even when the technical situation isn't clean.
>
>   
>
> #### Q: Tell me about a time you were caught between two teams who had a legitimate disagreement about ownership. 
>
>  
>
> At Zemoso, the expanded table component I was reworking was in the shared UI library — documented as "stable, do not change behavior without UX review." The Chem team lead gave me the task without routing through the UX team, reasoning that it was a visual alignment fix, not a behavior change.
>
>  
>
> The UX team found out mid-review. One of their designers was on the PR and flagged it: this component appears in UX-specified flows across multiple screens — any padding change cascades. They wanted the PR held for a design review. The Chem lead's position: visual spec alignment isn't behavior change, this doesn't require a gate. The UX lead's position: in a shared component library, visual changes are behavior changes.
>
>  
>
> I was the developer who wrote the change, caught between two team leads in a thread that was going sideways fast.
>
>  
>
> What I did: I wrote a summary of exactly what the change did — specific, with before/after screenshots, a list of every component in the library that referenced the table, and which layouts were affected. I shared it in the thread without taking a side. I moved the conversation from "who has authority here" to "here's the actual scope, let's decide from this." The UX team signed off with one small adjustment. The review that looked like it was going to take another week happened in a day.
>
>  
>
> The useful thing I took from that: when two people are disagreeing about ownership, it's often because they don't have the same information about the actual scope. Getting that information on the table — neutral, specific, without editorializing — is almost always the fastest way through.
>
>   
>
> ### 4. Showing Up When Things Get Hard 
>
>   
>
> #### Q: Tell me about a time something you built broke in production. What did you do? 
>
>  
>
> At Samay, we had a distributed identity event ingestion pipeline that was silently dropping events under load. No errors, no alerts — the pipeline looked healthy from the outside, but the event counts were off. An auditor noticed that a user's access history had gaps. That's how we found it — not from a monitoring alert, from a human noticing something wrong in a manual review. The fact that it surfaced that way bothered me more than the bug itself.
>
>  
>
> I ran it down by adding counters at every stage of the pipeline — events received, events processed, events written — and comparing the deltas. The failure was a Spark job hitting memory limits and silently discarding the overflow batch instead of raising an error. It had been configured with error handling that was too defensive.
>
>  
>
> Fix: reduce batch size, change the error handling so memory failures raised visibly, and add an end-of-pipeline count reconciliation job that paged if the numbers didn't match.
>
>  
>
> But the more important fix was: I added the reconciliation job as a pattern across other pipelines too. Not just the one that broke. If one pipeline could fail silently, others could too.
>
>   
>
> #### Q: Tell me about a time the project was genuinely hard and you kept going. What made you stay? 
>
>  
>
> The compliance testing automation at Samay had a stretch in month two that was genuinely difficult. We had the core Lambda working but the multi-tenant orchestration wasn't right — Step Functions was sequencing the tenant invocations correctly but the per-tenant credential resolution from Secrets Manager was introducing intermittent failures we couldn't reproduce reliably.
>
>  
>
> The failures were non-deterministic. They happened 1 in 20 runs, under conditions we couldn't control. I spent a week on it — adding logging at every possible point, trying to isolate the timing window where the failure occurred. It was the kind of debugging where you're not sure you're making progress.
>
>  
>
> What kept me going: I had shown the auditors a working demo for one tenant. They had changed how they thought about the work based on what they saw. Walking away from the multi-tenant part would have meant they only ever got a single-client system. The gap between "working for one" and "working for all of them" was the actual value.
>
>  
>
> The fix ended up being a caching layer on the tenant credential resolution — the intermittent failure was a race condition on cold Lambda starts hitting Secrets Manager before the IAM policy propagation had fully completed. Once I understood the root cause, the fix was small. The path to understanding it was long.
>
>   
>
> #### Q: How do you handle it when you're stuck and the deadline is real? 
>
>  
>
> I timebox my rabbit holes. If I've been stuck on the same problem for more than two hours and I'm not making progress, I stop and ask someone. Not as a failure — as a tactic.
>
>  
>
> At Samay, the Secrets Manager race condition (above) — after two days of non-deterministic failures, I brought it to a senior engineer on the team. Not with "I don't know what's happening" but with a full writeup of what I'd tried, what the logs showed, and my current best hypothesis. That conversation led to the caching fix in about 30 minutes.
>
>  
>
> The thing I've learned: being stuck silently is the expensive choice. The cost of asking is embarrassment you feel for about 10 seconds. The cost of not asking is days.
>
>  
>
> For deadlines specifically: I communicate early. "I hit a blocker, here's what it is, here's my current plan, here's when I'll know if the plan is working." That gives the person who set the deadline the information they need to decide whether to adjust scope or timeline. It's not my job to absorb deadline pressure silently.
>
>   
>
> #### Q: Tell me about a time you showed up for someone else who was struggling — not a technical problem, a person problem. 
>
>  
>
> At Zemoso, there was a stretch near the end of a sprint where another developer on the Chem team had shipped their feature but the test coverage was thin — the kind that would flag in review and stall the PR. We were close to the deadline. I'd already closed my ticket for that sprint.
>
>  
>
> I picked up the test cases work without being asked. Traced through their code, figured out what was already covered, wrote the missing cases, submitted a PR against their ticket.
>
>  
>
> They were uncomfortable when they saw it. "You didn't have to do that." My response was: I had the time, they had the gap, the sprint needed both PRs to close. The right move was obvious.
>
>  
>
> What I understood after: they were also newer to the Strateos codebase than I was at that point. Writing test cases for someone else's feature on a system that complex — dozens of interrelated models, multiple microservices, different user permission layers — is harder than writing them for your own code. You have to reconstruct the intent, not just read the mechanics. When you're still building your mental model of a system and sprint velocity is real, test coverage is the first thing to slip. Not because you don't care — because you're still keeping up.
>
>  
>
> Picking that up wasn't a favor. It was just what the situation needed.
>
>   
>
> ### 5. Genuine Curiosity About Work and People 
>
>   
>
> #### Q: How do you stay current in this space? What have you been following? 
>
>  
>
> I'm subscribed to a few newsletters — TL;DR AI, a couple of Substacks — but honestly the most current signal I've found is X. Roj actually mentioned this, and it's accurate: the people shipping models and tools are posting about them in real time, before any article gets written. Anthropic's team, the OpenAI research accounts, the Grok/xAI team — you see what's being released and debated before it's been packaged into a think piece.
>
>  
>
> Recently I've been watching the MCP ecosystem specifically — Anthropic released MCP, then within a month you had n8n adding native MCP support, LangChain wrapping it, companies building public MCP tool registries. That's a real shift in how external tools get composed into agents. I used MCP as an architectural pattern in the take-home project before the SDK even existed, so watching it formalize into a standard is interesting to see play out.
>
>  
>
> I've also been closely watching the agent reliability work — how do you make an agent that doesn't hallucinate its tool calls, how do you give it memory that doesn't leak between users, how do you make the reasoning auditable. Those are the hard problems that matter for internal tools where the user is trusting the system to do real work on their behalf.
>
>   
>
> #### Q: What drew you to ad tech specifically? 
>
>  
>
> Honest answer: Roj drew me in during the first conversation. He described InMarket's problem in specific terms — heavy data pipelines, manual handoffs, Playwright-driven workflows that humans are doing by hand — and that's a pattern I've built automation for before.
>
>  
>
> But the thing that made it more interesting the more I thought about it: InMarket is a measurement company at its core. LCI processes $2.5 trillion in retail sales data. You're attributing media spend to actual visits and purchases. The data volume and the stakes are real — when a brand like Dunkin' or Bayer is making budget decisions based on LCI output, the internal tooling that produces those reports matters.
>
>  
>
> That's different from a lot of internal tooling work, where the impact is nice-to-have. Here, if an internal data pipeline breaks silently or a reporting workflow has a manual error, the downstream effect is real money in real campaign budgets. That makes the reliability and trust properties of the system much more interesting to me.
>
>   
>
> #### Q: How do you actually get curious about the people you're working with or building for — not the problem, the person? 
>
>  
>
> Work curiosity is easy — there's documentation, a codebase, a spec, something to read. Curiosity about a person takes more deliberate effort because the useful information isn't written anywhere.
>
>  
>
> At Samay, the most useful question I asked the compliance auditor wasn't "what data do you need?" It was "what's the worst part of audit season?" Not a requirements question — just a genuine question about her experience of the work. She said: "not knowing if we have enough evidence until it's too late to get more." That one answer shaped the design of the whole system in a way that no requirements doc would have captured. The automated collection ran on a continuous schedule specifically because of that answer — so auditors had evidence accumulating before they needed it, not scrambling during the audit window.
>
>  
>
> The question I've found consistently useful: "what's the worst part of this?" People know what hurts. They don't always know what good would look like. Starting from the pain is almost always more revealing than starting from the wishlist.
>
>  
>
> A different version of this happened at Epik. During the observation sessions with security analysts, I asked one of them directly: "What's the part of this morning that bothers you the most?" She didn't say volume of alerts. She said: "Nobody believes me when I flag something that looks low-priority but feels wrong." That wasn't a question I could have gotten from a requirements doc, and it wasn't in scope for what I was building. But it told me something important about who she was at work — the frustration wasn't with the tools, it was with not being heard. I kept that in mind every time I designed how the triage pipeline surfaced its confidence levels. The system being calibrated wasn't just for accuracy — it was so that when she flagged something, the tool backed her up.
>
>  
>
> I notice I'm naturally more curious about people than I sometimes act in professional contexts — there's a tendency to be heads-down on the technical problem. I've had to deliberately build the habit of stopping to ask the person question first, before the technical one.
>
>   
>
> #### Q: What question do you wish people asked you more? 
>
>  
>
> "What did you learn from the thing that didn't work?"
>
>  
>
> The stuff that goes well is usually a combination of preparation and some luck. The stuff that fails teaches you something that doesn't go away.
>
>  
>
> The most useful failure I've had was the first version of the Epik executive dashboard — the one I built too data-dense. I was genuinely confident it was good. Watching an executive close it after 30 seconds and not come back was a clean signal that confidence without user feedback is just wishful thinking. That's stuck with me. Now I try to get something in front of a real user before I'm confident about it, not after.
>
>   
>
> ### 6. Building for Real Users 
>
>   
>
> #### Q: Tell me about a time you built something for non-technical users. How did you approach it? 
>
>  
>
> Two examples.
>
>  
>
> Epik dashboards for the C-suite: The first version had everything. Every metric from every one of the 15+ security systems we were ingesting. I thought more information was better. After a week, executives stopped using it. I asked one of them directly: "what were you hoping to see when you opened this?" The answer: "am I getting worse or better, and what do I need to act on today?"
>
>  
>
> I rebuilt the whole UI around those two questions. Traffic-light status per system. A "needs attention" list with plain-English descriptions of what was wrong and what to do. A week-over-week trend line. Everything else was a click-through if they wanted detail. That version got used every day.
>
>  
>
> Samay compliance chatbot: Compliance auditors needed to ask questions like "which users have access to this repository and changed their permissions in the last 30 days?" against a Neo4j knowledge graph. Teaching them Cypher was never going to work. Building a keyword search wasn't going to work either — the questions were too varied and too specific.
>
>  
>
> I built a Flask service on AppRunner that took their plain language question and translated it to a Cypher graph traversal using LangChain. The UX was a simple text box. The auditors could ask questions in their own language and get structured answers with sources they could cite in their reports. The translation layer was invisible to them.
>
>  
>
> What I got right there: I kept the interface at the level the user was actually at, not at the level of the underlying technology. The fact that there was a graph database with LangChain-generated queries was completely hidden. They saw a search box and answers. That was the right call.
>
>   
>
> #### Q: Talk about a time you had to simplify something complex for a non-technical audience. 
>
>  
>
> At Epik, I had to explain to a senior stakeholder why the AI incident triage pipeline needed a two-week shadow period before we trusted it to act autonomously. She wanted to flip it on immediately — it was working in testing, why wait?
>
>  
>
> I used an analogy: "Think of it like a new hire. They're clearly capable — they passed the interview. But you wouldn't let them make final calls on major incidents on day one without anyone reviewing their work. The shadow period is the same thing. We're watching what it recommends, comparing it to what our experienced analysts would do, and calibrating where it's over-confident."
>
>  
>
> She immediately got it. The two-week period became part of the plan without argument.
>
>  
>
> What I've found: technical constraints land better when they're translated into human dynamics the other person already understands. Everyone knows what it means to ramp up a new team member. Almost nobody knows what false positive rate calibration means in the context of a triage classifier.
>
>   
>
> #### Q: If you were embedded in InMarket's internal ops team tomorrow, where would you look first for automation opportunities? 
>
>  
>
> Based on what Roj described: the handoffs. Every time a human has to move data from one system to another manually — copying a report output, triggering a downstream process, verifying that a pipeline completed and then taking an action — that's an automation opportunity.
>
>  
>
> Specifically:
>
>   
> - Campaign operations workflows in GeoLink that involve human steps between setup and launch — if Async Avails got campaign setup from 49 to 16 minutes by improving the UI, there might be further time to cut on the operational side through automation 
> - Internal reporting handoffs — if LCI attribution data is being manually pulled and formatted for agency reports, that's a Playwright/headless browser problem that should be a scheduled pipeline 
> - Cross-system status checks — if someone is manually checking whether a data pipeline completed before triggering downstream work, that's a monitoring and orchestration problem  
>
> I'd want to spend time with the ops people first, the same way I do anywhere: watch what they're doing by hand, ask "how long does this take?", ask "how often does it break?", ask "what happens when it breaks?" The answers to those three questions tell you exactly where to start.
>
>   
>
> ### 7. InMarket-Specific & Product Thinking 
>
>   
>
> #### Q: What do you know about InMarket and what stands out to you? 
>
>  
>
> The core positioning is that you're a measurement company more than an ad network — real-time ROI, LCI attribution, iROAS guarantees. That's the bet: brands care about outcomes, not impressions, and InMarket is the one that can prove the connection.
>
>  
>
> What stands out: the scale of the data layer. $2.5 trillion in retail sales, 127 billion item-level receipt transactions, 200M+ mobile devices. That's not a startup playing with AI on top of small data. The measurement product is credible because the data is real and large enough to be statistically meaningful. When Dunkin' says "InMarket's LCI tool is a staple of our measurement analytics," that's because LCI actually closes the loop — impression to foot traffic to purchase — not just impression to click.
>
>  
>
> The internal angle that interests me: a platform this data-heavy has a lot of operational surface area. The external product is polished — Wei's SUS scores prove that — but the internal operations that feed it (data ingestion, pipeline monitoring, agency reporting workflows, campaign ops) are probably where the manual toil lives. That's the gap the AI Builder role is plugging.
>
>   
>
> #### Q: Wei's work includes things like InMarKit — the design system. What does a design system mean to you as an engineer? 
>
>  
>
> It's a shared contract. When it works, I'm not making UI decisions I'm not qualified to make, and Wei isn't chasing down engineers who went off-spec. The design system is the place where "this is the truth" lives — component behavior, visual language, interaction patterns.
>
>  
>
> The engineering equivalent is an API contract or a module interface. When it's clear and respected, everyone moves faster because they're not rediscovering decisions that were already made.
>
>  
>
> Wei's numbers back this up — 40% faster front-end implementation. That's real. When I know exactly what component to use and exactly how it behaves, I'm not hunting through Figma files or making judgment calls about spacing. I'm implementing.
>
>  
>
> Where I'd want to contribute: the AI-generated components side. LLMs are increasingly good at scaffolding UI code — if you have a design system and the prompt is grounded in it, Copilot can generate a component that's on-spec most of the time. But that only works if the design system is well-documented and has clear usage patterns. Poorly documented design systems produce confidently wrong AI-generated code.
>
>   
>
> #### Q: The AI Builder role involves both building new things and modernizing existing workflows. How do you decide which to prioritize? 
>
>  
>
> Modernizing first, usually. New tools built on top of broken processes just fail in different ways.
>
>  
>
> The example I use: at Epik, I could have built a brand new incident classification AI from scratch. But the actual problem was upstream — the events coming into the triage system weren't consistently formatted, the sources had different schemas, and some of them were missing fields the classifier needed. If I had just trained a better model without fixing the ingestion, I'd have a more sophisticated system producing unreliable output.
>
>  
>
> I spent the first week standardizing the input pipeline — normalizing event schemas, adding validation, fixing the sources that were sending malformed data. Then I built the classifier on clean input. The classifier was actually the easier part.
>
>  
>
> At InMarket, I'd want to understand what the internal data flows look like before proposing new AI tooling. If the Playwright workflows Roj mentioned are fragile — brittle selectors, inconsistent page structures — the right first move is probably making them more reliable and observable before adding AI on top.
>
>   
>
> #### Q: What would you build first if you had two weeks and full access? 
>
>  
>
> I'd build an internal observability layer before building any automation. The thing Roj described — manual handoffs, headless browsers, pipelines — those are all things I'd want to be able to monitor before I try to automate them.
>
>  
>
> Concretely: a simple internal dashboard that shows which data pipelines are running, which are delayed, which completed with errors, and what the error was. Something the ops team can look at in the morning and immediately know if they need to intervene, instead of finding out an hour later when someone downstream notices a report is wrong.
>
>  
>
> At Samay we found a production pipeline failure because an auditor noticed gaps in a user's access history — not from any monitoring we had built. That was a wake-up call about how much I was operating blind. I'd rather know what's actually happening before automating anything on top of it.
>
>  
>
> That said — InMarket might already have something like this. I'd want to understand what exists before proposing anything new.
>
>  
>
> After that: automate the most painful handoff first. The one that happens most often, takes the most human time, and breaks most visibly when it fails. That's your highest-leverage starting point.
>
>   
>
> ### 8. Questions to Ask Wei 
>
>  
>
> These are conversation-openers, not interrogations. Let her talk.
>
>   
>
> #### On her work and the platform: 
>
>   
> -  
>
> "The campaign setup time going from 49 to 16 minutes with Async Avails — what was the hardest thing about shipping that feature? Was it the technical complexity, the stakeholder alignment, or something else entirely?"
>
>   
> -  
>
> "GeoLink Reports going from SUS 72 to 91 — what was the single biggest change that moved the score? I'm curious if it was one thing or a lot of small things."
>
>   
> -  
>
> "InMarKit is 4+ years old now — what's the hardest part of maintaining a design system as the product evolves? I imagine the internal tooling is a very different consumer than the external platform."
>
>     
>
> #### On the AI Builder role specifically: 
>
>   
> -  
>
> "When you think about where AI tooling is most useful internally — is it more in the ops/pipeline layer that Roj described, or are there product-level tools that design or PM need that engineering hasn't gotten to yet?"
>
>   
> -  
>
> "The manual handoffs Roj mentioned — do those mostly live in campaign ops, or is there a reporting/agency side to it too? I'm trying to understand the full surface area."
>
>     
>
> #### On collaboration and what working there looks like: 
>
>   
> -  
>
> "How does engineering and design work together on something like InMarKit — is it a you-maintain-it, engineers-consume-it model, or is it more of an ongoing collaboration?"
>
>   
> -  
>
> "What does showing up for the team when things get hard look like here — is there a specific situation you can think of where that mattered?"
>
>     
>
> #### On fit: 
>
>   
> - "What's the thing that would make you most confident that an AI Builder was going to succeed here in the first 60 days? Not technically — more about how they show up."   
>
> ### Quick Reference 
>
>    
>
>   | InMarket Product  | Key Stat  | What It Means 
>
>    
>
>   | GeoLink  | Campaign setup: 49 min → 16 min  | Wei shipped Async Avails — huge UX/ops win 
>
>  
>
>   | GeoLink Reports  | SUS 72.5 → 91.25  | She measures with SUS scores — speak that language 
>
>  
>
>   | InMarKit  | 40% faster front-end implementation  | Design system = shared contract 
>
>  
>
>   | LCI Sales Attribution by Dimension  | +83% revenue YOY  | Measurement product drives real revenue 
>
>  
>
>   | LCI data layer  | $2.5T retail sales, 127B+ receipt transactions  | Scale is real 
>
>  
>
>   | Activation/Moments  | 6x industry engagement benchmark  | Real-time push ads at point of purchase 
>
>  
>
>   | Company  | 300+ people, 15+ years, 35+ awards  | Established, not scrappy — culture is process-aware 
>
>     
>
> ### Things NOT to Say 
>
>   
> - Don't lead with technology in this round — lead with the user or the person doing the work 
> - Don't say "I can build anything" — be specific about what you'd prioritize and why 
> - Don't treat Wei as the gatekeeper to the technical round — she's evaluating real collaboration fit, give her real answers 
> - Don't forget she built internal tools herself at Perkins&Will — she knows what that work actually feels like, don't oversell it 
> - Don't pitch ideas for GeoLink's external product — focus on the internal ops/tooling layer that's actually the job   
>
> Last updated: June 4, 2026 — InMarket Wei Tang round prep

## Source provenance

- [Original HTML](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/AI%20Builder/InMarket%20JD%20and%20Resume%2C%20interview%20round%20info/Wei_Tang_Round_Prep.html) · AI Builder/InMarket JD and Resume, interview round info/Wei_Tang_Round_Prep.html
- [Original MD](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/AI%20Builder/InMarket%20JD%20and%20Resume%2C%20interview%20round%20info/Wei_Tang_Round_Prep.md) · AI Builder/InMarket JD and Resume, interview round info/Wei_Tang_Round_Prep.md
- [Original HTML](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Interview%20Prep%20company%20prep%20docs/AI%20Builder/InMarket%20JD%20and%20Resume%2C%20interview%20round%20info/Wei_Tang_Round_Prep.html) · Interview Prep company prep docs/AI Builder/InMarket JD and Resume, interview round info/Wei_Tang_Round_Prep.html
- [Original MD](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Interview%20Prep%20company%20prep%20docs/AI%20Builder/InMarket%20JD%20and%20Resume%2C%20interview%20round%20info/Wei_Tang_Round_Prep.md) · Interview Prep company prep docs/AI Builder/InMarket JD and Resume, interview round info/Wei_Tang_Round_Prep.md

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
