# Ansible Role: Users

[![Build Status](https://travis-ci.org/tschifftner/ansible-role-users.svg?branch=master)](https://travis-ci.org/tschifftner/ansible-role-users)

Configure users and ssh access on Debian/Ubuntu linux servers.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```
users_ssh_password_authentication: 'Yes'
users_ssh_permit_root_login: 'Yes'
users_ssh_port: '22'
```

### Manage admin users

```
users_admin_require_sudo_password: false
users_admin_group: 'admin'
users_admin:
  - name: admin1
    state: present
    group: admin1
    grous: ['{{ users_admin_group }}']
    password: '$6$Aqh2Oxtx...DzKWXeHgulX1SJ.'
    update_password: always
    sshkeys:
      - key: 'ssh-rsa AAAAB...XJtw== admin1@example.com'
      	state: present

  - name: admin2
    state: present
    group: admin2
    groups: ['{{ users_admin_group }}']
    password: '$6$Aqh2Oxtx...DzKWXeHgulX1SJ.'
    update_password: always
    sshkeys:
      - key: 'ssh-rsa AAAAB...XJtw== admin2@example.com'
        state: present
```

### Manage normal users

```
users_normal:
  - name: 'user1'
    state: present
    password: '$6$Aqh2Oxtx...DzKWXeHgulX1SJ.'
    update_password: 'always'
    group: "user1"
    home: '/var/www/user1'
    groups: ['sftp', 'ssh']
    mode: '0755'

  - name: 'user2'
    state: present
    password: '$6$Aqh2Oxtx...DzKWXeHgulX1SJ.'
    update_password: 'always'
    group: "user2"
    home: '/var/www/user2'
    groups: ['sftp']
    mode: '0755'
```

### Manage system users

System users are defined in vars file and therefore not supposed to be used for normal users!

```
users_system:
  - name: 'root'
    state: present
```

### Remove user

There are two ways to remove users

_1) Set state=absent_

```
users_normal:
  - name: 'user1'
    state: absent
    password: '$6$Aqh2Oxtx...DzKWXeHgulX1SJ.'
    update_password: 'always'
    group: "user1"
    home: '/var/www/user1'
    groups: ['sftp', 'ssh']
    mode: '0755'

  - name: 'user2'
    state: absent
```

_2) Add to ```users_remove``` array_

```
users_remove: ['user2', 'user22']
```

### User password

User passwords must be a generated hash. To generate a password hash use

```
mkpasswd --method=SHA-512
```

## SSH Config

### Manage sshd_config

```
users_ssh_config:
  - regexp: "^PasswordAuthentication"
    line: "PasswordAuthentication yes"
  - regexp: "^PermitRootLogin"
    line: "PermitRootLogin no"
  - regexp: "^Port"
    line: "Port 2222"
```

## Dependencies

None.

## Example Playbook

    - hosts: server
      roles:
        - { role: tschifftner.users }

## Supported OS

 - Debian 9 (Stretch)
 - Debian 8 (Jessie)
 - Ubuntu 18.04 (Bionic Beaver)
 - Ubuntu 16.04 (Xenial Xerus)
 
## Required ansible version

Ansible 2.5+

## License

[MIT License](http://choosealicense.com/licenses/mit/)

## Author Information

 - [Tobias Schifftner](https://twitter.com/tschifftner), [ambimax® GmbH](https://www.ambimax.de)