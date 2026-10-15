---
kind: "company-prep"
title: "RAPID SCAN"
collection: "Corteva"
topic: "Interview Prep"
imported: "2026-10-13"
source_files: ["Interview Prep company prep docs/Corteva/RAPID_SCAN.html"]
tags: ["career/library"]
source_status: "source-claims-not-verified"
---

# RAPID SCAN

[[The Climb/Career Library/Career Library]]

> [!info] Source context
> Historical preparation or source notes. First-person stories and numeric outcomes remain source claims until confirmed; this import does not verify them.

🎯 Interview TODAY — Adam Johnson @ 1:00 PM

 

## Corteva Rapid-Scan Sheet

 

Scan top-to-bottom. You already know all of this. This is just a trigger refresh.

  

 

### Who is Adam & What He Wants

  
- Technical — will ask real technical questions, not fluff 
- Super nice — conversational, not adversarial 
- Team player signal is critical — mention collaboration, small team ownership 
- Team: 5 senior engineers, tenured together — culture fit is as important as skill 
- Role: 85–90% backend, practical foundational work — not flashy, not greenfield startup chaos  

  

 

### Your Opening — "Tell Me About Yourself" (Memorize the 4 beats)

 

#### Beat 1 — Where you are (10 sec)

 

"Right now I'm at Epik Solutions building the security platform's Python backend — primarily the auth and identity layer. SCIM provisioning receiver, ReBAC permission evaluator, OAuth2 integration with Microsoft Entra ID."

 

#### Beat 2 — Before + the through-line (20 sec)

 

"Before that, Samay Systems — same thing: identity sync pipelines, Lambda, CDK, multi-tenant auth. And a summer at Monarch Tractor on MLOps data infrastructure — that's where I worked with ESRI for field boundary data, GPS telemetry from autonomous tractors. Agricultural domain isn't new to me — I understand what the data represents in a real farming operation."

 

#### Beat 3 — Why Corteva (15 sec)

 

"When I saw this role the overlap was immediate — Python, Lambda, Entra, ReBAC, geospatial in an ag context. What got me genuinely interested is the platform angle: foundational auth and data layer that everything else in the department runs on. Get it right once, everything built on top inherits that correctness."

 

#### Beat 4 — Hand it back (5 sec)

 

"Happy to go deeper anywhere — should we start with the auth work or more about the technical side generally?"

 

  

 

### Top Requirements — Be Ready to Go Deep

 

#### 1. ReBAC / Google Zanzibar

 

One-liner: Relationship-Based Access Control — permissions derived from relationships in a graph, not flat roles. User owns Field → can delegate read to Agronomist → Agronomist can share with Lab.

  
- Built a ReBAC system at Epik on PostgreSQL + Python (not Neo4j, not OpenFGA — justified for our scale) 
- Tuple: (object_type, object_id, relation, user_type, user_id) — e.g., (field, 123, viewer, user, 456) 
- Evaluation walks the graph: direct → inherited → time-bound delegations 
- Cached in Redis (permission_user_resource → boolean, 5-min TTL, invalidate on grant/revoke) 
- 60+ parametrized pytest cases for all edge cases  

Don't say "we used Neo4j for ReBAC." ReBAC is a model, not a storage technology. You implemented it on PostgreSQL.

 

Corteva bridge: Farmer owns field boundaries, shares with agronomist for a season, who delegates to a lab. Classic ReBAC. You've built this in production.

 

#### 2. Microsoft Entra ID (Azure AD)

 

One-liner: Microsoft's cloud identity platform. App Registrations, Service Principals, Managed Identities, Conditional Access.

  
- Registered apps in Entra, defined custom scopes (SecurityPlatform.TriageAccess, SecurityPlatform.ReportRead) 
- Validated tokens in FastAPI: fetch JWKS, decode JWT header for kid, verify signature, check iss/aud/exp/scp 
- Wrapped in Depends(validate_token) — structurally impossible to add an endpoint that forgets auth 
- Service-to-service: Client Credentials flow with app roles 
- JWKS rotation: if sig validation fails → clear cache → re-fetch → retry once  

OAuth2 ≠ authentication. OAuth2 = authorization framework. OIDC = auth (sits on top). Never say "we authenticate with OAuth2."

 

Don't say "Azure AD" if he says "Entra ID." Use his terminology.

 

#### 3. Python (Backend)

 

Key libraries: FastAPI, Pydantic v2, asyncpg, boto3, msal, PyJWT, langchain/langgraph, moto, pytest

  
- If asked "walk me through a Python service" → SCIM receiver at Epik 
- FastAPI + Depends() → auth enforced at framework level 
- Mangum adapter → FastAPI runs as Lambda handler 
- Idempotency: check Redis key (externalId) BEFORE write, set AFTER write succeeds 
- Async = right choice for I/O-bound auth services (Redis, Postgres, SNS)  

Don't say "I'd need time to learn Flask." You know Flask. It's just not your most recent primary. "FastAPI is my most recent — I'll adapt quickly and pick up the team's patterns."

 

  

 

### Your Best Story — SCIM Receiver at Epik (Use This Often)

  

 | What | FastAPI service that received Entra SCIM provisioning calls and fanned out to 15+ security tools

 

 | Input | SCIM HTTP POST/PATCH from Entra (new user, role change, deactivation)

 

 | Processing | Validate bearer token → write to PostgreSQL → set Redis idempotency key → publish to SNS

 

 | Output | 15 downstream SQS Lambdas provisioned users in parallel, asynchronously

 

 | Result | Deprovisioning: 2-3 days → under 30 seconds. Showed up on security vendor questionnaires.

 

 | Infra | FastAPI + Mangum → Lambda + API Gateway. CDK (Python). SSM for secrets.

 

 | Idempotency | Redis key on externalId → set ONLY after successful DB write → Entra retries are no-ops

  

  

 

