[![Build Status](https://travis-ci.org/while-true-do/ansible-role-cockpit.svg?branch=master)](https://travis-ci.org/while-true-do/ansible-role-cockpit)

# Ansible Role: cockpit
| A role to install and configure [cockpit project](http://cockpit-project.org) packages.

## Motivation

[Cockpit](http://cockpit-project.org) is a quite new, but very interesting management tool for Linux servers. It does provide an overview of different metrics and allows management for several features. In combination with other tools, it will become even better. Gathering diagnostics, Reviewing selinux alerts, Restarts, Updates and more can be done with Cockpit.

## Installation

Install from [Ansible Galaxy](https://galaxy.ansible.com/while-true-do/cockpit)

```
ansible-galaxy install while-true-do.cockpit
```

Install from [Github](https://github.com/while-true-do/ansible-role-cockpit)

```
git clone https://github.com/while-true-do/ansible-role-cockpit.git while-true-do.cockpit
```

## Requirements

**Used Modules**

-   [systemd_module](http://docs.ansible.com/ansible/latest/systemd_module.html)
-   [template_module](http://docs.ansible.com/ansible/latest/template_module.html)
-   [package_module](http://docs.ansible.com/ansible/latest/package_module.html)
-   [include_module](http://docs.ansible.com/ansible/latest/include_module.html)
-   [file_module](http://docs.ansible.com/ansible/latest/file_module.html)
-   [seport_module](http://docs.ansible.com/ansible/latest/seport_module.html)

## Dependencies

This role depends on some roles conditionally:

-   <https://galaxy.ansible.com/while-true-do/docker>
-   <https://galaxy.ansible.com/while-true-do/pcp>
-   <https://galaxy.ansible.com/while-true-do/selinux>

You can install all of them:

```
ansible-galaxy install -r requirements.yml
```

And afterwards, you can use/not use the features.

## Role Variables

```yaml
# defaults/main.yml

# You can enable or disable some features with the "state: [present|absent]":
#   present      - Install the feature + depending roles.
#   absent       - Not install / remove the packages.
#
# For some features, additional roles are needed. Please have a look at the dependencies.
# 
wtd_cockpit_base_state: 'present'
wtd_cockpit_base_packages:
  - 'cockpit-system'
  - 'cockpit-networkmanager'
  - 'cockpit-packagekit'
  - 'cockpit-storaged'
  - 'cockpit-sosreport'

# Depends on while-true-do.docker
wtd_cockpit_docker_state: 'absent'
wtd_cockpit_docker_packages: 'cockpit-docker'

# Depends on while-true-do.pcp
wtd_cockpit_pcp_state: 'present'
wtd_cockpit_pcp_packages: 'cockpit-pcp'

# Depends on while-true-do.selinux
wtd_cockpit_selinux_state: 'present'
wtd_cockpit_selinux_packages:
  - 'cockpit-selinux'
  - 'setroubleshoot-server'

# Cockpit Webserver
wtd_cockpit_webserver_state: 'absent'
wtd_cockpit_webserver_packages:
  - 'cockpit'
  - 'cockpit-ws'
  - 'cockpit-dashboard'

# See here: http://cockpit-project.org/guide/latest/listen.html#listen-systemd
wtd_cockpit_webserver_service: 'cockpit.socket'
wtd_cockpit_webserver_ListenStream: ''   # Defaults to 9090

# See here: http://cockpit-project.org/guide/latest/cockpit.conf.5.html
wtd_cockpit_webserver_Origins: ''
wtd_cockpit_webserver_ProtocolHeader: ''
wtd_cockpit_webserver_LoginTo: ''
wtd_cockpit_webserver_LoginTitle: ''
wtd_cockpit_webserver_RequireHost: ''
wtd_cockpit_webserver_MaxStartups: '3'
wtd_cockpit_webserver_AllowUnencrypted: ''
wtd_cockpit_webserver_UrlRoot: ''

# See here: http://cockpit-project.org/guide/latest/cockpit-ws.8.html
wtd_cockpit_webserver_cert: '
```

```yaml
# vars/{{ ansible_distribution }}.yml
These files are containing package names for the supported distributions.
```

## Example Playbook

Simple Example: Without Webserver, so you can access it from another instance

```
- hosts: servers
  roles:
    - { role: while-true-do.cockpit }
```

## Testing

All tests should be put in [test directory](./tests/).

## Contribute / Bugs

Thank you so much for considering to contribute. Every contribution helps us.
We are really happy, when somebody is joining the hard work. Please have a look
at the links first.

-   [Contribution Guidelines](./docs/CONTRIBUTING.md)
-   [Create an issue or Request](https://github.com/while-true-do/ansible-role-cockpit/issues)
-   [See who was contributing already](https://github.com/while-true-do/ansible-role-cockpit/graphs/contributors)

## License

This work is licensed under a [BSD License](https://opensource.org/licenses/BSD-3-Clause).

## Author Information

Blog: [blog.while-true-do.org](https://blog.while-true-do.org)

Mail: [hello@while-true-do.org](mailto:hello@while-true-do.org)
