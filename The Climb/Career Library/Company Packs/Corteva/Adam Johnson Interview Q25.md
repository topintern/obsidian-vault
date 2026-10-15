---
kind: "company-prep"
title: "Adam Johnson Interview Q25"
collection: "Corteva"
topic: "Interview Prep"
imported: "2026-10-13"
source_files: ["Interview Prep company prep docs/Corteva/Adam_Johnson_Interview_Q25.html","Interview Prep company prep docs/Corteva/Adam_Johnson_Interview_Q25.md"]
tags: ["career/library"]
source_status: "source-claims-not-verified"
---

# Adam Johnson Interview Q25

[[The Climb/Career Library/Career Library]]

> [!info] Source context
> Historical preparation or source notes. First-person stories and numeric outcomes remain source claims until confirmed; this import does not verify them.

# Corteva Technical Interview — Adam Johnson's 25 Most Likely Questions

> Role: Security Auth Backend Engineer | Python, Entra ID, AWS Lambda, Flask  
> Interviewer POV: 1 technical round, hiring manager is technical, urgent fill

---

## Python & Backend Fundamentals

**1. Walk me through how you structure a Python service from scratch — project layout, config management, error handling.**
> *Testing: production discipline, not just "it works". Expect details on env vars, structured logging, custom exceptions.*

**2. You list both FastAPI and Flask. Our team uses Flask — how would you approach building an auth endpoint in Flask vs. FastAPI? What would you miss, what would you gain?**
> *Testing: honest self-assessment, Flask familiarity depth. Be ready to discuss Blueprints, `g`, `before_request` hooks.*

**3. How do you handle dependency injection or service-layer separation in Python? Do you use any patterns or frameworks for that?**
> *Testing: whether you write testable, maintainable code or just flat scripts.*

**4. How do you manage secrets and environment-specific config in a Python service deployed to Lambda?**
> *Testing: AWS SSM / Secrets Manager usage, 12-factor discipline, no hardcoded creds.*

---

## Authentication & Authorization (Core of the Role)

**5. Explain ReBAC to me like I'm a senior engineer who's only used RBAC. Why would Corteva care about it for an agronomic platform?**
> *Testing: depth of understanding, not just buzzword. Drive toward: ownership chains, delegation, contextual access — e.g., "a field agronomist can share access to a specific crop layer with a partner without IT involvement."*

**6. You implemented a ReBAC model at Epik Solutions. What did the data model look like? How did you evaluate a permission check at query time?**
> *Testing: concrete implementation — graph traversal, relation tuples (Zanzibar-style), latency concerns.*

**7. Walk me through the OAuth2 authorization code flow. Where does Entra ID sit in that flow for a backend service?**
> *Testing: knows it deeply — PKCE, token exchange, introspection vs. JWT validation, not just "Entra issues tokens".*

**8. What's SCIM and why did you use it over just syncing via Graph API?**
> *Testing: understands provisioning vs. authentication, push vs. pull, lifecycle events (create/update/deprovision).*

**9. How do you validate a JWT on the backend — what do you actually check beyond the signature?**
> *Testing: iss, aud, exp, nbf, scope claims — and what happens when a key rotates (JWKS endpoint caching).*

**10. You mention 15+ integrated systems in your current role. How did you handle token propagation — did services call each other on behalf of the original user, or did you use service principals? What were the tradeoffs?**
> *Testing: on-behalf-of flow vs. client credentials, zero-trust posture.*

**11. What's the difference between ABAC and ReBAC in practice? Give me a scenario where ABAC breaks down and ReBAC is the right call.**
> *Testing: can distinguish attribute-based policy explosion vs. relationship-based graphs.*

---

## AWS Lambda & Serverless

**12. Your resume says Lambda pipelines processing 5M+ events daily. How did you handle throttling and backpressure on that pipeline?**
> *Testing: SQS visibility timeout, dead-letter queues, reserved concurrency, Lambda scaling limits.*

**13. How do you manage state across a multi-step Lambda workflow — what made you choose Step Functions over chaining Lambdas directly?**
> *Testing: error handling, retries, parallel branches, audit trail needs.*

