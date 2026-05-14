# Scenario: API Latency Spike

## Situation

Production API latency increases from 80ms to 900ms.

Observations:
- CPU normal
- memory normal
- pods healthy
- error rate low

---

# Investigation Flow

## Step 1: Confirm Blast Radius

Check:
- all APIs affected?
- regional issue?
- specific AZ?
- public or internal only?

---

## Step 2: Compare Healthy vs Unhealthy

Compare:
- nodes
- pods
- request paths
- downstream calls

---

## Step 3: Investigate Hidden Latency Sources

Possible causes:
- TCP retransmits
- DNS intermittency
- MTU mismatch
- queue buildup
- connection pool exhaustion
- blocked threads
- downstream saturation

---

## Step 4: Check Tail Latency

Look at:
- p95
- p99
- retries
- queue depth

---

## Step 5: Mitigate

Possible mitigation:
- rollback
- drain bad node
- scale temporarily
- fail over traffic
- disable expensive feature

---

# Key Learning

Low CPU does not mean healthy.

Latency is usually waiting introduced somewhere in the request lifecycle.
