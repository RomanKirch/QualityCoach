# Output Templates

Templates per output mode. **Executive Review is the default.** German output if input is German.
All visual styling follows `references/design-system.md` — do not improvise colors.

## Rendering surface — read first

- **If artifacts are available, ALWAYS render the Executive Review as ONE self-contained HTML
  artifact** (full inline `<style>`, no external CSS, no required web fonts). Do not answer the
  Executive Review as plain markdown when artifacts are available.
- **First visible screen must contain:** title, context line, summary cards, HQM wheel (with focus
  tags). The four summary values are **cards, never a markdown table**.
- **Acceptance criteria are cards, never a markdown table.**
- **HQM wheel image:** ship-path `assets/hqm-wheel.png`. A relative `src` will not resolve in an
  artifact — **read the file and embed it as a base64 `data:image/png;base64,…` URI**. If you cannot
  embed it, drop the `<img>` and keep the `.hqm-focus` panel (the focus tags are the analytical part).
- **Fallback (no artifact possible):** markdown cards (bold lines, not a wide table), summary not as a
  table, omit the image but **keep the „Relevant HQM Focus" text**.

---

## 1. Executive Review Template (DEFAULT — self-contained HTML artifact)

```html
<style>
:root{
  --hqm-bg:#fff; --hqm-card:#f5f3ed; --hqm-border:#e7e3dc; --hqm-text:#151515;
  --hqm-muted:#555; --hqm-warning:#6b5520; --hqm-critical:#9b2f2f; --hqm-good:#2f6b3a; --hqm-blue:#2b6f9f;
}
.hqm-doc{font-family:-apple-system,"Segoe UI",Roboto,Helvetica,Arial,sans-serif;color:var(--hqm-text);background:var(--hqm-bg);max-width:1024px;line-height:1.5;}
.hqm-title{font-size:30px;font-weight:800;margin:0 0 4px;}
.hqm-context{color:var(--hqm-muted);font-size:15px;margin-bottom:4px;}

.hqm-hero{display:grid;grid-template-columns:minmax(0,1.45fr) minmax(280px,0.75fr);gap:28px;align-items:stretch;margin:22px 0 34px;}
.hqm-summary{display:grid;grid-template-columns:1fr 1fr;gap:18px;}
.hqm-card{background:var(--hqm-card);border-radius:14px;padding:22px 26px;min-height:104px;}
.hqm-label{font-size:15px;color:var(--hqm-muted);margin-bottom:10px;}
.hqm-value{font-size:28px;font-weight:700;color:var(--hqm-text);line-height:1.2;}
.hqm-value.warning{color:var(--hqm-warning);}
.hqm-value.critical{color:var(--hqm-critical);}
.hqm-value.good{color:var(--hqm-good);}

.hqm-wheel-panel{background:#fff;border:1px solid var(--hqm-border);border-radius:16px;padding:16px;display:flex;flex-direction:column;justify-content:center;align-items:center;min-height:250px;}
.hqm-wheel{width:100%;max-width:300px;height:auto;opacity:.92;}
.hqm-wheel-caption{margin-top:8px;font-size:13px;color:var(--hqm-muted);text-align:center;}
.hqm-focus{margin-top:14px;width:100%;text-align:center;}
.hqm-focus-label{font-size:13px;color:var(--hqm-muted);margin-bottom:6px;}
.hqm-focus-tags{display:flex;flex-wrap:wrap;gap:8px;justify-content:center;}
.hqm-focus-tags span{background:#eef4f8;color:var(--hqm-blue);padding:3px 10px;border-radius:999px;font-size:13px;font-weight:600;}

.hqm-section{margin:26px 0 10px;font-size:20px;font-weight:700;}

.hqm-ak-list{display:flex;flex-direction:column;gap:10px;}
.hqm-ak-row{display:grid;grid-template-columns:auto 1fr auto;gap:14px;align-items:start;border:1px solid var(--hqm-border);border-radius:12px;padding:14px 18px;}
.hqm-ak-id{font-size:15px;font-weight:700;}
.hqm-ak-title{font-size:15px;font-weight:600;margin-bottom:3px;}
.hqm-ak-summary{font-size:14px;color:var(--hqm-text);}
.hqm-ak-meta{font-size:13px;color:var(--hqm-muted);margin-top:5px;display:flex;flex-wrap:wrap;gap:14px;}
.hqm-badge{padding:3px 12px;border-radius:999px;font-size:13px;font-weight:600;white-space:nowrap;height:fit-content;}
.hqm-badge-good{background:#e3f3e6;color:var(--hqm-good);}
.hqm-badge-unclear{background:#fdf4e0;color:var(--hqm-warning);}
.hqm-badge-weak{background:#fff7da;color:#7a6516;}
.hqm-badge-critical{background:#fbe6e6;color:var(--hqm-critical);}

table.hqm{border-collapse:collapse;width:100%;font-size:14px;margin:8px 0;}
table.hqm th,table.hqm td{border:1px solid var(--hqm-border);padding:8px 10px;text-align:left;vertical-align:top;}
table.hqm th{background:var(--hqm-card);}

.hqm-mvp{background:var(--hqm-card);border-left:5px solid var(--hqm-warning);border-radius:10px;padding:16px 20px;margin:10px 0;}
.hqm-mvp.good{border-left-color:var(--hqm-good);}
.hqm-mvp.critical{border-left-color:var(--hqm-critical);}
.hqm-mvp .decision{font-size:18px;font-weight:700;margin-bottom:6px;}

.hqm-actions{display:flex;flex-wrap:wrap;gap:10px;margin:12px 0;}
.hqm-btn{background:var(--hqm-text);color:#fff;border-radius:10px;padding:10px 16px;font-size:14px;font-weight:600;}

@media (max-width:900px){.hqm-hero{grid-template-columns:1fr;}.hqm-summary{grid-template-columns:1fr 1fr;}.hqm-wheel{max-width:260px;}}
</style>

<div class="hqm-doc">
  <div class="hqm-title">Feature-Evaluation: [Feature Name]</div>
  <div class="hqm-context">[System / Product] · [Review Context] · Reviewer: [Name]</div>

  <div class="hqm-hero">
    <div class="hqm-summary">
      <div class="hqm-card"><div class="hqm-label">Gesamtbewertung</div><div class="hqm-value warning">[Solide – mit Lücken]</div></div>
      <div class="hqm-card"><div class="hqm-label">Testbarkeit</div><div class="hqm-value">[4 / 6 AK klar testbar]</div></div>
      <div class="hqm-card"><div class="hqm-label">Kritischste Lücke</div><div class="hqm-value critical">[AK04 – Propagation]</div></div>
      <div class="hqm-card"><div class="hqm-label">Empfohlene Entscheidung</div><div class="hqm-value">[MVP-fähig mit Auflagen]</div></div>
    </div>
    <div class="hqm-wheel-panel">
      <img src="[BASE64_DATA_URI]" alt="HQM Quality Wheel" class="hqm-wheel" />
      <div class="hqm-wheel-caption">ISO 25010 / HQM Quality Wheel</div>
      <div class="hqm-focus">
        <div class="hqm-focus-label">Relevant HQM Focus</div>
        <div class="hqm-focus-tags"><span>Security</span><span>Maintainability</span><span>Compatibility</span></div>
      </div>
    </div>
  </div>

  <div class="hqm-section">Akzeptanzkriterien – Bewertung</div>
  <div class="hqm-ak-list">
    <div class="hqm-ak-row">
      <div class="hqm-ak-id">AK04</div>
      <div class="hqm-ak-main">
        <div class="hqm-ak-title">[kurzer Titel]</div>
        <div class="hqm-ak-summary">[größte Lücke in 1 Satz – warum nicht testbar]</div>
        <div class="hqm-ak-meta"><span><strong>Testbarkeit:</strong> [knapp]</span><span><strong>Fehlt:</strong> [knapp]</span></div>
      </div>
      <div class="hqm-badge hqm-badge-critical">× Kritisch</div>
    </div>
    <!-- one .hqm-ak-row per AK, WORST FIRST, badge right. Max 3-4 lines each.
         badges: hqm-badge-good ✓ Klar · hqm-badge-unclear ⚠ Unklar · hqm-badge-weak ~ Schwach · hqm-badge-critical × Kritisch -->
  </div>

  <div class="hqm-section">Identifizierte Qualitätslücken</div>
  <table class="hqm">
    <tr><th>Prio</th><th>ISO 25010</th><th>HQM Lens</th><th>Gap</th><th>Empfohlene Massnahme</th></tr>
    <tr><td>P1</td><td>Security / Confidentiality</td><td>Product</td><td>[gap]</td><td>[action]</td></tr>
  </table>

  <div class="hqm-section">NFR-Vorschläge</div>
  <table class="hqm">
    <tr><th>Prio</th><th>Qualität</th><th>NFR</th><th>Messbares Kriterium</th><th>Verifikation</th></tr>
    <tr><td>P1</td><td>Security</td><td>[NFR]</td><td>[threshold]</td><td>[method]</td></tr>
  </table>

  <div class="hqm-section">Top 3 Blocking Questions</div>
  <ol><li>[decision]</li><li>[decision]</li><li>[decision]</li></ol>

  <div class="hqm-section">MVP Readiness</div>
  <div class="hqm-mvp"><div class="decision">[Ready with conditions]</div><div>[2-3 Sätze + Bedingungen.]</div></div>

  <div class="hqm-section">Nächste mögliche Schritte</div>
  <div class="hqm-actions">
    <span class="hqm-btn">🧪 Testplan für kritische Lücken</span>
    <span class="hqm-btn">✍️ Akzeptanzkriterien verfeinern</span>
    <span class="hqm-btn">📋 Backlog-Items generieren</span>
    <span class="hqm-btn">👥 3-Amigos-Refinement vorbereiten</span>
    <span class="hqm-btn">📄 Detailed Review anfordern</span>
  </div>
</div>
```

