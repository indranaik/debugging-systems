# Production Latency Debugging

## Scenario

Production API latency jumps from 80ms to 900ms.

- CPU looks normal
- memory looks fine
- pods are healthy

This is where real systems debugging starts.

---

# First Principle

Latency means something is waiting.

The job is to identify:

> where wait time is introduced.

---

# Common Hidden Causes

## Network
- TCP retransmits
- packet loss
- MTU mismatch
- DNS intermittency
- SYN backlog overflow

## Infrastructure
- bad node
- noisy neighbor
- throttling
- conntrack exhaustion
- storage latency

## Application
- blocked threads
- thread pool exhaustion
- deadlocks
- GC pauses
- lock contention

## Database
- slow queries
- connection pool exhaustion
- lock waits
- replication lag

---

# Golden Debugging Flow

1. Confirm issue
2. Measure blast radius
3. Isolate request path
4. Compare healthy vs unhealthy
5. Mitigate impact
6. Validate hypothesis
7. Recover safely
8. Prevent recurrence

---

# Senior-Level Debugging Questions

- Is latency global or partial?
- What changed?
- Is this queueing or compute?
- Is p99 elevated or all latency?
- Are retries increasing?
- Are downstreams saturated?
- Is network introducing wait time?

---

# Key Principle

CPU low does not mean healthy.

Systems can still be slow because of:
- IO wait
- blocked threads
- DNS retries
- retransmissions
- queueing
- lock contention
- downstream latency
