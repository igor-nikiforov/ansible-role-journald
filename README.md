# Ansible Role: Journald

This role configures Journald parameters on your Linux distribution.

## Requirements

This role developed and tested with following Ansible versions:

| Name                                                   | Version         |
|--------------------------------------------------------|-----------------|
| [ansible](https://pypi.org/project/ansible/)           | ```>= 2.9.7```  |

Other Ansible versions was not tested but will probably work.

## Installation

Use ```ansible-galaxy install igor_nikiforov.journald``` to install the latest stable release of role.

You could also install it from requirements ```ansible-galaxy install -r requirements.yml```:

```yaml
# requirements.yml
---
roles:
  - name: igor_nikiforov.journald
    version: v1.0.0
```

## Usage

Role supports all Journald configuration parameters. Please refer to https://www.freedesktop.org/software/systemd/man/journald.conf.html for all possible parameters.

### Examples

```yaml
# playbook.yml
---
- hosts: all
  become: true
  gather_facts: false

  pre_tasks:
    - wait_for_connection: { timeout: 300 }
    - setup:

  vars:
    journald_config:
      Compress: yes
      ForwardToConsole: no
      ForwardToSyslog: no
      MaxRetentionSec: 1month
      RateLimitBurst: 10000
      RateLimitIntervalSec: 30s
      Storage: persistent
      SyncIntervalSec: 1s
      SystemMaxUse: 8g
      SystemKeepFree: 20%
      SystemMaxFileSize: 10M

  tasks:
    - name: Configure journald parameters
      import_role:
        name: journald
```

## License

MIT

## Author Information

[Igor Nikiforov](https://github.com/igor-nikiforov)
