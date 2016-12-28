# Setup Ubuntu 16.04 with ansible

Setup script to build my workstation for research environment.
I have confirmed that the script works in the following system configuration:

| | model/version |
|---|---|
| CPU | Intel Core i7-6850K |
| GPU | GeForce GTX 1080 |
| OS | Ubuntu 16.04 64-bit PC (AMD64) desktop image |



## Requirements on control host

- Ansible (2.2.0)


## Initial setup

This section describes minimum installation settings.
One must use a physical terminal directly connected to the workstation for the following settings.

1. Boot Ubuntu and install from [ISO image][1]
2. Create user, set locale and timezone
3. Connect the server to LAN. Make sure that the connection is established even just after boot.
4. Make sure that directory name in home is in English (optional)

  ```bash
  $ LANG=C xdg-user-dirs-gdk-update
  ```

5. Install openssh-server

  ```bash
  $ sudo apt-get install openssh-server
  ```


## Setup with ansible

The following settings are performed over ssh.
Make sure that a control host can access to the target workstation over ssh, and ansible is installed on the control host.
Procedure to build the workstation is described in the ansible playbook `site.yml`.
Check roles described in `site.yml` and `README.md` of each role to see what type of tasks will be performed.
Take the following procedure to configure the workstation.

1. Clone ubuntu_setup repository on the control host.

  ``` bash
  $ git clone https://github.com/yusekiya/ubuntu_setup.git
  ```

2. Copy template inventory file `template_hosts` to inventory file `hosts`, and write the ip address of the workstation into the inventory file, e.g.,

  ``` ini:hosts
  [workstation]
  192.168.xxx.xxx
  # or with port number
  192.168.xxx.xxx:yyyy
  ```

3. Copy `vars/template.yml` to `vars/main.yml`, and modify variables in the file.
See `README.md` of each role for detailed information about the variables.
4. Modify the value of `remote_user` in `ansible.cfg` to a user name you want to login as.
5. Fetch required roles

  ```bash
  $ ansible-galaxy install -r requirements.yml -p ./roles
  ```

6. Run playbook

  ``` bash
  $ ansible-playbook site.yml
  ```

7. Rerun playbook after reboot just in case, and confirm that each task is ok.

<!-- References -->
[1]: http://releases.ubuntu.com/16.04/
