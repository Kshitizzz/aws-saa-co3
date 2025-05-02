# SSH & SSH Key Pairs

## Memory Hook
- "It's like a digital handshake — one hand public, one hand private."
- Or
- "Lock (public key) on the door, key (private key) in your pocket."

## Must-Know Core Concepts
- **SSH (Secure Shell):** A secure network protocol for accessing remote machines (like EC2) via command line over an encrypted connection.
- Commonly used to:
  - Log into Linux servers
  - Execute remote commands
  - Transfer files securely (via `scp` or `sftp`)

- **SSH Key Pair:**
  - **Public Key**: Placed on the server (e.g., AWS EC2 instance under `.ssh/authorized_keys`)
  - **Private Key**: Kept securely by the user on their local machine.
  - SSH verifies the private key against the public key to allow access — no password is sent over the network.

- **Key Generation**:
  - Usually done using `ssh-keygen` (on Mac/Linux) or tools like PuTTYgen (on Windows)
  - AWS also lets you create key pairs via Console, CLI, or SDK

- **In AWS EC2**:
  - When launching an instance, you must associate a key pair to allow SSH login.
  - You connect using:  
    `ssh -i /path/to/private-key.pem ec2-user@<Public-IP>`

## Nuances & Edge Cases
- If you lose your private key, you cannot SSH into your instance — you must create a new key pair and manually add the new public key to the instance (e.g., via user-data or EC2 Session Manager workaround).
- **.pem vs .ppk**: `.pem` is used for OpenSSH (Linux/macOS); `.ppk` is for PuTTY on Windows.
- SSH keys are **region-independent** in AWS — but each EC2 launch must reference an existing key pair in that region.
- Public key content is safe to share, but the private key must remain confidential. Never commit it to version control.
