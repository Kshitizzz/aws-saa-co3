# AWS Route 53

## Memory Hook

- "Route 53: The traffic cop of the internet. DNS + health + routing, all in one."
- Or
- "Your app’s GPS: It tells the traffic where to go."

## Must-Know Core Concepts

- **What is Route 53?**
  - It’s AWS’s scalable, highly available DNS and domain name registration service.
  - Maps **domain names** to **IP addresses** via DNS records.

- **Core Functions**
  - Domain Registration (optional)
  - DNS Record Management (A, AAAA, CNAME, MX, TXT, etc.)
  - Health Checks
  - Routing Policies (for intelligent traffic direction)

- **Record Types**
  - **A Record**: Maps to IPv4
  - **AAAA Record**: Maps to IPv6
  - **CNAME**: Alias for another domain (no root domain support)
  - **Alias Record**: AWS magic! Alias to ELB, S3, CloudFront, etc. (can be used at zone apex/root)
  - **MX, TXT, SPF, etc.**: Email and verification related

- **Routing Policies**
  - **Simple**: One record, basic DNS resolution
  - **Weighted**: Distribute traffic based on weights (e.g., 80-20 split)
  - **Latency-Based**: Route based on closest AWS region latency
  - **Failover**: Primary-secondary setup, with health checks
  - **Geolocation**: Route based on user’s location (India -> Mumbai region)
  - **Geoproximity**: Like geolocation, but with bias (only in Traffic Flow)
  - **Multivalue Answer**: Like simple, but can return multiple healthy IPs

- **Health Checks**
  - You can associate health checks with:
    - Individual records (e.g., A record for EC2)
    - Endpoints outside AWS
  - Supports failover routing if health check fails

- **Hosted Zones**
  - A container for all your DNS records for a specific domain
  - **Public Hosted Zone**: Resolves names over the internet
  - **Private Hosted Zone**: Used within a VPC

## Nuances & Edge Cases

- **Alias vs CNAME**: Alias records are AWS-specific, faster, and free — and work on root domains (CNAME does not).
- **Latency-based routing ≠ geolocation routing**: One is based on latency, other on geography.
- **Multivalue Answer Routing** supports health checks but is not a true load balancer.
- **Health checks cannot be used with alias records pointing to ELB** — ELB has its own health checks.

## Exam Pointers

- **Use Alias Record instead of CNAME for root domain (`example.com`) → CloudFront/ELB**
- **Latency routing for globally distributed apps → low latency for users**
- **Failover + health check = active-passive HA setup**
- **Weighted routing when you need gradual rollout (canary deployment)**
- **Private Hosted Zones work only within VPCs and must be explicitly associated**
- **Supports split-horizon DNS with public + private zones**

## General Explanation

- Route 53 is your global, DNS-based traffic director. It’s tightly integrated with AWS services and gives fine-grained control over traffic redirection using smart routing logic.
