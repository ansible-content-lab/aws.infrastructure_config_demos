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
| [cloud.aws_roles.deploy_peered_networks](https://github.com/ansible-content-lab/cloud.aws_roles/blob/main/roles/deploy_peered_networks/README.md) | A role to create a VPC networking architecture that includes peer networking DMZ and private networks. |
| [cloud.aws_roles.peer_existing_networks](https://github.com/ansible-content-lab/cloud.aws_roles/blob/main/roles/peer_existing_networks/README.md) | A role to automate the peering of two or more VPCs through direct peering model.                       |

### Playbooks

| Name                                  | Role(s) Used                   | Description                                                                                |
| ------------------------------------- | ------------------------------ | ------------------------------------------------------------------------------------------ |
| `cloud.aws_roles.create_peer_network` | `roles.deploy_peered_networks` | A playbook to create a multi-VPC peer network configuration with DMZ and private networks. |
| `cloud.aws_roles.delete_peer_network` | `roles.deploy_peered_networks` | Deletes AWS resources created in the `create_peer_network` playbook.                       |
| `cloud.aws_roles.peer_networks`       | `roles.peer_networks`          | Peer two or more VPCs with VPC peering.                                                    |
<!--end collection content-->

## Installation and Usage

### Installing the Collection with the Ansible Galaxy CLI

Before using the aws_roles collection, you need to install it with the Ansible Galaxy CLI:

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