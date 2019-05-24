# 5. Connecting Remote Locations with VPNs

**VPN: Virtual Private Network**

### Old Days
VPNs were used mainly for people to be able to connect remotely to the Office through an encrypted and secure tunnel.

![VPN Diagram](vpc_vpn_high.png?raw=true "vpn")

### What we need

We need a way to connect our organization to our infrastructure on AWS.
![VPN Now Diagram](vpc_vpn_now.png?raw=true "vpn now")

### Major pieces of an AWS VPN
* Customer Gateway
* Virtual Private Gateway
* Tunnel -> Connecting Customer Gateway and Virtual Private Gateway

#### Pros
1. IPsec (secure)
1. Reliable
1. Allow Private IPs

#### Cons 
1. High Latency
1. Unreliable throughput

![VPN on AWS Diagram](vpc_vpn_aws.png?raw=true "vpn aws")

### Direct Connect
1. Uber connection to AWS
1. Better throughput
1. Lower Latency
1. Enterprise solution

Direct wire from your infrastructure to AWS. This requires to go through a **Colo Data Center**
![AWS Direct Connect Diagram](vpc_direct_connect.png?raw=true "AWS Direct Connect ")

#### Pros
1. Dedicated Fiber
  Better Network Performance
  Higher throughput
  **Note:** It is not latency the killer of hybrid system but throughput

#### Cons 
1. Not much here
1. Cost might be a con

[NEXT...](aws_vpc_qa.md)