# AWS Athena – Deepest Dive (Use Cases, Performance, Federated Queries, File Formats)

## Memory Hook  
- “Athena = SQL over S3”  
- “Serverless, schema-on-read, and shockingly useful when optimized right”

---

## ✅ What Is Athena?

> Athena is a **serverless, interactive query service** to run **SQL queries directly on S3**, without provisioning any infrastructure.

Powered by:
- Presto (distributed SQL engine)
- Integrated with Glue Data Catalog

---

## ✅ Why Use Athena?

| Benefit               | Description                                              |
|------------------------|----------------------------------------------------------|
| ✅ Serverless          | No provisioning or scaling needed                        |
| ✅ SQL Familiarity     | ANSI SQL syntax + complex functions supported            |
| ✅ Pay-per-query       | Billed per **scanned TB** ($5 per TB scanned, compressed) |
| ✅ Fast + Scalable     | Under-the-hood distributed Presto                        |
| ✅ Secure + Governed   | Integrates with Glue Catalog + Lake Formation permissions |
| ✅ Near real-time use  | Supports quick insight from streaming pipelines (S3)     |
| ✅ External sources    | Federated queries into RDS, DynamoDB, JDBC, Redshift     |

---

## ✅ Common Athena Use Cases

| Use Case                                     | Why Athena Works                                  |
|----------------------------------------------|---------------------------------------------------|
| Query structured/unstructured data in S3     | ✅ No data loading, schema-on-read                |
| Log/Clickstream analytics (CloudTrail, ALB)  | ✅ Use partitions + Parquet for blazing speed     |
| Data lake querying (Glue/Lake Formation)     | ✅ Catalog integration, column/row-level security |
| Federated queries into RDS, DynamoDB         | ✅ No need for ETL — query in-place               |
| BI dashboard backend (e.g., QuickSight)      | ✅ Fast ad-hoc analytics                          |
| Ad-hoc analytics in notebooks/Lambda         | ✅ Supports JDBC + SDK-based execution            |

---

## ✅ Performance & Cost Optimization Techniques

| Optimization Area        | Best Practice                                                    |
|---------------------------|------------------------------------------------------------------|
| **Partitioning**          | Organize S3 data into partitioned folders (e.g., `year/month`)  |
| **Columnar Formats**      | Use Parquet/ORC for compression + predicate pushdown            |
| **Compression**           | Use GZIP or Snappy compression                                 |
| **Projection Pushdown**   | Query only necessary columns                                   |
| **Use SELECT LIMIT**      | Avoid scanning entire datasets                                 |
| **CTAS / View Caching**   | Use **Create Table As Select** to pre-cache for repeat queries  |
| **File Size Optimization**| Avoid 10,000 tiny files — aim for 100–500 MB per partition      |
| **Query Scheduling**      | Use **Scheduled Queries** via EventBridge                      |

---

## ✅ Supported File Formats

| Format     | Optimized? | Notes                                 |
|------------|-------------|----------------------------------------|
| **CSV**    | ❌ No       | Uncompressed, largest scan volume     |
| **JSON**   | ❌ No       | No columnar compression               |
| **Parquet**| ✅ Yes      | Best performance + cost               |
| **ORC**    | ✅ Yes      | Good for Hive-originated pipelines    |
| **Avro**   | ✅ Yes      | Schema evolution supported            |
| **TSV**    | ❌ No       | Similar to CSV                        |

🧠 Parquet or ORC = always preferred , can use GLUE to convert from CSV / JSON to Parquet / Avro / ORC

---

## ✅ Federated Query Support

> Athena can run SQL queries on **non-S3 sources** via **data source connectors**

| Supported Source            | Use Case                                 |
|------------------------------|------------------------------------------|
| **RDS / Aurora**             | Query relational DBs (no ETL needed)     |
| **Redshift**                 | Access external Redshift tables          |
| **DynamoDB**                 | SQL over NoSQL data                      |
| **JDBC (MySQL, PostgreSQL)** | Any JDBC-compatible external DB          |
| **CloudWatch Logs / Prometheus** | Operational analytics                |

✅ Setup:
- Use AWS-provided **Lambda connectors**
- Connectors deployed in VPC or public

---

## ✅ Athena + Lambda

| Use Case                               | Behavior                                                 |
|----------------------------------------|-----------------------------------------------------------|
| Scheduled query execution              | Trigger via Lambda → run query → save to S3              |
| Event-driven query                     | New file in S3 triggers Athena via Lambda (EventBridge)  |
| Query orchestration                    | Lambda handles retries, monitors query status            |
| Automation                             | Lambda + SDK → dynamic table creation, result parsing    |

---

## ✅ Security & Access Control

| Mechanism             | Description                                      |
|------------------------|--------------------------------------------------|
| **Glue Catalog Permissions** | IAM or Lake Formation permissions apply     |
| **Lake Formation**    | ✅ Column- and row-level access enforcement       |
| **Encryption**        | ✅ S3 data encrypted with SSE-S3, SSE-KMS         |
| **IAM Policies**      | Control query execution & result bucket access   |
| **VPC Access**        | Use **VPC Interface Endpoint** for private queries|

---

## ✅ Monitoring & Logging

- ✅ CloudWatch logs per query
- ✅ Query history in Athena console
- ✅ CloudTrail logs access/metadata
- ✅ Use **Athena query results S3 bucket** for persisted result sets

---

## 📌 Exam Pointers

- “Need to run SQL on data stored in S3?” → ✅ Athena
- “Pay only per query, no infra to manage?” → ✅ Athena
- “Best performance for ad-hoc queries on raw logs?” → ✅ Use Parquet + Partitioned folders
- “Secure query access with column-level RBAC?” → ✅ Use Lake Formation with Athena
- “Need SQL access to DynamoDB without ETL?” → ✅ Athena Federated Queries
- “Need to trigger daily report query from Lambda?” → ✅ Athena + Lambda + EventBridge
- “What reduces cost in Athena?” → ✅ Columnar + compressed formats + SELECT LIMIT
