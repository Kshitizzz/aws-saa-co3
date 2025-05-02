# Why SNI doesnt work with TCP?

##  Memory Hook
- "TCP is blind — it moves packets. TLS is smart — it negotiates names and certs."
- Or: “SNI rides on TLS, not on plain TCP.”

## facts

- SNI only works if the protocol is TLS (i.e., HTTPS, or any TLS-encrypted service). It does NOT work with plain TCP listeners.
- TCP is a transport protocol — it's low-level and doesn't know about domains, certificates, or encryption.
- A TCP connection simply **establishes a byte stream between two endpoints** — it has no notion of “hostname” or SSL handshakes.
- Therefore, with just TCP, the server has no way to know which certificate to present, because no SNI field exists.
- ALB supports multiple HTTPS certificates via SNI — used for multi-domain HTTPS routing.
- NLB supports multiple TLS certs only if you use a TLS listener with SNI. If you use TCP, it supports only one target and one cert — no SNI support.
- If a question says "TCP listener", eliminate answers involving SNI/multiple certificates.