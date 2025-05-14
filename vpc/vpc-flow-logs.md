# VPC Flow Logs & Integrations

## Memory Hook
- “Wireshark-lite for your VPC”
- “It sees who tried to talk to whom — and if it was allowed”

---

## ✅ Must-Know Core Concepts

- VPC Flow Logs capture **network-level metadata**
- Generated for:
  - **VPC level**
  - **Subnet level**
  - **ENI level** (most granular)
- Captures:
  - Source/destination IP
  - Source/destination port
  - Protocol
  - Action (`ACCEPT` or `REJECT`)
  - Traffic direction (`ingress` or `egress`)
  - Bytes, packets, timestamps

> 🧠 No payload/content is captured — only metadata

---

## 🗂️ Storage Options (Integrations)

| Destination         | Use Case                                   |
|----------------------|---------------------------------------------|
| **CloudWatch Logs**  | Real-time monitoring, alarms, dashboards    |
| **S3**               | Archival, Athena querying, long-term storage|
| **Kinesis Data Stream** | Real-time processing with Lambda, analytics |
| **Kinesis Firehose** | Stream to S3, Redshift, Splunk for indexing |

---

## 🧠 Key Integration Examples

### ✅ CloudWatch Logs
- Use for **filtering, alerts, near real-time dashboards**
- Flow logs land in a Log Group you configure
- Use **Logs Insights** to query: e.g., `REJECT`ed connections

### ✅ S3 + Athena
- S3 = cheaper for long-term storage
- Flow logs are written as gzipped text files (partitioned by time)
- Use Athena to query logs like a SQL table:
  ```sql
  SELECT srcaddr, dstaddr, action FROM vpc_logs WHERE action = 'REJECT'


## Nuances & Gotchas
- You must specify Log Format Version (2 is most recent)
- Logs are not retroactive — only start collecting after enabled
- You can apply filters: All, Accept, or Reject traffic
- Supports IPv6
- High log volume can incur cost (especially in CloudWatch)

## Exam Pointers
- “Want to monitor network connections in a VPC?” → ✅ VPC Flow Logs
- “Need to detect failed SSH attempts to private EC2s?” → ✅ Flow logs + Athena query
- “Need real-time stream of denied connections?” → ✅ Flow Logs to Kinesis Stream + Lambda
- “Low-cost archival of flow data for 1 year?” → ✅ Flow Logs to S3
- “Can you see packet contents?” → ❌ No, metadata only