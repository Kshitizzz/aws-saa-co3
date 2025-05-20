# Amazon S3 – Versioning, Delete Markers, and Replication

## Memory Hook
- “Delete ≠ Delete”
- “Replication ≠ Recovery”
- “Versions protect data, but also create cost and complexity”

---

## ✅ Must-Know: S3 Versioning

- **Versioning enables S3 to keep multiple versions of the same object.**
- Enabled at the **bucket level**, not per object
- Every PUT/DELETE creates a **new version ID**

### ✅ Behavior

| Action         | What Happens                                   |
|----------------|------------------------------------------------|
| **PUT**        | Creates a new version                          |
| **DELETE**     | Adds a **Delete Marker**, doesn’t delete versions |
| **GET**        | Returns the **latest version** unless specified |
| **DELETE (with version ID)** | Permanently deletes that version   |

🧠 *Default GET and LIST ignore older versions and show only the latest*

---

## ❌ Delete Marker – Key Concept

> A delete marker is a **placeholder** version with no content.

| Scenario                                      | Outcome                        |
|-----------------------------------------------|--------------------------------|
| DELETE on versioned object                    | Adds a delete marker           |
| DELETE marker is present                      | Object seems "deleted"         |
| Remove delete marker                          | Object is “undeleted”          |
| DELETE (with version ID of delete marker)     | Object is "restored" (visible again) |

🧠 *Delete marker ≠ actual deletion*

---

## 🧪 Practical Scenarios

- **Recover deleted object?**
  → Find the version before delete marker and restore it

- **List shows empty?**
  → Likely hidden by delete marker

- **Empty bucket policy doesn't reduce storage?**
  → Because previous versions still exist

---

## 📦 S3 Replication Overview

| Type               | Purpose                                       |
|--------------------|-----------------------------------------------|
| **CRR** (Cross-Region Replication) | Replicate objects to a different region      |
| **SRR** (Same-Region Replication) | Replicate to another bucket in same region  |

- ✅ Uses **asynchronous, near real-time replication**
- ✅ **Per-bucket, per-prefix or tag-based**
- ✅ Must have:
  - Versioning **enabled on both source and destination**
  - IAM role for S3 to replicate on your behalf

---

## 🔄 Versioning + Replication Integration

| Event Type               | Replicated?                             |
|--------------------------|------------------------------------------|
| **New object version**    | ✅ Yes                                   |
| **Overwrite (PUT)**       | ✅ Yes (creates new version at dest)     |
| **DELETE (no version ID)**| ✅ Yes — replicates the **delete marker** |
| **DELETE with version ID**| ❌ No — delete of specific version does NOT replicate |

🧠 Delete marker = replicated  
🧠 Delete version = not replicated

---

## ⚠️ Nuances & Edge Cases

- Replication is **one-way** only — no bidirectional sync
- You can **filter by prefix or object tag**
- Existing objects before enabling replication are ❌ not auto-replicated
- **Replicated objects retain version IDs**, but version IDs at destination are different
- Must use **S3 Bucket Policy + KMS permissions** if SSE-KMS is involved

---

## 🧠 Cost Implications

- Versioning can double/triple storage usage
- CRR incurs:
  - Storage cost in destination
  - Replication PUT cost
  - Inter-region transfer ($0.02–$0.09/GB)

✅ Use **lifecycle rules** to manage expired versions

---

## 📌 Exam Pointers

- “User deletes object, but it’s versioned. Can it be recovered?” → ✅ Yes, remove delete marker
- “Can delete markers be replicated?” → ✅ Yes
- “Can specific version deletes be replicated?” → ❌ No
- “Want audit copy of data in another AZ?” → ✅ Use SRR (Same Region)
- “Want DR copy in another region?” → ✅ Use CRR
- “Bucket has versioning, user uploads 10 times. How many objects exist?” → ✅ 10 versions
- “Want to exclude objects starting with ‘tmp/’?” → ✅ Use prefix filter in replication rule

