Role Name
=========

A role to provision LXC containers, with network setup and support for ZFS.

Requirements
------------

The role requires a host setup with LXC and with an available interface (e.g.
`lxcbr0`). The role should be delegated to the host(s) where the containers are
to be deployed.

Role Variables
--------------

The following variables are set as default:

```
location: local
container_name: "{{ inventory_hostname }}"
lxc_distribution: debian
lxc_release: stretch
lxc_arch: amd64
lxc_root: '/var/lib/lxc'
```

The hosts need at least a network, which by default is `lxcbr0` with a DHCP
assignment. You can also enforce static IPs and add multiple interfaces to
it:

```
lxc_network:
  - name: eth0
    type: veth
    link: lxcbr0
#    ipv4: '192.168.1.10'
#    ipv4_netmask: '24'
#    ipv4_gateway: '192.168.1.1'
#  - name: eth1
#    type: phys
#    link: eth2
```

If ZFS is to be used, `zfs_root` should be set to the base dataset. This will be
used on LXC creation to create additional datasets for the containers.

```
# zfs_root: tank/lxc
```

Additional container configuration can be passed to the `container_config` var:

```
# container_config:
#   - "lxc.aa_profile=unconfined"
#   - "lxc.cgroup.devices.allow=a *:* rmw"
```

When a new host is created, commands set on the `container_prepare_commands` var
will be dispatched. Following defaults allow the container to be upgraded and
setup for ansible and SSH access:

```
container_prepare_commands: |
  apt-get update
  apt-get upgrade -y
  apt-get install -y python-minimal openssh-server
```


Dependencies
------------

None.

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

Gualter Barbas Baptista <gualter@ecobytes.net>
