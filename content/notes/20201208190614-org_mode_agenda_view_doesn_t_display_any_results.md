+++
title = "Org-mode agenda view doesn't display any results"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Doom Emacs]({{< relref "20201208184126-doom_emacs" >}})

In order for `org-mode` to show events scheduled or with a deadline in the agenda-view, the org-file containing these events must be listed in the variable org-agenda-files.

While one can customize this variable, the more practical way is to invoke the function `org-agenda-file-to-front`, which is commonly bound to `C-c [`
