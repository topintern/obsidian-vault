---
kind: "experience-source"
title: "Data Engineering In Healthcare Behavioural Prep"
collection: "Experience Sources"
topic: "Experience"
imported: "2026-10-13"
source_files: ["Data Engineering/Data Engineering in Healthcare Behavioural Prep.docx"]
tags: ["career/library"]
source_status: "source-claims-not-verified"
---

# Data Engineering In Healthcare Behavioural Prep

[[The Climb/Career Library/Career Library]]

> [!info] Source context
> Historical preparation or source notes. First-person stories and numeric outcomes remain source claims until confirmed; this import does not verify them.

**
Contexture Panel Interview Preparation (Behavioural):**

**Why contexture?**

- I’ve really valued my experience in large corporate healthcare, but a lot of that work supports internal operations. But why contexture is my next move, is that  it’s one of the largest regional HIEs in the west, is a community-focused, nonprofit and runs a unified platform across two states with a very broad participant network. It recently finished unifying multiple legacy HIE platforms into a single, shared platform across both states. I felt this could be my next best place.

**Where do you live in arizona?**

Everlee Terrace, patriot square apartments, Arizona, by celebrity theatre.

**Who are some people you work with?**

Sussana Hough - Manager

Christine Carlson - Director
Vijay L - Colleague

**Team Size?**

I’m part of a data engineering team of about 8–10 engineers, plus a few data analysts and a product owner

**Stakeholder interaction:**

*My stakeholders are primarily analytics teams and business SMEs. We do bi-weekly pipeline reviews, I translate their metrics needs into schemas and transformations, *

*and for incidents I give them immediate impact + ETA. The goal is they trust the data enough to make million-dollar decisions off it*

### ***Translating requirements***

*When analysts needed new metrics or datasets (e.g., "patient utilization by provider type")*

* I'd run a requirements workshop:*

- *Document their exact business question and desired grain*

- *Propose data model and transformation approach*

- *Mock up sample output and get signoff before building*

### ***Escalations and issue resolution***

*For production issues (e.g., late batch, data anomaly), I'd triage first, then give stakeholders a 2-minute status:*

- *What broke*

- *Business impact*

- *ETA to fix*

- *Workaround if needed*

- **Describe an end-to-end pipeline you built” / “How do you ingest from APIs / DBs / flat files?**

“At **UnitedHealth **Group, I designed and implemented an end-to-end data pipeline to **ingest clinical **and **claims data **from **multiple healthcare systems **into a **centralized analytics platform **on **AWS **and **Snowflake**, supporting **reporting**, population **health analytics**, and **downstream **BI (**Business** **Intelligence**) teams.”

### **1. Sources & ingestion**

“We were ingesting a mix of structured and semi-structured healthcare data:

- Relational sources like **Oracle **for **claims **and **member data**.

- **HL7/FHIR feeds** and **APIs from clinical systems** for encounters, diagnoses, procedures, and labs.

- **Flat files (CSV/JSON)** **periodically dropped **into SFTP or **cloud storage **for **partner feeds**.

**For **databases like **Oracle**, I used **parallelized extract jobs **(e.g., via **Spark on EMR **or **Glue jobs**) with **incremental strategies **based on **timestamps **or **surrogate keys**, so we only pulled **new/changed** data **each run**. For APIs and **HL7**/**FHIR** messages, we had ingestion services that wrote raw payloads into an **S3 landing zone**, **partitioned **by **source system **and **load date **for **traceability **and easy **reprocessing**.”

Key ideas to hit:

- Multiple heterogeneous healthcare sources.

- Incremental ingestion, not full reloads.

- Raw “landing” layer on S3 with partitioning.

### **2. Staging & validation**

“From the landing zone, the next step was a staging layer where we did schema validation and basic data quality checks before allowing data downstream.

- We used** Spark jobs to validate schemas** (**required** **columns**, basic types), check **record counts**, and detect **schema drift **or **malformed HL7**/**FHIR** **messages**.

