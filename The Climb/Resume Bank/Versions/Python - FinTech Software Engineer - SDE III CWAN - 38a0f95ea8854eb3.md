---
resume_title: "Python - FinTech Software Engineer - SDE III CWAN"
kind: "resume-bank-entry"
resume_kind: "Resume"
resume_owner: "Neel-labelled"
resume_family: "Python"
resume_families: ["Python"]
resume_role: "FinTech Software Engineer"
resume_company: ""
resume_context: "Python Kafka TimescaleDB PostgreSQL Market Data Ingestion Redis / 6 YOE / FinTech Software Engineer / SDE III CWAN"
resume_experience_labels: ["6 YOE"]
resume_source_modified: "2026-04-03"
resume_review: "unreviewed"
resume_favorite: false
resume_pdf: ["[[The Climb/Resume Bank/_Originals/85996336a5ad/Neel_Gali_Resume.pdf]]"]
resume_word: []
source_paths: ["D:\\HDD F\\downloads\\CV\\Resumes\\Python\\Python Kafka TimescaleDB PostgreSQL Market Data Ingestion Redis\\6 YOE\\FinTech Software Engineer\\SDE III CWAN\\Neel_Gali_Resume.pdf","D:\\HDD F\\downloads\\CV\\Resumes\\Python\\Python Kafka TimescaleDB PostgreSQL Market Data Ingestion Redis\\6 YOE\\FinTech Software Engineer\\SDE III CWAN\\Neel_Gali_Resume.tex"]
source_sha256: ["85996336a5ad0a8df3f96a0d85df7db1aea12a198c9eea1a9edc62af489ba505","5f75e699da97cc12cc3a047aa7ed3ea8df2bf56b5a5c84bcbab15551e7201456"]
imported: "2026-10-14"
tags: ["career/resumes"]
---

# Python - FinTech Software Engineer - SDE III CWAN

[[Resume Bank]] · [[Resume Catalogue.base]] · [[Tailoring Desk]]

> [!info] Imported source version
> Content and experience labels are preserved, not independently verified. No master resume or submission approval has been assigned.

## Original files

- [[The Climb/Resume Bank/_Originals/85996336a5ad/Neel_Gali_Resume.pdf|Original PDF]]

### File chooser path

After reviewing this version, copy this path into an application's file chooser when a local upload is required:

~~~text
D:\HDD F\downloads\CV\Previous Exp + Interview Prep\Obsidian Vault\The Climb\Resume Bank\_Originals\85996336a5ad\Neel_Gali_Resume.pdf
~~~

## Readable content

**Neel Gali**


 Software Engineer


neelgali7@gmail.com  |  +1(475)-291-1455  |  Austin, TX



## Professional Experience


**Software Engineer**  |  *Jul 2025 - Present*

*Epik Solutions | Enterprise FinTech Platform*




- Built a **Python** market data ingestion framework handling real-time equity, futures, and options tick feeds; normalized 15+ instrument streams with configurable deduplication and alerting thresholds.

- Built **Python** time series framework using **TimescaleDB** for high-frequency OHLCV storage, delivering sub-10ms query response across 3 years of historical market data for 20+ instruments.

- Engineered **Python** trade ingestion microservices processing 50K+ high-frequency trade events per second over **Kafka**, with idempotent handlers, configurable dead-letter queues, and full audit trail persistence.

- Developed **Python** adapters integrating three external market data vendor APIs with retry logic, circuit breakers, and vendor-specific protocol normalization into the Beacon platform ingestion pipeline.

- Extended the platform application framework with a **Python** plugin system, letting engineers register custom data processors and schedule jobs without modifying core platform configuration files.

- Built **pandas** and **NumPy** financial analytics modules computing rolling VWAP, momentum signals, and volatility metrics, feeding enriched instrument data into the Beacon platform real-time dashboard.

- Implemented **Python** order book reconstruction from Level 2 market data feeds using min-heap priority queue, enabling sub-millisecond best bid/offer spread calculation for 50+ equity instruments.

- Enforced **Pydantic** data contract schemas across all ingestion pipeline message types, automatically rejecting malformed upstream payloads before they reached downstream time series or analytics storage.



**Software Engineer**  |  *Jul 2022 - Jun 2025*

*Samay Systems LLC | B2B Data & Compliance Platform*




- Built **Python** ETL pipelines on **AWS Lambda** and **S3** processing 10M+ daily compliance records, reducing data ingestion lag from 4 hours to under 20 minutes.

- Architected **Kafka** event streaming for real-time compliance data sync across six microservices, layering **Redis** caching that cut downstream API latency by 65% at peak load.

- Designed **PostgreSQL** relational schemas and **MongoDB** document collections for a dual-store compliance system, tuning each to its query patterns and cutting ORM overhead by 40%.

