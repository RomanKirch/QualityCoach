# Architecture Quality Attributes

A quality requirement is architecturally significant when satisfying it requires a specific
deployment topology, communication pattern, structural decision, or a trade-off that cannot
be reversed cheaply.

## Architecture Drivers by Quality Attribute

| Attribute | Architectural Concerns | Possible Tactics | Evidence Needed |
|---|---|---|---|
| Performance | Response time budget, bottlenecks, resource contention | Caching, CDN, load balancing, async processing, read replicas | Load test results; p95/p99; resource utilisation under peak |
| Reliability | Single points of failure, dependency failure propagation, data durability | Redundancy, failover, circuit breaker, bulkhead, retry with backoff | Failover test; chaos results; SLO burn rate; tested RTO/RPO |
| Security | Trust boundaries, identity management, data protection, secrets | Least-privilege, mTLS, secrets manager, API gateway, encryption | Pen test; OWASP scan; access control test; audit log review |
| Maintainability | Coupling, testability, deployment granularity | Modularisation, dependency injection, API versioning, testing gates | Code metrics; change lead time; onboarding time |
| Scalability | Statelessness, partitioning, horizontal scaling limits | Stateless services, sharding, message queuing, autoscaling | Capacity test; queue depth metrics; autoscaling behaviour |
| Usability | Latency perception, error handling UX, accessibility | Progressive loading, optimistic UI, ARIA-compliant components | Usability test; Lighthouse; axe scan |
| Compatibility | API contract stability, versioning, data format evolution | Versioned APIs, consumer-driven contract tests, schema registry | Contract test results; API changelog |
| Portability | Platform dependencies, environment configuration, infrastructure | Containerisation, IaC, 12-factor app, environment parity | Deployment test; IaC validation |
| Recoverability | Backup strategy, replication lag, restore procedure | Point-in-time backup, geo-replication, automated restore pipeline | Quarterly restore test; measured RTO/RPO; DR runbook |
| Observability | Log completeness, metric coverage, trace propagation, alert coverage | Structured logging, metrics pipeline, distributed tracing (OpenTelemetry) | Log check; alert fire test; trace coverage |

---

## Trade-off Awareness

| Trade-off | Tension |
|---|---|
| Performance vs. Security | Encryption adds latency; aggressive caching can expose cross-tenant data |
| Reliability vs. Cost | Redundancy and multi-region failover are expensive; the business sets the SLO |
| Maintainability vs. Performance | Abstractions improve maintainability but can add overhead |
| Portability vs. Platform Optimisation | Managed cloud services improve DX but create lock-in |
| Consistency vs. Availability | Strong consistency often reduces availability (CAP theorem) |
| Security vs. Usability | MFA and session expiry create friction for users |
| Test Depth vs. Delivery Speed | Comprehensive gates slow pipelines; risk-based selection is necessary |

---

## Architecture Review Questions

Performance: Where are bottlenecks under peak load? Does caching risk cross-tenant leakage?
Reliability: What are single points of failure? How does the system behave when service X is down?
Security: Where are trust boundaries? How are secrets managed? How is authorisation enforced?
Maintainability: Can module X change without affecting Y? Can a new developer safely change this?
Scalability: What is the capacity ceiling? Are services stateless? How does a 10x spike behave?
Observability: Can you diagnose a production incident from logs and traces alone?