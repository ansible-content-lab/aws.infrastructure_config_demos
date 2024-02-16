# lab.aws_infrastructure_config_demos.mesh_demo

This role configures AWS infrastructure with a network and VM configuration that can be used for automation mesh demos including a public subnet, private subnet, hop node, and execution node; along with the dependent resources to allow networking traffic.

## Role Variables

```yaml
mesh_demo_aws_region: us-east-1
mesh_demo_tenancy: default
mesh_demo_vpc_priv_net_cidr: 10.0.0.0/20
mesh_demo_priv_subnet_cidr: 10.0.0.0/24
mesh_demo_pub_subnet_cidr: 10.0.1.0/24
mesh_demo_ssh_key_name: default_keypair
mesh_demo_hop_node_instance_type: t2.small
mesh_demo_hop_node_instance_name: hop_node
mesh_demo_execution_node_instance_type: t2.small
mesh_demo_execution_node_instance_name: execution_node
```

## Dependencies

### Collections

* `amazon.aws`

## Example Playbook

```yaml
---
- name: Deploy automation mesh demo
  hosts: localhost
  connection: local
  gather_facts: false
  tasks:
    - name: Create automation mesh demo
      ansible.builtin.include_role:
        name: lab.aws_infrastructure_config_demos.mesh_demo
```

## License

GPLv3

## Author Information

Scott Harwell <sharwell@redhat.com>
