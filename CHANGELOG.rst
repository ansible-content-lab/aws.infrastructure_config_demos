=========================================================
lab.azure.azure_infrastructure_config_demos Release Notes
=========================================================

.. contents:: Topics

This changelog describes changes after version 2.0.0.

v3.0.0
======

Release Summary
---------------

Updated the collection to match validated patterns.

Major Changes
-------------

- Moved playbooks into playbooks folder so that playbooks may be called from `namespace.collection.playbook` syntax.
- Updated Ansible Lint config.

Breaking Changes / Porting Guide
--------------------------------

- Playbook names have changed.
- Playbook paths have changed.
- Playbooks now reference role by FQRN.
