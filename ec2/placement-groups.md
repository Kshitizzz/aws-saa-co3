# EC2 Placement Groups – Deep Dive

## Memory Hook  
- “Placement Groups = how tightly or loosely you want your instances physically placed in the data center.”

---

## ✅ What Is a Placement Group?

> A **logical grouping of EC2 instances** that influences their **physical placement** within an AWS Availability Zone for performance or fault tolerance.

---

## 🔁 Types of Placement Groups

### 1. **Cluster Placement Group**
- Instances are placed in **the same rack or close-by racks** (low latency + high throughput).

| Feature            | Details                                  |
|---------------------|------------------------------------------|
| **Latency**         | ✅ Ultra low                             |
| **Bandwidth**       | ✅ High-speed networking (10–100 Gbps)   |
| **Use Case**        | HPC, ML training, tightly coupled apps  |
| **Risk**            | ❌ Single point of failure               |
| **AZ Scope**        | ❌ Single AZ only                        |

🧠 Works best when:
- Using same instance type
- Launched together (avoid launch failure)

---

### 2. **Spread Placement Group**
- Instances are placed **on distinct hardware**, **rack-level isolation** guaranteed.

| Feature             | Details                                |
|----------------------|----------------------------------------|
| **Fault tolerance**  | ✅ Very high                           |
| **Max per AZ**       | ✅ Up to 7 instances per AZ            |
| **Use Case**         | Critical EC2s (DB, master nodes)       |
| **AZ Scope**         | ✅ Multi-AZ supported                  |
| **Launch flexibility**| ✅ Add instances any time             |

🧠 Best for:
- High availability
- Low EC2 count but critical roles (HA master nodes, Zookeeper)

---

### 3. **Partition Placement Group**
- Instances divided into **logical partitions** → each partition on **separate racks, power, networking**.

| Feature             | Details                                  |
|----------------------|------------------------------------------|
| **Fault isolation**  | ✅ Between partitions                   |
| **Use Case**         | Big data (HDFS, Kafka, Cassandra)       |
| **# of partitions**  | Up to 7 per AZ                          |
| **AZ Scope**         | ✅ Multi-AZ supported                   |
| **Access to metadata** | ✅ You can get which partition an instance is in |

🧠 Enables:
- Rack-aware data replication
- Better failure domain awareness

---

## ⚠️ Launch Behavior & Limitations

| Scenario                     | Behavior                                           |
|------------------------------|----------------------------------------------------|
| Launching too many EC2s      | ❌ Cluster PG may fail if capacity isn’t available |
| Spread PG                    | ✅ Always launches if within instance limit         |
| Partition PG                 | ✅ Works for large, fault-tolerant distributed apps |

---

## 💣 Gotchas

- Cluster PG = lowest latency but highest risk
- Spread PG = safest, but strict limit (7/region/AZ)
- Partition PG = best for scalable distributed data layers

---

## 🧠 When to Use What?

| Use Case                                  | Placement Group Type     |
|-------------------------------------------|---------------------------|
| Real-time analytics, MPI, ML training     | ✅ Cluster                |
| Cassandra, Kafka, ElasticSearch, HDFS     | ✅ Partition              |
| HA for app servers, Zookeeper, control plane | ✅ Spread               |
| General web app or API servers            | ❌ Doesn’t need PG        |

---

## 🧩 Additional Details

- You can’t **change the type** of a placement group — recreate instead
- Launch templates can specify placement groups
- Placement groups don’t affect pricing
- Placement groups don’t guarantee instance affinity across reboots

---

## 📌 Exam Pointers

- “Tightly-coupled, high-throughput app?” → ✅ Cluster PG
- “Critical instances must avoid single point of failure?” → ✅ Spread PG
- “Need fault-isolated partitions for a distributed system?” → ✅ Partition PG
- “Launching fails in cluster PG?” → ✅ Not enough capacity in single rack — try spreading or relaunching
- “How many instances allowed in a spread PG per AZ?” → ✅ 7
