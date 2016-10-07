# ansible-openssh-server

A role to install and configure openssh-server on a target host.

## Requirements

### Ansible version

Minimum required ansible version is 2.0.


## Role Variables

### Variables conditionally loaded

Those variables from `vars/*.{yml,json}` are loaded dynamically during task
runtime using the `include_vars` module.

Variables loaded from `vars/Debian.yml`.

```yaml
sshd_service_name: ssh

sshd_packages:
  - openssh-server

```

Variables loaded from `vars/RedHat.yml`.

```yaml
sshd_service_name: sshd

sshd_packages:
  - openssh

```

### Default vars

Defaults from `defaults/main.yml`.

```yaml
# defaults/main.yml file for openssh-server
sshd_config: []

sshd_Port: 22
sshd_PermitRootLogin: 'yes'
sshd_ChallengeResponseAuthentication: 'no'
sshd_GSSAPICleanupCredentials: 'no'
sshd_X11Forwarding: 'yes'
sshd_ClientAliveInterval: 0
sshd_ClientAliveCountMax: 3
sshd_PasswordAuthentication: 'yes'
sshd_Banner: 'none'

```


## Installation

### Install with Ansible Galaxy

```shell
ansible-galaxy install archf.openssh-server
```

Basic usage is:

```yaml
- hosts: all
  roles:
    - role: archf.openssh-server
```

### Install with git

If you do not want a global installation, clone it into your `roles_path`.

```shell
git clone git@github.com:archf/ansible-openssh-server.git /path/to/roles_path
```

But I often add it as a submdule in a given `playbook_dir` repository.

```shell
git submodule add git@github.com:archf/ansible-openssh-server.git <playbook_dir>/roles/openssh-server
```

As the role is not managed by Ansible Galaxy, you do not have to specify the
github user account.

Basic usage is:

```yaml
- hosts: all
  roles:
  - role: openssh-server
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