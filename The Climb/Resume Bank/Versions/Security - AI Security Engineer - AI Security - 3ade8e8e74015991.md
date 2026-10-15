---
resume_title: "Security - AI Security Engineer - AI Security"
kind: "resume-bank-entry"
resume_kind: "Resume"
resume_owner: "Neel-labelled"
resume_family: "Security"
resume_families: ["Security"]
resume_role: "AI Security Engineer"
resume_company: ""
resume_context: "Threat Modeling STRIDE Python Prompt Injection Mitigation Security Design Reviews / 6 YOE / AI Security Engineer / AI Security"
resume_experience_labels: ["6 YOE"]
resume_source_modified: "2026-04-06"
resume_review: "unreviewed"
resume_favorite: false
resume_pdf: []
resume_word: []
source_paths: ["D:\\HDD F\\downloads\\CV\\Resumes\\Security\\Threat Modeling STRIDE Python Prompt Injection Mitigation Security Design Reviews\\6 YOE\\AI Security Engineer\\AI Security\\Neel_Gali_Resume.tex"]
source_sha256: ["644d0637ae940fd120fa3c64ec9edce91763cab2ddd3a5b4b9a95952ad9a4f37"]
imported: "2026-10-14"
tags: ["career/resumes"]
---

# Security - AI Security Engineer - AI Security

[[Resume Bank]] · [[Resume Catalogue.base]] · [[Tailoring Desk]]

> [!info] Imported source version
> Content and experience labels are preserved, not independently verified. No master resume or submission approval has been assigned.

## Original files

No PDF or Word document accompanies this source. The external source is preserved below; no upload-ready document was generated.

## Readable content

**Neel Gali**


 Security Engineer


neelgali7@gmail.com  |  +1(475)-291-1455  |  Austin, TX



## Professional Experience


**Security Engineer**  |  *Jul 2025 - Present*

*Epik Solutions | Enterprise SaaS Platform*




- Conducted **threat modeling** on the AI document ingestion pipeline, identifying **prompt injection** and adversarial input attack vectors and implementing mitigations across three critical model endpoints.

- Built **Python** scripting tools to fuzz **FastAPI** endpoints with adversarial payloads, detecting seven injection vulnerabilities before production release and reducing the application attack surface significantly.

- Performed **security design reviews** for the ML-powered OCR service, identifying insecure deserialization and **data poisoning** risks and coordinating remediation with the engineering team before launch.

- Implemented **JWT** token rotation, short-lived credential policies, and **OAuth2** scope enforcement on the Rails API, limiting credential compromise blast radius for 20,000+ enterprise SaaS users.

- Investigated **adversarial robustness** of the document classification model, scripting **FGSM** and **PGD** attack simulations in Python and deploying input normalization defenses that strengthened model accuracy.

- Configured **Rack::Attack** rate limiting and **TLS** mutual authentication on Rails API endpoints, enforcing transport-layer security and blocking credential stuffing attacks targeting 20,000+ concurrent enterprise users.

- Deployed secret scanning and dependency **CVE** audits across GitHub repositories, eliminating hardcoded credentials and patching 14 critical vulnerabilities in the Rails and Python dependency trees.



**Security Engineer**  |  *Jul 2022 - Jun 2025*

*Samay Systems LLC | B2B Compliance Platform*




- Led **threat modeling** sessions for B2B compliance platform features using **STRIDE**, producing risk registers and driving security remediation across the engineering team before each release.

- Ran **security assessments** on multi-tenant Rails APIs, uncovering broken object-level authorization and **IDOR** flaws that exposed cross-tenant records and remediating all findings before compliance audit.

- Conducted **security design review** of the Celery async task queue, identifying insecure task serialization and unauthorized job injection risks and hardening the worker authentication layer.

- Migrated the 3M+ record **PostgreSQL** database to per-tenant schema isolation, eliminating cross-tenant data leakage vectors and satisfying **SOC 2** and enterprise compliance audit security requirements.

- Added **Brakeman** and **Bandit** SAST scanning to the GitHub Actions pipeline, blocking high-severity vulnerability merges and reducing security defect escape rate to production by 70%.

