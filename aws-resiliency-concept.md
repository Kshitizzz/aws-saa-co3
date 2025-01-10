How to define Resilience of AWS Services:
- Globally resilient: 
  ○ No concept of region in globally resilient services
  ○ E.g. IAM and Route 53
  ○ If a region fails, services can still continue to operate in some other region
  ○ IAM or Route 53. No way for them to go down. Data is replicated throughout multiple regions
  
  From <https://github.com/alozano-77/AWS-SAA-C02-Course> 
  
  
- Region resilient:
  ○ Services are isolated among regions
  ○ Services are replicated on multiple Azs in a region
  ○ Such that if one AZ fails, the service can still continue to operate on another AZ in that region
  ○ Operate as separate services in each region. Generally replicate data to multiple AZs in that region.
  
  From <https://github.com/alozano-77/AWS-SAA-C02-Course> 
  
  
- AZ resilient:
  ○ Services run from single AZ
  ○ If that AZ fails, that service fails
  ○ It is possible for hardware to fail in an AZ and the service to keep running because of redundant equipment, but should not be relied on.
  
  From <https://github.com/alozano-77/AWS-SAA-C02-Course> 
