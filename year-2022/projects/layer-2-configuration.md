---
layout: project
title: Layer 2 Configuration
year: 2022
goal: Add layer 2 configuration capabilities
tags:
  - zebra
  - lib
  - configuration
  - dataplane
mentors:
  -
    name: "Stephen Worley"
    nick: "sworleys"
  -
    name: "Quentin Young"
    nick: "qlyoung"
skills:
  - C
  - netlink
  - Linux
  - networking
---

### Details
175 or 350hrs project (dependent on # of components added)

Add layer 2 functionality into FRR. Specifically, add the ability to configure layer 2 type data in dataplanes. For example, configuring VRFs or interfaces in FRR, should create them in the dataplanes as well. This project will be scoped for the Linux dataplane.

For example, configuring interface and VRF information in FRR should create interfaces and VRFs in the kernel. In current FRR, we must configure those separately using another tool (`iproute2` in Linux) and then reference them by name in FRR configurations.

This will require you to extend the appropriate `lib/*` APIs, dataplane code (`zebra/rt_netlink.c`), dataplane handler code (`zebra/zebra_dplane.c`), and add appropriate vty commands (`*_vty.c`) for the layer 2 configurations.


### Quick Start
  - Familiarize yourself with the dataplane handling in `zebra/zebra_dplane.c`
  - Review how netlink kernel layer 2 messaging works. Our code is in `zebra/if_netlink.c`
  - Learn how we parse the FRR [cli](http://docs.frrouting.org/projects/dev-guide/en/latest/cli.html#command-line-interface)
  - Understand how interfaces and VRFs are created in the Linux kernel with iproute2
