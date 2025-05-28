# Lambda@Edge vs CloudFront Functions – Practical Comparison

## Memory Hook  
- “CloudFront Functions = ultra-fast, ultra-light edge logic”  
- “Lambda@Edge = heavyweight edge compute with full power”

---

## ✅ TL;DR Use Case Split

| Feature / Use Case                         | **CloudFront Functions** | **Lambda@Edge**          |
|--------------------------------------------|---------------------------|---------------------------|
| **Runtime**                                | JS (only)                 | Node.js, Python (multi-runtime) |
| **Execution timing**                       | Viewer request/response only | All 4 CloudFront lifecycle phases |
| **Latency**                                | ⚡ Ultra-low (~ms)         | Slightly higher (cold starts possible) |
| **Max execution time**                     | 1 ms                      | 5 sec (Viewer), 30 sec (Origin) |
| **Payload limit**                          | 1 KB                      | 1 MB                      |
| **Memory**                                 | 2 MB                      | Up to 3,008 MB            |
| **Cost**                                   | ⚡ Cheap (microseconds)    | More expensive (by time + data transfer) |

---

## 🔁 Lifecycle Phases (CloudFront)

| Phase                | Supported In       |
|----------------------|--------------------|
| **Viewer Request**    | ✅ Both            |
| **Origin Request**    | ❌ CloudFront Fn   | ✅ Lambda@Edge  
| **Origin Response**   | ❌ CloudFront Fn   | ✅ Lambda@Edge  
| **Viewer Response**   | ✅ Both            |

---

## 🔧 What Each Is Good For

### ✅ CloudFront Functions

- Lightweight **request rewriting**, **URL routing**, **header manipulation**
- **Geo-blocking**, **A/B testing**, **custom caching logic**
- ✅ Executes in *every* CloudFront edge location
- 🧠 Think: JavaScript CDN logic

**Example Real Use Cases**:
- Fastly alternative for CDN customization (e.g., for Next.js static exports)
- Block requests by geo-IP at CDN level
- Add custom headers or route traffic based on cookies

---

### ✅ Lambda@Edge

- Full-blown compute at edge  
- Can make **network calls, auth checks, I/O operations**, etc.
- Used for:
  - SSR (Server-Side Rendering)
  - Dynamic redirects
  - JWT validation
  - Personalized content generation

**Example Real Use Cases**:
- **Next.js server-side rendering** at edge using `getServerSideProps` + Lambda@Edge
- **Cloudinary CDN plugins** using Lambda@Edge for image optimization
- Multi-tenant applications where each domain gets **dynamic routing logic**

---

## 🧪 Real-World Tech Examples

### 🧰 Next.js + Vercel (open-source/hosted)

| Feature                             | Used Technology          |
|-------------------------------------|--------------------------|
| Static asset rewrite at CDN        | ✅ CloudFront Function   |
| SSR with regional rendering         | ✅ Lambda@Edge           |
| Preview modes, A/B testing         | ✅ CloudFront Function   |

Vercel's open-source serverless functions + edge middleware mimic these patterns under the hood.

---

### 🧰 AWS Amplify Hosting

- **CloudFront Functions** used for:
  - Rewriting routes (SPA fallback)
  - Security headers
- **Lambda@Edge** used for:
  - Authentication flows
  - SSR with dynamic data

---

## 📌 When to Use What

| Scenario                                     | Use            |
|----------------------------------------------|----------------|
| Need blazing fast, cheap request manipulation | CloudFront Fn |
| Need to validate JWT at edge                 | Lambda@Edge   |
| Want SSR with personalization                | Lambda@Edge   |
| Simple geo-blocking or path rewriting        | CloudFront Fn |
| Need to call external API or DB              | Lambda@Edge   |
| Need all lifecycle hooks                     | Lambda@Edge   |

---

## 🧠 Exam Pointers (SAA-C03)

- “Add a security header to every CloudFront response with low latency” → ✅ CloudFront Function  
- “Fetch dynamic user data from DynamoDB during page load” → ✅ Lambda@Edge  
- “Block access from certain countries at edge with lowest cost” → ✅ CloudFront Function  
- “Handle auth + origin transformation at edge” → ✅ Lambda@Edge

