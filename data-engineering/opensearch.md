# Amazon OpenSearch – Deep Dive (SAA-C03 + Practical Use Cases)

## Memory Hook  
- “OpenSearch = search engine + analytics on steroids”  
- “Log, search, analyze, and visualize — all in one AWS-native stack”

---

## ✅ What Is Amazon OpenSearch?

> OpenSearch is a **managed, open-source fork of Elasticsearch** (after license changes in 2021)  
> Used for **search, log analytics, observability**, and **real-time dashboards** (with OpenSearch Dashboards)

---

## ✅ Core Features

| Feature                       | Description                                         |
|-------------------------------|-----------------------------------------------------|
| **Full-Text Search**          | ✅ Tokenized keyword search + scoring               |
| **Structured + Unstructured Data Support** | ✅ JSON, logs, metrics               |
| **OpenSearch Dashboards**     | Visual dashboard for analytics                     |
| **Log + Metrics Aggregation** | ✅ Ingest from CloudWatch, Kinesis, Firehose        |
| **Streaming Ingest**          | ✅ Supports near real-time via Lambda/Kinesis/Logstash |
| **In-place querying**         | ✅ Fast over structured + nested documents          |
| **Alerts + Monitors**         | Built-in notification system                        |
| **Multi-tenancy**             | Optional via fine-grained access control           |

---

## 🔍 How OpenSearch Works

- Ingests JSON documents
- Documents are **indexed** and stored across **shards**
- Queries are distributed across shards and aggregated

🧠 Query Types:
- `match`, `term`, `range`, `bool`, `nested`
- `aggregations`, `filters`, `facets`

---

## ✅ Integration with AWS Services

| Service                  | Use Case                                                 |
|---------------------------|-----------------------------------------------------------|
| **Amazon Kinesis Firehose** | Stream logs directly into OpenSearch (managed delivery) |
| **Lambda**                | Custom transformation or pre-processing                  |
| **CloudWatch Logs**       | Stream logs to OpenSearch for observability              |
| **S3**                    | Source for batch index jobs using custom ETL             |
| **IAM + Cognito**         | Fine-grained role-based access                           |
| **OpenSearch Dashboards** | Visual frontend for analytics and search                 |

---

## 🔐 Security & Access Control

- **IAM Policies** for resource-level access
- **Fine-Grained Access Control** (optional plugin)
  - Field-level permissions
  - Document-level filters
- **VPC support** for private access
- **KMS** for encryption at rest
- **HTTPS / TLS** for encryption in transit

---

## ✅ OpenSearch Use Cases

| Use Case                           | Why OpenSearch Works                                 |
|------------------------------------|-------------------------------------------------------|
| **Log analytics** (e.g., ELK stack)| ✅ Fast ingestion + querying + visual dashboards      |
| **App search** (e.g., products, docs) | ✅ Full-text, scoring, relevance, filters         |
| **Security analytics**             | ✅ Real-time alerts on log anomalies                  |
| **Observability**                  | ✅ Query logs + metrics in unified dashboard          |
| **E-commerce personalization**     | ✅ Filterable, ranked search                          |

---

## 💰 Pricing Model

| Resource Charged                   | Detail                                        |
|------------------------------------|-----------------------------------------------|
| **Instance hours**                 | Per OpenSearch node (e.g., m5.large.search)   |
| **Data storage**                   | On attached EBS volumes                       |
| **Snapshots**                      | Charged in S3                                 |
| **Data transfer**                  | Intra-region is free; cross-region costs      |
| **Dedicated Master Nodes**         | Separate billing                              |

🧠 Consider:
- UltraWarm = low-cost read-only storage (for infrequent queries)
- Cold Tier = even cheaper, no search unless restored

---

## ✅ OpenSearch Storage Tiers

| Tier        | Use Case                               | Cost            | Latency       |
|-------------|------------------------------------------|------------------|----------------|
| **Hot**     | Real-time, high-QPS analytics            | 💰 Highest      | ✅ Fastest     |
| **UltraWarm**| Historical data, daily queries           | 💸 Mid          | ⚠️ Medium     |
| **Cold**    | Archive logs, retention compliance       | 🪙 Cheapest      | ❌ Must restore|

---

## 📌 Exam Pointers

- “Need real-time, low-latency search over JSON documents?” → ✅ OpenSearch
- “Need to visualize logs ingested from Firehose?” → ✅ OpenSearch Dashboards
- “Secure OpenSearch access per user/team?” → ✅ IAM + Cognito + Fine-Grained Access
- “Index historical logs, low-frequency access?” → ✅ Use UltraWarm or Cold Tier
- “Want to run a managed search engine over log data?” → ✅ OpenSearch Service
- “Need to stream application logs into a search index?” → ✅ Firehose → OpenSearch
