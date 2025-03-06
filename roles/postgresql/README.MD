# PostgreSQL Ansible Role

This Ansible role installs and configures PostgreSQL with PostGIS extensions on Ubuntu systems. It supports both single instance and master-replica setups.

## Compatibility

- Ubuntu 22.04 LTS (Jammy Jellyfish)
- Ubuntu 24.04 LTS (Noble Numbat)

## Features

- Installation of PostgreSQL server with configurable version
- PostGIS 3 extension setup
- Custom data directory configuration
- Master-replica replication setup
- Secure repository key handling compatible with modern Ubuntu versions

## Requirements

- Ansible 2.13.5 
- Ubuntu 22.04 or 24.04 target systems
- Sudo privileges on target systems

## Role Variables

```yaml
#Postgres
top_db_dir: "/postgresqldata"
db_dir: "{{ top_db_dir }}/pgsql"
default_config_postgresql: true
replica: false
db_version: "16"
master_port: 5432
#master_ip: 172.19.50.101
#replica_ip: 172.19.50.102

```
## Example Playbook

### Single PostgreSQL Instance

```yaml
- name: Setup backend
  hosts: all
  become: true
  vars_files:
     - vars/box.yml
  roles:
     - postgresql #--tags=install-master for master or  --tags=install-replica for replica
```

## Tags

The role uses the following tags:

- `install-master` - Tasks related to master server installation and configuration
- `install-replica` - Tasks related to replica server installation and configuration

You can use these tags to run specific parts of the role:

1. If a replica is not needed, then `set replica: false` and `set ansible-playbook --diff -i hosts cz-init.yaml`
2. if a replica is needed, then enter the IP servers of the master and replica and run 1 time on the master `ansible-playbook --diff -i hosts cz-init.yaml --tags=install-master`
   after installation, run 2 times on the replica `ansible-playbook --diff -i hosts cz-init.yaml --tags=install-replica`

## Replication Setup

For replication, this role:

1. On the master:
   - Configures WAL (Write-Ahead Logging) for replication
   - Sets up replication slots and connections
   - Updates pg_hba.conf to allow the replica to connect

2. On the replica:
   - Creates a script directory
   - Deploys the initialization script
   - Runs the initialization script to set up the replica

## Handlers

The role includes handlers:

- `restart postgresql` - Restarts the PostgreSQL service after configuration changes

## Author Information

Created and maintained by Middleware

