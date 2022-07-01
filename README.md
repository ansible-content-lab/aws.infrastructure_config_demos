[![Validation CI](https://github.com/ansible-content-lab/cloud.aws_roles/actions/workflows/validate.yml/badge.svg)](https://github.com/ansible-content-lab/cloud.aws_roles/actions/workflows/validate.yml)

# Ansible Collection - cloud.aws_roles

This repository hosts the `cloud.aws_roles` Ansible Collection.

The collection includes a variety of Ansible roles and playbook to help automate the management of resources on AWS.

This content was developed as part of the [Ansible Content Lab for Cloud Content](https://ansible-content-lab.github.io/), a program from the Ansible team to help incubate Ansible cloud use cases from ideation to collections and roles.

## Included Content

<!--start collection content-->
### Roles

Click on the role name to be directed to the README specifically for that role.

| Name                                                                                                                                              | Description                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| [cloud.aws_roles.direct_peered_networks](https://github.com/ansible-content-lab/cloud.aws_roles/blob/main/roles/direct_peered_networks/README.md) | A role to create a VPC networking architecture that includes peer networking DMZ and private networks. |
| [cloud.aws_roles.peer_existing_networks](https://github.com/ansible-content-lab/cloud.aws_roles/blob/main/roles/peer_existing_networks/README.md) | A role to automate the peering of two or more VPCs through direct peering model.                       |

### Playbooks

| Name                                  | Role(s) Used                   | Description                                                                                |
| ------------------------------------- | ------------------------------ | ------------------------------------------------------------------------------------------ |
| `cloud.aws_roles.create_peer_network` | `roles.direct_peered_networks` | A playbook to create a multi-VPC peer network configuration with DMZ and private networks. |
| `cloud.aws_roles.delete_peer_network` | `roles.direct_peered_networks` | Deletes AWS resources created in the `create_peer_network` playbook.                       |
| `cloud.aws_roles.peer_networks`       | `roles.peer_networks`          | Peer two or more VPCs with VPC peering.                                                    |
<!--end collection content-->

#### Create Peer Network

The `cloud.aws_roles.create_peer_network` playbook runs the work in the `roles.direct_peered_networks` role.  It has another tasks block that will attempt to configure the resources deployed by that role a bit farther.  When the role completes, EC2 instances in the DMZ will still need to be configured with SSH configuration in order to communicate with EC2 instances in the private network(s).

To connect to the DMZ EC2 instance, the `ansible_ssh_private_key_file` variable needs to be set so that the machine running the playbook can connect to the newly created EC2 instance.  You may set this variable in any way that Ansible allows, i.e. extra var, host var, etc.  It must be set or the configuration step will be skipped.  The `ansible_ssh_user` variable is set automatically to the user `ec2-user` that is standard on AWS AMIs.

When the following variables are set, then the playbook will also configure the DMZ EC2 instance with the SSH config and a private key to communicate with each other.  This leaves the deployment in an immediately accessible state.

```yaml
# These variables determine if there is an attempt to configure the DMZ VM to connect to other VMs.
priv_network_ssh_key_name: aws-test-key # The name of the AWS SSH key used to configure EC2 instances on the private network
ansible_ssh_private_key_file_local_path: ~/.ssh/aws-test-key.pem # Must exist locally or be mapped in an EE
ansible_ssh_private_key_file_dest_path: ~/.ssh/aws-test-key.pem # This will be the destination for the private key
priv_network_hosts_pattern: 10.* # Will use the same username and ssh key for any host on the 10.* network
priv_network_ssh_user: ec2-user # Will likely always be `ec2-user`, but set here as an option
```

## Installation and Usage

### Installing the Collection with the Ansible Galaxy CLI

Before using the this collection, you need to install it with the Ansible Galaxy CLI:

`ansible-galaxy collection install git+https://github.com/ansible-content-lab/cloud.aws_roles.git`

You can also include it in a `requirements.yml` file and install it via `ansible-galaxy collection install -r requirements.yml`, using the format:

```yaml
---
collections:
  - name: https://github.com/ansible-content-lab/cloud.aws_roles.git
    type: git
    version: main
```

### Adding a Git Pre-Commit Hook

This repo includes a configuration file for `ansible-lint` to be run as a git [pre-commit](https://pre-commit.com/) hook. To install the hook, run `pre-commit install` from the root directory of this repo once you have the pre-commit utility installed on your machine.

# License
GNU General Public License v3.0 or later

See [LICENCE](https://github.com/ansible-content-lab/cloud.aws_roles/blob/main/LICENSE) to see the full text.