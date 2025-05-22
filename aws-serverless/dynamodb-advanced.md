# Advanced DynamoDB – Architectural Use Cases

## Memory Hook  
- “Beyond tables: power = in streams, regions, time, and integrations”

---

## ✅ 1. DAX (DynamoDB Accelerator)

### What It Is  
- Fully managed, **in-memory caching layer** for DynamoDB
- Reduces read latency from **milliseconds → microseconds**

### Use Cases  
- High-read, low-write applications (e.g., product catalog, social feeds)
- Real-time apps needing **read latency <1ms** without adding Redis
- Gaming leaderboards, real-time personalization

### Architecture  
- Drop-in replacement for existing SDK (`DynamoDB.Client → DAXClient`)
- Works transparently for reads (`GetItem`, `Query`)
- **Does not support write-through caching**

---

## ✅ 2. DynamoDB Streams

### What It Is  
- Change data capture (CDC) log of **item-level changes**
- Triggers **Lambda, Kinesis, or other processors**

### Use Cases  
- **Event-driven workflows** (send email on new order)
- **Audit logs** for regulatory systems
- **Real-time ETL** (transform + sync to S3, Redshift)

### Architecture  
- Streams contain `INSERT`, `MODIFY`, `REMOVE` events
- Integrated directly with **Lambda (event source mapping)**

---

## ✅ 3. Stream Processing with Kinesis (Data Streams + Firehose)

### When to Use Instead of DynamoDB Streams  
- Need **fan-out**, **custom ETL**, **cross-region processing**
- Want to connect to services like **OpenSearch**, **Redshift**, or **S3**

### Kinesis Data Streams  
- Real-time data pipeline from app → processor → downstream

**Use Case**: App writes to DynamoDB + pushes custom metrics to Kinesis → processed by consumers

### Kinesis Firehose  
- Fully managed, **buffered delivery** to:
  - S3
  - Redshift
  - OpenSearch
  - 3rd party (Datadog, Splunk)

**Use Case**: Write logs to DynamoDB → replicate to S3 for long-term analytics

---

## ✅ 4. DynamoDB Global Tables

### What It Is  
- Multi-region, multi-master replication of DynamoDB
- Automatically replicates all changes between regions

### Use Cases  
- Global mobile apps needing **low-latency** regional reads/writes
- Business continuity: if Region A fails, Region B keeps operating
- Disaster Recovery (DR) with **active-active architecture**

### Architecture  
- Synchronous replication in background
- Requires **identical table schema** in each region
- ⚠️ Conflict resolution is **last-writer-wins** (based on timestamps)

---

## ✅ 5. DynamoDB TTL (Time-to-Live)

### What It Is  
- Per-item **expiration timestamp**
- Items auto-deleted **asynchronously** after expiry

### Use Cases  
- Ephemeral sessions (auth tokens, carts)
- Cleanup temp items (caches, queues)
- GDPR-compliant data expiry

### Architecture  
- Set TTL field (must be numeric UNIX timestamp)
- AWS deletes item **eventually (not guaranteed instantly)**

---

## ✅ 6. Backups: Point-In-Time Recovery (PITR) vs On-Demand

### PITR  
- Continuous backups for last 35 days
- Restore to **any second-level granularity**
- ✅ Used for:
  - Accidental overwrite/revert
  - Logical corruption
  - Restore to specific timestamp

### On-Demand Backup  
- Manual, full backup
- Long-term retention
- ✅ Used for:
  - Compliance snapshots
  - Monthly backups
  - Before risky schema changes

---

## ✅ 7. DynamoDB + S3 Integration (Import/Export)

### Export to S3  
- Serverless snapshot of DynamoDB to **S3 in Parquet** format  
- ✅ Use with:
  - Athena
  - Redshift Spectrum
  - Machine Learning

**Use Case**: Export data nightly to S3 for BI dashboards

### Import from S3  
- Upload structured JSON to S3 → Import to DynamoDB table
- Useful for:
  - Backfilling historical data
  - Initial bootstrapping
  - Cross-account data migration

---

## 📌 Exam Pointers

- “Low latency read with no backend change?” → ✅ DAX
- “Trigger ETL on every item write?” → ✅ DynamoDB Streams + Lambda
- “Export DynamoDB to analytics?” → ✅ Export to S3 (Parquet)
- “Need DR in another region?” → ✅ Use Global Tables
- “Auto-delete temp items after X mins?” → ✅ Use TTL
- “Restore from 10 mins ago due to data corruption?” → ✅ PITR
- “Stream DynamoDB changes into OpenSearch?” → ✅ Kinesis Firehose

