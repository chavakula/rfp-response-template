# Section 17: Operational Runbook & SRE — Reusable Snippets

> **Usage:** Select applicable monitoring, alerting, and incident management templates.

---

## Snippet: Monitoring Stack by Cloud

### Azure Monitoring Stack

| Layer | Tool | What It Monitors | Key Metrics |
|---|---|---|---|
| **Application** | Application Insights | Requests, dependencies, exceptions, traces | Response time, failure rate, dependency calls |
| **Infrastructure** | Azure Monitor | VM/container CPU, memory, disk, network | Utilization %, saturation, errors |
| **Logs** | Log Analytics | Application logs, platform logs, audit logs | Error count, patterns, query response |
| **Security** | Microsoft Sentinel | Security events, threat intelligence, anomalies | Alert count, severity, MTTD, MTTR |
| **Custom** | Grafana (on AKS) | Business metrics, SLIs, dashboards | Domain-specific KPIs |
| **Uptime** | Azure Monitor Availability | Endpoint availability, SSL expiry | Uptime %, response time, SSL days |

### AWS Monitoring Stack

| Layer | Tool | What It Monitors | Key Metrics |
|---|---|---|---|
| **Application** | X-Ray + CloudWatch | Traces, requests, errors | Latency, fault rate, throttle rate |
| **Infrastructure** | CloudWatch | EC2/EKS CPU, memory, network | Utilization %, auto-scaling events |
| **Logs** | CloudWatch Logs Insights | Application and platform logs | Error count, parsed fields |
| **Security** | GuardDuty + Security Hub | Threats, compliance findings | Findings by severity, compliance % |
| **Custom** | Grafana Cloud / Datadog | Business metrics, SLIs | Domain-specific KPIs |

---

## Snippet: Alert Severity & Routing Template

| Severity | Definition | Example | Response | Routing |
|---|---|---|---|---|
| **P1 — Critical** | Service outage or data breach risk; customer impact | API 5xx > 5% for 5 min; DB replication lag > 10 min | Immediate page (24/7) | On-call engineer → Incident Commander |
| **P2 — Major** | Degraded performance or partial outage | P95 latency > 2× baseline; pod restart loop | Page during business hours; Slack alert 24/7 | On-call engineer → Team lead |
| **P3 — Minor** | Issue with workaround; no customer impact | Non-critical job failure; disk > 80% | Slack notification; next business day | DevOps team channel |
| **P4 — Info** | Enhancement or optimization opportunity | Cost anomaly; upcoming certificate expiry | Weekly digest | Team channel |

---

## Snippet: SLI / SLO / Error Budget Template

| Service | SLI (what we measure) | SLO (target) | Error Budget (30-day) |
|---|---|---|---|
| **API Gateway** | % of requests completing < 500ms with 2xx/3xx | 99.95% | 21.6 min downtime / 0.05% errors |
| **Authentication** | % of auth requests completing successfully < 200ms | 99.99% | 4.3 min downtime |
| **Data Ingestion** | % of messages processed within 30 seconds | 99.9% | 43.2 min allowed failure |
| **Dashboard** | % of page loads completing < 3s | 99.5% | 3.6 hrs allowed degradation |

**Error Budget Policy:**
- > 50% budget remaining: Normal release cadence; innovation sprints allowed
- 25–50% budget remaining: Caution; prioritize reliability work in next sprint
- < 25% budget remaining: Reliability freeze; no new features until budget recovers
- 0% budget consumed: All releases frozen; incident review required; reliability sprint mandatory

---

## Snippet: Incident Response Procedure Template

### Incident Lifecycle

```
Detect → Triage → Contain → Diagnose → Resolve → Communicate → Review
```

| Phase | Activities | Timeline | Owner |
|---|---|---|---|
| **Detect** | Alert fires; monitoring confirms | < [X] min (MTTD target) | Monitoring system → On-call |
| **Triage** | Classify severity (P1–P4); assess blast radius | < 5 min | On-call engineer |
| **Contain** | Stop bleeding: redirect traffic, disable feature, scale up | < 15 min (P1 target) | Incident Commander |
| **Diagnose** | Root cause investigation; log analysis; correlation | < 1 hour (P1 target) | Engineering team |
| **Resolve** | Apply fix: deploy patch, config change, failover | Per SLA resolution target | Engineering team |
| **Communicate** | Status page update; stakeholder notification | Throughout | Incident Commander |
| **Review** | Blameless post-mortem; causal analysis; action items | Within 48 hours | All involved parties |

### Post-Mortem Template (CMMI L5 — Causal Analysis)

| Field | Content |
|---|---|
| **Incident ID** | [ID] |
| **Severity** | [P1 / P2 / P3] |
| **Duration** | [Start] to [End] = [Duration] |
| **Impact** | [Users affected, data impact, SLA impact] |
| **Timeline** | Chronological timeline of events and actions |
| **Root Cause** | [Technical root cause — WHY, not just WHAT] |
| **Contributing Factors** | [Process / people / tooling gaps] |
| **What Went Well** | [Effective responses] |
| **What Could Be Improved** | [Gaps in detection, response, communication] |
| **Action Items** | [ITEM — Owner — Due Date — Systemic or Local fix] |
| **CMMI L5: Causal Analysis** | [Ishikawa / 5-Whys / Fault Tree results] |
| **CMMI L5: Process Change** | [If root cause is systemic — what process change prevents recurrence?] |

---

## Snippet: Maintenance Windows Template

| Activity | Frequency | Window | Duration | Impact | Notification |
|---|---|---|---|---|---|
| **Security Patching (OS)** | Monthly (2nd Tuesday) | [DAY] [TIME] UTC | 2 hours | Zero-downtime (rolling) | 5 business days advance |
| **Kubernetes Upgrade** | Quarterly | [DAY] [TIME] UTC | 4 hours | Zero-downtime (blue-green) | 10 business days advance |
| **Database Maintenance** | Monthly | [DAY] [TIME] UTC | 1 hour | Brief read-only window possible | 5 business days advance |
| **Certificate Rotation** | Automated (60 days before expiry) | N/A | None | None | Automated notification if fails |
| **Dependency Updates** | Weekly (automated PR) | N/A | None | None (tested in pipeline) | Weekly digest |
| **Major Platform Upgrade** | Semi-annual | Scheduled window | 6 hours | Planned downtime possible | 20 business days advance |
