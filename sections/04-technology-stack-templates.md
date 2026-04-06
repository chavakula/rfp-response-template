# Section: Technology Stack Templates by Cloud Provider

> **Usage:** Select the appropriate cloud provider block. Copy into Section 4.2 of the master template.

---

## Microsoft Azure Stack

| Layer | Technology | Rationale |
|---|---|---|
| **Cloud Platform** | Microsoft Azure | [Enterprise integration / Compliance certifications / Client preference] |
| **Container Orchestration** | Azure Kubernetes Service (AKS) | Managed K8s with Azure AD integration, KEDA autoscaling, Azure Policy |
| **Primary Database** | Azure Database for PostgreSQL — Flexible Server | Zone-redundant HA, read replicas, 99.99% SLA, open-source portability |
| **NoSQL / Document DB** | Azure Cosmos DB | Global distribution, multi-model, automatic indexing |
| **Time-Series DB** | Azure Data Explorer (ADX) | Columnar store optimized for telemetry; Kusto (KQL) query language |
| **Cache** | Azure Cache for Redis | Session state, API response caching, pub/sub |
| **Message Broker** | Azure Event Hubs / Service Bus | Event Hubs for streaming; Service Bus for transactional messaging |
| **Stream Processing** | Azure Stream Analytics | Window-based processing, late-arrival handling, SQL-like syntax |
| **IoT Platform** | Azure IoT Hub + DPS | Device lifecycle, zero-touch provisioning, D2C/C2D messaging |
| **API Gateway** | Azure API Management (APIM) | Rate limiting, developer portal, OAuth integration, API versioning |
| **CDN / Global LB** | Azure Front Door | Anycast, WAF, SSL offload, health-probe-based routing |
| **Frontend** | React + TypeScript + Vite | Component ecosystem, TypeScript safety, fast builds |
| **Identity** | Microsoft Entra ID + B2C | Enterprise SSO (Entra), consumer self-service (B2C), MFA, Conditional Access |
| **Authorization** | Open Policy Agent (OPA) | Decoupled policy-as-code, object-level RBAC, Rego language |
| **IaC** | Terraform + Helm | Cloud-agnostic state management, Helm for K8s packaging |
| **CI/CD** | Azure DevOps Pipelines | YAML pipelines, artifact management, board integration |
| **Monitoring** | Azure Monitor + Application Insights | Distributed tracing, metrics, log analytics, workbooks |
| **SIEM** | Microsoft Sentinel | Cloud-native SIEM+SOAR, AI-driven threat detection, Entra integration |
| **AI Security** | Microsoft Security Copilot | Natural-language threat hunting, automated triage, compliance posture |
| **Analytics** | Azure Synapse Analytics + Data Lake Gen2 | Serverless SQL, Spark, Power BI integration, medallion architecture |
| **ETL / Orchestration** | Azure Data Factory | Managed ETL, 90+ connectors, pipeline orchestration |
| **Secret Management** | Azure Key Vault (Premium/HSM) | HSM-backed keys, certificate management, secret rotation |

---

## Amazon Web Services (AWS) Stack

| Layer | Technology | Rationale |
|---|---|---|
| **Cloud Platform** | Amazon Web Services (AWS) | [Market maturity / Service breadth / Client preference] |
| **Container Orchestration** | Amazon EKS | Managed K8s, Karpenter autoscaler, IAM integration |
| **Serverless Compute** | AWS Lambda + Step Functions | Event-driven processing, workflow orchestration |
| **Primary Database** | Amazon Aurora PostgreSQL | MySQL/PostgreSQL compatible, auto-scaling storage, global database |
| **NoSQL / Document DB** | Amazon DynamoDB | Single-digit ms latency, auto-scaling, global tables |
| **Time-Series DB** | Amazon Timestream | Purpose-built time-series, auto-tiering (memory → magnetic) |
| **Cache** | Amazon ElastiCache (Redis) | Session caching, real-time leaderboards, pub/sub |
| **Message Broker** | Amazon MSK / SQS + SNS | MSK for Kafka workloads; SQS/SNS for decoupled messaging |
| **Stream Processing** | Amazon Kinesis Data Analytics | Real-time stream processing with SQL or Apache Flink |
| **IoT Platform** | AWS IoT Core + Greengrass | Device shadows, rules engine, edge computing |
| **API Gateway** | Amazon API Gateway | HTTP/REST/WebSocket APIs, throttling, usage plans |
| **CDN / Global LB** | Amazon CloudFront + ALB | Global edge delivery, WAF integration, sticky sessions |
| **Frontend** | React + TypeScript + Vite | Same as Azure — framework-agnostic |
| **Identity** | Amazon Cognito | User pools (B2C), identity pools (federated), MFA, OAuth |
| **Authorization** | Amazon Verified Permissions / OPA | Cedar policy language (Verified Permissions) or OPA for portability |
| **IaC** | Terraform / AWS CDK | Terraform for multi-cloud; CDK for AWS-native TypeScript IaC |
| **CI/CD** | GitHub Actions / AWS CodePipeline | GitHub Actions for flexibility; CodePipeline for AWS-native |
| **Monitoring** | Amazon CloudWatch + X-Ray | Metrics, logs, distributed tracing, anomaly detection |
| **SIEM** | AWS GuardDuty + Security Hub | Threat detection, centralized finding aggregation, compliance checks |
| **Analytics** | Amazon Redshift + S3 Data Lake | Serverless Redshift, Glue catalog, Athena ad-hoc queries |
| **ETL / Orchestration** | AWS Glue + Step Functions | Serverless ETL, Spark-based, workflow orchestration |
| **Secret Management** | AWS Secrets Manager + KMS | Automatic rotation, KMS for encryption key management |

