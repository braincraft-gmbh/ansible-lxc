Role Name
=========

This role automates the setup of LXC hosts with the needed packages, create containers and setup the forwarding rules.

Requirements
------------

This role is designed and tested for Debian 9 (stretch).

Role Variables
--------------

bridge_interface: lxcbr0

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
