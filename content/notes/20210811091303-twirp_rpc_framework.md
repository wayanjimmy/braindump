+++
title = "Twirp RPC Framework"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Tinkering]({{< relref "20210503100841-tinkering" >}}) [Golang]({{< relref "20201205165502-golang" >}})

link
: [Twirp Github](https://github.com/twitchtv/twirp)


## How to install Twirp? {#how-to-install-twirp}

Install Protocol Buffer compiler, `protoc` version 3. For installation, see [Protocol Buffer Compiler Installation](https://grpc.io/docs/protoc-installation/).

For ubuntu linux.

```bash
sudo apt install -y protobuf-compiler
protoc --version #Ensure compiler version is 3+
```


### Create a new project using go modules {#create-a-new-project-using-go-modules}

```bash
mkdir -p projects/twirpee
cd projects/twirpee
go mod init github.com/wayanjimmy/twirpee
```


### Define tools.go for versioning in go.mod {#define-tools-dot-go-for-versioning-in-go-dot-mod}

```go
// +build tools

package tools

import (
        _ "google.golang.org/protobuf/cmd/protoc-gen-go"
        _ "github.com/twitchtv/twirp/protoc-gen-twirp"
)
```


### Install the generators {#install-the-generators}

Execute these commands inside the project go modules.

```bash
go get github.com/twitchtv/twirp/protoc-gen-twirp
go get google.golang.org/protobuf/cmd/protoc-gen-go
```


### Verify our modules reflects the dependency {#verify-our-modules-reflects-the-dependency}

```bash
go list -m all
```

output

```txt
github.com/wayanjimmy/twirpee
github.com/golang/protobuf v1.5.0
github.com/google/go-cmp v0.5.5
github.com/pkg/errors v0.9.1
github.com/twitchtv/twirp v8.1.0+incompatible
golang.org/x/xerrors v0.0.0-20191204190536-9bdfabe68543
google.golang.org/protobuf v1.27.1
```


## Server Implementation in Golang {#server-implementation-in-golang}


### Write a Protobuf service definition {#write-a-protobuf-service-definition}

Create a package for storing the proto service definition

```bash
mkdir srva/protos
touch srva/protos/service.proto
```

service.proto content

```proto
syntax = "proto3";

package srva.protos;

option go_package = "srva/protos";

service AService {
rpc CallServiceA(GetServiceARequest) returns (GetServiceAResponse);
}

message GetServiceARequest {
int64 count = 1;
}

message GetServiceAResponse {
repeated ServiceAResponse responses = 1;
}

message ServiceAResponse {
string service_name = 1;
string status = 2;
}
```


### Generate code {#generate-code}

Execute this command in the root of the go modules.

```bash
protoc --twirp_out=. --go_out=. srva/protos/service.proto
```

The code should be generated in the same directory as the `.proto` files.

```nil
├── go.mod
├── go.sum
├── srva
│   ├── main.go
│   └── protos
│       ├── service.pb.go
│       ├── service.proto
│       └── service.twirp.go
└── tools.go

2 directories, 7 files
```


### Implement the server {#implement-the-server}

```go
package main

import (
	"context"
	"fmt"

	"github.com/wayanjimmy/twirpee/srva/protos"
)

type Server struct{}

var _ protos.AService = (*Server)(nil)

func (s *Server) CallServiceA(ctx context.Context, req *protos.GetServiceARequest) (*protos.GetServiceAResponse, error) {
	var (
		resp protos.GetServiceAResponse
		err  error
	)

	var responses []*protos.ServiceAResponse

	for i := 0; i < 10; i++ {
		responses = append(responses, &protos.ServiceAResponse{
			ServiceName: "A",
			Status:      "OK",
		})
	}

	resp.Responses = responses

	return &resp, err
}

func main() {
	fmt.Println("vim-go")
}
```


### Mount and run the server {#mount-and-run-the-server}

On `srva/main.go`

```go
func main() {
        // TODO: Try another mux, such as labstack's echo

        twirpHandler := protos.NewAServiceServer(&Server{})

        mux := http.NewServeMux()

        mux.Handle(twirpHandler.PathPrefix(), twirpHandler)

        http.ListenAndServe(":8080", mux)
}
```


## Client Implementation in Golang {#client-implementation-in-golang}

On `srvb/main.go`

```go

```


## Client Implementation in Javascript/Typescript {#client-implementation-in-javascript-typescript}


## Create a Proof of Concept {#create-a-proof-of-concept}

-   [ ] Create 2 server that communicate each other
-   [ ] One of the server has Javascript/Typescript client implementation


## Retro {#retro}


### Pros {#pros}


### Cons {#cons}
