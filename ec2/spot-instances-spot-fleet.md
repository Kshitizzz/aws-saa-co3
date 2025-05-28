# Spot Instances & Spot Fleet – Deep Dive

## Memory Hook  
- “Spot = spare EC2 capacity at 90% discount — but eviction can come anytime”  
- “Spot Fleet = orchestrated bidding strategy across multiple types and AZs”

---

## ✅ What Are Spot Instances?

> EC2 capacity that’s unused by AWS, offered at a massive discount — but **can be interrupted with 2-minute notice**

---

### 🔍 Key Spot Properties

| Feature                       | Detail                                                                 |
|-------------------------------|------------------------------------------------------------------------|
| **Pricing**                   | Dynamic, market-driven (but often stable in practice)                  |
| **Discount**                  | Up to **90% cheaper** than On-Demand                                   |
| **Interruption**              | AWS can reclaim capacity with **2-minute warning**                     |
| **Max lifetime**              | Unlimited (except for hibernation: 6-hour max)                         |
| **Instance types supported**  | ✅ Most EC2 families, including GPU/Graviton                            |
| **Interruption behavior**     | Configurable: **terminate**, **stop**, or **hibernate**                |
| **Billing granularity**       | Per second, like On-Demand                                             |
| **Data persistence**          | EBS volumes persist (unless explicitly deleted on termination)         |

---

### ✅ Common Use Cases

| Use Case                    | Why It Works                                      |
|-----------------------------|--------------------------------------------------|
| Big data (Hadoop/Spark)     | ✅ Parallelizable, retry-friendly workloads       |
| Machine learning training   | ✅ Long-running, checkpointable                   |
| CI/CD Pipelines             | ✅ Can rerun failed tests                         |
| Batch video/image processing| ✅ Fault-tolerant, queue-based                    |
| Container workloads         | ✅ ASG + ECS or EKS handles replacement           |

---

## ⚠️ When NOT to Use Spot

- Web frontends with session state
- Long-running single-node stateful apps
- Compliance-heavy environments (no capacity guarantees)
- Uptime-critical apps without retries or fallback

---

## ✅ How AWS Interrupts Spot Instances

- If AWS needs capacity, your instance may be:
  - Terminated
  - Stopped (can be resumed later)
  - Hibernate (saves memory + CPU state for restart)
- You get **2-minute warning** via:
  - **EC2 metadata endpoint**
  - **CloudWatch Events (EventBridge)**

---

## ✅ Spot Best Practices

| Strategy                     | Benefit                                               |
|------------------------------|--------------------------------------------------------|
| Use ASG Mixed Instance Policy| ✅ Automatically replaces interrupted instances        |
| Use `capacity-optimized`     | ✅ Chooses most available capacity pools               |
| Diversify AZs & types        | ✅ Reduces blast radius of interruption                |
| Use Spot + On-Demand base    | ✅ Guarantees minimum availability, cheap scale out    |
| Monitor with EventBridge     | ✅ Triggers clean-up or fallback logic                 |

---

## 🔁 Spot Allocation Strategies

| Strategy             | Description                                      |
|----------------------|--------------------------------------------------|
| **lowest-price**     | Choose the cheapest pool (can be volatile)       |
| **capacity-optimized** | Choose the most available (less likely to interrupt) |

---

## 🧠 Spot Integration with Auto Scaling

> Best practice: use **Auto Scaling Group with mixed instance policy**

- Define **base capacity** (On-Demand)
- Define **overflow** (Spot)
- Target multiple **instance types + AZs**
- Works well with **Launch Templates**

---

## ✅ What Is Spot Fleet?

> A Spot Fleet is an EC2 service that launches and manages a **group of Spot Instances** (and optionally On-Demand) to meet a **target capacity** based on your strategy.

---

### How It Works

1. You define:
   - `TargetCapacity` (e.g., 100 vCPUs)
   - List of instance types + subnets
   - Allocation strategy (`lowestPrice`, `capacityOptimized`)
   - Max price (optional)
   - IAM role for instance launch

2. AWS:
   - Tries to launch mix of instances to satisfy capacity
   - Replaces terminated Spot instances

---

### Spot Fleet vs Auto Scaling Group
- remember that you set a `target capacity`  and then AWS tries to match it using a mix of spot instances
- it replaces terninated instances with new ones to meet Target capacity but it does not scales based on workload
- it just kinda self heals to meet target capacity range

| Feature                     | Spot Fleet                            | ASG with Spot                      |
|-----------------------------|----------------------------------------|------------------------------------|
| **Flexibility**             | ✅ Many types, AZs                     | ✅ Many types, AZs                  |
| **Managed scaling**         | ❌ Not automatic scaling               | ✅ Built-in scaling policies        |
| **Launch Templates**        | ✅ Required                            | ✅ Recommended                      |
| **Use case**                | Big batch workloads, capacity targets | Auto-scaling services, containers  |
| **Preferred for**           | Fixed target capacity                  | Elastic, demand-based workloads    |

---

## 📌 Exam Pointers

- “Best compute savings with fault tolerance?” → ✅ Spot
- “Need to dynamically replace instances without losing capacity?” → ✅ ASG with Spot + On-Demand
- “Want to run ML workload across AZs at minimal cost?” → ✅ Spot Fleet or Mixed ASG
- “How does AWS notify you of interruption?” → ✅ EC2 Metadata + EventBridge (2-min warning)
- “Want to reduce interruption rate?” → ✅ Use `capacity-optimized` strategy

---

## 🔧 AWS Services That Support Spot

- EC2 Auto Scaling Groups
- ECS / EKS
- EMR (Spark/Hadoop)
- SageMaker
- Batch
- Spot Fleet
- Lambda (via container orchestration via Batch or ECS)

