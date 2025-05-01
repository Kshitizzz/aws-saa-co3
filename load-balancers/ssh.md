# SSH (Secure Shell)

- Not related to SSL or TLS at all

- A remote access protocol that also encrypts traffic (like windows RDP)

- Used to securely log in to remote servers (Linux/Unix)

- Runs on TCP Port 22

- 🧠 Think of SSH = Remote Terminal, while TLS = Encrypted Communication Layer

- AWS context:
- Use SSH to access EC2 instances (e.g., ssh -i mykey.pem ec2-user@...)
- SSH keys stored in EC2 Key Pairs