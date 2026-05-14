# Debugging Systems

## Production Systems Debugging & Principal Engineering Playbook

This repository focuses on how senior/principal DevOps, SRE, Platform, and Distributed Systems engineers think during real production incidents.

Most engineering content teaches tools.
This repository teaches:

- systems thinking
- production debugging
- incident handling
- latency analysis
- distributed systems reasoning
- Linux/network internals
- observability mindset
- queueing and contention analysis
- mitigation-first operations

---

# Core Philosophy

Production engineering is not about memorizing commands.
It is about understanding:

- where time is being spent
- what resource is contended
- where queueing happens
- which dependency is saturated
- how failures propagate
- how to reduce customer impact quickly

---

# Golden Principle

Latency usually means:

> something somewhere is waiting, retrying, blocking, queueing, contending, fragmenting, or timing out.

The job of a principal engineer is to:

1. isolate where wait time is introduced
2. reduce customer impact quickly
3. validate hypotheses systematically
4. recover safely
5. prevent recurrence

---

# Repository Structure

```text
/docs
/scenarios
/commands
/architecture
```

---

# Final Takeaway

Tools change.
Systems principles do not.

The best engineers are not the ones who memorize commands.
They are the ones who can reason clearly under pressure when dashboards stop giving obvious answers.
