# Security Group



## How to create Security Group?

A security group controls the traffic that is allowed to reach and leave the resources that it is associated with. For example, after you associate a security group with an EC2 instance, it controls the inbound and outbound traffic for the instance.

When you create a VPC, it comes with a default security group. You can create additional security groups for each VPC. You can associate a security group only with resources in the VPC for which it is created.

For each security group, you add rules that control the traffic based on protocols and port numbers. There are separate sets of rules for inbound traffic and outbound traffic.

## Security group basics

## Characteristics of security groups

- When you create a security group, you must provide it with a name and a description. The following rules apply:

- A security group name must be unique within the VPC.

- Names and descriptions can be up to 255 characters in length.

- Names and descriptions are limited to the following characters: a-z, A-Z, 0-9, spaces, and ._-:/()#,@[]+=&;{}!$*.

- When the name contains trailing spaces, we trim the space at the end of the name. For example, if you enter "Test Security Group " for the name, we store it as "Test Security Group".

- A security group name cannot start with sg-.

- Security groups are stateful. For example, if you send a request from an instance, the response traffic for that request is allowed to reach the instance regardless of the inbound security group rules. Responses to allowed inbound traffic are allowed to leave the instance, regardless of the outbound rules.

- There are quotas on the number of security groups that you can create per VPC, the number of rules that you can add to each security group, and the number of security groups that you can associate with a network interface. For more information

## Characteristics of security group rules

- You can specify allow rules, but not deny rules.

- When you first create a security group, it has no inbound rules. Therefore, no inbound traffic is allowed until you add inbound rules to the security group.

- When you first create a security group, it has an outbound rule that allows all outbound traffic from the resource. You can remove the rule and add outbound rules that allow specific outbound traffic only. If your security group has no outbound rules, no outbound traffic is allowed.

- When you associate multiple security groups with a resource, the rules from each security group are aggregated to form a single set of rules that are used to determine whether to allow access.

- When you add, update, or remove rules, your changes are automatically applied to all resources associated with the security group. The effect of some rule changes can depend on how the traffic is tracked. For more information, see Connection tracking in the Amazon EC2 User Guide for Linux Instances.

- When you create a security group rule, AWS assigns a unique ID to the rule. You can use the ID of a rule when you use the API or CLI to modify or delete the rule.

## Best practices

- Authorize only specific IAM principals to create and modify security groups.

- Create the minimum number of security groups that you need, to decrease the risk of error. Use each security group to manage access to resources that have similar functions and security requirements.

- When you add inbound rules for ports 22 (SSH) or 3389 (RDP) so that you can access your EC2 instances, authorize only specific IP address ranges. If you specify 0.0.0.0/0 (IPv4) and ::/ (IPv6), this enables anyone to access your instances from any IP address using the specified protocol.

- Do not open large port ranges. Ensure that access through each port is restricted to the sources or destinations that require it.

- Consider creating network ACLs with rules similar to your security groups, to add an additional layer of security to your VPC.

## Default security groups for your VPCs

Your default VPCs and any VPCs that you create come with a default security group. With some resources, if you don't associate a security group when you create the resource, we associate the default security group. For example, if you do not specify a security group when you launch an EC2 instance, we associate the default security group.

You can change the rules for a default security group. You can't delete a default security group. If you try to delete the default security group, you get the following error: Client.CannotDelete.

The following table describes the default rules for a default security group.

| Inbound ||| |
|--- |--- |--- |--- |
| Source |Protocol  |Port range	 |Description |
|     The security group ID (its own resource ID)   |  All       |   All         |   Allows inbound traffic from resources that are assigned to the same security group.       |
| Outbound | | | 
| Destination |Protocol |Port range |Description |
|  0.0.0.0/0   |    All    |    All      |     Allows all outbound IPv4 traffic.     |
|   ::/0 |  All  | All   | Allows all outbound IPv6 traffic. This rule is added only if your VPC has an associated IPv6 CIDR block.   |

## Security group rules

- The rules of a security group control the inbound traffic that's allowed to reach the resources that are associated with the security group. The rules also control the outbound traffic that's allowed to leave them.

- You can add or remove rules for a security group (also referred to as authorizing or revoking inbound or outbound access). A rule applies either to inbound traffic (ingress) or outbound traffic (egress). You can grant access to a specific CIDR range, or to another security group in your VPC or in a peer VPC (requires a VPC peering connection).

```
Warning
When you add rules for ports 22 (SSH) or 3389 (RDP) so that you can access your EC2 instances, we recommend that you authorize only specific IP address ranges. If you specify 0.0.0.0/0 (IPv4) and ::/ (IPv6), this enables anyone to access your instances from any IP address using the specified protocol.
```

For each rule, you specify the following:

- Protocol: The protocol to allow. The most common protocols are 6 (TCP), 17 (UDP), and 1 (ICMP).

- Port range: For TCP, UDP, or a custom protocol, the range of ports to allow. You can specify a single port number (for example, 22), or range of port numbers (for example, 7000-8000).

- ICMP type and code: For ICMP, the ICMP type and code. For example, use type 8 for ICMP Echo Request or type 128 for ICMPv6 Echo Request.

- Source or destination: The source (inbound rules) or destination (outbound rules) for the traffic to allow. Specify one of the following:

- A single IPv4 address. You must use the /32 prefix length. For example, 203.0.113.1/32.

- A single IPv6 address. You must use the /128 prefix length. For example, 2001:db8:1234:1a00::123/128.

- A range of IPv4 addresses, in CIDR block notation. For example, 203.0.113.0/24.

- A range of IPv6 addresses, in CIDR block notation. For example, 2001:db8:1234:1a00::/64.

- The ID of a prefix list. For example, pl-1234abc1234abc123. For more information, see Group CIDR blocks using managed prefix lists.

- The ID of a security group.
```
## Note

The ID of the security group can be the ID of another security group in the same VPC or a security group for a peered VPC (if the VPC is peered with another VPC).

For outbound rules, this means that EC2 instances associated with the current security group can send outbound traffic to the private IP address of EC2 instances associated with the specified security group. For inbound rules, this means that EC2 instances associated with the current security group can receive inbound traffic from the private IP address of EC2 instances associated with the specified security group.

If you add a security group as source or destination, no rules from the specified security group are added to the current security group.

If you configure routes to forward the traffic between two instances in different subnets through a middlebox appliance, you must ensure that the security groups for both instances allow traffic to flow between the instances. The security group for each instance must reference the private IP address of the other instance or the CIDR range of the subnet that contains the other instance as the source. If you reference the security group of the other instance as the source, this does not allow traffic to flow between the instances.
```


