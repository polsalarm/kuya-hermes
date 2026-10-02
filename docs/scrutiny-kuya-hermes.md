# IDEA Scrutiny Gate (SCRUTINY)

**Project:** Kuya Hermes
**Date:** 2026-10-02
**Version:** 0.1
**Owner:** Kuya Hermes team
**Status:** Locked
**Last reconciled:** 2026-10-02
**IDEA:** [idea-kuya-hermes.md](idea-kuya-hermes.md)

---

## 1. Verdict

**Decision:** PROCEED WITH FIXES

**One-line rationale:** The lock bar is specific, the sandbox claims check out against `data/store.db` on 2026-10-02, and the three hackathon layers are already in the repo.

**If PROCEED WITH FIXES, items carried into the build as TBD / risk:**
- PRD §8 and README: which teammate holds the mic is still open. Any of the six can present.
- WRAP §1: placement is unknown until judging ends. Record the result as not yet known.
- PRD §7 and AIA §1: the Hermes model on the demo laptop is whatever `hermes model` selected. The repo does not pin a provider.
- CLR §1 and OPS §2: the public site at https://kuya-hermes.vercel.app is a static snapshot. Live chat exists only while the team laptop runs the gateway.
- BUILD §5.2: no `robots.txt` is in the repo as of 2026-10-02.

---

## 2. Claim & Reference Audit

**Coverage:** Claims extracted: 16; checked: 16; verified: 14; unverified: 2; contradicted: 0.

| # | Category | Claim (from IDEA) | Finding | Source (required if Verified) | Severity if wrong |
|---|----------|-------------------|---------|-------------------------------|-------------------|
| FC-1 | Problem | 12 Suki Mart branches | Verified | `data/store.db` `branches` row count, queried 2026-10-02 | Critical |
| FC-2 | Problem | Sandbox "today" is 2026-09-30 21:00 | Verified | `data/store.db` `sandbox_info.sandbox_now`, queried 2026-10-02 | Critical |
| FC-3 | Problem | 47 items out of stock | Verified | `data/store.db` inventory `on_hand = 0` joined to active products at or under reorder point, queried 2026-10-02 | Critical |
| FC-4 | Problem | Ermita has 14 out-of-stock items and none of them have an open PO | Verified | Same query, branch code ERM, queried 2026-10-02 | Critical |
| FC-5 | Problem | 12 branch-product pairs have duplicate open POs | Verified | `purchase_orders` status in pending, in_transit, partially_received, grouped by branch and product, HAVING count > 1, queried 2026-10-02 | Critical |
| FC-6 | Problem | BGC Calamansi Juice 1L has 4 open POs | Verified | SKU SM-BEV-0050 at branch BGC, 4 open rows, queried 2026-10-02 | Significant |
| FC-7 | Problem | Visayas Canning Corp. promises 5 days and averages 11.3 | Verified | `suppliers.promised_lead_time_days` and average `julianday(received_at) - julianday(ordered_at)` on received POs, queried 2026-10-02 | Significant |
| FC-8 | Problem | 46 open or pending tickets have no first response | Verified | `support_tickets` status in open, pending and `first_response_at` is null, queried 2026-10-02 | Significant |
| FC-9 | Solution | Seven domain tools plus `describe_sandbox` and `list_branches` | Verified | `mcp-server/server.py` tool decorators, read 2026-10-02 | Critical |
| FC-10 | Solution | Writes are `create_purchase_order` and `assign_cover`, and both refuse to run as duplicates or on a non-upcoming shift | Verified | `mcp-server/server.py` write helpers, read 2026-10-02 | Critical |
| FC-11 | Solution | Skill workflows are sweep, pulse, fix stockouts, and cover an absence | Verified | `skills/kuya-hermes-ops/SKILL.md`, read 2026-10-02 | Critical |
| FC-12 | Solution | Desktop plugin id is `kuya-hermes-hq` | Verified | `desktop-plugin/kuya-hermes-hq/plugin.js` `PLUGIN_ID`, read 2026-10-02 | Critical |
| FC-13 | Technical / Feasibility | John Soriano has a 07:00 Alabang cashier shift on 2026-10-01, and Rowena Tomas is the top cover | Verified | `staff` and `shifts` plus the cover ranking query copied from `find_shift_cover`, shift id 14723, queried 2026-10-02 | Significant |
| FC-14 | Technical / Feasibility | Public site and Telegram bot are live for judges right now | Unverified; needs check | Links are cited below. This gate did not open the live site or the bot on 2026-10-02. | Minor |
| FC-15 | Insight | A human yes is required before either write | Verified | Skill workflows B and C, and write-tool docstrings, read 2026-10-02 | Critical |
| FC-16 | Cost / Metrics | Judging total is 100 points across seven criteria | Verified | [docs/JUDGING.md](JUDGING.md), read 2026-10-02 | Minor |

