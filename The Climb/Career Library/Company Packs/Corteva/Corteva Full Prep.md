---
kind: "company-prep"
title: "Corteva Full Prep"
collection: "Corteva"
topic: "Interview Prep"
imported: "2026-10-13"
source_files: ["Interview Prep company prep docs/Corteva/Corteva_Full_Prep.md"]
tags: ["career/library"]
source_status: "source-claims-not-verified"
---

# Corteva Full Prep

[[The Climb/Career Library/Career Library]]

> [!info] Source context
> Historical preparation or source notes. First-person stories and numeric outcomes remain source claims until confirmed; this import does not verify them.

# Corteva Full Interview Prep — Neel Gali
## Adam Johnson | Technical Round | June 23, 2026

> **How to use this:** Read Layer 1 first — no exceptions. Then Layer 2. Layer 3 is a quick skim.  
> Each keyword follows the same structure: Concept → Your Story → Follow-up Probes → Bridging → Trap to Avoid.

---

# LAYER 1 — MUST NAIL
> *Highest-risk keywords: deep claims, known gaps, or core role requirements. Own these cold.*

---

## 1. ReBAC (Relationship-Based Access Control)

**Concept in plain English**
ReBAC grants access based on *relationships between entities*, not flat roles or static attributes.  
Inspired by Google's Zanzibar paper. A relation tuple looks like:  
`document:doc1#viewer@user:alice` → "Alice is a viewer of doc1"  
Permission check = graph traversal: can user U perform action A on resource R?  
Supports **delegation chains** — Alice can share her document with Bob without IT involvement.

**Your story (Epik Solutions)**  
> "I designed and implemented a ReBAC model in Python for an enterprise security platform. The core was a relation tuples table — (object_type, object_id, relation, subject_type, subject_id). Permission evaluation traversed ownership and delegation chains at query time. We used it to enforce fine-grained access decisions for 500+ users across 15+ integrated systems, handling cases like 'a security team lead can delegate triage access to a contractor for a specific incident, but not the whole queue.'"

**Follow-up probes**
- *"What did your data model look like exactly?"*  
  → Relation tuples table with (object_type, object_id, relation, subject_type, subject_id, granted_by, expiry). Namespace config defined valid relations per resource type. Permission check evaluated direct tuples + transitive expansion (member-of → inherited permissions).

- *"How did you handle performance on permission checks?"*  
  → Cached resolved permission sets in Redis with short TTL (60s). Cache key = (user_id, resource_id, action). Invalidation on any relation tuple mutation. P99 under 20ms.

- *"How is this different from RBAC?"*  
  → RBAC: User → Role → Permissions. Static. Role explosion at scale. ReBAC: User → Resource via a relationship. Dynamic, contextual. A user can be an owner of one document and a viewer of another — same user, different relationship.

- *"How is this different from ABAC?"*  
  → ABAC uses policy rules on attributes: "if user.dept=finance AND resource.sensitivity=low → allow." ReBAC expresses this as relationships in a graph. ABAC breaks when you need to say "Alice shared X with Bob" — that's a relationship, not a policy.

**Bridging to Corteva**  
Corteva's agronomic platform has the exact ReBAC use case: a farmer owns field boundaries, can share access to specific layers with an agronomist, who can delegate read access to a third-party lab — all without IT. That's a delegation chain, not a role.

**Trap to avoid**  
Don't confuse ReBAC with graph databases — ReBAC is a *model*, you can implement it in PostgreSQL with a tuples table. Neo4j just makes traversal faster at scale.

---

## 2. OAuth2

