Role Name
=========

This role automates the setup of LXC hosts with the needed packages, create containers and setup the networking and forwarding rules.

Requirements
------------

This role is designed and tested for Debian 9 (stretch).

Role Variables
--------------

The following variables need to be present, exist as defaults in the role and require no additional definition in the playbooks or environment vars:

```
container_name: "{{ {{ inventory_hostname}} | regex_replace('host.') }}"
ip_int: 'dhcp'
network_setup: false
bridge_interface: lxcbr0
```

Furthermore, the role expects the variables ```location_sub``` ```type_sub``` and ```number``` to be able to properly assemble the network variables.

The following variables are undefined per default and will trigger additional setup when defined within the playbooks/run:

zfs_root: "storage/{{ container_name }}/rootfs"   # will make lxc use the zfs backend
host_interface_phys: "eno2"                       # physical interface from host, to be mounted in container as eth1



Dependencies
------------

This role has no dependencies.

Example Playbook
----------------

    - hosts: baremetal
      roles:
         - { role: bc.lxc }

License
-------

GNU GPLv3

Author Information
------------------

Gualter Barbas Baptista <gb@braincraft.de>
