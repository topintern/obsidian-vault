---
resume_title: "Golang - Full Stack AI Engineer - Ice Capital richard krause"
kind: "resume-bank-entry"
resume_kind: "Resume"
resume_owner: "Neel-labelled"
resume_family: "Golang"
resume_families: ["Golang"]
resume_role: "Full Stack AI Engineer"
resume_company: ""
resume_context: "Go Python React Snowflake Apache Airflow Azure OpenAI / 6 YOE / Full Stack AI Engineer / Ice Capital richard krause"
resume_experience_labels: ["6 YOE"]
resume_source_modified: "2026-03-26"
resume_review: "unreviewed"
resume_favorite: false
resume_pdf: []
resume_word: []
source_paths: ["D:\\HDD F\\downloads\\CV\\Resumes\\Golang\\Go Python React Snowflake Apache Airflow Azure OpenAI\\6 YOE\\Full Stack AI Engineer\\Ice Capital richard krause\\Neel_Gali_Resume_Senior_Full_Stack_AI_Engineer.tex"]
source_sha256: ["04398d7aa86e981d8b7cb6cba9b7257a772ff49c805795a95d0334f8608a244a"]
imported: "2026-10-14"
tags: ["career/resumes"]
---

# Golang - Full Stack AI Engineer - Ice Capital richard krause

[[Resume Bank]] · [[Resume Catalogue.base]] · [[Tailoring Desk]]

> [!info] Imported source version
> Content and experience labels are preserved, not independently verified. No master resume or submission approval has been assigned.

## Original files

No PDF or Word document accompanies this source. The external source is preserved below; no upload-ready document was generated.

## Readable content

**Neel Gali**

 Full Stack Engineer