**14. What's cold start, and how did you address it in a latency-sensitive auth service?**
> *Testing: provisioned concurrency, Lambda SnapStart (Java), keep-warm patterns, package size reduction.*

**15. You used CDK — walk me through how you structured your CDK stacks. Did you use nested stacks, and how did you handle cross-stack references for shared resources like a VPC or an SQS queue?**
> *Testing: real CDK usage vs. just "I deployed with CDK".*

---

## Geospatial (Esri / Mapbox)

**16. You mentioned ESRI exposure at Monarch Tractor. What specifically did you work with — ArcGIS, ArcPy, Feature Services, REST APIs? Walk me through what you actually touched.**
> *Testing: honest scoping. Don't over-claim. Good answer: "I consumed ArcGIS REST APIs and worked with GeoJSON/WKT geometries in Python — I wasn't building map layers from scratch."*

**17. If I handed you a geospatial feature — say, "given a farm boundary polygon, return all authorized users who have access to fields within it" — how would you approach the backend design?**
> *Testing: spatial query in PostGIS or a GIS service, auth intersection, not looking for Esri expertise, looking for problem-solving.*

---

## Data & Databases

**18. You designed multi-tenant schemas with per-tenant PostgreSQL schemas. How do you handle schema migrations in that model — do you run N migrations in parallel or use a shared migration runner?**
> *Testing: Alembic/Flyway in multi-tenant context, row-level security as alternative.*

**19. You mention Neo4j for access graphs. When would you choose Neo4j over modeling relationships in PostgreSQL with a recursive CTE?**
> *Testing: graph traversal depth, query complexity, operational overhead tradeoffs.*

---

## Security & Compliance

**20. How do you enforce tenant isolation at the API layer — what prevents a bug from leaking tenant A's data to tenant B?**
> *Testing: middleware/decorator pattern, always-applied tenant filter, test strategy for it.*

**21. What does "least privilege" mean in practice for a Lambda function that reads from S3 and writes to an SQS queue?**
> *Testing: specific IAM policy (not `*`), resource-level ARNs, condition keys.*

**22. You built an AI triage pipeline for security events. How did you make sure the AI output didn't become a security risk itself — prompt injection, data leakage, etc.?**
> *Testing: awareness of LLM security surface, input sanitization, output validation, no PII in prompts.*

---

## System Design & Architecture

**23. Design a permission check service for an agronomic platform: a user requests access to a geospatial data layer, and the system must evaluate their role, their organization's subscription tier, and the data owner's sharing settings — all in under 100ms.**
> *Testing: caching strategy (Redis), ReBAC graph lookup, async vs. sync evaluation, failure modes.*

**24. A Lambda function that handles auth token validation is seeing p99 latency spike to 3 seconds intermittently. Walk me through how you'd debug it.**
> *Testing: CloudWatch Logs Insights, X-Ray traces, cold start vs. downstream call timeout, JWKS cache miss.*

---

## Behavioral / Delivery

**25. Tell me about a time you owned a feature end-to-end on a small team — from requirements to production. What broke, and what would you do differently?**
> *Testing: independence, production mindset, honest retrospective. Reference the agile sprint delivery bullets.*

---

## Quick Reference: What Adam Most Cares About
| Priority | Signal He's Looking For |
|---|---|
| 🔴 Must-have | Python depth, Entra ID / OAuth2 / SCIM hands-on |
| 🔴 Must-have | Lambda + serverless architecture |
| 🟠 High | ReBAC / ABAC — can explain AND implement |
| 🟠 High | Independent delivery in agile |
| 🟡 Nice-to-have | Flask (you know FastAPI — bridge the gap) |
| 🟡 Nice-to-have | Geospatial awareness (honest scoping wins here) |


