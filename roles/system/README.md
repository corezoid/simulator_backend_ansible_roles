# Ansible System Role

This Ansible role performs basic system configuration and optimization for Linux servers, focusing on performance tuning and administrative convenience. It's designed to establish a solid foundation for servers that will run various workloads.

## Features

- System information display
- Hostname configuration
- Firewall management (iptables)
- Kernel parameter optimization for performance
- Root user shell customization
- System limits configuration for high performance
- Essential administrative tools installation

## Requirements

- Ansible 2.13.5 
- Target systems running Debian/Ubuntu

## Role Variables

| Variable | Description | Default | Required |
|----------|-------------|---------|----------|
| `hostname` | Hostname to set on the target system | undefined | No |
| `iptables_status` | Whether to enable iptables (true) or disable it (false) | undefined | No |


## Example Playbook

```yaml
- hosts: servers
  become: yes
  vars:
    hostname: "app-server-01"
    iptables_status: false
  roles:
    - system
```

## Optimizations Applied

### Kernel Parameters

The role applies the following kernel parameter optimizations:

| Parameter | Value | Purpose |
|-----------|-------|---------|
| vm.swappiness | 1 | Minimizes swap usage, improving performance for most applications |
| net.ipv4.tcp_tw_reuse | 1 | Allows reuse of TIME_WAIT sockets for new connections |
| net.ipv4.tcp_fin_timeout | 10 | Reduces connection closing wait time |
| net.core.somaxconn | 4096 | Increases maximum connection queue size |
| net.ipv4.tcp_max_syn_backlog | 8192 | Increases buffer for incoming connections |
| net.ipv4.ip_local_port_range | 10000 65000 | Expands local port range, allowing more concurrent connections |

### System Limits

The role sets the following system limits:

| Limit | Value | Purpose |
|-------|-------|---------|
| nofile | 512000 | Maximum number of open files, essential for high-traffic services |
| nproc | 64000 | Maximum number of processes, necessary for busy servers |

## Administrative Tools

The role installs a set of tools for system administration and monitoring:

| Tool | Purpose |
|------|---------|
| mc | Midnight Commander - file manager |
| iotop | I/O usage monitoring by processes |
| iftop | Network traffic monitoring |
| wget | Utility for downloading files |
| deltarpm | Optimization for RPM package updates |
| lsof | Information about open files |
| screen | Terminal session manager |
| finger | Information about system users |
| mlocate | Fast file search |
| ncdu | Disk space usage analyzer |
| netcat | Network utility for working with TCP/UDP |
| mtr | Network diagnostic tool |
| tcpdump | Network traffic analyzer |
| pigz | Parallel implementation of gzip |
| ngrep | Network grep for packet monitoring |
| net-tools | Classic network tools (ifconfig, netstat, etc.) |

## Shell Customization

The role improves the root user's shell experience with:

1. Custom prompt (PS1) displaying:
    - Current time
    - Timezone
    - Username and hostname (in purple)
    - Current working directory

2. Grep enhancements:
    - Automatic color highlighting
    - Purple highlighting for matches

## Tags

The role uses the following tags for selective execution:

| Tag | Purpose |
|-----|---------|
| system-all | All system tasks |
| system-info | System information display |
| system-set-hostname | Hostname configuration |
| system-iptables-action | Firewall management |
| system-change-sysctl | Kernel parameter optimization |
| system-change-limits-conf | System limits configuration |
| system-rpm | Package installation |

Example of using tags:

```bash
ansible-playbook playbook.yml --tags "system-info,system-rpm"
```


## Author Information

Created and maintained by Middleware