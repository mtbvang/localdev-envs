# localdev-envs

A vagrant controlled virtualbox VM with Ubuntu 18.04 provisioned with Python 3 and tools with the Ansible role https://github.com/mtbvang/ansible-python3-role.

## Configuring git in the guest

Commands to configure git in the guest.

```
git config --global credential.helper store
git config --global user.name "<REPLACE WITH USERNAME>"
git config --global user.email <REPLACE WITH EMAIL>