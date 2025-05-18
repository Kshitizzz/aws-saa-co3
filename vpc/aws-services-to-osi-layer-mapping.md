# AWS Network Security Services – Layer-Wise Mapping

## Memory Hook

- “Security = layered onion, not one gate”
- “SGs for instances, NACLs for subnets, Firewalls for VPCs, WAFs for HTTP”

---

## 🧱 OSI Layer Mapping

| Layer | AWS Service / Appliance          | Description                                                   |
|-------|----------------------------------|---------------------------------------------------------------|
| L7    | **AWS WAF**                      | Filters HTTP/S requests (URI, headers, body, IP, geolocation) |
| L7    | **Application Load Balancer**    | Routes HTTP/S traffic, integrates with WAF                     |
| L7    | **AppSync / API Gateway**        | Entry points for APIs, protected by WAF                        |
| L7    | **Shield Advanced** (some DDoS)  | Inspects HTTP floods                                           |
| L7    | **Network Firewall** (FQDN/HTTP) | Deep packet filtering by domain/HTTP                          |
|-------|----------------------------------|---------------------------------------------------------------|
| L4    | **Network Load Balancer (NLB)**  | TCP/UDP level load balancing                                   |
| L4    | **Security Groups (SGs)**        | Instance-level allow rules (stateful)                         |
| L4    | **AWS Network Firewall**         | Stateful IP/port filtering                                     |
| L4    | **Shield** (standard & adv)      | Protects ALB/NLB from L3/L4 attacks                           |
| L4    | **Gateway Load Balancer (GWLB)** | Inline forwarding of L3/L4 packets to appliances               |
|-------|----------------------------------|---------------------------------------------------------------|
| L3    | **Network ACLs (NACLs)**         | Subnet-level IP filtering (stateless)                         |
| L3    | **IGW / NATGW / EOIGW**          | Gateways for routing, not enforcement (but control flow)       |
| L3    | **Transit Gateway**              | Central hub, supports routing/firewall attachments            |
| L3    | **Route Tables**                 | Path decision, not filtering                                  |

## AWS WAF vs AWS Network Firewall

## Memory Hook

- “WAF for web apps, Firewall for VPC pipes”
- “WAF blocks bad requests; Firewall blocks bad packets”

---

## ✅ Comparison Table

| Feature                | AWS WAF                               | AWS Network Firewall                       |
|------------------------|----------------------------------------|---------------------------------------------|
| **Layer**              | Layer 7 (HTTP/S)                       | Layers 3, 4, and 7 (IP, port, DNS, HTTP)    |
| **Placement**          | ALB, CloudFront, API Gateway, AppSync | VPC subnet (via routing or GWLB)           |
| **Traffic Type**       | HTTP/S only                            | All IP traffic (TCP/UDP, DNS, TLS, HTTP)   |
| **Granularity**        | Request-level (URI, header, query)     | Packet/session level (IP, port, FQDN, TLS) |
| **Stateful?**          | ✅ Yes                                  | ✅ Yes (stateful + stateless rule support)  |
| **Use Case**           | App-layer attacks (SQLi, XSS, bots)    | Network-level threats (port scans, DNS exfiltration) |
| **Rule Engine**        | Rule groups, managed rules             | Stateless + Stateful rule groups           |
| **Integration**        | Native to L7 AWS services              | Requires routing through firewall subnet   |
| **Cost Model**         | Per web ACL + request                  | Per endpoint + per GB processed            |

---

## 🧠 When to Use What

| Scenario                                     | Use                             |
|----------------------------------------------|----------------------------------|
| Block SQLi on API Gateway                    | ✅ AWS WAF                       |
| Block egress to unknown domains from EC2     | ✅ AWS Network Firewall          |
| Stop HTTP POST abuse to ALB                  | ✅ AWS WAF                       |
| Detect port scan from EC2                    | ✅ AWS Network Firewall          |
| Multi-account firewall policy enforcement    | ✅ Use **Firewall Manager** (wraps both)


