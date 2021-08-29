+++
title = "Proxmox Terraform"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Proxmox]({{<relref "20210509131657-proxmox.md#" >}}) [Proxmox CloudInit]({{<relref "20210513125917-proxmox_cloudinit.md#" >}})

link
: [Install Proxmox virtual machine with Terraform](https://norocketscience.at/provision-proxmox-virtual-machines-with-terraform/)


## Example terraform file {#example-terraform-file}

> terraform {
>   required\_version = ">= 0.14"
>   required\_providers {
>     proxmox = {
>       source = "telmate/proxmox"
>     }
>   }
> }
>
> provider "proxmox" {
>   pm\_tls\_insecure = true
>   pm\_api\_url      = "<https://192.168.xx.xx:8006/api2/json>"
>   pm\_user         = "root@pam"
>   pm\_password     = "password"
> }
>
> resource "proxmox\_vm\_qemu" "example" {
>   count = 1
>   name  = "example-${count.index}"
>
> target\_node = "proxmox"
>
> clone = "debian10-cloudinit"
>
>   os\_type  = "cloud-init"
>   cores    = 2
>   agent    = 1
>   sockets  = "1"
>   cpu      = "host"
>   memory   = 1024
>   bootdisk = "scsi0"
>   scsihw   = "virtio-scsi-pci"
> }


## Terraform apply running forever {#terraform-apply-running-forever}

Make sure add the value `agent = 1`, to enable qemu agent. See [more](https://github.com/Telmate/terraform-provider-proxmox/issues/325).
