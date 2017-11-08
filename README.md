[![Build Status](https://travis-ci.org/while-true-do/ansible-role-cockpit.svg?branch=master)](https://travis-ci.org/while-true-do/ansible-role-cockpit)

# Ansible Role: cockpit
| A role to install [cockpit project](http://cockpit-project.org) packages.

## Installation

Galaxy Link: <https://galaxy.ansible.com/while-true-do/cockpit>

```
ansible-galaxy install while-true-do.cockpit
```

Github Link: <https://github.com/while-true-do/ansible-role-cockpit>

```
git clone https://github.com/while-true-do/ansible-role-cockpit while-true-do.cockpit
```

## Requirements

None.

## Dependencies

This role depends on <https://galaxy.ansible.com/while-true-do/pcp>.
You have to install the role:

```
ansible-galaxy install -r requirements.yml
```

And afterwards, can use/not use it with variables below.

## Role Variables

```
# defaults/main.yml
---
cockpit_packages: ['cockpit-system', 'cockpit-networkmanager', 'cockpit-packagekit', 'cockpit-storaged']
cockpit_selinux_packages: ['cockpit-selinux']
# Default with pcp dependency
cockpit_with_pcp: True
cockpit_pcp_packages: ['cockpit-pcp']
# Install cockpit with webserver (not recommended per default!)
cockpit_with_webserver: False
cockpit_packages_web: ['cockpit-ws', 'cockpit-dashboard']
```

## Example Playbook

Simple Example: Without webserver, so you can access it from another instance

```
- hosts: servers
  roles:
    - { role: while-true-do.cockpit }
```

Advanced Example: To install cockpit including cockpit-ws

```
- hosts: servers
  roles:
  - { role: while-true-do.cockpit, cockpit_packages: [ 'cockpit' ] }
```

## License

This work is licensed under a [BSD License](https://opensource.org/licenses/BSD-3-Clause).

## Contribute / Bugs

**bug reports:** <https://github.com/while-true-do/ansible-role-cockpit/issues>

**contributers:** <https://github.com/while-true-do/ansible-role-cockpit/graphs/contributors>

## Author Information

**blog:** <https://blog.while-true-do.org>

**github:** <https://github.com/daniel-wtd>

**contact:** [mail@while-true-do.org](mailto:mail@while-true-do.org)
