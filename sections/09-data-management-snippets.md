# Section 9: Data Management & Analytics — Reusable Snippets

> **Usage:** Select the data architecture pattern and pipeline template matching the project. Adapt storage selections to the chosen cloud provider.

---

## Snippet: Data Architecture Patterns

### Pattern 1: Medallion Architecture (Lakehouse)

```
Bronze (Raw) → Silver (Cleaned) → Gold (Business-Ready)
```

| Layer | Purpose | Storage | Format | Retention |
|---|---|---|---|---|
| **Bronze** | Raw ingestion, immutable | Data Lake / S3 | JSON, Avro, Parquet | [X] years (regulatory) |
| **Silver** | Validated, deduplicated, enriched | Data Lake / S3 | Parquet (partitioned) | [X] years |
| **Gold** | Aggregated, business metrics, serving | Data Warehouse / Synapse / Redshift | Star schema / Parquet | [X] years |

### Pattern 2: Domain-Driven Multi-Model

| Domain | Data Model | Storage | Why This Store |
|---|---|---|---|
| **Transactional / Master** | Relational | PostgreSQL / Aurora | ACID, referential integrity, joins |
| **Time-Series / Telemetry** | Columnar | ADX / TimescaleDB / Timestream | Fast time-windowed queries, compression |
| **Documents / Content** | Document | Cosmos DB / DynamoDB / MongoDB | Schema flexibility, nested objects |
| **Search** | Inverted index | Elasticsearch / OpenSearch | Full-text search, faceting |
| **Cache** | Key-Value | Redis / Memcached | Sub-ms latency, session state |
| **Analytics** | OLAP | Synapse / Redshift / BigQuery | Large aggregations, BI serving |

### Pattern 3: Event Sourcing + CQRS

| Component | Purpose | Technology |
|---|---|---|
| **Event Store** | Immutable append-only log | Event Hubs / Kafka / EventStoreDB |
| **Command Side** | Write model, validates business rules | Microservice + PostgreSQL |
| **Query Side** | Read-optimized projections | Read replica / Redis / Elasticsearch |
| **Projector** | Builds read models from events | Stream processor / Azure Functions / Lambda |

---

## Snippet: Data Pipeline Templates

### Real-Time Streaming Pipeline

```
Source → Ingestion → Processing → Storage → Serving
```

| Stage | Azure | AWS | GCP |
|---|---|---|---|
| **Source** | IoT Hub / Event Grid | IoT Core / EventBridge | Cloud IoT / Pub/Sub |
| **Ingestion** | Event Hubs | Kinesis Data Streams | Pub/Sub |
| **Processing** | Stream Analytics / Azure Functions | Kinesis Data Analytics / Lambda | Dataflow (Beam) |
| **Storage** | ADX / Data Lake Gen2 | Timestream / S3 | Bigtable / BigQuery |
| **Serving** | Synapse Serverless / Power BI | Athena / QuickSight | BigQuery / Looker |

### Batch ETL Pipeline

| Stage | Azure | AWS | GCP |
|---|---|---|---|
| **Extract** | Data Factory | Glue / Step Functions | Cloud Composer |
| **Transform** | Databricks / Synapse Spark | Glue / EMR | Dataproc / Dataflow |
| **Load** | Synapse / PostgreSQL | Redshift / Aurora | BigQuery |
| **Orchestrate** | Data Factory / Logic Apps | Step Functions / MWAA | Cloud Composer (Airflow) |
| **Catalog** | Purview | Glue Data Catalog | Data Catalog |

---

## Snippet: Data Governance Framework

| Practice | Implementation | Tools |
|---|---|---|
| **Data Catalog** | Automated discovery and classification of data assets | [Purview / Glue Catalog / Data Catalog] |
| **Data Lineage** | End-to-end tracking: source → transform → destination | [Purview / OpenLineage / custom metadata] |
| **Data Quality** | Validation rules at ingestion: schema, type, range, null, uniqueness | [Great Expectations / dbt tests / custom validators] |
| **Data Classification** | Automated PII/PHI detection and tagging | [Purview / Macie / DLP API] |
| **Access Control** | Column-level / row-level security based on user role | [Column masking / RLS policies / OPA] |
| **Retention & Lifecycle** | Automated Hot→Cool→Archive→Delete based on policy | [Lifecycle management policies] |
| **Anonymization** | De-identification for analytics, dev/test | [Presidio / custom anonymization pipeline] |
| **Master Data** | Golden record management, dedup, entity resolution | [Custom MDM / Informatica / Talend] |

---

## Snippet: Reporting & Visualization Matrix

| Audience | Dashboard Type | Refresh Rate | Tool | Key Metrics |
|---|---|---|---|---|
| **Executive / C-Suite** | Strategic KPI dashboard | Daily / Weekly | [Power BI / QuickSight / Looker] | Revenue, growth, costs, SLA summary |
| **Operations** | Real-time operational dashboard | Real-time (< 1 min) | [Grafana / custom React] | System health, pipeline status, alerts |
| **Analysts** | Self-service analytics | On-demand | [Power BI / Superset / Tableau] | Ad-hoc queries, cohort analysis |
| **Compliance** | Audit & compliance reports | Monthly | [PDF export / Power BI / custom] | Access logs, encryption status, policy compliance |
| **Engineering** | SRE / DevOps dashboard | Real-time | [Grafana / Azure Dashboards] | DORA metrics, SLIs, error budgets |
