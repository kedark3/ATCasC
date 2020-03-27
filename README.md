# Playbooks to Deploy-Configure Ansible Tower

THIS IS a WORK in PROGRESS.

This directory contains playbooks that can be used to deploy and configure Ansible Tower(AT) using Ansible.

Requirements
------------
In order to execute the playbooks successfully, you would want to review following two files:

* deploy-template-config.yml - This file contains all necessary variables to deploy a new VM on RHV using the template specified and resource configurations.
* tower-config-vars.yml - This variables file is dedicated to configure the Ansible Tower post deployment and is referenced by `configure-tower.yml` playbook.


How to use files in this directory
----------------------------------
There are 3 playbooks in this directory.
1) install-tower.yml -- This playbook is designed to use `deploy-template-config.yml` and Deploy a VM from template and configure it, install Ansible Tower, tower-cli etc.

2) configure-tower.yml -- This is next playbook, that is used to perform post deploy config on tower. That means, that playbook will create Users, Orgs, projects, Job Templates, LDAP Config and so on. It refers `tower-config-vars.yml` to understand what needs to be done. And to maintain AT as IaC(Infrastructure-as-Code) then it is best to updtae the config-vars and re-run the playbook.

3) deploy-tower-end-to-end.yml -- This playbook, very simply, combines above two playbooks and can run end-to-end to provide you ready to user Ansible tower.

Example Execution commands
---------------------------

* To run end-to-end:
```
ansible-playbook playbooks/setup-ansible-tower/deploy-tower-end-to-end.yml
```
* To run install-only:
```
ansible-playbook playbooks/setup-ansible-tower/install-tower.yml
```
* To run config only:
```
ansible-playbook -i inventory -i <ip_addr_for_tower>, -l <ip_addr_for_tower> -u root playbooks/setup-ansible-tower/configure-tower.yml -e target_hosts=<ip_addr_for_tower>
```

To Run meta backup/full backup:
```
ansible-playbook -i inventory -i <tower IP or hostname>, -l <tower IP or hostname> meta-json-only-backup.yml -e 'target_hosts=<tower IP or hostname>' -u root
ansible-playbook -i inventory -i <tower IP or hostname>, -l <tower IP or hostname> full-backup.yml -e 'target_hosts=<tower IP or hostname>' -u root
```

To Run meta backup/full restore:

```
ansible-playbook -i inventory -i <tower IP or hostname>, -l <tower IP or hostname> meta-json-only-restore.yml -e 'target_hosts=<tower IP or hostname>' -u root
ansible-playbook -i inventory -i <tower IP or hostname>, -l <tower IP or hostname> full-restore.yml -e 'target_hosts=<tower IP or hostname>' -u root
```

To configure LDAP on tower:
```
ansible-playbook -i inventory -i <tower IP or hostname>, -l <tower IP or hostname> playbooks/setup-ansible-tower/configure-ldap-on-tower.yaml -e target_hosts=<tower IP or hostname> -u root
```

To upgrade Ansible Tower:
```
ansible-playbook upgrade-tower.yml -u root -e target_hosts=<IP or hostname> -l <IP or hostname> -e tower_setup_bundle_tar_url=<setup_bundle_url_of_desired_version>
```

License
-------

BSD

Author Information
------------------

Kedar Kulkarni <kedar.kulkarni0@gmail.com>
