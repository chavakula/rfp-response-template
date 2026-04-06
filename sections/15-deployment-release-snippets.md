# Section 15: Deployment & Release Management — Reusable Snippets

> **Usage:** Select the deployment strategy and CI/CD pipeline template matching the engagement.

---

## Snippet: Deployment Strategy Comparison

| Strategy | How It Works | Risk | Rollback Time | Best For |
|---|---|---|---|---|
| **Blue-Green** | Two identical environments; swap traffic after validation | Low | < 5 min (swap back) | Critical apps requiring instant rollback |
| **Canary** | Route [X]% of traffic to new version; gradually increase | Low | < 5 min (route 0%) | Large user base; risk-averse releases |
| **Rolling** | Replace pods/instances one at a time | Medium | Minutes (rollback deployment) | Stateless microservices |
| **Feature Flags** | Deploy code to all; toggle feature per user/cohort | Very Low | Instant (flip flag) | Continuous deployment; A/B testing |
| **Recreate** | Stop old → Deploy new | High (downtime) | Minutes | Non-critical, tolerates downtime windows |

**Recommended for most engagements:** Blue-Green + Feature Flags (deploy frequently, control exposure)

---

## Snippet: CI/CD Pipeline Template

### Build → Test → Secure → Deploy → Validate

| Stage | Activities | Quality Gate | Tool |
|---|---|---|---|
| **1. Source** | Code commit to feature branch | PR created, linked to work item | Git ([Azure Repos / GitHub]) |
| **2. Build** | Compile, lint, dependency resolution | Build succeeds, 0 lint errors | [Azure Pipelines / GitHub Actions] |
| **3. Unit Test** | Execute unit tests | > [X]% coverage, 100% pass | [xUnit / Jest / pytest] |
| **4. Static Analysis** | SAST + code quality | 0 critical/high findings, quality gate pass | [SonarQube / Semgrep] |
| **5. Dependency Scan** | SCA / license check | 0 critical vulnerabilities, approved licenses only | [Snyk / Trivy / Dependabot] |
| **6. Container Build** | Build + push container image | Image tagged with commit SHA + version | [Docker / ACR / ECR] |
| **7. Container Scan** | Scan image for vulnerabilities | 0 critical/high in OS packages | [Trivy / Defender / ECR scan] |
| **8. Deploy to Dev** | Auto-deploy to dev environment | Smoke test pass | [Helm / ArgoCD / Flux] |
| **9. Integration Test** | API contract + service integration tests | > [X]% pass | [Pact / RestAssured / Postman] |
| **10. Deploy to Staging** | Promote to staging (prod-mirror) | All prior gates pass | [Helm + approval gate] |
| **11. Performance Test** | Load test against staging | P95 < [X]ms, 0 errors | [k6 / Gatling / Azure Load Testing] |
| **12. Security Test** | DAST scan against staging | 0 critical findings | [OWASP ZAP] |
| **13. Deploy to Prod** | Blue-green swap / canary rollout | Manual approval (first release); auto (subsequent) | [Helm + progressive delivery] |
| **14. Smoke Test** | Post-deploy synthetic monitoring | All critical paths pass | [Playwright / custom health checks] |
| **15. Monitor** | Watch error rates, latency, logs for [X] min | No anomalies detected | [Azure Monitor / CloudWatch] |

### Rollback Procedure

1. Anomaly detected (error rate spike / latency increase / health check failure)
2. Automated alert fires → on-call engineer notified (< 2 min)
3. Rollback initiated: [Blue-green swap / Canary route to 0% / Helm rollback]
4. Previous version serving traffic (< 5 min total)
5. Incident ticket created for RCA
6. Fix developed and deployed through standard pipeline

---

## Snippet: Environment Promotion Flow

```
Feature Branch → Dev → Test/QA → Staging → Production → DR
       ↓             ↓           ↓           ↓            ↓
    PR Build      Auto-deploy  Auto-deploy  Approval     Replication
    Unit Test     Int. Tests   Perf + Pen   Go/No-Go     Auto-sync
    SAST/SCA      E2E Tests    UAT          Blue-Green   Health probes
```

| Environment | Deployment Trigger | Approval | Data | Refresh |
|---|---|---|---|---|
| **Dev** | PR merge to develop | None (auto) | Synthetic / seed data | On deploy |
| **Test/QA** | Dev pipeline success | None (auto) | Anonymized subset of prod | Weekly |
| **Staging** | QA pipeline success | QA Lead approval | Production-mirror (anonymized) | Per release |
| **Production** | Staging validation pass | Release Manager + PO | Live data | N/A |
| **DR** | Production deploy | Auto-replicated | Replicated from prod | Continuous |

---

## Snippet: Release Governance Template

### Go/No-Go Checklist

| # | Criteria | Status | Owner |
|---|---|---|---|
| 1 | All P1/P2 defects resolved | [ ] Pass / [ ] Fail | QA Lead |
| 2 | Security scan — 0 critical/high | [ ] Pass / [ ] Fail | Security |
| 3 | Performance test — within SLA targets | [ ] Pass / [ ] Fail | SRE |
| 4 | UAT sign-off received | [ ] Pass / [ ] Fail | Product Owner |
| 5 | Rollback plan documented and tested | [ ] Pass / [ ] Fail | DevOps Lead |
| 6 | Monitoring/alerting configured for new features | [ ] Pass / [ ] Fail | SRE |
| 7 | Release notes prepared | [ ] Pass / [ ] Fail | Delivery Manager |
| 8 | Stakeholder notification sent | [ ] Pass / [ ] Fail | Program Manager |
| 9 | Compliance artifacts generated (if regulated) | [ ] Pass / [ ] Fail | QA Lead |
| **Decision** | **[ ] GO / [ ] NO-GO** | | Release Manager |
