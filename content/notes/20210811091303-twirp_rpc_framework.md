+++
title = "Twirp RPC Framework"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Tinkering]({{< relref "20210503100841-tinkering" >}}) [Golang]({{< relref "20201205165502-golang" >}})

link
: [Twirp Github](https://github.com/twitchtv/twirp) [Twirpee RPC Proof of Concept](https://github.com/wayanjimmy/twirpee)


## Goals {#goals}

-   [ ] Create 2 server that communicate each other
-   [ ] Create a client implementation using Javascript/Typescript


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

-   Use `protos.NewAServiceJSONClient` instead of the Protobuf Client for easier debugging when using HTTP Proxy. Read [here]({{< relref "20201205165949-attach_proxy_to_http_client" >}}) for details on how to setup http proxy to golang http client.
-   `http://localhost:8899` is the address of the proxy port, in this case I'm using [Whistle](https://github.com/avwo/whistle)

<!--listend-->

```go
func main() {
        // Set a http proxy to the http client
        // for easier debugging
        proxyURL, _ := url.Parse("http://localhost:8899")

        httpClient := &http.Client{
                Transport: &http.Transport{
                        Proxy: http.ProxyURL(proxyURL),
                },
        }

        // Use JSON client for enabling http proxy
        client := protos.NewAServiceJSONClient("http://localhost:8080", httpClient)

        resp, err := client.CallServiceA(context.Background(), &protos.GetServiceARequest{})
        if err != nil {
                log.Fatal(err)
        }

        for _, r := range resp.Responses {
                fmt.Printf("%s:%s\n", r.ServiceName, r.Status)
        }
}
```


## Client Implementation in Javascript/Typescript {#client-implementation-in-javascript-typescript}


### Generate the Typescript Generated based on the provided protos {#generate-the-typescript-generated-based-on-the-provided-protos}

-   Initialize the project with package.json

    ```bash
    npm init -y
    ```

-   Install [twirp-ts](https://github.com/hopin-team/twirp-ts) and [ts-proto](https://github.com/stephenh/ts-proto) (as peer dependency)

    ```bash
    npm i twirp-ts @protobuf-ts/plugin@next -S
    npm i ts-proto -S
    ```

-   Execute `generate.sh` in the root of the project

    ```bash
    mkdir generated
    bash generate.sh
    ```

    The script content was taken from this project

    ```bash
    PROTOC_GEN_TWIRP_BIN="./node_modules/.bin/protoc-gen-twirp_ts"
    PROTOC_GEN_TS_BIN="./node_modules/.bin/protoc-gen-ts_proto"

    OUT_DIR="./generated"

    protoc \
        -I ./srva/protos \
        --plugin=protoc-gen-ts_proto=${PROTOC_GEN_TS_BIN} \
        --plugin=protoc-gen-twirp_ts=${PROTOC_GEN_TWIRP_BIN} \
        --ts_proto_opt=esModuleInterop=true \
        --ts_proto_opt=outputClientImpl=false \
        --ts_proto_out=${OUT_DIR} \
        --twirp_ts_opt="ts_proto" \
        --twirp_ts_out=${OUT_DIR} \
        ./srva/protos/*.proto
    ```

    It will generate the typescript code, now our code tree will look like this

    ```nil
    ├── generated
    │   ├── service.ts
    │   └── service.twirp.ts
    ├── generate.sh
    ├── go.mod
    ├── go.sum
    ├── package.json
    ├── package-lock.json
    ├── README.md
    ├── srva
    │   ├── main.go
    │   └── protos
    │       ├── service.pb.go
    │       ├── service.proto
    │       └── service.twirp.go
    ├── srvb
    │   └── main.go
    └── tools.go

    4 directories, 14 files
    ```


### Scaffold a next.js project with typescript {#scaffold-a-next-dot-js-project-with-typescript}

Create a new next.js project in the root project, I use webui as the name of the project

```bash
npx create-next-app --ts
```

move the generated typescript to the nextjs project, and move the project files into src directory

```bash
mv generated webui/src
```

Now our project structure will look like this

```nil
├── generate.sh
├── go.mod
├── go.sum
├── package.json
├── package-lock.json
├── README.md
├── srva
│   ├── main.go
│   └── protos
│       ├── service.pb.go
│       ├── service.proto
│       └── service.twirp.go
├── srvb
│   └── main.go
├── tools.go
└── webui
    ├── next.config.js
    ├── next-env.d.ts
    ├── package.json
    ├── public
    │   ├── favicon.ico
    │   └── vercel.svg
    ├── README.md
    ├── src
    │   ├── generated
    │   │   ├── service.ts
    │   │   └── service.twirp.ts
    │   ├── pages
    │   │   ├── api
    │   │   │   └── hello.ts
    │   │   ├── _app.tsx
    │   │   └── index.tsx
    │   └── styles
    │       ├── globals.css
    │       └── Home.module.css
    ├── tsconfig.json
    └── yarn.lock

10 directories, 27 files
```

Try to fetch data from the next.js to srva service

```javascript
import axios from "axios";

import { AServiceClientJSON } from "../generated/service.twirp";

import styles from "../styles/Home.module.css";

const client = axios.create({
  baseURL: "http://localhost:8080/twirp",
});

const implementation = {
  request(service, method, contentType, data) {
    return client
      .post(`${service}/${method}`, data, {
        responseType:
          contentType === "application/protobuf" ? "arraybuffer" : "json",
        headers: {
          "content-type": contentType,
        },
      })
      .then((response) => {
        return response.data;
      });
  },
};

const jsonClient = new AServiceClientJSON(implementation);
```

Invoke the fetch data on component mount using useEffect

```javascript
useEffect(() => {
  console.log("did mount");

  async function getServiceARequest() {
    let req = {
      count: 10,
    };

    try {
      const res = await jsonClient.CallServiceA(req);
      console.log(res);
    } catch (err) {}
  }

  getServiceARequest();
}, []);
```

If there is a CORS related error when fetching data make sure we added cors handler to the srva's http handler

```go
func corsMiddleware(h http.HandlerFunc) http.HandlerFunc {
        return func(rw http.ResponseWriter, r *http.Request) {
                rw.Header().Set("Access-Control-Allow-Origin", "*")
                rw.Header().Set("Access-Control-Allow-Methods", "OPTIONS, GET, POST, PUT")
                rw.Header().Set("Access-Control-Allow-Headers", "Content-Type, X-CSRF-Token")

                if r.Method == "OPTIONS" {
                        rw.Write([]byte("allowed"))
                        return
                }

                h(rw, r)
        }
}

func main() {
        // TODO: Try another mux, such as labstack's echo

        twirpHandler := protos.NewAServiceServer(&Server{})

        mux := http.NewServeMux()

        mux.HandleFunc(twirpHandler.PathPrefix(), corsMiddleware(twirpHandler.ServeHTTP))

        http.ListenAndServe(":8080", mux)
}
```


## Retro {#retro}


### Pros {#pros}

-   We can implement contract driven development
-   Generated code for web client
-   JSON client make it easier for debugging
-   I'm thinking of this as an alternative of GraphQL and REST API


### Cons {#cons}

-   Not sure how to implement this with multiple repository project. Should we place the protos in a single project/module?


## What next? {#what-next}

-   Generate documentation using open api, see [here](https://github.com/kyawmyintthein/twirp-grpc-envoy-poc/blob/main/doc%5Fgen.sh).
