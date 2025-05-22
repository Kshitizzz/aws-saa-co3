# S3 Consistency Model & Event Notifications

## Memory Hook  
- “Read-after-write, even globally”  
- “Trigger everything from a single PUT”

---

## ✅ S3 Consistency Model

| Operation Type     | Consistency Behavior                                  |
|--------------------|--------------------------------------------------------|
| **PUT (new object)**     | ✅ **Read-after-write consistency**               |
| **PUT overwrite**        | ✅ Strong consistency                             |
| **DELETE**               | ✅ Immediate consistency                          |
| **LIST**                 | ✅ Eventually consistent **(across prefixes)**    |

### Notes
- S3 now offers **strong consistency for all operations** by default across **all AWS Regions**
- There's **no delay in seeing new or updated objects**
- Listing operations might not reflect changes immediately under heavy write/delete load

---

## 🧠 Practical Implications

- ✅ You can safely `GET` an object right after `PUT` it
- ❗ Be cautious when relying on `LIST` for new keys in parallel workflows (e.g., batch ETLs)
- ✅ Use S3 event notifications for event-driven reliability instead of relying on `LIST`

---

## ✅ S3 Event Notification Mechanisms

### What It Is  
S3 can **trigger notifications** when certain events happen on a bucket:
- Object Created
- Object Removed
- Multipart upload completed
- Others…

---

## 🔄 Supported Destinations

| Destination Type       | Use Case                                |
|------------------------|------------------------------------------|
| **Amazon SQS**         | Queue-based pipeline, decoupled systems |
| **Amazon SNS**         | Fan-out to multiple endpoints            |
| **AWS Lambda**         | Serverless, real-time object processors |
| **Amazon EventBridge** | Event routing, filtering, cross-service integration |

---

## 🧠 Lambda Triggers

- Used for **real-time processing**:
  - Image thumbnailing
  - Metadata extraction
  - Virus scanning
- Triggered **per object upload**
- ✅ Can filter by prefix/suffix
- ❌ Max object notification size = metadata only, **not file content**

---

## 🧠 SQS Triggers

- Best for **decoupled** or **batch pipelines**
- Example: Data lake ingestion → S3 → SQS → ETL
- ✅ Scalable, durable
- ❗ Must manually delete messages after processing

---

## 🧠 EventBridge Integration

- Advanced event routing
- Allows **centralized event management** across services
- Can match specific event patterns (e.g., only PUTs in `logs/` folder)
- Can send events to:
  - Lambda
  - Step Functions
  - Kinesis
  - …anything that integrates with EventBridge

---

## ⚠️ Gotchas

- You must configure event notifications at the **bucket level**
- Only one destination per event type per bucket (unless using EventBridge)
- Event delivery is **best-effort** for S3 direct-to-Lambda/SQS/SNS
- ✅ EventBridge provides **more reliable, flexible** delivery than legacy triggers

---

## 📌 Exam Pointers

- “Need real-time object processor (e.g., image resizer)?” → ✅ Use S3 → Lambda
- “Ingest pipeline needing durability + retries?” → ✅ S3 → SQS
- “Want complex filtering + routing + fan-out?” → ✅ S3 → EventBridge → other targets
- “List consistency delay is causing missed files?” → ✅ Switch to event-driven model

