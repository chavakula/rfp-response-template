# Section 18: Maintenance & Support Model — Reusable Snippets

> **Usage:** Select the support model tier matching the engagement. Adjust SLA targets based on client requirements and contract.

---

## Snippet: Support Models

### Model A: Premium Support (24/7 Mission-Critical)

| Attribute | Detail |
|---|---|
| **Coverage** | 24/7/365 for P1; 24/5 for P2; Business hours for P3/P4 |
| **Team** | Dedicated L1 (3 shifts), dedicated L2, shared L3 pool |
| **Response SLA** | P1: < 15 min, P2: < 30 min, P3: < 4 hrs, P4: < 1 business day |
| **Resolution SLA** | P1: < 4 hrs, P2: < 8 hrs, P3: < 3 business days, P4: next sprint |
| **Proactive** | Capacity planning, cost optimization, security posture reviews |
| **Typical Cost** | 15–20% of annual platform revenue (or $[X]K–$[X]K/month) |
| **Best For** | Healthcare, FinTech, e-commerce — any system where downtime = revenue/safety loss |

### Model B: Standard Support (Business Hours)

| Attribute | Detail |
|---|---|
| **Coverage** | Business hours (9 AM – 6 PM client timezone) + P1 on-call pager |
| **Team** | Shared L1/L2 team; dedicated L3 during business hours |
| **Response SLA** | P1: < 30 min, P2: < 1 hr, P3: < 8 hrs, P4: < 2 business days |
| **Resolution SLA** | P1: < 8 hrs, P2: < 16 hrs, P3: < 5 business days, P4: next sprint |
| **Proactive** | Monthly review; quarterly optimization |
| **Typical Cost** | 10–15% of annual platform cost |
| **Best For** | Internal tools, B2B SaaS, batch processing systems |

### Model C: Enhanced Dev Support (Build Phase)

| Attribute | Detail |
|---|---|
| **Coverage** | Business hours; extended hours during release windows |
| **Team** | Same build team provides support during hypercare / early operations |
| **Response SLA** | P1: < 1 hr, P2: < 4 hrs |
| **Duration** | [8–12] weeks post go-live (hypercare period) |
| **Transition** | Transitions to Model A or B after hypercare |
| **Best For** | New platform launches; bridge between build and steady-state support |

---

## Snippet: Support Tier Responsibilities

| Activity | L1 (Triage) | L2 (Investigation) | L3 (Engineering) |
|---|---|---|---|
| Alert monitoring & acknowledgment | ✅ | | |
| Known-issue resolution (runbook-driven) | ✅ | | |
| Initial triage & severity classification | ✅ | | |
| Root cause analysis | | ✅ | |
| Bug fixes & patches | | ✅ | |
| Configuration changes | | ✅ | |
| Performance tuning | | | ✅ |
| Architecture changes | | | ✅ |
| Security incident response | | ✅ | ✅ |
| Capacity planning & optimization | | | ✅ |
| On-call rotation (P1) | ✅ | ✅ (escalation) | ✅ (escalation) |

---

## Snippet: SLA Definition Table

| Metric | Definition | Target | Measurement | Penalty (if applicable) |
|---|---|---|---|---|
| **Availability** | % of time platform is operational (excl. planned maintenance) | [99.9% / 99.95% / 99.99%] | Synthetic monitoring + uptime calculation | [X]% credit per [Y]% below target |
| **P1 Response Time** | Time from alert to engineer acknowledgment | < [X] min | Ticketing system timestamp | Included in SLA credit |
| **P1 Resolution Time** | Time from alert to service restored | < [X] hours | Ticketing system timestamp | [X]% credit per hour overdue |
| **MTTD** | Mean Time To Detect | < [X] min | Average across all incidents/month | SPC tracked |
| **MTTR** | Mean Time To Resolve | < [X] min | Average across all incidents/month | SPC tracked |
| **Change Success Rate** | % of deployments without rollback | > [X]% | CI/CD pipeline data | SPC tracked |
| **Incident Recurrence** | % of incidents with same root cause | < [X]% | Causal analysis data | CMMI L5 review trigger |

---

## Snippet: Continuous Improvement Framework (CMMI L5)

| Activity | Cadence | Inputs | Outputs | Owner |
|---|---|---|---|---|
| **Monthly Service Review** | Monthly | SLA dashboard, incident log, change log | Action items, trend analysis, improvement plan | Service Delivery Manager |
| **Quarterly Architecture Review** | Quarterly | Performance data, cost reports, tech debt backlog | Optimization roadmap, architecture evolution plan | Solution Architect |
| **Quarterly Security Review** | Quarterly | Vulnerability scans, Sentinel findings, compliance status | Remediation plan, policy updates | Security Architect |
| **Annual Pen Test & Compliance** | Annually | Pen test report, audit findings | Remediation plan, re-certification | Security + Compliance |
| **Causal Analysis** | Per P1/P2 incident | Incident data, timeline, logs | Root cause, systemic fix, process change | Incident Commander |
| **Process Performance Review** | Monthly | SPC charts, metric trends | Control limit updates, baseline refresh | Process Lead |

**Improvement Workflow:**
1. **Identify** — Issue surfaces through metrics, incidents, or reviews
2. **Analyze** — Causal analysis (5-Whys, fishbone, Pareto)
3. **Propose** — Improvement action with expected impact (quantified)
4. **Implement** — Change deployed; monitored for effectiveness
5. **Verify** — Measure actual impact vs. expected
6. **Institutionalize** — If effective, update process assets; share across org

---

## Snippet: Support Reporting Template

### Monthly Support Report Contents

| Section | Content |
|---|---|
| **Executive Summary** | SLA performance, key incidents, accomplishments |
| **SLA Dashboard** | Availability %, response/resolution times vs. targets |
| **Incident Summary** | Count by severity, top categories, trends (↑↓→) |
| **Change Summary** | Deployments, success rate, rollbacks |
| **Problem Management** | Open problems, root causes identified, systemic fixes applied |
| **Capacity & Performance** | Resource utilization trends, scaling events, performance metrics |
| **Cost Summary** | Infrastructure cost, month-over-month trend, optimization savings |
| **Security Summary** | Vulnerabilities found/remediated, security incidents, compliance status |
| **Improvement Actions** | Open action items, new proposals, completed improvements |
| **Next Month Plan** | Planned maintenance, upcoming changes, capacity forecasts |
