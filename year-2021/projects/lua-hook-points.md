---
layout: project
title: Lua Hook Points 
year: 2021
goal: Implement hook system to call Lua scripts
tags:
  - lib
  - configuration
  - lua
mentors:
  -
    name: "Stephen Worley"
    nick: "sworleys"
  -
    name: "Quentin Young"
    nick: "qlyoung"
skills:
  - C
  - Lua
  - Linux
  - Systems design
---

### Details

FRR has fledgling infrastructure for calling Lua scripts to perform designated
tasks. There is currently a proof-of-concept implementation for one limited use
case. This project would see that capability generalized and extended to
provide an internal API allowing developers to specify points in the program to
call Lua scripts.

A feature of the Linux kernel called eBPF provides anchor or hook points within
the kernel to which eBPF programs can be attached. When the kernel reaches
those hook points, the attached programs are executed. This allows users and
other programs to change the behavior of the kernel at those hook points.
FRR will do the same thing with Lua scripts. When complete this project will
provide the same capability to FRR, except that the attached programs will be
Lua scripts and not eBPF.

Currently FRR has infrastructure for calling Lua and getting results back, but
we lack a cohesive and ergonomic internal API to use this feature, so each site
where we want to provide users with a Lua hook needs to be implemented largely
by hand. This project will fix that by providing a clean way to define hooks,
their arguments, and their results. It also will provide users with a way to
view available hooks and choose what scripts to attach.

This will be a challenging project, but if you enjoy architecting programs,
designing interfaces, and improving developer experience you'll have fun with
this one. It will lay the groundwork for FRR developers to provide users with
the capability to have deep programmable control over FRR, and have a large
impact on FRR's userbase.


### Quick Start
  - Familiarize yourself with the general design of eBPF [hook points](https://blog.stackpath.com/bpf-hook-points-part-1/)
  - Learn how Lua is used to [extend C programs](https://www.lua.org/pil/24.html)
  - Take a look at the Lua proof-of-concept [in FRR](https://github.com/FRRouting/frr/blob/master/bgpd/bgp_routemap.c#L363)
  - Think about what a system for defining user-accessible hooks might look like
