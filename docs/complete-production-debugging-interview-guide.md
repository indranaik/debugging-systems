# Complete Production Debugging Interview Guide

## All APIs are slow — where do you start?

First validate blast radius and isolate the request path.

Check:
- load balancer latency
- application latency
- DB latency
- downstream dependencies
- network health

Main goal:
Identify where wait time is introduced.

---

## How do you confirm it’s a real issue and not false alert?

Correlate multiple signals:
- user impact
- p95/p99 latency
- logs
- tracing
- synthetic monitoring
- traffic anomalies

Never trust a single alert blindly.

---

## What metrics do you check first?

Golden signals:
- latency
- traffic
- errors
- saturation

Then:
- p95/p99
- CPU
- memory
- IO
- retransmits
- DB connections
- thread pool usage

---

## What are common causes when all APIs are slow?

Common shared dependencies:
- DB saturation
- Redis latency
- DNS issues
- load balancer problems
- network degradation
- thread pool exhaustion
- downstream API slowness

---

## How do you check if it’s infra vs application?

Compare:
- app processing time
- end-to-end latency

Infra indicators:
- packet loss
- retransmits
- node issues
- DNS failures

Application indicators:
- blocked threads
- slow queries
- GC pauses
- lock contention

---

## What if only 2 out of 10 servers are slow?

Likely:
- bad node
- hardware issue
- noisy neighbor
- uneven traffic
- kernel instability

Compare healthy vs unhealthy nodes.

---

## How do you identify a bad node?

Check:
- iowait
- retransmits
- packet drops
- throttling
- disk latency
- kernel logs

Commands:
- top
- iostat
- sar
- dmesg
- ss -s

---

## What will you check on load balancer?

Check:
- active connections
- uneven traffic
- queue depth
- retries
- TLS handshake latency
- backend health

---

## What happens if traffic is not evenly distributed?

Some nodes become saturated while others idle.

Causes:
- sticky sessions
- hashing imbalance
- stale health checks
- LB routing issues

---

## Which commands do you run first after SSH?

Typical first commands:
- top
- htop
- uptime
- free -m
- iostat -x 1
- sar -n DEV 1
- ss -s
- dmesg

---

## How do you check CPU bottleneck?

Check:
- CPU utilization
- run queue
- throttling
- context switches
- steal time

---

## What does load average mean?

Load average represents:
- runnable tasks
- waiting tasks

Not just CPU usage.

High load with low CPU usually indicates waiting.

---

## High load but low CPU — why?

Possible causes:
- IO wait
- blocked processes
- network waits
- lock contention

Processes are waiting, not computing.

---

## How do you check disk I/O issues?

Use:
- iostat
- iotop
- sar -d

Look for:
- await
- utilization
- queue depth
- latency spikes

---

## What is iowait?

CPU idle time spent waiting for IO operations.

High iowait usually means storage bottleneck.

---

## How do you check memory pressure?

Check:
- available memory
- page faults
- reclaim activity
- swap usage
- OOM kills

---

## What happens if swap is used heavily?

Performance degrades heavily because memory pages move between RAM and disk.

Symptoms:
- latency spikes
- thread stalls
- slow applications

---

## How do you check network connections?

Use:
- ss -s
- netstat
- sar -n TCP

Check:
- retransmits
- resets
- backlog
- connection states

---

## Why do you suspect DB first?

Most applications are data-bound.

Slow DB impacts:
- APIs
- queues
- thread pools
- retries

---

## How do you identify slow queries?

Check:
- slow query logs
- execution plans
- lock waits
- sequential scans

Use EXPLAIN ANALYZE.

---

## What is connection pool exhaustion?

All DB connections become occupied.

New requests wait for free connections.

Symptoms:
- rising latency
- blocked threads
- request timeouts

---

## What if DB CPU is normal but latency high?

Possible causes:
- locks
- replication lag
- slow storage
- network latency
- connection exhaustion

