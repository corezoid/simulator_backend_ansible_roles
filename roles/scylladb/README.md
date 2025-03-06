# ScyllaDB Role

This Ansible role installs and configures ScyllaDB on Debian-based systems.

## Overview

The role performs the following main functions:
- Installs ScyllaDB from the official repository (versions 5.4 and 6.2 supported)
- Configures the database with custom settings
- Optimizes system parameters for ScyllaDB operation
- Optionally sets up a dedicated disk for improved performance
- Configures automatic startup on system boot

## Requirements

- Debian-based system Ubuntu(22.04/24.04)
- Access to the internet for package downloads
- Sufficient disk space for database operation
- When using the disk setup feature, an additional disk device is required

## Role Variables

### Required Variables

```yaml
scylla_ver: 6.2
interface: ens160

cluster_name: tbi-prod
master_node: 172.19.50.103 #если 1 нода то комментируем
snitch: SimpleSnitch  # SimpleSnitch - ставим на земле | Ec2Snitch - ставим на AWS
add_disk: false
#device_path: nvme1n1
```

## Templates

The role requires the following templates:
- `templates/scylla.yaml.j2` - Main ScyllaDB configuration

## Example Playbook

```yaml
- name: Setup backend
  hosts: all
  become: true
  vars_files:
    - vars/box.yml
  roles:
    - scylladb
```

## Role Structure

```
scylladb/
├── defaults/
│   └── main.yml          # Default variables
├── handlers/
│   └── main.yml          # Event handlers
├── meta/
│   └── main.yml          # Role metadata
├── tasks/
│   ├── main.yml          # Main tasks
│   └── add_disk.yml      # Second disk setup tasks
├── templates/
│   └── scylla.yaml.j2    # ScyllaDB configuration template
└── README.md             # Role documentation
```

## Tags

You can use the following tags to run specific parts of the role:

- `create-second-disk` - Configure an additional disk for ScyllaDB data

Example:
```
ansible-playbook -i inventory playbook.yml --tags "create-second-disk"
```

## Additional Disk Setup only AWS ec2

When `add_disk` is enabled, the role will:
1. Create a partition on the specified device
2. Format it with ext4 filesystem
3. Safely migrate existing ScyllaDB data
4. Configure the system for automatic mounting on boot
5. Set proper ownership and permissions

The disk setup improves performance by separating database files from the system disk.

## Author

Created and maintained by Middleware