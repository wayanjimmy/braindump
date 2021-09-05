+++
title = "Proxmox CloudInit"
author = ["Wayanjimmy"]
draft = false
+++

links
: [Proxmox CloudInit Tutorial](https://youtu.be/Ygk7oq--mak)

related
: [Proxmox]({{<relref "20210509131657-proxmox.md#" >}}) [Linux]({{<relref "20210502110347-linux.md#" >}})

<!--listend-->

```bash
##Delete default user
deluser --remove-home testuser

##Create swap file
dd if=/dev/zero of=/swapfile bs=1024 count=1536000
chmod 600 /swapfile
mkswap /swapfile
swapon /swapfile
echo "/swapfile       swap    swap    defaults        0 0" >> /etc/fstab

##Install pakages
#Mandatory
apt install -y cloud-init cloud-initramfs-growroot qemu-guest-agent sudo git curl
```
