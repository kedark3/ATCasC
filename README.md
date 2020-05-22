# Playbooks to Deploy-Configure Ansible Tower/AWX
![Ansible Lint](https://github.com/kedark3/ATCasC/workflows/Ansible%20Lint/badge.svg)

This repository contains all the required Collections, Roles, Sample configs and Playbooks that can let you configure your ansible tower using code and also let you maintain the configurations-as-code. Hence Ansible-Tower-Configuration-as-Code (ATCasC)

This is declarative way to configure AWX or Ansible Tower. You specify a list of resources you would like, whereas for imperative you specify a list of commands to run to create the resources that you want. In this repo, you just have to declare WHAT you need in `tower-configs/` directory and it takes care of HOW it can be created/achieved.

Requirements
------------
In order to execute the playbooks successfully, you would want to review following two files:

* Tower-CLI python package is needed to be installed on your computer. Also, Python3-pip. If not, `tower-cli-installer` role will attempt to install it.

* Another thing that you need to do is look at `tower-configs/` directory that will house all the configurations-as-code pieces. You don't necessarily have to have everything, but at the minimum you need to have `tower-configs/tower-hostname.yml` filled with correct hostname, username and password.

* This repo assumes you have installed the Ansible Tower or AWX and it has license added to it, if needed.

Directory structure
-------------------

We have following directories in the Repo:

* collections: This directory houses awx.awx collection that is downloaded from ansible galaxy As-is using following command:
```
ansible-galaxy collection install awx.awx -p collections/
```

* playbooks: This directory contains all the provided playbooks.

* roles: contains all the tower configuration roles.

* tower-configs: This directory houses all the files needed to config various parts of Ansible Tower.

* ansible.cfg: only config we are adding here is collections_paths, everything else is inherited from global ansible.cfg file automatically.

Playbooks in this repo
----------------------
There are 3 playbooks in this directory.
* configure-ldap-on-tower.yml : This playbook allows you to only configure LDAP on your AT, and it uses settings from `tower-configs/tower-settings-params.yml` which actually can house LDAP and other AT settings too. Since it primarily is used for LDAP, playbook is named such.

* configure-tower.yml : This playbook will call all of the Roles in `roles/` directory systematically to configure your tower using configurations from `tower-configs/` directory.

* TODO: List other playbook.



Example Execution commands
---------------------------

* To deploy tower on a VM: https://github.com/kedark3/infra-playbooks/tree/master/roles/tower-roles/deploy_ansible_tower

* To run config LDAP only:
```
ansible-playbook playbooks/configure-ldap-on-tower.yml -K
```
`-K` is needed in case you define `install_pip: true` for `tower-cli-installer` role.

* To configure tower:
```
ansible-playbook playbooks/configure-tower.yml -K
```
`-K` is needed in case you define `install_pip: true` for `tower-cli-installer` role.

* To run backup - meta only(JSON):
```
ansible-playbook playbooks/meta-json-only-backup.yml
```
Default path for backup is `backups/` in root of this repo.

* To run restore - meta only(JSON):
```
ansible-playbook playbooks/meta-json-only-restore.yml
```
Default path for backup is `backups/` in root of this repo.

License
-------

BSD

Author Information
------------------

Kedar Kulkarni <kedar.kulkarni0@gmail.com>
