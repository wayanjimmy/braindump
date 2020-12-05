+++
title = "Domain driven over MVC"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Go for Industrial Programming]({{< relref "20201205171405-go_for_industrial_programming" >}})

If your project has multiple binaries, it's a good idea to have a `cmd/` subdirectory to hold them.

If your project is large and has significant of non-Go code, like UI assets or sophisticated build tooling, it might be a good idea to keep your Go code isolated in `pkg/` subdirectory.

If you're going to have multiple packages, it's probably a good idea to orient them around the business domain, rather than around accidents of implementation.

That is: package user, yes; package models, no.
