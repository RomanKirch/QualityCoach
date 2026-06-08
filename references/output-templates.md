# Output Templates

Templates per output mode. **Executive Review is the default.** Keep German output if the input is
German.

## Rendering surface — read first

The Executive Review hero is a **two-column dashboard** (summary cards left, HQM wheel right). Raw
HTML/CSS only renders in an **HTML artifact / canvas**, not in plain chat. Therefore:

- **When the surface supports artifacts (claude.ai, Claude Code, Cowork): render the entire Executive
  Review as a single HTML artifact** using the structure below. This is strongly preferred — it is the
  "review board" experience.
- **The four summary values must be rendered as cards, never as a markdown table.**
- **HQM wheel image:** the skill ships `assets/hqm-wheel.png`. A relative `src` will not resolve inside
  an artifact, so **read `assets/hqm-wheel.png` and embed it as a base64 `data:` URI** in the `<img>`
  src. If you cannot read/embed it, render the `.hqm-wheel-placeholder` block instead. The wheel must
  **support** the analysis, not dominate it — keep it in the right column at the given max-width.
- **Plain-text/markdown-only fallback** (no artifact possible): use bold "card" lines, not a wide
  table, and skip the image — but prefer the artifact whenever available.

---

## 1. Executive Review Template (DEFAULT — render as HTML artifact)

Full single-file HTML. Replace bracketed values. Order below the hero: AK assessment → quality gaps →
NFRs → Top 3 Blocking Questions → MVP Readiness → next steps.

```html
<style>
.hqm-doc { font-family: -apple-system, Segoe UI, Roboto, sans-serif; color:#1a1a1a; max-width: 1024px; }
.hqm-title { font-size: 30px; font-weight: 800; margin: 0 0 4px 0; }
.hqm-context { color:#666; font-size: 15px; margin-bottom: 4px; }

.hqm-hero {
  display: grid;
  grid-template-columns: minmax(0, 1.45fr) minmax(280px, 0.75fr);
  gap: 28px; align-items: stretch; margin: 22px 0 34px 0;
}
.hqm-summary { display: grid; grid-template-columns: 1fr 1fr; gap: 18px; }
.hqm-card { background:#f5f3ed; border-radius:14px; padding:22px 26px; min-height:104px; }
.hqm-label { font-size:15px; color:#444; margin-bottom:10px; }
.hqm-value { font-size:28px; font-weight:700; color:#111; line-height:1.2; }
.hqm-value.warning { color:#6b5520; }
.hqm-value.critical { color:#9b2f2f; }
.hqm-value.good { color:#2f6b3a; }

.hqm-wheel-panel {
  background:#fff; border:1px solid #e7e3dc; border-radius:16px; padding:16px;
  display:flex; flex-direction:column; justify-content:center; align-items:center; min-height:250px;
}
.hqm-wheel { width:100%; max-width:320px; height:auto; opacity:0.92; }
.hqm-wheel-caption { margin-top:10px; font-size:13px; color:#666; text-align:center; }
.hqm-wheel-placeholder {
  text-align:center; font-size:13px; color:#555; line-height:1.6; padding:14px;
}

.hqm-section { margin: 26px 0 10px 0; font-size:20px; font-weight:700; }
.hqm-ak { border:1px solid #e7e3dc; border-radius:12px; padding:14px 18px; margin:10px 0; }
.hqm-ak h4 { margin:0 0 6px 0; font-size:16px; }
.badge { display:inline-block; padding:2px 10px; border-radius:999px; font-size:13px; font-weight:600; }
.badge.klar { background:#e3f3e6; color:#2f6b3a; }
.badge.unklar { background:#fdf4e0; color:#6b5520; }
.badge.schwach { background:#fff7da; color:#7a6516; }
.badge.kritisch { background:#fbe6e6; color:#9b2f2f; }
.hqm-ak p { margin:4px 0; font-size:14px; }

table.hqm { border-collapse:collapse; width:100%; font-size:14px; margin:8px 0; }
table.hqm th, table.hqm td { border:1px solid #e7e3dc; padding:8px 10px; text-align:left; vertical-align:top; }
table.hqm th { background:#f5f3ed; }

.hqm-mvp { background:#f5f3ed; border-left:5px solid #6b5520; border-radius:10px; padding:16px 20px; margin:10px 0; }
.hqm-mvp .decision { font-size:18px; font-weight:700; margin-bottom:6px; }

.hqm-actions { display:flex; flex-wrap:wrap; gap:10px; margin:12px 0; }
.hqm-btn { background:#1a1a1a; color:#fff; border-radius:10px; padding:10px 16px; font-size:14px; font-weight:600; }

@media (max-width: 900px) {
  .hqm-hero { grid-template-columns: 1fr; }
  .hqm-summary { grid-template-columns: 1fr 1fr; }
  .hqm-wheel { max-width:260px; }
}
</style>

<div class="hqm-doc">
  <div class="hqm-title">Feature-Evaluation: [Feature Name]</div>
  <div class="hqm-context">[System / Product] · [Review Context] · Reviewer: [Name]</div>

  <div class="hqm-hero">
    <div class="hqm-summary">
      <div class="hqm-card">
        <div class="hqm-label">Gesamtbewertung</div>
        <div class="hqm-value warning">[Solide – mit Lücken]</div>
      </div>
      <div class="hqm-card">
        <div class="hqm-label">Testbarkeit</div>
        <div class="hqm-value">[4 / 6 AK klar testbar]</div>
      </div>
      <div class="hqm-card">
        <div class="hqm-label">Kritischste Lücke</div>
        <div class="hqm-value critical">[AK04 – Propagation]</div>
      </div>
      <div class="hqm-card">
        <div class="hqm-label">Empfohlene Entscheidung</div>
        <div class="hqm-value">[MVP-fähig mit Auflagen]</div>
      </div>
    </div>

    <div class="hqm-wheel-panel">
      <!-- Embed assets/hqm-wheel.png as a base64 data URI: src="data:image/png;base64,...." -->
      <img src="[DATA_URI_OR_OMIT]" alt="HQM Quality Wheel" class="hqm-wheel" />
      <div class="hqm-wheel-caption">ISO 25010 / HQM Quality Wheel</div>
    </div>
  </div>

  <div class="hqm-section">Akzeptanzkriterien – Bewertung</div>
  <div class="hqm-ak">
    <h4>[AK04 – Titel] <span class="badge kritisch">❌ Kritisch</span></h4>
    <p><strong>Bewertung:</strong> [ein Satz]</p>
    <p><strong>Testbarkeit:</strong> [ein Satz]</p>
    <p><strong>Fehlt:</strong> [knapp]</p>
    <p><strong>Verbesserung:</strong> [knapp]</p>
  </div>
  <!-- badges: klar ✅ Klar · unklar ⚠️ Unklar · schwach 🟡 Schwach · kritisch ❌ Kritisch. One .hqm-ak per AK, worst first. -->

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
  <ol>
    <li>[design/test-blocking decision]</li>
    <li>[design/test-blocking decision]</li>
    <li>[design/test-blocking decision]</li>
  </ol>

  <div class="hqm-section">MVP Readiness</div>
  <div class="hqm-mvp">
    <div class="decision">[Ready with conditions]</div>
    <div>[2-3 Sätze Begründung + Bedingungen.]</div>
  </div>

  <div class="hqm-section">Nächste mögliche Schritte</div>
  <div class="hqm-actions">
    <span class="hqm-btn">🧪 Testplan für kritische Lücken</span>
    <span class="hqm-btn">✍️ Akzeptanzkriterien verfeinern</span>
    <span class="hqm-btn">📋 NFR-Backlog-Items generieren</span>
    <span class="hqm-btn">👥 3-Amigos-Refinement vorbereiten</span>
    <span class="hqm-btn">📄 Detailed Review anfordern</span>
  </div>
</div>
```

