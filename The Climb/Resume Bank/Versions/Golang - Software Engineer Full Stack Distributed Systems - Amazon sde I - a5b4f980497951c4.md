---
resume_title: "Golang - Software Engineer Full Stack Distributed Systems - Amazon sde I"
kind: "resume-bank-entry"
resume_kind: "Resume"
resume_owner: "Neel-labelled"
resume_family: "Golang"
resume_families: ["Golang"]
resume_role: "Software Engineer Full Stack Distributed Systems"
resume_company: "Amazon"
resume_context: "Go Python React AI n8n AWS Bedrock / 6 YOE / Software Engineer Full Stack Distributed Systems / Amazon sde I"
resume_experience_labels: ["6 YOE"]
resume_source_modified: "2026-03-27"
resume_review: "unreviewed"
resume_favorite: false
resume_pdf: ["[[The Climb/Resume Bank/_Originals/f4920f367225/Neel_Gali_Resume_Senior_Full_Stack_AI_Engineer.pdf]]"]
resume_word: []
source_paths: ["D:\\HDD F\\downloads\\CV\\Resumes\\Golang\\Go Python React AI n8n AWS Bedrock\\6 YOE\\Software Engineer Full Stack Distributed Systems\\Amazon sde I\\Neel_Gali_Resume_Senior_Full_Stack_AI_Engineer.pdf","D:\\HDD F\\downloads\\CV\\Resumes\\Golang\\Go Python React AI n8n AWS Bedrock\\6 YOE\\Software Engineer Full Stack Distributed Systems\\Amazon sde I\\Neel_Gali_Resume_Senior_Full_Stack_AI_Engineer.tex"]
source_sha256: ["f4920f36722537b346b147925e57b9763ad169feb13490b66d1924463641b00d","02233053c152b4fcf77f5b2b9b778259445de8cd346c1167714e3c0838f1ea69"]
imported: "2026-10-14"
tags: ["career/resumes"]
---

# Golang - Software Engineer Full Stack Distributed Systems - Amazon sde I

[[Resume Bank]] · [[Resume Catalogue.base]] · [[Tailoring Desk]]

> [!info] Imported source version
> Content and experience labels are preserved, not independently verified. No master resume or submission approval has been assigned.

## Original files

- [[The Climb/Resume Bank/_Originals/f4920f367225/Neel_Gali_Resume_Senior_Full_Stack_AI_Engineer.pdf|Original PDF]]

### File chooser path

After reviewing this version, copy this path into an application's file chooser when a local upload is required:

~~~text
D:\HDD F\downloads\CV\Previous Exp + Interview Prep\Obsidian Vault\The Climb\Resume Bank\_Originals\f4920f367225\Neel_Gali_Resume_Senior_Full_Stack_AI_Engineer.pdf
~~~

## Readable content

**Neel Gali**

 Software Development Engineer | Full Stack & Distributed Systems

