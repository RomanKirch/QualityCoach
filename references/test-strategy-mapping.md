# Test Strategy Mapping

| Characteristic | Primary Test Approaches | Required Evidence | Common Blind Spot |
|---|---|---|---|
| Functional Suitability | Functional testing, exploratory, UAT | Test results, defect log, UAT sign-off | Missing edge cases; wrong spec accepted as correct |
| Performance Efficiency | Load, stress, capacity, endurance testing | Load test report with p95/p99, resource utilisation | Testing with non-production data volumes |
| Reliability | Resilience, failover, chaos engineering, backup/restore | Uptime metrics, failover results, RTO/RPO measurement | No failure injection; assuming monitoring equals testing |
| Security | Security testing, pen test, OWASP scan, SAST, access control | Pen test report, OWASP scan, audit log review | No threat model; skipping IDOR boundary tests |
| Usability | Usability testing, accessibility testing (WCAG), user interviews | Test observations, axe scan, task completion rates | Asking devs to evaluate usability; skipping accessibility |
| Compatibility | API contract testing, integration testing, environment validation | Contract test results, integration report, platform matrix | Assuming contracts are stable without contract tests |
| Maintainability | Code review, static analysis, architecture review, coverage | Code metrics, complexity scores, change lead time | Measuring coverage without checking what is covered |
| Portability | Deployment validation, environment migration, IaC validation | Deployment test results, environment comparison | Assuming it works in dev; environment secrets in code |

## Test Approach Definitions

| Approach | Purpose |
|---|---|
| Load testing | Verify performance targets under expected peak load |
| Stress testing | Find system behaviour and breaking point beyond normal load |
| Chaos engineering | Inject random failures to find unknown weaknesses |
| API contract testing | Verify service interfaces conform to agreed contracts |
| Accessibility testing | Verify WCAG 2.1 AA or agreed accessibility standard |
| Operational readiness | Verify monitoring, alerting, runbooks before go-live |

## Common Blind Spots

Performance: Small datasets; no concurrent load; average not percentiles; ignoring downstream latency.
Security: No threat model; testing auth but not authz; no IDOR test; skipping secrets review.
Reliability: No failure injection; backup never tested for restore; recovery path not tested.
Usability: Not observing real users; skipping accessibility because "no one asked."
Observability: Deploying monitoring without testing alerts fire; no runbook for alert response.