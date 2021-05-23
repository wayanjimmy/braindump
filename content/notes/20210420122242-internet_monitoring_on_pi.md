+++
title = "Internet Monitoring on Pi"
author = ["Wayanjimmy"]
draft = false
+++

link
: [Internet Monitoring](https://github.com/geerlingguy/internet-monitoring)

related
: [Pi Single Board Computer]({{< relref "20210420122611-pi_single_board_computer" >}}) [Tinkering]({{< relref "20210503100841-tinkering" >}})

Dockerized internet monitoring based on Speedtest.

{{< figure src="/ox-hugo/20210420_122521_EnOJ4R.png" >}}


## Speedtest not working? {#speedtest-not-working}

If you're in armhf architecture there is an issue related to the alpine image. Read [here](https://github.com/MiguelNdeCarvalho/speedtest-exporter/issues/71) and [here](https://docs.linuxserver.io/faq#libseccomp)
