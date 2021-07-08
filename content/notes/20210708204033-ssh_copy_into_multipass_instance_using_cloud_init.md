+++
title = "SSH copy into Multipass Instance using cloud init"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Multipass]({{< relref "20210228151250-multipass" >}}) [Tinkering]({{< relref "20210503100841-tinkering" >}})

Create `cloud-init.yaml`

```yaml
ssh_authorized_keys:
  - <your_ssh_key>
```

and create a vm using this config

> multipass launch --cloud-init cloud-init.yaml

Once launched, you can get the ip using `multipass list` and `ssh ubuntu@ip`
