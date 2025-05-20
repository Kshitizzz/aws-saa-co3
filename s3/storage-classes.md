# Amazon S3 Storage Classes

## Memory Hook
- “Data = Cold, Warmer, Hot”
- “The colder the data, the cheaper it gets — but slower and riskier to access”

---

## ✅ Overview of All Storage Classes

| Class                        | Durability         | Availability    | Min Duration | Retrieval Time | Use Case                              |
|-----------------------------|--------------------|-----------------|---------------|----------------|----------------------------------------|
| **S3 Standard**             | 99.999999999% (11 9s)| 99.99%          | None          | Instant        | General-purpose active data            |
| **S3 Intelligent-Tiering** | 11 9s              | 99.9–99.99%     | None          | Instant        | Auto-optimize cost for unknown access  |
| **S3 Standard-IA**         | 11 9s              | 99.9%           | 30 days       | Instant        | Infrequently accessed data             |
| **S3 One Zone-IA**         | 11 9s              | 99.5%           | 30 days       | Instant        | Infrequent, non-critical in 1 AZ only  |
| **S3 Glacier Instant**     | 11 9s              | 99.9%           | 90 days       | Instant        | Archive with fast access               |
| **S3 Glacier Flexible**    | 11 9s              | 99.9%           | 90 days       | 1–5 minutes     | Archival, deep cost savings            |
| **S3 Glacier Deep Archive**| 11 9s              | 99.9%           | 180 days      | 12–48 hours     | Coldest storage, long-term archives    |
| **S3 Reduced Redundancy**  | ❌ Deprecated       | —               | —             | —              | (Not used anymore)                     |

---

## 🧠 Intelligent Tiering Breakdown

S3 Intelligent-Tiering auto-moves objects based on access frequency:
- ✅ No retrieval fee
- 🧠 Charges small monthly **monitoring + automation fee**
- Has the following internal tiers:
  - Frequent
  - Infrequent (IA)
  - Archive Instant Access
  - Archive (Glacier Flexible) — opt-in only

Best for: *“I don’t know how often this will be accessed.”*

---

## 📦 Lifecycle Transitions

Use **S3 Lifecycle Policies** to:
- Move Standard → IA → Glacier
- Expire objects automatically
- Clean up previous versions or delete markers

## 🧠 Standard use case:

- Day 0 → S3 Standard
- Day 30 → Standard-IA
- Day 90 → Glacier Deep Archive

## Edge Cases & Gotchas
- ❌ Min storage duration fees apply even if you delete early

- ❌ Retrieval fees apply for IA/Glacier (not Standard or Intelligent)

- ❌ Deep Archive restores can take 12–48 hours

- ✅ Versioning applies regardless of class

- ✅ Encryption and replication work across classes

- ❌ One Zone-IA has no AZ redundancy — not for critical data

## Optimization Scenarios
- Need	Use Class
- Active app data -> S3 Standard
- Backup for restore -> S3 Standard-IA
- Log archives -> S3 Glacier Deep Archive
- Unknown access pattern -> S3 Intelligent-Tiering
- Cost-efficient ML pipeline cache -> S3 One Zone-IA (non-critical)
- DR archive with fast access -> S3 Glacier Instant Retrieval

## Exam Pointers
- “Which storage class has lowest latency?” → ✅ S3 Standard / Intelligent
- “Cheapest for long-term archive?” → ✅ Glacier Deep Archive
- “Need 1 AZ only, non-critical backups?” → ✅ One Zone-IA
- “Auto-tiering storage for unpredictable access?” → ✅ Intelligent-Tiering
- “Which class to use with minimum access guarantee?” → ❌ IA classes (have 30/90 day min)