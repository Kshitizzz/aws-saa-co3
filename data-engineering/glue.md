- managed and serverless ETL service by AWS
- Glue Bookmarks - Prevents reprocessing of already processed data
- Glue DataBrew - Data cleaning and normalization use pre-built transformations
- Glue Studio - GUI to create and monitor Glue jobs
- Glue Streaming ETL - run real time stream processing jobs instead of batch processing, compatible with kinesis data streaming, kafka, MSK..
- Glue Catalog and Glue Datacrawler - catalog maps out your datasets in multiple sources (s3, RDS, any odbc type connector data source), datacrawler actually does this mapping by crawling through the dataset and creating metadata 
---------------------------------------------------------

# AWS Glue – Deep Dive (Data Catalog + ETL + Crawlers + Jobs)

## Memory Hook  
- “Glue = Serverless data wrangler”  
- “Catalog + Crawler + Transform + Load — all without managing servers”

---

## ✅ What Is AWS Glue?

> AWS Glue is a **serverless data integration service** used to **discover, catalog, clean, enrich, and move data** between sources.

Glue supports:
- **ETL (Extract, Transform, Load)**
- **ELT** workflows via pushdown predicates
- **Data discovery** via **Crawlers**
- **Schema registry + metadata** via the **Glue Data Catalog**
- **Job orchestration** via **Workflows and Triggers**

---

## 🔧 Core Glue Components

| Component         | Description                                                          |
|--------------------|----------------------------------------------------------------------|
| **Glue Data Catalog** | Central schema/metadata repository (can be shared with Athena, Redshift, EMR) |
| **Glue Crawlers**     | Auto-detect schema from files in S3 and populate Data Catalog     |
| **Glue Jobs**         | Code to transform/process data (PySpark, Python shell, Scala)     |
| **Glue Workflows**    | Orchestrate multi-step ETL pipelines                              |
| **Glue Triggers**     | Event or time-based job execution                                 |
| **Glue Studio**       | Visual interface for building and monitoring pipelines            |
| **Glue Tables**       | Metadata schema definitions in Data Catalog                       |

---

## ✅ Glue Job Types

| Job Type        | Description                                            |
|------------------|--------------------------------------------------------|
| **Spark ETL Job** | Distributed ETL job using Apache Spark               |
| **Python Shell Job** | Simple Python scripts (no distributed compute)   |
| **Ray Job (Preview)** | Distributed Python for ML, preprocessing         |
| **Custom Connectors** | Integrate JDBC sources, SaaS APIs, etc.         |

---

## 🔍 Glue Data Catalog

- Centralized **schema registry** for:
  - **Athena**
  - **Redshift Spectrum**
  - **EMR**
  - **Lake Formation**

🧠 It is **Hive-compatible**, but fully managed and global per region.

---

## 🤖 Glue Crawlers

> Automatically **scan data sources**, infer schema, and create/refresh Data Catalog entries

| Feature               | Details                                 |
|------------------------|------------------------------------------|
| **Supports**           | S3, JDBC, DynamoDB, MongoDB, etc.       |
| **Partitions**         | Detects and adds partitions automatically |
| **Scheduling**         | Can be run on-demand or on schedule     |

---

## ⚙️ Glue Job Execution Model

- Jobs run on **serverless Apache Spark**
- You can provide:
  - **PySpark code**
  - Visual transforms (via Glue Studio)
  - Python shell for lightweight scripts
- Optionally use **bookmarking** to avoid reprocessing same data
- Can use **pushdown predicates** to **filter at source** (JDBC)

---

## 📊 Glue + Other Services

| Service            | Integration Notes                                           |
|---------------------|-------------------------------------------------------------|
| **Athena**          | Uses Glue Catalog to query structured S3 data              |
| **Redshift Spectrum** | External tables defined in Glue                         |
| **S3**              | Default data lake landing zone                             |
| **Lake Formation**  | Uses Glue Catalog + adds RBAC for column/row-level security |
| **EventBridge**     | Use triggers to run Glue jobs on file arrival              |

---

## 💡 Real-World Use Cases

- Data lake ETL pipelines (S3 → S3 → Athena or Redshift)
- Incremental processing (with job bookmarking)
- Schema-on-read pipelines
- Preprocessing for ML
- Log aggregation + cleaning

---

## 🧠 Gotchas & Nuances

| Detail                              | Insight                                                |
|-------------------------------------|---------------------------------------------------------|
| Glue is **region-specific**         | You need to sync Data Catalogs across regions manually |
| Glue Spark jobs are **slow to start** | Startup latency ≈ 2-3 minutes                        |
| Costs scale by **DPUs used + duration** | Default: 10 DPUs                                     |
| **Python shell jobs** ≠ distributed | Use only for lightweight or boto3 tasks               |
| **Crawlers can overwrite schema**   | Use partition detection carefully                     |

---

## 📌 Exam Pointers

- “Serverless data integration and transformation?” → ✅ AWS Glue
- “Central metadata store for Athena & Redshift Spectrum?” → ✅ Glue Data Catalog
- “Want schema auto-detection from S3?” → ✅ Glue Crawler
- “Run PySpark ETL jobs without managing infra?” → ✅ Glue Job
- “Need to schedule a multi-step pipeline?” → ✅ Glue Workflow + Triggers
- “Avoid reprocessing the same files?” → ✅ Enable job bookmarking
