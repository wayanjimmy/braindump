+++
title = "Setup Wireless Connection on Pi"
author = ["Wayanjimmy"]
draft = false
+++

link
: [Armbian Forum](https://forum.armbian.com/topic/13628-help-me-to-setup-a-wifi-ap-via-command-line/)

related
: [Pi Single Board Computer]({{< relref "20210420122611-pi_single_board_computer" >}})


## Use NMCLI (Network Manager CLI) {#use-nmcli--network-manager-cli}


### Check Device Status {#check-device-status}

```bash
nmcli device status
```


### Scan for Access Points {#scan-for-access-points}

```bash
nmcli dev wifi list
```


### Connecting to an Open AP {#connecting-to-an-open-ap}

```bash
nmcli device wifi connect <SSID>
```


### Connecting to a password protected AP {#connecting-to-a-password-protected-ap}

```bash
nmcli device wifi connect <SSID> password <password>
```