- Wrote **Python** data analysis tools to detect anomalous API authorization patterns, flagging 300+ suspicious access attempts daily and feeding alerts into security incident response workflow.

- Enforced **mutual TLS** between Rails microservices and configured **AWS EKS** network policies, encrypting all inter-service traffic and eliminating the lateral movement attack surface in production.



**Software Engineer**  |  *Jul 2020 - Aug 2022*

*Zemoso Technologies | LabOps Platform*




- Built **Python** automation scripts for **DAST** vulnerability scanning, integrating **OWASP ZAP** into CI and automating weekly security scan reports for the LabOps platform review process.

- Implemented **RBAC** and session security hardening in the Rails LabOps platform, enforcing least-privilege access controls and preventing unauthorized researcher access to protected laboratory sample data.

- Reviewed **Python** data export pipeline for injection vulnerabilities, applying parameterized queries and **input sanitization** across all file paths and eliminating the SQL injection attack surface.

- Hardened the **Rails** application against **OWASP Top 10** threats, configuring secure HTTP headers, **HSTS**, **CSP**, and encrypted cookies to eliminate XSS and clickjacking attack surfaces.




## Skills


**Languages**: Python, Ruby, SQL, Bash, JavaScript

**Frameworks & Tools**: Ruby on Rails, FastAPI, Rack::Attack, Celery, RSpec, pytest, Brakeman, Bandit, OWASP ZAP

**Cloud & Infra**: AWS (EKS, Lambda, S3), Docker, Kubernetes, GitHub Actions

**Databases**: PostgreSQL, Redis

**Security**: Threat Modeling (STRIDE), SAST/DAST, OAuth2, JWT, mTLS, RBAC, IDOR, Adversarial ML, Prompt Injection, CVE Triage


## Education


**Master's in Computer Science**, Oklahoma State University, Stillwater

