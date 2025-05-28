# AWS EMR – Node Types, Pricing Models & Comparison with AWS Glue

## Memory Hook  
- “EMR = Customizable big data factory on EC2”  
- “EMR nodes = brain, arms, and legs of your cluster”  
- “Glue = serverless, EMR = customizable cluster beast”

---

## ✅ What Is AWS EMR?

> A **managed big data cluster service** that runs open-source frameworks like:
- Apache Spark
- Hadoop (MapReduce, HDFS)
- Hive, Presto, Flink, Hudi, Iceberg, Trino
- Jupyter, Zeppelin, Airflow (with EMR Notebooks)

🧠 You get full control over:
- Compute/storage
- Network config
- Installed frameworks
- Auto-scaling, security, logging, etc.

---

## 🧩 EMR Node Types (Cluster Roles)

| Node Type       | Purpose                                           |
|------------------|--------------------------------------------------|
| **Master Node**  | Coordinates cluster (YARN, HDFS NameNode, etc.) |
| **Core Node**    | Stores data + runs compute tasks                |
| **Task Node**    | Runs compute only (no HDFS, no persistent data) |

🧠 Master: Brain  
🧠 Core: CPU + Disk  
🧠 Task: Extra CPU when needed

---

## ✅ Purchasing Options (EC2-backed)

| Option                 | Description                                          |
|-------------------------|------------------------------------------------------|
| **On-Demand**           | No commitments, flexible, costlier                  |
| **Spot Instances**      | Save up to 90%, risk of interruption                |
| **Reserved Instances**  | Save 30-70%, commit for 1 or 3 years                |
| **Savings Plans**       | Commit to spend, apply across EC2 and EMR           |
| **EMR on EKS**          | Run Spark jobs on shared EKS cluster                |

### ⚙️ Typical Strategy
- Master = On-Demand (stability)
- Core = On-Demand + Reserved (if persistent storage needed)
- Task = Spot (cheap compute bursts)

---

## 🔥 EMR Pricing Tips

- You pay for:
  - EC2 instance time
  - EMR surcharge (~$0.015 per hour per instance)
- Can use:
  - HDFS, S3, or both as storage layers
- Use Auto Scaling + Spot for savings

---

## ✅ EMR vs Glue – When to Use What

| Feature                        | **EMR**                                     | **Glue**                                  |
|--------------------------------|----------------------------------------------|--------------------------------------------|
| **Compute Control**            | Full EC2 control, cluster tuning             | ✅ Serverless, auto-managed                |
| **Framework Support**          | ✅ Spark, Hadoop, Flink, Hive, Trino         | PySpark, Python shell (Glue 3.0+)          |
| **Runtime Environment**        | Customizable (JARs, AMIs, bootstrap scripts) | ❌ Limited customization                   |
| **Cluster Size**               | Big, multi-node jobs, long-running pipelines | Small/medium ETL, on-demand jobs           |
| **Job Execution Time**         | Minutes to hours (boot + process)            | Slower start (~1–3 min cold start)         |
| **Notebook Integration**       | Jupyter, Zeppelin, EMR Studio                | Glue Studio (visual + code)                |
| **Orchestration**              | Manual or via Step Functions                 | Glue Workflows or EventBridge              |
| **Data Format Flexibility**    | ✅ Full (Parquet, ORC, Iceberg, Delta, Hudi) | ✅ Limited but supports most common formats|
| **Cost Model**                 | EC2-based (RI, Spot, On-Demand)              | Per-DPU second                             |
| **Use Case Fit**               | Data lakes, large ETL, machine learning      | Lightweight ETL, schema conversion         |

---

## ✅ When to Use EMR vs Glue (Exam Pointers)

- “Need to run Hadoop, Hive, or Presto?” → ✅ EMR
- “Spark job must access private subnet with custom AMI?” → ✅ EMR
- “Need serverless ETL with schema discovery?” → ✅ Glue
- “Processing large amounts of raw S3 data in parallel with Spark?” → ✅ EMR
- “Need native job bookmarking & catalog integration?” → ✅ Glue
- “Want to run distributed ML with Spark MLlib or TensorFlow?” → ✅ EMR
