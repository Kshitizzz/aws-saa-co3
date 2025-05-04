## Supporting Services

### 🧱 Security Groups

- Virtual firewalls for EC2, RDS, etc. at instance level.
- Operates at Layer 3/4 (IP/port).
- **Stateful**.
- **Regional**.

### 🔗 API Gateway

- Exposes **REST**, **HTTP**, and **WebSocket APIs**.
- Integrated with Lambda, VPC, IAM, WAF.
- Handles throttling, caching, transformation.
- **Regional** (REST/HTTP), **Edge-optimized** (via CloudFront), **Private** (VPC-only).

### 🌐 AWS Global Accelerator

- Uses AWS global edge network + Anycast IPs.
- Improves availability & latency by routing to optimal endpoints.
- Works with ALB, NLB, EC2, Elastic IP.
- **Global service**.

### 🚀 AWS AppSync

- Managed **GraphQL API** service.
- Real-time updates with subscriptions.
- Connects to DynamoDB, Lambda, RDS.
- **Regional**.

### 🌎 CloudFront

- Global CDN for caching content.
- Works with S3, ALB, API Gateway, Lambda@Edge.
- **Global service**.
- Can apply **global-scope WAF WebACLs**.

---

## Nuances & Edge Cases

- WAF cannot attach to **NLB** or **Global Accelerator** (not HTTP-based).
- Global Accelerator = Layer 4 routing with static Anycast IPs.
- Firewall Manager helps enforce compliance across multiple AWS accounts.
- Managed rule groups in WAF save time, follow best practices.

---

## Exam Pointers

- 🔐 Use **WAF** for custom traffic filtering at HTTP(S) level.
- 🛡️ Use **Shield Advanced** when SLA, compliance, or DDoS mitigation matters.
- 🧠 Use **Firewall Manager** in **AWS Org** setups for centralized policy management.
- 🧱 **Security Groups = Stateful**, NACLs = Stateless (not covered here).
- 🌍 **CloudFront is Global**, and works with WAF (global ACLs).
- ⚡ **Global Accelerator** provides performance boost and failover for **non-HTTP** traffic.
- ⚙️ **API Gateway** is the go-to service for building **serverless APIs**.
- 🔌 **AppSync** is for managed **GraphQL APIs** with real-time features.