---

## How do you debug external API slowness?

Measure:
- DNS time
- connect time
- TLS handshake
- response latency

Check:
- retries
- upstream incidents
- rate limiting

---

## What if no infra issue is found?

Then investigate:
- blocked threads
- deadlocks
- GC pauses
- queue buildup
- inefficient code
- downstream dependencies

---

## How do you check thread pool exhaustion?

Check:
- active threads
- blocked threads
- queue size
- rejected tasks

---

## What happens when threads are blocked?

Requests pile up.
Queues grow.
Latency increases.

---

## How do you identify deadlocks?

Use thread dumps.

Look for:
- BLOCKED state
- cyclic lock dependencies

---

## Which metrics are most important for latency issues?

Important metrics:
- p95/p99
- retries
- queue depth
- saturation
- thread pool usage
- DB wait time
- retransmits

---

## Difference between p95 and p99 latency?

p95:
95% requests complete within this duration.

p99:
Tail latency.
Represents worst user experience.

---

## Why average latency is misleading?

Averages hide outliers.

Tail latency matters more.

---

## How do you use tracing in debugging?

Tracing shows:
- request lifecycle
- downstream calls
- exact wait time
- slow spans

---

## What will you do first — fix or investigate?

Mitigation first.
RCA second.

Reduce customer impact quickly.

---

## How do you prioritize during incident?

Priority:
1. customer impact
2. restore service
3. contain blast radius
4. communicate
5. RCA

---

## How do you communicate with stakeholders?

Communicate:
- impact
- mitigation status
- ETA if known
- next update timeline

Stay calm and avoid speculation.

---

## When do you decide to rollback?

Rollback when:
- issue correlates with deployment
- rollback risk is lower
- customer impact is significant

---

## What immediate actions will you take?

Possible actions:
- rollback
- scale
- failover
- drain bad node
- rate limiting
- disable expensive feature

---

## When will you scale vs restart?

Scale:
- saturation issue
- traffic increase

Restart:
- deadlock
- memory leak
- stuck process

---

## When will you remove a node from LB?

When node shows:
- packet loss
- high latency
- hardware instability
- inconsistent behavior

---

## What if restart doesn’t fix it?

Then issue is likely:
- systemic
- dependency-related
- network-related
- architectural

---

## All metrics look normal, still latency high — now what?

Investigate:
- retransmits
- MTU mismatch
- DNS intermittency
- queueing
- kernel/socket issues
- tail latency

---

## CPU low, memory fine, but system slow — explain

Possible causes:
- blocked IO
- waiting threads
- DNS retries
- retransmits
- connection exhaustion
- lock contention

---

## Only p99 latency high — what does that mean?

Small percentage of requests experience severe delay.

Usually caused by:
- retries
- intermittent contention
- slow downstreams
- GC pauses

---

## Intermittent latency spikes — how do you debug?

Correlate:
- deployments
- autoscaling
- retransmits
- DNS failures
- traffic bursts
- GC pauses

Need:
- tracing
- timestamps
- high-cardinality metrics

---

## Tell me about a real incident you handled

Good structure:
- situation
- impact
- investigation
- mitigation
- root cause
- prevention

---

## What went wrong?

Focus on:
- technical gaps
- monitoring gaps
- process weaknesses
- architectural assumptions

Avoid blaming individuals.

---

## What did you learn?

Examples:
- improve observability
- better rollback strategy
- stronger alerting
- reduce single points of failure

---

## What did you improve after that?

Examples:
- added tracing
- improved dashboards
- tuned autoscaling
- added runbooks
- improved DB indexes
- added canary deployments

---

# Final Takeaway

Production systems slow down because something somewhere is:
- waiting
- queueing
- retrying
- blocking
- contending
- saturating
- timing out

The job of a principal engineer is to:
- isolate where time is introduced
- reduce customer impact quickly
- validate hypotheses systematically
- recover safely
- prevent recurrence
