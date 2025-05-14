# VPC Endpoints & AWS PrivateLink

## Memory Hook
- “Endpoint = Private AWS highway”
- “PrivateLink = Offer services like an AWS-native API”

---

## ✅ Types of VPC Endpoints

| Type               | Used For                                 | Example Services                     |
|--------------------|-------------------------------------------|--------------------------------------|
| **Gateway Endpoint**  | Public AWS services over private route     | ✅ S3, ✅ DynamoDB (only these two)    |
| **Interface Endpoint**| Private elastic network interface (ENI)   | ✅ STS, EC2 API, SNS, SQS, SecretsMgr |
| **PrivateLink**       | Cross-VPC service exposure (via ENI)     | ✅ Expose/consume internal services   |

---

## 📦 Gateway Endpoint (S3 / DynamoDB)

- Adds a **route to route table**
- Traffic stays **within AWS network**
- No NAT or IGW needed
- **Free of cost** (except standard S3/DynamoDB request charges)

---

## 📡 Interface Endpoint (powered by PrivateLink)

- Creates an **ENI in your subnet** with private IP
- AWS service endpoint resolves to that ENI
- You access the service **as if it were inside your VPC**
- ✅ Works with many services:
  - STS, SSM, Secrets Manager, ECR, CloudWatch Logs, etc.
- **Paid**: hourly charge + per GB processed

---

## 🔄 AWS PrivateLink (Custom Cross-VPC Service Exposure)

| Role            | What It Does                                   |
|------------------|-------------------------------------------------|
| **Service Provider** | Offers internal app as PrivateLink service     |
| **Service Consumer** | Uses an **Interface Endpoint** to connect to it |

- **Securely expose apps across accounts or regions**
- No peering, no NAT, no public IPs

---

## 📌 Exam Pointers

- “Want EC2 in private subnet to access S3 with no NAT?” → ✅ Gateway VPC Endpoint
- “Need to access STS, Secrets Manager from private subnet?” → ✅ Interface Endpoint
- “Expose service across VPCs without peering?” → ✅ Use PrivateLink
- “Need to restrict S3 access to VPC only?” → ✅ S3 Bucket Policy + VPC Endpoint condition
- “Can PrivateLink connect multiple VPCs?” → ✅ Yes, but only as **consumer** per endpoint

---

## ⚠️ Nuances & Gotchas

- Interface Endpoints ≠ scalable by default — **each one = 1 ENI per AZ**
- You can’t use **NAT and Interface Endpoint** for same service — pick one
- Gateway Endpoints only work with **S3 and DynamoDB**
- Must allow traffic in SGs (Interface Endpoint uses ENIs)
- You can use **VPC Endpoint policies** to control access per principal/service

