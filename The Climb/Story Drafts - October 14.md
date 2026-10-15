---
kind: "climb-story-source"
status: "unverified-draft"
tags: ["climb/source"]
---

# Story Drafts · October 14

[[STORIES|Experience & stories]] · [[Claims to Reconcile]]

Substantive narrative preserved from the prior STORIES page. Only Markdown quote prefixes were removed. This is a draft, not independent proof of every detail, metric, title, date or tool. Neel's newer explicit confirmations and [[Resume Working Context]] take precedence. Validate precise contributions before using these details in an interview or resume.

I’m a full-stack engineer. I’ve been working across backend, frontend, cloud and automation for about 4 years, and over the last couple of years I’ve been doing more AI-related work as well.
Most recently, at CIFC. A lot of my work has been around taking security data and finance data that lives across different systems and turning it into useful workflows for the business. I’ve mainly worked on AI-based security incident triage workflow, kpi metric dashboard automations and financial reporting automation.
For that AI workflow, the basic problem was that security information was coming from different vendors and someone still had to manually go through it and figure out what mattered. We built a pipeline that collected and cleaned that information, gave the AI the relevant context, and then produced prioritized classifications and summaries with the supporting evidence, confidence and recommended next steps. We still kept a person in the loop before important actions were taken.
On the technical side, I was working with Python, APIs, SQL, React and TypeScript, along with AWS and Microsoft systems like Dataverse, Power Automate, Power BI and Fabric.
Before CIFC, I was at Samay Systems. That was probably where I had the most end-to-end ownership. We were building an AI-based compliance software product for companies. The simple idea was: companies have evidence spread across systems like cloud accounts, identity systems and other tools, and someone normally has to collect all of that manually for audits and compliance checks.
I worked on building the system that connected to those sources, pulled the evidence in, processed it, and then used AI to help evaluate that evidence and explain whether a requirement was being met. We also built a React interface so users could see the result, the evidence behind it and what still needed attention.
That work involved Python, React, PostgreSQL, AWS Lambda and other AWS services, APIs, authentication and authorization, infrastructure using CDK and Terraform-style infrastructure concepts, and RAG and LLM-based workflows.
Before that, I worked in more traditional full-stack roles using things like React, Node, Java, Rails and SQL, so my background started as general software engineering and gradually moved more toward cloud systems, automation, security and AI.
So overall, I’d describe myself as a full-stack engineer who likes owning a problem end to end — understanding the workflow, building the backend and APIs, building the UI when needed, connecting the data and cloud pieces, and getting the whole thing working in production.


CIFC:

At CIFC, one of the more interesting problems I worked on was around security incident triage.
The issue was that the information needed to understand an incident was spread across multiple systems. You might have an alert coming from one security product, device information somewhere else, identity activity in another place, vulnerability context in another source, and then historical information that might help explain whether something was actually suspicious.
So the problem was not really “summarize an alert with AI.” The bigger problem was building a system that could take an incident, gather all the relevant context around it, reason over that context, and produce something useful enough that an analyst could actually act on it.
I worked on that as an end-to-end module.
On the backend side, I used Python to build most of the orchestration layer. We had services that accepted an incident or alert as the starting point and then fanned out into different data sources using APIs. Instead of treating every API independently, I built the backend around a common internal model for things like users, devices, alerts, vulnerabilities, sign-in events and related entities.
That mattered because different systems describe the same thing differently. One API may identify a user by object ID, another by email, another may only give a device identifier. So part of the backend work was resolving those relationships and building a connected incident context rather than just returning a collection of API responses.
I also added logic around API reliability — pagination, retry and backoff, token refresh, rate limits, partial failures and caching. Some sources were more expensive or slower to query, so we did not want every investigation to blindly call everything. The Python layer decided which additional sources were worth querying based on what we had already found.
From there, I built enrichment logic in Python. For example, instead of only saying that a device had an alert, the system could add things like recent identity activity, known vulnerabilities, recent security events, whether the user or device had appeared in other incidents, and other signals that changed the risk of the event.
We also maintained historical snapshots of some of that data so we could compare the current state with what was normal before. That part connected into Dataverse, Power Automate and later some of our Power BI and Fabric work.
The AI layer sat on top of that backend rather than replacing it.
Before anything was sent to the model, the Python service assembled a structured investigation package. We separated confirmed facts, historical context, retrieved reference material and unresolved questions. The model was given only the evidence that the system had actually collected.
For some areas we used a retrieval-style approach, where the system could bring in relevant internal guidance, previous investigation patterns or security knowledge rather than expecting the model to know everything from memory.
Then the model produced things like a concise incident summary, likely explanation, risk level, supporting evidence and recommended next steps.
The important part was guardrails. We did not want the model inventing evidence or taking an action because it sounded confident.
So we required claims to map back to evidence in the investigation package. If the supporting data was missing, the output had to say that rather than fill in the gap. We also kept the actual enforcement actions outside the model. The model could recommend something like isolating a device or investigating a user, but a deterministic workflow or a human analyst had to approve the action.
We also worked on evaluation separately from the prompt. I used representative incident cases and compared outputs across things like whether the model identified the right risk, whether important evidence was included, whether it introduced unsupported claims, and whether the recommended action matched what an analyst would reasonably do.
That gave us a regression set, so if we changed the prompt, model or retrieval logic, we could see whether we actually improved the system or just made the response sound better.
On the UI side, I worked with React and TypeScript to expose the investigation as something an analyst could actually use. The goal was not just to show an AI paragraph. The UI showed the incident, related entities, evidence collected from the different systems, the AI assessment, confidence and recommended next actions. An analyst could drill back into the evidence instead of trusting a black-box answer.
For deployment, the backend pieces were cloud-hosted and designed as separate services rather than one large script. Python services handled orchestration and enrichment, background jobs handled longer-running work, and we used cloud storage and data systems for persisted investigation state and historical data. We also had logging around each stage so we could see which external calls succeeded, what context was assembled, what went to the model and what came back.
So when I describe that project, the AI was actually one layer of it. The bulk of the engineering was building the backend and cloud system that could reliably construct an investigation, maintain state, connect different identities and systems, and then use AI safely on top of that.


