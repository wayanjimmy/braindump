+++
title = "Delete multiple Git Branch using a Pattern"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Git]({{< relref "20210217134705-git" >}})

<!--listend-->

```bash
git branch | rg 'put-pattern-here' | xargs git branch -D
```
