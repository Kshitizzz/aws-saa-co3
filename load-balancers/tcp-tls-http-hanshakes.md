# Flow of TCP, TLS and HTTP Handsahkes

## Memory Hook

-"TCP connects, TLS protects, HTTP communicates."
- Or:
- “TTT → TCP first, TLS second, then Talk (HTTP).”

## flow - tcp Handshake -> tls handshake -> http handshake

- Let’s say your browser goes to https://app.example.com:
- TCP Handshake happens to establish connection.
- TLS Handshake occurs to securely exchange keys and verify identity (app.example.com via SNI).
- HTTPS Request is made, now encrypted with the shared keys.

## Nuances & Edge Cases

- You must have TCP before TLS. No TLS without an underlying transport.
- HTTP can run over plain TCP (i.e., no encryption). That’s just http://.
- HTTPS = HTTP over TLS over TCP.
- TLS handshake must complete before any HTTP headers or data is seen or decrypted.
- Some exam scenarios ask about latency — remember, TLS adds extra round-trips because of its handshake.