Samay:


At Samay, I worked on a compliance automation product where the bigger problem was that companies usually have compliance evidence scattered across many different systems.
For something like SOC 2 or HIPAA, a company may need to prove that users are being deprovisioned correctly, MFA is enabled, cloud resources are configured safely, access is controlled, changes are logged, backups exist and a large number of other controls are being followed.
Normally, someone has to go into each system, collect screenshots or exports, understand what that evidence means, and then map it manually to compliance controls.
We wanted to make that much more automated.
I worked on an end-to-end module where a customer could connect one of their systems — for example Microsoft Graph, AWS or another SaaS system — and our platform would continuously collect evidence, evaluate it against controls and show the result to the user.
The backend was primarily Python.
The first part was integration infrastructure. I built connector services that handled authentication, credentials, token refresh and API access for the external systems. These were not one-off scripts. We needed them to work across multiple customers, so every execution had tenant context, connection configuration and permission boundaries.
For APIs that returned large datasets, we handled pagination and incremental synchronization rather than downloading everything every time. We stored checkpoints so that a later sync could continue from where the previous one ended. We also handled API throttling, retries and transient failures, because some external platforms would fail or rate-limit you even when your own service was working correctly.
Then there was the Python processing layer.
Instead of letting every integration define its own version of compliance logic, we normalized raw external objects into internal domain objects. So a Microsoft identity, an AWS IAM user and a user from another system could all become a common concept like an identity, with properties around access, authentication and privilege.
The same pattern applied to resources, policies, configuration findings and evidence.
That gave us a reusable rules engine. A compliance control could say something like “privileged users must have MFA” without caring whether that information originally came from Microsoft, AWS or another provider.
Python workers processed those normalized objects and evaluated them against control logic. Some controls were deterministic — for example, a field either satisfied a requirement or it did not.
Other controls required more context.
That is where we started using AI and retrieval.
A lot of compliance evidence is unstructured: policy documents, explanations, audit notes, security procedures and exceptions. So I worked on a RAG-based flow where those documents were chunked and indexed, and when the system evaluated a particular control it retrieved only the pieces that were relevant to that control.
The model would then answer a narrow question like whether the evidence supported the requirement, what part of the evidence supported it and what was missing.
We did not ask the model something broad like “is this company compliant?”
The backend determined the control being evaluated, selected the structured evidence, retrieved the relevant document context and then gave the model a constrained task.
We put guardrails around that as well.
The model had to return structured output rather than free-form text. For example, it might return a status, explanation, supporting evidence references and missing information. The backend validated that response before storing it.
If the model cited evidence, that evidence had to exist in the retrieval results. If it produced something we could not trace back to a source, the system would not treat that statement as verified.
And for high-confidence deterministic checks, we did not use AI at all. If a rule could be answered reliably in code, we answered it in Python. AI was mainly used where interpretation of unstructured evidence added value.
For evaluation, we built examples for individual controls where we already knew the expected result. We tested whether the system classified the control correctly, whether the explanation was grounded in the source material, whether it missed critical evidence and whether it produced unsupported claims.
That gave us a way to compare prompt changes or model changes against known examples.
On the frontend, I worked in React.
The UI let users connect integrations, see sync status, browse compliance controls and inspect why a control passed or failed. For an AI-assisted evaluation, we showed the result alongside the evidence that supported it, rather than simply showing a green checkmark and asking the user to trust the model.
We also surfaced missing evidence so that the product could tell the user something actionable, like which configuration or document was still needed.
On the cloud side, we ran this as a set of services on AWS.
Different workloads had different execution patterns. Some API calls could happen synchronously, but a full evidence synchronization might involve thousands of records and several external APIs, so those jobs ran asynchronously.
We used AWS services such as Lambda and S3, along with scheduled and event-driven jobs, so that integration syncs, evidence processing and AI evaluation did not all have to happen in a single request.
We persisted application state in PostgreSQL and used object storage for larger evidence artifacts and documents. We also separated customer data by tenant throughout the processing path.
For deployment, we used CI/CD and infrastructure-as-code so environments could be reproduced rather than manually configured. I worked with AWS deployment tooling and Terraform-style infrastructure management, and we had environment-specific configuration, secrets management and logging around jobs and integrations.
So the end-to-end flow was basically:
a customer connects a system → our backend authenticates and syncs it → Python normalizes the external data → rules evaluate the structured evidence → RAG and AI handle the pieces that require interpretation → the result and evidence are persisted → and the React application gives the customer a clear view of what passed, what failed and why.
That project gave me a lot of experience beyond just using an LLM API. I was working on the surrounding software system — APIs, backend architecture, data models, cloud jobs, frontend, retrieval, AI reliability and deployment.