### HQM Focus rules
- Max 4 tags in `.hqm-focus-tags`. Use the ISO 25010 dimensions **actually relevant** to this
  requirement. Primary focus first, secondary after (secondary may be fewer). The wheel + focus tags
  must reflect the analysis — never a generic list.
- Example: Primary `Security · Maintainability`, Secondary `Compatibility · Reliability`.

### Markdown fallback (only when no artifact is possible)
Summary as bold card-lines (not a table), AK as short bold blocks with emoji badge, keep a one-line
**Relevant HQM Focus:** Security · Maintainability · Compatibility, omit the image.

---

## 2. Detailed Review Template
Only on explicit request for a deep/detailed/full report. Same analysis, expanded; may be markdown:
Verdict · Context · AK-Bewertung (all, badges) · Qualitätslücken (full, incl. Owner) · NFR ·
Acceptance Criteria to Add (Given/When/Then) · Verification Approach · Architecture Implications ·
Risks & Assumptions · HQM Observations (Process/People/Values) · Open Questions · Hints by Role ·
Next Steps.

## 3. Acceptance Criteria card (per AK)
`.hqm-ak-row` (id · main · badge). Worst first, badge right, max 3-4 lines. Detail overflow → Detailed Review.

## 4. NFR Table
`Prio | Qualität | NFR | Messbares Kriterium | Verifikation`. Every NFR measurable + verification;
no vague NFRs; unknown threshold → placeholder + „zu validieren".

