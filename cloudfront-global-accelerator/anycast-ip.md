# Anycast IPs

## Memory Hook
- "One IP, many homes — closest wins."
- "Anycast = Same IP, fastest edge, lowest latency."

---

## ✅ Must-Know Core Concepts

- **Anycast** allows the **same IP address to be advertised from multiple locations**.
- Client’s request is routed to the **nearest location** (based on **BGP routing decisions**).
- Used by **AWS Global Accelerator**, **Cloudflare**, **Google DNS**, etc.
- Improves **latency**, **resilience**, and **DDoS absorption**.

---

## 💡 Real-World Example

| User Location | IP Requested | Resolved By Edge In |  
|---------------|---------------|----------------------|  
| Tokyo         | 13.54.22.17   | Tokyo Edge Location  |  
| London        | 13.54.22.17   | London Edge Location |  
| California    | 13.54.22.17   | SF Edge Location     |

Same IP → handled by **closest and healthiest edge**.

---

## 🧠 Exam Pointers

- **Global Accelerator uses Anycast** to provide **static IPs that are globally distributed**.
- “Low latency + same IP for all clients” → ✅ Anycast
- “Avoid DNS TTL delays in failover” → ✅ Use Anycast via Global Accelerator
- If traffic must stay **within AWS backbone**, Anycast ensures that with GA.

---

Let me know if you want a **visual diagram** that shows how Anycast flows differ from DNS-based routing, or if we proceed with VPC networking next.
