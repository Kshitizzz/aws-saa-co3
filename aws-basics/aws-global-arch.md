# AWS Global Architecture: Regions, AZs, and Edge Locations

## Memory Hook
- “Region = Where your app lives”
- “AZ = Physical redundancy”
- “Edge = Gateway to your users”

---

## ✅ Must-Know Core Concepts

### 🌎 Global Infrastructure Components

| Concept               | Description                                                                |
|------------------------|-----------------------------------------------------------------------------|
| **Region**             | A geographic location (e.g., `us-east-1`, `ap-south-1`)                    |
| **Availability Zone (AZ)** | One or more physically isolated DCs within a region — connected via low-latency links |
| **Local Zone**         | Infrastructure placed closer to users in large cities (subset of region)   |
| **Wavelength Zone**    | For ultra-low latency 5G apps (used with Telco infra)                      |
| **Edge Location**      | Global network entry point used by CloudFront, Route 53, Global Accelerator |

---

### 🌐 Region

- Isolated from other regions
- You choose region for:
  - Data residency
  - Latency
  - Regulatory requirements
- Services may be **Regional, Global, or Zonal**

---

### 🏢 Availability Zones (AZs)

- Each AZ = 1+ **data center**
- AZs are **physically separated** (power, networking, HVAC)
- Used for **high availability** and **resilience**
- Multi-AZ deployments protect against **DC failure**

---

### 🌍 Edge Locations

- Over **400+ locations globally**
- Used by:
  - **CloudFront** (cache + TLS termination)
  - **Global Accelerator** (TCP/UDP routing)
  - **Route 53** (DNS resolution)
- Used to reduce **latency** and absorb **DDoS attacks**

---

## 🔄 Global vs Regional vs Zonal Services

| Scope        | Examples                                        |
|--------------|--------------------------------------------------|
| **Global**   | IAM, Route 53, CloudFront, ACM Public Certs     |
| **Regional** | EC2, S3, Lambda, RDS, DynamoDB                  |
| **Zonal**    | EBS, EC2 instances (unless Multi-AZ), ENI       |

🧠 *Global services span all regions. Regional services are isolated per region. Zonal services exist in 1 AZ.*

---

## 📌 Exam Pointers

- “Service runs across the globe with one config?” → ✅ Global (like IAM, Route 53)
- “Service must be designed for HA?” → ✅ Use **Multi-AZ** (across AZs in one region)
- “Why choose region X?” → ✅ Data residency, latency, legal constraints
- “Where is CloudFront content served from?” → ✅ Edge locations
