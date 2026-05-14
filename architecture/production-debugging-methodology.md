# Production Debugging Methodology

## Core Principle

Production debugging is the process of identifying where wait time or failure is introduced inside a distributed system.

---

# Standard Debugging Flow

## 1. Confirm Issue

Validate:
- customer impact
- latency increase
- error rates
- blast radius

---

## 2. Identify Scope

Questions:
- all services affected?
- specific region?
- specific node?
- internal or public?

---

## 3. Isolate Layers

Break request path into:
- client
- load balancer
- application
- database
- downstream dependencies
- network

---

## 4. Compare Healthy vs Unhealthy

Golden debugging technique.

Compare:
- nodes
- pods
- requests
- traces
- latency distributions

---

## 5. Mitigate Blast Radius

Mitigation examples:
- rollback
- failover
- drain bad node
- scale out
- disable expensive features

---

## 6. Validate Hypothesis

Use:
- metrics
- logs
- traces
- packet captures
- thread dumps

Never assume without evidence.

---

## 7. Prevent Recurrence

Improve:
- observability
- alerts
- runbooks
- resiliency
- automation

---

# Principal Engineering Mindset

A principal engineer thinks in:
- queueing
- contention
- retries
- saturation
- blast radius
- customer impact
- distributed failure patterns
