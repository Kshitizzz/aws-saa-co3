# TLS

## facts

- encryption-in-transit
- secures data between server and clients over the internet
- cryptographic protocol

## TLS termination

- decrypt traffic at the LB level and then send to target
- offload decryption work from target to load balancer
- eg: client -> HTTPS -> ALB/NLB (terminate TLS) -> HTTP - EC2
- certificate must be attached via ACM to emply termination of TLS at the load balancer

## Exam Hook

- If you want to decrypt once and inspect, use TLS termination at ALB/NLB. If app must see raw encrypted traffic, use TLS passthrough
- TLS passthrough (forward encrypted traffic as is) supported
- TLS termination (decrypt traffic and forward plain text) also supported
- use TLS passthrough if end-to-end encryption is mandated

## mental orgasm

- So Why TLS When You Already Have HTTP & TCP?
- TCP moves data, but it doesn’t secure it
- HTTP defines the structure of the data but is insecure
- TLS is what secures data in transit — not HTTP or TCP
- You can use TLS with any TCP-based protocol — not just HTTP
- (That’s why NLB supports “TLS listeners” even when not using HTTP)

## SSL (Secure Sockets Layer)

- Predecessor of TLS — now deprecated
- Used to encrypt communications between client/server (e.g., browser to web server)
- Replaced by TLS due to vulnerabilities
- When people say “SSL certificate”, they almost always mean TLS certificate now
- **Exam Hook:** AWS services use TLS, not SSL. "SSL" is used colloquially but TLS is what actually runs