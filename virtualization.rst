Virtualization
==============

Clients and servers are expensive - what if we could run different clients and servers on the same machine?

Techniques
----------

- Multiplexing: create multiple virtual objects from one underlying object
    - e.g. disk partitioning, virtual memory, sockets
- Aggregation: create one virtual object from multiple underlying objects
    - e.g. RAID
- Emulation: create a new type of virtual object from underlying objects
    - e.g. console emulators

Common Abstractions
-------------------

- send and recv with bounded buffer
    - abstraction of communication
- virt memory
    - abstraction of physical memory
- threads and processors
    - abstraction of interpreter

All of these are more general and can be provided directly, or by using virtualization

Multiplexing
^^^^^^^^^^^^
**Physical v. Temporal**

Take, for example, the CPU. We need to multiplex the CPU but obviously can't have certain applications only use
*part* of the CPU - so we multiplex in **time** using **threads**.

This is called **timesharing**. Only one application is really using the CPU at a time.

On the other hand, we *can* multiplex memory by splitting it up into virtual blocks - which is **physical**
multiplexing. (handled by the Memory Management Unit on CPU)

A thread (CPU abstraction) + virtual memory is called a **process**.

Threads
"""""""

- a single thread state consists of:
    - reference to next instruction (PC)
    - references to environment (stack, heap, registers, etc)
- single thread can be suspended at any time and later resumed
    - save thread state, protect the environment
- OS multiplexes the CPU using threads

**Managing Threads**

- thread created by another thread
    - program says to create a thread
    - user requests one (special case of program doing it)
- first thread created by OS: ``init``, parent of all processes
    - child threads (in unix) are spawned using ``fork()``
- OS
    - initializes the thread state
    - finds the thread code and data and loads it into memory
    - sets the initial PC
- thread manager in OS maintains illusion of vCPU
    - gives CPU to one thread at a time
    - ensures one thread doesn't monopolize CPU
    - protects threads from one another

**Interrupts**

- a change in "normal" execution of a CPU
- 2 different kinds:
    - computer-wide: hardware such as a disk or network card
    - thread-specific: address error, illegal instruction, math error
- computer-wide interrupts:
    - may have nothing to do with the current running thread
    - runs in the context of the OS (interrupt handler)
    - delivered to appropriate thread when it's running (maybe later)
- thread-specific interrupts (**exceptions**):
    - runs in the state of the current thread
    - delivered to individual thread without impacting other threads

Bounded Buffer
^^^^^^^^^^^^^^

- OS provides bounded buffers
    - allows threads to communicate
    - supports SEND/RECV
    - various implementations - threads don't care
- threads can't communicate directly w/o the OS
    - reduces error propogation
    - allows use of different mechanisms

Emulation
^^^^^^^^^
An OS is an "easy to use" abstraction - VMs are virtualization via emulation

the interface appears exactly the same as raw hardware, but it's not
