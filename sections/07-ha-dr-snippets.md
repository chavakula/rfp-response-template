# Section 7: HA/DR — Reusable Snippets

> **Usage:** Select the DR strategy matching the client's RPO/RTO requirements. Adapt failover procedures to the chosen cloud provider.

---

## Snippet: DR Strategy Options

### Option A: Active-Active (Multi-Region)

| Attribute | Detail |
|---|---|
| **Best For** | Mission-critical, zero-tolerance for downtime |
| **RPO** | 0 – < 10 seconds |
| **RTO** | < 60 seconds |
| **Cost** | Highest (~2× infrastructure) |
| **Architecture** | Both regions serve live traffic simultaneously; global load balancer distributes requests; synchronous or near-synchronous replication |
| **Database** | PostgreSQL bi-directional replication / Cosmos DB multi-write / Aurora Global / CockroachDB |
| **When to Use** | Financial transactions, life-safety systems, real-time operations |

### Option B: Active-Passive (Warm Standby)

| Attribute | Detail |
|---|---|
| **Best For** | Business-critical applications with some downtime tolerance |
| **RPO** | < 30 seconds – 5 minutes |
| **RTO** | 5 – 30 minutes |
| **Cost** | Moderate (~1.4× infrastructure) |
| **Architecture** | Primary region serves traffic; DR region runs at reduced capacity; async replication; health-probe-triggered failover |
| **Database** | Read replicas in DR region; promote on failover |
| **When to Use** | SaaS platforms, healthcare, enterprise applications |

### Option C: Pilot Light

| Attribute | Detail |
|---|---|
| **Best For** | Cost-sensitive applications with moderate downtime tolerance |
| **RPO** | 5 – 30 minutes |
| **RTO** | 30 min – 2 hours |
| **Cost** | Lower (~1.15× infrastructure) |
| **Architecture** | Only core services (DB, storage) replicated to DR; compute infrastructure defined in IaC, provisioned on demand during failover |
| **Database** | Async replication; data is current, compute is not |
| **When to Use** | Internal tools, batch processing, non-customer-facing |

### Option D: Backup & Restore (Cold Standby)

| Attribute | Detail |
|---|---|
| **Best For** | Non-critical, cost-minimized applications |
| **RPO** | 1 – 24 hours |
| **RTO** | 4 – 24 hours |
| **Cost** | Minimal (storage only in DR) |
| **Architecture** | Periodic backups to cross-region storage; full rebuild from IaC + restore from backup on disaster |
| **Database** | Point-in-time backups; manual restore |
| **When to Use** | Dev/test, archives, batch analytics |

---

## Snippet: Failover Procedure Template

### Automated Failover (Active-Active / Active-Passive)

1. Health probes detect primary region failure (3 consecutive failures, ~[X] seconds)
2. Global load balancer ([Front Door / CloudFront / Global LB]) routes traffic to DR region
3. Message broker geo-DR activates (Event Hubs paired namespace / MSK multi-region)
4. [IoT Hub DPS / IoT Core] redirects device connections to DR endpoint
5. Database promoted ([read replica promotion / global database failover])
6. Monitoring validates DR region is serving traffic (synthetic tests pass)
7. Alert notification sent to on-call team: "Failover completed at [TIMESTAMP]"

### Manual Failover (Pilot Light / Cold)

1. Alert fires: primary region unresponsive for > [X] minutes
2. Incident commander confirms outage (not transient)
3. Terraform/IaC applies DR infrastructure ([X] minutes to provision)
4. Database restored from latest backup / replica promoted
5. DNS updated (TTL-aware; propagation time ~[X] minutes)
6. Smoke tests executed against DR endpoints
7. Traffic admitted after all smoke tests pass
8. Incident communication sent to stakeholders

### Failback Procedure

1. Primary region infrastructure validated (health checks, data integrity)
2. Data synchronization: DR → Primary (replication reversal or export/import)
3. Traffic shifted gradually: 10% → 50% → 100% (monitored at each step)
4. DR region returned to standby mode
5. Post-incident review: timeline, data integrity, lessons learned

---

## Snippet: DR Testing Plan Template

| Test Type | Frequency | Scope | Duration | Success Criteria | CMMI L5 Metric |
|---|---|---|---|---|---|
| **Tabletop Exercise** | Quarterly | All teams review procedures | 2 hours | Procedures validated, gaps documented | Gaps found per exercise (trend ↓) |
| **Component Failover** | Monthly | Individual services | 1 hour | Service recovers within RTO | Actual RTO vs. target (SPC chart) |
| **Full DR Drill** | Semi-annually | End-to-end failover | 4 hours | All services in DR within RTO, data integrity confirmed | Drill success rate (target 100%) |
| **Chaos Engineering** | Monthly | Production (controlled blast) | Varies | System self-heals; no customer impact | Auto-recovery rate (target > 95%) |
| **Data Recovery Test** | Quarterly | Backup restore validation | 2 hours | Data restored, integrity check passes | Restore time vs. target |
