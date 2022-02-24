---
layout: project
title: ZAPI Versioning Protobuf
year: 2022
goal: Add a supportable versioning system to ZAPI and convert to protobuf
tags:
  - zebra
  - lib
  - protobuf
  - api
mentors:
  -
    name: "Stephen Worley"
    nick: "sworleys"
  -
    name: "Quentin Young"
    nick: "qlyoung"
skills:
  - C
  - Linux
  - protobuf
---

### Details
350hrs project

In FRR, our routing daemons run as separate processes that communicate to Zebra via sockets. We use an internal stream protocol called ZAPI to accomplish this documented [here](http://docs.frrouting.org/projects/dev-guide/en/latest/zebra.html#overview-of-the-zebra-protocol). The code for it is largely found in `lib/zclient.h` and `zebra/zapi_msg.c`. There is some pseudo-versioning done with it but nothing that we support users to make use of in their own out-of-tree code. The protocol is currently supported insofar that we assume only daemons in our code tree will use it.

For this project, you will research/design a versioned API we can support long term in our daemons. Along with this, you will also convert our encoding to use [protobuf](https://developers.google.com/protocol-buffers/). This API and protocol should also provide a way for us to logically extend it to support other programmatic interaction with Zebra (ex: general routing database to provide route dumps). The API should be well documented on the [docs page](http://docs.frrouting.org/projects/dev-guide/en/latest) so people can easily use it.

These changes will need to be heavily tested (unit and integration) across our daemons to ensure existing functionality is not broken as it touches all of them.

### Quick Start
  - Review our current ZAPI [docs](http://docs.frrouting.org/projects/dev-guide/en/latest/zebra.html#overview-of-the-zebra-protocol)
  - Familiarize yourself with ZAPI in `lib/zclient.c`, `zebra/zapi_msg.c`, and `zebra/zserv.c`
  - Read up on [protobuf](https://developers.google.com/protocol-buffers/)
