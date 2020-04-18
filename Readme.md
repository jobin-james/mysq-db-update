## Role for changing mysql DB parameters

Note: Ansible mysql module doesn't support changing character set once the db is created. So using shell script to achieve this.

### Required Variables

mysql_db_type_aurora must be `true`(if it is aurora db) or `false`(if it is Percona/mysql db)

```bash
vault_mysql_login_host: []
vault_mysql_login_user: []
vault_mysql_login_password: []
mysql_db_name: [] //database name
mysql_character_set: "utf8mb4"
mysql_collation: "utf8mb4_unicode_ci"
```

Script will be removed at the end of play as it contain DB credentils

Eg: create a playbook `mysql-update.yml` 

```yml
---
- hosts: mysql
  gather_facts: false
  role:
    - mysql-db-update
```
```yml
ansible-playbook -i <inventory file> mysql-update.yml -e mysql_db_type_aurora=true