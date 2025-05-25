# DynamoDB Throttling Mechanics & Multi-Region Global Tables Behavior

## Memory Hook  
- "Throttle = exceed speed limit"  
- "Global tables = region replicas with local writes, global sync pain"

---

## 🚦 What Is Throttling in DynamoDB?

> Throttling happens when a request exceeds the available **Read or Write Capacity Units (RCUs/WCUs)**

### 🔥 When Does It Happen?

| Condition                                 | Result                     |
|-------------------------------------------|----------------------------|
| Provisioned mode – RCUs/WCUs exceeded     | ❌ Request gets throttled  |
| Auto scaling is **too slow** to catch spike | ❌ Short-term throttle     |
| On-Demand – **account/service limits** hit| ❌ Still throttled         |
| GSI capacity is exceeded                  | ❌ Index writes are throttled independently

---

## 🧠 How Do Throttled Requests Behave?

| Request Type     | Retry Behavior                                     |
|------------------|----------------------------------------------------|
| SDK clients      | Exponential backoff with jitter (built-in)         |
| Batch operations | Only failed items need to be retried (`UnprocessedKeys`) |
| Stream processors| Processing stops if writes to downstream are throttled |

🧠 Writes to a throttled table **do not fail silently** — you get `ProvisionedThroughputExceededException`

---

## 📊 Tools to Detect & Debug Throttling

- **CloudWatch Metrics**:
  - `ThrottledRequests`
  - `ConsumedReadCapacityUnits` vs `ProvisionedReadCapacityUnits`
- **DynamoDB Console**:
  - Throughput graphs
- **X-Ray + SDK logs**:
  - Trace hot partitions
- **DynamoDB Table Dashboard**:
  - View GSI usage, top keys

---

## 🧱 Common Throttling Causes

- **Hot partition**: Too many writes to a single PK → overloaded partition
- **Bursty traffic**: Exceeds auto scaling or on-demand burst rate
- **Poor key design**: Low cardinality PKs → uneven partitioning
- **GSI bottlenecks**: GSI capacity is separate from base table!

---

## ✅ Mitigation Techniques

- Use **On-Demand** mode for unpredictable loads
- Enable **Auto Scaling** and configure higher min/max
- **Write sharding**: Append random suffixes to PK to spread load
- Use **DAX** or caching to reduce read pressure
- Increase **RCUs/WCUs** or GSI capacity
- **Decouple writes** via SQS or Kinesis

---

# 🌍 Global Tables & Capacity Modes

## ✅ What Are Global Tables?

- **Multi-region DynamoDB replication**
- Supports **active-active writes** in all participating regions
- Each region has a **replica table**
- Behind the scenes: **streams + replication layer**

---

## 🧠 Capacity Mode + Global Tables

| Capacity Mode    | Behavior with Global Tables                     |
|------------------|--------------------------------------------------|
| **Provisioned**  | You must set capacity **per region** manually   |
| **Auto Scaling** | Scales each region’s replica **independently**  |
| **On-Demand**    | Each region **auto-scales separately**          |

🧠 You pay for read/write capacity in **every region**

---

## 🧠 Global Write Path and Throttling

### Write flow:
1. Client writes to Region A
2. Region A writes to local table (consumes WCU or on-demand units)
3. Streams replicate to Region B
4. Region B writes to replica table (consumes capacity there)

### Throttling impact:
- If Region B is underprovisioned → replication is throttled
- This can cause **replication lag**
- Each region must have enough **write capacity for incoming replication writes**

---

## 🧠 Conflict Resolution

- DynamoDB uses **last-writer-wins**, based on a **timestamp field** (`versionNumber` or `updatedAt`)
- No native CRDTs or merge logic — you must **design for conflict tolerance**

---

## 📌 Exam & Design Pointers

- “Table is throttling despite auto scaling enabled?” → ✅ Scaling delay or hot partition
- “Want zero-throttle behavior on unpredictable workloads?” → ✅ On-Demand mode
- “Global Table in us-east-1 and eu-west-1, writes are failing in EU?” → ✅ Check WCU in eu-west-1
- “Replication lag growing across global table?” → ✅ Underprovisioned replica region
- “How to avoid overloading single partition key?” → ✅ Write sharding

---

## 🔧 Advanced Patterns

- Use **EventBridge or SQS** to decouple writes and smooth burst load
- Store **immutable events in DynamoDB**, use streams to forward to analytics
- Build **conflict-aware writes** with `conditionExpression` and `updatedAt` fields

