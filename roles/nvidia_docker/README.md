Ansible role: nvidia docker
=========

Install nvidia docker on Ubuntu 14.04 through 16.04.
All the tasks need root privilege.

Requirements
------------

None.

Role Variables
--------------

None.

Dependencies
------------

None.

Example Playbook
----------------

``` yaml
- hosts: all
  vars_files:
    - vars/main.yml
  roles:
    - {role: nvidia_docker, become: yes}
```

License
-------

MIT

