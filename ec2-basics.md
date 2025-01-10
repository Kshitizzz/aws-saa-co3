1.2.5. Elastic Compute Cloud (EC2)
Default compute service. Provides access to virtual machines called instances.

1.2.5.1. Infrastructure as as Service (IaaS)
	1. The unit of consumption is an instance. 
	2. An EC2 instance is configured to launch into a single VPC subnet. 
	3. Private service by default, public access must be configured. 
	4. The VPC needs to support public access. 
	5. If you use a custom VPC then you must handle the networking on your own.

EC2 deploys into one AZ. If it fails, the instance fails. -- AZ resilient

Different sizes and capabilities. All use On-Demand Billing - Per second. Only pay for what you consume.

Local on-host storage or Elastic Block Storage

Pricing based on:

	CPU
	Memory
	Storage
	Networking
	Extra cost for any commercial software the instance deploys with.

1.2.5.2. Running State
	Charged for all four categories.
	
		Running on a physical host using CPU.
		Using memory even with no processing.
		OS and its data are stored on disk, which is allocated to you.
		Networking is always ready to transfer information.

1.2.5.3. Stopped State
	Charged for EBS storage only.

		No CPU resources are being consumed
		No memory is being used
		Networking is not running
		Storage is allocated to the instance for the OS together with any applications.
		
1.2.5.4. Terminated State
	No charges, deletes the disk and prevents all future charges.

1.2.5.5. AMI (Server Image) (Amazon Machine Image)
AMI can be used to create an instance or can be created from an instance. 
AMIs in one region are not available from other regions.

Contains:

	Permissions: controls which accounts can and can't use the AMI.
	
		Public - Anyone can launch it.
		
		Owner - Implicit allow, only the owner can use it to spin up new instances
		
		Explicit - Owner grants access to AMI for specific AWS accounts

Root Volume: contains the Boot Volume

Block Device Mapping: links the volumes that the AMI has and how they're presented to the operating system. Determines which volume is a boot volume and which volume is a data volume.

1.2.5.6. Connecting to EC2
	AMI Types:
	
		Amazon Quick Start AMIs
		
		AWS Marketplace AMIs
		
		Community AMIs
		
		Private AMIs

	Windows using RDP (Remote Desktop Protocol), Port 3389
	
	Linux SSH protocol, Port 22
	
	Login to the instance using an SSH key pair. 
	Private Key - Stored on local machine to initiate connection. 
	Public Key - AWS places this key on the instance.

![image](https://github.com/user-attachments/assets/ba9b0dee-98ea-45a9-91d6-ca44e522c639)
