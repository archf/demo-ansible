# ansible-common

A meta role to perform basic configuration.

## Requirements

### Ansible version

Minimum required ansible version is 2.0.

## Description

This is a meta role to perform basic configuration. It contains no tasks and
its sole purpose is to tie together the roles listed as dependencies below.


## Role Variables

### Variables conditionally loaded

None.

### Default vars

None.

## Installation

### Install with Ansible Galaxy

```shell
ansible-galaxy install archf.common
```

Basic usage is:

```yaml
- hosts: all
  roles:
    - role: archf.common
```

### Install with git

If you do not want a global installation, clone it into your `roles_path`.

```shell
git clone git@github.com:archf/ansible-common.git /path/to/roles_path
```

But I often add it as a submdule in a given `playbook_dir` repository.

```shell
git submodule add git@github.com:archf/ansible-common.git <playbook_dir>/roles/common
```

As the role is not managed by Ansible Galaxy, you do not have to specify the
github user account.

Basic usage is:

```yaml
- hosts: all
  roles:
  - role: common
```

## Ansible role dependencies

  * accounts
  * packages
  * openssh-server
  * ntpd

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