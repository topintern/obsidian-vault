---
resume_title: "Python - Software Engineer - Splink"
kind: "resume-bank-entry"
resume_kind: "Resume"
resume_owner: "Neel-labelled"
resume_family: "Python"
resume_families: ["Python"]
resume_role: "Software Engineer"
resume_company: ""
resume_context: "Python PostgreSQL Ruby on Rails Kafka Redis Sidekiq / 6 YOE / Software Engineer / Splink"
resume_experience_labels: ["6 YOE"]
resume_source_modified: "2026-04-06"
resume_review: "unreviewed"
resume_favorite: false
resume_pdf: ["[[The Climb/Resume Bank/_Originals/57835d867f13/Neel_Gali_Resume.pdf]]"]
resume_word: []
source_paths: ["D:\\HDD F\\downloads\\CV\\Resumes\\Python\\Python PostgreSQL Ruby on Rails Kafka Redis Sidekiq\\6 YOE\\Software Engineer\\Splink\\Neel_Gali_Resume.pdf","D:\\HDD F\\downloads\\CV\\Resumes\\Python\\Python PostgreSQL Ruby on Rails Kafka Redis Sidekiq\\6 YOE\\Software Engineer\\Splink\\Neel_Gali_Resume.tex"]
source_sha256: ["57835d867f1396e1c158844b2b16213a4ff733c1e96fc20e0cf1a6e1bb99feac","0f7fe2dc46b711057e22a75e3a2bfc2b8de2f08b81e3c1a603ceadef70f5169d"]
imported: "2026-10-14"
tags: ["career/resumes"]
---

# Python - Software Engineer - Splink

[[Resume Bank]] · [[Resume Catalogue.base]] · [[Tailoring Desk]]

> [!info] Imported source version
> Content and experience labels are preserved, not independently verified. No master resume or submission approval has been assigned.

## Original files

- [[The Climb/Resume Bank/_Originals/57835d867f13/Neel_Gali_Resume.pdf|Original PDF]]

### File chooser path

After reviewing this version, copy this path into an application's file chooser when a local upload is required:

~~~text
D:\HDD F\downloads\CV\Previous Exp + Interview Prep\Obsidian Vault\The Climb\Resume Bank\_Originals\57835d867f13\Neel_Gali_Resume.pdf
~~~

## Readable content

**Neel Gali**


 Senior Software Engineer


neelgali7@gmail.com  |  +1(475)-291-1455  |  Austin, TX



## Professional Experience


**Software Engineer**  |  *Jul 2025 - Present*

*Epik Solutions | Enterprise SaaS Platform*




- Architected **Rails** RESTful API for the enterprise SaaS platform, defining data models, endpoint contracts, and **JWT** authentication that scaled to 20,000+ daily active users reliably.

- Built **Python** **FastAPI** data ingestion service with **Pydantic** schema validation and async **SQLAlchemy**, enforcing end-to-end correctness guarantees across 10,000+ daily document uploads without schema drift.

- Built **Sidekiq** background job system with priority queues, dead-letter routing, and retry logic, processing 50,000+ async tasks daily and guaranteeing at-least-once delivery on every job.

- Introduced **Apache Kafka** as the event streaming backbone for async service decoupling, enabling replay-safe data pipelines that ingested 100K+ events per minute without message loss.

- Diagnosed **N+1** query regressions and added composite **PostgreSQL** indexes with eager loading, cutting average API response time by 65% and establishing query performance baselines platform-wide.

- Authored zero-downtime **PostgreSQL** migration playbooks using the expand-contract pattern, decoupling schema changes from deploys and enabling safe column removals across the live production SaaS database.

- Deployed **Prometheus** and **Grafana** observability on Rails and Python services, tracking request throughput, error rates, and p99 latency to support on-call triage and capacity planning.



**Software Engineer**  |  *Jul 2022 - Jun 2025*

*Samay Systems LLC | B2B Compliance Platform*




- Owned backend and **data platform** for a B2B compliance SaaS, shipping product releases on schedule and serving 10,000+ enterprise users with consistent data correctness guarantees.

- Migrated 3M+ **PostgreSQL** records from a single-schema **Rails** app to per-tenant schema isolation, eliminating cross-tenant data leakage and satisfying all enterprise **SOC 2** compliance requirements.

