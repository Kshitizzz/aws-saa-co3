# Amazon S3 Object Lambda – Transform Objects on the Fly

## Memory Hook  
- “Lambda runs before the S3 object hits the client”  
- “Intercept. Transform. Serve.”

---

## ✅ What Is S3 Object Lambda?

S3 Object Lambda Access Points allow you to **intercept S3 GET/HEAD requests** and run a **Lambda function to transform the object** before it's returned to the client.

Instead of:
→ Client → S3 → Raw Object  
It becomes:  
→ Client → Object Lambda Access Point → Lambda → Transformed Object → Client

---

## 🔧 How It Works with S3 Access Points

- You **must configure a standard S3 Access Point** as the source.
- Then you create an **Object Lambda Access Point** that:
  - Proxies requests to the base access point
  - Triggers your Lambda function
  - Returns transformed content to the requester

---

## ✅ Real-World Use Cases

| Use Case                                | How Object Lambda Helps                        |
|------------------------------------------|------------------------------------------------|
| Redact PII from objects dynamically      | Lambda filters/obfuscates PII on-the-fly       |
| Convert raw data to CSV, JSON, Parquet   | Lambda transforms format at read-time          |
| Inject metadata (e.g., timestamp, userID)| Lambda augments object with runtime context    |
| Resize/Watermark an image before serving | Lambda uses PIL/ImageMagick to modify object   |
| Serve different versions per user        | Lambda applies user-specific logic to data     |

---

## 🧩 What Is "Multi-Tenant Bucket Design"?

> A **multi-tenant bucket** is one shared by **many users, teams, or applications**, usually in a large organization or data lake.

Instead of creating separate buckets for:
- App A, App B, App C  
You use **one centralized bucket** with:
- Multiple prefixes, or
- Multiple Access Points (one per team/app/user)

**Object Lambda allows each tenant to get a “filtered” or “custom” view of the same object**, based on:
- Their identity
- Their role
- Runtime logic in Lambda

✅ This pattern reduces redundancy and supports **fine-grained, per-tenant content delivery**.

---

## 🛠️ Supported Operations

- Only supports:
  - `GetObject`
  - `HeadObject`
  - `ListObjects` (optional customization)

Not supported for `PutObject`, `DeleteObject`, or replication.

---

## 🔐 Security & Permissions

- Lambda needs access to:
  - The original S3 object (via access point)
  - The S3 Object Lambda invocation event
- Object Lambda Access Points use **their own ARN**
- You can enforce IAM policies and Lambda logic together

---

## ❗ Limitations

- ❌ No write-time transformation — only read-time
- ❌ Slight latency from Lambda execution
- ❌ Not supported with EventBridge or S3 Replication
- 💲 You are charged for:
  - Lambda execution time
  - Regular S3 GET request

---

## 📌 Exam Pointers

- “Need to return a filtered/modified object without saving extra versions?” → ✅ Use S3 Object Lambda
- “Can Object Lambda work without a base access point?” → ❌ No — it must be linked to a standard S3 Access Point
- “Want different tenants to view object differently?” → ✅ Object Lambda + dynamic logic
- “Can I use Object Lambda to upload transformed files?” → ❌ No — read-only

---

## 🔁 Flow Summary

1. Upload raw object to S3
2. Create a standard S3 Access Point (source)
3. Create Object Lambda Access Point → link to source
4. Attach Lambda function to transform object
5. Client accesses object via Object Lambda endpoint → gets modified response
