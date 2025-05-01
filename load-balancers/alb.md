# application-load-balancers

## memory-hook

- “ALB is picky with rules, talks HTTP fluently, and always wants a cookie.”
- Picky with rules: Listener rules by priority
- HTTP fluently: Layer 7 + content routing
- Wants a cookie: Stickiness via application cookie
- DOES NOT SUPPORT ELASTIC IP

## facts

- handle http/https traffic
- especially useful when need to forward traffic to multiple HTTP/S applications, ECS containers, IPs, lambda functions, IPs etc.
- examples
- load balancing to applications across multiple machines is a usecase of target groups
- load balancing to applications across the same machine is a usecase of ECS containers
- feature of having fixed hostname
- routing table capable of forwarding traffic based on URL (hostname, path, http headers, query strings)

## strong usecase

- ALBs are great fit for microservice based architecture and container based apps
- has port mappping feature to redirect to dynamic host in ECS

## comparision with CLB

- would need multiple CLBs per applications if we want forwarding rules like ALB

## ALB target groups

- target groups are basically group of instances for which the load balancing happens for
- multiple ec2 instances can be part of a target group (auto-scaling group supported)
- ecs containers target group
- tg for lambda functions and so on
- IMP: health checks are done at the target group level
- ALBs can route to multple target groups

## X-forwarded-something

- app servers cant directly see the backend client IP
- true IP inserted in the header X-Forwarded-For
- true port: X-Forwarded-Port
- true protocol: X-Forwarded-Proto