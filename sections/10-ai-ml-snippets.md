# Section 10: AI/ML & Intelligent Automation — Reusable Snippets

> **Usage:** Select applicable AI/ML use cases by industry. Adapt MLOps and Responsible AI sections to the engagement scope.

---

## Snippet: Common AI/ML Use Cases by Industry

### Healthcare & Life Sciences

| # | Use Case | Model Type | Data Source | Business Value |
|---|---|---|---|---|
| 1 | Anomaly detection in device telemetry | Unsupervised (Isolation Forest, Autoencoders) | IoT telemetry stream | Early detection of device malfunction; patient safety |
| 2 | Predictive patient outcomes | Supervised (XGBoost, Random Forest) | Clinical data + device data | Personalized treatment, clinical trial optimization |
| 3 | Clinical NLP — report summarization | GenAI (GPT-4 / fine-tuned LLM) | Clinical notes, radiology reports | Clinician time savings, structured data extraction |
| 4 | Image analysis (X-ray, MRI) | Computer Vision (CNN, Vision Transformer) | Medical imaging (DICOM) | Automated screening, prioritization |
| 5 | Population health risk stratification | Supervised (Logistic Regression, Gradient Boosting) | De-identified patient cohorts | Resource allocation, preventive interventions |

### Financial Services

| # | Use Case | Model Type | Data Source | Business Value |
|---|---|---|---|---|
| 1 | Fraud detection (real-time) | Supervised + Unsupervised ensemble | Transaction stream | Reduce fraud losses by [X]%; sub-second decision |
| 2 | Credit risk scoring | Supervised (LightGBM, Neural Net) | Application data + bureau data | More accurate risk assessment; reduce defaults |
| 3 | Customer churn prediction | Supervised (XGBoost) | Usage, transaction, support data | Proactive retention; reduce churn by [X]% |
| 4 | Document processing (KYC, claims) | GenAI + OCR (Document Intelligence) | Scanned documents, PDFs | Automated extraction; reduce manual processing by [X]% |
| 5 | Conversational AI (customer service) | GenAI (RAG + fine-tuned LLM) | Knowledge base, FAQs, policies | Deflect [X]% of support queries; 24/7 availability |

### Retail & E-Commerce

| # | Use Case | Model Type | Data Source | Business Value |
|---|---|---|---|---|
| 1 | Product recommendation | Collaborative filtering + content-based | Purchase history, browsing | Increase AOV by [X]%, conversion by [Y]% |
| 2 | Demand forecasting | Time-series (Prophet, ARIMA, LSTM) | Sales history, events, weather | Reduce stockouts by [X]%; optimize inventory |
| 3 | Dynamic pricing | Reinforcement learning / optimization | Competitor prices, demand, inventory | Revenue optimization; margin improvement |
| 4 | Visual search | Computer Vision (embedding + kNN) | Product catalog images | Enhanced product discovery |
| 5 | Customer segmentation | Unsupervised (K-Means, DBSCAN) | Transaction + behavioral data | Targeted marketing; improved CX |

### Manufacturing & IoT

| # | Use Case | Model Type | Data Source | Business Value |
|---|---|---|---|---|
| 1 | Predictive maintenance | Supervised (Survival analysis, XGBoost) | Sensor telemetry | Reduce unplanned downtime by [X]% |
| 2 | Quality inspection (visual) | Computer Vision (YOLO, EfficientNet) | Production line cameras | Defect detection accuracy > [X]% |
| 3 | Energy optimization | Reinforcement learning | Smart meter data, weather | Reduce energy costs by [X]% |
| 4 | Supply chain optimization | Operations research + ML | Inventory, logistics, demand | Reduce lead time, optimize routing |

---

## Snippet: MLOps Maturity Model

| Level | Practices | Tooling | Applicable When |
|---|---|---|---|
| **Level 0 — Manual** | Jupyter notebooks, manual deployment, no versioning | Local tools | PoC / exploration only |
| **Level 1 — Basic** | Version-controlled code, automated training, manual deployment | [Azure ML / SageMaker / Vertex AI], Git | Single model, infrequent updates |
| **Level 2 — Managed** | Automated training + deployment, model registry, A/B testing | ML platform + CI/CD, MLflow/Weights&Biases | Multiple models, regular retraining |
| **Level 3 — Optimized** | Automated retraining triggers, drift detection, feature store, governance | Full ML platform + monitoring + feature store | Production-critical ML, continuous learning |

---

## Snippet: MLOps Pipeline Template

| Stage | Activity | Tools | CMMI L5 Metric |
|---|---|---|---|
| **Data Preparation** | Ingestion, feature engineering, validation | [Data Factory / Glue], [Feature Store] | Data quality score per dataset |
| **Experimentation** | Model training, hyperparameter tuning | [Azure ML / SageMaker / Vertex AI] | Experiments per sprint |
| **Evaluation** | Accuracy, precision, recall, F1, AUC-ROC | [MLflow / Weights&Biases] | Model performance vs. baseline |
| **Registry** | Version, stage (dev/staging/prod), lineage | [Azure ML Registry / SageMaker Registry] | Models registered per sprint |
| **Deployment** | Containerized inference, A/B / canary | [AKS / EKS / Cloud Run] | Deployment success rate |
| **Monitoring** | Drift detection, performance tracking | [Azure ML Monitor / Evidently / WhyLabs] | Drift alerts, prediction accuracy |
| **Retraining** | Triggered by drift / scheduled | [Pipeline automation] | Retraining frequency, accuracy recovery time |

---

## Snippet: Responsible AI Framework

| Principle | Implementation | Validation |
|---|---|---|
| **Fairness** | Bias detection (demographic parity, equalized odds) during training; debiasing techniques | Fairlearn / Aequitas audit per model release |
| **Transparency** | Model explainability (SHAP, LIME) for all predictions; feature importance reporting | Explainability report generated per model |
| **Privacy** | Data minimization, differential privacy, anonymization; no PII in features | Privacy impact assessment per use case |
| **Accountability** | Human-in-the-loop for high-stakes decisions; audit trail for all predictions | Decision log with model version, input hash, output |
| **Safety** | Guardrails for generative AI (content filters, PII redaction, hallucination detection) | Red-team testing before production deployment |
| **Reliability** | Model performance SLA; fallback to rules-based system if model degrades | SLA monitoring; automatic fallback trigger |
