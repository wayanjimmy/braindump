+++
title = "Install Grafana on Pi"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Pi Single Board Computer]({{<relref "20210420122611-pi_single_board_computer.md#" >}})

Head to this [url](https://grafana.com/grafana/download?platform=arm), since Orange Pi based on armhf architecture, follow the (ARMv7) install guide

```bash
sudo apt-get install -y adduser libfontconfig1
wget https://dl.grafana.com/oss/release/grafana_7.4.5_armhf.deb
sudo dpkg -i grafana_7.4.5_armhf.deb
```
