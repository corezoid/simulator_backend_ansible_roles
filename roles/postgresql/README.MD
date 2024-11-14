#Role Description

The role installs postgressql on Ubuntu servers

#####role supports variables (example in box.yaml)
```
top_db_dir: "/postgresqldata"

db_dir: "{{ top_db_dir }}/pgsql"

default_config_postgresql: true

db_version: "16"

replica: true

master_port: 5432

master_ip: 10.60.101.129

replica_ip: 10.60.101.140 
```
#### for proper installation you need
1. If a replica is not needed, then `set replica: false` and `set ansible-playbook --diff -i hosts cz-init.yaml`
2. if a replica is needed, then enter the IP servers of the master and replica and run 1 time on the master `ansible-playbook --diff -i hosts cz-init.yaml --tags=install-master`
   after installation, run 2 times on the replica `ansible-playbook --diff -i hosts cz-init.yaml --tags=install-replica`