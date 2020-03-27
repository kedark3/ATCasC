Role Name
=========

This role will allow you to run backup of Ansible Tower.

Requirements
------------

One of the things you need to make sure to setup is `tower-cli` which can be done using `pip install ansible-tower-cli`.

Role Variables
--------------

- full_backup: Bool. This can be set to True/False, based on if you want to run a Full(comprehensive) backup that is comprising of postgresql db backup too. It will create a tar file automatically with timestamp and also symlink it with `-latest` filename.
- meta_backup: Bool. This can be set to True/False, based on if you want to run a small(metadata) only, which is done using tower-cli and it will create json file with timestamp and symlink it with `-latest` filename.

- backup_path: this is where the backed up files would end up.
- backup_json_file: this var will tell role where to put the json file that is created by backup.
- tower_setup_bundle_tar_url: using this variable we are pulling latest(or you can choose based on your tower varsion) to download setup bundle which will allow us to run `./setup.sh` with `-b` for backup. Downloaded tar and extracted directories are removed irrespective of success or failure.

Example Playbook
----------------

Full backup:

    - hosts: servers
      roles:
         - role: tower-backup
           full_backup: True
           # Other variables from above variable list you wish to override


Meta backup:

    - hosts: servers
      roles:
         - role: tower-backup
           meta_backup: True
           # Other variables from above variable list you wish to override



License
-------

BSD

Author Information
------------------

Kedar Kulkarni <kedar.kulkarni0@gmail.com>
