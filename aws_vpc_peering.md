# 4. Configuring Routing between VPCs

### Typical Scenario (BAD)
![VPC Bad Inter-communication Diagram](vpc_bad_intercom.png?raw=true "VPC Bad Inter-communication")

Naively, one would need to connect two VPCs tha live in the same region through the Internet. This would require using elastic IPs and separate internet gateways to make them talk to each other by going through the internet.

### VPC Peering
A VPC peering connection is a networking connection between two VPCs that enables you to route traffic between them using private IPv4 addresses or IPv6 addresses. Instances in either VPC can communicate with each other as if they are within the same network. You can create a VPC peering connection between your own VPCs, or with a VPC in another AWS account. The VPCs can be in different regions (also known as an inter-region VPC peering connection).

![VPC Peering Diagram](vpc_peering.png?raw=true "VPC Peering")

1. 1-to-1 connections
1. Enable communication using private IPs
1. Only works between VPCs in the same region
1. Peering connections are not transitive
  This means that `VPC 1` below cannot use `VPC 2` below to talk to `VPC 3` as a peer. It needs its own direct connection.
  ![VPC Peering non Transitive Diagram](vpc_peering_non_transitive.png?raw=true "VPC Peering non Transitive")
1. Only one peering connection between any two VPCs
1. Do not overlap CIDR blocks
1. Works across AWS accounts
1. Be careful accepting peering requests
1. Each VPC gets a VPC connection object

 ### Technically
 To achieve this you need to setup the route table of the subnets that need to talk to each other and point them to the private IP range of the other one with the **Target** being the `VPC Peering ID`

[NEXT...](aws_vpc_vpn.md)