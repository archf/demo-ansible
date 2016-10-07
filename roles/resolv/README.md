# ansible-resolv

A role to configure /etc/resolv.conf.

## Requirements

### Ansible version

Minimum required ansible version is 2.0.

## Description

You might not want to use this role depending on target device as it is often
a better practice to configure DNS settings through the network interfaces.


## Role Variables

### Variables conditionally loaded

None.

### Default vars

Defaults from `defaults/main.yml`.

```yaml
# defaults file for resolv

resolv_domain: ''

resolv_search: []

resolv_sortlist: []
resolv_options: []

```


## Installation

### Install with Ansible Galaxy

```shell
ansible-galaxy install archf.resolv
```

Basic usage is:

```yaml
- hosts: all
  roles:
    - role: archf.resolv
```

### Install with git

If you do not want a global installation, clone it into your `roles_path`.

```shell
git clone git@github.com:archf/ansible-resolv.git /path/to/roles_path
```

But I often add it as a submdule in a given `playbook_dir` repository.

```shell
git submodule add git@github.com:archf/ansible-resolv.git <playbook_dir>/roles/resolv
```

As the role is not managed by Ansible Galaxy, you do not have to specify the
github user account.

Basic usage is:

```yaml
- hosts: all
  roles:
  - role: resolv
```

## Ansible role dependencies

None.

## License

BSD.

## Author Information

Peter Hudec.

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