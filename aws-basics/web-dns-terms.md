# 🌐 Web & DNS Terminology Mapping

## Memory Hook

- "Think of domains as names, hosts as machines, and URLs as directions."
- "URL = Full address, Host = Server, Domain = ID tag, IP = Actual address"

---

## ✅ Core Terminology & Mappings

| Term                | What it Refers To                                                                 |
|---------------------|-----------------------------------------------------------------------------------|
| **Domain Name**     | Human-readable name mapped to IPs via DNS (e.g., `example.com`)                  |
| **Host**            | Physical or virtual machine (EC2, on-prem, etc.) hosting a service                |
| **Hostname**        | Specific label assigned to a host (e.g., `api.example.com`)                       |
| **Host IP**         | IP address assigned to a host (e.g., `34.212.10.8`)                               |
| **URL**             | Full address to a resource (e.g., `https://example.com/app?query=123`)            |
| **Host URL Endpoint**| API or service endpoint exposed on a host (e.g., `/users`, `/orders`)           |
| **Host Domain**     | Domain associated with a host (e.g., in `app.myco.com`, the domain is `myco.com`)|
| **Application Server**| Runs business logic/backend services (e.g., Flask, Spring Boot on EC2)         |
| **Web Server**      | Serves static content or proxies traffic (e.g., NGINX, Apache)                    |
| **DB Server**       | Stores structured or NoSQL data (e.g., MySQL, DynamoDB)                           |

---

## ✅ Quick Examples

- `https://api.example.com/orders`  
  - **Protocol**: `https`  
  - **Hostname**: `api.example.com`  
  - **Path**: `/orders`  
  - **Type**: Host URL Endpoint

- `34.221.1.5`  
  - **Type**: Host IP  
  - **Maps To**: EC2 instance or Load Balancer

---

## ✅ Summary

- **Domain Name** = Identifier
- **Host/IP** = Machine + Address
- **URL/Endpoint** = Specific resource location
- **Server types** = App (logic), Web (content), DB (storage)

