+++
title = "Configure program using flags"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Go for Industrial Programming]({{< relref "20201205171405-go_for_industrial_programming" >}})

Flags are the best way to configure your program, because they're a self documenting way to describe the configuration surface area of your program at a runtime.

Flags can be inspected by other users of the system, and env vars can easily get **forgotten**

[Domain driven over MVC]({{< relref "20201205171728-domain_driven_over_mvc" >}}) Just ensure that explicit command line flags, if given, take highest **priority**
