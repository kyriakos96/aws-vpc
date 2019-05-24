# 6. Common questions about AWS VPCs

#### Q1. What Is the Most Common Mistake People Make with AWS VPCs?
##### A1. Getting the network range (CIDR block) wrong
1. Make sure it's not already in use on your current network(s)
1. Talk to your network team and agree on the ranges
1. Treat VPC network addresses as you would treat your existing network

#### Q2. What Is the Most Misunderstood AWS VPC Concept?
##### A2. Private and Public IPs
1. Instances don't know about public IPs
1. Public IPs are implemented on the Internet Gateway
1. Use Elastic IPs (EIP) for public IP addresses that won't change

#### Q3. Should Multiple Environments (dev, qa, prod) Use a Single VPC?
##### A3. NO

#### Q4. Should I Use Network ACLs or Security Groups?
##### A4. Both!
1. Think `defence in depth`
1. Protect at the **subnet level** with NACLs
1. Protect at the **instance level** with Security Groups
1. Create practices for your security and stick to them
1. Feel free to use additional 3rd party security technologies. i.e. intrusion prevention system, antivirus etc.

#### Q5. How Do I Mitigate Against AWS Outages?
##### A5. Spread service over as much of AWS as possible
1. Spread across Availability Zones (AZ)
1. Spread across Regions
1. Spread across Cloud providers

#### Q6. What Is the Simplest Thing to Do with the Biggest Benefit?
##### A6. Name your AWS stuff

#### Q7. When Should I Use Public Subnets and Private Subnets?
##### A7. Use public subnets sparingly
1. Load Balancers
1. Firewalls
1. Proxy Servers