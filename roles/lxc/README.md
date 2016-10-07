# ansible-lxc

A role to install and configure lxc on a host.

## Requirements

### Ansible version

Minimum required ansible version is 1.8.

### Other considerations

You have to setup networking. Basically, you have the several options.

  1. Use lxc-net service (on ubuntu)
  2. Use libvirt `virbr0` bridge.
  3. Create your own linux brigde.
  4. Use an openvswitch bridge

It is not within the scope of this role to alter in any way your network stack. On the opposite, you must specify this role what network infrastructure to use.


## Description

- install the packages (if on ubuntu will install the ppa).
- template lxc config files
  - system wide files
  - unprivileged users config file

After that, your are ready to spawn lxc containers. Check out my ansible-lxcm
('m' for manager) role.


## Role Variables

### Variables conditionally loaded

Those variables from `vars/*.{yml,json}` are loaded dynamically during task
runtime using the `include_vars` module.

Variables loaded from `vars/Debian.yml`.

```yaml
---

lxc_pkgs:
  - lxc
  - lxd
  - lxc-templates
  - python3-lxc
  - python-lxc
  # - lxd-tools

```

Variables loaded from `vars/RedHat.yml`.

```yaml
lxc_pkgs:
  - lxc
  - lxc-extra
  - lxc-templates

```

### Default vars

Defaults from `defaults/main.yml`.

```yaml
# defaults file for ansible-lxc

lxc_pkg_state: installed

private_dir: "{{ playbook_dir }}/private"

# upriviledged users directory to create
lxc_directories:
  - '.local/share/lxc'
  - '.local/share/lxcsnaps'
  - '.cache/lxc'
  - '.config/lxc'

# container defaults (defaults.conf)
# /etc/lxc/default.conf | ~/.config/lxc/default.conf
lxc_network_type: veth
lxc_network_link: lxcbr0
lxc_network_bridge_type: bridge
lxc_network_flags: up
lxc_network_hwaddr: '00:16:3e:xx:xx:xx'
lxc_network_ipv4_gateway: auto
lxc_network_ipv6_gateway: auto

# lxc.conf defaults
# /etc/lxc/lxc.conf | ~/.config/lxc/lxc.conf

# backend storage
# lxc_bdev_lvm_vg: lxc
# location in which all containers are stored
# lxc_lxcpath: /var/lib/lxc
# path to the default container configuration
# lxc_default_config: /etc/lxc/default.conf ||  ~/.config/lxc/default.conf

# lxc-net defaults
# lxc_bridge_port: none

# lxc_use_bridge: yes
# lxc_bridge: lxcbr0
# lxc_ipv4: 10.0.3.1/24
# lxc_ipv6: fd4b:93da:8643:3046::1/64
# lxc_ipv6_nat: yes

# lxc_netmask: 255.255.255.0
# lxc_network: 10.0.3.0/24
#lxc_mtu: 1500

# # if "none" no gateway will on the LXC bridge, nat must
# # be "false" to use a gateway.
# lxc_gateway: none

# # lxc container nat enabled
# lxc_nat: true  ## If "true" nat rules will be created with the lxc network.

# lxc container dhcp settings
lxc_dhcp_range: 10.0.3.2,10.0.3.253
lxc_dhcp_max: 253
lxc_dhcp_config: ''
lxc_domain: 'lxc'

```


## Installation

### Install with Ansible Galaxy

```shell
ansible-galaxy install archf.lxc
```

Basic usage is:

```yaml
- hosts: all
  roles:
    - role: archf.lxc
```

### Install with git

If you do not want a global installation, clone it into your `roles_path`.

```shell
git clone git@github.com:archf/ansible-lxc.git /path/to/roles_path
```

But I often add it as a submdule in a given `playbook_dir` repository.

```shell
git submodule add git@github.com:archf/ansible-lxc.git <playbook_dir>/roles/lxc
```

As the role is not managed by Ansible Galaxy, you do not have to specify the
github user account.

Basic usage is:

```yaml
- hosts: all
  roles:
  - role: lxc
```

## Ansible role dependencies

None.

## License

MIT.

## Author Information

Felix Archambault.

## Role stack


This role was carefully selected to be part an ultimate deck of roles to manage
your infrastructure.

All roles' documentation is wrapped in this [convenient guide](http://127.0.0.1:8000/).


---
This README was generated using ansidoc. This tool is available on pypi!

```shell
pip3 install ansidoc

# validate by running a dry-run (will output result to stdout)
ansidoc --dry-run <rolepath>

# generate you role readme file
ansidoc <rolepath>
```

You can even use it programatically from sphinx. Check it out.