## 5. Test Strategy
Name the risk first, then per recommendation: Recommended technique · Why it fits · What it covers ·
What it misses · Example test ideas. Always state *what it misses*.

## 6. Backlog Mode Template (Jira-ready)
Triggered when the user asks for Jira items, backlog items, implementation tasks, NFR stories, quality
enablers, or follow-up tasks. Output a list of ready-to-paste backlog items (markdown is fine here —
these are meant to be copied into a tracker):

```markdown
### [Title — imperative, specific]
**Type:** [Story | Enabler | Task | Spike]
**Priority:** [P1–P4]
**ISO 25010:** [characteristic(s)]
**Owner:** [role(s)]

**Description:**
[1-3 sentences: what and why.]

**Acceptance Criteria:**
- [verifiable]
- [verifiable]

**Verification:**
[test/review/monitoring method]
```

Rules: derive items from the P1/P2 gaps and undecided design questions. Spikes for undecided
architecture (e.g. propagation model); Enablers for NFRs; Stories for user-facing behaviour; Tasks for
concrete fixes. Every item has measurable acceptance criteria and a verification method.

## 7. Follow-up Actions
`.hqm-btn` blocks (HTML) or inline-code (markdown). Pick 3-5: 🧪 Testplan · ✍️ AK verfeinern ·
📋 Backlog-Items · 👥 3-Amigos · ✅ Quality Gate Checkliste · 📄 Detailed Review