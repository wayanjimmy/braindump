+++
title = "Attach proxy to HTTP client"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Golang]({{< relref "20201205165502-golang" >}}) [Menggunakan Proxy Tool untuk Debugging]({{< relref "20201203183009-menggunakan_proxy_tool_untuk_debugging" >}})

link
: [Setting up proxy for HTTP client](https://stackoverflow.com/questions/14661511/setting-up-proxy-for-http-client) [ProxyFromEnvironment](https://pkg.go.dev/net/http#ProxyFromEnvironment)


## Attach proxy to HTTP Client {#attach-proxy-to-http-client}

Construct a http client with a proxy

```go
proxyURL, _ := url.Parse("http://proxyIp:proxyPort")

myClient := &http.Client{Transport: &http.Transport{Proxy: http.ProxyURL(proxyURL)}}
```

We could also modify the default transport used by the `net/http` package. This would affect the entire program.

```go
proxyURL, _ := url.Parse("http://proxyIp:proxyPort")

http.DefaultTransport := &http.Transport{Proxy: http.ProxyURL(proxyURL)}
```
