# Quality Requirement Patterns

## NFR Evaluation Dimensions

For each NFR, assess these ten dimensions:

| Dimension | Good Signal | Weak Signal | Coaching Question |
|---|---|---|---|
| Clarity | Understandable without hidden assumptions | Vague words: fast, secure, intuitive | What exactly, for whom, under which condition? |
| Scope | Affected component is named | Applies to the whole system | Which feature, journey, API, or process? |
| Context | Operating conditions defined | No load, environment, or failure condition | Under which conditions must this quality be achieved? |
| Observability | Expected response can be observed | Describes abstract property only | What would we see if this is met or violated? |
| Measurability | Includes threshold, target, or evidence type | No acceptance threshold | How will we know it is good enough? |
| Testability | A verification method is possible | No test, review, or monitoring approach | How can we verify this before or after release? |
| Risk Relevance | Linked to user, business, or compliance risk | Included because "quality is important" | What risk does this requirement reduce? |
| Feasibility | Can plausibly be achieved | Conflicts with architecture, budget, timeline | What design or cost implications does this create? |
| Trade-off Awareness | Possible conflicts are known | Assumes all qualities can be maximised | What may become worse if we optimise this quality? |
| Ownership | Someone can decide, implement, verify, or accept | No accountable stakeholder | Who can decide whether this is good enough? |

---

## NFR Quality Rating

| Rating | Meaning | Action |
|---|---|---|
| A | Clear, measurable, testable, risk-based, and owned | Keep and use as quality criterion |
| B | Mostly clear but missing one or two details | Improve before implementation or testing |
| C | Useful direction but not yet testable | Refine with stakeholders |
| D | Vague, generic, or not verifiable | Rewrite before use |
| E | Misleading, unrealistic, or solution-biased | Challenge and replace |

---

## NFR Review Output Format

When reviewing existing NFRs:

| Original NFR | Rating | Issue | Improved Version | Verification Method | Open Questions |
|---|---|---|---|---|---|
| "The system must be fast." | D | No scope, load, or threshold | "For customer search, under normal load, 95% of requests return results within 300 ms." | Load test with p95 assertion | What is the expected concurrent user count? |

---

## NFR Refinement Template

```
Quality concern:            [What quality dimension?]
Affected users/components:  [Who or what is affected?]
Business or risk rationale: [What risk does this reduce?]
Operating context:          [Load, environment, failure condition]
Expected behavior:          [What should the system do?]
Response measure:           [Threshold, target, or range]
Verification method:        [Test, review, analysis, or monitoring]
Acceptance threshold:       [When is it good enough?]
Owner:                      [Who decides this is acceptable?]
Open questions:             [What must be resolved before implementation?]
Trade-offs:                 [What might get worse if this is optimised?]
```

---

## Writing Patterns

Condition-based: Under [condition], [system] shall [response] within [measure].
User-task-based: For [user], [task] completed with [success criterion] under [context].
Failure-based: When [failure] occurs, [system] shall [recover/degrade] within [limit].
Change-based: For [change type], [team] shall implement and verify within [constraint].

---

## Anti-patterns and Rewrites

| Anti-pattern | Why it fails | Better version |
|---|---|---|
| "The system shall be fast." | No journey, threshold, or load | "Under normal load, 95% of customer search requests return results within 300 ms." |
| "The solution must be scalable." | No dimension, target, or timeline | "Shall support growth from 10k to 100k users in 18 months without architectural redesign." |
| "The UI must be intuitive." | Not observable or measurable | "New users complete registration in <= 5 min; task-completion >= 90% (usability test, n=5)." |
| "The system must be secure." | No scope, threat, or evidence | "All endpoints require auth; OWASP Top 10 passes with zero High/Critical before each release." |
| "We need high availability." | No target, scope, or failure mode | "Login service >= 99.9%/month; auto-recovery from single-node failure within 60 s." |
| "The system must be robust." | No context | "When payment gateway unavailable, checkout queues transactions without data loss." |
| "The code must be maintainable." | No change context | "For business-rule changes, developer implements with localised modifications, no unintended impact." |

---

## Separation of Concerns

| Layer | Question | Example |
|---|---|---|
| Quality goal | What outcome matters? | Users trust the system to be available. |
| Quality requirement | What must be true? | Availability >= 99.9%/month. |
| Quality scenario | How is it exercised? | User places order during peak; system responds. |
| Design response | How might it be satisfied? | Active-passive failover, health checks every 30 s. |
| Test idea | How can it be verified? | Chaos test: kill primary node; measure recovery. |
| Metric | How is it monitored? | SLO dashboard tracking error budget burn rate. |
| Acceptance criterion | When is it good enough? | Zero violations > 10 min in past 30 days. |