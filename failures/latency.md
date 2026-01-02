# Latency

## What it really is?
Bookish definition: The amount of time required for an action to be completed.
Ex: Node A send a request to Node B, time required to send the request, Node B to compute the request (this will include all the service calls, IO calls, scheduler wait time etc done by Node B ), Node B sends back the response to Node A.

Another way of looking at the latency (in terms of user or Node A who is initiating the request)
Latency means waiting.
Latency is the amount of time when a service is sitting idle, not doing anything usefull and waiting for some action to be completed.

This is more from the point of view of user or the service who has inititated the request.


## Why latency is bad or why it hurts
- latency is not fixed, it is variable: same request can have different latency at due to any reason
- latency compounds, each service some more waiting: Service A calls Service B; Service B call Service C; Service C waiting for Disk; Disk waiting for I/O scheduler; Scheduler waits because machine is not free
- latency creates hidden queue: when something is slow, request piles up, queues fills, threads getting blocked, memory fills etc, latency becomes load.

## How should we measure latency in systems
- people always look for average latency, but **system suffers because of slowest latency**

### Tail Latency (things to look for)
- means: P99, P95 meaning 99th percentile, 95th percentile, slowest 1% or slowest 5%.
### Thread pool exhaustion
- 1 slow request per second
- blocks a thread; delays other request-
- soon threads will be exhausted
- latency spike
### "System is up but slow" complaints
- after latency spike in above point
- the logs and monitoring will tell you system is up but it is slow.

## Follow up after latency spiking
- a bad design would be to scale the system, that will worsen the situation
- scaling means adding more resources, more hops, more network calls, more tail latency sources, and more waiting.

### **Scaling increased capacity but doesn't always solve latency**

### Mental shift required to create better designs
- Every network call must justify itself: every network call adds latency; adding failure chances; adding tail risk
- Timeouts are mandatory: prevents unbounded waiting
- Async boundaries exist because of latency: sync operations increases latency

### Trade-off introduced
- Complexity increases: system is up but slow, we do not know which part is adding that extra slowness (latency).
- Harder debugging: now we have to monitor everything to know what is slow
- Eventual consistency often required: due to latency we would be unable to make all the services consistent instanctly.

### How to handle latency
- timeouts: 