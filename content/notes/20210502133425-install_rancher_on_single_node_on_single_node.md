+++
title = "Install Rancher on Single Node"
author = ["Wayanjimmy"]
draft = false
+++

links
: [Install Rancher on Single Node](https://rancher.com/docs/rancher/v2.0-v2.4/en/installation/other-installation-methods/single-node-docker/)

related
: [Docker]({{<relref "20210518095808-docker.md#" >}})


## Install Docker {#install-docker}

Make sure you have docker installed by execute the command below

```bash
curl https://releases.rancher.com/install-docker/19.03.sh | sh
```

Read [more](https://rancher.com/docs/rancher/v2.5/en/installation/requirements/installing-docker/)


## Install on Single Node {#install-on-single-node}

We need to run the rancher web admin on the port other than 80, because port 80 will be used by nginx-ingress, read [here](https://github.com/rancher/rancher/issues/12846) about this issue.

```bash
docker run -d --restart=unless-stopped \
  -p 8080:80 -p 8443:443 \
  --privileged \
  rancher/rancher:latest
```
