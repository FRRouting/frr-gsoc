---
layout: project
title: Zebra Traffic Control
year: 2022
goal: Add traffic control capabilities to zebra
tags:
  - zebra
  - lib
  - qos
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
350hrs project - Hard Difficulty

Add the ability for ZEBRA to modify TC tables via the netlink protocol. Currently FRR has no ability to modify the underlying TC tables. This would be extremely useful for BGP Flowspec as well as with PBR.

This will require you to extend the appropriate lib\* APIs, dataplane code (`zebra/rt_netlink.c`), dataplane handler code (`zebra/zebra_dplane.c`). The current code for BGP flow spec is in hook calls in `zapi_msg.c`.


### Quick Start
  - Familiarize yourself with the dataplane handling in `zebra/zebra_dplane.c`
  - Review the tc [program](https://www.linux.com/training-tutorials/qos-linux-tc-and-filters/) and it’s interface with the kernel
  - Understand the hook calls for rule addition in `zebra/zapi_msg.c`
