lvm
==========
- [Introduction](#introduction)
- [Requirements](#requirements)
- [Variables](#variables)
- [Usage](#usage)

# Introduction
Manage logical volumes

# Requirements
- Ansible >= 2.0

# Variables
| Name | Description | Default |
|:-----|:------------|:--------|
| lvm_package_name | Package name | depends on __ansible_os_family__ and __ansible_distribution_major_version__ |
| lvm_package_state | Package state | present |
| lvm_volume_groups | List of volume groups to ensure | [] |
| lvm_logical_volumes | List of volumes definitions to ensure | [] |

# Usage
Ensure volume group _datavg_ exists and located on device _/dev/sdb_, and a logical volume named _docker_ with a size of 32G.
In addition make sure that the volume is formated as _btrfs_ filesystem and is mounted in _/var/lib/docker_.

```yaml
---
- hosts: servers
  vars:
    lvm_volume_groups:
    - vg: datavg
      pvs: /dev/sdb
    lvm_logical_volumes:
    - vg: datavg
      name: docker
      size: 32G
      fstype: btrfs
      mount_point: /var/lib/docker
  roles:
  - role: lvm
```
