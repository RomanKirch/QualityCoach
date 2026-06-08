# Output Templates

Concrete templates for each output mode. The Executive Review is the default. Keep German output if
the input is German. Prefer the most visually readable form that the environment renders — in chat
that is **markdown tables + emoji badges** (raw HTML is not rendered in chat; use HTML cards only
inside an artifact/canvas).

---

## 1. Executive Review Template (DEFAULT)

```markdown
# Feature Evaluation: [Feature Name]
[System / Product] · [Review Context] · [Reviewer if provided]

## Überblick

| Gesamtbewertung | Testbarkeit |
|---|---|
| **[Solide – mit Lücken]** | **[4 / 6 AK klar testbar]** |

| Kritischste Lücke | Empfohlene Entscheidung |
|---|---|
| **[AK04 – Change Propagation]** | **[Ready with conditions]** |

## Akzeptanzkriterien – Bewertung

### [AK01 – kurzer Titel]
**Status:** ✅ Klar
**Bewertung:** [ein Satz]
**Testbarkeit:** [ein Satz]
**Fehlt:** [knapp, oder „—"]
**Verbesserung:** [knapp, oder „—"]

### [AK04 – kurzer Titel]
**Status:** ❌ Kritisch
**Bewertung:** [ein Satz]
**Testbarkeit:** [ein Satz]
**Fehlt:** [knapp]
**Verbesserung:** [knapp]

## Identifizierte Qualitätslücken

| Prio | ISO 25010 | HQM Lens | Gap | Empfohlene Massnahme |
|---|---|---|---|---|
| P1 | Security / Confidentiality | Product | [gap] | [action] |
| P1 | Functional / Correctness | Product + Process | [gap] | [action] |

## NFR-Vorschläge

| Prio | Qualität | NFR | Messbares Kriterium | Verifikation |
|---|---|---|---|---|
| P1 | Security | [NFR] | [threshold] | [method] |

## Top 3 Blocking Questions

1. [design/test-blocking decision]
2. [design/test-blocking decision]
3. [design/test-blocking decision]

*Weitere offene Fragen:* [one line, optional]

## MVP Readiness

**Decision:** [Ready / Ready with conditions / Needs refinement / Not ready]
[2-3 Sätze Begründung. Welche Bedingungen müssen erfüllt sein?]

## Nächste mögliche Schritte

`🧪 Testplan für kritische Lücken erstellen`
`✍️ Akzeptanzkriterien verfeinern`
`📋 NFR-Backlog-Items generieren`
`👥 3-Amigos-Refinement vorbereiten`
`✅ Quality Gate Checkliste erstellen`
```

### Status badge legend (use exactly these)
- `✅ Klar` — clear, testable as written
- `⚠️ Unklar` — ambiguous; needs clarification
- `🟡 Schwach` — directionally ok but weak/incomplete
- `❌ Kritisch` — blocking; not testable / risk-bearing as written

### Dashboard — optional HTML (only inside an artifact, never plain chat)

```html
<div class="dashboard">
  <div class="card"><div class="label">Gesamtbewertung</div><div class="value">Solide – mit Lücken</div></div>
  <div class="card"><div class="label">Testbarkeit</div><div class="value">4 / 6 AK klar testbar</div></div>
  <div class="card"><div class="label">Kritischste Lücke</div><div class="value">AK04 – Change Propagation</div></div>
  <div class="card"><div class="label">Empfohlene Entscheidung</div><div class="value">Ready with conditions</div></div>
</div>
```

---

## 2. Detailed Review Template

Used only when the user explicitly asks for a deep/detailed/full report. Same analytical content as
the Executive Review, expanded:

```markdown
# [Feature] — Detailed Quality Review

## Verdict (1 Zeile)
## Context Summary (2-3 Sätze)
## Akzeptanzkriterien – Bewertung   (badges, all ACs)
## Identifizierte Qualitätslücken   (full table incl. Owner column)
## NFR-Vorschläge                    (full table)
## Acceptance Criteria to Add        (Given/When/Then, P1/P2)
## Verification Approach             (grouped by risk; technique named; Automated/Manual; one monitoring)
## Architecture Implications         (only if design-driving)
## Risks & Assumptions
## HQM Observations (Process / People / Values)
## Open Questions for Refinement     (P1 first)
## Hints by Role                     (PO / Dev / Tester / Architect / SRE — only where non-obvious)
## Next Steps — pick one
```

---

## 3. Acceptance Criteria Review Template

```markdown
### [AK-ID – Titel]
**Status:** [✅ Klar | ⚠️ Unklar | 🟡 Schwach | ❌ Kritisch]
**Bewertung:** [one line — is it concrete?]
**Testbarkeit:** [can it drive a test as written?]
**Fehlt:** [the specific missing element]
**Verbesserung:** [the concrete rewrite direction]
```

Rules: one block per AK, concise. Lead with the worst (❌/🟡) ACs.

---

## 4. NFR Table Template

```markdown
| Prio | Qualität | NFR | Messbares Kriterium | Verifikation |
|---|---|---|---|---|
```

Rules: every NFR measurable; every NFR has a verification method; no vague NFRs; unknown threshold →
placeholder + „zu validieren".

---

## 5. Test Strategy Template

Used for the Test Strategy mode. Name the risk first, then techniques (see `references/risk-based-testing.md`
and `references/test-design-techniques.md`). Per recommendation:

```markdown
**[Risk name] — [ISO characteristic] · [Prio]**
- Recommended technique: …
- Why it fits: …
- What it covers: …
- What it misses: …
- Example test ideas: …
```

Always state *what it misses*.

---

## 6. Follow-up Actions Template

Render as button-like inline-code blocks the user can click/copy as the next prompt. Pick the 3-5 most
relevant to the review:

```markdown
`🧪 Testplan für kritische Lücken erstellen`
`✍️ Akzeptanzkriterien verfeinern`
`📋 NFR-Backlog-Items generieren`
`👥 3-Amigos-Refinement vorbereiten`
`✅ Quality Gate Checkliste erstellen`
`📄 Detailed Review anfordern`
```