- Any **records **that **failed **validation were **moved **into **quarantine tables**/**paths** **with error reasons captured**, and **alerts **were **sent **so we could follow up with the source system.

- For **successful records**, we **standardized formats **like **dates**, **IDs**, and basic code sets, but still kept them close to the source structure in this stage.”

Key points:

- Explicit **staging layer**.

- **Quarantine **for bad records + alerts.

- Early, **cheap **data **quality checks**.

### **3. Core transformations: standardization, normalization, dedup, joins**

“After staging, we had **transformation jobs **that turned raw healthcare data into a **canonical**, **analytics**-**ready** model.

- We **standardized patient **and encounter **representations **so **data from different providers followed **a **common schema **(e.g., **consistent patient IDs**, **encounter types**, **date**/**time** **formats**).

- We performed **normalization **and **mapping **of **clinical codes**: mapping **local **codes to **ICD**-**10** **for diagnoses**, **CPT for procedures**, and LOINC/SNOMED where applicable for labs and clinical concepts, **using centralized mapping tables**.

- We **implemented deduplication logic **for **claims **and **encounters **(for example, **removing exact duplicates from resend **scenarios, and **resolving multiple entries **for the **same encounter **based on **timestamps **and **status fields**).

- We joined across domains—members, eligibility, claims, and clinical events—to build a coherent longitudinal view at the patient level.

