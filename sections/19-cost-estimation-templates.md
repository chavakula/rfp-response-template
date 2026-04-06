# Section: Cost Proposal — Estimation Templates

> **Usage:** Select the applicable infrastructure cost template and sizing model. These provide realistic starting points that should be adjusted based on actual requirements.

---

## Azure Infrastructure Sizing Guide

### Small Platform (< 100K users, single region)

| Service | SKU | Monthly Est. | Notes |
|---|---|---|---|
| AKS | 3× D4s v5 (4 vCPU, 16 GB) | $620 | 2 AZs, HPA enabled |
| PostgreSQL Flexible | GP D2s v3, 64 GB, HA | $195 | Zone-redundant |
| Redis Cache | Standard C1 (1 GB) | $80 | API caching |
| Blob Storage | LRS Hot, 500 GB | $9 | Application assets |
| API Management | Developer/Standard, 1 unit | $50–680 | Dev for PoC, Standard for prod |
| Front Door | Standard | $35+ | CDN + WAF |
| App Gateway WAF v2 | 2 instances | $580 | Regional LB + WAF |
| Key Vault | Standard | $3 | Secrets, certs |
| Monitor + App Insights | 10 GB/day | $830 | Distributed tracing, logs |
| **Monthly Total** | | **$2,400–$3,000** | |
| **Annual (with RI -30%)** | | **~$22,000** | |

### Medium Platform (100K–500K users, 2 regions)

| Service | SKU | Monthly Est. | Notes |
|---|---|---|---|
| AKS (Primary) | 6× D8s v5 (8 vCPU, 32 GB), 3 AZs | $3,120 | HA with pod anti-affinity |
| AKS (Secondary) | 4× D8s v5, 2 AZs | $2,080 | Data residency region |
| PostgreSQL (Primary) | GP D4s v3, 256 GB, HA + 1 read replica | $1,170 | Zone-redundant + reporting replica |
| PostgreSQL (Secondary) | GP D4s v3, 128 GB, HA | $780 | Regional data residency |
| Redis Cache | Standard C2 (6 GB) | $200 | Per region |
| Blob/Data Lake | LRS, 5–20 TB | $100–400 | Hot + Cool tiers |
| API Management | Standard, 2 units | $1,360 | 1 per region |
| Front Door | Standard | $310 | Global LB + WAF |
| Monitor | 30–50 GB/day | $2,500–4,200 | Commitment tier recommended |
| Sentinel | 10–15 GB/day | $600–900 | SIEM |
| **Monthly Total** | | **$13,000–$16,000** | |
| **Annual (with RI -35%)** | | **~$110,000–$130,000** | |

### Large Platform (500K–1M+ users, 3+ regions)

| Service | Monthly Est. | Notes |
|---|---|---|
| AKS (3 regions) | $6,500–$9,000 | Auto-scaling, 3 AZs each |
| PostgreSQL (3 regions + replicas) | $3,000–$4,500 | HA + read replicas per region |
| ADX / Specialized DB | $4,000–$8,000 | Time-series, telemetry, analytics |
| Event Hubs / Kafka | $500–$2,000 | Throughput-based |
| Stream Processing | $500–$1,500 | SU-based |
| Storage (all tiers) | $500–$2,000 | 50–200 TB across tiers |
| API Management | $2,000–$3,500 | Multi-region |
| Front Door + App Gateways | $1,500–$2,500 | Global + regional |
| Monitor + Sentinel | $5,000–$9,000 | Commitment tiers |
| Synapse / Analytics | $500–$2,000 | Serverless + dedicated pools |
| Supporting (DNS, Bastion, KV, etc.) | $500–$1,000 | Fixed costs |
| **Monthly Total** | | **$25,000–$45,000** |
| **Annual (with RI + Savings Plan)** | | **~$200,000–$380,000** |

---

## AWS Infrastructure Sizing Guide

### Small Platform (< 100K users, single region)

| Service | SKU | Monthly Est. | Notes |
|---|---|---|---|
| EKS | 3× m6i.xlarge (4 vCPU, 16 GB) | $550 | 2 AZs, Karpenter |
| RDS Aurora PostgreSQL | db.r6g.large, Multi-AZ | $400 | Graviton, auto-scaling storage |
| ElastiCache (Redis) | cache.r6g.large | $200 | Cluster mode |
| S3 | Standard, 500 GB | $12 | Intelligent-Tiering |
| API Gateway | HTTP API | $50+ | Pay-per-request |
| CloudFront | Standard | $30+ | CDN + WAF |
| ALB | 1 per AZ | $50 | Application Load Balancer |
| Secrets Manager + KMS | Standard | $10 | Secret rotation |
| CloudWatch + X-Ray | 10 GB/day | $700 | Logs, metrics, traces |
| **Monthly Total** | | **$2,000–$2,500** | |
| **Annual (with Savings Plan -30%)** | | **~$19,000** | |

### Medium Platform (same scale as Azure Medium)

| Service | Monthly Est. | Notes |
|---|---|---|
| EKS (2 regions) | $4,500–$5,500 | Graviton instances, Karpenter |
| Aurora (2 regions, Global Database) | $1,800–$2,400 | Global Database for cross-region |
| DynamoDB (if NoSQL needed) | $500–$1,500 | On-demand or provisioned |
| ElastiCache (2 regions) | $400–$600 | Redis cluster |
| S3 + Data Lake | $100–$400 | Intelligent-Tiering |
| API Gateway | $200–$500 | HTTP/REST APIs |
| CloudFront + ALB | $300–$500 | Global + regional |
| CloudWatch + X-Ray | $2,000–$3,500 | Logs Insights |
| GuardDuty + Security Hub | $300–$600 | Threat detection |
| **Monthly Total** | | **$10,000–$15,000** |
| **Annual (with SP -35%)** | | **~$90,000–$125,000** |

---

## Cost-Per-Unit Benchmarks (From Our Portfolio)

> **CMMI L5 Practice:** These baselines are derived from our organizational process performance data across [N] cloud projects.

| Metric | Small | Medium | Large |
|---|---|---|---|
| **Cost per active user/month** | $0.05–$0.15 | $0.03–$0.08 | $0.02–$0.05 |
| **Cost per device/month (IoT)** | $0.10–$0.25 | $0.05–$0.15 | $0.03–$0.08 |
| **Cost per GB ingested/month** | $0.50–$1.50 | $0.30–$0.80 | $0.15–$0.40 |
| **Cost per API call (M calls)** | $3.50–$5.00 | $1.50–$3.00 | $0.80–$1.50 |

---

## Multi-Year Projection Template

| Component | Year 1 | Year 2 | Year 3 | 3-Year Total |
|---|---|---|---|---|
| Professional Services (Build) | $[X]K | — | — | $[X]K |
| Professional Services (Enhancements) | — | $[X]K | $[X]K | $[X]K |
| Cloud Infrastructure (Optimized) | $[X]K | $[X]K | $[X]K | $[X]K |
| Licensing & Tools | $[X]K | $[X]K | $[X]K | $[X]K |
| Support & Maintenance | — | $[X]K | $[X]K | $[X]K |
| **Annual Total** | **$[X]K** | **$[X]K** | **$[X]K** | **$[X]K** |

**Growth Assumptions:**
- Year 1 → Year 2: [X]× user/device growth → [Y]% infrastructure cost increase
- Year 2 → Year 3: [X]× user/device growth → [Y]% infrastructure cost increase
- Reserved Instance / Savings Plan discount: [30–40]% on compute
- Storage growth: [X] GB/day × 365 × retention years = cumulative storage
