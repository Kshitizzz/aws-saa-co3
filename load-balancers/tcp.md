
### 📘 **Topic: TCP-Based Protocols**

---

### ✅ **What is TCP?**

TCP (Transmission Control Protocol) is a **connection-oriented** protocol at **Layer 4 (Transport Layer)** of the OSI model. It ensures:

- **Reliable** delivery (resends if packets are lost)
- **Ordered** data (delivers in correct sequence)
- **Error-checked** communication

---

### ✅ **Common Protocols That Use TCP**

Here are the **most common TCP-based protocols**, grouped by function:

#### 🌐 **Web & APIs**
- **HTTP** (Port 80)  
- **HTTPS** (Port 443, which is HTTP over TLS)  
- **WebSockets (WS/WSS)** – rides over HTTP/S  
- **REST APIs / GraphQL APIs** – typically use HTTP/S  
- **gRPC** – typically uses HTTP/2 over TLS

#### 📧 **Email**
- **SMTP** (Port 25, 587 with TLS) – sending email  
- **POP3** (Port 110) – downloading email  
- **IMAP** (Port 143, or 993 for TLS) – email sync

#### 🖧 **Remote Access & Admin**
- **SSH** (Port 22)  
- **Telnet** (Port 23 – outdated/insecure)  
- **FTP** (Port 21)  
- **SFTP** (Port 22 – runs over SSH)

#### 🗄️ **File Sharing / Storage**
- **SMB/CIFS** (Port 445) – Windows file sharing  
- **NFS** (Port 2049) – Network File System

#### 🧠 **Database & Caching**
- **MySQL / MariaDB** (Port 3306)  
- **PostgreSQL** (Port 5432)  
- **MongoDB** (Port 27017)  
- **Redis (in some configs)** – can use TCP (Port 6379)  
- **Elasticsearch** – TCP with RESTful API (Port 9200)

#### 📡 **Directory / Identity / Messaging**
- **LDAP** (Port 389, or 636 with TLS)  
- **Kerberos** (Port 88)  
- **MQTT** (Port 1883 or 8883 for secure TLS)

#### 📦 **Other Common TCP Services**
- **DNS over TCP** (Port 53 – used for large queries or zone transfers)  
- **RDP** (Remote Desktop Protocol – Port 3389)  
- **VPNs** (like OpenVPN – can use TCP or UDP)

---

### ⚠️ **Edge Case: Not Everything Uses TCP**

Many real-time or streaming protocols use **UDP** instead of TCP:
- **DNS** (usually UDP unless fallback)  
- **VoIP, SIP, RTP**  
- **Video streaming (QUIC, RTSP)**  
- **Game networking**

> 🔒 **TLS requires TCP**, so any TLS-encrypted connection (HTTPS, SMTPS, IMAPS, etc.) inherently uses TCP.

---

### 🧠 Memory Hook

> **“If it needs guaranteed delivery, it's probably TCP.”**  
> Think **bank transactions, login sessions, file transfers** — these must not fail quietly.

---

### 📘 Exam Tie-Ins (SAA-C03)  

- **NLB** can be used for **TCP or TLS** traffic  
- **ALB** is designed for **HTTP/HTTPS (Layer 7)** only  
- TLS termination or passthrough only works on **TCP**, not **UDP**
