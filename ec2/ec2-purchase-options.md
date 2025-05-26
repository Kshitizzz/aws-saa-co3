# EC2 Purchasing Options + Spot Instances & Spot Fleet – Deep Dive

## Memory Hook  
- “Choose your pricing like you choose your seats — reserved, flexible, or auction”

---

## ✅ EC2 Purchasing Options – Overview

| Option                | When to Use                          | Key Trait                          |
|------------------------|--------------------------------------|-------------------------------------|
| **On-Demand**          | Unpredictable, burst workloads       | Pay-per-second, no commitment       |
| **Reserved Instances** | Predictable, steady workloads        | 1 or 3 year commitment, big savings |
| **Savings Plans**      | Commit to a flexible usage plan      | Applies to EC2, Fargate, Lambda     |
| **Spot Instances**     | Flexible, fault-tolerant workloads   | Up to 90% cheaper, can be interrupted |
| **Dedicated Hosts**    | Licensing or compliance needs        | Physical server allocation          |
| **Dedicated Instances**| Isolation at hypervisor level        | Still shares hardware               |
| **Capacity Reservations** | Guaranteed AZ capacity          | Used for scheduling-sensitive apps  |

- ```fault tolerant``` as in a system that can work fine even after a fault occured (like batch pipelines)
- pipeline failed -> no worries, run again

---

## ✅ 1. On-Demand Instances

- ✅ Billed per second (after 60 sec min)
- ✅ No long-term commitment
- ❌ Most expensive over time

**Use Cases**:
- Dev/test environments
- Short-term unpredictable workloads
- Burst scaling with auto-scaling groups

---

## ✅ 2. Reserved Instances (Standard vs Convertible)

| Type           | Description                                     |
|----------------|--------------------------------------------------|
| **Standard RI** | Locked to instance type + AZ; up to 72% cheaper |
| **Convertible RI** | Switch types (e.g., t3 → m5) mid-term; less discount |

**Term Options**:
- 1 or 3 years
- No upfront / Partial / All upfront

**Use Cases**:
- Databases
- Backend services
- Consistently running workloads

---

## ✅ 3. Savings Plans

> Commit to $/hr spend, not instance type

| Plan Type          | Flexibility               | Applies To            |
|---------------------|---------------------------|------------------------|
| **Compute SP**       | ✅ Any compute in any region | EC2, Fargate, Lambda   |
| **EC2 Instance SP**  | Locked to family + region   | Only EC2               |

✅ Ideal for:
- Multi-service environments
- Flexible EC2 workloads with varied instance types

---

## ✅ 4. Spot Instances – Deep Dive

> Bid for unused EC2 capacity — **up to 90% cheaper**, but can be **interrupted** with 2-minute warning

### Key Properties

| Property                     | Value                          |
|------------------------------|---------------------------------|
| **Pricing model**            | Market-based, fluctuates        |
| **Interruption behavior**    | ✅ Can stop/terminate/hibernate |
| **Interruption notice**      | 2-minute warning via metadata   |
| **Max lifetime**             | 6 hours for hibernate, no max otherwise (unless enforced) |

### ✅ Use Cases
- Batch jobs
- Big data processing (Spark, Hadoop)
- CI/CD pipelines
- Containers (Fargate or ECS) 
- Fault-tolerant backend workers (fault tolerant as in worker failed but will run file if its retried)

### ❌ Avoid Spot For:
- Stateful apps without retry (like Chat Apps - can't host a session based auth server)
- Real-time web frontends
- Persistent sessions (without failover)

---

## 🔥 Spot Tips

- Always run Spot **with Auto Scaling Groups (ASG)** to automatically replace if interrupted
- Combine Spot with **On-Demand in ASG mixed instance policies**
- Use **price-capacity-optimized allocation strategy** to reduce interruption risk with optimized price

---

## ✅ 5. Spot Fleet – Advanced Spot Management

> A collection of Spot (and optionally On-Demand) requests across multiple instance types and AZs

### Why Use Spot Fleet?

- ✅ Flexibility: define target capacity, let AWS optimize pricing/capacity
- ✅ Multi-instance type diversification
- ✅ Fallback to On-Demand when Spot unavailable

### Parameters You Define:

| Parameter             | Purpose                                         |
|------------------------|-------------------------------------------------|
| `TargetCapacity`       | Total vCPUs or units needed                    |
| `SpotPrice` (optional) | Max price willing to pay per instance type     |
| `LaunchSpecification`  | Instance types, AMIs, subnets, etc.            |
| `AllocationStrategy`   | `lowestPrice` or `capacityOptimized`     or `priceCapacityOptimized`  |

---

## 🧠 EC2 Auto Scaling + Spot = Best Practice

- Use **ASG Mixed Instances** with:
  - ✅ Base capacity (On-Demand)
  - ✅ Additional capacity (Spot)
  - ✅ Diversification across AZs/types

---

## 📌 Exam Pointers

- “Predictable EC2 workload, wants to save money?” → ✅ Reserved Instance
- “Needs flexibility across services, but predictable spend?” → ✅ Compute Savings Plan
- “Run Hadoop/Spark job on cheap compute?” → ✅ Spot Instance
- “Wants high availability and Spot cost savings?” → ✅ ASG with Spot + On-Demand
- “Needs physical isolation for compliance?” → ✅ Dedicated Host