neelgali7@gmail.com  |  +1(475)-291-1455  |  Austin, TX | [linkedin.com/in/neelgali](https://linkedin.com/in/neelgali)

## Professional Experience

**Full Stack Engineer (AI)**  |  *Jun 2025 - Present*

*Epik Solutions*

- Engineered high-performance microservices in Go and Python to ingest telemetry from 15+ systems into a centralized Snowflake warehouse, automating 40% of SOC workflows and reducing MTTR by 15 mins

- Built real-time React-based analytics dashboards aggregating telemetry from 15+ systems, eliminating 20+ hours/week of manual reporting and improving decision latency for C-suite stakeholders

- Developed AI-driven incident triage pipelines (Airflow, Azure OpenAI) processing 1,000+ daily events, reduced analyst workload by 30% and enforced data governance via Terraform-managed access policies.

- Automated cross-functional enterprise workflows with ETL pipelines using PySpark to process and ingest enterprise data into Databricks Delta Lake, serving 500+ users, reducing operational cycle times by 40%

- Deployed services using Azure cloud-native infrastructure, Docker, Kubernetes, Github Actions and resolved silent execution failures in distributed Go runbooks, improving pipeline success rates by 25%

Complex UI Features

Delivered a force-directed identity graph explorer (Profile360) using react-force-graph-2d + D3 force simulation with 7 color-coded node types (User, App, Role, Department, Team, Location, Resource), custom canvas renderers, click-to-select detail panels, and node clustering — allowing security teams to visually audit access relationships across thousands of identities in real time

Shipped a rich text document editor with multi-format export using react-quill with 17 registered fonts, server-side content conversion to Markdown, RTF, and DOCX, change-detection gating, and base64-chunked document processing (10 docs/chunk) to prevent main-thread blocking — used by compliance officers to author and version audit artifacts

Built a two-level hierarchical controls registry (Objectives → Focus Areas) with inline expand/collapse, cross-level full-text search, independent pagination at both levels, filterable by framework and category, and a tabbed detail view (Evidence, Tests, Policies, Comments, Linked Documents) — replacing manual spreadsheet tracking for SOC 2 audit workflows

Integrated a multi-format evidence viewer supporting PDF rendering (@react-pdf-viewer/core with Web Worker), image previews (react-viewer), and react-dropzone file upload with base64 encoding — enabling auditors to attach and review evidence artifacts directly within control detail views

Platform Architecture & Infrastructure

Architected and deployed a production-grade, multi-tenant B2B SaaS compliance automation platform (TrustX ATAP) on AWS, provisioning 17 CDK stacks,  15 Lambda functions, 2 ECS Fargate services, 1 AppRunner service, and 1 AppSync GraphQL API — reducing infrastructure setup time from weeks to a single cdk deploy -all command

Designed and implemented end-to-end tenant isolation across PostgreSQL schemas, per-tenant Neo4j databases, S3 buckets, and Secrets Manager namespaces — enabling 10,000+ users per organization to operate in fully segregated environments with zero cross-tenant data leakage

Established a 361/month production cloud footprint supporting 100+ concurrent users across 3 enterprise integrations (Microsoft Entra ID, GitHub, Jira), benchmarked against a target data throughput of  1 GB per pipeline run

AI / LLM Automation

Built an LLM-powered SOC 2 compliance testing engine using AWS Bedrock (Llama 3.3 70B) that automatically collects evidence from CloudTrail, CloudWatch, AWS Config, Security Hub, and Inspector v2, then generates a scored compliance report per control — cutting manual auditor review time by an estimated 70

Delivered a Natural Language → Cypher query interface via a LangChain + OpenAI GPT Flask API deployed on AWS AppRunner, allowing compliance analysts at enterprise customers to query identity graphs in plain English without writing database queries

Implemented semantic document search by generating and persisting 32+ vector embeddings via AWS Bedrock, enabling auditors to surface contextually relevant compliance evidence in seconds rather than manually scanning document repositories

Data Pipeline & Graph Engineering

Led the design and delivery of the Profile 360 identity graph pipeline, orchestrating 5 Lambda functions across 2 parallel AWS Step Functions stages to ingest and model Entra ID, GitHub, and Jira data as nodes and relationships in per-tenant Neo4j databases — running automatically every night via EventBridge

Shipped a force-directed identity/access graph visualization in React (react-force-graph-2d) consumed by security and compliance teams at enterprise customers, replacing spreadsheet-based access reviews and reducing time-to-insight from hours to seconds

Security & Compliance

Implemented SOC 2 automated control testing for enterprise SaaS customers, covering controls including TX-MON04.01 and CC7.1, with AI-generated evidence artifacts stored in S3 and compliance scores persisted in PostgreSQL — enabling customers to maintain continuous compliance posture rather than point-in-time audit snapshots

Enforced least-privilege IAM, VPC-isolated Lambdas, Auth0 JWT validation, and Secrets Manager credential management across all 17 stacks, meeting OWASP and SOC 2 security requirements and eliminating hardcoded credentials across the entire codebase

Full-Stack Product Delivery

Delivered a React + AppSync GraphQL frontend (50+ commits, 12+ feature branches) covering compliance controls, evidence management, policy authoring, document storage, and integration configuration — serving compliance officers and security engineers at B2B enterprise accounts managing their SOC 2 audit lifecycle end-to-end

**Founding Engineer (Full Stack AI)**  |  *Jul 2024 - Jun 2025*

*Samay Systems LLC*

- Architected and built an AI compliance SaaS platform serving 15+ enterprise clients, scaling to 10,000+ users per org on AWS, engineered isolated multi-tenant architectures with Snowflake and PostrgeSQL

- Designed Golang-based distributed pipelines (AWS Glue, Kinesis, CDK, Lambda) and Airflow for multi-stage ETLs to automate SOC2/ISO 27001 evidence collection and real-time control validation

- Built LLM-powered compliance automation (AWS Bedrock, LangChain, MCP, n8n) to orchestrate evidence collection, summarization, and control scoring, reducing manual auditor effort by 70%

- Developed distributed ETL pipelines ingesting 5M+ daily events into knowledge graphs, utilized SQL (PostgreSQL) and graph databases to prepare and normalize complex datasets for real-time analytics

Developed distributed data ingestion pipelines (Step Functions, Lambda) to ingest identity and activity data from enterprise systems into graph-based access models, implemented GraphRAG compliance querying.

- Developed fullstack React + GraphQL applications enabling compliance controls, evidence management, policy authoring, identity graph visualization and document storage for enterprise users

- Optimized computer vision inference pipelines for production semi-autonomous tractor fleets using PyTorch and OpenCV, improving object detection accuracy by 15% and cutting per-frame inference latency by 20ms directly impacting safety reliability across 500+ deployed units

- Delivered full-stack enhancements to internal ML data labeling infrastructure used by Monarch's research team, improving annotation throughput by 20% and accelerating model training iteration cycles for autonomous navigation systems

**SDE Intern**  |  *Jun 2023 - Aug 2023*

*Monarch Tractor*

- Built an automated identity lifecycle system syncing 500+ employees across UKG, JumpCloud, and Azure AD using (AWS/Azure) Serverless architecture, reducing provisioning time by 80%

- Developed full-stack features (React, Golang) for MLOps data labeling infrastructure, improving annotation throughput by 20% for ML training pipelines

**Software Engineer**  |  *Jul 2021 - Aug 2022*

*ZeMoSo Technologies*

- Delivered full-stack features for a cloud-based robotic lab automation platform used by 500+ scientists, working across React, Ruby on Rails, spring boot and PostgreSQL in a microservices architecture

- Designed and implemented features across 10+ core product modules (inventory, compounds, batch tracking, LCMS uploads, container linkage), enabling accurate tracking of complex experimental data

- Authored 100+ test cases and resolved critical production issues, integrated CI/CD pipelines using Jenkins to enforce quality checks, and promote artifacts in a regulated scientific platform

## Skills

**Languages**: Python, Golang, Ruby, Java, TypeScript, JavaScript, SQL, Bash, C++

**AI & ML**: LLMs (Azure OpenAI, AWS Bedrock), RAG, LangChain, MCP, TensorFlow, OpenCV

**Frameworks**: React, Node.js, GraphQL, Spring Boot, Ruby on Rails, Gin

**Cloud & DevOps**: AWS (Glue, Kinesis, EMR), Azure, Docker, Kubernetes, Terraform, Github Actions

**Databases**: Snowflake, Databricks, PostgreSQL, MySQL, MongoDB, Redis, OpenSearch, Pinecone, Neo4j

**Tools & Methodologies**: Git, Apache Airflow, n8n, Power Platform, WSL2, Linux, Agile (Scrum/Kanban), Medallion Architecture, Data Observability, TDD, CI/CD, SRE

## Education

**Master's in Computer Science**, Oklahoma State University, Stillwater  |  *Aug 2022 - May 2024*

**Bachelor's in Computer Science**, JNTU Hyderabad, India  |  *Jul 2017 - Jun 2021*

> [!example]- Exact LaTeX source — archived, never executed
> ~~~~latex
> \documentclass[11pt]{article}
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
> 
> \renewcommand\labelitemi{$\vcenter{\hbox{\small$\bullet$}}$}
> \setlist[itemize]{itemsep=2pt, topsep=1pt, parsep=0pt, partopsep=0pt, leftmargin=12pt}
> \titlespacing*{\section}{0pt}{4pt}{3pt}
> \begin{document}
> \centerline{\Huge \textbf{Neel Gali}}
> \vspace{2pt}
> \centerline{\Large Full Stack Engineer}
> \vspace{1pt}
> \centerline{neelgali7@gmail.com  |  +1(475)-291-1455  |  Austin, TX | {\href{https://linkedin.com/in/neelgali}{linkedin.com/in/neelgali}}}
> \vspace{0pt}
> 
> \section*{Professional Experience}
> 
> \textbf{Full Stack Engineer (AI)} \hfill \textit{Jun 2025 - Present} \\
> \textit{Epik Solutions} \\
> \begin{itemize}
> \item Engineered high-performance microservices in Go and Python to ingest telemetry from 15+ systems into a centralized Snowflake warehouse, automating 40\% of SOC workflows and reducing MTTR by 15 mins
> 
> \item Built real-time React-based analytics dashboards aggregating telemetry from 15+ systems, eliminating 20+ hours/week of manual reporting and improving decision latency for C-suite stakeholders
> 
> \item Developed AI-driven incident triage pipelines (Airflow, Azure OpenAI) processing 1,000+ daily events, reduced analyst workload by 30\% and enforced data governance via Terraform-managed access policies.
> 
> \item Automated cross-functional enterprise workflows with ETL pipelines using PySpark to process and ingest enterprise data into Databricks Delta Lake, serving 500+ users, reducing operational cycle times by 40\%
> 
> \item Deployed services using Azure cloud-native infrastructure, Docker, Kubernetes, Github Actions and resolved silent execution failures in distributed Go runbooks, improving pipeline success rates by 25\%
> \end{itemize}
> 
> 
> 
> 
> \begin{comment}
> 
> Complex UI Features
> 
> Delivered a force-directed identity graph explorer (Profile360) using react-force-graph-2d + D3 force simulation with 7 color-coded node types (User, App, Role, Department, Team, Location, Resource), custom canvas renderers, click-to-select detail panels, and node clustering — allowing security teams to visually audit access relationships across thousands of identities in real time
> 
> Shipped a rich text document editor with multi-format export using react-quill with 17 registered fonts, server-side content conversion to Markdown, RTF, and DOCX, change-detection gating, and base64-chunked document processing (10 docs/chunk) to prevent main-thread blocking — used by compliance officers to author and version audit artifacts
> 
> Built a two-level hierarchical controls registry (Objectives → Focus Areas) with inline expand/collapse, cross-level full-text search, independent pagination at both levels, filterable by framework and category, and a tabbed detail view (Evidence, Tests, Policies, Comments, Linked Documents) — replacing manual spreadsheet tracking for SOC 2 audit workflows
> 
> Integrated a multi-format evidence viewer supporting PDF rendering (@react-pdf-viewer/core with Web Worker), image previews (react-viewer), and react-dropzone file upload with base64 encoding — enabling auditors to attach and review evidence artifacts directly within control detail views
> 
> Platform Architecture \& Infrastructure
> 
> Architected and deployed a production-grade, multi-tenant B2B SaaS compliance automation platform (TrustX ATAP) on AWS, provisioning 17 CDK stacks, ~15 Lambda functions, 2 ECS Fargate services, 1 AppRunner service, and 1 AppSync GraphQL API — reducing infrastructure setup time from weeks to a single cdk deploy --all command
> 
> Designed and implemented end-to-end tenant isolation across PostgreSQL schemas, per-tenant Neo4j databases, S3 buckets, and Secrets Manager namespaces — enabling 10,000+ users per organization to operate in fully segregated environments with zero cross-tenant data leakage
> 
> Established a $361/month production cloud footprint supporting 100+ concurrent users across 3 enterprise integrations (Microsoft Entra ID, GitHub, Jira), benchmarked against a target data throughput of ~1 GB per pipeline run
> 
> AI / LLM Automation
> 
> Built an LLM-powered SOC 2 compliance testing engine using AWS Bedrock (Llama 3.3 70B) that automatically collects evidence from CloudTrail, CloudWatch, AWS Config, Security Hub, and Inspector v2, then generates a scored compliance report per control — cutting manual auditor review time by an estimated 70%
> 
> Delivered a Natural Language → Cypher query interface via a LangChain + OpenAI GPT Flask API deployed on AWS AppRunner, allowing compliance analysts at enterprise customers to query identity graphs in plain English without writing database queries
> 
> Implemented semantic document search by generating and persisting 32+ vector embeddings via AWS Bedrock, enabling auditors to surface contextually relevant compliance evidence in seconds rather than manually scanning document repositories
> 
> Data Pipeline \& Graph Engineering
> 
> Led the design and delivery of the Profile 360 identity graph pipeline, orchestrating 5 Lambda functions across 2 parallel AWS Step Functions stages to ingest and model Entra ID, GitHub, and Jira data as nodes and relationships in per-tenant Neo4j databases — running automatically every night via EventBridge
> 
> Shipped a force-directed identity/access graph visualization in React (react-force-graph-2d) consumed by security and compliance teams at enterprise customers, replacing spreadsheet-based access reviews and reducing time-to-insight from hours to seconds
> 
> Security \& Compliance
> 
> Implemented SOC 2 automated control testing for enterprise SaaS customers, covering controls including TX-MON04.01 and CC7.1, with AI-generated evidence artifacts stored in S3 and compliance scores persisted in PostgreSQL — enabling customers to maintain continuous compliance posture rather than point-in-time audit snapshots
> 
> Enforced least-privilege IAM, VPC-isolated Lambdas, Auth0 JWT validation, and Secrets Manager credential management across all 17 stacks, meeting OWASP and SOC 2 security requirements and eliminating hardcoded credentials across the entire codebase
> 
> Full-Stack Product Delivery
> 
> Delivered a React + AppSync GraphQL frontend (50+ commits, 12+ feature branches) covering compliance controls, evidence management, policy authoring, document storage, and integration configuration — serving compliance officers and security engineers at B2B enterprise accounts managing their SOC 2 audit lifecycle end-to-end
> 
> 
> \end{comment}
> 
> 
> 
> 
> 
> 
> \textbf{Founding Engineer (Full Stack AI)} \hfill \textit{Jul 2024 - Jun 2025} \\
> \textit{Samay Systems LLC} \\
> \begin{itemize}
> \item Architected and built an AI compliance SaaS platform serving 15+ enterprise clients, scaling to 10,000+ users per org on AWS, engineered isolated multi-tenant architectures with Snowflake and PostrgeSQL
> 
> \item Designed Golang-based distributed pipelines (AWS Glue, Kinesis, CDK, Lambda) and Airflow for multi-stage ETLs to automate SOC2/ISO 27001 evidence collection and real-time control validation
> 
> \item Built LLM-powered compliance automation (AWS Bedrock, LangChain, MCP, n8n) to orchestrate evidence collection, summarization, and control scoring, reducing manual auditor effort by 70\%
> 
> \item Developed distributed ETL pipelines ingesting 5M+ daily events into knowledge graphs, utilized SQL (PostgreSQL) and graph databases to prepare and normalize complex datasets for real-time analytics
> 
> \begin{comment}
> Developed distributed data ingestion pipelines (Step Functions, Lambda) to ingest identity and activity data from enterprise systems into graph-based access models, implemented GraphRAG compliance querying.
> \end{comment}
> 
> \item Developed fullstack React + GraphQL applications enabling compliance controls, evidence management, policy authoring, identity graph visualization and document storage for enterprise users
> 
> 
> \end{itemize}
> 
> 
> \begin{comment}
> 
> \item Optimized computer vision inference pipelines for production semi-autonomous tractor fleets using PyTorch and OpenCV, improving object detection accuracy by 15\% and cutting per-frame inference latency by 20ms directly impacting safety reliability across 500+ deployed units
> \item Delivered full-stack enhancements to internal ML data labeling infrastructure used by Monarch's research team, improving annotation throughput by 20\% and accelerating model training iteration cycles for autonomous navigation systems
> 
> \end{comment}
> 
> \textbf{SDE Intern} \hfill \textit{Jun 2023 - Aug 2023} \\
> \textit{Monarch Tractor} \\
> \begin{itemize}
> 
> \item Built an automated identity lifecycle system syncing 500+ employees across UKG, JumpCloud, and Azure AD using (AWS/Azure) Serverless architecture, reducing provisioning time by 80\%
> \item Developed full-stack features (React, Golang) for MLOps data labeling infrastructure, improving annotation throughput by 20\% for ML training pipelines
> \end{itemize}
> 
> \textbf{Software Engineer} \hfill \textit{Jul 2021 - Aug 2022} \\
> \textit{ZeMoSo Technologies} \\
> \begin{itemize}
> \item Delivered full-stack features for a cloud-based robotic lab automation platform used by 500+ scientists, working across React, Ruby on Rails, spring boot and PostgreSQL in a microservices architecture
> 
> \item Designed and implemented features across 10+ core product modules (inventory, compounds, batch tracking, LCMS uploads, container linkage), enabling accurate tracking of complex experimental data
> 
> \item Authored 100+ test cases and resolved critical production issues, integrated CI/CD pipelines using Jenkins to enforce quality checks, and promote artifacts in a regulated scientific platform
> \end{itemize}
> 
> \section*{Skills}
> \textbf{Languages}: Python, Golang, Ruby, Java, TypeScript, JavaScript, SQL, Bash, C++  \\
> 
> \textbf{AI \& ML}: LLMs (Azure OpenAI, AWS Bedrock), RAG, LangChain, MCP, TensorFlow, OpenCV \\
> 
> \textbf{Frameworks}: React, Node.js, GraphQL, Spring Boot, Ruby on Rails, Gin \\
> 
> \textbf{Cloud \& DevOps}: AWS (Glue, Kinesis, EMR), Azure, Docker, Kubernetes, Terraform, Github Actions \\
> 
> \textbf{Databases}: Snowflake, Databricks, PostgreSQL, MySQL, MongoDB, Redis, OpenSearch, Pinecone, Neo4j \\
> 
> \textbf{Tools \& Methodologies}: Git, Apache Airflow, n8n, Power Platform, WSL2, Linux, Agile (Scrum/Kanban), Medallion Architecture, Data Observability, TDD, CI/CD, SRE
> 
> \section*{Education}
> \textbf{Master's in Computer Science}, Oklahoma State University, Stillwater \hfill \textit{Aug 2022 - May 2024} \\
> \textbf{Bachelor's in Computer Science}, JNTU Hyderabad, India \hfill \textit{Jul 2017 - Jun 2021} \\
> \end{document}
> ~~~~

## Source provenance

Source modification date is filesystem metadata, not a verified authorship date. This is a one-time import snapshot; later external edits are not automatically synced.

- [Golang / Go Python React Snowflake Apache Airflow Azure OpenAI / 6 YOE / Full Stack AI Engineer / Ice Capital richard krause / Neel_Gali_Resume_Senior_Full_Stack_AI_Engineer.tex](file:///D:/HDD%20F/downloads/CV/Resumes/Golang/Go%20Python%20React%20Snowflake%20Apache%20Airflow%20Azure%20OpenAI/6%20YOE/Full%20Stack%20AI%20Engineer/Ice%20Capital%20richard%20krause/Neel_Gali_Resume_Senior_Full_Stack_AI_Engineer.tex)

For claim checks, consult [[Claims to Reconcile]] and supporting experience evidence before tailoring.
