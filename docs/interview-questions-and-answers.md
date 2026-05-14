# Production Debugging Interview Questions & Answers

## All APIs are slow — where do you start?

First validate scope and blast radius.
Then isolate request path:
- LB
- application
- DB
- downstream services
- network

The key question:
Where is wait time introduced?

---

## CPU low, memory fine, but latency high — explain

Possible causes:
- IO wait
- blocked threads
- queueing
- connection pool exhaustion
- retransmits
- DNS retries
- lock contention

Systems fail through waiting, not just utilization.

---

## Difference between p95 and p99 latency

p95:
95% of requests complete within this time.

p99:
Tail latency.
Represents worst user experience.

p99 reveals:
- retries
- intermittent contention
- queue spikes
- slow downstreams

---

## Why average latency is misleading

Averages hide outliers.

Example:
99 requests = 50ms
1 request = 10 seconds

Average still looks acceptable.

---

## What if only 2 out of 10 servers are slow?

Likely causes:
- bad node
- hardware degradation
- noisy neighbor
- uneven traffic
- kernel instability

Compare healthy vs unhealthy nodes.

---

## What if all metrics look normal but latency is high?

Then investigate deeper:
- retransmits
- MTU mismatch
- DNS intermittency
- queueing
- kernel/socket issues
- blocked threads
- tail latency

This is where systems knowledge matters.

---

## What is connection pool exhaustion?

All DB connections become occupied.
New requests wait for available connections.

Symptoms:
- rising latency
- blocked threads
- request timeouts
- low CPU usage

---

## What is iowait?

CPU idle time spent waiting for IO operations.

High iowait usually means:
- storage bottleneck
- blocked IO operations
- slow disks

---

## What will you do first — fix or investigate?

Mitigation first.
RCA second.

Reduce customer impact quickly:
- rollback
- scale
- drain bad node
- fail over
- disable feature
