# Design System — HQM Quality Coach

The single source of truth for the look of every HTML artifact the skill produces. **Reuse this
system for all HTML artifact outputs. Do not improvise new colors** unless the user explicitly asks
for a custom theme. Every artifact must be **self-contained**: paste the full `<style>` block inline
(no external stylesheets, no web fonts required).

## Color palette (CSS variables)

```css
:root{
  --hqm-bg: #ffffff;
  --hqm-card: #f5f3ed;
  --hqm-border: #e7e3dc;
  --hqm-text: #151515;
  --hqm-muted: #555555;
  --hqm-warning: #6b5520;
  --hqm-critical: #9b2f2f;
  --hqm-good: #2f6b3a;
  --hqm-blue: #2b6f9f;
}
```

Semantic use:
- **warning** (`--hqm-warning`) — „mit Lücken", 🟡 Schwach, conditional readiness.
- **critical** (`--hqm-critical`) — ❌ Kritisch, blocking gap, „Not ready".
- **good** (`--hqm-good`) — ✅ Klar, „Ready", green light.
- **blue** (`--hqm-blue`) — neutral accents, focus tags, links/buttons hover.
- **card/border** — surfaces and dividers. Keep backgrounds calm; let badges carry the color.

## Typography
- Font stack: `-apple-system, "Segoe UI", Roboto, Helvetica, Arial, sans-serif`.
- Title 30px/800; section headings 20px/700; body 14-15px/400; labels 15px/500 in `--hqm-muted`.
- Card value 28px/700. Line-height 1.2 for headings, 1.5 for body. Never justify text.

## Dashboard grid (hero)
- `.hqm-hero`: CSS grid, `grid-template-columns: minmax(0,1.45fr) minmax(280px,0.75fr)`, gap 28px,
  `align-items: stretch`, margin `22px 0 34px`.
- `.hqm-summary`: 2×2 grid, `grid-template-columns: 1fr 1fr`, gap 18px.
- Collapse to single column under 900px; summary stays 2×2.

## Card style
- `.hqm-card`: background `--hqm-card`, radius 14px, padding `22px 26px`, min-height 104px.
- `.hqm-label` (muted, 15px) over `.hqm-value` (28px/700). Value tone via `.warning/.critical/.good`.

## Badge style
- Pill: `padding:3px 12px; border-radius:999px; font-size:13px; font-weight:600;`
- `hqm-badge-good`: bg `#e3f3e6`, text `--hqm-good`, mark `✓ Klar`
- `hqm-badge-unclear`: bg `#fdf4e0`, text `--hqm-warning`, mark `⚠ Unklar`
- `hqm-badge-weak`: bg `#fff7da`, text `#7a6516`, mark `~ Schwach`
- `hqm-badge-critical`: bg `#fbe6e6`, text `--hqm-critical`, mark `× Kritisch`

## Acceptance-criteria card
- `.hqm-ak-list`: vertical stack, gap 10px.
- `.hqm-ak-row`: grid `auto 1fr auto`, gap 14px, align-items start, border `1px solid --hqm-border`,
  radius 12px, padding `14px 18px`. Badge column right-aligned. Worst AK first. Max 3-4 lines per AK.
- `.hqm-ak-id` 15px/700; `.hqm-ak-title` 15px/600; `.hqm-ak-summary` 14px in `--hqm-text`;
  `.hqm-ak-meta` 13px in `--hqm-muted`, items separated with spacing.

## Focus tags (analytical wheel)
- `.hqm-focus`: small panel under the wheel. `.hqm-focus-label` 13px muted.
- `.hqm-focus-tags span`: pill, bg `#eef4f8`, text `--hqm-blue`, `padding:3px 10px; border-radius:999px;
  font-size:13px; font-weight:600;`. Max 4 tags. Primary focus first; secondary may be lighter.

## Section spacing
- `.hqm-section`: 20px/700, margin `26px 0 10px`. Keep sections short; whitespace over density.

## Table style
- `table.hqm`: full width, `border-collapse: collapse`, font 14px.
- Cells: border `1px solid --hqm-border`, padding `8px 10px`, top-aligned. Header row bg `--hqm-card`.
- Never exceed 5 columns.

## Button style
- `.hqm-actions`: flex wrap, gap 10px.
- `.hqm-btn`: bg `--hqm-text`, color `#fff`, radius 10px, `padding:10px 16px`, 14px/600. These are
  click/copy next-prompt affordances, not real buttons.

## MVP callout
- `.hqm-mvp`: bg `--hqm-card`, left border `5px solid` (good/warning/critical per decision), radius
  10px, padding `16px 20px`. `.decision` 18px/700.