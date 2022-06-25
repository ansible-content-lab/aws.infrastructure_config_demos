[![Validation CI](https://github.com/ansible-content-lab/cloud.aws_roles/actions/workflows/validate.yml/badge.svg)](https://github.com/ansible-content-lab/cloud.aws_roles/actions/workflows/validate.yml)

# Ansible Collection - cloud.aws_roles

This repository hosts the `cloud.aws_roles` Ansible Collection.

The collection includes a variety of Ansible roles and playbook to help automate the management of resources on AWS.

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
| `cloud.aws_roles.peer_networks`       | `roles.peer_networks`          | Peer two or more VPCs.                                                                     |
<!--end collection content-->

## Installation and Usage

### Installing the Collection from Ansible Galaxy

Before using the aws_roles collection, you need to install it with the Ansible Galaxy CLI:

    ansible-galaxy collection install cloud.aws_roles

You can also include it in a `requirements.yml` file and install it via `ansible-galaxy collection install -r requirements.yml`, using the format:

```yaml
---
collections:
  - name: [cloud.aws_roles](https://github.com/ansible-content-lab/cloud.aws_roles)
    type: git
    version: main
```

# License
GNU General Public License v3.0 or later

See [LICENCE](https://github.com/Ansible-Incubated-Content/cloud.aws_roles/blob/main/LICENSE) to see the full text.