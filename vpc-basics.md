	Ø VPC is a service used to create private networks(virtual) inside of AWS infrastructure
	Ø A VPC is within 1 account and 1 region
	Ø Private and isolated unless you decide otherwise
	Ø Isolated in the sense that services in one private VPC cant communicate with services in an another private VPC unless explicitally configured to do so
	Ø Two types of VPC:
		○ Default VPC
			§ One per region -- can be deleted and recreated
			§ Default VPC CIDR is always == 172.31.0.0/16
			§ Smaller /20 subnet is created in each AZ in a region (by default)
			§ 16 x /20 subnets can fit into 1 /16 VPC, hence covering 16 AZ in a region
			§ This can be configured depending on the number of AZ in a region
			§ VPC connect with the public internet using IGW (Internet GateWay)
			§ Subnets assign public IPV4 addresses
		○ Custom VPCs
	Ø There can be only one default VPC per region -- IMPORTANT
	Ø There can be multiple custom VPCs in a region
	Ø Custom VPCs are private by default
	Ø  VPCs are regionally resilient 
	Ø VPC CIDR is the range of IP addresses in a VPC
	
	
![image](https://github.com/user-attachments/assets/2c786f89-c3bd-455e-91f4-81684a8df603)
