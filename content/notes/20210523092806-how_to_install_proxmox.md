+++
title = "How to Install Proxmox"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Proxmox]({{< relref "20210509131657-proxmox" >}})

link
: [Proxmox Install](https://youtu.be/%5Fu8qTN3cCnQ)


## Increase Storage {#increase-storage}

Before executing make sure delete the localvm from the storage section

```bash
lvremove /dev/pve/data

lvresize -l +100%FREE /dev/pve/root

resize2fs /dev/mapper/pve-root
```
