# EC2 Instance Stores

- memory blocks attached physcially with the EC2 instance when its created
- size depends on the ec2 instance type
- useful for random I/O operations and to store ephermal data
- since they are attached to EC2 instances, I/O disk operations are fast
- In case of a EC2 fleet, these can be accessed via ephermal stores
- ephermal stores will have ephermal0, epphermal1, ephermal2 disks
- Usecase:
- store same temporary dataset accross a fleet of ec2 instances (on all instances in the fleet) for reseliency (if 1 ec2 goes does, data is replicated hence process can go on)
- other random I/O operation