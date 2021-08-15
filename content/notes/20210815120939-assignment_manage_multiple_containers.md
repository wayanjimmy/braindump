+++
title = "Assignment: Manage Multiple Containers"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Docker Mastery]({{< relref "20210815122912-docker_mastery" >}})


## Assignment {#assignment}

1.  Run a `nginx`, a `mysql`, and a `httpd` (apache) server
2.  Run all of them `--detach` (or `-d`), name them with `--name`
3.  `nginx` should listen on `80:80`, httpd on `8080:80`, mysql on `3306:3306`
4.  When running `mysql`, use the `--env` option (or `-e`) to pass in `MYSQL_RANDOM_ROOT_PASSWORD=yes`
5.  Use `docker container logs` on mysql to find the random password it created on startup
6.  Clean it all up with docker container stop and docker container rm (both can accept multiple names or ID's)
7.  Use `docker container ls` to ensure everything is correct before and after


## Answers {#answers}

```bash
# Run nginx container
docker container run --name nginx -p 80:80 -d nginx

# Run mysql container
docker container run --name mysql -p 3306:3306 -e MYSQL_RANDOM_ROOT_PASSWORD=yes -d mysql

# Run httpd container
docker container run --name httpd -p 8080:80 -d httpd
```

Retrieve the mysql's random root password

```bash
docker container logs mysql | grep "ROOT PASSWORD"
```

Check containers status

```bash
docker container ls
```

Stop all running containers

```bash
docker container stop nginx mysql httpd
```

Remove containers

```bash
docker container rm nginx mysql httpd
```
