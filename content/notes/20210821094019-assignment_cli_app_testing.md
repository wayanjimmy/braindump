+++
title = "Assignment: CLI App Testing"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Docker Mastery]({{<relref "20210815122912-docker_mastery.md#" >}})


## Assignment {#assignment}

-   Use different Linux distro containers to check `curl` cli tool version
-   Use two different terminal windows to start bash in both `centos:7` and `ubuntu:14.04`, using `-it`
-   Learn the `docker container --rm` option so you can save cleanup
-   Ensure `curl` is installed and on latest version for that distro
    -   ubuntu: `apt-get update && apt-get install curl`
    -   centos: `yum update curl`


## Answer {#answer}

Run a docker container and get into the shell

```bash
docker container run --rm -it ubuntu:14.04
```

Inside the docker container

```bash
apt-get update && apt-get install curl
```

```bash
curl --version
```

asciiname record [here](https://asciinema.org/a/431480).

In `centos:7`

```bash
docker container run --rm -it centos:7
```

```bash
curl --version
```

in this case, curl was installed by default in `centos`

```bash
yum update curl
```

The one already installed was already the latest version of `curl`, because before and after update the version number still the same.

See asciinema record [here](https://asciinema.org/a/431481).
