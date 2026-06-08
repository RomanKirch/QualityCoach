# Agile Quality Gates

Lightweight, risk-based quality checks. Make quality decisions explicit — not bureaucratic overhead.

## Definition of Ready

- [ ] Acceptance criteria unambiguous enough to drive a test
- [ ] Edge cases, error paths, and object states covered or explicitly deferred
- [ ] "Done" defined so both developer and tester agree
- [ ] Relevant quality characteristics identified (not all eight need to apply)
- [ ] Quality risks briefly discussed: what could go wrong, what is the impact?
- [ ] NFRs stated with a measurable criterion, or marked as open question
- [ ] Test environments and test data known
- [ ] Performance, security, or accessibility testing needs flagged if relevant
- [ ] Compliance requirements understood (GDPR, HIPAA, etc.)

## Definition of Done

- [ ] All functional acceptance criteria met
- [ ] Relevant quality acceptance criteria met, or consciously deferred with documented decision
- [ ] Security, performance, and accessibility checks completed where relevant
- [ ] Known residual risks documented (not silently ignored)
- [ ] Automated checks added where useful
- [ ] Exploratory testing performed where automated coverage is insufficient
- [ ] Code review completed; no new unresolved quality debt introduced silently
- [ ] Monitoring and alerting updated if this feature changes observable system behaviour
- [ ] Evidence of quality checks captured (test results, scan reports, review notes)

## Release Quality Gates

- [ ] All P1/P2 quality acceptance criteria met
- [ ] Performance test confirms SLOs at expected peak load
- [ ] Security scan shows no new High or Critical findings
- [ ] Accessibility scan passes at agreed conformance level
- [ ] Integration and contract tests passing in staging
- [ ] Monitoring and alerting in place for new functionality
- [ ] Rollback plan defined and tested
- [ ] Known residual risks accepted by product owner

---

## Risk-Based Gate Selection

| Risk Level | Trigger | Minimum Gate |
|---|---|---|
| Low | Internal tooling, admin UI, non-critical reporting | DoR: AC defined. DoD: Functional tests pass. |
| Medium | Customer-facing features, integrations, data-modifying ops | DoR: + NFRs checked. DoD: + Exploratory test, observability updated. |
| High | Auth, payments, health/safety data, compliance changes | DoR: + Security review. DoD: + Security scan, performance test, evidence captured. |
| Critical | Safety-critical, regulated, multi-tenant data isolation | Full gate; sign-off from security, architecture, compliance before release. |

---

## Lightweight Conversation Starters

- "Which quality characteristic matters most for this story?"
- "What is the riskiest thing that could go wrong, and how would we know?"
- "Is the acceptance criterion testable, or do we need to add a measure?"
- "Who needs to be involved before this story is ready — security, SRE, accessibility?"