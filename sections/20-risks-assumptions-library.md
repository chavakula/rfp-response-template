# Risk Register Template — Common RFP Risks

> **Usage:** Select applicable risks from the categories below. Customize probability/impact based on the specific engagement. Copy into Section 20.3 of the master template.

---

## Technical Risks

| # | Risk | Probability | Impact | Mitigation | Owner |
|---|---|---|---|---|---|
| T1 | Legacy system integration complexity exceeds estimates | Medium | High | Early integration spike in Phase 1; dedicated integration test environment; API contract testing | Tech Lead |
| T2 | Cloud service limitations discovered during build | Low | High | PoC key services in Phase 0; maintain alternative technology options in ADRs | Cloud Architect |
| T3 | Performance targets not met at scale | Medium | High | Performance testing from Sprint 1; load test in production-like environment; auto-scaling validation | SRE Lead |
| T4 | Data migration complexity (volume, quality, mapping) | High | High | Data profiling in Phase 0; pilot migration in Phase 2; automated validation scripts; rollback plan | Data Engineer |
| T5 | Third-party API changes or deprecations | Medium | Medium | API version pinning; contract testing; abstraction layer to isolate dependencies | Tech Lead |
| T6 | Technology stack skill ramp-up takes longer than expected | Medium | Medium | Training sprint in Phase 0; pair programming; leverage reusable accelerators | Delivery Manager |

## Organizational / People Risks

| # | Risk | Probability | Impact | Mitigation | Owner |
|---|---|---|---|---|---|
| O1 | Key personnel attrition during engagement | Medium | High | Contractual lock-in for key roles; knowledge workshops; documented decision records (ADRs); shadow resources identified | Engagement Director |
| O2 | Client SME availability insufficient | Medium | High | Define SME time commitment in SOW; pre-schedule workshops; async Q&A channel; escalation to Steering Committee | Delivery Manager |
| O3 | Scope creep due to evolving requirements | High | High | Change control process; bi-weekly scope review; fixed-price phases with defined scope; change request budget reserve | Program Manager |
| O4 | Split team across time zones causes communication delays | Medium | Medium | 4-hour overlap window; async standups; recorded design sessions; shared documentation | Scrum Master |

## Compliance & Regulatory Risks

| # | Risk | Probability | Impact | Mitigation | Owner |
|---|---|---|---|---|---|
| C1 | Regulatory requirements change during build | Low | High | Quarterly regulatory scan; compliance architect on retainer; modular architecture allows isolated changes | Security Architect |
| C2 | Compliance certification delays (SOC 2, HITRUST, etc.) | Medium | Medium | Start audit preparation in Phase 3; engage auditor early; automated evidence collection | Security Architect |
| C3 | Data residency requirements conflict with architecture | Low | High | Confirm data residency requirements in Phase 0; multi-region architecture with policy-based routing from Day 1 | Cloud Architect |
| C4 | Security vulnerability discovered in production | Medium | High | Automated scanning in CI/CD; vulnerability SLA (critical < 24 hrs fix); bug bounty program consideration | Security Architect |

## External / Dependency Risks

| # | Risk | Probability | Impact | Mitigation | Owner |
|---|---|---|---|---|---|
| E1 | Cloud provider service outage during critical phase | Low | High | Multi-AZ/multi-region architecture; DR plan tested before go-live; SLA credits negotiated | Cloud Architect |
| E2 | Vendor tool license changes or price increases | Low | Medium | Prefer open-source where quality equivalent; avoid deep vendor coupling; IaC portability | Solution Architect |
| E3 | Client infrastructure provisioning delays | Medium | High | Define provisioning timeline in dependencies table; pre-provision dev environment; escalation process | Delivery Manager |
| E4 | Dependent system (EHR, ERP, CRM) integration delays | Medium | High | Mock services for development; contract-first API design; integration testing with stubs; define hard dates in SOW | Tech Lead |

---

## Common Assumptions (Select Applicable)

| # | Category | Assumption |
|---|---|---|
| A1 | Access | Client will provide timely access to SMEs, systems, and environments within [X] business days of request |
| A2 | Infrastructure | Cloud subscription(s) will be provisioned and accessible before Phase 1 start |
| A3 | Data | Client will provide representative test data (anonymized if PHI/PII) within Phase 1 |
| A4 | Integrations | Third-party system APIs are documented and available in test environments |
| A5 | Compliance | Regulatory submissions and filings are the client's responsibility; we provide supporting documentation |
| A6 | Scope | Hardware, firmware, and physical device development are out of scope |
| A7 | Hosting | Cloud infrastructure costs are borne by the client (pass-through, not included in our pricing) |
| A8 | Change | Changes to agreed scope will follow the change control process and may impact timeline/cost |
| A9 | Licensing | Client will procure necessary third-party software licenses (databases, IdP, monitoring tools) |
| A10 | Network | Client will provide VPN / ExpressRoute / Direct Connect access to on-premises systems if required |
