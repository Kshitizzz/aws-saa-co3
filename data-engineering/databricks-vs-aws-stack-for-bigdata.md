# Databricks on AWS vs Native AWS Data Lake Stack (Lake Formation, Glue, EMR)

## Memory Hook  
- “Databricks = Unified platform on Spark”  
- “AWS Native = Modular building blocks for data lakes”

---

## ✅ Overall Philosophy

| Aspect               | **Databricks on AWS**                                  | **Lake Formation + Glue + EMR Stack**                          |
|----------------------|--------------------------------------------------------|----------------------------------------------------------------|
| **Vision**           | End-to-end data + AI platform                          | Assemble-your-own modular data lake                           |
| **Core Engine**      | Apache Spark + Delta Lake                              | Glue (PySpark), EMR (Hadoop/Spark), Athena (Presto)           |
| **Target Users**     | Data scientists, ML engineers, analytics teams         | Data engineers, BI teams, ops-heavy teams                     |
| **Setup**            | Fully managed SaaS-like experience                     | AWS-native services; you provision/manage separately          |
| **Pricing Model**    | Databricks Units (DBU)                                 | Pay-as-you-go by DPU/hour, EMR/hour, S3/GB, etc.              |

---

## ✅ Data Management & Governance

| Feature                     | **Databricks**                                 | **Lake Formation + Glue Catalog**                             |
|-----------------------------|------------------------------------------------|----------------------------------------------------------------|
| **Catalog**                 | Unity Catalog (multi-layer governance)         | Glue Data Catalog (Hive-compatible, region-specific)          |
| **Access Control**          | Table/column-level via Unity & Delta sharing   | ✅ Fine-grained control via LF permissions + tags             |
| **Multi-tenancy**           | Built-in Delta Sharing, workspace isolation    | Manual via resource links, IAM roles                          |

---

## ✅ Storage & Format Support

| Feature                     | **Databricks**                                | **AWS Native**                                                |
|-----------------------------|-----------------------------------------------|----------------------------------------------------------------|
| **Storage Layer**           | S3 (external table storage)                  | S3 (Lake Formation registry)                                  |
| **File Format**             | Delta Lake (default) + Parquet, ORC, JSON    | Parquet, ORC, JSON, CSV, Avro (no Delta by default)           |
| **ACID Transactions**       | ✅ Delta Lake (strong ACID, versioning)       | ❌ Not native; use Iceberg or manually with EMR/Glue          |
| **Schema Evolution**        | ✅ Seamless with Delta                        | ❌ Glue crawler schema overwrite can cause issues             |

---

## ✅ Compute & Processing

| Feature                     | **Databricks Runtime**                         | **AWS Compute Options**                                       |
|-----------------------------|------------------------------------------------|----------------------------------------------------------------|
| **Processing Engine**       | Apache Spark, Photon (optimized Spark)         | Glue (PySpark), EMR (Spark, Hive, Flink), Athena (Presto)     |
| **Cluster Management**      | Serverless or auto-managed clusters            | EMR (customizable), Glue (serverless DPUs), manual control    |
| **Notebook Support**        | ✅ First-class notebooks, MLflow, visualizations | SageMaker, JupyterHub on EMR, Zeppelin on EMR                |

---

## ✅ Data Engineering + ML Workflow Integration

| Feature                     | **Databricks**                                 | **AWS Native Stack**                                          |
|-----------------------------|------------------------------------------------|----------------------------------------------------------------|
| **ML Pipelines**            | Integrated MLflow tracking + model registry    | SageMaker, Step Functions, custom-built orchestration         |
| **Job Scheduling**          | Built-in scheduler + workflows                 | Glue Workflows, EventBridge, Step Functions                   |
| **Versioning**              | ✅ Delta Lake + Git-backed notebooks           | Manual versioning (S3 versioning, Git CI/CD pipelines)        |

---

## ✅ Real-World Decision Factors

| Decision Factor                | Choose **Databricks**                    | Choose **AWS Native Stack**                             |
|-------------------------------|------------------------------------------|----------------------------------------------------------|
| Unified data + ML team usage  | ✅ Databricks                            | ❌ Fragmented toolchain in AWS                           |
| Deep Spark/Delta support      | ✅ Databricks                            | ❌ No Delta support unless EMR + custom setup            |
| Fine-grained data governance  | ✅ Unity Catalog (advanced)              | ✅ Lake Formation + Tags                                 |
| Infra and ops control         | ❌ Limited                                | ✅ Total control with EMR, IAM, policies                 |
| Lowest cost (modular control) | ❌ DBU-based billing                      | ✅ Serverless Glue + Athena + S3 = pay-per-use           |
| Open-source parity            | ✅ OSS-like runtime + Photon              | ❌ Fragmented Spark/Hadoop support across services        |

---

## 📌 Exam Pointers

- “Need serverless data catalog + secure sharing across accounts?” → ✅ Lake Formation + Glue Catalog
- “Need to process S3-based data using PySpark without managing infra?” → ✅ AWS Glue
- “Need full data + ML platform with Delta Lake support?” → ✅ Databricks
- “Need Hive-compatible metastore across Athena and EMR?” → ✅ Glue Data Catalog
- “Need ACID transactions + time travel on S3 data?” → ✅ Databricks with Delta Lake
- “Need to register and enforce column-level policies across teams?” → ✅ Lake Formation with tags

