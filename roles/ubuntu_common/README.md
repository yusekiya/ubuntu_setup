Ansible role: ubuntu_common
=========

Common setup of ubuntu.
This role performs the followig tasks:

- Change timezone (tags: timezone)
- Change hostname (tags: hostname)
- Install packages through apt-get (tags: apt)

All the tasks need root privilege.


Requirements
------------

- Ansible (2.1.1+)


Role Variables
--------------

Available variables are listed below.

``` yaml
# hostname
ubuntu_common_hostname: ubuntu
# timezone
ubuntu_common_timezone: 'Asia/Tokyo'
# Packages to be installed
ubuntu_common_packages:
  - {name: vim}
  - {name: git}
  - {name: fonts-takao}
  - {name: rsync}
```


Dependencies
------------

None


Example Playbook
----------------

``` yaml
- hosts: all
  vars_files:
      - vars/main.yml
  roles:
      - {role: ubuntu_common, become: yes}
```


License
-------

MIT

