# EC2 Storage Options – Deep Dive (EBS, EFS, FSx, Instance Store)

## Memory Hook  
- “EBS = Block for one EC2”  
- “EFS = Shared file system”  
- “FSx = Managed enterprise-grade FS”  
- “Instance Store = Local, volatile speed demon”

---

## ✅ 1. Amazon EBS (Elastic Block Store)

> Block-level storage attached to a single EC2 instance

### Types of EBS Volumes

| Type           | Use Case                              | Notes                              |
|----------------|----------------------------------------|-------------------------------------|
| gp3 (General Purpose SSD) | ✅ Default choice                | Predictable performance, 3,000 IOPS baseline |
| gp2 (Old gen SSD)         | Legacy, still supported         | Performance tied to volume size    |
| io2/io2 Block Express      | I/O-intensive apps (databases) | Up to 64,000 IOPS, durable          |
| st1 (Throughput HDD)      | Big, sequential workloads       | Data warehouses, logs               |
| sc1 (Cold HDD)            | Infrequent access               | Archive-like, not bootable          |

### Key Features

- ✅ Snapshots → stored in S3, used for backup, cloning
- ✅ Encrypted with KMS (at rest, in-transit)
- ✅ Supports resizing, changing type, adding IOPS live
- ✅ Durable: **replicated within an AZ**

### Limitations

- ❌ Cannot be shared across AZs
- ❌ One EC2 per EBS volume (but multi-attach works for io1/io2 with clustering apps)

---

## ✅ 2. Instance Store (a.k.a. Ephemeral Storage)

> High-speed **physically attached SSD/HDD** to the EC2 host

### Key Traits

| Feature                | Value                         |
|------------------------|-------------------------------|
| Volatile?              | ✅ Yes (data lost on stop/terminate) |
| Speed                  | ✅ Ultra-fast (NVMe/SSD)       |
| Cost                   | ✅ Included with instance cost |
| Use Cases              | Temp files, cache, scratch data |

🧠 Use it when you can **tolerate data loss** (e.g., batch processing)

---

## ✅ 3. Amazon EFS (Elastic File System)

> Scalable, shared **NFS-based file system** for Linux EC2 instances

### Key Features

- ✅ Fully managed, serverless file system
- ✅ Mountable by **100s of instances**
- ✅ Grows/shrinks automatically
- ✅ Supports **burst throughput** or **provisioned throughput**
- ✅ Regional (not AZ-bound)
- ✅ Supports KMS encryption

### Use Cases

- Shared home dirs
- Lift-and-shift NFS apps
- HPC apps, CMS

### Access & Performance Modes

| Mode                 | Description                          |
|----------------------|--------------------------------------|
| General Purpose      | ✅ Default, low latency               |
| Max I/O              | High-throughput, higher latency      |
| One Zone EFS         | Cheaper, AZ-scoped                   |

---

## ✅ 4. FSx – Managed Enterprise File Systems

### ✅ FSx for Windows File Server

> Fully managed SMB file system for Windows EC2 instances

- ✅ AD-integrated (supports ACLs)
- ✅ Used for Windows apps (SQL Server, SharePoint)
- ✅ Multi-AZ or single-AZ deployment
- ✅ Supports backup/restore, quotas, data deduplication

### ✅ FSx for Lustre

> High-performance parallel file system for compute-heavy workloads

- ✅ Integrates with S3 for lazy-loading files
- ✅ Ideal for ML/AI, genomics, financial modeling
- ✅ Supports 100s of GBps throughput and millions of IOPS

---

## 🧠 Comparison Summary

| Feature               | EBS                       | EFS                       | FSx                              | Instance Store         |
|------------------------|---------------------------|----------------------------|-----------------------------------|------------------------|
| Type                   | Block                     | File (NFS)                 | File (SMB/Lustre)                 | Block (local)          |
| Shared?                | ❌ (1 EC2)                 | ✅ (many EC2s)             | ✅ (depends on FSx type)          | ❌                     |
| Persist after stop?    | ✅                         | ✅                          | ✅                                 | ❌                     |
| Max Throughput         | Up to 4,000 MB/s (io2)     | Scales with usage          | FSx for Lustre: insane parallelism| Highest (but volatile) |
| AZ-scope               | Single AZ (multi-AZ via snapshot) | ✅ Regional             | Depends on config                 | AZ-bound              |
| Use Case               | Boot volumes, databases    | Shared content, home dirs  | Windows file shares, HPC         | Cache, scratch         |

---

## 📌 Exam Pointers

- “Which EC2 storage is best for sharing between 100s of instances?” → ✅ EFS
- “Need fast local storage for batch job temp files?” → ✅ Instance Store
- “Require POSIX file system + NFS + auto scale?” → ✅ EFS
- “Need NTFS + SMB + Windows ACLs?” → ✅ FSx for Windows
- “Need storage with IOPS tuning + snapshot backup?” → ✅ EBS
- “High-performance compute app with large datasets?” → ✅ FSx for Lustre
