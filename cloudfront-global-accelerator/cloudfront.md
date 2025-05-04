# AWS CloudFront (Content Delivery Network)

## Memory Hook

- "CloudFront = Bouncer at the door, Cache in the alley, Armor on the chest."
- Or
- "Fast, Safe, Cached — From AWS Edge to Your Browser."

---

## ✅ Must-Know Core Concepts

- **Content Delivery Network (CDN)** service that delivers content via global **Edge Locations**.
- Reduces **latency, DDoS exposure, and origin load**.
- Works with:
  - S3 static websites
  - ALB, EC2, API Gateway
  - Media Streaming (HLS/DASH)
- Supports:
  - **HTTP/HTTPS**
  - **TLS termination** at edge
  - **Gzip & Brotli compression**
  - **Signed URLs and cookies** for secure access
  - **Origin Shield** for centralized caching
- **Regional Edge Caches** sit between Edge and Origin (adds extra buffer).
- Can route requests to multiple origins (failover, dynamic content).

---

## ⚠️ Nuances & Edge Cases

- Must use **ACM certs in us-east-1** for HTTPS.
- **Field-level encryption** available for sensitive form data.
- Paired with:
  - **AWS WAF** for L7 filtering
  - **Shield** (Standard by default) for DDoS protection
  - **CloudWatch/Access Logs** for observability
- Can be used with **Lambda@Edge** for request/response manipulation at edge.
- Not ideal for non-HTTP protocols — that’s where **Global Accelerator** comes in.

---

## 📌 Exam Pointers

- If the question says:
  - “Accelerate content globally” → ✅ CloudFront
  - “Reduce latency for static + dynamic content” → ✅ CloudFront
  - “Protect S3 origin with signed URLs” → ✅ CloudFront
  - “Terminate TLS at edge + add WAF” → ✅ CloudFront
  - “Inspect or transform HTTP headers before origin” → ✅ CloudFront + Lambda@Edge

- Remember:
  - **Global** service
  - Needs **ACM cert in us-east-1**
  - **Edge-first** caching & security

---

## 🧠 When to Use CloudFront

- High-traffic websites / global apps
- API acceleration (REST APIs via API GW)
- Protecting S3/EC2 origin behind CDN
- Compliance with geo-blocking, HTTPS enforcement
