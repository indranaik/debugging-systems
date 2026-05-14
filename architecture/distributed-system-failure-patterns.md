# Distributed System Failure Patterns

## Introduction

Distributed systems rarely fail in obvious ways.

Most production failures are not complete outages where servers crash immediately. Instead, modern distributed systems often degrade slowly through retries, queue buildup, contention, dependency saturation, and latency amplification.

Understanding these patterns is what separates experienced production engineers from engineers who only rely on dashboards.

---

## Retry Storms

Retries are useful during temporary failures, but excessive retries can amplify outages.

For example, if a downstream database becomes slightly slow, upstream services may retry aggressively. Those retries increase load further, which slows the database even more. Eventually the entire platform experiences cascading latency.

This is why retry policies, circuit breakers, and timeout management are critical in distributed systems.

---

## Queue Buildup

Most latency problems are queueing problems.

When requests arrive faster than systems can process them, queues begin forming:

- request queues
- DB connection queues
- thread pool queues
- Kafka lag
- network buffer queues

Initially systems still appear healthy, but latency grows rapidly because requests spend most of their time waiting.

---

## Partial Failures

Distributed systems often fail partially instead of completely.

Examples:

- only one region affected
- only specific APIs failing
- only p99 latency increasing
- only some nodes behaving poorly

Partial failures are difficult because dashboards may still appear mostly healthy while customers experience severe issues.

---

## Slow Dependency Propagation

A single slow dependency can degrade the entire platform.

For example:

- slow database
- slow DNS
- external API latency
- authentication provider delay

These issues propagate through retries, blocked threads, and connection pool exhaustion.

---

## Tail Latency Amplification

Tail latency is one of the most important distributed systems concepts.

Even if average latency looks healthy, a small percentage of slow requests can severely impact customer experience.

Tail latency often reveals:

- intermittent contention
- retries
- uneven load balancing
- garbage collection pauses
- downstream instability

---

## Operational Takeaway

Distributed systems debugging is fundamentally about understanding:

- where waiting occurs
- which dependency is saturated
- how failures propagate
- how retries amplify load
- how contention builds gradually

The best engineers think in systems behavior, not individual commands.
