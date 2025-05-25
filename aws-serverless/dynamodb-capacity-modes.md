# DynamoDB Capacity Modes – Provisioned, Auto Scaling, On-Demand

## Memory Hook  
- “Provisioned = predict and reserve”  
- “Auto Scaling = flexible reservation”  
- “On-Demand = burst anytime, pay as you go”

---

## ✅ 1. Provisioned Capacity Mode

### What It Means  
You manually define:
- **RCUs (Read Capacity Units)**  
- **WCUs (Write Capacity Units)**

This means:
- You **pay per hour** for the reserved capacity
- DynamoDB will **throttle requests** if you exceed provisioned throughput

### Use Case  
- Predictable workloads (steady read/write rates)  
- Cost-optimized when traffic is known (e.g., 100 reads/sec = 100 RCUs)

### Example  
- 1 RCU = 1 strongly consistent read/sec for item ≤ 4 KB
- 1 WCU = 1 write/sec for item ≤ 1 KB

## 2. Auto Scaling for Provisioned
### What It Does
- Dynamically adjusts RCUs and WCUs between a min–max range
- Based on utilization thresholds (default 70% utilization)

### How It Works
- Uses CloudWatch metrics + Application Auto Scaling
- Adjusts gradually (not instant)
- Takes 5–15 minutes for scale-up under load

### Use Case
- Workloads with daily/weekly patterns (e.g., lunchtime traffic spikes)

### Auto Scaling Caveats
- Doesn’t respond well to sudden burst traffic
- Scaling lag can cause throttling
- Use On-Demand or write sharding for bursty loads

## 3. On-Demand Capacity Mode
- DynamoDB automatically handles all scaling for you
- No need to specify RCUs/WCUs
- Instantly handles spiky, unpredictable workloads
- No throttling (unless you hit account-level limits)
- Billing: Pay per request:
- $X per million reads
- $Y per million writes
- More expensive than provisioned at scale
- No planning needed

### Use Case
- Startups or unknown traffic patterns
- Event-driven workloads (e.g., gaming, flash sales)

### Internal Behavior (Exam + Design Insight)
Feature	| Provisioned	| On-Demand
Scaling Delay	| Manual or slow (auto-scaling delay)	| Instantly scales
Throttling Risk	| ✅ Yes (if over limit)	| ❌ No (unless hard limits hit)
Cost predictability	| ✅ High	| ❌ Variable with spikes
Cold start latency	| ❌ No cold starts	| ❌ No cold starts
Read/Write Control	| ✅ Precise	| ❌ Abstracted away

## Exam Pointers
- “Need cost-efficient capacity for known traffic pattern?” → ✅ Provisioned + Auto Scaling
- “Need to handle sudden spikes without throttling?” → ✅ On-Demand
- “App getting throttled despite auto scaling enabled?” → ✅ Scale lag / burst mismatch
- “Which mode is easiest for new app with variable load?” → ✅ On-Demand
- “Want max control over throughput + billing?” → ✅ Provisioned mode