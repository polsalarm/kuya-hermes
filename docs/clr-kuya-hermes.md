# Compliance & Legal Readiness Register (CLR)

**Project:** Kuya Hermes
**Date:** 2026-10-02
**Version:** 0.1
**Owner:** Kuya Hermes team
**Status:** Locked
**Last reconciled:** 2026-10-02
**PRD:** [prd-kuya-hermes.md](prd-kuya-hermes.md)
**SDD:** [sdd-kuya-hermes.md](sdd-kuya-hermes.md)

---

> **Structural and regulatory awareness only. NOT legal advice.** This register maps data and flags obligations. It does not draft a privacy policy or terms. Anything marked counsel needed needs a lawyer qualified in the relevant jurisdiction before a real launch.

---

## 0. Target Markets (drives the rest of this document)

| Market | Role in this build | Notes |
|--------|--------------------|-------|
| Philippines | Demo audience and fictional setting (Metro Manila) | Hackathon on 2026-10-02 at Avtica Office |
| Other | No product rollout | Do not claim GDPR or CCPA readiness |

The sandbox business, staff, customers, and suppliers are fictional (`sandbox_info.note` in `data/store.db`). A live Telegram message or local web chat can contain words typed by a real person on the team or a judge.

---

## 1. Data Inventory / Record of Processing

| Data | Who | Where it lives | Purpose | Retention |
|------|-----|----------------|---------|-----------|
| Sandbox staff names, shifts, absences | Fictional employees | `data/store.db` | PRD-F1 cover ranking | The git blob. Reset restores it. |
| Sandbox tickets, orders, customers | Fictional | `data/store.db` | Pulse and unanswered counts | Same |
| HQ and Telegram prompts | Real person at the keyboard | Hermes session on the laptop | PRD-F2, PRD-F5 | Hermes local history. Not in this repo. |
| `/api/chat` message | Real person if the local site is used | Forwarded to Hermes. Not stored by `web/app.py`. | PRD-F6 | Upstream Hermes `store: true` on that request. |
| `API_SERVER_KEY`, optional `SITE_PASSWORD` | Team | Hermes `.env`, process env | Auth to the local API | Not committed. See `.gitignore`. |
| Vercel snapshot | Nobody's live chat | Pre-rendered JSON | Read-only numbers | Until the next `vercel deploy` |

No account signup. No payments product. Ticket category `payment` is an enum in fixture data, not card data.

Public URL status: https://kuya-hermes.vercel.app was not fetched during scrutiny on 2026-10-02. Treat it as the static snapshot described in `web/build_static.py` until someone loads it.

---

## 2. Multi-Jurisdiction Obligations Matrix

| Topic | PH demo | If this ever left the hackathon |
|-------|---------|--------------------------------|
| Privacy notice | Not required for a fictional database shown on a laptop. A public chat that stores judge text would need a notice. | Counsel needed |
| Lawful basis | Demo of a course project on fictional data | Counsel needed |
| Sub-processors | Hermes model provider chosen on the laptop (TBD). Vercel hosts static files. | Name them in a notice before a real pilot |
| Cross-border model calls | Possible, depending on the provider. Unknown until `hermes model` is read. | Counsel needed |
| Children | Not a feature | N/A |

This matrix is not a legal conclusion.

---

## 3. Escalation Flags; Counsel Required

| Flag | Present? | Counsel needed? | Why |
|------|----------|-----------------|-----|
| Real personal data in the sandbox | No | No | Fictional people |
| Live chat text from a real person | Yes, if someone types | Yes, before any public always-on bot | Hermes may store the turn |
| Employment decisioning | Pattern only | Yes, before a real workforce | `find_shift_cover` ranks absences. PRD-F4 keeps a human yes. Do not use it on real staff without counsel. |
| Health, biometric, or payments product | No | No | Not in PRD scope |
| Children | No | No | Not in PRD scope |

Evidence link: [prd-kuya-hermes.md](prd-kuya-hermes.md) §7 and [sdd-kuya-hermes.md](sdd-kuya-hermes.md) §8.1.

---

## 4. Terms of Use / EULA Readiness

No terms page. Appropriate for a hackathon demo on fictional data. A public always-on bot would need terms. Counsel needed before that.

---

## 5. IP Infringement & Protection Readiness

| Item | Status |
|------|--------|
| Repo license | MIT. See [LICENSE](../LICENSE). |
| Hermes Agent | Upstream product. Docs linked, not vendored. |
| Mascot PNGs in `assets/` | Team assets for this project. |
| Sandbox data | Fictional, from the hackathon starter. |
| Starter kit | https://github.com/TadeyRuk/hermes. Our submission is the Kuya Hermes layers, not the starter instructions. |

Trademark: "Suki Mart" and "Kuya Hermes" are project names for the hackathon. No filing is claimed.

---

## 6. App Store / Platform Compliance

Not shipping to Apple or Google app stores. Desktop surface is Hermes Desktop. Chat surface is Telegram via the Hermes gateway. Website is static hosting.

---

## Self-Check

- [x] Markets named in §0
- [x] Data inventory names fictional sandbox data and real chat text separately
- [x] Counsel flags are yes where a real workforce or a public bot would change the answer
- [x] Disclaimer stays at the top
- [x] No privacy policy was drafted