**Concept in plain English**  
Authorization framework — delegates access without sharing credentials. NOT authentication (that's OIDC on top of OAuth2).  
Four flows: **Authorization Code + PKCE** (user-facing apps), **Client Credentials** (service-to-service), Device Code (CLI/IoT), Implicit (deprecated).

**Authorization Code + PKCE flow (the one that matters):**
1. Client generates `code_verifier` → hashes to `code_challenge`
2. Redirect to Entra with `client_id`, `redirect_uri`, `scope`, `state`, `code_challenge`
3. User authenticates → Entra returns `code`
4. Client exchanges `code` + `code_verifier` → gets `access_token` + `refresh_token`
5. API validates `access_token` on every request

**Client Credentials (service-to-service):**  
No user. Service sends `client_id` + `client_secret` → gets access token. Used for Lambda-to-Lambda calls.

**Your story**  
> "In both Epik and Samay, I integrated services with Entra ID using OAuth2. On the backend, every request came in with a Bearer token — I validated the JWT (signature, issuer, audience, expiry, scopes) using the JWKS endpoint. For service-to-service calls inside the platform, we used Client Credentials flow so Lambdas could authenticate to each other without user context."

**Follow-up probes**
- *"How do you validate a JWT on the backend?"*  
  → Fetch public keys from JWKS endpoint (cache them, rotate on 401). Validate: signature, `iss` matches your Entra tenant, `aud` matches your app's client ID, `exp` not expired, `nbf` not in future, `scp`/`roles` contain required scope.

- *"What happens when keys rotate?"*  
  → JWKS endpoint returns multiple keys with `kid` (key ID). JWT header contains `kid` — pick the right key. On 401 from key validation failure, clear JWKS cache and re-fetch once before giving up.

- *"What's the difference between access token and ID token?"*  
  → Access token: for the API, proves authorization, opaque or JWT. ID token: for the client app, proves who the user is, always JWT (OIDC). Never send ID tokens to your API.

**Bridging to Corteva**  
Corteva's auth backbone is almost certainly OAuth2 + Entra. Backend service validates Bearer tokens exactly as described above. This is day-one familiar territory.

**Trap to avoid**  
OAuth2 ≠ authentication. If Adam asks "how do you authenticate users with OAuth2," clarify: OAuth2 is authorization; OIDC (built on top) handles authentication and issues the ID token.

---

## 3. Microsoft Entra ID (Azure AD)

**Concept in plain English**  
Microsoft's cloud identity platform. Acts as the OAuth2/OIDC identity provider, handles user directories, MFA, conditional access, app registrations, service principals, and managed identities.

**Key concepts:**
- **App Registration:** defines your app in Entra, gives you client_id, lets you define API permissions and expose scopes
- **Service Principal:** the identity of an app in a specific tenant
- **Managed Identity:** identity for Azure resources (no secrets needed) — system-assigned or user-assigned
- **Conditional Access:** policies that gate token issuance (require MFA from untrusted locations, block legacy auth, etc.)
- **SCIM provisioning:** automate user lifecycle from HR/IdP into Entra and downstream apps

**Your story**  
> "At Epik, our entire stack was Microsoft — I configured App Registrations for each service, defined custom API scopes, and used Client Credentials for service-to-service auth. I also implemented SCIM provisioning so identity lifecycle events (hire/terminate/role change) automatically propagated to 15+ connected systems without manual admin work."

**Follow-up probes**
- *"How do you configure a Python service to validate Entra tokens?"*  
  → Use `msal` library or `python-jose`. Fetch JWKS from `https://login.microsoftonline.com/{tenant_id}/discovery/v2.0/keys`. Validate `iss` = `https://sts.windows.net/{tenant_id}/`, `aud` = your app's client ID.

- *"What's a managed identity and when would you use it over a client secret?"*  
  → Managed identity = Azure assigns and rotates credentials automatically. No secret in code/config. Use it whenever the caller is an Azure resource (Lambda equivalent = IAM role). Client secrets are for non-Azure callers or when managed identity isn't available.

- *"What's the difference between delegated and application permissions?"*  
  → Delegated: app acts on behalf of a signed-in user (Authorization Code flow). Application: app acts as itself, no user context (Client Credentials). Admin consent required for application permissions.

**Bridging to Corteva**  
If Corteva's platform is Entra-backed (likely), Neel knows the admin side too — not just the developer integration side.

**Trap to avoid**  
Don't use "Azure AD" and "Entra ID" interchangeably mid-sentence as if they're different things — they're the same product, Entra ID is the new name. Just say "Entra ID (formerly Azure AD)" once if needed.

---

## 4. SCIM

**Concept in plain English**  
SCIM (System for Cross-domain Identity Management) = a REST API standard for automating user/group provisioning.  
Endpoints: `/Users`, `/Groups`, `/ServiceProviderConfig`  
Operations: `POST` (create), `GET` (read), `PUT` (full replace), `PATCH` (partial update), `DELETE` (deprovision)  
Entra pushes SCIM events to your app when a user is assigned, modified, or removed from the enterprise app.

**Why SCIM over polling Graph API?**  
SCIM is *push-based* (Entra calls your endpoint) vs. Graph API polling (you call Microsoft). SCIM is also an open standard — works with Okta, Google, Ping, not just Entra.

**Your story**  
> "At Epik, I built a SCIM 2.0 receiver endpoint in FastAPI. Entra would POST to `/scim/v2/Users` when a new employee was provisioned, PATCH when their role changed, and DELETE (or deactivate via active=false) when they left. Our service then propagated those lifecycle events to all 15 downstream systems, so zero manual deprovisioning was needed."

**Follow-up probes**
- *"How do you handle SCIM auth?"*  
  → SCIM endpoints are protected by a long-lived bearer token that Entra is configured with in the provisioning settings. Not OAuth2 flow — it's a static secret. Rotate it via re-configuration.

- *"What happens if your SCIM endpoint is down when Entra pushes an event?"*  
  → Entra retries with exponential backoff for up to 40 days. Events queue up. On recovery, you'll receive all missed events. Good to have an idempotency check on user ID to avoid duplicate creates.

- *"SCIM vs. just using Graph API webhooks?"*  
  → SCIM = standard, portable, your endpoint is the receiver. Graph webhooks = Microsoft-specific, your endpoint receives change notifications, then you call Graph to get the actual data. SCIM is simpler for provisioning use cases.

**Bridging to Corteva**  
Corteva likely provisions agronomist accounts from an HR or partner system into Entra, then propagates to the agronomic platform. SCIM is the right tool for that.

**Trap to avoid**  
SCIM is not an auth protocol — it's a *provisioning* protocol. It doesn't handle login, tokens, or sessions. Conflating SCIM with OAuth2 in an answer is a red flag.

---

## 5. Flask (Bridging from FastAPI)

**Concept in plain English**  
Micro web framework, WSGI-based (synchronous by default). Minimalist — you add what you need via extensions.  
Key concepts: **Blueprints** (modular routing), **Application Factory** (`create_app()`), **`g`** (request-scoped globals), **`before_request` / `after_request`** hooks, **Flask-JWT-Extended** (JWT handling).

**FastAPI → Flask mental mapping:**
| FastAPI | Flask equivalent |
|---|---|
| `Depends(get_current_user)` | `@before_request` + `g.current_user` |
| `APIRouter` | `Blueprint` |
| Pydantic models | `flask-pydantic` or manual `request.get_json()` |
| Async handlers | Synchronous (or use `asyncio` carefully) |
| Auto OpenAPI docs | `flask-smorest` or `flasgger` |

**Bridging answer (rehearse this)**  
> "I've used Flask and FastAPI — FastAPI is my primary framework, but they share the same mental model. Blueprints are like APIRouters, `before_request` is like middleware/Depends. The main adjustment is losing Pydantic's automatic validation — I'd use `flask-pydantic` or marshmallow. Honestly Flask is simpler in some ways; less magic, easier to trace a request path."

**Follow-up probes**
- *"Walk me through an auth middleware in Flask."*  
  → Register a `before_request` on the Blueprint. Extract `Authorization: Bearer <token>` header. Validate JWT. Store decoded payload in `g.current_user`. Route handlers read from `g`. Return 401 if validation fails.

- *"How do you structure a larger Flask app?"*  
  → Application Factory pattern: `create_app(config)` function. Register Blueprints inside it. Config from environment via `os.environ`. Extensions initialized with `init_app()` pattern (Flask-SQLAlchemy, etc.).

- *"How do you handle async in Flask?"*  
  → Flask 2.0+ supports `async def` route handlers natively with `asyncio`. For CPU-heavy work, use Celery. For I/O-heavy, async Flask works. But the team likely uses sync Flask — I'd follow team conventions.

**Trap to avoid**  
Don't say "I've only used FastAPI, I'd need time to learn Flask." Say "I know Flask, FastAPI is my default but it's the same paradigm."

---

## 6. Esri / Mapbox (Geospatial)

**Concept in plain English**  
- **Esri / ArcGIS:** Enterprise GIS platform. ArcGIS REST API exposes Feature Services (queryable geographic feature layers), Map Services, and Geoprocessing Services. Python SDK: `arcpy` (Esri-specific), `arcgis` library.  
- **Mapbox:** Web mapping platform. Vector tiles, GL JS for frontend. Geocoding, routing, spatial analysis APIs.  
- **Common formats:** GeoJSON (JSON-based), WKT (Well-Known Text: `POLYGON((...))`) — used in PostGIS queries.  
- **PostGIS:** PostgreSQL extension for spatial data. `ST_Within`, `ST_Intersects`, `ST_Contains`, `ST_Distance` — spatial SQL functions.

**Your honest story (Monarch Tractor)**  
> "At Monarch Tractor, I was in the MLOps data infrastructure space — processing location telemetry and sensor data from autonomous tractors. I worked with geospatial data in the sense that I handled coordinate data, bounding box queries, and consumed Esri REST APIs for crop field context. My depth is on the data pipeline and backend side — I understand Feature Services, GeoJSON, spatial queries — not production Esri admin or cartography."

**Bridging to Corteva**  
> "The use cases I'd expect here — field boundary queries, layer access control, spatial filtering in backend APIs — are exactly the kind of adjacent backend work I'm comfortable with. The Esri/Mapbox tooling itself I'd get up to speed on quickly given the domain familiarity."

**Follow-up probes**
- *"How would you query which users have access to fields within a given boundary?"*  
  → Backend: receive boundary as GeoJSON polygon. Use PostGIS `ST_Within(field.geometry, ST_GeomFromGeoJSON($boundary))` to find matching fields. Then evaluate ReBAC/ABAC permission for each field against requesting user. Return intersection.

- *"What's a Feature Service?"*  
  → An Esri REST endpoint that exposes a layer of geographic features. You can query it with spatial filters (`geometry`, `spatialRel`, `outFields`). Returns GeoJSON or Esri JSON. Supports CRUD on features.

**Trap to avoid**  
Don't overclaim. If he asks "have you built production Esri features?" — be direct: "My exposure is at the data pipeline and API consumption level, not building map layers or Esri admin workflows. But I understand the domain and the adjacent backend work."

---

# LAYER 2 — SHOULD NAIL
> *Core role requirements. Likely to come up; follow-ups will probe depth.*

---

## 7. AWS Lambda

**Concept**  
Serverless compute. Event-triggered, stateless, 15-min max execution, memory 128MB–10GB (CPU scales with memory).

**Key mechanics:**
- **Cold start:** First invocation spins up execution environment (~100ms–1s). Mitigation: provisioned concurrency (pre-warms N instances), smaller package size, avoid VPC if possible (VPC adds 1–10s historically, improved with Hyperplane).
- **Scaling:** 1000 concurrent default (soft limit). Burst: +500/min until limit.
- **Event sources:** SQS (batch), S3 (object events), API Gateway, EventBridge, Step Functions, DynamoDB Streams.
- **SQS backpressure:** Set visibility timeout > Lambda timeout. DLQ for failed batches. `bisect_on_error=true` to split failing batches. Max receive count before DLQ.

**Your story**  
> "At Samay, I built identity sync pipelines on Lambda — SQS-triggered, processing 5M+ daily Entra/GitHub events. Lambda fetched events, updated the Neo4j access graph, and emitted downstream events to SNS. Batch size was tuned to keep each invocation under 30 seconds. DLQ with alerting caught poison-pill events without blocking the queue."

**Follow-up probes**
- *"p99 latency spike to 3s — how do you debug?"*  
  → CloudWatch Logs Insights: query for `REPORT` lines, sort by duration, filter by cold start. X-Ray traces: find which downstream call is slow (JWKS fetch? DB query? external API?). Check if spike correlates with traffic burst (cold starts), time of day (token expiry causing JWKS re-fetch), or specific input.

- *"How do you share state between Lambda invocations?"*  
  → You don't, by design. Stateless. Use ElastiCache (Redis) for hot shared state, DynamoDB for durable state, SQS for coordination. Execution context (global variables outside handler) is reused within same warm container but never rely on it.

---

## 8. Step Functions

**Concept**  
Serverless workflow orchestration. Define state machines in ASL (Amazon States Language). Coordinates Lambda calls, waits, parallel branches, error handling.

**Standard vs Express:**
- Standard: durable, exactly-once, audit history, up to 1 year. Use for critical business workflows.
- Express: high-throughput, at-least-once, up to 5 min. Use for high-volume event processing.

**Why not just chain Lambdas?**  
Step Functions gives you: retry/backoff per state, catch blocks, parallel execution, audit trail (every state transition logged), wait states, human approval steps — without writing orchestration code.

**Your story**  
> "At Samay, identity sync was orchestrated by Step Functions. The state machine had parallel branches for GitHub and Entra events, a Map state to process batches, and Catch blocks routing failures to a remediation Lambda instead of dropping them. The audit trail in Step Functions was critical for SOC 2 compliance — every access graph update had a logged workflow execution."

**Follow-up probes**
- *"How do you pass large payloads between states?"*  
  → Step Functions payload limit is 256KB. For large data, store in S3 and pass the S3 key between states. Lambda reads from S3, writes result back to S3, passes key to next state.

---

## 9. AWS CDK

**Concept**  
Infrastructure as Code in real languages (Python, TypeScript). Compiles to CloudFormation.  
**Constructs:** L1 (raw CFN resource), L2 (opinionated, e.g., `Function`, `Bucket`), L3 (patterns, e.g., `ApplicationLoadBalancedFargateService`).  
**Stacks:** unit of deployment = one CFN stack.

**Your story**  
> "At Samay, I owned all infrastructure as Python CDK. Stacks were split by concern: a `NetworkStack` (VPC, subnets), `DataStack` (RDS, ElastiCache), `AppStack` (Lambda functions, SQS, Step Functions). Cross-stack references used `CfnOutput` and `Fn.importValue`. CDK Context stored VPC IDs and AMI lookups in `cdk.json` so deploys were deterministic across environments."

**Follow-up probes**
- *"How do you manage multi-environment deployments in CDK?"*  
  → Environment-specific config passed via CDK context (`-c env=prod`) or separate config files loaded in the app. Stack is instantiated per environment: `MyStack(app, "prod-stack", env=PROD_ENV)`. Separate AWS accounts per environment for hard isolation.

---

## 10. Multi-tenant Systems

**Concept**  
Multiple customers share the same infrastructure but with strict data isolation.  
**Isolation models:**
- Row-level security (RLS): single schema, PostgreSQL policies enforce `WHERE tenant_id = current_setting('app.tenant_id')`. Simplest ops, most risk if RLS misconfigured.
- Schema-per-tenant: separate PostgreSQL schema per tenant, same DB. Good isolation, works at <1000 tenants. Alembic migrations run per schema.
- Database-per-tenant: max isolation, max ops overhead. For enterprise/regulated customers.

**Your story**  
> "At Samay, we used schema-per-tenant PostgreSQL. Each tenant got their own schema at onboarding, provisioned by a Lambda that ran Alembic migrations against that schema. The API layer always extracted tenant ID from the JWT claim (never trusted client-provided tenant ID), set a connection-level schema search path, and middleware enforced it on every request."

**Follow-up probes**
- *"What prevents a bug from leaking tenant A's data to tenant B?"*  
  → Defence in depth: (1) Schema isolation means a `SELECT * FROM users` query only sees that tenant's table. (2) API middleware validates and sets tenant context from JWT — cannot be spoofed. (3) Integration tests with two tenants verify no cross-contamination. (4) Schema-per-tenant means even a missing WHERE clause can't cross tenants.

---

## 11. RBAC and ABAC

**RBAC (Role-Based Access Control)**  
User → Role → Permissions. Simple, auditable. Breaks at scale (role explosion: too many specific roles for edge cases).

**ABAC (Attribute-Based Access Control)**  
Policy rules evaluated against attributes: user attributes (dept, clearance), resource attributes (sensitivity, owner), environment attributes (time, IP). Flexible but policy explosion at scale.

**When each breaks:**
- RBAC breaks: "Field rep in Iowa can see Iowa customers but not Nebraska" — now you need a role per region × function.
- ABAC breaks: "Alice shared her report with Bob" — that's a relationship, ABAC can't express it as policy.
- ReBAC covers what both break on.

**Your story**  
> "At Samay, the compliance platform used a hybrid: RBAC for coarse-grained tenant roles (admin, auditor, viewer), ABAC for data sensitivity labels (SOC2-evidence, PII, public), and ReBAC for ownership and delegation of specific compliance frameworks. Each layer checked in order — role check, attribute check, relationship check."

---

## 12. Event-Driven Architecture

**Concept**  
Producers emit events, consumers react asynchronously. Decoupled, scalable, resilient.

**Key patterns:**
- **Pub/Sub:** SNS fan-out to multiple SQS queues. Each consumer gets its own queue.
- **Event sourcing:** store all state changes as immutable events; current state = replay of events.
- **CQRS:** separate read and write models. Write = events; Read = materialized view.

**Idempotency:** consumers must handle duplicate events. Use event ID in a `processed_events` table with a unique constraint.  
**Ordering:** SQS FIFO guarantees ordering within a message group. Standard SQS = best-effort.

**Your story**  
> "The identity sync pipeline was fully event-driven. Entra emitted SCIM events → Lambda wrote to SQS → Step Functions processed → updated Neo4j → emitted downstream events to SNS (fan-out to 10+ services). Each Lambda was idempotent — checked the event ID before processing. FIFO SQS used for ordering-sensitive access graph updates."

---

# LAYER 3 — SOLID BASELINE
> *Skim these. Answers should be fluent but deep probing here is unlikely.*

---

## 13. FastAPI

Your primary framework. Lead with: async-first, Pydantic validation, `Depends()` for DI, auto OpenAPI docs. For Corteva: "My day-to-day but I adapt to Flask easily — same paradigm."

## 14. PostgreSQL

Key points: ACID, indexes (B-tree default, GIN for JSONB, GiST for geospatial via PostGIS), partitioning (range for time-series, list for tenant), `EXPLAIN ANALYZE` for debugging. Your story: "40% query improvement through partitioning and index design on security event tables."

## 15. LangChain / LangGraph

LangChain: chains, agents, tools, memory. LangGraph: graph-based stateful multi-agent workflows (nodes = LLM steps, edges = transitions). Your story: AI triage pipeline (Epik) and compliance automation (Samay). LangGraph for multi-step workflows where a single chain wasn't enough.

## 16. Neo4j

Graph DB, Cypher query language. Nodes + Relationships + Properties. Use case: access graphs where traversal depth matters. vs PostgreSQL recursive CTE: Neo4j faster at depth >3, easier to model complex relationship types. Your story: Samay identity graph — modeled user → group → resource ownership chains.

## 17. RAG / Pinecone / Vector Embeddings

RAG = Retrieval-Augmented Generation: chunk docs → embed → store in vector DB → on query, embed query → similarity search → retrieve top-k chunks → pass to LLM as context. Pinecone = managed vector DB. Your story: compliance document search over 5M+ regulatory docs, sub-second response.

## 18. AWS Bedrock

Managed foundation model API (Claude, Llama, Titan, etc.). No GPU infra to manage. Your story: Samay compliance automation — orchestrated evidence collection and control testing workflows. Reduced manual auditor effort by 70%.

## 19. S3

Object storage. Event notifications (→ Lambda, SNS, SQS). Lifecycle policies for archival. Your story: data ingestion pipeline foundation at Epik — Lambda wrote enriched events to S3, established schema standards adopted by 10+ downstream services.

## 20. JWT

JSON Web Token. Three parts: header (alg, kid), payload (claims), signature. Validate: signature (JWKS), `iss`, `aud`, `exp`, `nbf`, `scope`/`roles`. Stateless auth — no DB lookup needed. Tradeoff: can't revoke before expiry (use short TTL + refresh tokens or token introspection).

## 21. SAML

XML-based enterprise SSO (older than OIDC). Used in legacy enterprise apps. IdP-initiated (IdP starts the flow) vs SP-initiated (app redirects to IdP). In skills but unlikely to be deep-dived — "I understand SAML for enterprise SSO integration; modern projects I use OIDC/OAuth2."

## 22. Docker

Container runtime. Dockerfile → image → container. Multi-stage builds to minimize image size. `.dockerignore`. Healthchecks. Your story: containerized all services in Samay; CDK deployed to ECS Fargate.

## 23. PostgreSQL — Multi-tenant Migrations

Alembic with schema-per-tenant: maintain one migration history table per schema, run `alembic upgrade head` against each schema. Script iterates tenant schemas. Alternatively, use a single schema with row-level security and one migration history.

## 24. DynamoDB / Redis

DynamoDB: key-value + document, single-table design, partition key + sort key, on-demand or provisioned throughput, TTL for auto-expiry. Redis: in-memory, sub-millisecond, used for session caching, JWKS caching, rate limiting. Your story: Redis for permission check caching (short TTL, invalidated on tuple mutation).

## 25. CI/CD (pytest, Jenkins, Agile)

pytest for unit/integration tests, fixtures, parametrize, mock. Jenkins/GitHub Actions for pipelines. Your story: "Authored 100+ test cases at Zemoso, established CI/CD pipeline. At Epik/Samay: tests ran on every PR, deploys gated on test pass + security scan."

---

# SYSTEM DESIGN — #23 (Practice out loud)

**Question:** Design a permission check service for an agronomic platform. User requests access to a geospatial data layer. Evaluate: role, org subscription tier, and data owner's sharing settings — all under 100ms.

**How to talk through it:**

1. **Clarify:** "Is this a real-time API check on every request, or a pre-computed cache?" → assume real-time with caching.
2. **Inputs:** `{user_id, resource_id, action}` → output: `{allowed: bool, reason: str}`
3. **Three layers of evaluation:**
   - Layer 1 (RBAC): Is user's role permitted to perform this action class at all? (Redis cache, TTL 5min)
   - Layer 2 (ABAC): Does org's subscription tier include this data layer type? (Redis cache, TTL 1hr)
   - Layer 3 (ReBAC): Does a sharing relationship exist between data owner and user? (Neo4j traversal or relation tuples in Redis, TTL 60s)
4. **Short-circuit:** fail fast on Layer 1 before hitting DB.
5. **Cache invalidation:** publish an event on any permission mutation → invalidate affected cache keys.
6. **Failure mode:** if permission service is down → fail closed (deny, don't allow). Surface 503 to caller.
7. **Under 100ms:** Layer 1+2 = Redis lookups (~1ms each). Layer 3 = Redis cache hit (~1ms) or Neo4j traversal (~10-20ms). Total well under 100ms on cache hit. Cache miss path = ~30-50ms.

---

# BEHAVIORAL — #25 (Your story)

**Question:** Tell me about a time you owned a feature end-to-end on a small team.

**Story (Epik, AI triage pipeline):**
> "At Epik, I was asked to reduce security analyst workload for incident triage. I took it from requirements to production solo over 3 weeks.  
> I designed a Lambda-triggered pipeline: security events → SQS → Lambda → Azure OpenAI → enriched summary stored in PostgreSQL → surfaced in the security dashboard.  
> What broke: the first version had no rate limiting on the OpenAI calls. A spike of 800 events in 5 minutes hit the API rate limit and started failing silently. I caught it in logs on day 2.  
> Fix: added a token bucket rate limiter, fallback to a rule-based summarizer when OpenAI was unavailable, and an SQS dead-letter queue with alerting.  
> What I'd do differently: rate limit from day one, and define the fallback path before going to prod — not after."

---

# QUICK CHEAT SHEET — 2 min before the call

| They ask about | Lead with |
|---|---|
| ReBAC | "Relation tuples, graph traversal, delegation chains. I built this at Epik." |
| OAuth2 | "Authorization Code + PKCE for users, Client Credentials for services. I validate JWT on every request." |
| Entra ID | "App Registrations, SCIM provisioning, JWKS validation. My current stack is entirely Microsoft." |
| SCIM | "Push-based provisioning standard. Entra calls my endpoint. Not auth — lifecycle management." |
| Flask | "Same paradigm as FastAPI. Blueprints = APIRouter, before_request = Depends. I can adapt immediately." |
| Esri | "I've worked with ArcGIS REST APIs and geospatial data formats at Monarch Tractor. Backend/pipeline depth, not cartography." |
| Lambda | "Event-driven, stateless, SQS-triggered. Built 5M events/day pipelines. I own cold start and backpressure." |
| System design | Slow down. Clarify. Layer the solution. Talk through failure modes. |


## Source provenance

- [Original MD](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Interview%20Prep%20company%20prep%20docs/Corteva/Corteva_Full_Prep.md) · Interview Prep company prep docs/Corteva/Corteva_Full_Prep.md

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
