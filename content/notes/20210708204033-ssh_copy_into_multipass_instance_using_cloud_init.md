+++
title = "SSH copy into Multipass Instance using cloud init"
author = ["Wayanjimmy"]
draft = false
+++

link
: [Multipass Key-Based Authentication](https://www.ivankrizsan.se/2020/12/23/multipass-key-based-authentication/)

related
: [Multipass]({{<relref "20210228151250-multipass.md#" >}})

Create `cloud-init.yaml`

```yaml
ssh_authorized_keys:
  - <your_ssh_public_key>
```

and create a vm using this config

> multipass launch --cloud-init cloud-init.yaml

Once launched, you can get the ip using `multipass list` and `ssh ubuntu@ip`
