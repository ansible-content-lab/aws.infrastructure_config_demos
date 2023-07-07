# Create VM Role

This Ansible role contains repeatable steps to provision new VMs into an existing VPC subnet. This operation works off a series of default variables that can be overridden from the calling playbook.

## Variables

The following variables are defined as defaults and are intended to be overridden by the user for different VM deployments.

### Required

```yaml
---
aws_region: us-east-1 # The region in which the resources are deployed
aws_keypair_name:  aws-test-key ## The AWS SSH key to use when configuring access to the EC2 instances
aws_instance_size: t2.micro # The instance size to deploy

## AMI Lookup - These variables are used to select the AMI to deploy
aws_image_filter: 'RHEL-8*HVM-*Hourly*' # The filter string used to search for an AMI
aws_image_owners: 309956199498 # (optional) Used for private AMIs such as Red Hat Cloud Access
aws_image_architecture: x86_64 # (optional) Used as required by the AMI and filter criteria
# aws_instance_ami: undef (optional) Used to override the filter parameters and explicitly identify an AMI

## Tag Defaults - These variables are the default tags for the created instance
vm_name: demo_vm
vm_deployment: default
vm_environment: default
vm_owner: ansible
vm_purpose: demo
```

### Other Variables

```yaml
tenancy: default
aws_securitygroup_name: private-network-sg # Name of security group to associate with the new VM
aws_vpc_subnet_name: priv-net-private-subnet # Name of the subnet to build the new VM
aws_ec2_wait: true # wait for confirmation that the instance has been created before proceeding
aws_userdata_template: default # userdata template to use for VM creation. default == empty userdata script
```

## Example Playbook

```yaml
---
- name: Create VM Demo
  hosts: localhost
  connection: local
  gather_facts: false
  vars_files:
    - "vm_blueprints/{{vm_blueprint}}.yml" #override variables here
  tasks:
    - name: Fail if variables not defined
      ansible.builtin.assert:
        that:
          - aws_region is defined
          - aws_keypair_name is defined
          - aws_instance_size is defined
        fail_msg: "Required variables not set"

    - name: include create vm role
      include_role:
        name: create_vm
```
