---
layout: project
title: Lua Userscripting
year: 2020
goal: Implement C <-> Lua interface to support userscripting on routers!
tags:
  - routing
  - sdn
  - policy
  - ffi
  - extensibility
  - community
mentors:
  -
    name: "Stephen Worley"
    nick: "sworley"
  -
    name: "Quentin Young"
    nick: "qlyoung"
skills:
  - C
  - Lua
---

### Details

FRR, as a network routing suite, has a large variety of user-configurable
policy settings. These include ACLs, "route-maps" (small data transform
programs defined in FRR's configuration DSL that change attributes of IP
routes), and various protocol-specific knobs that influence anything from the
path cost metric on routes to node preference values in high availibility
failover protocols such as VRRP. Presently these are all implemented as bespoke
options within FRR's configuration grammar, and have to be statically defined
in its configuration file. We would like to vastly increase the flexibility and
extensibility of FRR by adding support for hooking into user-defined Lua
programs to change runtime behavior on the fly. If you are familiar with eBPF,
you can think of this project as implementing eBPF, but for a userspace network
routing stack. Or, if you are more familiar with Web technologies - Lua is to C
as Javascript is to HTML.

FRR currently has some sparse glue code to connect to Lua via its C interface,
but this is all exploratory / testing code and is not shipped in release
builds. The ideal result of this project would be an interface that allows FRR
developers to define hook points in the code that transfer control to a user's
Lua program, run the program, and pass any results back to FRR. This would
allow extremely advanced functionality and effectively make FRR a completely
programmable routing stack. New features such as monitoring, policy
definitions, flow control, deployment management etc. could be shipped as plain
text Lua scripts, shared among users, and allow FRR to operate in any number of
environments with minimal or no patching to FRR's C codebase.

FRR has high performance constraints and operates in production networks, so
the implementation of this Lua interface should be highly performant. Students
proficient in writing safe, efficient C - or who are willing to learn - are a
must. Since we have no serious implementation of this feature currently, this
is effectively a green field project, meaning overhead should be relatively
minimal.

### Bonus Goal

If the Lua interface is completed, FRR has a slew of features that are
excellent candidates for integration with it. These include route-maps, various
patchwork monitoring features, and flow control protocols. We would love to see
any of these, or anything else, converted to use the new interface so we can
pass the fruits of your labor on to users!

### Quick Start
- If you're unfamiliar with Lua, a good summary of what Lua can provide to C
  programs is located [here](https://www.lua.org/about.html).
- Have a look at some of FRR's exploratory Lua code; this exmaple offloads
  basic route-map functionality to a Lua script:
  https://github.com/FRRouting/frr/blob/master/bgpd/bgp_routemap.c#L344
- Read our [user docs on
  routemaps](http://docs.frrouting.org/en/latest/routemap.html); this is a good
  working example of the sort of functionality FRR would like to offload to Lua
  scripts.
