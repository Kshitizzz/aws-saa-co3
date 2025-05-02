# network-load-balancers

## Memory Hook (Updated)

- "NLB = No Look Balancer: Fast, dumb, direct — and now sticky by IP."
- Breakdown:
- "No Look" → Layer 4 only (TCP/UDP/TLS), no content inspection
- "Fast" → Millions of requests/sec, ultra-low latency
- "Dumb" → Doesn’t make decisions based on URL, headers, etc.
- "Direct" → Preserves source IP, supports Elastic IPs, passthrough traffic
- "Sticky by IP" → Supports IP-based stickiness (TCP/TLS only, 1–3600 sec, no cookies)
- “No cookies, just IP — that’s how NLB sticks to thee.”
- nlb support all three health checks: tcp, http and https

## facts

- you need: few static IPs for your application
- you need: elastic IP support
- you need: to handle TCP/UDP traffic for your application
- you need: extreme performance
- NLB target groups can be of 
- EC2 instances
- IP addresses
- ALBs too (NLB + ALB chaining allowed)
- NLB health checks support TCP, HTTP & HTTPS protocols
- Static IP support:
- One per AZ — NLB provides static IPs by default.
- Can also assign an Elastic IP (EIP) per subnet (this is exam-tested often)
- cross zone load balancing is supported, one AZ fails, send to health targets in other AZ

## edge cases

- preservers SOURCE IP unlike ALBs
- TLS passthrough (forward encrypted traffic as is) supported
- TLS termination (decrypt traffic and forward plain text) also supported
- No sticky sessions / session affinity / cookies supported
- Security groups are not supported, access must be managed by TARGET SGs and VPC network ACLs
- CROSS ZONE LOAD BALANCING is turned OFF by default UNLIKE ALB