- Built **Python** **Celery** task queue with **Redis** broker, priority lanes, and dead-letter retries, processing 200K+ daily background jobs with durable delivery and observable failure recovery.

- Designed idempotent Python task handlers with **Redis** deduplication keys, guaranteeing exactly-once **Celery** job processing under retries and eliminating duplicate compliance record writes on worker restarts.

- Refactored compliance services from synchronous **Python** to **asyncio** with **httpx**, enabling concurrent third-party regulatory API calls and cutting external validation round-trip latency by 55 percent.

- Integrated **Elasticsearch** on the compliance data platform, indexing 5M+ regulatory documents and reducing document lookup latency from 8 seconds to under 300ms for compliance officers.

- Introduced **Redis** caching for compliance lookups and **Rails** sessions, reducing **PostgreSQL** read load by 60% and cutting API response time by 45% at peak traffic.

- Introduced **LaunchDarkly** feature flags to decouple backend feature rollouts from deploys, enabling dark launches of compliance features and reducing production incidents caused by big-bang integrations.

- Deployed **Rails** to **AWS EKS** with **Docker** and **Kubernetes**, configuring rolling deployments, autoscaling, and health checks that maintained 99.9% uptime across all compliance platform services.



**Software Engineer**  |  *Jul 2020 - Aug 2022*

*Zemoso Technologies | LabOps Platform*




- Built **Ruby on Rails** features from scratch for a LabOps SaaS, authoring CRUD interfaces, REST endpoints, and **ActiveRecord** models for multi-step laboratory sample processing workflows.

- Built **Python** **pandas** transformation pipelines for lab reporting, processing 500K+ monthly records with automated QC rules and cutting researcher manual data preparation time by 50%.

- Built **Python** ETL jobs exporting lab datasets to **AWS S3** as **Parquet** files, enabling downstream analytics and cutting ad-hoc production **PostgreSQL** query load by 40%.

- Authored optimized **PostgreSQL** queries and **ActiveRecord** scopes for lab sample tracking, reducing report generation time by 30% through targeted index tuning and query planning improvements.

- Configured **GitHub Actions** CI/CD for Rails and Python services, running **RSpec**, **pytest**, and **Rubocop** on every PR and automating **Heroku** staging deployments for continuous releasability.




## Skills


**Languages**: Ruby, Python, SQL, JavaScript, TypeScript, Bash

**Frameworks & Tools**: Ruby on Rails, FastAPI, Pydantic, SQLAlchemy, pandas, asyncio, httpx, Sidekiq, Celery, Kafka, LaunchDarkly, RSpec, pytest, Rubocop

**Cloud & Infra**: AWS, Azure, Redis, Elasticsearch, Docker, Kubernetes, GitHub Actions, Prometheus, Grafana

**Concepts**: REST, JWT, OAuth2, RBAC, multi-tenancy, event streaming, idempotency, exactly-once delivery, feature flags, zero-downtime migrations, data correctness, observability, CI/CD


## Education


**Master's in Computer Science**, Oklahoma State University, Stillwater

**Bachelor's in Computer Science**, JNTU Hyderabad, India

