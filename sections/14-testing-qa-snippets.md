# Section 14: Testing & Quality Assurance — Reusable Snippets

> **Usage:** Select applicable testing levels and tools. Populate CMMI L5 baselines with actual organizational data.

---

## Snippet: Testing Tool Matrix by Cloud / Stack

### Azure + .NET / Node.js Stack

| Test Level | Tool | CI/CD Integration | License |
|---|---|---|---|
| Unit | xUnit / Jest / pytest | Azure Pipelines | Open Source |
| Integration | RestAssured / Supertest / Pact | Azure Pipelines | Open Source |
| E2E / UI | Playwright / Cypress | Azure Pipelines (containerized) | Open Source |
| Performance | k6 / Azure Load Testing | Azure Pipelines + Load Testing service | Open Source + Azure |
| Security (SAST) | SonarQube / Semgrep | Pipeline stage | Open Source / Commercial |
| Security (DAST) | OWASP ZAP | Pipeline stage | Open Source |
| Security (SCA) | Snyk / Trivy / Dependabot | Pipeline stage | Open Source / Commercial |
| Container Scan | Trivy / Microsoft Defender | Pipeline + registry scan | Open Source / Azure |
| Accessibility | axe-core / Lighthouse | Pipeline stage | Open Source |
| API Contract | Pact / Schemathesis | Pipeline stage | Open Source |

### AWS + Java / Node.js Stack

| Test Level | Tool | CI/CD Integration | License |
|---|---|---|---|
| Unit | JUnit 5 / Jest / pytest | GitHub Actions / CodePipeline | Open Source |
| Integration | REST Assured / Testcontainers | GitHub Actions | Open Source |
| E2E / UI | Playwright / Selenium | GitHub Actions (containerized) | Open Source |
| Performance | Gatling / k6 | GitHub Actions | Open Source |
| Security (SAST) | SonarQube / CodeGuru | Pipeline stage | Open Source / AWS |
| Security (DAST) | OWASP ZAP / Burp Suite | Pipeline stage | Open Source / Commercial |
| Security (SCA) | Snyk / npm audit / Safety | Pipeline stage | Open Source / Commercial |
| Container Scan | Trivy / ECR scanning | Pipeline + registry | Open Source / AWS |
| Accessibility | axe-core / pa11y | Pipeline stage | Open Source |

---

## Snippet: Test Automation Pyramid

```
          /  E2E Tests  \        ← Few: 5-10% (critical user journeys)
         /  Integration  \       ← Moderate: 20-30% (API contracts, service interactions)
        /   Unit Tests    \      ← Many: 60-70% (business logic, functions)
       /  Static Analysis  \     ← Always: SAST, linting, type checking
```

| Level | What We Test | Speed | Count | Ownership |
|---|---|---|---|---|
| **Static** | Code quality, security, types | Seconds | All files | Developers (pre-commit) |
| **Unit** | Functions, classes, business logic | Seconds | [X]000+ | Developers |
| **Integration** | Service-to-service, DB queries, API contracts | Minutes | [X]00+ | Developers + QA |
| **E2E** | Full user workflows, cross-service | Minutes | [X]0–[X]00 | QA |
| **Performance** | Load, stress, endurance | Hours | [X]0 scenarios | QA + SRE |
| **Security** | Vulnerabilities, pen test | Hours–Days | As scheduled | Security team |

---

## Snippet: Performance Test Scenarios Template

| # | Scenario | Type | Target | Duration | Success Criteria |
|---|---|---|---|---|---|
| 1 | Normal load — typical business day | Load | [X] concurrent users, [Y] req/sec | 1 hour | P95 < [X]ms, 0 errors |
| 2 | Peak load — highest expected traffic | Load | [X × 2] concurrent users | 30 min | P95 < [X]ms, < 0.1% errors |
| 3 | Stress test — beyond peak | Stress | [X × 3–5] concurrent users | 15 min | System degrades gracefully; no crashes |
| 4 | Endurance — sustained load | Soak | [X] concurrent users | 8–24 hours | No memory leaks, stable response times |
| 5 | Spike — sudden traffic burst | Spike | 0 → [X × 5] in 30 seconds | 5 min | Auto-scale responds; recovery < 2 min |
| 6 | Data volume — large dataset queries | Volume | [X] TB dataset, complex queries | 1 hour | P95 query < [X]s |

---

## Snippet: Regulatory Test Artifacts (Healthcare / Medical)

| Artifact | Standard | Auto-Generated? | Content |
|---|---|---|---|
| **Requirements Traceability Matrix (RTM)** | IEC 62304 §5.1 | Yes (CI/CD) | Req ID → Design → Code → Test Case → Test Result |
| **Software Bill of Materials (SBOM)** | FDA/EU MDR | Yes (per build) | All dependencies, versions, licenses (CycloneDX/SPDX) |
| **Unit Test Report** | IEC 62304 §5.5 | Yes (CI/CD) | Pass/fail, coverage, execution time |
| **Integration Test Report** | IEC 62304 §5.6 | Yes (CI/CD) | API contract results, service interaction verification |
| **Code Review Evidence** | IEC 62304 §5.5 | Yes (Git platform) | PR approvals, review comments, resolution |
| **Static Analysis Report** | IEC 62304 §5.5 | Yes (CI/CD) | SAST findings, severity, resolution status |
| **SOUP Analysis** | IEC 62304 §8 | Semi-auto | Software of Unknown Provenance: risk assessment per dependency |
| **Risk File Traceability** | ISO 14971 | Manual + tooling | Hazard → Risk Control → Verification → Residual Risk |
| **Release Notes** | IEC 62304 §6.1 | Yes (CI/CD) | Version, changes, known issues, validation evidence |
