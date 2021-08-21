+++
title = "Assignment: DNS Round Robin Test"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Docker Mastery]({{<relref "20210815122912-docker_mastery.md#" >}})


## Assignment {#assignment}

-   Ever since Docker Engine 1.11, we can have multiple containers on a created network respond to the same DNS address
-   Create a new virtual network (default bridge driver)
-   Create two containers from `elasticsearch:2` image
-   Research and use `--network-alias search` when creating them to give them an additional DNS name to respond to
-   Run `alpine nslookup search` with `--net` to see the two containers list for the same DNS name
-   Run `centos curl -s search:9200` with `--net` multiple times until you see both "name" fields show


## Answer {#answer}

Create the network

```bash
docker network create dude
```

Create 2 elastic search containers

```bash
docker container run --rm -d --net dude --net-alias search elasticsearch:2
```

run it 2 times, so we have 2 containers running in the background

```bash
docker container ls
```

Check using nslookup

```bash
docker container run --rm -it --net dude alpine nslookup search
```

We can see that there is 2 dns

Check using curl

```bash
docker container run --rm -it --net dude centos curl search:9200
```

run it multiple times, you can see there are 2 instances of elasticseach that give you response

Here is the asciinema [record](https://asciinema.org/a/FFAiX40A5CbgPT54BIHe8Rr4y).
