+++
title = "Provision multipass using ansible"
author = ["Wayanjimmy"]
draft = false
+++

link
: [Ansible Boilerplates](https://github.com/xcad2k/ansible-boilerplates) [Deploy Docker with Ansible](https://www.the-digital-life.com/deploy-docker-with-ansible/)

related
: [Multipass]({{< relref "20210228151250-multipass" >}}) [Ansible]({{< relref "20210807084603-ansible" >}})


## Install the Docker Galaxy Extension for Ansible {#install-the-docker-galaxy-extension-for-ansible}

```bash
ansible-galaxy collection install community.docker
```


## Create ansible configuration files {#create-ansible-configuration-files}

```bash
touch inventory ansible.cfg
```

Put the server IP inside the `inventory` file, since I'm using multipass, I can execute `multipass info <vm_name>` to get this information

```bash
multipass info devbox
```

The `inventory` file should look like this

```nil
192.168.122.157
```

The `ansible.cfg` file should look like this

```nil
[defaults]

inventory = inventory

host_key_checking = False

deprecation_warnings = False

remote_user = ubuntu

private_key_file = ./ubuntu_key
```
