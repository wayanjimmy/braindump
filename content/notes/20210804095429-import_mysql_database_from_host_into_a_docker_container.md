+++
title = "Import Mysql database from host into a docker container"
author = ["Wayanjimmy"]
draft = false
+++

-   related:: [MySQL]({{< relref "20210415133341-mysql" >}}) [Docker]({{< relref "20210518095808-docker" >}})


## Importing database {#importing-database}

```bash
docker exec -i {container_name} mysql -u{username} -p{password} {db_name} < {filename}.sql
```


## Troubleshooting {#troubleshooting}


### Connection reset by peer {#connection-reset-by-peer}

> ERROR 2006 (HY000) : MySQL server has gone away
> read unix @->/var/run/docker.sock: read: connection reset by peer

there is a possibility the error above caused by too large file, try to solve it by manually set the max allowed packet

> MariaDB [(none)]> SET GLOBAL max\_allowed\_packet=1073741824;
> Query OK, 0 rows affected (0.004 sec)

and set the mysql config right from the `docker-compose.yml`

```yaml
db:
  image: mysql:5.7
  volumes:
    - dbdata:/var/lib/mysql
  ports:
    - "3306:3306"
  environment:
    MYSQL_ROOT_PASSWORD: secret
    MYSQL_DATABASE: doctorassist
  command:
    - --wait_timeout=28800
    - --innodb_log_file_size=128M
```
