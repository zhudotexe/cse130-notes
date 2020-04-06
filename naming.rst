Naming
======

Memory
^^^^^^
Memory is a fundamental abstraction - it just means storage

- basic operations:
    - WRITE (name, value)
    - value <- READ (name)
- memory can be provided by both hardware and complex systems
    - RAM
    - Disk
    - files
    - database
- use layering and modularity to select specific memory module
- main characteristics:
    - latency: time to r/w 1st byte
    - bandwidth: how long it takes to r/w X bytes
    - cost
    - capacity
    - volatility/lifetime
    - rewritability

But you might have:

- different terms for the units that make up values (e.g. bytes v. sequences)
- different mechanisms for naming
- different performance

**Naming in Memory**

For memory, each name needs to be unique - each name must point to at most one value (they can also point to nothing...)

Usually, memory names are linearly mapped (e.g. pointers)

**Layering in Memory**

- file system
    - inodes are numeric names
    - file names built on top of inodes
- internet
    - MAC addresses
    - IP addresses
    - DNS names
- the web combines multiple high-level naming schemes together