> [!example]- Text from the original PDF — preserved separately
> Neel Gali
> 
>                                     Senior Software Engineer
> 
>                                         neelgali7@gmail.com | +1(475)-291-1455 | Austin, TX
> 
> Professional Experience
> 
> Software Engineer                                                                                Jul 2025 - Present
> 
> Epik Solutions | Enterprise SaaS Platform
> 
> • Architected Rails RESTful API for the enterprise SaaS platform, defining data models, endpoint contracts, and
> 
> JWT authentication that scaled to 20,000+ daily active users reliably.
> 
> • Built Python FastAPI data ingestion service with Pydantic schema validation and async SQLAlchemy, enforcing
> 
> end-to-end correctness guarantees across 10,000+ daily document uploads without schema drift.
> 
> • Built Sidekiq background job system with priority queues, dead-letter routing, and retry logic, processing 50,000+
> 
> async tasks daily and guaranteeing at-least-once delivery on every job.
> 
> • Introduced Apache Kaf ka as the event streaming backbone for async service decoupling, enabling replay-safe data
> 
> pipelines that ingested 100K+ events per minute without message loss.
> 
> • Diagnosed N+1 query regressions and added composite PostgreSQL indexes with eager loading, cutting average
> 
> API response time by 65% and establishing query performance baselines platform-wide.
> 
> • Authored zero-downtime PostgreSQL migration playbooks using the expand-contract pattern, decoupling schema
> 
> changes from deploys and enabling safe column removals across the live production SaaS database.
> 
> • Deployed Prometheus and Grafana observability on Rails and Python services, tracking request throughput, error
> 
> rates, and p99 latency to support on-call triage and capacity planning.
> 
> Software Engineer                                                                            Jul 2022 - Jun 2025
> 
> Samay Systems LLC | B2B Compliance Platform
> 
> • Owned backend and data platform for a B2B compliance SaaS, shipping product releases on schedule and serving
> 
> 10,000+ enterprise users with consistent data correctness guarantees.
> 
> • Migrated 3M+ PostgreSQL records from a single-schema Rails app to per-tenant schema isolation, eliminating
> 
> cross-tenant data leakage and satisfying all enterprise SOC 2 compliance requirements.
> 
> • Built Python Celery task queue with Redis broker, priority lanes, and dead-letter retries, processing 200K+ daily
> 
> background jobs with durable delivery and observable failure recovery.
> 
> • Designed idempotent Python task handlers with Redis deduplication keys, guaranteeing exactly-once Celery job
> 
> processing under retries and eliminating duplicate compliance record writes on worker restarts.
> 
> • Refactored compliance services from synchronous Python to asyncio with httpx, enabling concurrent third-party
> 
> regulatory API calls and cutting external validation round-trip latency by 55 percent.
> 
> • Integrated Elasticsearch on the compliance data platform, indexing 5M+ regulatory documents and reducing
> 
> document lookup latency from 8 seconds to under 300ms for compliance officers.
> 
> • Introduced Redis caching for compliance lookups and Rails sessions, reducing PostgreSQL read load by 60% and
> 
> cutting API response time by 45% at peak traffic.
> 
> • Introduced LaunchDarkly feature flags to decouple backend feature rollouts from deploys, enabling dark launches
> 
> of compliance features and reducing production incidents caused by big-bang integrations.
> 
> • Deployed Rails to AWS EKS with Docker and Kubernetes, configuring rolling deployments, autoscaling, and
> 
> health checks that maintained 99.9% uptime across all compliance platform services.
> 
> Software Engineer                                                                            Jul 2020 - Aug 2022
> 
> Zemoso Technologies | LabOps Platform
> 
> • Built Ruby on Rails features from scratch for a LabOps SaaS, authoring CRUD interfaces, REST endpoints, and
> 
> ActiveRecord models for multi-step laboratory sample processing workflows.
> 
> • Built Python pandas transformation pipelines for lab reporting, processing 500K+ monthly records with
> 
> automated QC rules and cutting researcher manual data preparation time by 50%.
> 
> • Built Python ETL jobs exporting lab datasets to AWS S3 as Parquet files, enabling downstream analytics and
> 
> cutting ad-hoc production PostgreSQL query load by 40%.
> 
> • Authored optimized PostgreSQL queries and ActiveRecord scopes for lab sample tracking, reducing report
> 
> generation time by 30% through targeted index tuning and query planning improvements.
> 
> • Configured GitHub Actions CI/CD for Rails and Python services, running RSpec, pytest, and Rubocop on every
> 
> PR and automating Heroku staging deployments for continuous releasability.
> 
> Skills
> 
> Languages: Ruby, Python, SQL, JavaScript, TypeScript, Bash
> Frameworks & Tools: Ruby on Rails, FastAPI, Pydantic, SQLAlchemy, pandas, asyncio, httpx, Sidekiq, Celery, Kafka,
> LaunchDarkly, RSpec, pytest, Rubocop
> Cloud & Infra: AWS, Azure, Redis, Elasticsearch, Docker, Kubernetes, GitHub Actions, Prometheus, Grafana
> Concepts: REST, JWT, OAuth2, RBAC, multi-tenancy, event streaming, idempotency, exactly-once delivery, feature
> flags, zero-downtime migrations, data correctness, observability, CI/CD
> 
> Education
> 
> Master’s in Computer Science, Oklahoma State University, Stillwater
> Bachelor’s in Computer Science, JNTU Hyderabad, India

