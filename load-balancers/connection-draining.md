# Connection Draining (a.k.a. Deregistration Delay in AWS)

## Memory Hook
- "Deregistration delay = Graceful goodbye. No rage quitting the load balancer."
- Or
- “Drain before you kill.”

## Must-Know Core Concepts
- Connection Draining ensures that when a target (EC2, container, etc.) is removed from a load balancer, it is not killed abruptly while still serving live requests.
- Instead, it is marked as “draining” — allowing in-flight requests to complete before termination or deregistration.
- In AWS, this feature is known as “Deregistration Delay”.
- Default timeout:
- 300 seconds (5 minutes) on ALB, NLB, CLB — can be configured from 0 to 3600 seconds.
- Applies to:
- ALB, NLB, and Classic ELB
- Works during:
- EC2 instance termination
- Auto Scaling scale-in
- Manual deregistration from a target group
- Rolling deployments / Blue-Green switches

## Nuances & Edge Cases
- New connections are not sent to a draining instance, but old connections are allowed to finish.
- If the timeout expires and connections are still running, they will be forcefully closed.
- In NLB, since it supports long-lived TCP connections, connection draining is critical — abrupt removal can drop a persistent session.
- In Lambda target groups, connection draining does not apply, since invocations are stateless and short-lived.

## Memory Hook
- "Deregistration delay = Graceful goodbye. No rage quitting the load balancer."
- Or
- “Drain before you kill.”