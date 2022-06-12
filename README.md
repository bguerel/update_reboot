![Header](https://raw.githubusercontent.com/bguerel/update_reboot/main/update_reboot.png "Header")

[![Open Source Love](https://badges.frapsoft.com/os/v3/open-source.png?v=103)](https://opensource.org/licenses/OSL-3.0)
[![Author](https://img.shields.io/badge/Powered%20by-Benhur%20Gürel-blue)](https://github.com/bguerel/bguerel)
[![CI](https://github.com/bguerel/update_reboot/workflows/CI/badge.svg?branch=main&event=push)](https://github.com/bguerel/update_reboot/actions?query=workflow%3ACI)
[![Ansible Galaxy Downloads](https://img.shields.io/ansible/role/d/53007?color=blue&label=Galaxy%20Downloads&logo=Ansible)](https://galaxy.ansible.com/bguerel/update_reboot)
[![Version](https://img.shields.io/github/v/release/bguerel/update_reboot?label=update_reboot&logo=Ansible)](https://github.com/bguerel/update_reboot/releases)

**Note:** A simple update and reboot role with checking if a reboot is required!
Although a reboot is required, you can prevent certain nodes from rebooting by using --extra-vars.

```yaml
-e 'update_reboot_required_enable=false'
```

Requirements
------------

- [x] Ansible version >= 2.9

Dependencies
------------

- [x] needs-restarting (EL/Fedora)
- [x] needrestart (Debian/Ubuntu)
- [x] none (Suse)

Installation
------------

- [x] git

Use `git@github.com:bguerel/update_reboot.git` to pull the latest edge commit of the role from git.

Platforms
---------

```yaml
EL:
  versions:
    - 8
    - 7
Fedora:
  versions:
    - all
Debian:
  versions:
    - Bullseye
    - Buster
    - Stretch
Ubuntu:
  versions:
    - Focal
    - Bionic
SLES:
  versions:
    - 15
    - 12
OpenSUSE:
  version:
    - all
```

Role Variables
--------------

The descriptions and default settings for all variables can be found in the **`defaults/main.yml`** directory in the following file:

- **[defaults/main.yml](./defaults/main.yml)**

## Example

### Configuration

```yaml
# Install dependencies
update_reboot_install_pkgs: true

# Enable the logging of installation packages.
update_reboot_log_enable: true

# Directory for log files.
update_reboot_log_directory: $HOME/.ansible/logs/UPDATE

# Enable the required reboot check after the update.
update_reboot_required_enable: true

# Maximum seconds to wait for a successful connection to the managed hosts before trying again.
update_reboot_connect_timeout: 5

# Maximum seconds to wait for machine to reboot and respond to a test command.
update_reboot_timeout: 7200

# Seconds to wait after the reboot command was successful before attempting to validate the system rebooted successfully.
update_reboot_post_delay: 10

# Seconds to wait before reboot.
update_reboot_pre_delay: 5

# Command to run on the rebooted host and expect success from to determine the machine is ready for further tasks.
update_reboot_test_command: "uptime"

# .:EXCLUDE-PACKAGES:.

# Exclude packages on certain nodes from update. (RedHat)
update_reboot_redhat_exclude_pkgs:
  example-redhat-01v:
    - nginx
    - mariadb-server
    - php-fpm

# Exclude packages on certain nodes from update. (Debian)
update_reboot_debian_exclude_pkgs: []

# Exclude packages on certain nodes from update. (Suse)
update_reboot_suse_exclude_pkgs: []
```

### Playbook

Use it in a playbook as follows:

```yaml
- hosts: whatever
  become: yes
  roles:
    - update_reboot
```

License
-------

[![MIT license](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)