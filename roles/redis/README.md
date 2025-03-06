# Redis Role

This Ansible role installs and configures Redis for Ubuntu systems with monitoring support via Monit.

## Overview

The role performs the following main functions:
- Installs Redis from the official Redis repository
- Configures Redis with custom settings
- Sets up Redis to start automatically on boot
- Configures Monit for Redis monitoring
- Supports both Ubuntu 22.04 (Jammy) and 24.04 (Noble)

## Requirements

- Ubuntu 22.04 (Jammy Jellyfish) or Ubuntu 24.04 (Noble Numbat)
- Access to the internet to download packages
- Ansible 2.13.5

## Role Variables

### Required Variables box.yml

```yaml
redis_version: "7.4.2"
redis_name: "redis-server"
redis_port: 6379
redis_password: "Eevae0quai7p"
```

## Templates

The role requires the following templates:
- `templates/redis.j2` - Redis configuration file
- `templates/monit.conf.j2` - Main Monit configuration
- `templates/redis.monit.j2` - Monit configuration for Redis monitoring

## Example Playbook

```yaml
- name: Setup backend
  hosts: all
  become: true
  vars_files:
    - vars/box.yml
  roles:
    - redis
```

## Role Structure

```
redis/
├── defaults/
│   └── main.yml          # Default variables
├── handlers/
│   └── main.yml          # Event handlers (restart services)
├── tasks/
│   └── main.yml          # Main tasks
├── templates/
│   ├── redis.j2          # Redis configuration template
│   ├── monit.conf.j2     # Monit main configuration template
│   └── redis.monit.j2    # Redis monitoring configuration
└── README.md             # Role documentation
```

## Tags

You can use the following tags to run specific parts of the role:

- `redis-all` - Run all tasks
- `redis-repo` - Configure Redis repository
- `redis-install` - Just install Redis packages
- `redis-config` - Update Redis configuration
- `redis-service` - Configure and start Redis service
- `redis-monit` - Update Monit configuration

Example:
```
ansible-playbook -i inventory playbook.yml --tags "redis-config"
```

## Handlers

- `restart redis` - Restarts the Redis service when configuration changes
- `restart monit` - Restarts the Monit service when its configuration changes

## Notes

- The role automatically detects your Ubuntu version and applies the appropriate package settings
- Redis will be configured to start automatically on system boot
- Monit will be configured to monitor Redis and restart it if it fails

## Author

Created and maintained by Middleware