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
  * average waiting time less than FIFO
* but, you need to know the length of the next CPU burst
  * for long-term scheduling, can use the process time limit that a user specifies
  * users are motivated to submit an accurate time
    * lower value = faster response
    * too low a value = time-limit-exceed error + resubmission
* SJF cannot be used with short-term scheduling
* can predict the next CPU burst
  * exponential average of the measured lengths of previous bursts
  * for `Tn` = length of `nth` CPU burst, and `Yn+1` = predicted value
  * then for `0 <= A <= 1`, `Yn+1 = ATn + (1-A)Yn`
    * `A` controls relative weight of recent and past history in the prediction
  * this alg. can be preemptive/nonpreemptive
    * the next CPU burst of a newly arrived process may be shorter than what is left of a currently existing process
      * a preemptive will preempty the current process (shortest-remaining-time-first)
      * a nonpreemptive will allow the current process to finish first
      
Priority:

* CPU allocated to process with highest priority
* equal-priority are scheduled as FIFO
* here, assume low numbers represent high priority (but irl, different systems use different priority numbers)
* internally defined priorities
  * use some measurable quantity to compute priority
  * time, memory limits, num. of open files etc
* externally defined priorities
  * set by OS criteria
  * importance, type and amount of funds being paid for computer use etc
* preemptive - preempt CPU if priority of new process is higher than current
* nonpreemptive - put new process at head of ready queue
* **indefinite blocking/starvation** - a process that is ready to run but waiting for the CPU
  * low priority processes may wait indefinitely
    * either they will eventually be run when the system is lightly loaded
    * or the system will crash and lose all unfinished low priority processes
 * solution - **aging**
   * gradually increase priority of processes that wait for a long time
   
Round-robin:

* designed for time-sharing systems
* FIFO with added preemption
* time slice is defined
* ***ready*** queue treated as circular
* scheduler goes around the queue, allocating CPU to each process for specified time interval
* process may have CPU burst < 1 time quantum
  * release CPU voluntarily
* process may have CPU burst > 1 time quantum
  * timer interrupt
  * context switch
  * process moved to tail of queue
* average waiting time often long
* preemptive
* want the time quantum to be large with respect to the context-switch time
  * if context switch is 10% of the time quantum, then 10% of CPU time is spent in context switching
* turnaround time depends on time quantum
  * can be improved if most processes finish their burst in a single time quantum
  * context switching increases average turnaround time
* if the time quantum is too large, RR scheduling degenerates to FIFO
* generally, 80% of CPU bursts should be smaller than the time quantum

Multilevel queue:

* foreground/background processes
  * different response time requirements
  * different scheduling needs
  * foreground may have external priority over background
* partition ***ready*** queue into several queues
  * processes permanently assigned to one queue based on some property
  * each queue has its own scheduling alg.
  * scheduling among the queues is commonly fixed-priority preemptive (foreground may have absolute priority over background)
* queues can also be time-sliced
  * eg 80% of CPU to foreground to RR
  * 20% of CPU to background to FCFS (first come first served - FIFO)
* low scheduling overhead
* inflexible (processes stay in one queue all the time)
  
Multilevel feedback queue:

* processes can move between queues
* separate processes according to the characteristics of their bursts
  * process using too much time --> moved to lower-priority queue
  * leaves IO-bound and interactive processes in higher priority
  * there is also aging so a low priority queue can be moved to a higher one
* generally defined by the following parameters
  * num. of queues
  * scheduling alg. of each queue
  * method to determine when to upgrade to higher-priority
  * method to determine when to upgrade to lower-priority
  * method to determine which queue a process will enter when it needs service
* can be configured to match a specific system
* most complex alg.

#### Thread Scheduling

OS schedules kernel-level threads (not processes)  
   User-level threads managed by a thread library  
   These threads must be mapped to a kernel-level thread (indirect and uses a lightweight process)
   
