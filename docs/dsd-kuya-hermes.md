# Design System Document (DSD)

**System Name:** Kuya Hermes HQ
**Date:** 2026-10-02
**Version:** 0.1
**Owner:** Kuya Hermes team
**Status:** Locked
**Last reconciled:** 2026-10-02
**PRD:** [prd-kuya-hermes.md](prd-kuya-hermes.md)

---

## 0. Brand Stance

**Three rules:**
1. The mascot is a person you would ask for help on the floor, not a generic robot.
2. Risk has to be readable before the sentence under it. Gold is the action. Red and amber are the problems.
3. The Hermes Desktop plugin borrows the host theme. The website does not pretend to be a second desktop.

**Mode:** Product. The landing page may show the mascot large. The dashboard and the HQ page are for the sweep.

**Provenance:** Shipped UI. Tokens copied from `web/static/styles.css` on 2026-10-02. HQ layout follows `assets/ui-inspo.png` and `desktop-plugin/kuya-hermes-hq/plugin.js`. Impeccable init was not re-run. The screens already exist.

**Archetype:** The HQ ops lead, standing over 12 branches, needing the worst one first.

**Slop to avoid:** Purple gradient SaaS, interchangeable robot, stock "AI assistant" illustrations.

---

## 0.5 Concept Visuals (from IDEA)

See [idea-kuya-hermes.md](idea-kuya-hermes.md) §5.

| Screen | Path |
|--------|------|
| Hero mascot | `assets/kuya-hermes-fullbody.png` |
| Plugin avatar | `assets/kuya-hermes-avatar-160.png` |
| HQ reference | `assets/ui-inspo.png` |
| Landing and dashboard | `web/static/index.html`, `web/static/dashboard.html` |

---

## 1. Design Philosophy & Vision

Night-market grocery operations. Dense enough to show 12 branches. Quiet enough that a red badge is the loudest thing on the card. Taglish is allowed in the product voice. The UI chrome stays short English labels: Run full sweep, Branch pulse, Fix stockouts, Cover shift gaps.

---

## 2. Brand Primitives

From `:root` in `web/static/styles.css`.

| Token | Value | Use |
|-------|-------|-----|
| `--bg` | `#070b1d` | Page |
| `--bg-2` | `#0c1230` | Secondary field |
| `--card` | `#111a3d` | Cards |
| `--card-2` | `#16204a` | Raised card, chat bubble |
| `--stroke` | `#24305e` | Hairline |
| `--text` | `#eef1ff` | Primary text |
| `--text-2` | `#b7bfe6` | Secondary text |
| `--text-3` | `#7d87b8` | Meta |
| `--gold` | `#f5b83d` | Action, eyebrow |
| `--gold-2` | `#ffd27a` | Gold highlight |
| `--red` | `#ff6b6b` | Out of stock, high risk |
| `--amber` | `#ffb347` | Warning |
| `--green` | `#4ade80` | Live dot |
| `--radius` | `14px` | Cards |
| Font | Inter, system-ui, Segoe UI | Website |

Desktop plugin: `var(--ui-text-primary)` and the other Hermes theme variables. Do not paste the hex values into `plugin.js`.

Icons: `assets/icons.md`. 24 by 24, `currentColor`, round caps.

---

## 3. Layout & Spatial System

- Website content width: `min(1120px, 100% - clamp(32px, 10vw, 160px))`.
- Hero: two columns, copy then mascot, stacking on a narrow viewport.
- Stats: four columns on the landing problem row.
- HQ page: header with mascot, sweep card, KPI tiles, 12 branch cards, action row, Ask Kuya, pulse panel.
- Side pane: same actions, compact, next to the Hermes chat.

---

## 4. Core Component Specs

| Component | Spec |
|-----------|------|
| Primary button | Gold gradient, dark brown label `#1b1300`, class `btn-gold` on the web. Plugin uses the host `Button`. |
| Branch card | Code, name, risk badge. Actions: pulse, stock, staff. |
| Risk badge | Filled from `network_sweep` after the tool completes. Empty before the first sweep. |
| Ask box | Placeholder example: "kumusta ang Alabang?" |
| Chat bubble | Card-2, gold is not the body text color. |

Empty: no sweep yet, badges unset. Loading: sweep in flight. Error: gateway text, not fake zeros. Success: 12 cards with scores.

---

## 5. Motion & Micro-interactions

- Mascot float on the landing hero: 5s ease-in-out, 10px.
- Buttons: 0.12s background, slight scale on press.
- No motion required to understand the sweep result.

---

## 6. Accessibility (a11y)

- Gold on `#1b1300` is the primary button pair. Do not put gold text on the navy page for long paragraphs. Gold is for eyebrows and the button.
- Body text is `#eef1ff` on `#070b1d`.
- Plugin text uses the host theme so Hermes contrast settings still apply.
- Icons are inline SVG with `currentColor`. Pair them with a text label. The sweep button has a label, not only an icon.
- A full audit with a screen reader was not run on 2026-10-02.

---

## 7. Taste-Skill Settings

Not re-run. The shipped direction is the setting: product mode, navy and gold, mascot as the brand object, dense ops UI, no purple SaaS default.

---

## 8. Impeccable Quality Gate

`/impeccable audit` was not run on 2026-10-02. Scores are not invented.

| Dimension | Score | Notes |
|-----------|-------|-------|
| Accessibility | Not scored | See §6. No P0 filed because no audit ran. |
| Performance | Not scored | Static pages, one PNG mascot. |
| Theming | Not scored | Plugin uses host variables. Website uses the tokens above. |
| Responsive | Not scored | Landing grid collapses by the CSS already in `styles.css`. |
| Anti-patterns | Not scored | Direction in §0 is the bar the team already shipped. |

Open P0/P1 from this gate: none recorded, because the gate did not run. Do not treat that as a pass.

---

## 9. Materialization

`BRAND.md` and `DESIGN.md` at the repo root are short pointers plus the token table. They are not a second design system. Edit this file first.

---

## Self-Check

- [x] §0 filled from the shipped UI
- [x] Tokens match `web/static/styles.css`
- [x] Plugin theming rule is explicit
- [x] §8 does not invent audit scores
