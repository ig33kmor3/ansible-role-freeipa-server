# ansible-role-freeipa-server

## Requirements

- CentOS 8
- ```/etc/hosts``` - configured for the master and replicas

## Installation

Define in requirements.yml

```bash
- src: https://github.com/ig33kmor3/ansible-role-freeipa-server.git
  version: master
  name: ig33kmor3-freeipa-server
```

Add to project:

```bash
ansible-galaxy install -r requirements.yml -f
```

## Configuration

Set variables in playbook for [ all ] group

```yml
realm: DOMAIN.LOCAL
domain: domain.local
ds_password: password
admin_password: password
dns_forwarder_1: 8.8.8.8
dns_forwarder_2: 8.8.4.4
```

Inventory must have [ master ] and [ replica ] group

```bash
[master]
ipa1.domain.local ansible_host=ipa1.domain.local

[replica]
ipa2.domain.local ansible_host=ipa2.domain.local
```
