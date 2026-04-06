# Section 5: Functional Capabilities — Reusable Snippets

> **Usage:** Use these templates to document microservices, web apps, and APIs. Adapt the traceability matrix to map to the client's RFP requirement IDs.

---

## Snippet: Functional Traceability Matrix Template

> Map every RFP functional requirement to your proposed solution. CMMI L5 requires bidirectional traceability.

| RFP Req ID | Requirement Description | Compliance | Module / Service | How We Address It | Test Reference |
|---|---|---|---|---|---|
| FR-001 | [REQUIREMENT] | Fully Met | [SERVICE NAME] | [APPROACH] | TC-[ID] |
| FR-002 | [REQUIREMENT] | Fully Met | [SERVICE NAME] | [APPROACH] | TC-[ID] |
| FR-003 | [REQUIREMENT] | Partially Met | [SERVICE NAME] | [APPROACH + GAP EXPLANATION] | TC-[ID] |
| FR-004 | [REQUIREMENT] | Alternative Proposed | [SERVICE NAME] | [WHY ALTERNATIVE IS BETTER] | TC-[ID] |
| FR-005 | [REQUIREMENT] | Not Applicable | — | [REASON — e.g., "Scope exclusion per §X.X"] | — |

---

## Snippet: Microservice Description Template

### [SERVICE NAME] Service

| Attribute | Detail |
|---|---|
| **Purpose** | [BUSINESS CAPABILITY — e.g., "Manages user authentication, session lifecycle, and authorization decisions"] |
| **Domain** | [BOUNDED CONTEXT — e.g., "Identity & Access Management"] |
| **Key Features** | • [FEATURE 1]<br>• [FEATURE 2]<br>• [FEATURE 3] |
| **Technology** | [RUNTIME — e.g., ".NET 8 / Node.js / Java 21"] on [CONTAINER — e.g., "AKS / EKS"] |
| **Data Store** | [DB TYPE — e.g., "PostgreSQL (master data)", "Redis (session cache)"] |
| **APIs Exposed** | REST ([N] endpoints), [GraphQL / gRPC if applicable] |
| **Events Published** | [EVENT 1 — e.g., "user.created"], [EVENT 2 — e.g., "session.expired"] |
| **Events Consumed** | [EVENT — e.g., "device.provisioned"] |
| **Dependencies** | [SERVICES — e.g., "Notification Service, Audit Service"] |
| **Availability SLA** | [TARGET — e.g., "99.99%"] |
| **Scaling Strategy** | [e.g., "HPA based on CPU + custom requests/sec metric; min 2, max 8 replicas"] |

---

## Snippet: Common Microservices (Pick Applicable)

| Service | Applicable When | Key Features |
|---|---|---|
| **Authentication & Authorization** | Always | OAuth 2.0/OIDC, MFA, SSO, RBAC/ABAC, session management |
| **User Management** | Multi-tenant apps | Registration, profile, preferences, role assignment |
| **Audit & Compliance** | Regulated industries | Immutable event log, retention policies, export, search |
| **Notification & Messaging** | User-facing apps | Email, SMS, push, in-app; template engine; delivery tracking |
| **Administration & Config** | Multi-tenant / SaaS | Feature flags, app config, tenant onboarding, system settings |
| **Device Provisioning** | IoT platforms | Zero-touch enrollment, device lifecycle, firmware management |
| **Telemetry & Ingestion** | IoT / data-heavy | Stream processing, schema validation, dedup, late-arrival handling |
| **File / Document Management** | Document-centric apps | Upload, storage, versioning, virus scan, metadata extraction |
| **Workflow / Task Engine** | Process-driven apps | State machine, approvals, SLA tracking, escalation |
| **Search & Discovery** | Content-rich apps | Full-text search, faceted navigation, relevance ranking |
| **Billing & Subscription** | SaaS products | Plans, metering, invoicing, payment gateway integration |
| **Reporting & Export** | Analytics / BI | Report generation, scheduled delivery, PDF/CSV/Excel export |

---

## Snippet: Web Application Description Template

### [APPLICATION NAME] Portal

| Attribute | Detail |
|---|---|
| **Target Users** | [PERSONA — e.g., "Clinicians (Orthopedic Surgeons, PAs, Nurses)"] |
| **Primary Functions** | • [FUNCTION 1 — e.g., "Patient dashboard with health trends"]<br>• [FUNCTION 2]<br>• [FUNCTION 3] |
| **Technology** | [FRAMEWORK — e.g., "React 18 + TypeScript + Vite"] |
| **Authentication** | [METHOD — e.g., "Entra ID SSO with MFA"] |
| **Authorization** | [MODEL — e.g., "OPA-based object-level RBAC — clinicians see only their patients"] |
| **Responsive** | [Yes / No] — Supported devices: [Desktop, Tablet, Mobile] |
| **Accessibility** | [STANDARD — e.g., "WCAG 2.1 AA"] |
| **Localization** | [LANGUAGES — e.g., "EN, FR, DE"] |
| **Key Integrations** | [e.g., "Deep-link into EHR system, iFrame embedding for partner portals"] |

---

## Snippet: API & Integration Template

| API | Type | Version | Auth | Rate Limit | Documentation | Purpose |
|---|---|---|---|---|---|---|
| [API 1] | REST | v1 (OpenAPI 3.0) | OAuth 2.0 (client_credentials) | [X] req/min | Auto-generated Swagger UI | [PURPOSE] |
| [API 2] | FHIR R4 | STU3/R4 | SMART on FHIR | [X] req/min | FHIR IG published | [PURPOSE] |
| [API 3] | GraphQL | — | Bearer token | [X] req/min | GraphQL Playground | [PURPOSE] |
| [API 4] | Webhook | v1 | HMAC signature | N/A (push) | Event catalog | [PURPOSE] |
| [API 5] | gRPC | proto3 | mTLS | [X] req/sec | Protobuf docs | [PURPOSE — internal service-to-service] |
