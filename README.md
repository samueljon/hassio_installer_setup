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

Example Playbook
----------------

    - hosts: homeassitant
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

License
-------

BSD, MIT

Author Information
------------------

The role was created by @samueljon. Pull Requests are welcome and please report bugs in the issues section.
