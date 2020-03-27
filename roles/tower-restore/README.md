Role Name
=========

This role will allow you to run restore of Ansible Tower using tar or JSON file.

Requirements
------------

One of the things you need to make sure to setup is `tower-cli` which can be done using `pip install ansible-tower-cli`.

Role Variables
--------------

- full_backup: Bool. If you wish to restore from a full backup tar file, use this variable - set it to True.
- meta_backup: Bool. If you only have a json file to restore from, use this variable - set it to True
- backup_path: this is where this role will look for backup files on your tower vm.
- restore_json_file: this is the location of json backup file which would be used by meta-backup-restore tasks.
- restore_tar_file: this is the location of tar backup file which would be used by full-backup-restore tasks.
- tower_setup_bundle_tar_url: using this variable we are pulling latest(or you can choose based on your tower varsion) to download setup bundle which will allow us to run `./setup.sh` with `-r` for backup. Downloaded tar and extracted directories are removed irrespective of success or failure.
- tower_admin_password: This role assumes 'admin' user is availble and asks you to provide password for it, so that tower-cli can authenticate with your tower.

Example Playbook
----------------

Full restore:

    - hosts: servers
      roles:
         - role: tower-restore
           full_backup: True
           # Other variables from above variable list you wish to override


Meta restore:

    - hosts: servers
      roles:
         - role: tower-restore
           meta_backup: True
           # Other variables from above variable list you wish to override



License
-------

BSD

Author Information
------------------

Kedar Kulkarni <kedar.kulkarni0@gmail.com>
