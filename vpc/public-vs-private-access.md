# AWS Services and Public Subnet Access

## Memory Hook

- “Some AWS services live on the internet. Some only live inside your VPC.”

---

## ✅ Public Internet–Accessible AWS Services

These services are **hosted on the public internet**:
- ✅ Amazon S3
- ✅ AWS STS (Security Token Service)
- ✅ AWS API Gateway
- ✅ DynamoDB
- ✅ Amazon SNS, SQS
- ✅ CloudFormation
- ✅ CloudWatch Logs / Metrics
- ✅ EC2 Instance Metadata (from inside EC2)
- ✅ Lambda Control Plane
- ✅ Secrets Manager, Systems Manager (control plane)

**➡️ You can access these via public subnet (or NAT from private subnet)**  
**➡️ These services do NOT live “inside” your VPC**

---

## ❌ Private-Only / VPC-Scoped Services

These services **run inside your VPC**:
- 🚫 EC2 Instances
- 🚫 RDS / Aurora
- 🚫 ElastiCache
- 🚫 Redshift (unless publicly exposed, not recommended)
- 🚫 Private ALBs, NLBs (if subnet is private)
- 🚫 ECS tasks (if in private subnet)

**➡️ These need NAT GW / EIPs to talk to internet (from private subnet)**  
**➡️ Cannot be accessed directly from public internet unless exposed via ALB/NLB**

---

## 🧠 Exam Pointers

| Question Scenario                                      | Answer                                          |
|--------------------------------------------------------|--------------------------------------------------|
| “Private EC2 can’t access S3?”                        | ❌ No NAT GW or no S3 endpoint                    |
| “Want to access S3 from private subnet with no NAT?”  | ✅ Use **Gateway VPC Endpoint for S3**           |
| “Which services require public subnet to be accessed?”| ✅ S3, STS, DynamoDB, etc.                        |
| “How does EC2 get IAM credentials?”                   | ✅ Instance metadata → calls STS (via public IP)  |

---

## 🧪 Common Misconceptions

- ❌ **S3 is NOT inside your VPC** — it’s accessed over **public internet**
- ✅ **S3 endpoint** routes S3 traffic **privately** using AWS internal network
- ❌ **Lambda itself runs outside your VPC**, unless placed in a VPC manually

---

## 🔐 Security Tip

Use **VPC Endpoints** (Gateway or Interface) to:
- Keep traffic private (no internet)
- Avoid needing NAT Gateways for services like S3, DynamoDB

