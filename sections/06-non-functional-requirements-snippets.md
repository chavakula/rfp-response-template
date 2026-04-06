# Section 6: Non-Functional Requirements — Reusable Snippets

> **Usage:** Select applicable NFR categories. Populate targets based on client requirements. CMMI L5 requires baselines from organizational data.

---

## Snippet: Performance Targets by Platform Type

### High-Throughput API Platform (FinTech, E-Commerce)

| Metric | Target | Measurement |
|---|---|---|
| API Response Time (P50) | < 50 ms | Application Insights / X-Ray |
| API Response Time (P95) | < 200 ms | Application Insights / X-Ray |
| API Response Time (P99) | < 500 ms | Application Insights / X-Ray |
| Throughput | 10,000+ req/sec sustained | Load testing |
| Concurrent Users | 50,000+ | Load testing |
| Page Load (FCP) | < 1.5s | Lighthouse / RUM |
| Page Load (LCP) | < 2.5s | Lighthouse / RUM |

### IoT / Telemetry Platform (Healthcare, Manufacturing, Energy)

| Metric | Target | Measurement |
|---|---|---|
| Data Freshness (end-to-end) | < 30 seconds (real-time), < 5 min (batch) | Pipeline instrumentation |
| Ingestion Throughput | [X] GB/day sustained, [Y] GB/day burst | Event Hub / Kinesis metrics |
| Query Response (time-series) | < 2s on 30-day window, < 10s on 1-year | ADX / Timestream metrics |
| Device Connection Time | < 5 seconds | IoT Hub / IoT Core metrics |
| Message Loss Rate | < 0.001% | End-to-end audit |

### SaaS / Enterprise Application

| Metric | Target | Measurement |
|---|---|---|
| API Response Time (P95) | < 300 ms | APM tooling |
| Page Load (LCP) | < 3.0s | Lighthouse / RUM |
| Search Response | < 500 ms | Application metrics |
| Report Generation | < 10s for standard, < 60s for complex | Application metrics |
| File Upload/Download | > 50 MB/s | Network + storage metrics |

---

## Snippet: Scalability Requirements Template

| Dimension | Current State | Year 1 Target | Year 3 Target | Scaling Approach |
|---|---|---|---|---|
| **Active Users** | [X] | [Y] | [Z] | HPA + KEDA on API pods |
| **Devices / Endpoints** | [X] | [Y] | [Z] | IoT Hub unit scaling + partitioning |
| **Data Volume (daily)** | [X] GB | [Y] GB | [Z] GB | Stream processing auto-scale + storage tiering |
| **Cumulative Storage** | [X] TB | [Y] TB | [Z] TB | Lifecycle policies (hot/cool/archive) |
| **API Calls (daily)** | [X]M | [Y]M | [Z]M | API gateway scaling + CDN caching |
| **Concurrent Sessions** | [X] | [Y] | [Z] | Redis session store + connection pooling |
| **Geographic Regions** | [X] | [Y] | [Z] | Multi-region deployment + Front Door |

---

## Snippet: Reliability & Availability Tiers

### Standard 3-Tier Model

| Tier | Services | Availability | RPO | RTO | HA Strategy |
|---|---|---|---|---|---|
| **Tier 1 — Critical** | Authentication, Core APIs, Data Ingestion | 99.99% | < 30s | < 15 min | Active-Active, multi-AZ, auto-failover |
| **Tier 2 — Important** | Dashboards, Notifications, Reporting | 99.95% | < 5 min | < 30 min | Warm standby, manual switchover |
| **Tier 3 — Standard** | Admin Console, Analytics, Batch Jobs | 99.9% | < 1 hr | < 4 hrs | Cold standby, restore from backup |

### Enhanced 4-Tier Model (Mission-Critical)

| Tier | Availability | RPO | RTO | Architecture |
|---|---|---|---|---|
| **Tier 0 — Life Safety** | 99.999% | 0 (synchronous) | < 60s | Active-Active multi-region, synchronous replication |
| **Tier 1 — Critical** | 99.99% | < 10s | < 5 min | Active-Active, async replication, auto-failover |
| **Tier 2 — Important** | 99.95% | < 5 min | < 30 min | Warm standby |
| **Tier 3 — Standard** | 99.9% | < 1 hr | < 4 hrs | Cold standby |

---

## Snippet: Accessibility Requirements

| Standard | Level | Scope | Testing Approach |
|---|---|---|---|
| WCAG 2.1 | AA | All user-facing pages | Automated (axe-core) + manual audit |
| WCAG 2.1 | AAA | [SPECIFIC PAGES — e.g., patient-facing] | Manual audit by accessibility specialist |
| Section 508 | Compliant | All web applications (US Gov) | VPAT documentation |
| EN 301 549 | Compliant | All web applications (EU) | Conformance statement |
| ARIA 1.2 | Implemented | Interactive components | Screen reader testing (NVDA, VoiceOver) |

**Testing Tools:**
- Automated: axe-core, Lighthouse, pa11y
- Screen Readers: NVDA (Windows), VoiceOver (macOS/iOS), TalkBack (Android)
- Keyboard Navigation: Full tab-order and focus management testing
- Color Contrast: Minimum 4.5:1 (AA), 7:1 (AAA) validated via contrast analyzers

---

## Snippet: Localization Framework

| Capability | Implementation |
|---|---|
| **UI Strings** | Externalized in i18n resource files (JSON/XLIFF); no hardcoded text |
| **Date/Time** | ISO 8601 storage; display in user's locale and timezone |
| **Numbers/Currency** | Locale-aware formatting (Intl API / ICU) |
| **RTL Support** | [CSS logical properties + dir attribute / Not required] |
| **Content Translation** | [Manual — professional translation / Machine — Azure Translator / Hybrid] |
| **Supported Languages** | [LIST — e.g., en-US, en-GB, fr-FR, fr-CA, de-DE, es-ES, pt-BR, ja-JP, zh-CN] |
| **Language Detection** | Browser locale → User preference → Default (en-US) |
| **Pseudo-localization** | Used in testing to detect truncation, concatenation, and hardcoded strings |
