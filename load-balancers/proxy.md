# Topic: Proxies in AWS Load Balancer Context

## Memory Hook

- “Proxy = Middleman. Reverse proxies serve your app. Transparent proxies serve your firewall.”
- “If it decrypts, it proxies. If it passes through, it’s transparent.”

## ✅ What Is a Proxy?

- A proxy is a network component that sits between a client and a server.
- It intercepts traffic, and may inspect, modify, or forward it.
- It can terminate TLS, route requests, or pass traffic transparently.

## Types of Proxies Relevant to AWS

- Forward Proxy:
- Sits in front of the client.
- Typically used for outbound access control, logging, caching.
- Not used in AWS Load Balancers.

- Reverse Proxy:
- Sits in front of the server.
- Handles inbound client traffic, routes to backend.
- Used by ALB and Gateway Load Balancer.

- Transparent Proxy:
- Intercepts traffic without the client’s awareness.
- Used in GWLB to send traffic to firewalls or inspection appliances.

- TLS Terminating Proxy:
- Decrypts TLS/HTTPS traffic at the edge.
- Used in ALB and NLB (with TLS termination).

## How AWS Load Balancers Behave as Proxies

- Application Load Balancer (ALB):
- Acts as a full reverse proxy.
- Terminates TLS, parses HTTP headers, rewrites paths.
- Supports advanced routing, WAF, cookie-based stickiness.

- Network Load Balancer (NLB):
- Acts as a transparent proxy by default.
- Can become a TLS proxy if TLS termination is enabled.
- Preserves client IP and offers IP stickiness (not cookie-based).

- Gateway Load Balancer (GWLB):
- Acts as a transparent L3 proxy.
- Designed for traffic inspection, not app routing.
- Forwards all traffic to third-party appliances (e.g., firewall, IDS).

## Nuances & Edge Cases

- ALB always hides backend IPs — client talks only to the ALB.
- NLB can operate in passthrough mode, preserving full traffic s tructure.
- TLS passthrough = encrypted traffic passed to backend untouched.
- TLS termination = decrypts at the Load Balancer for inspection/routing.
- GWLB doesn't terminate TLS or HTTP — it passes packets to appliances.

## Proxy-Related Feature Requirements

- TLS Termination → Requires a proxy that can decrypt → ALB, NLB (with TLS termination).
- Header-based routing → Requires Layer 7 proxy → ALB only.
- Cookie-based stickiness → Requires proxy to inject cookie → ALB only.
- Client IP preservation → NLB supports this natively (no proxying needed).
- Traffic inspection (e.g., firewalls) → Needs transparent proxy → GWLB.

## Memory Hook

- “Proxy = Middleman. Reverse proxies serve your app. Transparent proxies serve your firewall.”
- “If it decrypts, it proxies. If it passes through, it’s transparent.”

