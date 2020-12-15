+++
title = "Private functions as being less stable"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Learn go with tests]({{< relref "20201208202033-learn_go_with_tests" >}})

link
: [But isn't mocking evil?](https://quii.gitbook.io/learn-go-with-tests/go-fundamentals/mocking#but-isnt-mocking-evil)

Altough [Golang]({{< relref "20201205165502-golang" >}}) lets you test private functions, I would avoid it, as private functions are implementation detail to support public behaviour.

> Test the public behaviour -- Sandi Metsz

Sandi Metz describes private functions as being _less stable_ and you don't want to couple your tests to them.
