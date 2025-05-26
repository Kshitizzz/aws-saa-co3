# EC2 Auto Scaling Groups (ASG) – Deep Dive

## Memory Hook  
- “ASG = Your automatic babysitter for EC2s — scales up, scales down, heals fast”

---

## ✅ What Is an Auto Scaling Group (ASG)?

> A service that automatically manages **scaling and health** of a group of EC2 instances based on **demand or schedule**

---

## 🔧 ASG Core Components

| Component           | Description                                                                 |
|----------------------|-----------------------------------------------------------------------------|
| **Launch Template**  | ✅ Required; defines instance type, AMI, key pair, SGs, volumes             |
| **Min/Max/Desired**  | ✅ Minimum, maximum, and starting number of EC2 instances                   |
| **Scaling Policies** | Rules that trigger scale-out/in based on metrics or schedules              |
| **Health Checks**    | ✅ Built-in EC2 + optional ELB health checks                                |
| **Availability Zones** | Distributes EC2s across selected AZs for HA                             |
| **Instance Refresh** | Roll out config changes without downtime (blue/green-style updates)        |

---

## ✅ Types of Scaling

### 1. Dynamic Scaling
> Responds to **real-time metrics** from CloudWatch

| Policy Type                | Description                                             |
|----------------------------|---------------------------------------------------------|
| **Target Tracking**        | Most common – e.g., “keep CPU at 50%”                  |
| **Step Scaling**           | Scales in steps based on threshold breach              |
| **Simple Scaling**         | Legacy – one trigger per action                        |

### 2. Predictive Scaling
> Uses **ML-based forecasting** to anticipate traffic spikes

- Learns patterns (e.g., lunch traffic)
- Pre-warms EC2 instances ahead of time
- Best when combined with dynamic scaling

### 3. Scheduled Scaling
> Based on time – e.g., scale out every Monday 9 AM

---

## 💡 Instance Distribution Strategies

When using **Mixed Instance Policies**, you can:
- Use **On-Demand + Spot** in same group
- Define **percentage per type**
- Use **capacity-optimized or lowest-price** strategy

---

## 🧠 ASG + Load Balancer = Best Practice

- Attach **ALB or NLB** to your ASG
- ASG registers/deregisters EC2s automatically
- ✅ Enables **zero-downtime rolling updates**

---

## 💣 ASG Lifecycle Hooks

> Allow you to run code **before instance fully joins or leaves** the group

| Hook               | Use Case Example                             |
|--------------------|-----------------------------------------------|
| `autoscaling:EC2_INSTANCE_LAUNCHING` | Run bootstrapping scripts before LB registration |
| `autoscaling:EC2_INSTANCE_TERMINATING` | Back up logs, drain connections               |

🧠 Hooks integrate with:
- SQS
- SNS
- Lambda

---

## 🛡️ ASG Health Checks

| Type         | Behavior                                             |
|--------------|------------------------------------------------------|
| **EC2**      | Checks instance status (default)                     |
| **ELB**      | Checks via target group/ALB health                   |
| ❌ unhealthy instance → auto replaced                                |

---

## 📦 EC2 Instance Refresh

> Blue/green–style rolling update built into ASG

- Update **AMI**, **launch template**, **instance type**
- ASG replaces instances **gradually**
- Ensures **no downtime** and controlled rollout

---

## 🔁 Warm Pools

> Pre-initialized EC2s ready to go → **faster scale-out**

- Useful when boot time is long (e.g., large AMIs, heavy startup logic)
- Stored in a “suspended but prepped” state

---

## 🧩 Integration with Other AWS Services

| Service         | Integration Use Case                              |
|------------------|---------------------------------------------------|
| **CloudWatch**   | Metric source for scaling                         |
| **ALB/NLB**      | Load distribution + health checks                 |
| **Launch Templates** | EC2 config baseline                           |
| **EventBridge**  | Scale actions, lifecycle event logging            |
| **Lambda/SNS**   | Lifecycle hook responders                         |
| **Spot Instances** | Cheap overflow compute                         |
| **CloudFormation** | Infrastructure as code for ASGs                |

---

## 📌 Exam Pointers

- “Auto-replace unhealthy EC2?” → ✅ ASG with health checks
- “Scale based on traffic patterns?” → ✅ Predictive scaling
- “Need to scale web tier + balance traffic?” → ✅ ASG + ALB
- “Update EC2 AMI with no downtime?” → ✅ Instance Refresh
- “Want to use Spot with fallback to On-Demand?” → ✅ Mixed Instance ASG
- “Want faster scale-up despite long startup time?” → ✅ Warm Pools
