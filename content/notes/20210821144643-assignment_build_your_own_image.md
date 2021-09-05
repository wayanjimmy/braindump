+++
title = "Assignment: Build Your Own Image"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Docker Mastery]({{<relref "20210815122912-docker_mastery.md#" >}})


## Assignment {#assignment}

-   Take existing [Golang]({{<relref "20201205165502-golang.md#" >}}) app and Dockerize it
-   Make `Dockerfile`. Build it. Test it. Push it. (rm it). Run it.
-   Expect this to be iterative. Rarely do I get it right the first time.
-   Use the alpine image.


## Answer {#answer}

In this case I'm using [Podman]({{<relref "20210717001214-podman.md#" >}}), instead of [Docker]({{<relref "20210518095808-docker.md#" >}}) for the sake of learning.


### Clone my personal project yulje {#clone-my-personal-project-yulje}

```sh
git clone git@github.com:wayanjimmy/yulje.git
```


### Write Containerfile {#write-containerfile}

Write `build.sh` script for injecting version for variable at build time.

```bash
GIT_COMMIT=$(git rev-list -1 main)
go build -ldflags "-X main.GitCommit=$GIT_COMMIT" -o app yulje/cmd/yulje
```

Integrate `build.sh` to Containerfile

```Dockerfile
FROM docker.io/golang:1.16-alpine AS build

RUN apk update && apk add --no-cache git

WORKDIR /build

COPY .git .
COPY . .

RUN sh build.sh

FROM docker.io/alpine:latest AS final

COPY --from=build /build/app /app

ENTRYPOINT ["/app"]
```


### Build the container {#build-the-container}

```sh
podman build -t wayanjimmy/yulje:latest .
```


### Create a pod {#create-a-pod}

Since the web server on the project [yulje](https://github.com/wayanjimmy/yulje) exposing port 8080, I need to publish the port.

```sh
podman pod create -p 8080:8080
```


### Run the container inside the pod {#run-the-container-inside-the-pod}

Run with detached mode

```sh
podman run -d -e DATABASE_URL=mysql://user:password@host:port/database_name -d --pod pod_name wayanjimmy/yulje:latest
```
