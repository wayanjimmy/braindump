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

> lvremove /dev/pve/data

<!--quoteend-->

> lvresize -l +100%FREE /dev/pve/root

<!--quoteend-->

> resize2fs /dev/mapper/pve-root