---

## Google Cloud Platform (GCP) Stack

| Layer | Technology | Rationale |
|---|---|---|
| **Cloud Platform** | Google Cloud Platform (GCP) | [Data/AI strength / Kubernetes heritage / Client preference] |
| **Container Orchestration** | Google Kubernetes Engine (GKE) | Autopilot mode, multi-cluster mesh, GKE Enterprise |
| **Serverless Compute** | Cloud Run + Cloud Functions | Fully managed containers (Run), event-driven (Functions) |
| **Primary Database** | Cloud SQL (PostgreSQL) / AlloyDB | Cloud SQL for standard; AlloyDB for high-performance PostgreSQL |
| **NoSQL / Document DB** | Firestore / Cloud Bigtable | Firestore for documents; Bigtable for wide-column (IoT/time-series) |
| **Time-Series DB** | Cloud Bigtable | Wide-column store suitable for time-series at massive scale |
| **Cache** | Memorystore (Redis) | Managed Redis, sub-ms latency |
| **Message Broker** | Cloud Pub/Sub | Global messaging, exactly-once delivery, dead-letter topics |
| **Stream Processing** | Dataflow (Apache Beam) | Unified batch+stream, auto-scaling, Apache Beam portability |
| **API Gateway** | Apigee | Enterprise API management, developer portal, monetization |
| **CDN / Global LB** | Cloud CDN + Global Load Balancer | Anycast IP, SSL, Cloud Armor WAF |
| **Frontend** | React + TypeScript + Vite | Framework-agnostic |
| **Identity** | Identity Platform (Firebase Auth) | Multi-provider, MFA, phone auth, anonymous auth |
| **IaC** | Terraform | Cloud-agnostic, strong GCP provider |
| **CI/CD** | Cloud Build / GitHub Actions | Cloud Build for GCP-native; GitHub Actions for multi-platform |
| **Monitoring** | Cloud Monitoring + Cloud Trace | Operations suite, SLO monitoring, error reporting |
| **SIEM** | Chronicle / Security Command Center | Google-scale threat detection, SOAR |
| **Analytics** | BigQuery + Looker | Serverless analytics, ML integration (BQML), Looker BI |
| **ETL / Orchestration** | Dataflow + Cloud Composer (Airflow) | Beam-based ETL, managed Airflow for orchestration |
| **Secret Management** | Secret Manager + Cloud KMS | Automatic rotation, CMEK/CSEK support |

---

## Multi-Cloud / Hybrid Stack (Cloud-Agnostic)

| Layer | Technology | Rationale |
|---|---|---|
| **Container Orchestration** | Kubernetes (vanilla / managed per cloud) | Portable across all clouds |
| **Service Mesh** | Istio / Linkerd | Cross-cloud traffic management, mTLS, observability |
| **Primary Database** | PostgreSQL (managed per cloud) | Available as managed service on all 3 clouds |
| **Message Broker** | Apache Kafka (Confluent Cloud) | Cloud-agnostic managed Kafka |
| **IaC** | Terraform | Multi-provider support |
| **CI/CD** | GitHub Actions | Cloud-agnostic, marketplace ecosystem |
| **Monitoring** | Datadog / Grafana Cloud | Multi-cloud observability |
| **Identity** | Okta / Auth0 | Cloud-agnostic IdP |
| **Secret Management** | HashiCorp Vault | Cloud-agnostic secrets, PKI, dynamic credentials |
