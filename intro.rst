Intro
=====

Complexity
----------

Modern computer systems are large and complex - this course is about the problems with designing complex systems
and how to manage the complexity and these problems.

Issues
^^^^^^
Complex systems exhibit 4 basic issues:

- emergent properties
    - properties that show up only when combining individual components
- propogation of effects (butterfly effect)
    - problems in one component affect other components
    - relationship between components isn't always obvious
- incommensurate scaling
    - not all parts of a system scale at the same rate
- tradeoffs
    - limits mean that increasing one characteristic may harm another
    - e.g. utilization v. latency tradeoff

Symptoms
^^^^^^^^

- large number of components
- large number of interconnections
- lots of irregularities
- long description / high information content
- large team of designers, implementers, or maintainers

Sources
^^^^^^^

- interactions of requirements
    - a general purpose tool that can do X and other things is more complex than a tool that can *only* do X
    - more jobs -> more complexity
    - more constraints -> more complexity, even if constraints don't apply at the same time

- increasing efficiency (or other measure of "goodness")
    - "low-hanging fruit" is easy to get
    - additional gains in efficiency require more complexity
    - same applies to cost

Managing Complexity
-------------------
We can manage complexity in systems in a few ways:

- modularity
- abstraction
- layering
- hierarchy
- naming (controls/manages all of these)

But these aren't really different things! They're a method of constraining complexity - it makes it
easier to understand why code is doing what it's doing.

Modularity
^^^^^^^^^^

- break big things into little things (divide and conquer)
- allows development of a smaller unit
    - reduce number of components and interactions
    - reduce complexity
    - reduce # of bugs
- allows for interchangeable modules
    - replace a module with a "better" one
    - replace a broken module
- stitching together big pieces that only interact in certain ways

However, for people to be able to use modules well, you need a *spec* - a document that details how
exactly this module work.

That creates a **level of indirection**. Now clients don't care about how your module is implemented - only
that it will do what it says in the spec.

Abstraction
^^^^^^^^^^^
maybe thought of as one of the means to get to modularity

- break into components at logical points
- treat an individual component as a black box
    - inputs and outputs and behaviours
    - trust that it'll do it
- robustness principle
    - be tolerant of inputs: try and do the right thing
    - be strict on outputs: underpromise, overdeliver, always follow the spec
- mantain a safety margin: fragility is bad
- a way to take functions and make them more general

Layering
^^^^^^^^
Used to reduce interconnections - build higher layers on top of lower layers

creates a "stack" - constrain the ways layers/modules are allowed to interact with one another

It's often the design of the layers that defines what modules should look like.

Hierarchy
^^^^^^^^^
How to group boxes of boxes into boxes - making bigger modules out of smaller ones

- for example, ASM <- LOC <- functions <- class/module <- service
- each of these are modules that have specs, but are made up of smaller modules

Names
^^^^^
Now we need to understand what boxes are, and how to assemble them

- names help us identify things in an independent way
    - replace a module but keep a name
    - use names to look up which components to use, where to find them
- a way for a component to talk about another component that it's using
- **binding**: going from a name to the actual code that's being run

Approaches
----------

Iteration
^^^^^^^^^

- you likely won't make the right choices the first time, so make it easy to fix
- make small steps, have fallbacks and try a lot of choices

KISS
^^^^
Keep it Simple, Stupid

- resist temptation to add unnecessary features, which increases complexity and you can't take them away

Fundamental Abstractions
------------------------

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

Coherence
^^^^^^^^^
Related to ordering/timing - that a read will always return the most recent write

Atomicity
^^^^^^^^^
reads/writes happen all at once - can't interleave actions between multiple reads/writes

Coherence and atomicity seem simple, but can be difficult for many reasons.

Interpreter
^^^^^^^^^^^

- an interpreter performs actions in the computer system
    - do what the program says in the way it says to do it
- 3 basic components:
    - instruction reference - where is the next instruction
    - repertoire - what can this interpreter do
    - environment reference - where is the current state

Communication Channel
^^^^^^^^^^^^^^^^^^^^^
A way to move information between components

Two main components: send, receive

For example:

- shared memory
    - might have atomicity issues
- message pipeline
    - might have coherency issues (race)
