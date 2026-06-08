# Test Design Techniques

Use this reference when the user asks for test design, test cases, test ideas, test coverage,
test techniques, or how to verify requirements.

> This reference is inspired by common ISTQB Foundation Level testing concepts but must NOT
> reproduce official ISTQB syllabus text. Use it as practical coaching guidance in your own words.

## Core Rule — Do Not Jump to Test Cases

Do not start by writing test cases immediately. First understand:

1. What is being tested?
2. What risk should the tests reduce? (see `references/risk-based-testing.md`)
3. What information is available?
4. Which quality attribute or requirement is involved?
5. Which test level is appropriate (unit, integration, system, acceptance)?
6. Which test technique fits the situation?
7. What evidence is needed?

The goal is not to maximise the number of test cases. The goal is to select techniques that
provide useful evidence against relevant risks.

---

## Technique Categories

**Black-box** — derived from requirements, specifications, business rules, interfaces, workflows,
or expected behaviour:
Equivalence partitioning · Boundary value analysis · Decision table testing · State transition
testing · Use case testing · Acceptance-criteria-based testing · Pairwise / combinatorial testing

**White-box** — derived from structure, code, logic, control flow, data flow:
Statement coverage · Branch / decision coverage · Path-oriented thinking · Condition coverage ·
Code-review-supported test design

**Experience-based** — when specifications are weak, risks uncertain, or expert knowledge matters:
Exploratory testing · Error guessing · Checklist-based testing · Session-based testing ·
Defect-taxonomy-based testing · Attack-based testing (security)

**Collaboration-based** — when shared understanding matters:
Example mapping · Specification by example · ATDD · Three Amigos · Story refinement with
testability focus

---

## Selection Heuristic

Ask: Is the input space large? Are there clear boundaries? Are there business-rule combinations?
Does behaviour depend on state? Is there a realistic user workflow? Is implementation logic
important? Are requirements incomplete? What is the risk type (functional, technical, security,
usability, operational)? What test level fits? What evidence is needed?

## Technique Decision Table

| If the problem has... | Use primarily... | Combine with... |
|---|---|---|
| Many input values groupable into valid/invalid classes | Equivalence partitioning | Boundary value analysis |
| Ranges, limits, dates, sizes | Boundary value analysis | Equivalence partitioning |
| Complex business-rule combinations | Decision table testing | Example mapping |
| Statuses and lifecycle changes | State transition testing | Negative transition tests |
| User journeys / business processes | Use case testing | Exploratory testing |
| Many configuration combinations | Pairwise / combinatorial testing | Risk-based prioritisation |
| Complex or safety-critical code logic | White-box techniques | Code review, black-box tests |
| Weak or ambiguous specifications | Exploratory testing | Checklist-based testing |
| Known defect history | Error guessing / defect taxonomy | Regression testing |
| Agile story refinement | Example mapping | Acceptance test design |
| Integration contracts | Contract testing | Boundary and negative tests |
| Non-functional concern | Specific verification method | Monitoring or review evidence |

---

## Key Techniques in Brief

**Equivalence partitioning** — divide input/output into groups handled the same way; test one
representative per group. Ask: valid partitions? invalid partitions? special values? hidden
business partitions? Are roles, states, or configurations also partitions?

**Boundary value analysis** — defects cluster at edges. Test on and just outside each boundary
(e.g. for "age >= 18": 17, 18, 19; plus missing and non-numeric).

**Decision table testing** — enumerate combinations of conditions and their expected outcomes.
Makes rule interactions explicit and surfaces undefined combinations.

**State transition testing** — model valid states and transitions; test valid transitions AND
invalid ones (attempting a transition that should be blocked).

**Use case testing** — exercise a realistic end-to-end workflow, including alternate and exception
flows, not just the happy path.

**Exploratory testing** — time-boxed, charter-driven investigation to find unknown risks and
clarify behaviour where the spec is weak.

---

## Output Recommendation Format

When recommending a test design approach, answer with:

```
Recommended technique:
Why it fits:
What it covers:
What it misses:
Example test ideas:
Open questions:
```

Always state **what it misses** — no single technique is complete. Naming the gap tells the team
where to add a complementary technique or accept a residual risk.