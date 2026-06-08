# HQM Quality Coach

A Claude skill that helps software teams turn vague requirements into **high-quality, verifiable,
testable** quality requirements, quality attributes, and test strategies. It is grounded in the
**Holistic Quality Model (HQM)** — product quality emerges from the interaction of **Product**
(ISO/IEC 25010), **Process**, **People**, and **Values**.

## What it does

- **Reviews requirements & user stories** for quality gaps across the eight ISO 25010 characteristics
- **Challenges vague words** (fast, secure, scalable, robust…) and rewrites them into measurable criteria
- **Rates and improves existing NFRs** (A–E rating, 10 evaluation dimensions, refinement template)
- **Designs risk-based test strategies** — names the product risk first, then picks fitting test
  techniques and states what each one *misses*
- **Right-sizes itself**: it first estimates the risk of the change (Light / Standard / Deep) and
  scales its depth accordingly, so a trivial UI tweak gets a short answer and a payment flow gets
  the full treatment

## Installation

Copy the `hqm-quality-coach` folder into your personal Claude skills directory:

| OS | Path |
|---|---|
| Windows | `C:\Users\<you>\.claude\skills\hqm-quality-coach\` |
| macOS / Linux | `~/.claude/skills/hqm-quality-coach/` |

Then restart Claude Code (or reload the window). The skill triggers automatically — no manual command needed.

## Example prompts

- "Review this user story for quality: *As a user I want to log in so I can see my dashboard.*"
- "Rate these NFRs and tell me which ones to rewrite."
- "What quality attributes apply to a multi-tenant document export feature?"
- "How should we test this feature? Give me a risk-based test approach."
- "Help me prepare a Risk Storming session for our checkout redesign."

## Structure

```
hqm-quality-coach/
├── SKILL.md                  # behaviour, workflow, navigation
└── references/               # loaded on demand
    ├── iso25010.md
    ├── quality-requirement-patterns.md
    ├── quality-attribute-scenarios.md
    ├── test-strategy-mapping.md
    ├── test-design-techniques.md
    ├── risk-based-testing.md
    ├── architecture-quality-attributes.md
    ├── quality-review-checklists.md
    └── agile-quality-gates.md
```

## Note on ISO 25010

This skill describes ISO/IEC 25010 concepts in its own words for coaching purposes. It deliberately
does **not** reproduce the proprietary normative text of the standard.

---

*Created by Roman Kirchmeier. Based on the Holistic Quality Model.*
