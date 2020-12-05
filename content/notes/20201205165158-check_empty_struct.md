+++
title = "Check Empty Struct"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Golang]({{< relref "20201205165502-golang" >}})

Cara mengecek apakah struct di golang empty atau engga dengan reflect package

```go
type Person struct {
	Name string
}

jimmy := Person{}

if reflect.valueOf(jimmy).IsZero() {
	// struct is empty
}
```