### Nice-to-Have Skills

 

 

 

#### Flask

  
- Used at Zemoso — familiar, comfortable 
- Blueprint = APIRouter, before_request = middleware, g = request-scoped context 
- Application Factory pattern: create_app(config) 
- "FastAPI is my most recent, Flask is the adjustment — one day, not one week"  

 

 

#### ESRI / Geospatial

  
- Monarch Tractor internship — queried ESRI Feature Services (REST API), consumed GeoJSON 
- Shapely for in-process spatial containment: Point(lon, lat).within(polygon) 
- PostGIS: ST_Within, ST_Intersects, ST_Distance 
- Honest scope: API consumer, not ArcGIS admin. Say so confidently.  

 

 

 

 

#### AWS Lambda

  
- Samay: 5M+ events/day, SQS → Lambda → Neo4j 
- Batch size 25, visibility timeout 90s (Lambda max 60s + 30s buffer) 
- DLQ for poison-pill messages, CloudWatch alarm on DLQ depth 
- Cold start mitigation: provisioned concurrency for auth services 
- p99 spike debug: REPORT logs → Init Duration → X-Ray traces  

 

 

#### React (Light)

  
- Fixed a 200ms frame-advance lag at Monarch: useState → useRef 
- +20% annotation throughput from keyboard shortcut redesign 
- Honest: frontend is 10-15% of what I do. Backend is home.  

 

 

  

 

### Questions to Ask Adam (Pick 3-4)

  
- 🎯 "What does the auth layer look like today — are there specific pain points in the permission model you're trying to solve, or is this more about scaling what's already working?" (shows you understand the actual work) 
- 🎯 "How does the team think about the boundary between the core platform services and the product teams that consume them? Is there a clear contract, or is it still being defined?" (platform thinking, senior-level question) 
- 🎯 "In the first 30-60 days, what would make you feel like a new engineer is really contributing — is it more about getting into the codebase quickly, or understanding the domain context first?" (shows you're thinking about onboarding correctly) 
- ✅ "What does success look like in this role at the 6-month mark?" 
- ✅ "How does the team handle the balance between moving fast on new features and maintaining the stability of services that the whole department depends on?" 
- ✅ "What do you enjoy most about the work here — what keeps the team engaged on foundational infrastructure work day to day?" (shows genuine interest in team culture)  

  

 

### Culture Fit — Weave These In Naturally

  
- Team player signals: "At Epik we were a small team — I owned the auth services end-to-end but always ran the approach by the team before shipping anything foundational." 
- Small tenured team: Show respect for existing patterns. "I'd spend the first week reading existing code before writing any new endpoints." 
- Practical, not flashy: "Foundational infrastructure work is what I find most satisfying — getting the permission model right once means everything built on top just works." 
- Agile: Mention sprint cadence, PR reviews, incremental delivery — don't need to be asked.  

  

 

### What Corteva Does (Brief — Show You Know)

  
- Global agriculture company — seeds, crop protection, digital agronomy 
- Corteva Agriscience spun off from DowDuPont in 2019 
- This team builds the agronomic software platform — the auth and data foundation for digital farming tools used by agronomists, farmers, and partner organizations 
- Field boundaries + crop data layers + multi-party access = classic ReBAC use case  

  

 

### Quick Mental Map — Topic → Your Story

  

 | Topic | Your Story | Key Number

 

 | ReBAC | Permission evaluator at Epik, PostgreSQL + Redis | 60+ test cases

 

 | Entra / OAuth2 | Token validation middleware, SCIM receiver auth | 15+ integrated systems

 

 | SCIM | FastAPI receiver → SNS fan-out to 15 tools | 2-3 days → 30 seconds

 

 | Lambda | Samay identity sync pipeline | 5M+ events/day, $800 → $30/mo

 

 | Python | Three different service shapes at Epik (HTTP, event-driven, LLM orchestration) | —

 

 | ESRI / Geospatial | Monarch Tractor — field boundary enrichment pipeline | 20% annotation throughput

 

 | Flask | Zemoso — state machine APIs, 100+ pytest cases | —

 

 | Testing | pytest, moto, parametrize — discipline from Zemoso, carried forward | 100+ state machine tests

  

  

 

### Traps to Avoid — All in One Place

  
- Don't say "OAuth2 authenticates users" — OAuth2 = authorization. OIDC = authentication. 
- Don't say "we used Neo4j for ReBAC" — ReBAC is a model, not a storage choice. 
- Don't say "I'd need time to learn Flask" — you know Flask, it's a quick adjustment. 
- Don't overclaim ESRI depth — "API consumer, not ArcGIS admin" is the honest, defensible line. 
- Don't say "Azure AD" if Adam says "Entra ID" — match his terminology. 
- Don't confuse App Registration (identity definition) vs Service Principal (identity instance in a tenant). 
- Don't confuse SCIM (provisioning) with OAuth2 (auth tokens) — completely different things.  

 

You built this. You know it. Go get it. — Generated 2026-06-23

## Source provenance

- [Original HTML](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Interview%20Prep%20company%20prep%20docs/Corteva/RAPID_SCAN.html) · Interview Prep company prep docs/Corteva/RAPID_SCAN.html

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
