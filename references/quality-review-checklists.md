# Quality Review Checklists

Coaching questions per characteristic. Use in requirements reviews, 3 Amigos sessions,
refinement, or architecture reviews.

## Functional Suitability
- Does the requirement describe what, not how?
- What happens in the error path? Is every failure case defined?
- Are all distinct object states covered (active, locked, suspended, archived)?
- Is "done" unambiguous enough to drive a test?

## Performance Efficiency
- What are the most critical user journeys from a response-time perspective?
- What load profile is expected now, in 6 months, in 2 years?
- Is there a defined SLO for response time and throughput?
- Has performance been tested with production-representative data volumes?

## Reliability
- What are the most important failure modes?
- How does the system behave when a dependency is unavailable?
- Has the RPO and RTO been defined and tested?
- Is there a graceful degradation path, or is failure binary?

## Security
- What assets or data need protection?
- How are authentication and authorisation enforced and tested?
- Are there IDOR risks (User A accessing User B data by manipulating an ID)?
- How are secrets managed? Are any in version control?
- What compliance requirements apply (GDPR, HIPAA, PCI-DSS)?

## Usability
- Who are the primary users, and what is their skill level?
- Where can users make a hard-to-recover mistake?
- Have real users been observed using this feature?
- Are error messages actionable — do they tell the user what to do next?

## Compatibility
- Which external systems, APIs, browsers, or platforms must be supported?
- Are contract tests in place for consumer-provider integrations?

## Maintainability
- Which parts are expected to change most frequently?
- Can a new developer safely change this module without deep system knowledge?
- Are code quality gates enforced in CI?

## Portability
- Are environment-specific settings externalised?
- Has the application been validated in all target environments?

## Observability (cross-cutting)
- Are structured logs emitted for key events with a correlation ID?
- Can a production incident be diagnosed from logs and traces alone?
- Has alerting been tested — does the alert actually fire?

---

## Workshop Facilitation Prompts

- "Which quality failure would hurt us most?"
- "Which quality attribute is assumed but not written down anywhere?"
- "Which trade-off do we need to decide explicitly — and who owns that decision?"
- "What would a user say if this feature worked as specified but still felt wrong?"