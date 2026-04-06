# Section 12: Project Plan & Delivery — Reusable Snippets

> **Usage:** Select the phase plan template matching the engagement type. Adjust durations and milestones based on scope.

---

## Snippet: Phase Plans by Engagement Type

### Greenfield Platform Build (12–18 months)

| Phase | Duration | Key Deliverables | Exit Criteria |
|---|---|---|---|
| Phase 0: Discovery & Planning | 6–8 weeks | SRS, HLD, Project Plan, Risk Register | Client-signed SRS |
| Phase 1: Architecture & Design | 6–8 weeks | Architecture Freeze, ADRs, LLD, IaC scaffold | Architecture review passed |
| Phase 2: Core Development (MVP) | 12–16 weeks | Core services + primary web app, CI/CD pipeline | MVP demo accepted |
| Phase 3: Advanced Features | 12–16 weeks | Full feature set, integrations, multi-region | Feature-complete sign-off |
| Phase 4: Testing & Validation | 8–12 weeks | UAT, performance test, pen test, compliance | All P1/P2 resolved; pen test passed |
| Phase 5: Deployment & Launch | 4–6 weeks | Production deployment, data migration, cutover | Go-live checklist passed |
| Phase 6: Hypercare | 4–8 weeks | Stabilization, SLA monitoring, minor fixes | SLA met for [X] consecutive weeks |

### Application Modernization (9–15 months)

| Phase | Duration | Key Deliverables | Exit Criteria |
|---|---|---|---|
| Phase 0: Assessment | 4–6 weeks | Current-state analysis, target architecture, migration plan | Assessment report approved |
| Phase 1: Foundation | 6–8 weeks | Cloud landing zone, CI/CD pipeline, IaC, auth framework | Platform foundation verified |
| Phase 2: Strangler Build | 16–24 weeks | Incremental migration of modules (prioritized by risk/value) | Each module: integration test passed |
| Phase 3: Data Migration | 8–12 weeks | Data migration scripts, validation, parallel run | Data integrity confirmed |
| Phase 4: Cutover & Validation | 6–8 weeks | Progressive cutover, performance validation, legacy retirement plan | Production stable |
| Phase 5: Hypercare | 4–8 weeks | Stabilization, legacy decommissioning | Legacy systems retired |

### Managed Services Onboarding (4–8 weeks)

| Phase | Duration | Key Deliverables | Exit Criteria |
|---|---|---|---|
| Phase 0: Knowledge Transfer | 2–3 weeks | System documentation review, architecture walkthrough, access setup | Team can independently navigate codebase |
| Phase 1: Shadow | 2–3 weeks | Shadow client team; handle L2/L3 with oversight | Successfully resolved [N] tickets |
| Phase 2: Reverse Shadow | 2–3 weeks | Lead operations; client team oversees | All ticket categories handled independently |
| Phase 3: Steady State | Ongoing | Full operational ownership per SLA | SLA targets met for first month |

### Data Platform Build (6–12 months)

| Phase | Duration | Key Deliverables | Exit Criteria |
|---|---|---|---|
| Phase 0: Data Discovery | 4–6 weeks | Data catalog, source profiling, quality assessment, architecture | Data architecture approved |
| Phase 1: Foundation | 4–6 weeks | Data Lake/Lakehouse scaffold, ingestion framework, IaC | Bronze layer ingesting from 1 source |
| Phase 2: Core Pipelines | 8–12 weeks | ETL/ELT for all sources, Silver layer, data quality rules | All sources ingesting; quality metrics green |
| Phase 3: Analytics | 6–8 weeks | Gold layer, dashboards, self-service analytics, ML models | BI users validated; accuracy targets met |
| Phase 4: Governance & Optimization | 4–6 weeks | Data governance (lineage, catalog, security), performance tuning | Governance policies enforced |

---

## Snippet: Milestone Template

| # | Milestone | Target Date | Gate | Dependency |
|---|---|---|---|---|
| M1 | Project Kickoff | [DATE] | — | Contract executed |
| M2 | Architecture Freeze | [DATE] | Architecture Review Board | Client SME availability |
| M3 | Dev Environment Ready | [DATE] | DevOps validation | Cloud subscription provisioned |
| M4 | MVP / Core Demo | [DATE] | Sprint Review | Core requirements defined |
| M5 | Integration Complete | [DATE] | Integration Test Pass | Third-party system access |
| M6 | Feature Complete | [DATE] | Product Owner sign-off | All stories accepted |
| M7 | UAT Complete | [DATE] | UAT Sign-off | Test data availability |
| M8 | Security Clearance | [DATE] | Pen Test Report | Pen test vendor engaged |
| M9 | Production Go-Live | [DATE] | Go/No-Go Checklist | All prior gates passed |
| M10 | Hypercare Complete | [DATE] | SLA Achievement Report | [X] weeks SLA met |
| M11 | Transition / Design Transfer | [DATE] | Handover Acceptance | Training completed |

---

## Snippet: Delivery Methodology Statement

We follow an **Agile-Scrum methodology within a CMMI Level 5 governance framework**, combining the flexibility of iterative delivery with the predictability of quantitative process management.

**Key Practices:**
- **Sprint Duration:** 2 weeks
- **Definition of Done:** Code reviewed → Unit tested (> [X]% coverage) → Integration tested → Security scanned (0 critical/high) → Documentation updated → Product Owner accepted
- **Ceremonies:** Sprint Planning (4 hrs), Daily Standup (15 min), Sprint Review (2 hrs), Retrospective (1 hr)
- **Scaling:** [Scrum / Scrum-of-Scrums / SAFe] for teams > [X] members
- **CMMI L5 Integration:**
  - Velocity tracked on SPC chart from Sprint 3
  - Defect density monitored against organizational baselines
  - Causal Analysis triggered for any escaped P1/P2 defect
  - Estimation accuracy reviewed at each phase gate
