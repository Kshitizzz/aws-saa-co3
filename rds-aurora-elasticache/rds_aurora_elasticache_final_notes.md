
# AWS RDS, Aurora & ElastiCache - Consolidated Study Notes

## Amazon RDS (Relational Database Service)

### Memory Hook

- "RDS = Managed SQL, minus the admin headache."
- "RDS handles the undifferentiated heavy lifting of database ops."

### Must-Know Core Concepts

- Supports **MySQL, PostgreSQL, MariaDB, Oracle, and SQL Server**.
- Handles backups, patching, failover, and scaling.
- Supports **Multi-AZ deployments** as standby DBs for high availability (standby not for reads).
- Supports **Read Replicas** for scaling reads (MySQL, Postgres, MariaDB).
- **RDS Proxy** improves connection management & failover time by providing fully managed pooling service.
- **Custom RDS** lets you bring your own software configurations (Oracle/SQL Server).

### Nuances & Edge Cases

- **Multi-AZ** means **High availability**
- **Multi-AZ ≠ Read Scaling**. For that, use **Read Replicas**.
- **Backups** are automatic (up to 35 days) and enabled by default.
- Can encrypt at rest using **KMS**, and in transit using **SSL/TLS**.
- Point-in-time restore, manual snapshots supported.

### Exam Pointers

- Use Multi-AZ for HA, Read Replicas for scalability.
- Read Replicas **can be promoted** to standalone DBs.
- Automated failover in Multi-AZ does not cause data loss.
- RDS **does not auto-scale compute** (Aurora does).

### General Explanation

- RDS simplifies relational DB setup with built-in HA, backups, and security.
- You manage schema/data, AWS manages infra and engine patching.

## Amazon Aurora (MySQL/PostgreSQL-compatible)

### Memory Hook

- "Aurora = RDS on steroids."
- "Distributed, durable, auto-healing storage + MySQL compatibility."

### Must-Know Core Concepts

- **Fully managed**, cloud-native database engine by AWS.
- Compatible with **MySQL and PostgreSQL**.
- **Decoupled compute & storage** (auto scales storage up to 128 TiB).
- **Aurora Replicas**: Up to 15 low-latency replicas for read scaling.
- **Backtrack**: Rewind DB to previous state (up to 72 hrs).
- **Aurora Global Databases**: 1 primary + up to 5 secondary regions.
- **Aurora Serverless** (v1/v2): Auto-scales capacity based on load.
- **Custom endpoints**: Route read traffic to selected replicas.
- Supports **IAM authentication** & **KMS encryption**.

### Nuances & Edge Cases

- **Global DB failover** is ~1 minute (for disaster recovery).
- **Aurora replicas ≠ RDS read replicas** – they share storage layer.
- Aurora Serverless v2 supports fine-grained scaling + VPC integration.
- Serverless v1 has cold start latency.
- Cannot use traditional instance storage resizing (it's auto-managed).

### Exam Pointers

- Aurora offers **5x throughput** of MySQL on RDS.
- Aurora **shares storage volume** across replicas — faster replication.
- Use **Global DB** for low-latency global reads + DR.
- Use **Backtrack** for non-destructive rewinds (MySQL only).
- Choose Serverless for **variable workloads or dev/test**.

### General Explanation

- Aurora is designed for high throughput and distributed resilience.
- Ideal for cloud-native apps requiring consistent performance.

## Aurora Advanced Features

### Memory Hook

- "Global, granular, serverless, smart endpoints."

### Must-Know Core Concepts

- **Global DB**: Replicates to up to 5 secondary regions.
- **Custom Reader Endpoints**: Target specific replica sets.
- **Aurora ML**: Call SageMaker/Comprehend directly from SQL.
- **I/O-Optimized Aurora**: Pay only for compute, no IOPS charge.

### Nuances & Edge Cases

- Aurora ML supports **in-database inference**, not training.
- **Aurora Global DB** is ideal for multi-region SaaS apps.
- You can have **read-only** workloads at secondary regions.
- **I/O-Optimized** config is cost-effective for heavy workloads.

### Exam Pointers

- If you see **multi-region, low-latency read** in scenario → **Aurora Global**.
- If app does **ML inference from DB** → **Aurora ML**.
- Choose I/O-Optimized when you want **flat pricing**.

## Amazon ElastiCache (Redis & Memcached)

### Memory Hook

- "ElastiCache = Fast lane for your reads."
- "Redis = Smart cache with persistence, Memcached = Lightweight speed."

### Must-Know Core Concepts

- **In-memory cache** layer for read-heavy apps.
- Supports **Redis** and **Memcached** engines.
- Redis: Multi-AZ, backup & restore, persistence, pub/sub, streams.
- Memcached: Simple, multi-threaded, no persistence.
- ElastiCache is **regional**, supports **encryption in transit + at rest**.
- Integrates with **RDS, Aurora, DynamoDB** for caching query results.

### Nuances & Edge Cases

- Redis supports **replication + automatic failover**.
- Memcached is **simpler** but doesn’t support replication or persistence.
- Supports IAM policies, Redis AUTH, TLS.
- Scaling can be done via **replication or sharding** (Redis clusters).

### Exam Pointers

- Use Redis for **complex caching, pub/sub**, or **failover support**.
- Use Memcached when you need **simple, volatile cache** with horizontal scaling.
- If you see **low-latency reads + write-heavy DB**, use **Redis as write-through cache**.

### General Explanation

- ElastiCache accelerates app performance by reducing load on primary DBs.
- Redis is more powerful, while Memcached is simpler and faster to use.

## Additional Concepts & Features

### Read Replicas vs Multi-AZ (RDS)

- **Read Replicas**: Improve read performance, can be promoted.
- **Multi-AZ**: HA for writes, synchronous standby, not for read scaling.

### RDS Proxy

- Connection pooling for apps with thousands of DB connections.
- Improves failover time & performance.
- Useful for Lambda or microservices apps.

### RDS Snapshot Cloning & Restore

- Clone from snapshots for dev/test environments.
- Fast, cost-effective way to duplicate DBs.

### RDS Custom

- Custom OS-level configurations for Oracle/SQL Server.
- Bring-your-own licensing model (BYOL).

## Quiz Note Highlights

- Aurora = Shared distributed storage.
- RDS = Each replica has own EBS.
- Aurora scales storage automatically.
- IOPS billing only in RDS, Aurora I/O-Optimized skips it.
- Read Replicas ≠ Multi-AZ — serves different use cases.
- Backtrack ≠ Point-in-time restore — it's near-instant rewind.
