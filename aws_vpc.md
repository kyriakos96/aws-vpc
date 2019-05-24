[1. AWS VPCs](aws_vpc.md)
[2. Securing Your VPC](aws_vpc_security.md)
[3. Configuring Load Balancing](aws_vpc_load_balancing.md)
[4. Configuring Routing between VPCs](aws_vpc_peering.md)
[5. Connecting Remote Locations with VPNs](aws_vpc_vpn.md)
[6. Common questions about AWS VPCs](aws_vpc_qa.md)


# 1. AWS VPCs

Amazon Virtual Private Cloud (Amazon VPC) enables you to launch AWS resources into a virtual network that you've defined. This virtual network closely resembles a traditional network that you'd operate in your own data center, with the benefits of using the scalable infrastructure of AWS

## The Default VPC
AWS has a default VPC for every region.
- You cannot change it
- You can delete it. **IF DELETED** it cannot be retrieved. **Do not delete it**

## Major VPC Options

## Building Subnets

## Routing
More specific VPCs take precedence over less specific ones



## *Configuring Internet Access*

### Create Internet Gateway
An internet gateway is a horizontally scaled, redundant, and highly available VPC component that allows communication between instances in your VPC and the internet. It therefore imposes no availability risks or bandwidth constraints on your network traffic.

An internet gateway serves two purposes: to provide a target in your VPC route tables for internet-routable traffic, and to perform network address translation (NAT) for instances that have been assigned public IPv4 addresses.

### Update Route Table
More specific VPCs take precedence over less specific ones. You can set 0.0.0.0/0 to point to the internet gateway on the public subnets Route table and this will direct any non internal VPC calls to the internet.

### Public IPs
You can enable public IP auto assignment on the subnet settings. While public IPs are created easily they can change whenever an ec2 is rebooted. This is where Elastic IPs come into play.

### Elastic IPs
Elastic IPs never change unless explicitly released back to AWS. *Note:* AWS charges Elastic IP when they are not associated to running instances.

### Private Subnets and NAT Instance
We do not want our private subnet to have full-on access to the internet.
This is more suitable for hosts that might need patches from the internet or updates.
1. Spin up a NAT instance
1. It will work as a router
    a. It lives in the public subnet
    b. It directs data from our private subnet instance to the internet
1. Update the Route table to send everything not matching the routes to the Nat instance `0.0.0.0/0 -> NAT Intance`

## VPC So far:
![VPC Diagram](vpc.png?raw=true "VPC")

[NEXT...](aws_vpc_security.md)