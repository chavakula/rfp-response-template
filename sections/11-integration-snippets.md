# Section 11: Integration & Interoperability — Reusable Snippets

> **Usage:** Select applicable integration patterns and legacy coexistence strategies based on the engagement.

---

## Snippet: Integration Architecture Patterns

### Pattern 1: API-Led Integration (Recommended for Most)

```
Experience APIs (UI-facing) → Process APIs (orchestration) → System APIs (backend adapters)
```

| Layer | Purpose | Example |
|---|---|---|
| **Experience APIs** | Optimized for consumer (web, mobile, partner) | GET /patients/{id}/dashboard |
| **Process APIs** | Orchestrate cross-system workflows | POST /orders (coordinates inventory + payment + shipping) |
| **System APIs** | Adapter for each backend system | GET /legacy-erp/inventory/{sku} |

### Pattern 2: Event-Driven Integration (Async)

```
Source System → Event Broker → Consumer(s)
```

| Component | Azure | AWS | GCP |
|---|---|---|---|
| Event Broker | Event Grid / Service Bus | EventBridge / SNS+SQS | Pub/Sub |
| Stream | Event Hubs | Kinesis | Pub/Sub |
| Consumer | Azure Functions / AKS | Lambda / EKS | Cloud Functions / Cloud Run |

### Pattern 3: ETL/ELT Batch Integration

| Stage | Approach | Tools |
|---|---|---|
| Extract | Scheduled pull from source systems | [Data Factory / Glue / Airbyte] |
| Transform | Data cleansing, mapping, enrichment | [Spark / dbt / custom] |
| Load | Write to target data store | [Synapse / Redshift / BigQuery] |

---

## Snippet: Legacy Coexistence Strategies

### Strategy A: Strangler Fig (Gradual Replacement)

| Phase | Approach | Risk |
|---|---|---|
| 1. Proxy | Route all traffic through new API gateway; gateway forwards to legacy | Low — legacy unchanged |
| 2. Capture | Intercept specific routes; new service handles them; rest to legacy | Medium — dual maintenance |
| 3. Replace | Migrate functionality module by module; shrink legacy routing | Medium — data sync complexity |
| 4. Retire | All traffic on new platform; legacy decommissioned | Low — if phased correctly |

### Strategy B: Parallel Run (Dual Operation)

| Component | Old System | New System | Sync Mechanism |
|---|---|---|---|
| Write Path | Primary | Shadow (verify only) | Event-based replication |
| Read Path | Primary for prod users | New for pilot users | Feature flags per user/cohort |
| Data | Source of truth | Replicated + validated | CDC / ETL / dual-write |

Cutover criteria: [X] weeks of parallel run with < [X]% discrepancy → switch primary.

### Strategy C: Big Bang (Single Cutover)

| Attribute | Detail |
|---|---|
| When to Use | Small systems, low transaction volume, acceptable downtime window |
| Approach | Full migration during maintenance window; hard cutover |
| Rollback | Full rollback plan (restore DB + DNS revert) within [X] hours |
| Risk | High — requires exhaustive pre-cutover testing |

---

## Snippet: Common Integration Points

| Integration | Protocol | Direction | Auth | Data Format | Frequency |
|---|---|---|---|---|---|
| **ERP** (SAP, Oracle, Dynamics) | REST / OData / RFC | Bidirectional | OAuth 2.0 / API Key | JSON / XML | Real-time + batch |
| **CRM** (Salesforce, HubSpot) | REST | Bidirectional | OAuth 2.0 | JSON | Real-time (webhook + polling) |
| **EHR/EMR** (Epic, Cerner) | FHIR R4 / HL7 v2 | Bidirectional | SMART on FHIR | FHIR JSON / HL7 | Real-time |
| **Payment** (Stripe, Adyen) | REST | Outbound + webhook | API Key + webhook signature | JSON | Real-time |
| **Email** (SendGrid, SES) | REST / SMTP | Outbound | API Key | JSON / MIME | Event-driven |
| **SMS** (Twilio, SNS) | REST | Outbound | API Key | JSON | Event-driven |
| **Identity** (Okta, Entra ID) | OIDC / SAML 2.0 | Bidirectional | Federation | JWT / SAML | Real-time |
| **Analytics** (Segment, Mixpanel) | REST / SDK | Outbound | API Key | JSON | Real-time (events) |
| **File Transfer** (SFTP, AS2) | SFTP / AS2 | Bidirectional | SSH key / certificate | CSV / EDI | Batch (scheduled) |
| **Data Warehouse** | JDBC / REST | Outbound | Service account | SQL / Parquet | Batch (nightly) |

---

## Snippet: API Versioning Strategy

| Strategy | When to Use | Example |
|---|---|---|
| **URI Path** | Public APIs with clear version boundaries | `/api/v1/patients`, `/api/v2/patients` |
| **Header** | Internal APIs where URI cleanliness matters | `Accept: application/vnd.api.v2+json` |
| **Query Param** | Simple versioning, backward-compatible | `/api/patients?version=2` |

**Deprecation Policy:**
- New version announced: old version enters "sunset" period ([6–12] months)
- Sunset version returns `Sunset` HTTP header with date
- Usage tracking: monitor old version traffic; notify consumers
- End of life: old version returns 410 Gone after sunset date
