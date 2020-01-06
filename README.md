Ansible Role: hassio_installer_setup
=========

Ansible role for installing Home Assistant via hassio-installer ( https://github.com/home-assistant/hassio-installer ) on CentOS

Requirements
------------

Only requirement is base installation of CentOS 7 and that firewalld is used as default firewall. The role takes care of installing dependencies, docker and opens required firewall ports.

Role Variables
--------------

The following configuration variables are available. The values provided below are the default values.
```yaml
# Opens ports for homekit in firewalld
hassio_fw_enable_homekit: false
# Opens ports for mqtt in firewalld
hassio_fw_enable_mqtt: false
# Opens ports for http in firewalld
hassio_fw_enable_http: false
# Opens ports for https in firewalld
hassio_fw_enable_https: false
# Opens ports for Nginx Proxy Manager Addon in firewalld
hassio_fw_enable_proxymanager: false
# Opens ports for homeassistant default port in firewalld
hassio_fw_enable_homeassistant: true
# Opens ports for unify addon in firewalld
hassio_fw_enable_unifi: false
# Opens ports for multicast dns in firewalld
hassio_fw_enable_mdns: false
```

Dependencies
------------

This role uses geerlingguy.docker for installing or upgrading docker on the host.

Example Inventory
----------------

Start by creating inventory ( for example `inventory.ini` where you specify where your homeassistant is located. You can specify `ansible_host="your-ip-number"` if you do not have a dns name for homeassistant machine.

```ini
[homeassistant]
hassio.local ansible_host="192.168.0.10"
```

Example Playbook
----------------

Create a playbook with the following contents, for example `install_homeassistant.yml`.

```yaml
- hosts: homeassistant
  become: true

  tasks:
    - include_role:
        name: samueljon.hassio_installer_setup
      vars:
        hassio_fw_enable_homekit: true
        hassio_fw_enable_mqtt: true
        hassio_fw_enable_http: true
        hassio_fw_enable_https: true
        hassio_fw_enable_proxymanager: true
        hassio_fw_enable_homeassistant: true
        hassio_fw_enable_unifi: true
        hassio_fw_enable_mdns: true
```
Example Playbook run
--------------------

```shell
# Start by checking if homeassistant is reachable
ansible -m ping -i inventory.ini homeassistant
# Install the ansible galaxy role that the playbook uses
ansible-galaxy install samueljon.hassio_installer_setup
ansible-galaxy install geerlingguy.docker
# If the server responds with PONG then you can execute the playbook. If the host is unreachable then refer to the ansible documentation on how to connect to hosts with ansible. 
ansible-playbook -i inventory.ini install_homeassistant.yml
```

License
-------

BSD, MIT

Author Information
------------------

The role was created by @samueljon. Pull Requests are welcome and please report bugs in the issues section.