> [!example]- Exact LaTeX source — archived, never executed
> ~~~~latex
> \documentclass[10pt]{article}
> \raggedbottom
> \flushbottom
> \usepackage[a4paper, top=0.5in, bottom=0.35in, left=0.6in, right=0.6in]{geometry}
> \usepackage{verbatim}
> \usepackage{XCharter}
> \usepackage[T1]{fontenc}
> \usepackage[utf8]{inputenc}
> \usepackage{enumitem}
> \usepackage[hidelinks]{hyperref}
> \usepackage{titlesec}
> \raggedright
> \setlength{\parskip}{0pt}
> \setlength{\parindent}{0pt}
> \pagestyle{empty}
> \input{glyphtounicode}
> \pdfgentounicode=1
> \titleformat{\section}{\bfseries\large}{}{0pt}{}[\titlerule]
> \renewcommand\labelitemi{$\vcenter{\hbox{\small$\bullet$}}$}
> \setlist[itemize]{itemsep=0pt, topsep=1pt, parsep=0pt, partopsep=0pt, leftmargin=12pt}
> \titlespacing*{\section}{0pt}{3pt}{2pt}
> \begin{document}
> \centerline{\Huge \textbf{Neel Gali}}
> \vspace{5pt}
> \centerline{\Large Senior Software Engineer}
> \vspace{1pt}
> \centerline{neelgali7@gmail.com  |  +1(475)-291-1455  |  Austin, TX}
> \vspace{-4pt}
> \section*{Professional Experience}
> \textbf{Software Engineer} \hfill \textit{Jul 2025 - Present} \\
> \textit{Epik Solutions | Enterprise SaaS Platform} \\
> \begin{itemize}
> \item Architected \textbf{Rails} RESTful API for the enterprise SaaS platform, defining data models, endpoint contracts, and \textbf{JWT} authentication that scaled to 20,000+ daily active users reliably.
> \item Built \textbf{Python} \textbf{FastAPI} data ingestion service with \textbf{Pydantic} schema validation and async \textbf{SQLAlchemy}, enforcing end-to-end correctness guarantees across 10,000+ daily document uploads without schema drift.
> \item Built \textbf{Sidekiq} background job system with priority queues, dead-letter routing, and retry logic, processing 50,000+ async tasks daily and guaranteeing at-least-once delivery on every job.
> \item Introduced \textbf{Apache Kafka} as the event streaming backbone for async service decoupling, enabling replay-safe data pipelines that ingested 100K+ events per minute without message loss.
> \item Diagnosed \textbf{N+1} query regressions and added composite \textbf{PostgreSQL} indexes with eager loading, cutting average API response time by 65\% and establishing query performance baselines platform-wide.
> \item Authored zero-downtime \textbf{PostgreSQL} migration playbooks using the expand-contract pattern, decoupling schema changes from deploys and enabling safe column removals across the live production SaaS database.
> \item Deployed \textbf{Prometheus} and \textbf{Grafana} observability on Rails and Python services, tracking request throughput, error rates, and p99 latency to support on-call triage and capacity planning.
> \end{itemize}
> 
> \textbf{Software Engineer} \hfill \textit{Jul 2022 - Jun 2025} \\
> \textit{Samay Systems LLC | B2B Compliance Platform} \\
> \begin{itemize}
> \item Owned backend and \textbf{data platform} for a B2B compliance SaaS, shipping product releases on schedule and serving 10,000+ enterprise users with consistent data correctness guarantees.
> \item Migrated 3M+ \textbf{PostgreSQL} records from a single-schema \textbf{Rails} app to per-tenant schema isolation, eliminating cross-tenant data leakage and satisfying all enterprise \textbf{SOC 2} compliance requirements.
> \item Built \textbf{Python} \textbf{Celery} task queue with \textbf{Redis} broker, priority lanes, and dead-letter retries, processing 200K+ daily background jobs with durable delivery and observable failure recovery.
> \item Designed idempotent Python task handlers with \textbf{Redis} deduplication keys, guaranteeing exactly-once \textbf{Celery} job processing under retries and eliminating duplicate compliance record writes on worker restarts.
> \item Refactored compliance services from synchronous \textbf{Python} to \textbf{asyncio} with \textbf{httpx}, enabling concurrent third-party regulatory API calls and cutting external validation round-trip latency by 55 percent.
> \item Integrated \textbf{Elasticsearch} on the compliance data platform, indexing 5M+ regulatory documents and reducing document lookup latency from 8 seconds to under 300ms for compliance officers.
> \item Introduced \textbf{Redis} caching for compliance lookups and \textbf{Rails} sessions, reducing \textbf{PostgreSQL} read load by 60\% and cutting API response time by 45\% at peak traffic.
> \item Introduced \textbf{LaunchDarkly} feature flags to decouple backend feature rollouts from deploys, enabling dark launches of compliance features and reducing production incidents caused by big-bang integrations.
> \item Deployed \textbf{Rails} to \textbf{AWS EKS} with \textbf{Docker} and \textbf{Kubernetes}, configuring rolling deployments, autoscaling, and health checks that maintained 99.9\% uptime across all compliance platform services.
> \end{itemize}
> 
> \textbf{Software Engineer} \hfill \textit{Jul 2020 - Aug 2022} \\
> \textit{Zemoso Technologies | LabOps Platform} \\
> \begin{itemize}
> \item Built \textbf{Ruby on Rails} features from scratch for a LabOps SaaS, authoring CRUD interfaces, REST endpoints, and \textbf{ActiveRecord} models for multi-step laboratory sample processing workflows.
> \item Built \textbf{Python} \textbf{pandas} transformation pipelines for lab reporting, processing 500K+ monthly records with automated QC rules and cutting researcher manual data preparation time by 50\%.
> \item Built \textbf{Python} ETL jobs exporting lab datasets to \textbf{AWS S3} as \textbf{Parquet} files, enabling downstream analytics and cutting ad-hoc production \textbf{PostgreSQL} query load by 40\%.
> \item Authored optimized \textbf{PostgreSQL} queries and \textbf{ActiveRecord} scopes for lab sample tracking, reducing report generation time by 30\% through targeted index tuning and query planning improvements.
> \item Configured \textbf{GitHub Actions} CI/CD for Rails and Python services, running \textbf{RSpec}, \textbf{pytest}, and \textbf{Rubocop} on every PR and automating \textbf{Heroku} staging deployments for continuous releasability.
> \end{itemize}
> 
> \section*{Skills}
> \textbf{Languages}: Ruby, Python, SQL, JavaScript, TypeScript, Bash \\
> \textbf{Frameworks \& Tools}: Ruby on Rails, FastAPI, Pydantic, SQLAlchemy, pandas, asyncio, httpx, Sidekiq, Celery, Kafka, LaunchDarkly, RSpec, pytest, Rubocop \\
> \textbf{Cloud \& Infra}: AWS, Azure, Redis, Elasticsearch, Docker, Kubernetes, GitHub Actions, Prometheus, Grafana \\
> \textbf{Concepts}: REST, JWT, OAuth2, RBAC, multi-tenancy, event streaming, idempotency, exactly-once delivery, feature flags, zero-downtime migrations, data correctness, observability, CI/CD \\
> \section*{Education}
> \textbf{Master's in Computer Science}, Oklahoma State University, Stillwater \\
> \textbf{Bachelor's in Computer Science}, JNTU Hyderabad, India \\
> \end{document}
> 
> ~~~~

## Source provenance

Source modification date is filesystem metadata, not a verified authorship date. This is a one-time import snapshot; later external edits are not automatically synced.

- [Python / Python PostgreSQL Ruby on Rails Kafka Redis Sidekiq / 6 YOE / Software Engineer / Splink / Neel_Gali_Resume.pdf](file:///D:/HDD%20F/downloads/CV/Resumes/Python/Python%20PostgreSQL%20Ruby%20on%20Rails%20Kafka%20Redis%20Sidekiq/6%20YOE/Software%20Engineer/Splink/Neel_Gali_Resume.pdf)
- [Python / Python PostgreSQL Ruby on Rails Kafka Redis Sidekiq / 6 YOE / Software Engineer / Splink / Neel_Gali_Resume.tex](file:///D:/HDD%20F/downloads/CV/Resumes/Python/Python%20PostgreSQL%20Ruby%20on%20Rails%20Kafka%20Redis%20Sidekiq/6%20YOE/Software%20Engineer/Splink/Neel_Gali_Resume.tex)

For claim checks, consult [[Claims to Reconcile]] and supporting experience evidence before tailoring.
