+++
title = "Provide env for docker container using a file"
author = ["Wayanjimmy"]
draft = false
+++

link
: [Docker ARG, ENV and .env - a Complete Guide](https://vsupalov.com/docker-arg-env-variable-guide/)

related
: [Docker]({{<relref "20210518095808-docker.md#" >}}) [Podman]({{<relref "20210717001214-podman.md#" >}})


## Take values from a file (env\_file) {#take-values-from-a-file--env-file}

```sh
docker run --env-file=env_file_name alpine env
```


## Example using Podman {#example-using-podman}

```sh
podman container run --pod <pod_name> --env-file=../.env alpine:latest
```
