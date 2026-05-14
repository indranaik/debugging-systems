# Scenario: CPU Normal But System Slow

## Symptoms

- CPU low
- memory healthy
- APIs slow
- intermittent timeouts

---

# Possible Causes

## IO Wait

Processes blocked waiting for disk/network IO.

## Thread Blocking

Application threads waiting on:
- locks
- DB connections
- downstream APIs

## DNS Retries

Slow DNS resolution causing request delay.

## TCP Retransmits

Packet loss introducing retries and latency.

## Queue Buildup

Requests waiting in:
- thread pools
- DB pools
- request queues

---

# Key Principle

Systems fail through waiting and contention, not only high utilization.
