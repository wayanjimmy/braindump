+++
title = "Dockerize Golang App"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Golang]({{<relref "20201205165502-golang.md#" >}}) [Docker]({{<relref "20210518095808-docker.md#" >}})


## Example {#example}

Create a docker file, `Dockerfile.local`

```dockerfile
FROM golang:1.13-alpine AS build
RUN go env -w GOPRIVATE=github.com/OkadocTech/*

ARG GITHUB_USERNAME=username
ARG GITHUB_TOKEN=password

RUN apk update && apk add --no-cache git
RUN git config --global url."https://$GITHUB_USERNAME:$GITHUB_TOKEN@github.com".insteadOf "https://github.com"

WORKDIR /build
COPY . .
RUN go build -o app

FROM alpine:latest AS final

COPY --from=build /build/keys /keys
COPY --from=build /build/app /app

ENTRYPOINT ["/app"]
```

Build the docker image using this command

```bash
docker build -f Dockerfile.local --build-arg GITHUB_USERNAME=wayanjimmy --build-arg GITHUB_TOKEN=token -t wayanjimmy/reponame:latest .
```


## Resources {#resources}

-   [Fix go get private repo return error](https://medium.com/easyread/today-i-learned-fix-go-get-private-repository-return-error-terminal-prompts-disabled-8c5549d89045)
-   [Docker compose demo by imrenagi](https://github.com/imrenagi/docker-compose-demo)
