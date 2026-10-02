# Operations & Observability Runbook (OPS)

**Project:** Kuya Hermes
**Date:** 2026-10-02
**Version:** 0.1
**Owner:** Kuya Hermes team
**Status:** Locked
**Last reconciled:** 2026-10-02
**SDD:** [sdd-kuya-hermes.md](sdd-kuya-hermes.md)
**PRD rollback:** [prd-kuya-hermes.md](prd-kuya-hermes.md) §9

---

## 1. SLOs & SLIs

| SLI (what you measure) | SLO (target) | Measured by | Breach action |
|------------------------|--------------|-------------|---------------|
| Sweep returns 12 branches for 2026-09-30 | 100 percent on a fresh `store.db` before the mic | `network_sweep` or GET `/api/sweep` | Reset the database. Do not demo on a dirty file. |
| Live chat answers while the gateway is up | Best effort during the 5-minute slot | Person at the laptop | Switch to the static dashboard. |
| Static dashboard HTTP | Page loads | Browser on https://kuya-hermes.vercel.app/dashboard | Use the local `web/static` files if Vercel fails. Not re-checked live on 2026-10-02. |
| Duplicate PO inserts | Zero | `create_purchase_order` result `created: false` when an open PO exists | Stop. Reset. |

---

## 2. Observability; Logs, Metrics, Traces

| Signal | Where | What it tells you |
|--------|-------|-------------------|
| Hermes gateway | The terminal that launched `hermes gateway` | Agent up or crashed |
| MCP stderr | The `uv run mcp-server/server.py` process if started by hand | Import and SQLite errors |
| Web | stderr lines prefixed `[kuya-web]` | HTTP status and chat proxy errors |
| Tool results | Hermes chat and the HQ plugin | The actual numbers judges see |
| Traces | None | No tracing vendor in this repo |

There is no metrics backend. The actionable check before the mic is: gateway process is running, plugin reloaded, `store.db` not dirty, Telegram session open.

The Vercel project is a static snapshot produced by `web/build_static.py`. It does not tail the laptop logs.

---

## 3. Alerting & On-Call

| Alert | How you notice | Who |
|-------|----------------|-----|
| Gateway down | Telegram silent, local chat returns 502 | Person at the laptop |
| Wrong branch ranked first | Sweep table disagrees with Ermita's 14 stockouts | Same person, before the mic |
| Write landed early | PO numbers appear before the yes line | Stop the demo and reset |

No pager. Six people in the room. One laptop. Best effort for the hackathon hour. After the event, on-call is none until someone keeps the gateway up on purpose.

---

## 4. Incident Response

1. Stop typing into the agent.
2. Say the live path is down and open the static dashboard.
3. If a write was wrong, run `git checkout -- data/store.db` from the repo root, or `python data/seed.py`.
4. Restart with `hermes gateway restart` if the process died.
5. Reload desktop plugins with Ctrl+K.
6. After the event, write a postmortem only if data was lost in a way seed cannot restore. That has not happened.

Rollback reference: PRD §9. The revert mechanism is git checkout of `data/store.db` or `python data/seed.py`.

---

## 5. Routine Operations

| When | Action |
|------|--------|
| Before the mic | Gateway up, plugin reloaded, fresh database, Telegram open, deck on slide 1 |
| After a demo that filed POs or covers | Reset `store.db` |
| After a code change to `server.py` | Restart Hermes. MCP servers load at startup. |
| Static site refresh | `uv run web/build_static.py`, then deploy `web/dist` |

---

## Self-Check

- [x] SLOs match what this laptop can actually defend
- [x] At least one actionable pre-mic check is listed
- [x] Incident steps include the PRD §9 rollback
- [x] Logs have a real destination, even if that destination is a terminal
