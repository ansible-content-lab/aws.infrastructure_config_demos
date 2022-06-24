# Peer Existing Network Role

This role attempts to speed up the process of peering newly created VPCs with an existing set of VPCs using direct peering.

## Peering Networks

When using this role, the following actions take place.

1. Direct network peering is established between the new VPC that you created and your existing VPCs that may already have a network configuration.
2. The peerings are automatically accepted.
3. A security group is create to allow traffic into the new VPC from the existing VPCs. You can set the `security.type` extra var to `all`, `ssh`, or `icmp`.

### Variables

The following variables are used during deployment.

| Type Choice                                  | Description                                                                          |
| -------------------------------------------- | ------------------------------------------------------------------------------------ |
| `aws_region`                                 | The region that your VPCs reside in.                                                 |
| `source_vpc.vpc_id`                          | The newly created VPC that you want to pair to other networks.                       |
| `source_vpc.cidr_block`                      | The CIDR block of the new VPC.                                                       |
| `peerings`                                   | The VPC ids of the VPCs that you want to peer to.                                    |
| `security.type`                              | The security model implemented in a new security group created for the peering.      |
| `security.security_group_ingress_cidr_block` | The ingress CIDR block that will be used when creating security group rules.         |
| `security.security_group_engress_cidr_block` | The egress CIDR block that will be used when creating security group rules.          |
| `route_tables`                               | The route tables to update in the new VPC to route traffic to the newly peered VPCs. |

**Note**: Route table updates are only performed in the new VPC.  If you want to route traffic from your existing VPCs to the new VPC, then the route tables for those VPCs must be updated as well.

```yaml
---
aws_region: us-east-1
source_vpc:
  vpc_id: vpc-05b1c86f6 # Newly created vpc
  cidr_block: 10.2.0.0/16
peerings:
  - vpc-0639fb93ca # Existing vpc
  - vpc-0e8909bd8c # Existing vpc
security:
  type: all # Options: all, ssh, icmp
  security_group_ingress_cidr_block: 10.0.0.0/8
  security_group_engress_cidr_block: 0.0.0.0/0
route_tables: 
  - rtb-05957ee1d # Route table(s) of the new VPC
```

#### Security Type Choices

When setting the security type variable, the following choices can be used. 

| Type Choice | Description                                                      |
| ----------- | ---------------------------------------------------------------- |
| `all`       | Allows all traffic from the peered VPC(s) into the new VPC       |
| `ssh`       | Allows only ssh traffic from the peered VPC(s) into the new VPC  |
| `icmp`      | Allows only ICMP traffic from the peered VPC(s) into the new VPC |

### Architecture Diagram

![Deployment Architecture Diagram](./files/peer_network_diagram.png)