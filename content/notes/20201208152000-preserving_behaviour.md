+++
title = "Preserving Behaviour"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Working Effectively with Legacy Code]({{< relref "20201208151850-working_effectively_with_legacy_code" >}})

Dari table dibawah dapat disimpulkan kalau proses refactoring pada dasarnya mirip dengan penambahan fitur dan optimizing, mengapa ?

karena sama-sama tidak mengubah fungsi yang lama.

|                   | Adding Feature | Fixing a Bug | Refactoring | Optimizing |
|-------------------|----------------|--------------|-------------|------------|
| Structure         | Changes        | Changes      | Changes     | -          |
| New Functionality | Changes        | -            | -           | -          |
| Functionality     | -              | Changes      | -           | -          |
| Resource Usage    | -              | -            | -           | Changes    |

Itu kenapa mempertahankan fungsi yg lama adalah hal yang sering dilakukan dalam programming.

{{< figure src="/ox-hugo/preserving-behaviour.png" >}}

Mempertahankan fungsi yg sekarang adalah tantangan terbesar dalam pengembangan perangkat lunak. Meskipun mengubah fungsi utama, sering kali cakupkan kode yang ingin dipertahankan juga cukup besar.

> Preserving existing behaviour is one of the largest challenges in software development. Even when we are changing primary features, we often have very large areas of behaviour that we have to preserve
