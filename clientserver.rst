Client-Server Model
===================

So why use client-server?

Well, just using procedures is a kind of soft-modularity - our modules agree to only interact in some way, but
nothing's actually stopping them from messing with each other.

Just using procedures is also fate-sharing. If the callee fails, the caller fails. This is an error that shouldn't
propogate up to the caller - but it does.

So the client-server modules enforces modularity by only allowing the caller and callee to communicate over one
channel/wire. We can represent interactions with a timing diagram.

But there are potential issues too:

- representation
    - serialization, deserialization
    - little-endian, big-endian
- ordering of messages
- client or server behaving badly

Advantages:

- no shared state (aside from messages)
    - errors can only propogate via messages
- limited interaction = limited errors
- client and server can protect against failure to response
    - e.g. timeouts
- well-defined interface
    - client and server can have independent implementations

Hard v. Soft Modularity
-----------------------

Whereas soft modularity is an agreement to only interact in some way, hard modularity means that components can
only interact in well-defined ways.

Isolation: calling convention (soft) v. physical boundaries

Mechanism: functions, classes, etc v. client/server

Failures: total v. partial

Programmability: easy v. hard

The Bad: less isolation v. more executions