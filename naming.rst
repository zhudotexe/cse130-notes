Naming
======

Mapping
-------

There are several techniques to map names to values, often combined for a single name resolution.

The main idea is ``resolve(name, context)``, that maps a name in a context to exactly one value.

- table-based lookup: correspondence of name-value in a table
- recursive lookup: resolution provides a new name rather than a mapping, new name looked up
- multiple lookup: search multiple contexts to find the name

So why names?

Computer systems use names to identify components

- addresses of values in objects
- addresses of other systems

Components may be passed by value or reference

- value: copy component
    - only makes sense for some usage
    - better for modularity: minimizes side effects
- reference: provide the name of the component

Names facilitate sharing

- different components can reference the same object
- name is used to provide a reference to each component

Names allow deferred lookup

- to which object does a name refer?
- decision can be make when the name is looked up

**Indirection**: using intermediary to associate name and object

**Binding**: association of a name to a particular object

Contexts and Operations
-----------------------

- context: information that helps determine name
    - e.g. identity of the user
    - location making the request
    - current working directory