### Wheel image not available → placeholder (use instead of the `<img>`)

```html
<div class="hqm-wheel-placeholder">
  <strong>HQM Quality Wheel</strong><br/>
  ISO 25010 Scan: Functional Suitability · Performance · Compatibility · Usability ·
  Reliability · Security · Maintainability · Portability
</div>
```

### Status badge legend
✅ Klar (`klar`) · ⚠️ Unklar (`unklar`) · 🟡 Schwach (`schwach`) · ❌ Kritisch (`kritisch`)

---

## 2. Detailed Review Template

Only when the user explicitly asks for a deep/detailed/full report. Same analytical content, expanded.
May be rendered as markdown (it is long-form, not a dashboard):

```markdown
# [Feature] — Detailed Quality Review
## Verdict (1 Zeile)
## Context Summary
## Akzeptanzkriterien – Bewertung   (badges, all ACs)
## Identifizierte Qualitätslücken   (full table incl. Owner)
## NFR-Vorschläge
## Acceptance Criteria to Add        (Given/When/Then, P1/P2)
## Verification Approach             (grouped by risk; technique named; Automated/Manual; one monitoring)
## Architecture Implications
## Risks & Assumptions
## HQM Observations (Process / People / Values)
## Open Questions for Refinement
## Hints by Role
## Next Steps — pick one
```

---

## 3. Acceptance Criteria Review (per AK)
`Status` badge · `Bewertung` (concrete?) · `Testbarkeit` · `Fehlt` · `Verbesserung`. Worst (❌/🟡) first.

## 4. NFR Table
`Prio | Qualität | NFR | Messbares Kriterium | Verifikation`. Every NFR measurable + verification;
no vague NFRs; unknown threshold → placeholder + „zu validieren".

## 5. Test Strategy
Name the risk first, then per recommendation: Recommended technique · Why it fits · What it covers ·
What it misses · Example test ideas. Always state *what it misses*.

## 6. Follow-up Actions
Button-style blocks (`.hqm-btn` in HTML, or inline-code in markdown) — pick the 3-5 most relevant:
🧪 Testplan · ✍️ AK verfeinern · 📋 NFR-Backlog · 👥 3-Amigos · ✅ Quality Gate Checkliste · 📄 Detailed Review