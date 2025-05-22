# AWS CloudFront - Core Components Explained

## Memory Hook

- "Edge = Near the user. Origin = Where truth lives."

---

## ✅ Edge Location

- AWS-operated **datacenter close to end users**.
- Caches and serves content via CloudFront for low latency.
- Does **not** run compute or store full infrastructure — it’s for caching & TLS termination.
- Used for:
  - Static content caching
  - TLS offloading
  - WAF inspection
  - Lambda@Edge execution

---

## ✅ CloudFront Origin

### S3 Origin

- Static files (HTML, CSS, JS, images, etc.) served directly from S3 bucket.
- Needs **public access** or **OAI/Origin Access Control** for private buckets.
- Optimized automatically for static file delivery.

### Custom Origin

- Any HTTP server → EC2 instance, ALB, on-premises server, etc.
- Must handle **HTTP 200/404/500** codes correctly.
- Supports:
  - Path-based routing
  - Multiple origins
  - TLS termination at origin or at CloudFront

### VPC Origin (Private)

- EC2, ALB, or service inside a VPC (private subnet).
- Requires:
  - PrivateLink
  - AWS Global Accelerator (optional)
  - NAT Gateway or Lambda@Edge for access routing

---

## 🔐 S3 / CloudFront Signed URLs

- Generate **time-limited** and/or **IP-restricted** access to S3 objects.
- Common for:
  - Temporary downloads
  - Content you don’t want publicly exposed
- Works with both **S3 directly** and via **CloudFront**.
- Requires:
  - Signed using IAM credentials or CloudFront key group.

---

## 🚀 API Acceleration

- CloudFront placed in front of:
  - **API Gateway**
  - **ALB with REST APIs**
- Benefits:
  - Reduces latency with caching (even partial responses)
  - Protects API with WAF
  - Terminates TLS at the edge
  - Adds support for **Geo-blocking, Header re-writing, Rate limiting**
- Used in:
  - Global SaaS apps
  - GraphQL or REST APIs

---

## Exam Pointers

- "Edge Location = Cache near user"  
- "Origin = S3 or HTTP backend"  
- "Signed URL = Time-bound secure access"  
- "Custom Origin = Anything not S3"  
- "Use API acceleration = CloudFront + API Gateway"  
- "Private EC2 behind CloudFront?" → Needs **OAI/OAC**, or **VPC NAT/Link setup**

