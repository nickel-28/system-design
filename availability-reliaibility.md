# Availability & Reliability

These two words get used interchangeably but mean different things in
interviews — being precise about them signals seniority.

## Availability
The percentage of time a system is operational and able to serve
requests. Usually expressed in "nines."

| Availability | Downtime / year | Downtime / month |
|---|---|---|
| 99% ("two nines") | 3.65 days | 7.2 hours |
| 99.9% ("three nines") | 8.7 hours | 43.2 min |
| 99.99% ("four nines") | 52.6 min | 4.3 min |
| 99.999% ("five nines") | 5.3 min | 26 sec |

**How to increase availability**
- Redundancy — no single point of failure (multiple servers, multi-AZ, multi-region)
- Failover — automatic detection + rerouting when a node dies
- Graceful degradation — serve a reduced experience instead of erroring out
- Health checks + auto-healing

### Availability in series vs parallel
```mermaid
graph LR
    subgraph Series (dependent) — availability multiplies
    A1[Service A<br/>99.9%] --> A2[Service B<br/>99.9%]
    end
```
Two 99.9% services chained in series → overall availability ≈ 99.8%
(0.999 × 0.999). Chaining dependencies **reduces** overall availability —
this is why deep synchronous call chains are risky.

```mermaid
graph LR
    subgraph Parallel (redundant) — availability improves
    R[Request] --> B1[Replica 1<br/>99.9%]
    R --> B2[Replica 2<br/>99.9%]
    end
```
Two 99.9% replicas in parallel (only one needs to succeed) →
1 − (0.001 × 0.001) = 99.9999% availability.

## Reliability
The probability a system performs **correctly** for a given time period —
i.e., it doesn't just respond, it responds with the right answer and
doesn't lose or corrupt data. A system can be available (responding fast)
but unreliable (returning wrong/stale/corrupted results).

**How to increase reliability**
- Redundancy + replication of data (no data loss on node failure)
- Checksums / data validation
- Idempotent operations (safe retries)
- Comprehensive testing, canary deploys, chaos engineering

## SLA / SLO / SLI
- **SLI** (Indicator): the actual measured metric, e.g., "99.95% of
  requests succeeded in the last 30 days."
- **SLO** (Objective): the internal target, e.g., "99.9% success rate."
- **SLA** (Agreement): the external, often contractual, promise to
  customers — usually looser than the SLO, with penalties if breached.

## Fault tolerance vs high availability
- **Fault tolerance**: system keeps working correctly even when
  components fail (no interruption at all — e.g., RAID, replicated state
  machines).
- **High availability**: system recovers *quickly* from failure (brief
  interruption acceptable, e.g., failover taking a few seconds).

## Interview tip
When asked "how would you make this highly available," don't just say
"add redundancy." Name the specific single points of failure in your
design (load balancer, DB primary, cache node) and how each is made
redundant (e.g., active-passive LB pair with a floating IP, DB
primary-replica with automatic failover, cache cluster with replicas).

## Related
- [CAP theorem](cap-theorem.md)
- [Replication](../02-building-blocks/replication.md)
- [Load balancing](../02-building-blocks/load-balancing.md)