**Bachelor's in Computer Science**, JNTU Hyderabad, India

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
> \centerline{\Large Security Engineer}
> \vspace{1pt}
> \centerline{neelgali7@gmail.com  |  +1(475)-291-1455  |  Austin, TX}
> \vspace{-4pt}
> \section*{Professional Experience}
> \textbf{Security Engineer} \hfill \textit{Jul 2025 - Present} \\
> \textit{Epik Solutions | Enterprise SaaS Platform} \\
> \begin{itemize}
> \item Conducted \textbf{threat modeling} on the AI document ingestion pipeline, identifying \textbf{prompt injection} and adversarial input attack vectors and implementing mitigations across three critical model endpoints.
> \item Built \textbf{Python} scripting tools to fuzz \textbf{FastAPI} endpoints with adversarial payloads, detecting seven injection vulnerabilities before production release and reducing the application attack surface significantly.
> \item Performed \textbf{security design reviews} for the ML-powered OCR service, identifying insecure deserialization and \textbf{data poisoning} risks and coordinating remediation with the engineering team before launch.
> \item Implemented \textbf{JWT} token rotation, short-lived credential policies, and \textbf{OAuth2} scope enforcement on the Rails API, limiting credential compromise blast radius for 20,000+ enterprise SaaS users.
> \item Investigated \textbf{adversarial robustness} of the document classification model, scripting \textbf{FGSM} and \textbf{PGD} attack simulations in Python and deploying input normalization defenses that strengthened model accuracy.
> \item Configured \textbf{Rack::Attack} rate limiting and \textbf{TLS} mutual authentication on Rails API endpoints, enforcing transport-layer security and blocking credential stuffing attacks targeting 20,000+ concurrent enterprise users.
> \item Deployed secret scanning and dependency \textbf{CVE} audits across GitHub repositories, eliminating hardcoded credentials and patching 14 critical vulnerabilities in the Rails and Python dependency trees.
> \end{itemize}
> 
> \textbf{Security Engineer} \hfill \textit{Jul 2022 - Jun 2025} \\
> \textit{Samay Systems LLC | B2B Compliance Platform} \\
> \begin{itemize}
> \item Led \textbf{threat modeling} sessions for B2B compliance platform features using \textbf{STRIDE}, producing risk registers and driving security remediation across the engineering team before each release.
> \item Ran \textbf{security assessments} on multi-tenant Rails APIs, uncovering broken object-level authorization and \textbf{IDOR} flaws that exposed cross-tenant records and remediating all findings before compliance audit.
> \item Conducted \textbf{security design review} of the Celery async task queue, identifying insecure task serialization and unauthorized job injection risks and hardening the worker authentication layer.
> \item Migrated the 3M+ record \textbf{PostgreSQL} database to per-tenant schema isolation, eliminating cross-tenant data leakage vectors and satisfying \textbf{SOC 2} and enterprise compliance audit security requirements.
> \item Added \textbf{Brakeman} and \textbf{Bandit} SAST scanning to the GitHub Actions pipeline, blocking high-severity vulnerability merges and reducing security defect escape rate to production by 70\%.
> \item Wrote \textbf{Python} data analysis tools to detect anomalous API authorization patterns, flagging 300+ suspicious access attempts daily and feeding alerts into security incident response workflow.
> \item Enforced \textbf{mutual TLS} between Rails microservices and configured \textbf{AWS EKS} network policies, encrypting all inter-service traffic and eliminating the lateral movement attack surface in production.
> \end{itemize}
> 
> \textbf{Software Engineer} \hfill \textit{Jul 2020 - Aug 2022} \\
> \textit{Zemoso Technologies | LabOps Platform} \\
> \begin{itemize}
> \item Built \textbf{Python} automation scripts for \textbf{DAST} vulnerability scanning, integrating \textbf{OWASP ZAP} into CI and automating weekly security scan reports for the LabOps platform review process.
> \item Implemented \textbf{RBAC} and session security hardening in the Rails LabOps platform, enforcing least-privilege access controls and preventing unauthorized researcher access to protected laboratory sample data.
> \item Reviewed \textbf{Python} data export pipeline for injection vulnerabilities, applying parameterized queries and \textbf{input sanitization} across all file paths and eliminating the SQL injection attack surface.
> \item Hardened the \textbf{Rails} application against \textbf{OWASP Top 10} threats, configuring secure HTTP headers, \textbf{HSTS}, \textbf{CSP}, and encrypted cookies to eliminate XSS and clickjacking attack surfaces.
> \end{itemize}
> 
> \section*{Skills}
> \textbf{Languages}: Python, Ruby, SQL, Bash, JavaScript \\
> \textbf{Frameworks \& Tools}: Ruby on Rails, FastAPI, Rack::Attack, Celery, RSpec, pytest, Brakeman, Bandit, OWASP ZAP \\
> \textbf{Cloud \& Infra}: AWS (EKS, Lambda, S3), Docker, Kubernetes, GitHub Actions \\
> \textbf{Databases}: PostgreSQL, Redis \\
> \textbf{Security}: Threat Modeling (STRIDE), SAST/DAST, OAuth2, JWT, mTLS, RBAC, IDOR, Adversarial ML, Prompt Injection, CVE Triage \\
> \section*{Education}
> \textbf{Master's in Computer Science}, Oklahoma State University, Stillwater \\
> \textbf{Bachelor's in Computer Science}, JNTU Hyderabad, India \\
> \end{document}
> 
> ~~~~

## Source provenance

Source modification date is filesystem metadata, not a verified authorship date. This is a one-time import snapshot; later external edits are not automatically synced.

- [Security / Threat Modeling STRIDE Python Prompt Injection Mitigation Security Design Reviews / 6 YOE / AI Security Engineer / AI Security / Neel_Gali_Resume.tex](file:///D:/HDD%20F/downloads/CV/Resumes/Security/Threat%20Modeling%20STRIDE%20Python%20Prompt%20Injection%20Mitigation%20Security%20Design%20Reviews/6%20YOE/AI%20Security%20Engineer/AI%20Security/Neel_Gali_Resume.tex)

For claim checks, consult [[Claims to Reconcile]] and supporting experience evidence before tailoring.
