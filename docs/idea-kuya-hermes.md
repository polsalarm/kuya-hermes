# Idea Brief (IDEA)

**Project:** Kuya Hermes
**Date:** 2026-10-02
**Version:** 0.1
**Owner:** Kuya Hermes team
**Status:** Locked
**Last reconciled:** 2026-10-02
**Event / context:** CAMP / RUN Hermes Agent hackathon, 2 October 2026, Avtica Office. Track: Open Innovation.

---

## 1. The Spark

**Production intent:** A real branch-ops copilot on the Suki Mart sandbox, with confirm-before-write, a reset path for the database, and a public read-only snapshot. The hackathon demo is a milestone, not the product.

**One-line pitch:** One Hermes agent runs Suki Mart branch ops for HQ in Hermes Desktop and for branch managers on Telegram, over the same MCP tools and skill.

**Problem:** As of 2026-09-30 in `data/store.db`, 47 items are out of stock, Ermita has 14 of those with no open purchase order, 12 branch-product pairs have duplicate open purchase orders (BGC Calamansi Juice 1L has 4), Visayas Canning Corp. promises 5 days and averages 11.3, and 46 open or pending tickets were never answered. Stock, orders, suppliers, shifts, and tickets are not connected in time.

**Insight (why us, why now):** The useful loop is detect, check, propose, confirm, act. Reads can run immediately. The two write tools wait for an explicit yes. Hermes Desktop and Telegram can share that loop today because the hackathon sandbox and the Hermes gateway are already on the team laptop.

---

## 2. Who It's For

**Primary user (named, specific):** The Suki Mart HQ ops lead who watches all 12 Metro Manila branches from Hermes Desktop.

**Their moment of pain:** On the sandbox morning of 2026-09-30, Ermita is at 14 items with zero on hand and no purchase order, while BGC already has four open purchase orders for Calamansi Juice 1L.

**Success in their words:** "I ran one sweep, saw Ermita first, and nothing was filed until I said yes."

Secondary user: a branch manager on the floor, messaging in Taglish. Demo line: "di pumasok si John Soriano bukas ng 7am sa Alabang." John Soriano (EMP-0152) has a scheduled cashier shift at Alabang on 2026-10-01 at 07:00. The top cover candidate for that shift is Rowena Tomas (EMP-0156).

---

## 3. Scope & Cut Line

**In scope for this sprint:**

| # | Capability | Demo-critical? |
|---|------------|----------------|
| 1 | `suki` MCP server with seven domain tools plus two starter helpers | Yes |
| 2 | `kuya-hermes-ops` skill: sweep, pulse, stockouts, shift cover, Taglish, confirm before write | Yes |
| 3 | `kuya-hermes-hq` desktop page, side pane, and Ctrl+K commands | Yes |
| 4 | Telegram gateway using the same skill and tools | Yes |
| 5 | Read-only web dashboard and static Vercel snapshot | No |

**Explicitly out of scope (v0):** A generic SQL tool. Replacing the sandbox with a live Suki Mart. The earlier single-store `sari-sari/` prototype as the submission. Autonomous purchase orders or shift changes without a yes.

**If we only ship one thing:** A full network sweep that ranks branch risk and will not file a purchase order or book a shift cover without an explicit yes.

---

## 4. Success & Judging Criteria

**How we win (metrics or rubric):** [docs/JUDGING.md](JUDGING.md), 100 points. The spoken pitch is the Google Slides deck, not a markdown pitch file.

| Criterion (from rubric / brief) | How we hit it |
|---------------------------------|---------------|
| MCP Server, 20 | Seven domain tools in `mcp-server/server.py`. SQL stays inside the tools. |
| Skill, 20 | `skills/kuya-hermes-ops/SKILL.md` chains those tools and asks before writes. |
| Desktop Plugin GUI, 20 | `desktop-plugin/kuya-hermes-hq/plugin.js` HQ page inside Hermes Desktop. |
| End-to-End Integration, 10 | Button or Telegram message, skill, `mcp_suki_*`, `data/store.db`, reply in the same chat. |
| Relevance, 15 | The 2026-09-30 stock, PO, lead-time, shift, and ticket problems above. |
| Uniqueness, 10 | Two surfaces, real versus promised lead time, duplicate-PO refusal, Taglish field reports. |
| Demo and Pitch, 5 | Deck slide 10: 0:30 sweep, 1:30 Ermita restock, 2:30 Telegram cover. |

**Demo script (30–90 seconds):** Open the [Kuya Hermes Pitch](https://docs.google.com/presentation/d/1FUpL2Lwria9scJyw579aeD1j7PTHWj7t_eRVc9OhJ8Y/edit?usp=sharing). Problem on slides 2 and 3. Hermes on slides 5 to 9. Working output on slide 10.

---

## 5. Concept Visuals

*The UI already shipped. These are the references the team built against, not new concept frames.*

**Visual direction (one sentence):** Night-market grocery HQ: deep navy field, gold accent, a full-body Kuya mascot, and risk badges a manager can read at a glance.

**Tooling used:** Shipped assets in `assets/` and the live CSS in `web/static/styles.css`. No new image generation on 2026-10-02.

| Screen / section | Asset path | Notes |
|------------------|------------|-------|
| Mascot, landing hero | `assets/kuya-hermes-fullbody.png` | Also used on the public landing page |
| Avatar in the HQ plugin | `assets/kuya-hermes-avatar-160.png` | Embedded in `plugin.js` because disk plugins cannot import local files |
| HQ page direction | `assets/ui-inspo.png` | Design reference for the sidebar page |
| Landing and dashboard | `web/static/index.html`, `web/static/dashboard.html` | Public snapshot at https://kuya-hermes.vercel.app |

**Team decision:** Keep the shipped navy and gold HQ. Do not restyle for the doc pass.

---

## 6. Open Questions

| Question | Owner | Resolve by |
|----------|-------|------------|
| Which of the six presents on the mic? | Kuya Hermes team | Demo call, 2026-10-02 |
| Hackathon placement | Kuya Hermes team | After judging |
| Which Hermes model is selected on the demo laptop? | Whoever runs `hermes model` | Before the mic starts |

---

## Self-Check

- [x] Production intent stated in §1 (real product, not throwaway demo)
- [x] One-line pitch is specific; a stranger can repeat it (not generic SaaS filler)
- [x] Problem and insight are filled (not TBD / placeholder)
- [x] Primary user is named and specific
- [x] Pain moment is a concrete scene
- [x] Cut line is explicit; "If we only ship one thing" is named
- [x] Judging criteria mapped to how we hit them
- [x] Concept visuals linked if UI exists
- [x] Lock bar satisfied before Status: Locked
- [x] AGENTS hard bans applied; VOICE polish pass before lock (no em-dashes)
- [x] Next suggested doc: lite PRD (VALIDATION skipped for Rapid Production)