### 2.1 References Integrity

| # | Cited as | Backs claim | Resolves? | Supports the claim? | Finding | Source |
|---|------------------------------|-------------|-----------|---------------------|---------|--------|
| R-1 | `data/store.db` | FC-1 to FC-8, FC-13 | Yes | Yes | Verified | Queried 2026-10-02 |
| R-2 | `mcp-server/server.py` | FC-9, FC-10 | Yes | Yes | Verified | Read 2026-10-02 |
| R-3 | `skills/kuya-hermes-ops/SKILL.md` | FC-11, FC-15 | Yes | Yes | Verified | Read 2026-10-02 |
| R-4 | `desktop-plugin/kuya-hermes-hq/plugin.js` | FC-12 | Yes | Yes | Verified | Read 2026-10-02 |
| R-5 | [docs/JUDGING.md](JUDGING.md) | FC-16 | Yes | Yes | Verified | Read 2026-10-02 |
| R-6 | `assets/kuya-hermes-fullbody.png`, `assets/kuya-hermes-avatar-160.png`, `assets/ui-inspo.png` | Concept visuals | Yes | Yes | Verified | Files present 2026-10-02 |
| R-7 | `web/static/index.html`, `web/static/dashboard.html`, `web/static/styles.css` | Concept visuals | Yes | Yes | Verified | Files present 2026-10-02 |
| R-8 | https://docs.google.com/presentation/d/1FUpL2Lwria9scJyw579aeD1j7PTHWj7t_eRVc9OhJ8Y/edit?usp=sharing | Demo script | Yes | Yes | Verified | Text export fetched 2026-10-02 |
| R-9 | https://kuya-hermes.vercel.app | Public snapshot | Unverified | Unverified | Unverified | Not fetched during this gate |
| R-10 | https://github.com/polsalarm/kuya-hermes | Source remote | Yes | Yes | Verified | `git remote -v` on 2026-10-02 |
| R-11 | https://github.com/TadeyRuk/hermes | Upstream starter, named in the current README | Unverified | Partly | Unverified | Not fetched during this gate |
| R-12 | https://t.me/kuyahermes_bot | Telegram surface | Unverified | Unverified | Unverified | Not opened during this gate |

---

## 3. Gap Analysis

| # | Missing input | Needed by (doc) | Blocker or TBD |
|---|---------------|-----------------|----------------|
| G-1 | Named primary user and pain moment | IDEA §2 | Filled. Not a blocker. |
| G-2 | Who presents | README demo pre-flight | TBD |
| G-3 | Placement result | WRAP §1 | TBD |
| G-4 | Pinned model provider | PRD §7, AIA §1 | TBD |
| G-5 | Whether the Vercel URL and Telegram bot answer right now | OPS §2, CLR §1 | TBD. Treat the site as a static snapshot until someone loads it. |
| G-6 | `robots.txt` for the public snapshot | BUILD §5.2 | TBD |
| G-7 | User-data and AI-risk register | CLR, AIA | Fill-as-docs. Not a blocker. The sandbox people are fictional. A live Telegram chat can contain a real manager's words. |

No Blocker rows. Section 7 stays empty on purpose.

---

## 4. Assumption Stress-Test

