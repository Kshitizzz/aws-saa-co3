# Elasticity vs Availability vs Fault Tolerance vs Resilience vs Scalability

## Memory Hook

- "Scalability is the **potential** to grow, Elasticity is the **reflex** to grow or shrink as needed."
- "High Availability **recovers**, Fault Tolerance **doesn’t fail**, Resilience **bounces back**."
- "High Availability (HA) is achieved via redundancy across multiple AZs"
- "Elasticity = Automatic; Scalability = Possible; Resilience = Recover; Fault Tolerance = Immunity."

---

## Must-Know Core Concepts

### ✅ Scalability

- The **capacity of a system to grow** in response to increasing load.
- Can be achieved **vertically (scale up)** or **horizontally (scale out)**.
- Can be **manual or automatic**.
- **Example**: Add more EC2s to handle more traffic.

### ✅ Elasticity

- The ability to **automatically scale** up/down in response to real-time demand.
- A *subset of scalability* with automation built-in.
- Core to cloud-native design — **you don’t overpay or underperform**.
- **Example**: Auto Scaling Group adds/removes EC2s based on CPU load.

### ✅ High Availability (HA) (achieved via redundancy across multiple AZs)

- Ensures your application is **up and accessible** even when failures occur.
- Achieved via **redundancy** across **Availability Zones (AZs)**.
- **Not zero downtime**, but **minimal downtime**.
- **Example**: ALB deployed across 3 AZs reroutes traffic if one AZ fails.

### ✅ Fault Tolerance

- Ensures the system **continues operating correctly** even when components fail.
- Focuses on **zero interruption**, even during failure.
- Achieved through **redundant, isolated infrastructure**.
- **Example**: S3 stores data across 3+ AZs and continues serving requests even if one AZ goes down.

### ✅ Resilience

- The system's **ability to recover quickly** from disruptions.
- Often built through **self-healing**, monitoring, automation, and backups.
- **Downtime may occur**, but **the system restores itself** efficiently.
- **Example**: RDS failover promotes standby DB automatically when primary fails.

### ✅ Dynamic Scaling

- The act of **scaling resources automatically** in real time based on monitoring.
- Part of elasticity, but focuses on the **mechanism of scaling** — metrics, alarms, automation.
- **Example**: CloudWatch alarm triggers scale-out policy when CPU > 80%.

---

## Nuances & Edge Cases

- **Elasticity ≠ Scalability**: All elastic systems are scalable, but not all scalable systems are elastic.
- **High Availability ≠ Fault Tolerance**: HA allows *some* failure with *quick recovery*; FT means failure doesn’t interrupt at all.
- **Resilience is broader**: It includes *detection*, *response*, *recovery*, not just continuity.
- Fault-tolerant systems usually cost more — e.g., **always-on replicas**, multiple AZs.
- Elasticity can include **scale-in**, which is often missed — saves cost by reducing unused resources.

---

## Memory Hook (Repeat for Reinforcement)

- "Scalability is **how big you can get**, Elasticity is **how fast and smart you react**."
- "HA = Accessible, FT = Unbreakable, Resilience = Bounce-back."
- "Cloud-native = Elastic + Resilient by design."

---

## 🧠 Flashcards

**Q:** What’s the difference between Elasticity and Scalability?  
**A:** Scalability is the *capacity* to grow; Elasticity is *automatic* real-time scaling.

**Q:** Is Fault Tolerance the same as High Availability?  
**A:** No. HA allows for *fast recovery*; FT allows for *no disruption at all*.

**Q:** What’s a real-world example of Resilience in AWS?  
**A:** RDS Multi-AZ failover promoting standby DB during failure.

**Q:** What AWS services show Elasticity?  
**A:** Auto Scaling Groups, Lambda (serverless), DynamoDB on-demand mode.

**Q:** Can a system be Highly Available but not Fault Tolerant?  
**A:** Yes — if it fails briefly but recovers quickly, it's HA but not FT.
