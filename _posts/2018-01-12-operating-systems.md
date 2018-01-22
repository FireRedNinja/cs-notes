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
  
Interrupts:

* transfer control to appropriate interrupt service routine
  * invoke generic routine to examine interrupt info.
    * call interrupt-specific handler
  * table of pointers to interrupt routines is used
    * low memory (first hundred locations or so)
  * **interrupt vector** - array of addresses 
    * indexed by unique device number
* must save address of interrupted instruction
  * stored on system stack
  
Storage:

* programs run from rewritable main memory (D/RAM) but this is **volatile**
* EEROM/ROM - stores factory installations/bootstrap program
* magnetic disk - secondary storage
* magnetic tape
* cache
* solid state disk
* NVRAM - DRAM with battery backup power
* ***load*** - move byte/word from main to internal register
* ***store*** - move content of a register to main

Intruction-execution cycle:

* fetch instruction from memory
* store in the instruction register
* decode and execute intructions on operands
* result may be stored back in memory

### CPU Scheduling

Multiprogramming:

* maximise CPU utilisation
* several processes kept in memory at one time
  * when one process has to wait, OS takes all CPU from it and gives it to another process
  * repeat
  
CPU/IO burst cycle:

* process execution 
  * CPU burst --> IO burst (repeat)
    * exponential/hyperexponential frequency curve (lots of short CPU and not many long CPU bursts)
    * IO-bound program has many short CPU bursts
    * CPU-bound program might have a few long CPU bursts
  * final CPU burst ends with system request to terminate execution
  
CPU scheduler:

* short-term
* select from list of processes that are ready to execute
  * not necessarily FIFO
  
Preemptive scheduling - scheduling decisions may take place under the following 4 circumstances:

1. process switching from running to waiting (IO or ***wait***)
2. process switching from running to ready (interrupt)
3. process switching from waiting to ready (completion of IO)
4. process terminating

* for ***1*** and ***4***, the scheduling scheme is **nonpreemptive**/**cooperative** (no choice in the matter)
  * doesn't require special hardware (timer) needed for preemptive scheduling
* preemptive results in race conditions when data is shared among processes
  * while a process is updating data, it is preempted so that a second process can run
  * 2nd tries to read data, which is in an inconsistent state
* preemption affects design of OS kernel
  * during processing a system call, kernel may be busy with an activity on behalf of a process
  * may involve changing kernel data (eg IO queues)
  * what if process is preempted in the middle of these changes and the kernel needs to read/modify the same structure?
    * wait for system call to complete
    * wait for IO block to take place before switching context
    * ensures simple kernel structure
    * poor support of real-time computing
    
Dispatcher:

* gives CPU control to process selected by short-term scheduler
  * switch context
  * switch to user mode
  * jump to proper location in user program
* invoked during every process switch
* dispatch latency - time taken to stop one process and start another

Scheduling criteria - when choosing a CPU-scheduling algorithm:

* CPU utilisation
  * CPU should be as busy as possible
  * ideally usage should be 40-90%
* throughput
  * number of processes completed per time unit
  * 1 per hour for long processes
  * 10 per second for short processes
* turnaround time
  * interval from time of submission of a process --> its completion
  * sum of periods spent waiting to get into memory, waiting in ***ready*** queue, execution, and doing IO
  * generally limited by speed of output device
* waiting time
  * alg. doesn't affect amount of time during which a process executes or does IO
  * only affects waiting time
  * sum of periods spent waiting
* response time
  * time from submission of request --> production of first response
  * time to start responding, not time it takes to output the response
  
Desirable to maximise CPU utilisation and throughput, and minimise the others.  
   In most cases, we optimise the average measure.  
   A system with reasonable and predictable response time may be considered more desirable than one that is faster on average, but highly variable.
   
#### Scheduling Algorithms

FIFO:

* simple to understand and implement
* average waiting time often quite long
  * may vary substantially if CPU burst times vary greatly
* convoy effect where processes wait for one big process to get off the CPU
* nonpreemptive (only releases upon termination or IO)
  * bad for time-sharing systems
  
Shortest-job-first:

* associates with each process the length of the process' next CPU burst
* CPU assigned to process with the smallest next CPU burst
* FIFO to break ties
* gives minimum average waiting time for a given set of processes