# Intermittent Latency War Room Scenario

## Incident Overview

A production e-commerce platform started experiencing intermittent latency spikes during peak evening traffic. Most requests completed normally within 70-90 milliseconds, but every few minutes a subset of requests suddenly jumped to 4-6 seconds. Customers complained that checkout occasionally froze while dashboards still looked mostly healthy.

At first glance, the infrastructure team could not find obvious resource exhaustion. CPU usage remained below 45 percent, memory utilization looked stable, and Kubernetes pods continued passing readiness and liveness checks.

This is the kind of incident where systems thinking becomes more important than dashboard reading.

---

## Initial Investigation

The first step was not restarting services blindly. The incident commander focused on understanding the blast radius.

Questions asked immediately:

- Is the issue global or regional?
- Does it affect all APIs or only checkout?
- Are internal service calls slow too?
- Is p99 latency affected while p50 remains healthy?
- Did any deployment happen recently?

The team compared healthy requests against slow requests using distributed tracing.

That comparison revealed something critical:

Most application processing times remained normal, but network wait time between services occasionally increased dramatically.

---

## Deep Investigation

The engineers then shifted focus toward hidden infrastructure latency.

They checked:

- TCP retransmissions
- DNS latency
- connection retries
- Kubernetes node networking
- conntrack usage
- packet drops
- load balancer behavior

One node consistently showed higher retransmissions than the others.

Even though the node still looked healthy from Kubernetes health checks, packet retransmissions caused intermittent delays during service-to-service communication.

This explained why:

- CPU looked healthy
- memory looked healthy
- pods appeared healthy
- but customers still experienced severe latency spikes

---

## Mitigation

The node was drained from the cluster and removed from the load balancer.

Latency immediately stabilized.

Only after customer impact was reduced did the team continue deep root-cause analysis.

---

## Root Cause

The final root cause involved a networking issue causing intermittent packet loss on a specific node. Retransmissions introduced hidden latency that traditional dashboards did not expose clearly.

---

## Lessons Learned

The incident reinforced several important production engineering principles:

- low CPU does not mean healthy systems
- intermittent failures are harder than hard outages
- queueing and retries often create hidden latency
- tail latency matters more than averages
- comparison-based debugging is extremely effective
- mitigation must happen before deep RCA

---

## Principal Engineering Takeaway

Strong engineers do not panic when dashboards stop giving obvious answers.

They systematically isolate layers, validate hypotheses, compare healthy vs unhealthy behavior, and reduce customer impact while continuing investigation.
