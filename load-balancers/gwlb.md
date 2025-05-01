# gateway load balancers

## memory tip

- “GWLB = Gateway + GENEVE + Glue for Appliances”
- Gateway → L3 routing, like a NAT
- GENEVE → Tunnels packets without altering them
- Glue → Centralizes 3rd-party appliances into your architecture

## facts

- operates at L3 like NAT
- can be accessed via GWLBe (gateway load balancer endpoint) in a VPC
- no content based routing, only IP packet level inspection
- GWLBe endpoints are zonal, must be deployed in every AZ
- GENEVE protocol on Port 6081
- Target groups for GWLB consist of EC2 instances running network appliances (e.g., Palo Alto, Fortinet, custom packet inspection apps).
- Security Group rules don’t apply directly to the GWLB or its endpoints — unlike ALB/NLB. You control traffic at the appliance level or VPC route tables.

## usecase

- when you wanna route traffic to a security appliance
- security appliance such as firewall, trafic analyzers etc
