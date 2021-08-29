+++
title = "Remove ONLY_FULL_GROUP_BY on MySQL"
author = ["Wayanjimmy"]
draft = false
+++

related
: [MySQL]({{< relref "20210415133341-mysql" >}}) [Docker]({{< relref "20210518095808-docker" >}})


## By Query {#by-query}

Connect to mysql shell, you can use tools like mycli for this.

```sql
SET GLOBAL sql_mode=(SELECT REPLACE(@@sql_mode,'ONLY_FULL_GROUP_BY',''));
```


## By Docker Compose {#by-docker-compose}

```yaml
version: "3.7"
services:

  db:
    image: mysql:5.7
    ports:
      - "3306:3306"
    volumes:
      - mysqldata:/var/lib/mysql:delegated
      - "./my.cnf:/etc/mysql/conf.d/mysql.cnf"
    environment:
      - MYSQL_DATABASE=database_name
      - MYSQL_ROOT_PASSWORD=root
```