**Load-bearing assumption:** One skill plus one MCP server can serve both Hermes Desktop and Telegram, and a human yes is enough control for the two write tools.

**Strongest argument against it:** The gateway, the model, and the Telegram session all have to be up on one laptop. If that process dies, the live half of the demo dies with it. The Vercel site cannot file a PO.

**Does it hold?** Holds with caveat. The code path is in the repo and the sandbox numbers are real. The live path still depends on the laptop.

**Second-order effects worth noting:** `assign_cover` ranks real-looking fictional staff by absences. That pattern would be an employment decision if the database were real. Keep the human yes, and do not point this build at a real workforce without counsel.

### 4.1 Audience / 10-second stress

| Check | Finding | Severity if fail |
|-------|---------|------------------|
| Stranger hook (10 seconds): can you state who hurts and why without slides? | Pass. HQ cannot see that Ermita is empty and BGC is double-ordering until one sweep connects them. | Critical if Fail and no internal-tool exception |
| Named user + pain present in IDEA §2 | Pass. HQ ops lead, Ermita versus BGC Calamansi Juice, sandbox morning 2026-09-30. | Critical if Fail |
| One-liner repeatable (not generic SaaS) | Pass. One Hermes agent, Desktop plus Telegram, same tools. | Critical if Fail |
| Substitute indifference: why not keep coping with the status quo? | Pass. The status quo is four separate corners (stock, POs, suppliers, shifts) and 46 unanswered tickets. | Significant; Critical if Fail and insight hollow |

**Audience verdict:** Holds. A judge who has seen the sandbox can repeat the pain without the slides.

---

## 5. Feasibility & Scope

| Check | Finding |
|-------|---------|
| Time box realistic for the scope? | The product is already in the repo. This pass documents it. The original build window was 45 to 60 minutes. |
| "If we ship only one thing" actually shippable in the window? | Yes. `network_sweep` plus the confirm-before-write rule are already implemented. |
| Production-grade reachable (security, data, rollback) in the window? | Lean-but-real. Rollback is `git checkout -- data/store.db` or `python data/seed.py`. Secrets stay in the Hermes `.env`. The public snapshot does not write. |
| Scope honest, or is the cut line hiding work? | Honest. `sari-sari/` and a generic SQL tool are named as out of scope. |

---

## 6. Risk & Compliance Pre-flight

| Flag | Present? | Pulls in |
|------|----------|----------|
| Collects user data / PII | Y | CLR. Fictional sandbox staff, plus whatever a person types into Telegram or the local web chat. |
| Children, health, payment, or biometric data | N | No product feature targets those categories. Sandbox tickets can mention payment as a category enum. That is fixture data, not a payments product. |
| AI component with untrusted input or tools | Y | SDD §8.1, QAD §7, AIA. Field text is untrusted. Tool results are the only numbers the skill may quote. |
| Security-critical paths (auth, money, deletes) | Y | SDD §5 and QAD abuse paths. Writes change POs and shifts. Optional `SITE_PASSWORD` on the local web process. |
| Public deploy | Y | OPS and CLR. Static snapshot on Vercel. Live agent stays on the laptop. |

---

## 7. Blocking Questions

None. The verdict is not DO NOT BUILD YET.

---

## Self-Check

- [x] Verdict (§1) is set and matches the findings
- [x] §2 coverage line filled; every checkable IDEA detail has a row (not a sample)
- [x] No claim row reports Verified without a source (trust rule honored; `scripts/check.py` enforces it)
- [x] §2.1 audits every reference cited in the IDEA (or states there are none)
- [x] §4.1 audience / 10-second stress filled (even in Quick Mode)
- [x] Critical list honored; narrative blockers are Critical, not silent TBDs
- [x] Every Blocker gap appears in §7 when the verdict is DO NOT BUILD YET
- [x] Risk flags (§6) name the docs they pull into scope
- [x] On PROCEED WITH FIXES, every fix names the doc it lands in
- [x] AGENTS hard bans applied; VOICE polish pass before lock (no em-dashes)
- [x] On PROCEED: index row added; build sequence continues
