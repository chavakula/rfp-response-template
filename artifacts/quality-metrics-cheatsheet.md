# Quality Metrics Cheat Sheet — CMMI Level 5

> **Usage:** Reference this when populating quality metrics in Sections 14 (Testing & QA) and Appendix D.

---

## DORA Metrics (DevOps Research & Assessment)

| Metric | Elite | High | Medium | Low |
|---|---|---|---|---|
| **Deployment Frequency** | On-demand (multiple/day) | Weekly to monthly | Monthly to 6-monthly | > 6 months |
| **Lead Time for Changes** | < 1 hour | 1 day – 1 week | 1 week – 1 month | 1–6 months |
| **Change Failure Rate** | < 5% | 5–10% | 10–15% | > 15% |
| **MTTR (Failed Deployment)** | < 1 hour | < 1 day | < 1 week | > 1 week |

**Our Target:** Elite across all four metrics by Phase 4.

---

## Quality Metrics Reference

| Metric | Formula | Good Target | Our Baseline |
|---|---|---|---|
| **Defect Density** | Total defects / KLOC | < 3.0/KLOC | [X]/KLOC |
| **Defect Removal Efficiency** | (Defects found before release / Total defects) × 100 | > 95% | [X]% |
| **Escaped Defects** | Defects found in production per release | < 2 P1/P2 per release | [X] |
| **Unit Test Coverage** | Lines covered / Total lines × 100 | > 85% | [X]% |
| **Code Review Coverage** | PRs reviewed / Total PRs × 100 | 100% | 100% |
| **Build Success Rate** | Successful builds / Total builds × 100 | > 95% | [X]% |
| **Sprint Goal Achievement** | Sprints meeting goal / Total sprints × 100 | > 90% | [X]% |
| **Rework Rate** | Rework effort / Total effort × 100 | < 10% | [X]% |
| **Technical Debt Ratio** | Remediation cost / Development cost × 100 | < 5% | [X]% |
| **Automation Rate** | Automated tests / Total tests × 100 | > 80% | [X]% |

---

## SPC Chart Quick Guide

**When to use SPC charts (CMMI L5 requirement):**
- Velocity per sprint (X-bar chart)
- Defect density per release (Individuals chart)
- Cycle time per story (Individuals + Moving Range)
- Build duration trend (Individuals chart)

**Control Limits:**
- UCL = X̄ + 3σ
- LCL = X̄ - 3σ
- Investigate any point outside control limits (special cause)
- Investigate 7+ consecutive points on same side of mean (trend)
- Investigate 7+ consecutive ascending/descending points (shift)

---

## SLA Metric Templates

### For Platform / Application Support

| Metric | P1 (Critical) | P2 (Major) | P3 (Minor) | P4 (Low) |
|---|---|---|---|---|
| **Response Time** | < 15 min | < 1 hr | < 4 hrs | < 1 business day |
| **Resolution Time** | < 4 hrs | < 8 hrs | < 3 business days | Next sprint |
| **Availability** | 99.95% | 99.9% | 99.9% | — |
| **MTTD** | < 3 min | < 10 min | < 30 min | — |
| **MTTR** | < 15 min | < 1 hr | < 4 hrs | — |

### For Development Delivery

| Metric | Target | Measurement |
|---|---|---|
| Sprint Predictability | > 90% stories completed per sprint | Sprint burndown |
| Release Predictability | ±10% of estimated date | Milestone tracking |
| Velocity Stability | σ < 15% of mean velocity | SPC chart |
| Defect Leakage | < 5% defects escape to UAT/Prod | Phase containment analysis |
