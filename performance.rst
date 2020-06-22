Performance
===========
What is performance?

- complete tasks faster
- use less power/energy
- do more tasks

How is performance measured?

How can we design systems to improve performance?

Measuring Performance
---------------------

- capacity: amount of a resource that's available
    - utilization: how much capacity is being used?
    - overhead: resource "wasted"
    - useful work: amount of resource spent on actual work
- time-based
    - latency: time between input and result
    - throughput: rate of results per unit time

Latency v Throughput
---------------------

- latency: elapsed time for a single action
- throughput: rate of actions per time
- throughput = 1/latency

- multistage requests: handle requests in stages
    - may increase latency (bad)
- pipelining: stages work concurrently on different requests
    - may increase throughput (good)
    - latency = time it takes a request to go thru all stages
    - throughput = limited by throughput of slowest stage

Designing
---------

1. first, actually make the system work
2. then, iterate:
    1. measure the system to see if it needs to be better
    2. measure again to find the bottleneck
    3. predict the impact of the proposed improvement by assuming the improvement will remove the bottleneck
    4. implement and measure

Fast Path
---------
When some resources are requested way more than others, you can create a special fast path for those resources

- reduces latency for *some* requests
    - common/easy requests

Concurrency
-----------

- concurrency can reduce latency
    - run multiple stages in parallel
    - reduces overall latency
    - potential issues: amdahl's (diminishing returns) law, sync
- can increase throughput
    - each stage works on a different request
    - pipelining

Pipelining
^^^^^^^^^^

- pipelines often don't actually decrease latency
- pipelines increase throughput by hiding the higher latency
    - keep each stage busy
    - only requires that each stage be handled by different resources
    - each stage has its own interpeter and mem
- use a bounded buffer between stages to keep stages busy
    - if different stages take different amounts of time to execute
    - absorbs burst
    - if incoming request rate > average thruput for one stage, you have *overload*

Bottlenecks
^^^^^^^^^^^

dealing with:

- batching
    - handle requests as a group to amortize fixed overhead
- dallying
    - delay a request - maybe it won't be needed or will be batched
- speculation
    - guess what the request is
    - increases work, decreases latency
    - might be easier to do request at earlier time
