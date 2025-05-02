# Auto Scaling Groups (ASG)

## Memory Hook
- “ASG = Always the right number of EC2s. Not too many, not too few.”
- Or
- "Auto Scaling: Your personal ops team that never sleeps."
- asg coupled with load balancers enable **elastic self healing architectures**.

## Must-Know Core Concepts
- **Auto Scaling Group (ASG)**: A service that automatically adjusts the number of EC2 instances in a group based on demand or defined conditions.
- Built on top of **Launch Templates** or **Launch Configurations** which define:
  - AMI ID (OS image)
  - Instance type
  - Key pair
  - Security groups
  - User data (bootstrap scripts)
  - storage type

- Key Parameters:
  - **Min Size**: Minimum number of instances (always running)
  - **Max Size**: Upper limit for scaling
  - **Desired Capacity**: Target number of instances ASG tries to maintain

- **Scaling Triggers**:
  - **Dynamic Scaling**: Reacts to CloudWatch metrics (e.g., CPU > 80%) (CloudWatch means alarms)
  - **Scheduled Scaling**: Based on predictable patterns (e.g., weekends, business hours)
  - **Predictive Scaling** (optional): Uses ML to anticipate demand (limited scenarios)

- **Health Checks**:
  - ASG checks EC2 instance health (via EC2 or ELB health checks).
  - Unhealthy instances are automatically replaced (self-healing). 

- **Integration with Load Balancers**:
  - ALB/NLB distributes traffic to healthy ASG-managed EC2s.
  - ASG handles registration/deregistration from Target Groups automatically. (elastic)

## Nuances & Edge Cases
- If an instance is terminated manually, ASG will **automatically launch a replacement** (to meet desired capacity).
- **Instance Refresh** feature allows rolling updates to all instances (e.g., during AMI change or config update).
- AZ balancing: ASG can span multiple AZs to increase availability. (**important**)
- **Lifecycle hooks** let you pause at instance launch/terminate stages (e.g., to run config scripts or drain connections).
- Launch Templates are preferred over older Launch Configurations — support for newer instance types and features.
- ASGs cannot span multiple regions — they are region-specific. (region specific but cross-AZ)

## Good Metric to scale on? (via CloudWatch)
- CPUUtilization 
- RequestCountPerTarget no. of req per EC2 Instance
- Avg Network in/out if app of EC2 in network bound\
- Any custom metric via CloudWatch

## Cooldown period
- Post a scaling activity (scale in or out based on alarms / trigger), ASG will not add/remove any target instance so as to take the new scaled instances to take effect
- stablises CloudWatch metrics
- default is 300 sec / 5 Min
- Use ready-to-use AMIs to reduce the EC2 bootstrap time and lower the cooldown period
