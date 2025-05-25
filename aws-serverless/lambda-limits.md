# AWS Lambda Limits (SAA-C03 + System Design)

## Memory Hook  
- “Limits aren’t just performance — they define what your Lambda *can’t* do.”

---

## ✅ General Execution Limits

| Limit Type                 | Value                             |
|----------------------------|-----------------------------------|
| **Max execution timeout**   | 900 seconds (15 minutes)         |
| **Min execution timeout**   | 1 second                         |
| **Memory allocation**       | 128 MB – 10,240 MB (10 GB)       |
| **CPU allocation**          | Proportional to memory           |
| **Ephemeral disk (`/tmp`)** | 512 MB (default), **up to 10 GB** with `EphemeralStorage` config |
| **Environment variables**   | Max 4 KB per key; 65 KB total    |
| **Deployment package size (ZIP)** | 50 MB (direct upload)        |
| **Deployment via S3**       | 250 MB unzipped (code + deps)    |
| **Container image size**    | 10 GB (must be in ECR)           |
| **Concurrent executions (account-wide)** | 1,000 (soft limit, raiseable) |

---

## ✅ Invocation & Payload Limits

| Limit                             | Value                          |
|----------------------------------|--------------------------------|
| **Event payload size (sync)**     | 6 MB via API Gateway / SDK     |
| **Event payload size (async)**    | 256 KB                         |
| **Event payload (synchronous invoke)** | 6 MB                       |
| **Event response size**           | 6 MB                           |
| **Max batch size (SQS)**          | 10 messages (FIFO), 10,000 (std) |
| **Max batch size (Kinesis/DDB streams)** | 10,000 records (1 MB total) |

---

## ✅ Layers & Versions

| Limit                        | Value                              |
|-----------------------------|-------------------------------------|
| **Max # of layers per function** | 5                               |
| **Layer size limit**          | 50 MB per layer (zipped)          |
| **Max versions per function** | 75 (delete old to make room)      |

---

## ✅ Concurrency & Scaling

| Concept                     | Default/Limit                      |
|-----------------------------|-------------------------------------|
| **Burst scaling (per region)** | Starts at ~500–3,000/sec depending on region |
| **Reserved concurrency per function** | Configurable up to account limit |
| **Provisioned concurrency** | No set limit, but cost applies     |

---

## 📌 Exam Pointers

- “Function runs over 15 minutes?” → ❌ Lambda not suitable (use ECS or Step Functions)
- “Lambda hits storage space error writing to `/tmp`?” → ✅ Increase ephemeral storage (up to 10 GB)
- “You need to deploy a 200 MB ML package?” → ✅ Use Lambda Container Image (up to 10 GB via ECR)
- “Cold starts are a problem?” → ✅ Use provisioned concurrency
- “Function is being throttled?” → ✅ Check reserved concurrency + account limit