These **transformations **were **implemented as Spark jobs **(Scala/**PySpark**) **running on EMR **and, in some cases, **SQL transformations in Snowflake **for downstream shaping and aggregations.”

Key points:

- **Canonical model **across sources.

- Code-set mapping (ICD-10, CPT, etc.).

- Dedup + joins for longitudinal view.

- Mix of **Spark **and **warehouse**-**side** **SQL**.

### **4. Data storage layers (lake + warehouse)**

“For storage, we used a layered approach:

- On** S3**, we stored **curated data **in columnar formats like **Parquet**, **partitioned **by key dimensions such as **load_date **and sometimes **payer or market**, to **optimize downstream access**.

- In **Snowflake**, we designed schemas to support **analytics**: dimension and fact tables for members, providers, encounters, and claims. We leveraged **clustering**/**partitioning** **strategies **and appropriate keys to improve query performance on large, **terabyte**-**scale** datasets.

The idea was: **S3 **acted as the long-term, **cost**-**effective** data lake and **raw archive**, while **Snowflake **was the **primary analytics**/**BI** **warehouse **that analysts and data scientists queried.”

Key points:

- Multi-layer model (landing → staging → curated).

- Parquet + partitioning on S3; modeled tables in Snowflake.

- Reason: performance + cost + flexibility.

### **5. Orchestration, scheduling, and fault tolerance**

“All these steps were orchestrated through workflow tools like Airflow:

- We **defined DAGs **that encapsulated the end-to-end flow: **extract **→ **stage **→ **transform **→ **load **into **Snowflake **→ **data quality checks **→ **publish**/**notify**.

- Each step had retries with backoff, and we designed **tasks **to be **idempotent**—**re**-**running** for a given **batch**/date would **overwrite or upsert **the same data slice rather than duplicating rows.

- We implemented **dependency checks **so downstream steps **only ran **when **upstream sources were complete **and data quality checks passed.

- Operationally, we had **centralized logging and metrics **(e.g., rows processed, error counts, runtime), and alerts wired into our monitoring system if a DAG failed, ran too long, or produced anomalous volumes.”

Key points:

- Airflow-like orchestration.

- Idempotent batch design.

- SLAs and monitoring.

### **6. Data quality, SLAs, and monitoring**

“Because this was healthcare data with strict SLAs and regulatory reporting implications, data quality and observability were critical:

- We implemented **row-count reconciliation between source and target**, **referential integrity checks **(e.g., no encounters without a member), and business rule checks (e.g., valid date ranges, no negative costs).

- We **monitored **key metrics like **daily volume **per source, distinct patient counts, and distribution of diagnosis/procedure codes to **detect anomalies early**.

- If metrics fell outside expected ranges, the pipeline could mark the run as degraded and avoid publishing to production schemas until we investigated.

This ensured that downstream teams and clinicians could trust the data.”

Key points:

- DQ checks at multiple stages.

- Volume and distribution monitoring.

- Safe failure mode (degraded run, not silent corruption).

### **7. Security, privacy, and compliance**

“Given we were dealing with** PHI and HIPAA constraints**, we built security into the pipeline:

- **All data in transit used TLS;** data **at rest in S3 and Snowflake was encrypted**.

- **Access **to **S3 **buckets, **EMR**, and **Snowflake schemas **was controlled via fine-grained **IAM **and role-based access, following **least**-**privilege** principles.

- We **avoided logging PHI **in **application logs **and **used tokenization **or de-identification for certain analytics use cases.

- Changes to pipelines went through version control, code reviews, and a controlled release process, aligning with a secure SDLC.”

Key points:

- Encryption, IAM, least privilege.

- No PHI in logs; de-identification where needed.

- SSDLC: reviews + controlled releases.

### **8. Business outcomes**

“From a business standpoint, this end-to-end pipeline enabled:

- Reliable** daily refreshes of healthcare utilization **and quality metrics.

- Faster, more **scalable queries **on **large datasets **thanks to proper **partitioning **and **Snowflake optimization**.

- A single, **consistent view **of **patients **and **encounters **that could be used **across teams**—for **BI dashboards**, actuarial models, and **clinical analytics**.

Overall, it reduced **manual data wrangling **for **analytics teams **and improved confidence and timeliness of healthcare insights.”

**Other Projects:**

A migration initiative to move certain subject-area datasets from on‑prem systems into Snowflake, where I worked on schema design, incremental load strategies, and performance tuning

quality and monitoring framework where I helped define and implement automated checks (row counts, referential integrity, code-set coverage) and integrated them into our orchestration workflows.

**2. ****Tell me about a time you significantly improved a pipeline’s performance or reliability.**

At UnitedHealth Group, I took ownership of a daily healthcare claims processing pipeline that was consistently running 2-3x over its SLA due to full table scans on massive Oracle extracts.

The pipeline processed ~500M claims records monthly from Oracle into S3/Snowflake for downstream analytics, but transformation jobs were taking 4+ hours instead of the targeted 90 minutes.​

I implemented three key optimizations:

- Partitioning strategy: Changed from date-only partitioning to composite keys (load_date + payer_id) which reduced Spark shuffle operations by 60% and enabled much better partition pruning.

- Incremental processing: Rewrote the extract to use CDC (change data capture) logic instead of full daily extracts, cutting source data volume from 100GB/day to ~5GB/day of actual changes.

- Query optimization: Added clustering keys to Snowflake target tables on frequently filtered columns (member_id, service_date) and rewrote several wide aggregations as incremental materialized views.

Runtime dropped from 4+ hours to 68 minutes (well under SLA), saving ~200 compute hours/month and enabling more frequent refreshes for the analytics team.​

Reliability also improved because incremental processing made the pipeline idempotent - reruns for a given date only reprocessed changed records, eliminating the risk of duplicate data from retries.

The analytics team could now run intraday utilization reports instead of waiting for EOD, which was a big win for their population health dashboards.

Memorize this 60-second version:

*"At UnitedHealth, I owned a claims pipeline running 4+ hours past SLA. I implemented composite partitioning, CDC-based incremental extracts, and Snowflake clustering - cutting runtime from 4 hours to 68 minutes while making it idempotent. Analytics team went from EOD to intraday reporting."*

At UnitedHealth Group, our nightly healthcare claims pipeline failed when a hospital partner sent a massive HL7-formatted claims file (500GB uncompressed) that overwhelmed the Spark cluster memory during parsing and transformation.

The job OOM-killed after 3 hours, blocking downstream Snowflake loads and causing intraday utilization dashboards to show stale data for 15% of our patient population.

Detection was immediate: Airflow DAG alerted on task failure + runtime exceeded 2x normal, and volume monitors flagged the oversized input file.

Immediate response (first 30 minutes):

- Marked the DAG run "degraded" and notified analytics stakeholders with exact business impact

- Scaled up EMR cluster from 10 to 30 nodes temporarily

- Split the oversized file into 10 manageable chunks using parallel S3 operations

- Reran only the failed transform task (not full pipeline) which completed in 45 minutes

Root cause and permanent fix:

- Partner was dumping 6 months backlog in one file due to their internal outage

- Implemented file size validation + auto-splitting logic in the ingestion layer

- Added memory headroom checks and dynamic cluster scaling based on input size

- Created a "large file handling" playbook for ops team

Result: Pipeline resumed normally, no data loss, dashboards refreshed by 8 AM. Analytics team regained trust through transparent communication. The auto-splitting logic caught 3 similar incidents since, preventing future failures.

60-second version to memorize:
*"Nightly claims pipeline OOM-killed on 500GB HL7 file from partner backlog. Scaled cluster, split file, reran transform task in 45 min. Added file size validation + auto-splitting. No data loss, dashboards back online by 8 AM, and logic prevents repeats."*

**3. Give an example of when you made a mistake in your data work. What did you learn?**

At Liberty Mutual, I made a critical mistake in a policy claims pipeline by applying a filter that accidentally excluded all policies from one major business line (underwriting division), causing 25% of expected claims data to vanish from downstream pricing models.

The pipeline had been running smoothly for weeks with new PySpark transformations on Databricks. One day, analytics teams reported their risk models were suddenly underpredicting premiums by millions because claims volume dropped dramatically. Data quality alerts flagged the volume anomaly, but I initially missed it while focused on other priorities.

What happened: I added a business logic filter to exclude "cancelled" policies from aggregations, but I used status == 'cancelled' instead of status != 'active' (the correct inverse logic). This excluded *all active policies* from that business line because their status field used a different enum value.

Immediate fix (Day 1):

- Rolled back the faulty transformation code via Git

- Used Databricks time travel to restore the last good claims dataset

- Reran the pipeline for affected dates, restoring all data by EOD

- Communicated exact impact and timeline to stakeholders

What I learned and changed:

- Added regression tests for every business rule - before this, we only tested row counts, not business logic outcomes

- Implemented pre-prod validation - now run sample aggregations against known good baselines before promoting to production

- Improved code review rigor - added mandatory peer review checklist including "does this filter make logical sense?"

- Better alerting - added business-level metric alerts (e.g., "claims per policy type") alongside volume alerts

Result: No lasting business impact, but it was a wake-up call. The regression tests caught 2 similar logic errors in the next 6 months before they hit production.

60-second version:
*"Filtered out 25% of claims data by mistake in a PySpark policy pipeline - wrong business logic excluded active policies. Rolled back via Git/Databricks time travel, restored data same day. Added regression tests for business rules + pre-prod validation. Caught 2 similar bugs before production since."*

**4. Tell me about a time you had to balance speed of delivery vs. data quality or compliance requirements.**

At UnitedHealth Group, leadership urgently requested a new FHIR clinical data pipeline for a regulatory quality reporting deadline 3 weeks away, but the incoming FHIR bundles from partner EHRs had inconsistent schemas and missing mandatory fields that violated our HIPAA data validation standards.

The business pressure was intense - missing the deadline risked $2M in penalties. However, pushing unvalidated PHI through production pipelines violated our SSDLC and data quality gates.

My approach to balance both:

- Week 1 (speed): Delivered a "minimum viable pipeline" - raw FHIR landing zone + basic parsing that got 85% of records through with known gaps flagged

- Week 2 (compliance): Added progressive validation layers - lenient parsing for deadline, strict validation for production publish

- Week 3 (quality): Implemented schema evolution handling and code-set mapping (LOINC/SNOMED) with quarantine for failures

Technical decisions:

- Staged rollout: Landing → Staging (lenient) → Curated (strict). Only curated data fed regulatory reports.

- Configurable validation: Toggle between "regulatory mode" (accept gaps) and "production mode" (reject gaps)

- Fallback logic: Missing fields defaulted to NULL with clear provenance tracking for audit

- Stakeholder transparency: Daily status showed acceptance rates and known gaps

Result: Hit regulatory deadline with compliant, auditable data (97% clean record rate). Production pipeline achieved 99.8% quality post-launch. Business avoided penalties while maintaining our data governance standards.

**5. ****Tell me about a time you worked closely with non-technical stakeholders (analysts, clinicians, product owners).**

At UnitedHealth Group, I partnered closely with clinical analytics analysts and a product owner to build utilization dashboards from our new claims + encounters pipeline. They needed patient-level metrics like ER visits per thousand members, but translating their clinical requirements into data models required multiple iterations.

The challenge: Analysts spoke in clinical terms ("frequency of preventable admissions") while I needed exact grain, filters, and joins. Initial mockups had wrong encounter types and missing risk adjustment.

My collaboration approach:

- Weekly 30-min requirement workshops - I brought sample data + proposed schemas, they validated business logic

- Visual mockups first - Built Tableau prototypes with dummy data so they could "see" the metrics before I built pipelines

- Data dictionary handoff - Documented every field, calculation, refresh cadence, known limitations

- Live validation sessions - After first pipeline run, walked through actual numbers together and fixed discrepancies

Specific example: They wanted "30-day readmissions," but different sources had different definitions. We settled on:

- Index admission (inpatient stay)

- Readmission within 30 days (same or different facility)

- Excluding planned procedures

I translated this into SQL joins across claims, encounters, and member eligibility tables with proper date logic and facility type filters.

Result: Delivered dashboards they adopted immediately. They went from monthly Excel reports to daily self-serve Tableau. Most importantly, clinicians trusted the metrics because we validated together.

Key takeaway: I treat analysts as the real data experts and focus on being the translator between their domain knowledge and technical implementation.

60-second version:
*"Built utilization dashboards with clinical analysts. Held weekly workshops translating 'preventable readmissions' into exact SQL joins across claims/encounters. Mocked up Tableau first, validated live data together. They went from monthly Excel to daily self-serve dashboards they trusted."*​

**6. Describe a time you had to gather ambiguous requirements and turn them into a concrete data solution.**

At Liberty Mutual, the underwriting analytics team came to me with a vague request: "We need better data for pricing models across all policy types." No specific metrics, grain, or source systems mentioned - classic ambiguous requirements.

I turned this into a concrete solution through structured discovery:

Step 1: Clarify the "why" (30-minute kickoff)

- Asked: "What business decision are you trying to improve? What are your current pain points?"

- Discovered: They needed premium-to-risk ratios by policy line, geography, and customer segment for pricing optimization

Step 2: Define the "what" (requirements workshop)

- Drew their ideal output table on whiteboard: Policy_ID, Line_of_Business, State, Customer_Segment, Premium, Claims_Count, Loss_Ratio

- Confirmed grain = policy-month

- Identified sources: policy master, claims transactions, customer demographics

Step 3: Propose the "how" (technical solution)

text

Policy_Monthly_Facts:

├── policy_snapshot (monthly)

├── LEFT JOIN claims (past 12 months lookback)

├── LEFT JOIN customer_segmentation

└── GROUP BY policy_id, month, line_of_business, state, segment

- Showed sample SQL + output schema

- Got signoff: "Yes, that's exactly what we need"

Step 4: Build + validate iteratively

- Delivered MVP with 3 policy types first

- Weekly demos showing actual numbers vs their Excel baselines

- Added remaining policy types based on feedback

Result: Delivered a policy-monthly fact table powering $50M+ pricing decisions. They went from ad-hoc Excel to self-serve queries. Most importantly, I forced clarity upfront - the 2-hour workshop saved weeks of back-and-forth.

What I learned: Ambiguous requirements hide missing shared understanding. whiteboard the output table first, confirm it solves their decision, then reverse-engineer the pipeline.

60-second version:
*"Underwriting team said 'need pricing data.' Clarified via workshop: policy-monthly facts with premiums, claims, loss ratios. Whiteboarded output table, confirmed grain/joins, built Azure pipeline. Delivered $50M+ pricing table from vague request."*

**7. ****Tell me about a time a stakeholder was unhappy with the data or deliverable. What did you do?**

At Target, the merchandising analytics team was furious when my new POS-to-inventory pipeline delivered dramatically lower sales figures than their legacy Teradata reports. They accused me of "losing data" and threatened to revert to manual extracts.

The issue: My Hive tables showed 30% fewer transactions. Stakeholders were escalating to leadership, claiming the pipeline was broken.

My response (calm diagnosis first):

- Immediate triage (Day 1): Compared source Sqoop extracts vs their Teradata queries - source data matched exactly

- Found the root cause: Their legacy reports included *test stores* (store_id < 1000) for forecasting models. My pipeline correctly filtered to production stores only (per requirements doc)

- Transparency meeting: Showed both teams the exact SQL differences side-by-side. Test stores = 28% of their inflated volume

Resolution:

- Gave them both: Production-only fact table (my pipeline) + separate test store table for their models

- Documented clearly: Every filter, exclusion, and business rule in Confluence

- Added self-serve views: sales_production_stores and sales_all_stores_including_test

Outcome: They kept my pipeline but gained flexibility. Most importantly, they learned to read the data dictionary. Pipeline became their gold standard within 2 months.

Key learning: When stakeholders reject data, it's rarely "broken" - it's usually misaligned expectations. Show your work transparently, give them options, and over-document.

**8. Describe a time you had to push back on a request that wasn’t feasible or was risky.**

At UnitedHealth Group, our analytics lead requested raw HL7 clinical messages be loaded directly into Snowflake analytical tables without validation, parsing, or standardization to "save time" for urgent regulatory reporting.

I pushed back hard because this was both technically risky and a HIPAA compliance violation:

The risks I explained:

- Data quality: Raw HL7 is messy - missing segments, inconsistent delimiters, unescaped characters would corrupt tables

- Performance: 100GB+ unparsed text blobs scanning poorly vs structured Parquet tables

- Compliance: Unvalidated PHI straight to analytics warehouse violated our data classification policy

- Downstream pain: Analysts would spend weeks cleaning in SQL instead of using curated data

My counter-proposal (feasible alternative):

text

Phase 1 (3 days): Raw HL7 landing zone in S3 + basic volume counts

Phase 2 (Week 2): Parsed staging tables with 80% field extraction  

Phase 3 (Week 3): Curated analytics tables for reporting

How I framed the conversation:

"I can get you *something* in 3 days that proves we have the data and meets audit requirements. Raw HL7 in Snowflake breaks 4 policies, kills performance, and leaves analysts with garbage. Let me deliver production-quality data by Week 3."

Outcome: They accepted phased delivery. Phase 1 satisfied auditors, Phase 3 powered their final reports. Most importantly, I established "no raw PHI in analytics" as team precedent.

Key learning: Never say "no" outright. Always offer a better path with clear tradeoffs and timelines.

60-second version:
*"Analytics wanted raw HL7 in Snowflake to save time. Pushed back - compliance risk, performance killer, analyst nightmare. Offered phased delivery: landing zone (Day 3), staging (Week 2), curated (Week 3). They accepted, set quality precedent."*​

**9. Tell me about a time you received critical feedback. How did you respond and what changed?**

At Liberty Mutual, during a quarterly pipeline review, my tech lead gave me direct feedback: "Your Airflow DAGs work but they're unmaintainable - no documentation, magic numbers everywhere, and retry logic buried in custom operators. The next engineer will hate you."

It stung because I prioritized delivery speed over writing maintainable code. He was right - I was leaving tech debt.

My immediate response:

- Thanked him sincerely: "Appreciate the candor. You're right, I've been delivery-focused at the expense of sustainability."

- Asked for specifics: "Can you walk me through one DAG and show me what you'd expect to see?"

What changed (implemented over 2 weeks):

- Documentation standard: Added READMEs to every DAG explaining purpose, inputs/outputs, SLAs, error handling

- Configuration-driven: Extracted all magic numbers/timestamps into config.yaml files

- Operator patterns: Created reusable custom operators for common patterns (retry, notify, validate)

- Code review checklist: Made documentation + config externalization mandatory for PRs

Follow-up: 3 months later, same tech lead said during 1:1: "Your DAGs are now the cleanest on the team. Others are copying your patterns."

Key learning: Critical feedback often points to blind spots. Respond with gratitude + action, not defense. Sustainable code > hero delivery.

60-second version:
*"Tech lead called my Airflow DAGs unmaintainable. Thanked him, asked for specifics. Added READMEs, config files, reusable operators, review checklist. He later said they were team-best. Learned: gratitude + action beats defensiveness."*

**10. Tell me about a time you had to balance competing priorities from multiple teams.**

At UnitedHealth Group, I was simultaneously tasked by two teams with tight deadlines: the clinical analytics team needed an urgent Snowflake table refresh for regulatory reporting (due EOD Friday), while the actuarial team needed a new claims aggregation pipeline for Monday's pricing cycle.

Both were critical path, but I only had capacity for one full implementation that week.

My prioritization approach:

- Impact assessment: Regulatory = compliance risk + $500K penalty exposure. Actuarial = business delay but no compliance risk

- Stakeholder alignment: Met with both leads Thursday morning, laid out tradeoffs: "Clinical gets Friday delivery, actuarial gets MVP Monday with full version next week"

- Technical scoping:

- Clinical: Existing pipeline + config change (2 hours work)

- Actuarial: New Spark job + testing (3 days work)

Execution:

text

Thu PM: Delivered clinical refresh (high impact, low effort)

Fri-Sun: Built actuarial MVP (basic aggregations, no partitioning)

Mon AM: Delivered MVP to actuaries with clear "v1 - full optimization next week"

Mon-Wed: Delivered production-grade actuarial pipeline

Communication throughout:

- Daily status emails: "Clinical ✅ Regulatory done. Actuarial 📈 MVP Monday, optimized Wed"

- Set realistic expectations upfront: "This sequence maximizes business value given constraints"

Result: Clinical team met deadline penalty-free. Actuaries had usable data Monday morning (despite missing advanced features). No trust lost with either team.

Key learning: Prioritize by impact × effort, communicate tradeoffs early and often, deliver partial value over perfect delays.

60-second version:
*"Clinical team needed regulatory refresh Friday, actuaries needed pricing pipeline Monday. Prioritized regulatory (compliance risk), delivered clinical Thu PM. Built actuarial MVP Sunday for Monday use, full version Wed. Both happy through clear tradeoffs + partial delivery."*

**11. Describe a time when requirements or architecture changed mid-project. How did you adapt?**

At UnitedHealth Group, midway through building a claims-to-Snowflake pipeline, leadership decided to pivot from batch processing to real-time FHIR streaming for clinical events to support intraday population health dashboards.

Original plan (Month 1): Daily Spark batch jobs from Oracle extracts → S3 → Snowflake curated tables
New requirement (Week 6): Real-time FHIR from Kafka → incremental Snowflake updates every 15 minutes

The pivot broke 70% of my existing code - batch partitioning strategies didn't work for streaming.

How I adapted:

- Quick architecture reset (Day 1): Drew new flow: Kafka → Spark Streaming → Delta Lake → Snowflake streaming

- Preserved what worked: Kept the Snowflake target schema and code-set mappings

- Parallel delivery: Ran batch pipeline in parallel while building streaming (no downtime for existing users)

- Incremental migration: Started with high-volume clinical events, phased in claims later

Technical changes:

text

OLD: Airflow → Spark batch → S3 Parquet → Snowflake COPY

NEW: Kafka → Spark Structured Streaming → Delta Lake → Snowflake MERGE

Stakeholder management:

- Clinical team: "Streaming MVP in 10 days, full production in 3 weeks"

- Batch consumers: "Your data stays reliable during transition"

Result: Delivered streaming pipeline ahead of schedule. Batch pipeline retired 2 months later with zero disruption. Dashboards went from EOD to real-time.

Key learning: When requirements pivot, identify reusable components (schemas, business logic), build in parallel, and over-communicate timelines.

60-second version:
*"Claims batch pipeline pivoted to real-time FHIR streaming mid-project. Repurposed Snowflake schema, built Kafka→Spark Streaming→Delta→Snowflake in parallel. Delivered real-time MVP in 10 days. Ran both systems seamlessly during transition."*

## Source provenance

- [Original DOCX](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Data%20Engineering/Data%20Engineering%20in%20Healthcare%20Behavioural%20Prep.docx) · Data Engineering/Data Engineering in Healthcare Behavioural Prep.docx

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
