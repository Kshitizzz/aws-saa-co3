# Amazon DynamoDB – One-Shot, No-BS Study Guide

## Memory Hook

- “Fully managed NoSQL with predictable latency, because it's **designed to be boringly consistent at scale**.”

---

## ✅ What DynamoDB Actually Is

- **NoSQL key-value and document database** (NOT a graph DB, not relational)
- Fully **serverless** — no servers, OS, maintenance, or patching
- Serverless meaning you dont need to manage the server, OS, maintenance, patching
- You just manage your own data that you store
- Built on **distributed hash table principles (like Amazon's internal Dynamo paper)**

---

## 🧱 Under-the-Hood Architecture

| Property                    | What Powers It                                               |
|-----------------------------|---------------------------------------------------------------|
| **Massive scale**           | Data sharded by **partition key** across **multiple partitions** |
| **High availability**       | Data automatically replicated across **3 AZs** per region      |
| **Low latency**             | All operations served via **in-memory indexes**, local replicas, optimized B-tree variants
| **NoSQL**                   | No joins, no foreign keys, schema-less attributes             |
| **Consistent performance**  | Provisioned or auto scaling read/write throughput             |

---

## 🧠 Core Data Model

- **Table** = like a collection
- **Item** = like a row (but schema-less)
- **Attribute** = like a column

### Key Schema
- **Partition key (PK)** → Mandatory
- **Sort key (SK)** → Optional

🧠 PK determines **which partition** the item is stored in  
🧠 SK enables **range-based queries**

---

## 🔑 Read/Write Patterns

| Operation            | Notes                                       |
|----------------------|---------------------------------------------|
| `GetItem`            | Fast lookup by PK (+ optional SK)           |
| `PutItem` / `UpdateItem` | Overwrites item by PK                    |
| `Query`              | Returns multiple items **with same PK**, ordered by SK  
| `Scan`               | Returns entire table (expensive!)           |
| `BatchGet/Write`     | Parallel batched access (with limits)       |

✅ Use `Query` whenever possible — avoid `Scan` in prod

---

## ⚙️ Performance Configuration

| Mode                     | Description                                           |
|--------------------------|-------------------------------------------------------|
| **Provisioned**          | Fixed RCU/WCU (Read/Write Capacity Units)             |
| **On-Demand**            | Pay-per-request (burst-friendly, expensive at scale)  |
| **Auto Scaling**         | Adjusts RCU/WCU within bounds                         |
| **DAX** (Accelerator)    | In-memory caching layer for DynamoDB (millisecond to microsecond read speeds)

---

## 🔐 Durability & Availability

- **3-way replicated within an AWS region**
- Strong consistency is optional (eventual by default)
- Global tables replicate data **across regions**

✅ No need to worry about disk corruption, replication lags, or failover yourself

---

## 🧠 Indexing

### ✅ Local Secondary Index (LSI)
- Same Partition Key, different Sort Key
- Max 5 per table
- Created at table creation time only

### ✅ Global Secondary Index (GSI)
- Different Partition + Sort Key
- Max 20 per table
- Can be added/removed at any time

🧠 GSI consumes its **own RCU/WCU or billing**  
🧠 GSI is **eventually consistent by default**

---

## 🧬 Consistency Models

| Mode                   | Description                            |
|------------------------|----------------------------------------|
| **Eventually Consistent** | Default; faster, cheaper               |
| **Strongly Consistent**   | Slower, reads latest write            |
| **Transactional**         | ACID ops via `TransactWrite` / `TransactGet` (limit: 25 items)

---

## 💣 Limitations (a.k.a. real-world traps)

| Limit                         | Value                      |
|-------------------------------|-----------------------------|
| Item size                     | Max 400 KB                 |
| Table size                    | Unlimited (auto scaling)   |
| Partition throughput (per key)| ~1,000 WCU or 3,000 RCU/sec |
| LSI count                     | Max 5 per table            |
| GSI count                     | Max 20 per table           |

🧠 **Hot partition problem** occurs when too many requests hit the same partition key  
🧠 Spread write load by using **high-cardinality partition keys**

---

## 🧠 Patterns & Anti-Patterns

| Pattern                       | Do it?   | Notes                                            |
|-------------------------------|----------|--------------------------------------------------|
| **1:1 relationships**         | ✅ Yes   | Store all attributes in one item                 |
| **1:N relationships**         | ✅ Yes   | Use composite SK (`post#1`, `post#2`, etc.)      |
| **Joins / multi-table joins** | ❌ No    | Denormalize; fetch separately                    |
| **Ad-hoc analytics**          | ❌ No    | Use Athena, Redshift, or DDB Streams + ETL       |
| **Range queries**             | ✅ Yes   | Use Sort Key with `begins_with`, `between`, etc. |

---

## 📡 Serverless Integrations

- ✅ Triggers via **DynamoDB Streams** → Lambda
- ✅ Real-time pipelines using **Kinesis + DynamoDB**
- ✅ Async writes via **Step Functions**
- ✅ Use with **AppSync** (GraphQL + DynamoDB)

---

## 📌 Exam Pointers

- “Need single-digit latency for unpredictable workloads?” → ✅ Use DynamoDB On-Demand
- “Cross-region, multi-master data store?” → ✅ DynamoDB Global Tables
- “Data lake access with flexible schema?” → ❌ Use S3 + Athena
- “Trigger function on every new item?” → ✅ Enable DynamoDB Streams + Lambda
- “Need ACID transactions?” → ✅ Use `TransactWriteItems` API

---

Let me know if you want to drill into:
- **Data modeling principles (1:N, composite key design)**  
- **DynamoDB Streams + Lambda pipelines**  
- **Global Tables + Multi-Region KMS integration**

Or I can quiz you now on the full DynamoDB one-shot.
