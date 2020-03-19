Ansible Role SSH client
=========

[![Build Status](https://travis-ci.com/Turgon37/ansible-ssh-client.svg?branch=master)](https://travis-ci.com/Turgon37/ansible-ssh-client)
[![License](https://img.shields.io/badge/license-MIT%20License-brightgreen.svg)](https://opensource.org/licenses/MIT)
[![Ansible Role](https://img.shields.io/badge/ansible%20role-Turgon37.ssh_client-blue.svg)](https://galaxy.ansible.com/Turgon37/ssh_client/)

## Description

:grey_exclamation: Before using this role, please know that all my Ansible roles are fully written and accustomed to my IT infrastructure. So, even if they are as generic as possible they will not necessarily fill your needs, I advice you to carrefully analyse what they do and evaluate their capability to be installed securely on your servers.

This roles allow configuration of ssh client with defaults settings such available cipher, macs, ...

## Requirements

Require Ansible >= 2.4

### Dependencies

## OS Family

This role is available for Debian and CentOS

## Features

At this day the role can be used to :

  * configure ssh client
  * [local facts](#facts)

## Role Variables

All variables which can be overridden are stored in [defaults/main.yml](defaults/main.yml) file as well as in table below. To see default values please refer to this file.

Most of the variable refer to the pure ssh config parameter. Please fetch informations from the man page.

| Name                                            | Types/Values| Description                                        |
| ------------------------------------------------| ------------|--------------------------------------------------- |
| `ssh_client__facts`                             | Boolean     | Install the local fact script                      |
| `ssh_client__port`                              | Integer     |                                                    |
| `ssh_client__address_family`                    | String      |                                                    |
| `ssh_client__proxy_command`                     | String      |                                                    |
| `ssh_client__password_authentication`           | Boolean     |                                                    |
| `ssh_client__challenge_response_authentication` | Boolean     |                                                    |
| `ssh_client__keyboardinteractive_authentication`| Boolean     |                                                    |
| `ssh_client__pubkey_authentication`             | Boolean     |                                                    |
| `ssh_client__host_based_authentication`         | Boolean     |                                                    |
| `ssh_client__gssapi_authentication`             | Boolean     |                                                    |
| `ssh_client__gssapi_delegate_credentials`       | Boolean     |                                                    |
| `ssh_client__gssapi_key_exchange`               | Boolean     |                                                    |
| `ssh_client__gssapi_trust_dns`                  | Boolean     |                                                    |
| `ssh_client__forward_x11`                       | Boolean     |                                                    |
| `ssh_client__custom_config_global|group|host`   | Dict        | Define custom options per host (see example below) |


## Facts

By default the local fact are installed and expose the following variables :


```
ansible_local.ssh_client:
  version_full: '7.9p1'
  version_major: '7'
```

## Example

### Playbook

Use it in a playbook as follows:

```yaml
- hosts: all
  roles:
    - turgon37.ssh_client
```

### Inventory

To use this role create or update your playbook according the following example :

```
ssh_client__global_known_host_file: /etc/ssh/ssh_known_hosts
ssh_client__global_known_host_hashed_file: '{{ ssh_client__global_known_host_file }}_hashed'

ssh_client__known_hosts:
  - '{{ ssh_client__global_known_host_hashed_file }}'
  - '/var/lib/sss/pubconf/known_hosts'

ssh_client__proxy_command: '/usr/bin/sss_ssh_knownhostsproxy -p %p %h'

ssh_client__custom_config_global:
  host1:
    GSSAPIServerIdentity: host1.mgmt
```