- Integrated seven third-party compliance data providers via REST and SFTP adapters in **Python**, building idempotent reconciliation logic that detected and resolved cross-system data discrepancies automatically.

- Tuned **Python** data pipeline throughput using connection pooling, batched writes, and async I/O, sustaining 3x data volume growth with zero additional infrastructure or latency degradation.

- Deployed and maintained **FastAPI** REST services on **Azure** for compliance report delivery, integrating **Azure Blob Storage** to archive processed data exports with tenant-scoped access controls.

- Implemented **PostgreSQL** date-range partitioning on 500M+ compliance event records, cutting query scan costs by 70% and enabling automated partition pruning for regulatory data retention policies.



**Software Engineer**  |  *Jul 2020 - Aug 2022*

*Zemoso Technologies | LabOps Platform*




- Developed **Python** REST APIs for a LabOps platform, leveraging priority queues and graph algorithms for sample processing workflows, reducing average API response times by 35%.

- Authored optimized **PostgreSQL** queries and stored procedures for lab sample tracking, reducing report generation time by 30% through strategic index tuning and targeted query denormalization.

- Developed **Java Spring Boot** microservices alongside **Python** services in a multi-language stack, maintaining 75%+ test coverage with JUnit and pytest across all platform service boundaries.

- Containerized **Python** microservices using **Docker** and provisioned cloud environments through **Terraform**, enabling local development setups and reducing new-developer onboarding and configuration time by 60%.

- Refactored **Python** ingestion jobs to async I/O using **asyncio**, reducing per-batch processing time by 55% and supporting concurrent polling across multiple upstream data sources simultaneously.

- Configured **GitHub Actions** CI/CD pipelines for Python and Java services, automating unit test execution, Docker image builds, and staging environment deployments on every pull request.




## Skills


**Languages**: Python, Java, SQL, JavaScript, Bash

**Data & Streaming**: Kafka, Redis, ETL pipelines, pandas, NumPy, market data ingestion, time series (TimescaleDB, OHLCV), HFT trade ingestion, event-driven architecture

**Databases**: PostgreSQL, MongoDB, TimescaleDB

**Cloud & Infra**: AWS (Lambda, S3), Azure (App Service, Blob Storage), Docker, Terraform

**Frameworks & Tools**: FastAPI, Pydantic, Spring Boot, asyncio, REST APIs, microservices, CI/CD, pytest, JUnit


## Education


**Master's in Computer Science**, Oklahoma State University, Stillwater

**Bachelor's in Computer Science**, JNTU Hyderabad, India

