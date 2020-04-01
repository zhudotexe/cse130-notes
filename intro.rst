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

But these aren't really different things! They're a method of constraining complexity

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

Layering
^^^^^^^^
Used to reduce interconnections - build higher layers on top of lower layers

creates a "stack" - constrain the ways layers are allowed to interact with one another
