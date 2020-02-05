---
layout: project
title: Dataplane Batching
year: 2020
goal: Implement dataplane batch sending
tags:
  - zebra
  - dataplane
mentors:
  -
    name: "Stephen Worley"
    nick: "sworley"
  -
    name: "Quentin Young"
    nick: "qlyoung"
skills:
  - C
  - netlink
  - linux
---

### Details
Certain dataplanes allow for batch sending messages to them (linux kernel via netlink). With our dataplane abstraction in `zebra/zebra_dplane.c`, we create a queue of dataplane context objects for messages we want to send to the kernel. In a separate thread, we loop over this queue and send the context objects to the appropriate dataplane. A batching enhancement should tightly integrate with the dataplane context objects so they are able to be batch send to dataplanes that support it.

The dataplane netlink code in `zebra/rt_netlink.c` error handling will need to be adjust from what it is currently (they know an error occurred for message X immediately). With batching, you send N messages and maybe 1 of them fails. You will need to relate that failed message to a context object via a sequence of some kind and alert the upper level dataplane handling code about it.

### Bonus Goal
The dataplane context objects are currently `malloc()`d/`free()`d every time they are created/handled. Switching these to use a memory pool scheme where the context objects are pre-allocated and handed off as needed would improve processing time and should be a logical extension of batching.

### Quick Start
  - Familiarize yourself with the dataplane handling in `zebra/zebra_dplane.c`
  - Review how netlink kernel messaging works. Our code is in `zebra/rt_netlink.c`
  - Take a look at libmnl's [implementation](https://netfilter.org/projects/libmnl/doxygen/html/nlmsg_8c_source.html#l00413) of netlink batching.