neelgali7@gmail.com  |  +1(475)-291-1455  |  Austin, TX | [linkedin.com/in/neelgali](https://linkedin.com/in/neelgali)

## Professional Experience

**Automation Engineer (Full Stack / Distributed Systems)**  |  *Jun 2025 - Present*

*Epik Solutions*

- Implemented scalable microservices using Go and Python, integrating enterprise security platforms and
automating 40% of SOC workflows and reducing MTTR by 15 minutes for internal security teams

- Built real-time React-based analytics dashboards aggregating telemetry from 15+ systems, eliminating 20+ hours/week of manual reporting and improving decision latency for C-suite stakeholders

- Developed AI-driven incident triage pipelines (Python, n8n, AWS Bedrock) processing 1,000+ daily
security events, reducing analyst workload by 30% while ensuring CI/CD governance using TF Sentinel

- Automated cross-functional enterprise workflows using AWS Lambda, Step-Functions, S3 and CLI scripting serving 500+ users, reducing operational cycle times by 40%

- Deployed services using AWS cloud-native infrastructure, Docker, Kubernetes, Github Actions and
resolved silent execution failures in distributed Go runbooks, improving pipeline success rates by 25

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

- Architected and built a multi-tenant AI compliance SaaS platform serving 15+ enterprise clients, scaling to 10,000+ users per org on AWS, ensuring scalability, tenant isolation, and high availability

- Designed distributed backend systems using Golang, AWS CDK, Lambda, ECS, AppSync, SQS, PostgreSQL, and Neo4j with strict tenant isolation across relational, graph, and object storage layers

- Built LLM-powered compliance automation (AWS Bedrock, LangChain, MCP, n8n) to orchestrate evidence collection, summarization, and control scoring, reducing manual auditor effort by 70%

- Developed distributed pipelines ingesting 5M+ daily identity events into knowledge graphs, built
GraphRAG-based compliance chatbots, reducing unauthorized user access footprints by 30%

- Developed fullstack React + GraphQL applications enabling compliance controls, identity graph visualization, evidence management, policy authoring, and document storage for enterprise users

- Optimized computer vision inference pipelines for production semi-autonomous tractor fleets using PyTorch and OpenCV, improving object detection accuracy by 15% and cutting per-frame inference latency by 20ms directly impacting safety reliability across 500+ deployed units

- Developed full-stack features (React, Golang) for MLOps data labeling infrastructure for autonomous navigation systems, improving annotation throughput by 20% for ML training pipelines

- Delivered full-stack enhancements to internal ML data labeling infrastructure used by Monarch's research team, improving annotation throughput by 20% and accelerating model training iteration cycles for autonomous navigation systems

**SDE Intern**  |  *Jun 2023 - Aug 2023*

*Monarch Tractor*

- Built an automated identity lifecycle system syncing 500+ employees across UKG, JumpCloud, and Azure AD using AWS and Python, reducing provisioning time by 80%

- Developed full-stack features (React, Golang) for MLOps data labeling infrastructure for autonomous navigation systems, improving annotation throughput by 20% for ML training pipelines

**Software Engineer**  |  *Jul 2021 - Aug 2022*

*ZeMoSo Technologies*

- Delivered full-stack features for a cloud-based robotic lab automation platform used by 500+ scientists, working across React, Ruby on Rails, spring boot and PostgreSQL in a microservices architecture

- Designed and implemented features across 10+ core product modules (inventory, compounds, batch tracking, LCMS uploads, container linkage), enabling accurate tracking of complex experimental data

- Authored 100+ test cases and resolved critical production issues, integrated CI/CD pipelines using
Jenkins to enforce quality checks, and promote artifacts in a regulated scientific platform

## Skills

**Languages**: Python, Golang, Java, Ruby, TypeScript, JavaScript, SQL, Bash, C++,

**AI & ML**: LLMs (Azure OpenAI, AWS Bedrock), RAG, LangChain, MCP, TensorFlow, OpenCV

**Frameworks**: React, Node.js, GraphQL, Spring Boot, Ruby on Rails, Gin, Echo, Express.js

**Cloud & DevOps**: AWS, Azure, Docker, Kubernetes, Terraform, Github Actions, Jenkins

**Databases**: PostgreSQL, MySQL, MongoDB, Redis, OpenSearch, Pinecone, Neo4j

**Tools**: Git, n8n, Power Platform, WSL2, Linux, Agile (Scrum/Kanban), TDD, CI/CD, SRE

## Education

**Master's in Computer Science**, Oklahoma State University, Stillwater  |  *Aug 2022 - May 2024*

**Bachelor's in Computer Science**, JNTU Hyderabad, India  |  *Jul 2017 - Jun 2021*

> [!example]- Text from the original PDF — preserved separately
> Neel Gali
> 
>         Software Development Engineer | Full Stack & Distributed Systems
> 
>            neelgali7@gmail.com | +1(475)-291-1455 | Austin, TX | linkedin.com/in/neelgali
> 
> Professional Experience
> 
> Automation Engineer (Full Stack / Distributed Systems)               Jun 2025 - Present
> 
> Epik Solutions
> 
> • Implemented scalable microservices using Go and Python, integrating enterprise security platforms and
> 
> automating 40% of SOC workflows and reducing MTTR by 15 minutes for internal security teams
> 
> • Built real-time React-based analytics dashboards aggregating telemetry from 15+ systems, eliminating
>   20+ hours/week of manual reporting and improving decision latency for C-suite stakeholders
> 
> • Developed AI-driven incident triage pipelines (Python, n8n, AWS Bedrock) processing 1,000+ daily
>   security events, reducing analyst workload by 30% while ensuring CI/CD governance using TF Sentinel
> 
> • Automated cross-functional enterprise workflows using AWS Lambda, Step-Functions, S3 and CLI
>   scripting serving 500+ users, reducing operational cycle times by 40%
> 
> • Deployed services using AWS cloud-native infrastructure, Docker, Kubernetes, Github Actions and
> 
> resolved silent execution failures in distributed Go runbooks, improving pipeline success rates by 25
> 
> Founding Engineer (Full Stack AI)                                    Jul 2024 - Jun 2025
> 
> Samay Systems LLC
> 
> • Architected and built a multi-tenant AI compliance SaaS platform serving 15+ enterprise clients, scaling
> 
> to 10,000+ users per org on AWS, ensuring scalability, tenant isolation, and high availability
> 
> • Designed distributed backend systems using Golang, AWS CDK, Lambda, ECS, AppSync, SQS,
>   PostgreSQL, and Neo4j with strict tenant isolation across relational, graph, and object storage layers
> 
> • Built LLM-powered compliance automation (AWS Bedrock, LangChain, MCP, n8n) to orchestrate
>   evidence collection, summarization, and control scoring, reducing manual auditor effort by 70%
> 
> • Developed distributed pipelines ingesting 5M+ daily identity events into knowledge graphs, built
>   GraphRAG-based compliance chatbots, reducing unauthorized user access footprints by 30%
> 
> • Developed fullstack React + GraphQL applications enabling compliance controls, identity graph
> 
> visualization, evidence management, policy authoring, and document storage for enterprise users
> 
> SDE Intern                                                           Jun 2023 - Aug 2023
> 
> Monarch Tractor
> 
> • Built an automated identity lifecycle system syncing 500+ employees across UKG, JumpCloud, and
> 
> Azure AD using AWS and Python, reducing provisioning time by 80%
> 
> • Developed full-stack features (React, Golang) for MLOps data labeling infrastructure for autonomous
> 
> navigation systems, improving annotation throughput by 20% for ML training pipelines
> 
> Software Engineer                                                    Jul 2021 - Aug 2022
> 
> ZeMoSo Technologies
> 
> • Delivered full-stack features for a cloud-based robotic lab automation platform used by 500+ scientists,
> 
> working across React, Ruby on Rails, spring boot and PostgreSQL in a microservices architecture
> 
> • Designed and implemented features across 10+ core product modules (inventory, compounds, batch
>   tracking, LCMS uploads, container linkage), enabling accurate tracking of complex experimental data
> 
> • Authored 100+ test cases and resolved critical production issues, integrated CI/CD pipelines using
>   Jenkins to enforce quality checks, and promote artifacts in a regulated scientific platform
> 
> Skills
> 
> Languages: Python, Golang, Java, Ruby, TypeScript, JavaScript, SQL, Bash, C++,
> AI & ML: LLMs (Azure OpenAI, AWS Bedrock), RAG, LangChain, MCP, TensorFlow, OpenCV
> Frameworks: React, Node.js, GraphQL, Spring Boot, Ruby on Rails, Gin, Echo, Express.js
> Cloud & DevOps: AWS, Azure, Docker, Kubernetes, Terraform, Github Actions, Jenkins
> Databases: PostgreSQL, MySQL, MongoDB, Redis, OpenSearch, Pinecone, Neo4j
> Tools: Git, n8n, Power Platform, WSL2, Linux, Agile (Scrum/Kanban), TDD, CI/CD, SRE
> 
> Education
> 
> Master’s in Computer Science, Oklahoma State University, Stillwater  Aug 2022 - May 2024
> Bachelor’s in Computer Science, JNTU Hyderabad, India                 Jul 2017 - Jun 2021

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
> \centerline{\Large Software Development Engineer | Full Stack \& Distributed Systems}
> \vspace{1pt}
> \centerline{neelgali7@gmail.com  |  +1(475)-291-1455  |  Austin, TX | {\href{https://linkedin.com/in/neelgali}{linkedin.com/in/neelgali}}}
> \vspace{0pt}
> 
> \section*{Professional Experience}
> 
> \textbf{Automation Engineer (Full Stack / Distributed Systems)} \hfill \textit{Jun 2025 - Present} \\
> \textit{Epik Solutions} \\
> \begin{itemize}
> \item Implemented scalable microservices using Go and Python, integrating enterprise security platforms and
> automating 40\% of SOC workflows and reducing MTTR by 15 minutes for internal security teams
> 
> \item Built real-time React-based analytics dashboards aggregating telemetry from 15+ systems, eliminating 20+ hours/week of manual reporting and improving decision latency for C-suite stakeholders
> 
> \item Developed AI-driven incident triage pipelines (Python, n8n, AWS Bedrock) processing 1,000+ daily
> security events, reducing analyst workload by 30\% while ensuring CI/CD governance using TF Sentinel
> 
> \item Automated cross-functional enterprise workflows using AWS Lambda, Step-Functions, S3 and CLI scripting serving 500+ users, reducing operational cycle times by 40\%
> 
> \item Deployed services using AWS cloud-native infrastructure, Docker, Kubernetes, Github Actions and
> resolved silent execution failures in distributed Go runbooks, improving pipeline success rates by 25%
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
> \item Architected and built a multi-tenant AI compliance SaaS platform serving 15+ enterprise clients, scaling to 10,000+ users per org on AWS, ensuring scalability, tenant isolation, and high availability
> 
> \item Designed distributed backend systems using Golang, AWS CDK, Lambda, ECS, AppSync, SQS, PostgreSQL, and Neo4j with strict tenant isolation across relational, graph, and object storage layers
> 
> \item Built LLM-powered compliance automation (AWS Bedrock, LangChain, MCP, n8n) to orchestrate evidence collection, summarization, and control scoring, reducing manual auditor effort by 70\%
> 
> \item Developed distributed pipelines ingesting 5M+ daily identity events into knowledge graphs, built
> GraphRAG-based compliance chatbots, reducing unauthorized user access footprints by 30\%
> 
> \item Developed fullstack React + GraphQL applications enabling compliance controls, identity graph visualization, evidence management, policy authoring, and document storage for enterprise users
> 
> 
> \end{itemize}
> 
> 
> \begin{comment}
> 
> \item Optimized computer vision inference pipelines for production semi-autonomous tractor fleets using PyTorch and OpenCV, improving object detection accuracy by 15\% and cutting per-frame inference latency by 20ms directly impacting safety reliability across 500+ deployed units
> \item Developed full-stack features (React, Golang) for MLOps data labeling infrastructure for autonomous navigation systems, improving annotation throughput by 20\% for ML training pipelines
> \item Delivered full-stack enhancements to internal ML data labeling infrastructure used by Monarch's research team, improving annotation throughput by 20\% and accelerating model training iteration cycles for autonomous navigation systems
> 
> \end{comment}
> 
> \textbf{SDE Intern} \hfill \textit{Jun 2023 - Aug 2023} \\
> \textit{Monarch Tractor} \\
> \begin{itemize}
> 
> \item Built an automated identity lifecycle system syncing 500+ employees across UKG, JumpCloud, and Azure AD using AWS and Python, reducing provisioning time by 80\%
> \item Developed full-stack features (React, Golang) for MLOps data labeling infrastructure for autonomous navigation systems, improving annotation throughput by 20\% for ML training pipelines
> \end{itemize}
> 
> \textbf{Software Engineer} \hfill \textit{Jul 2021 - Aug 2022} \\
> \textit{ZeMoSo Technologies} \\
> \begin{itemize}
> \item Delivered full-stack features for a cloud-based robotic lab automation platform used by 500+ scientists, working across React, Ruby on Rails, spring boot and PostgreSQL in a microservices architecture
> 
> \item Designed and implemented features across 10+ core product modules (inventory, compounds, batch tracking, LCMS uploads, container linkage), enabling accurate tracking of complex experimental data
> 
> \item Authored 100+ test cases and resolved critical production issues, integrated CI/CD pipelines using
> Jenkins to enforce quality checks, and promote artifacts in a regulated scientific platform
> \end{itemize}
> 
> \section*{Skills}
> \textbf{Languages}: Python, Golang, Java, Ruby, TypeScript, JavaScript, SQL, Bash, C++,  \\
> 
> \textbf{AI \& ML}: LLMs (Azure OpenAI, AWS Bedrock), RAG, LangChain, MCP, TensorFlow, OpenCV \\
> 
> \textbf{Frameworks}: React, Node.js, GraphQL, Spring Boot, Ruby on Rails, Gin, Echo, Express.js \\
> 
> \textbf{Cloud \& DevOps}: AWS, Azure, Docker, Kubernetes, Terraform, Github Actions, Jenkins
>  \\
> 
> \textbf{Databases}: PostgreSQL, MySQL, MongoDB, Redis, OpenSearch, Pinecone, Neo4j \\
> 
> \textbf{Tools}: Git, n8n, Power Platform, WSL2, Linux, Agile (Scrum/Kanban), TDD, CI/CD, SRE
> 
> \section*{Education}
> \textbf{Master's in Computer Science}, Oklahoma State University, Stillwater \hfill \textit{Aug 2022 - May 2024} \\
> \textbf{Bachelor's in Computer Science}, JNTU Hyderabad, India \hfill \textit{Jul 2017 - Jun 2021} \\
> \end{document}
> ~~~~

## Source provenance

Source modification date is filesystem metadata, not a verified authorship date. This is a one-time import snapshot; later external edits are not automatically synced.

- [Golang / Go Python React AI n8n AWS Bedrock / 6 YOE / Software Engineer Full Stack Distributed Systems / Amazon sde I / Neel_Gali_Resume_Senior_Full_Stack_AI_Engineer.pdf](file:///D:/HDD%20F/downloads/CV/Resumes/Golang/Go%20Python%20React%20AI%20n8n%20AWS%20Bedrock/6%20YOE/Software%20Engineer%20Full%20Stack%20Distributed%20Systems/Amazon%20sde%20I/Neel_Gali_Resume_Senior_Full_Stack_AI_Engineer.pdf)
- [Golang / Go Python React AI n8n AWS Bedrock / 6 YOE / Software Engineer Full Stack Distributed Systems / Amazon sde I / Neel_Gali_Resume_Senior_Full_Stack_AI_Engineer.tex](file:///D:/HDD%20F/downloads/CV/Resumes/Golang/Go%20Python%20React%20AI%20n8n%20AWS%20Bedrock/6%20YOE/Software%20Engineer%20Full%20Stack%20Distributed%20Systems/Amazon%20sde%20I/Neel_Gali_Resume_Senior_Full_Stack_AI_Engineer.tex)

For claim checks, consult [[Claims to Reconcile]] and supporting experience evidence before tailoring.
