# Quality Attribute Scenarios

Make abstract quality requirements concrete and testable. Especially valuable for
architecture-relevant attributes that drive design decisions.

## Six-Part Scenario Structure

| Part | Question | Example |
|---|---|---|
| Source of stimulus | Who or what triggers the event? | End user / External system / Attacker |
| Stimulus | What happens? | Searches / Sends malformed request / Load spike |
| Environment | Under what conditions? | Normal hours / Peak load / After node failure |
| Artifact | What part of the system? | Search service / Payment API / Auth module |
| Expected response | What should happen? | Return results / Reject / Degrade gracefully |
| Response measure | How do we know it is good enough? | p95 < 300 ms / HTTP 401 / Recovery < 60 s |

---

## Examples by ISO 25010 Dimension

### Performance Efficiency
Source: End user | Stimulus: Customer search | Environment: Normal hours, 500 concurrent users
Artifact: Search service | Response: Results returned | Measure: p95 < 300 ms; p99 < 800 ms

Source: Batch scheduler | Stimulus: Nightly invoice generation, 200k customers | Environment: Off-peak
Artifact: Invoice service | Response: All invoices generated | Measure: < 4 hours; no duplicates

### Reliability
Source: Infrastructure failure | Stimulus: Primary database unreachable | Environment: Normal hours
Artifact: Order management | Response: Switches to replica; requests continue
Measure: Failover < 60 s; zero orders lost

Source: Dependent service | Stimulus: Payment gateway HTTP 503 for 5 min | Environment: Peak checkout
Artifact: Checkout service | Response: Transactions queued; user sees retry message
Measure: All queued transactions processed within 10 min of recovery; zero data loss

### Security
Source: Unauthenticated caller | Stimulus: Request to protected endpoint without token
Environment: Production | Artifact: API gateway | Response: Request rejected
Measure: HTTP 401; no internal details exposed; event logged

Source: Authenticated user Tenant A | Stimulus: Accesses Tenant B resource by manipulating ID
Environment: Multi-tenant SaaS | Artifact: Access control | Response: Request rejected
Measure: HTTP 403; IDOR attempt logged; automated IDOR test passes

### Usability
Source: First-time user | Stimulus: Completes account registration | Environment: Standard browser
Artifact: Registration flow | Response: User succeeds
Measure: >= 90% task completion (n=5); median <= 5 min; error rate < 2 per session

### Maintainability
Source: Dev team | Stimulus: New payment provider integration | Environment: Active codebase
Artifact: Payment module | Response: Added without changes to order mgmt or UI
Measure: Confirmed by architecture review; no unintended dependencies (static analysis)

### Recoverability
Source: Operator | Stimulus: Restore from backup after data corruption
Artifact: Customer data store | Response: Restored to last valid state; application functional
Measure: RTO <= 1 h; RPO <= 15 min; tested quarterly

---

## When to Use Scenarios

- A quality requirement drives significant architecture decisions
- A trade-off between quality attributes must be made explicit
- Team disagrees on what "good enough" means
- Preparing evidence-backed acceptance criteria for NFRs
- Architecture review or quality workshop preparation