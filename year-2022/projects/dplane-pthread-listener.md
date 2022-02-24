---
layout: project
title: Dplane Pthread Listener
year: 2022
goal: Move netlink notification listener to dplane pthread
tags:
  - zebra
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
---

### Details
350hrs project

In FRR we interact with the linux kernel through 2 different pthreads in zebra (main and dplane). For the dplane pthread, we have spent a lot of time moving most of our route/neighbors/etc. installs into this pthread via context object "snapshots" we take of the object we want to install into the kernel. We take a route or other object we want to install/update and create a context object for it to be passed to our dplane pthread and installed. This goes through to be handled by our dplane specific code (`zebra/rt_netlink` for linux as an example). Moving our kernel installs to a separate pthread has proven to significantly improve our processing time since it alleviates zebra's main thread to continue handling other things like messages from our protocols.

However, all of our incoming messages from our netlink listening socket (`zns->netlink`) still happen on the main pthread. This netlink socket listens for notifications from the kernel about events external to FRR (interface link downs/ups and others). These are events we did not initiate but have to handle in FRR by updating our internal state and responding however appropriate.

For this project, you will be moving all of the netlink listening to be handled in the dplane pthread. In zebra we have an abstracted API for all dataplanes (linux, bsd, others) in `zebra/zebra_dplane.c` Your code should be tightly integrated with that. You will need to modify the code to take an update and turn it into a context object that can be passed onto the main pthread to be eventually handled. It will be architectured very similar to how we communicate INTO the kernel and should re-use some common code where applicable.


### Bonus Goal
The dataplane context objects are currently `malloc()`d/`free()`d every time they are created/handled. Switching these to use a memory pool scheme where the context objects are pre-allocated and handed off as needed would improve processing time and should be a logical extension of batching.

### Quick Start
  - Read up on our architecture [here](http://docs.frrouting.org/projects/dev-guide/en/latest/process-architecture.html#process-architecture)
  - Familiarize yourself with the dataplane handling in `zebra/zebra_dplane.c`
  - Review how netlink kernel messaging works. Our code is in `zebra/*_netlink.c`
  - Turn on some debugs via vtysh (`debug zebra kernel`) and set links down with iproute2 (`ip link set INTF down`) to see our logging of the event in zebra
