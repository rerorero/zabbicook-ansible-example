This is an example to show how to use [Zabbicook](https://github.com/rerorero/zabbicook) with Ansible.

You can easily run a Zabbix server with the [Docker image](https://www.zabbix.org/wiki/Dockerized_Zabbix).

```
docker run \
    -d \
    --name zabbix-db \
    --env="MARIADB_USER=zabbix" \
    --env="MARIADB_PASS=my_password" \
    monitoringartist/zabbix-db-mariadb

docker run \
    -d \
    --name zabbix \
    -p 8080:80 \
    -p 10051:10051 \
    -v /etc/localtime:/etc/localtime:ro \
    --link zabbix-db:zabbix.db \
    --env="ZS_DBHost=zabbix.db" \
    --env="ZS_DBUser=zabbix" \
    --env="ZS_DBPassword=my_password" \
    --env="XXL_zapix=true" \
    --env="XXL_grapher=true" \
    monitoringartist/zabbix-xxl:latest
```

Run the playbook with the Zabbix server running.
```
ansible-playbook playbook.yml
```
