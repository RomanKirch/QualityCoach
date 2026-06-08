# HQM Quality Wheel — Reference

Use the HQM Quality Wheel as a **mental completeness checklist**, not as a rendering. Scan the eight
ISO 25010 product-quality dimensions and their sub-characteristics, then extend the analysis with HQM
observations across **Process, People, and Values**. The wheel exists to catch *missing* dimensions —
it is not a prompt to mechanically list all of them. Only surface a dimension when there is a real gap.

> Do not render the wheel unless the user explicitly asks for a visual. If a PNG of the wheel is
> placed next to this file (e.g. `assets/hqm-wheel.png`), reference it only on request.

## Inner ring — ISO 25010 product quality (8 characteristics)

| Characteristic | Sub-characteristics (outer ring) |
|---|---|
| **Functionality** (Functional Suitability) | Completeness · Correctness · Appropriateness |
| **Performance** (Efficiency) | Response Time · Resource Use · Capacity |
| **Compatibility** | Coexistence · Interoperability |
| **Usability** | Recognizability · Learnability · Operability · User-error Protection · UI Aesthetics · Accessibility |
| **Reliability** | Maturity · Availability · Fault Tolerance · Recoverability |
| **Security** | Confidentiality · Integrity · Non-repudiation · Accountability · Authenticity |
| **Maintainability** | Modularity · Reusability · Analyzability · Modifiability · Testability |
| **Portability** | Adaptability · Installability · Replaceability |

## Outer context — HQM organisational lenses

Product quality (above) is shaped by three organisational lenses. Tag each gap with the lens that
best explains it:

- **Product** — the ISO 25010 quality of the artifact itself.
- **Process** — how work flows: release coordination, feedback loops, change propagation, governance.
- **People** — knowledge, collaboration, ownership, cross-team engagement (who decides "good enough").
- **Values** — priorities and trade-offs: simplicity vs. stability, speed vs. safety, debt tolerance.

## How to use it in a review

1. Walk the inner ring: for each ISO characteristic, ask "does the input define this, and is it
   measurable?" Note only the gaps.
2. For each gap, pick the sub-characteristic that names it precisely (e.g. Security → Confidentiality,
   not just "Security").
3. Add the HQM lens: many gaps are not purely technical — a missing governance owner is **People**, an
   undefined change-propagation model is **Product + Process**, an unspoken simplicity-vs-stability
   choice is **Values**.
4. This produces a complete-but-focused map instead of a generic ISO sweep.