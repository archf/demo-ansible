# ansible-synergy

A role to install synergy from a debian or rhel package.

## Requirements

### Ansible version

Minimum required ansible version is 2.0.

### Other considerations

Place your synergy package inside the `file` directory.
This role might not be the latest. Fork it 'n update if needed.


## Description

The package is copied to `/opt/` on target host. It creates a synergy unix
group. You should then append your user to it.


## Role Variables

### Variables conditionally loaded

Those variables from `vars/*.{yml,json}` are loaded dynamically during task
runtime using the `include_vars` module.

Variables loaded from `vars/Debian.yml`.

```yaml
# list of packages to install
synergy_package: synergy-v1.7.4-stable-c734bab-Linux-x86_64.deb

```

Variables loaded from `vars/RedHat.yml`.

```yaml
# list of packages to install

synergy_package: synergy-v1.7.4-stable-c734bab-Linux-x86_64.rpm

```

### Default vars

Defaults from `defaults/main.yml`.

```yaml
# An external directory containing the synergy packages.
packages_dir: "{{ playbook_dir }}/private/packages"

# A list of files inside the synergy package. This is used to adjust group
# ownership and permissions.
synergy_paths:
  - /usr/bin/synergy
  - /usr/bin/synergyd
  - /usr/bin/synergyc
  - /usr/bin/synergys
  - /var/log/synergy.log

```


## Installation

### Install with Ansible Galaxy

```shell
ansible-galaxy install archf.synergy
```

Basic usage is:

```yaml
- hosts: all
  roles:
    - role: archf.synergy
```

### Install with git

If you do not want a global installation, clone it into your `roles_path`.

```shell
git clone git@github.com:archf/ansible-synergy.git /path/to/roles_path
```

But I often add it as a submdule in a given `playbook_dir` repository.

```shell
git submodule add git@github.com:archf/ansible-synergy.git <playbook_dir>/roles/synergy
```

As the role is not managed by Ansible Galaxy, you do not have to specify the
github user account.

Basic usage is:

```yaml
- hosts: all
  roles:
  - role: synergy
```

## Ansible role dependencies

None.

## Todo

  * put package outside of roles

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