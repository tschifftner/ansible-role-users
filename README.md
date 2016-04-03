# Ansible Role: Users

[![Build Status](https://travis-ci.org/tschifftner/ansible-role-users.svg)](https://travis-ci.org/tschifftner/ansible-role-users)

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


## User password

To generate a password hash use

```
mkpasswd --method=SHA-512
```

## Dependencies

None.

## Example Playbook

    - hosts: server
      roles:
        - { role: tschifftner.users }

## License

MIT / BSD

## Author Information

 - Tobias Schifftner, @tschifftner