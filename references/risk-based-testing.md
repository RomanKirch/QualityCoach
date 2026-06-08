# Risk-Based Testing

Use this guide when testing effort must be prioritised. Risk-based testing means test analysis,
design, execution, and reporting are guided by product risk — you spend effort where failure
would hurt most and is most likely, not evenly across all features.

## Product Risk Model

Assess each risk along these dimensions:

| Dimension | Question |
|---|---|
| Impact | How bad would the failure be? |
| Likelihood | How likely is the failure? |
| Detectability | How easily would we notice it? |
| Controllability | Can users or operations recover? |
| Exposure | How often is the feature used? |
| Complexity | How technically or logically complex is it? |
| Change | How much has recently changed? |
| Defect history | Has this area failed before? |
| Compliance | Are there legal, regulatory, or audit consequences? |
| Reputation | Would failure damage trust? |

## Simple Risk Score

Use a lightweight scale to keep the conversation moving:

```
Impact:      1-5
Likelihood:  1-5
Risk Score = Impact x Likelihood   (range 1-25)
```

Treat the score as a conversation tool, not a precise metric. Two people scoring the same risk
differently is a signal worth discussing — it usually means a hidden assumption.

| Risk Score | Testing Response |
|---|---|
| 15-25 (High) | Deep, deliberate testing. Multiple techniques. Automated regression. Possibly pen test / load test / chaos test depending on the attribute. |
| 6-14 (Medium) | Targeted testing of the main risk. One or two techniques. Some automation. |
| 1-5 (Low) | Light touch. Smoke test or exploratory pass. Do not over-invest. |

## Connecting Risk to Quality Attributes

Each risk usually maps to one or more ISO 25010 characteristics. Name the characteristic so the
right verification approach follows naturally:
- Reputation + Exposure risk on a login flow -> Reliability + Security
- Compliance risk on data export -> Security (accountability/audit) + Functional Suitability
- Complexity + Change risk on a pricing engine -> Functional Suitability (correctness) + Maintainability

See `references/test-strategy-mapping.md` for the characteristic-to-test-approach mapping, and
`references/test-design-techniques.md` for choosing the technique within an approach.

## Risk-Based Testing in a Workshop

Risk identification is best done collaboratively (Risk Storming, 3 Amigos). Useful prompts:
- "Which failure would hurt us most — and how likely is it really?"
- "Where would we notice a failure too late to recover?"
- "What changed recently that we have not re-tested?"
- "Which area has burned us before?"
- "What carries compliance or reputational consequences?"

## Coaching Rules

- Prioritise by risk, not by feature count or by what is easy to test.
- Make the risk explicit before designing tests — every test should reduce a named risk.
- Re-assess risk when the system changes; risk is not static.
- Do not over-test low-risk areas to feel thorough — that effort is better spent on high-risk areas.
- A high-risk area with no test coverage is a finding worth escalating, not a quiet gap.