> [!example]- Text from the original PDF — preserved separately
> Neel Gali
> 
>                                          Software Engineer
> 
>                                         neelgali7@gmail.com | +1(475)-291-1455 | Austin, TX
> 
> Professional Experience
> 
> Software Engineer                                                                             Jul 2025 - Present
> 
> Epik Solutions | Enterprise FinTech Platform
> 
> • Built a Python market data ingestion framework handling real-time equity, futures, and options tick feeds;
> 
> normalized 15+ instrument streams with configurable deduplication and alerting thresholds.
> 
> • Built Python time series framework using TimescaleDB for high-frequency OHLCV storage, delivering sub-10ms
> 
> query response across 3 years of historical market data for 20+ instruments.
> 
> • Engineered Python trade ingestion microservices processing 50K+ high-frequency trade events per second over
> 
> Kaf ka, with idempotent handlers, configurable dead-letter queues, and full audit trail persistence.
> 
> • Developed Python adapters integrating three external market data vendor APIs with retry logic, circuit breakers,
> 
> and vendor-specific protocol normalization into the Beacon platform ingestion pipeline.
> 
> • Extended the platform application framework with a Python plugin system, letting engineers register custom data
> 
> processors and schedule jobs without modifying core platform configuration files.
> 
> • Built pandas and NumPy financial analytics modules computing rolling VWAP, momentum signals, and volatility
> 
> metrics, feeding enriched instrument data into the Beacon platform real-time dashboard.
> 
> • Implemented Python order book reconstruction from Level 2 market data feeds using min-heap priority queue,
> 
> enabling sub-millisecond best bid/offer spread calculation for 50+ equity instruments.
> 
> • Enforced Pydantic data contract schemas across all ingestion pipeline message types, automatically rejecting
> 
> malformed upstream payloads before they reached downstream time series or analytics storage.
> 
> Software Engineer                                                                            Jul 2022 - Jun 2025
> 
> Samay Systems LLC | B2B Data & Compliance Platform
> 
> • Built Python ETL pipelines on AWS Lambda and S3 processing 10M+ daily compliance records, reducing data
> 
> ingestion lag from 4 hours to under 20 minutes.
> 
> • Architected Kaf ka event streaming for real-time compliance data sync across six microservices, layering Redis
> 
> caching that cut downstream API latency by 65% at peak load.
> 
> • Designed PostgreSQL relational schemas and MongoDB document collections for a dual-store compliance system,
> 
> tuning each to its query patterns and cutting ORM overhead by 40%.
> 
> • Integrated seven third-party compliance data providers via REST and SFTP adapters in Python, building
> 
> idempotent reconciliation logic that detected and resolved cross-system data discrepancies automatically.
> 
> • Tuned Python data pipeline throughput using connection pooling, batched writes, and async I/O, sustaining 3x
> 
> data volume growth with zero additional infrastructure or latency degradation.
> 
> • Deployed and maintained FastAPI REST services on Azure for compliance report delivery, integrating Azure Blob
> 
> Storage to archive processed data exports with tenant-scoped access controls.
> 
> • Implemented PostgreSQL date-range partitioning on 500M+ compliance event records, cutting query scan costs
> 
> by 70% and enabling automated partition pruning for regulatory data retention policies.
> 
> Software Engineer                                                                            Jul 2020 - Aug 2022
> 
> Zemoso Technologies | LabOps Platform
> 
> • Developed Python REST APIs for a LabOps platform, leveraging priority queues and graph algorithms for sample
> 
> processing workflows, reducing average API response times by 35%.
> 
> • Authored optimized PostgreSQL queries and stored procedures for lab sample tracking, reducing report generation
> 
> time by 30% through strategic index tuning and targeted query denormalization.
> 
> • Developed Java Spring Boot microservices alongside Python services in a multi-language stack, maintaining
> 
> 75%+ test coverage with JUnit and pytest across all platform service boundaries.
> 
> • Containerized Python microservices using Docker and provisioned cloud environments through Terraform,
> 
> enabling local development setups and reducing new-developer onboarding and configuration time by 60%.
> 
> • Refactored Python ingestion jobs to async I/O using asyncio, reducing per-batch processing time by 55% and
> 
> supporting concurrent polling across multiple upstream data sources simultaneously.
> 
> Skills
> 
> Languages: Python, Java, SQL, JavaScript, Bash
> Data & Streaming: Kafka, Redis, ETL pipelines, pandas, NumPy, market data ingestion, time series (TimescaleDB,
> OHLCV), HFT trade ingestion
> Databases: PostgreSQL, MongoDB, TimescaleDB
> Cloud & Infra: AWS (Lambda, S3), Azure (App Service, Blob Storage), Docker, Terraform
> Frameworks & Tools: FastAPI, Pydantic, Spring Boot, asyncio, pytest, JUnit, GitHub Actions
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
> \centerline{\Large Software Engineer}
> \vspace{1pt}
> \centerline{neelgali7@gmail.com  |  +1(475)-291-1455  |  Austin, TX}
> \vspace{-4pt}
> \section*{Professional Experience}
> \textbf{Software Engineer} \hfill \textit{Jul 2025 - Present} \\
> \textit{Epik Solutions | Enterprise FinTech Platform} \\
> \begin{itemize}
> \item Built a \textbf{Python} market data ingestion framework handling real-time equity, futures, and options tick feeds; normalized 15+ instrument streams with configurable deduplication and alerting thresholds.
> \item Built \textbf{Python} time series framework using \textbf{TimescaleDB} for high-frequency OHLCV storage, delivering sub-10ms query response across 3 years of historical market data for 20+ instruments.
> \item Engineered \textbf{Python} trade ingestion microservices processing 50K+ high-frequency trade events per second over \textbf{Kafka}, with idempotent handlers, configurable dead-letter queues, and full audit trail persistence.
> \item Developed \textbf{Python} adapters integrating three external market data vendor APIs with retry logic, circuit breakers, and vendor-specific protocol normalization into the Beacon platform ingestion pipeline.
> \item Extended the platform application framework with a \textbf{Python} plugin system, letting engineers register custom data processors and schedule jobs without modifying core platform configuration files.
> \item Built \textbf{pandas} and \textbf{NumPy} financial analytics modules computing rolling VWAP, momentum signals, and volatility metrics, feeding enriched instrument data into the Beacon platform real-time dashboard.
> \item Implemented \textbf{Python} order book reconstruction from Level 2 market data feeds using min-heap priority queue, enabling sub-millisecond best bid/offer spread calculation for 50+ equity instruments.
> \item Enforced \textbf{Pydantic} data contract schemas across all ingestion pipeline message types, automatically rejecting malformed upstream payloads before they reached downstream time series or analytics storage.
> \end{itemize}
> 
> \textbf{Software Engineer} \hfill \textit{Jul 2022 - Jun 2025} \\
> \textit{Samay Systems LLC | B2B Data \& Compliance Platform} \\
> \begin{itemize}
> \item Built \textbf{Python} ETL pipelines on \textbf{AWS Lambda} and \textbf{S3} processing 10M+ daily compliance records, reducing data ingestion lag from 4 hours to under 20 minutes.
> \item Architected \textbf{Kafka} event streaming for real-time compliance data sync across six microservices, layering \textbf{Redis} caching that cut downstream API latency by 65\% at peak load.
> \item Designed \textbf{PostgreSQL} relational schemas and \textbf{MongoDB} document collections for a dual-store compliance system, tuning each to its query patterns and cutting ORM overhead by 40\%.
> \item Integrated seven third-party compliance data providers via REST and SFTP adapters in \textbf{Python}, building idempotent reconciliation logic that detected and resolved cross-system data discrepancies automatically.
> \item Tuned \textbf{Python} data pipeline throughput using connection pooling, batched writes, and async I/O, sustaining 3x data volume growth with zero additional infrastructure or latency degradation.
> \item Deployed and maintained \textbf{FastAPI} REST services on \textbf{Azure} for compliance report delivery, integrating \textbf{Azure Blob Storage} to archive processed data exports with tenant-scoped access controls.
> \item Implemented \textbf{PostgreSQL} date-range partitioning on 500M+ compliance event records, cutting query scan costs by 70\% and enabling automated partition pruning for regulatory data retention policies.
> \end{itemize}
> 
> \textbf{Software Engineer} \hfill \textit{Jul 2020 - Aug 2022} \\
> \textit{Zemoso Technologies | LabOps Platform} \\
> \begin{itemize}
> \item Developed \textbf{Python} REST APIs for a LabOps platform, leveraging priority queues and graph algorithms for sample processing workflows, reducing average API response times by 35\%.
> \item Authored optimized \textbf{PostgreSQL} queries and stored procedures for lab sample tracking, reducing report generation time by 30\% through strategic index tuning and targeted query denormalization.
> \item Developed \textbf{Java Spring Boot} microservices alongside \textbf{Python} services in a multi-language stack, maintaining 75\%+ test coverage with JUnit and pytest across all platform service boundaries.
> \item Containerized \textbf{Python} microservices using \textbf{Docker} and provisioned cloud environments through \textbf{Terraform}, enabling local development setups and reducing new-developer onboarding and configuration time by 60\%.
> \item Refactored \textbf{Python} ingestion jobs to async I/O using \textbf{asyncio}, reducing per-batch processing time by 55\% and supporting concurrent polling across multiple upstream data sources simultaneously.
> \item Configured \textbf{GitHub Actions} CI/CD pipelines for Python and Java services, automating unit test execution, Docker image builds, and staging environment deployments on every pull request.
> \end{itemize}
> 
> \section*{Skills}
> \textbf{Languages}: Python, Java, SQL, JavaScript, Bash \\
> \textbf{Data \& Streaming}: Kafka, Redis, ETL pipelines, pandas, NumPy, market data ingestion, time series (TimescaleDB, OHLCV), HFT trade ingestion, event-driven architecture \\
> \textbf{Databases}: PostgreSQL, MongoDB, TimescaleDB \\
> \textbf{Cloud \& Infra}: AWS (Lambda, S3), Azure (App Service, Blob Storage), Docker, Terraform \\
> \textbf{Frameworks \& Tools}: FastAPI, Pydantic, Spring Boot, asyncio, REST APIs, microservices, CI/CD, pytest, JUnit \\
> \section*{Education}
> \textbf{Master's in Computer Science}, Oklahoma State University, Stillwater \\
> \textbf{Bachelor's in Computer Science}, JNTU Hyderabad, India \\
> \end{document}
> 
> ~~~~

## Source provenance

Source modification date is filesystem metadata, not a verified authorship date. This is a one-time import snapshot; later external edits are not automatically synced.

- [Python / Python Kafka TimescaleDB PostgreSQL Market Data Ingestion Redis / 6 YOE / FinTech Software Engineer / SDE III CWAN / Neel_Gali_Resume.pdf](file:///D:/HDD%20F/downloads/CV/Resumes/Python/Python%20Kafka%20TimescaleDB%20PostgreSQL%20Market%20Data%20Ingestion%20Redis/6%20YOE/FinTech%20Software%20Engineer/SDE%20III%20CWAN/Neel_Gali_Resume.pdf)
- [Python / Python Kafka TimescaleDB PostgreSQL Market Data Ingestion Redis / 6 YOE / FinTech Software Engineer / SDE III CWAN / Neel_Gali_Resume.tex](file:///D:/HDD%20F/downloads/CV/Resumes/Python/Python%20Kafka%20TimescaleDB%20PostgreSQL%20Market%20Data%20Ingestion%20Redis/6%20YOE/FinTech%20Software%20Engineer/SDE%20III%20CWAN/Neel_Gali_Resume.tex)

For claim checks, consult [[Claims to Reconcile]] and supporting experience evidence before tailoring.
