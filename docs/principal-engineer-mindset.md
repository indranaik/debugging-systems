# Principal Engineer Mindset

## Systems Thinking Over Tool Knowledge

Senior and principal engineers do not debug systems by memorizing tools.

They think in:

- bottlenecks
- queueing
- contention
- retries
- saturation
- failure propagation
- latency distribution
- resource exhaustion

---

# Core Principle

When dashboards stop giving obvious answers, real engineering starts.

The question is never:

> Which command should I run?

The real question is:

> Where is time being spent?

---

# How Senior Engineers Think

## Junior Thinking

API slow → restart pods.

## Mid-Level Thinking

Check CPU and memory.

## Senior Thinking

Is latency caused by:
- network wait?
- disk wait?
- queueing?
- retransmits?
- blocked threads?
- downstream saturation?
- lock contention?

## Principal Thinking

What resource is being contended?
What changed?
How do we reduce customer impact FIRST?

---

# Production Reality

Most outages are not crashes.

Most outages are:
- slow systems
- partial failures
- retries
- intermittent latency
- queue buildup
- dependency saturation

---

# Queueing Mindset

Most production latency is waiting.

Examples:
- DB connection queue
- thread pool queue
- request backlog
- Kafka lag
- disk queue
- network buffer queue

Latency is often queueing delay, not execution time.

---

# Mitigation First

During incidents:

Mitigation > Root Cause

Examples:
- rollback deployment
- drain bad node
- fail over traffic
- disable expensive feature
- scale temporarily

Restore service first.
Deep RCA later.
