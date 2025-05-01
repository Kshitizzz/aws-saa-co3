# elastic IP

## facts

- STATIC public IPV4 address from AWS
- does not change when system restarts
- usecase is when you dont want the IP to change, eg: firewall whitelisting
- EIPs are regional and can't be used across regions — common trap in Global Accelerator vs NLB questions