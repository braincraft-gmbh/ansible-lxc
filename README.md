Role Name
=========

This role automates the setup of LXC hosts with the needed packages, create containers and setup the forwarding rules.

Requirements
------------

This role is designed and tested for Debian 9 (stretch).

Role Variables
--------------

bridge_interface: lxcbr0

The following variables are undefined per default and will trigger additional setup when defined within the playbooks/run:

zfs_root: "storage/{{ container_name }}/rootfs"   # will make lxc use the zfs backend
host_interface_phys: "eno2" # physical interface from host, to be mounted in container as eth1


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
