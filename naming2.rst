Naming, Part 2
==============
Naming supports the basic techniques for building systems

- modularity
- abstraction
- layering
- hierarchy

Naming systems designed to make systems easy to use, implement, and more reliable/predicatable

we can use them to refer to the same thing, something with the same name but a new implementation, or just finding
something

Modularity
----------
How do we handle 2 instances of different things with the same name?

Context-based resolution/disambiguation

We solve this using a **scope**: the context in which the name appears

- different names inside and outside of the scope
    - ``init()`` vs ``std::vector::init()``
    - scope can be dynamic or static
- allows use of the same name in different contexts
    - name resolves according to predefined rules
    - e.g. nested scopes in python - go up the stack until name resolves in one

Metadata
--------
Information about data

- ex:
- object name
- object context
- size
- unique system wide identifier
- type of data in object
- timestamps (creation/modification/access)
- ownership
- checksum

It's often possible to change metadata without changing the underlying data

- ideally, names are just identifiers
- metadata is used to store "other information"
- but often names contain some metadata
    - file extension
    - version number (e.g. ``foo-v2.txt``)
    - hierarchy/locator (e.g. website parts between dots)
    - these are considered *overloaded* names - they contain more than just an identifier
- names that aren't overloaded are *pure names* - they contain no information, all you can do is pass it to a resolver

Obtaining Metadata
^^^^^^^^^^^^^^^^^^

- directly (if stored separately)
    - takes a name and returns metadata
    - e.g. ``lstat()`` calls
- by parsing the name
    - e.g. university name from URL
    - parent directory from file name
- path names are often overloaded - easy to encode information in a directory path

Problems
^^^^^^^^
Overloaded names are fragile!

- e.g. changing the date in a filename may break scripts pointing to that file
- e.g. library names like ``foo2.so`` renames to ``foo3.so``
- Level of indirection: a symbolic link fixes this

Locators
--------

- Addresses are modular names that tell a system where to find an object
- can be physical or virtual (and virtual names are stable)
- address can be used as both name and locator
    - e.g. web URLs are both addresses and names
    - addresses can be numeric or not

Uniqueness
----------
It's often necessary to assign unique names to things - but how?

- hand out names centrally
    - e.g. ICANN - hand out large batches of names to servers to distribute
- use a random name from a very large name space
    - random 256-bit name
- generate name from content
    - e.g. SHA-1 or SHA-256
    - all objects with same content get same name
    - technically overloaded, but useful if name should depend on content

Lifetimes
---------

- names can have limited lifetimes
    - e.g. lifetime of a fd is the time the file is open
    - after the file is closed, the descriptor can be reused
- limited-life names are often assigned rather than chosen
    - e.g. file descriptor, outgoing port
    - prevents collision
- short-lived names tend to be local
    - takes time to distribute/invalidate
- long-lived names can be global
    - e.g. domain->IP, url->file
    - changes take even more time to propogate
- if a reference outlives the name, it's *dangling*
- similarly, if an object outlives all names, it's *orphaned* (GC fixes this)

Resolution
----------
Resolution is usually multiparted and recursive, with lots of parts cached!

e.g. Hierarchy of a URL:

1. protocol
2. website - ``edu`` server, then so on and so forth - caching
3. resource on server - after the ``/``
