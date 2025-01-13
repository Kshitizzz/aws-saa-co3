# load balancers?

## what?

- load balancers are servers that forward incoming traffic to multiple downstream servers
- fully managed service by AWS
- means load balancer would be operational always, as guaranteed by AWS
- instances could be of EC2, ECS containers etc
- 4 types of LBs offered by AWS
- 1. CLB (classic): deperecated now
- 2. ALB (application): http, https, websockets
- 3. NLB (network): tcp, tls, udp
- 4. GWLB (gateaway): operates at layer-3 network, IP protocol
- health checks allows load balancers to determine if a downstream server is up and running (has not failed)
- done routinely on usually /health endpoint
- if server replies with 200 (OK) response, then only LB sends traffic to it
