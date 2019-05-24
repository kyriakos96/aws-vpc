# 2. Securing Your VPC

## The Big Picture
![VPC Security Diagram](vpc_security.png?raw=true "VPC Security")

## Security Groups
A security group acts as a **virtual firewall** for your instance to control inbound and outbound traffic. When you launch an instance in a VPC, you can assign up to five security groups to the instance. **Security groups act at the instance level, not the subnet level**. Therefore, each instance in a subnet in your VPC could be assigned to a different set of security groups. If you don't specify a particular group at launch time, the instance is automatically assigned to the default security group for the VPC.

For each security group, you add rules that control the inbound traffic to instances, and a separate set of rules that control the outbound traffic. This section describes the basic things you need to know about security groups for your VPC and their rules.

#### Security Group Basics
The following are the basic characteristics of security groups for your VPC:

1. You have limits on the number of security groups that you can create per VPC, the number of rules that you can add to each security group, and the number of security groups you can associate with a network interface. For more information, [see Amazon VPC Limits](https://docs.aws.amazon.com/vpc/latest/userguide/amazon-vpc-limits.html).

1. You can specify allow rules, but not deny rules.

1. You can specify separate rules for inbound and outbound traffic.

1. When you create a security group, it has no inbound rules. Therefore, no inbound traffic originating from another host to your instance is allowed until you add inbound rules to the security group.

1. By default, a security group includes an outbound rule that allows all outbound traffic. You can remove the rule and add outbound rules that allow specific outbound traffic only. If your security group has no outbound rules, no outbound traffic originating from your instance is allowed.

1. Security groups are stateful — if you send a request from your instance, the response traffic for that request is allowed to flow in regardless of inbound security group rules. Responses to allowed inbound traffic are allowed to flow out, regardless of outbound rules.
    **Note:** Some types of traffic are tracked differently to others. For more information, see [Connection Tracking](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-network-security.html#security-group-connection-tracking) in the Amazon EC2 User Guide for Linux Instances.

1. Instances associated with a security group can't talk to each other unless you add rules allowing it (exception: the default security group has these rules by default).

1. Security groups are associated with network interfaces. After you launch an instance, you can change the security groups associated with the instance, which changes the security groups associated with the primary network interface (eth0). You can also change the security groups associated with any other network interface. For more information about network interfaces, see [Elastic Network Interfaces](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-eni.html).

1. When you create a security group, you must provide it with a name and a description. The following rules apply:

  * Names and descriptions can be up to 255 characters in length.
  * Names and descriptions are limited to the following characters: a-z, A-Z, 0-9, spaces, and ._- : / ( )#,@[]+=&;{}!$*.
  * A security group name cannot start with sg-.
  * A security group name must be unique within the VPC.



## Network Access Control Lists (NACL) - Sec Groups for Subnets
A network access control list (ACL) is an optional layer of security for your VPC that acts as a firewall for controlling traffic in and out of one or more subnets.
#### Network ACL Basics
The following are the basic things that you need to know about network ACLs:

1. VPC automatically comes with a modifiable default NACL. By default, it allows all inbound and outbound IPv4 traffic and, if applicable, IPv6 traffic.
1. You can create a custom NACL and associate it with a subnet. By default, each custom NACL denies all inbound and outbound traffic until you add rules.
1. Each subnet in your VPC must be associated with a NACL. If you don't explicitly associate a subnet with a NACL, the subnet is automatically associated with the default NACL.
1. You can associate a NACL with multiple subnets; however, a subnet can be associated with only one NACL at a time. When you associate a NACL with a subnet, the previous association is removed.
1. A NACL contains a numbered list of rules that we evaluate in order, starting with the lowest numbered rule, to determine whether traffic is allowed in or out of any subnet associated with the network ACL. The highest number that you can use for a rule is 32766. We recommend that you start by creating rules in increments (for example, increments of 10 or 100) so that you can insert new rules where you need to later on.
1. A network ACL has separate inbound and outbound rules, and each rule can either allow or deny traffic.
1. NACLs are stateless; responses to allowed inbound traffic are subject to the rules for outbound traffic (and vice versa).

[NEXT...](aws_vpc_load_balancing.md)