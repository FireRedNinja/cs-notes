---
layout: post
title:  "Operating Systems H"
date:   2018-01-10 18:50:00
categories: Level3 Semester2
author: dasha
---

### Introduction

OS:

* manages computer's hardware
* provides basis for application programs
* intermediary between user and hardware
* an environment within which other programs can do useful work
<!--excerpt-->

Hardware:

* CPU
* memory
* IO devices

Application programs:

* define ways in which the above resources are used to solve users' computing problems

User view:

1. PC - maximise ease of use for a single user to monopolise resources
2. mainframe - maximise resource utilisation for lots of users accessing through terminals
3. workstations - share resources, but also have dedicated resources, connected through networks of workstations and servers
4. mobile devices - similar to PC, with touch screen

System view:

1. OS is resource allocator
2. OS controls IO devices and user programs - control program

Moore's Law - predicts that the number of transistors on an integrated circuit would double every 18 months

Common definition of an OS:

* the one program running at all times on the computer
* **kernel**
* there are also
  * system programs - associated with OS but not necessarily part of kernel
  * application programs - not associated with operation of the system
  
Today, mobile OS include **middleware** as well as the kernel:

* set of software frameworks that provide additional services to app devs
* can support databases, multimedia and graphics

#### Computer-System Operation

Modern general-purpose computer system:

* 1+ CPUs
* device controllers connected through common bus that provides access to shared memory
  * in charge of a specific type of device
* execute in parallel, competing for memory cycles
  * memory controller synchronises memory access

**Bootstrap** program:

* stored in ROM or electrically erasable ROM (EEROM)
* firmware
* initialises all aspects of system
* locates OS kernel and loads it into memory

Once kernel is loaded, it provides services to the system and users

Services provided outside of the kernel:

* system programs that are loaded into memory at boot time
  * system processes/daemons
* run while kernel is running
* on UNIX, first process is "init"
* once initial phase complete, system is fully booted and waits for some event to occur

Event occurence:

* signalled by **interrupt**
  * from hardware - send signal to CPU
  * from software - executing **system call**
* CPU transfers execution to a fixed location
  * containing starting address where the service routine for the interrupt is located
  * executes
  * on completion, CPU resumes interrupted computation
  
