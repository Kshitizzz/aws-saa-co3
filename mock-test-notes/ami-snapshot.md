# EC2 AMI Snapshots

- Instance AMIs can be created via the snapshots of the instances
- AMI are regionally available, but can be copied to another region (region B)
- When copied, the underlying snapshot is also copied to another region (region B)
- Hence both AMI + Snapshot are copied
- Same EC2 instance can now be spun up using the AMI of region A 