> [!example]- Alternate source version (html)
> ## Corteva Technical Interview — Adam Johnson's 25 Most Likely Questions 
>
>   
>
> Role: Security Auth Backend Engineer | Python, Entra ID, AWS Lambda, Flask
>  Interviewer POV: 1 technical round, hiring manager is technical, urgent fill
>
>    
>
> ### Python & Backend Fundamentals 
>
>  
>
> 1. Walk me through how you structure a Python service from scratch — project layout, config management, error handling.
>
>   
>
> Testing: production discipline, not just "it works". Expect details on env vars, structured logging, custom exceptions.
>
>   
>
> 2. You list both FastAPI and Flask. Our team uses Flask — how would you approach building an auth endpoint in Flask vs. FastAPI? What would you miss, what would you gain?
>
>   
>
> Testing: honest self-assessment, Flask familiarity depth. Be ready to discuss Blueprints, g, before_request hooks.
>
>   
>
> 3. How do you handle dependency injection or service-layer separation in Python? Do you use any patterns or frameworks for that?
>
>   
>
> Testing: whether you write testable, maintainable code or just flat scripts.
>
>   
>
> 4. How do you manage secrets and environment-specific config in a Python service deployed to Lambda?
>
>   
>
> Testing: AWS SSM / Secrets Manager usage, 12-factor discipline, no hardcoded creds.
>
>    
>
> ### Authentication & Authorization (Core of the Role) 
>
>  
>
> 5. Explain ReBAC to me like I'm a senior engineer who's only used RBAC. Why would Corteva care about it for an agronomic platform?
>
>   
>
> Testing: depth of understanding, not just buzzword. Drive toward: ownership chains, delegation, contextual access — e.g., "a field agronomist can share access to a specific crop layer with a partner without IT involvement."
>
>   
>
> 6. You implemented a ReBAC model at Epik Solutions. What did the data model look like? How did you evaluate a permission check at query time?
>
>   
>
> Testing: concrete implementation — graph traversal, relation tuples (Zanzibar-style), latency concerns.
>
>   
>
> 7. Walk me through the OAuth2 authorization code flow. Where does Entra ID sit in that flow for a backend service?
>
>   
>
> Testing: knows it deeply — PKCE, token exchange, introspection vs. JWT validation, not just "Entra issues tokens".
>
>   
>
> 8. What's SCIM and why did you use it over just syncing via Graph API?
>
>   
>
> Testing: understands provisioning vs. authentication, push vs. pull, lifecycle events (create/update/deprovision).
>
>   
>
> 9. How do you validate a JWT on the backend — what do you actually check beyond the signature?
>
>   
>
> Testing: iss, aud, exp, nbf, scope claims — and what happens when a key rotates (JWKS endpoint caching).
>
>   
>
> 10. You mention 15+ integrated systems in your current role. How did you handle token propagation — did services call each other on behalf of the original user, or did you use service principals? What were the tradeoffs?
>
>   
>
> Testing: on-behalf-of flow vs. client credentials, zero-trust posture.
>
>   
>
> 11. What's the difference between ABAC and ReBAC in practice? Give me a scenario where ABAC breaks down and ReBAC is the right call.
>
>   
>
> Testing: can distinguish attribute-based policy explosion vs. relationship-based graphs.
>
>    
>
> ### AWS Lambda & Serverless 
>
>  
>
> 12. Your resume says Lambda pipelines processing 5M+ events daily. How did you handle throttling and backpressure on that pipeline?
>
>   
>
> Testing: SQS visibility timeout, dead-letter queues, reserved concurrency, Lambda scaling limits.
>
>   
>
> 13. How do you manage state across a multi-step Lambda workflow — what made you choose Step Functions over chaining Lambdas directly?
>
>   
>
> Testing: error handling, retries, parallel branches, audit trail needs.
>
>   
>
> 14. What's cold start, and how did you address it in a latency-sensitive auth service?
>
>   
>
> Testing: provisioned concurrency, Lambda SnapStart (Java), keep-warm patterns, package size reduction.
>
>   
>
> 15. You used CDK — walk me through how you structured your CDK stacks. Did you use nested stacks, and how did you handle cross-stack references for shared resources like a VPC or an SQS queue?
>
>   
>
> Testing: real CDK usage vs. just "I deployed with CDK".
>
>    
>
> ### Geospatial (Esri / Mapbox) 
>
>  
>
> 16. You mentioned ESRI exposure at Monarch Tractor. What specifically did you work with — ArcGIS, ArcPy, Feature Services, REST APIs? Walk me through what you actually touched.
>
>   
>
> Testing: honest scoping. Don't over-claim. Good answer: "I consumed ArcGIS REST APIs and worked with GeoJSON/WKT geometries in Python — I wasn't building map layers from scratch."
>
>   
>
> 17. If I handed you a geospatial feature — say, "given a farm boundary polygon, return all authorized users who have access to fields within it" — how would you approach the backend design?
>
>   
>
> Testing: spatial query in PostGIS or a GIS service, auth intersection, not looking for Esri expertise, looking for problem-solving.
>
>    
>
> ### Data & Databases 
>
>  
>
> 18. You designed multi-tenant schemas with per-tenant PostgreSQL schemas. How do you handle schema migrations in that model — do you run N migrations in parallel or use a shared migration runner?
>
>   
>
> Testing: Alembic/Flyway in multi-tenant context, row-level security as alternative.
>
>   
>
> 19. You mention Neo4j for access graphs. When would you choose Neo4j over modeling relationships in PostgreSQL with a recursive CTE?
>
>   
>
> Testing: graph traversal depth, query complexity, operational overhead tradeoffs.
>
>    
>
> ### Security & Compliance 
>
>  
>
> 20. How do you enforce tenant isolation at the API layer — what prevents a bug from leaking tenant A's data to tenant B?
>
>   
>
> Testing: middleware/decorator pattern, always-applied tenant filter, test strategy for it.
>
>   
>
> 21. What does "least privilege" mean in practice for a Lambda function that reads from S3 and writes to an SQS queue?
>
>   
>
> Testing: specific IAM policy (not *), resource-level ARNs, condition keys.
>
>   
>
> 22. You built an AI triage pipeline for security events. How did you make sure the AI output didn't become a security risk itself — prompt injection, data leakage, etc.?
>
>   
>
> Testing: awareness of LLM security surface, input sanitization, output validation, no PII in prompts.
>
>    
>
> ### System Design & Architecture 
>
>  
>
> 23. Design a permission check service for an agronomic platform: a user requests access to a geospatial data layer, and the system must evaluate their role, their organization's subscription tier, and the data owner's sharing settings — all in under 100ms.
>
>   
>
> Testing: caching strategy (Redis), ReBAC graph lookup, async vs. sync evaluation, failure modes.
>
>   
>
> 24. A Lambda function that handles auth token validation is seeing p99 latency spike to 3 seconds intermittently. Walk me through how you'd debug it.
>
>   
>
> Testing: CloudWatch Logs Insights, X-Ray traces, cold start vs. downstream call timeout, JWKS cache miss.
>
>    
>
> ### Behavioral / Delivery 
>
>  
>
> 25. Tell me about a time you owned a feature end-to-end on a small team — from requirements to production. What broke, and what would you do differently?
>
>   
>
> Testing: independence, production mindset, honest retrospective. Reference the agile sprint delivery bullets.
>
>    
>
> ### Quick Reference: What Adam Most Cares About 
>
>    
>
>   | Priority  | Signal He's Looking For 
>
>    
>
>   | 🔴 Must-have  | Python depth, Entra ID / OAuth2 / SCIM hands-on 
>
>  
>
>   | 🔴 Must-have  | Lambda + serverless architecture 
>
>  
>
>   | 🟠 High  | ReBAC / ABAC — can explain AND implement 
>
>  
>
>   | 🟠 High  | Independent delivery in agile 
>
>  
>
>   | 🟡 Nice-to-have  | Flask (you know FastAPI — bridge the gap) 
>
>  
>
>   | 🟡 Nice-to-have  | Geospatial awareness (honest scoping wins here)

## Source provenance

- [Original HTML](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Interview%20Prep%20company%20prep%20docs/Corteva/Adam_Johnson_Interview_Q25.html) · Interview Prep company prep docs/Corteva/Adam_Johnson_Interview_Q25.html
- [Original MD](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Interview%20Prep%20company%20prep%20docs/Corteva/Adam_Johnson_Interview_Q25.md) · Interview Prep company prep docs/Corteva/Adam_Johnson_Interview_Q25.md

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
