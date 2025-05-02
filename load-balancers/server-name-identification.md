# Server Name Indication (SNI) - extension of the TLS protocol

## Memory Hook
- “SNI = TLS says ‘Hey server, I want example.com — give me the right cert.’”
- Think of SNI as a “name tag” the client shows during the TLS handshake so the server knows which certificate to respond with.

## Must-Know Core Concepts

- SNI (Server Name Indication) is an extension to the TLS protocol.
- It allows a client (like a browser) to specify which hostname it’s trying to reach during the TLS handshake, before the encrypted connection is fully established.
- This allows multiple TLS/HTTPS websites to be hosted on a single IP address (just like virtual hosts for HTTP).
- Without SNI, the server wouldn’t know which certificate to present during handshake if multiple domains share the same listener.
- In AWS:
- ALB supports SNI — you can associate multiple HTTPS listeners and SSL certificates (via ACM) with the same ALB.
- ALB chooses the right certificate based on SNI in the TLS Client Hello.
- This enables multi-tenant applications or host-based routing over HTTPS.

## Nuances & Edge Cases
- NLB only supports 1 certificate per listener by default, unless you use TLS listener + SNI (which is a newer feature).
- Some older clients (pre-2010) don’t support SNI — in those cases, AWS defaults to the “default” certificate associated with the listener.
- SNI happens before the application protocol is even negotiated — it’s part of the TLS handshake, so you can’t route based on headers, cookies, or paths at that stage.
- You cannot use SNI with TCP listeners — it only applies to TLS/HTTPS, because it's a TLS-layer concept, not a TCP-layer one.

