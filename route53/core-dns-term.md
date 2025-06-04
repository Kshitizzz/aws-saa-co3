# 🌐 DNS Terminology Cheat Sheet

## Memory Hook
- "Think of DNS as a phonebook for the internet — domains = names, IPs = numbers."

---

## ✅ Core DNS Terms

### Root Domain
- The highest level of the DNS hierarchy.
- Represented by a `.` (dot), but usually implied (e.g., `example.com.`).

### TLD (Top-Level Domain)
- The last part of a domain name (e.g., `.com`, `.org`, `.net`, `.io`).
- Managed by **IANA** and TLD registries.

### SLD (Second-Level Domain)
- The name directly left of the TLD (e.g., `example` in `example.com`).
- Registrable portion under a TLD.

### FQDN (Fully Qualified Domain Name)
- A complete domain name that specifies exact location in the DNS hierarchy.
- Ends with a `.` (e.g., `www.example.com.`).
- Includes hostname + domain + TLD + root.

### Name Server (NS)
- Specialized DNS servers that store records for a domain.
- Pointed to by the **Registrar** and queried by resolvers.
- Examples: `ns-123.awsdns-45.com`

### Zone Files
- Text file stored on a Name Server.
- Contains DNS records like `A`, `CNAME`, `MX`, etc.
- Defines how a domain resolves.

### Registrar
- Organization authorized to sell/manage domain registrations (e.g., GoDaddy, Namecheap, Route 53).
- Manages records with the TLD registry.

### DNS Records (Types)
| Record Type | Purpose                                           | Example                     |
|-------------|----------------------------------------------------|-----------------------------|
| `A`         | Maps domain to IPv4 address                        | `example.com -> 192.0.2.1`  |
| `AAAA`      | Maps domain to IPv6 address                        | `example.com -> ::1`        |
| `CNAME`     | Alias to another domain                            | `www.example.com -> example.com` |
| `MX`        | Mail server routing                                | `10 mail.example.com`       |
| `NS`        | Delegates to a name server                         | `ns1.exampledns.com`        |
| `TXT`       | Stores arbitrary text (e.g., SPF, DKIM)            | `"v=spf1 include:..."`      |
| `SRV`       | Defines service-specific records                   | For VoIP, LDAP, etc.        |
| `PTR`       | Reverse DNS lookup (IP to domain)                  | `1.2.0.192.in-addr.arpa`    |

---

## ✅ Summary

- **FQDN** = Fully qualified path in DNS.
- **TLD/SLD** = Hierarchical parts of a domain.
- **Zone File** = Where all DNS record mappings live.
- **Name Server** = Stores zone files.
- **Registrar** = Where you buy/manage domains.

