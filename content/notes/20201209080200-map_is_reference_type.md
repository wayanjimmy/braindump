+++
title = "Map is reference type"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Learn go with tests]({{< relref "20201208202033-learn_go_with_tests" >}})

An interesting property of maps is that you can **modify** them without passing them as a pointer. This is because `map` is a _reference type_.

Meaning it holds a reference to the underlying data structure, much like a pointer.


## Always initialize an empty map {#always-initialize-an-empty-map}

Therefore, you should never initialize an empty map variable

```go
var m map[string]string
```

Instead, you can initialize an empty map like we were doing above, or use the `make` keyword to create a map for you

```go
var dictionary = map[string]string{}

// OR

var dictionary = make(map[string]string)
```
