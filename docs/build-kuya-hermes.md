# Project Build Guide

**Project:** Kuya Hermes
**Date:** 2026-10-02
**Version:** 0.1
**Owner:** Kuya Hermes team
**Status:** Locked
**Last reconciled:** 2026-10-02
**PRD:** [prd-kuya-hermes.md](prd-kuya-hermes.md)
**SDD:** [sdd-kuya-hermes.md](sdd-kuya-hermes.md)
**SAD:** N/A. No subagent roster. One Hermes agent is the product.

---

## 1. How to Build From These Docs

The documentation suite describes a system that is already in the repo. Read in this order before changing it:

1. `docs/index.md`
2. `docs/prd-kuya-hermes.md` for what must keep working (PRD-F1 through PRD-F5)
3. `docs/sdd-kuya-hermes.md` for where the code lives
4. `docs/qad-kuya-hermes.md` before calling a change done
5. `skills/kuya-hermes-ops/SKILL.md` and `mcp-server/server.py` for the behavior judges see

Do not add a generic SQL tool. Do not file writes without the confirm step.

---

## 2. Subagents

None. SAD was skipped. The only agent in the product is Hermes, and it is configured by the skill plus MCP, not by a roster of coding subagents.

---

## 3. Stack Currency & Deprecations

Verified against this repo on 2026-10-02.

| Piece | Pin | Do not regress |
|-------|-----|----------------|
| Python | `>=3.10` in the script headers | |
| MCP SDK | `mcp>=1.2,<2` | v2 removed the FastMCP import this file uses. Stay on v1. |
| Runner | `uv run` | Respects the inline pin. Do not `pip install mcp` into a global v2. |
| Web | stdlib `http.server` | No second framework. |
| Desktop plugin | `@hermes/plugin-sdk`, `react`, `react/jsx-runtime` only | No JSX syntax. `jsx()` / `jsxs()` only. Theme variables only. |
| Data | SQLite `data/store.db` | Path is relative to `server.py`. Do not move that file without changing `DB_PATH`. |
| Hosting | Vercel static files from `web/dist` | Not a Node server. |

Deprecations: none recorded beyond the mcp v2 break.

---

## 4. Golden-Path Patterns

**Add a read tool.** Follow `branch_pulse`: docstring written for the model, SQL inside the function, small dict back, sandbox clock only.

**Add a write tool.** Follow `create_purchase_order`: refuse the bad state first, then insert, then return ids. Call it only after the skill's confirm step. Update `skills/kuya-hermes-ops/SKILL.md` in the same change.

**Reset data.** `git checkout -- data/store.db` or `python data/seed.py`.

**Register MCP on Windows.**

```powershell
hermes mcp add suki --command uv --args run C:\absolute\path\mcp-server\server.py
hermes gateway restart
hermes mcp test suki
```

**Install skill and plugin.** Hermes home on Windows is `%LOCALAPPDATA%\hermes`, not `%USERPROFILE%\.hermes`.

```powershell
xcopy /E /I skills\kuya-hermes-ops %LOCALAPPDATA%\hermes\skills\kuya-hermes-ops
xcopy /E /I desktop-plugin\kuya-hermes-hq %LOCALAPPDATA%\hermes\desktop-plugins\kuya-hermes-hq
```

Folder name must equal the skill `name` and the plugin `id`.

---

## 5. Conventions & Guardrails

- Money is PHP, shown as ₱, and only from tool output.
- Branch codes are the ones in `list_branches` (ALB, BGC, CUB, ERM, KAT, KPT, MAN, MKT, ORT, PQE, TMR, MKN).
- Open PO statuses: `pending`, `in_transit`, `partially_received`.
- Do not commit `.env`, API keys, or `SITE_PASSWORD`.
- Plugin file is plain JS. A new identifier must be imported or the loader throws.
- Definition of done: QAD rows for the Must-Have you touched, plus a database reset if you wrote.

### 5.1 Brownfield Change Workflow

No `docs/changes/` folder yet. A later change to a Locked Must-Have needs a change record under `docs/` and a row in `docs/index.md`. Until then, do not silently retitle PRD-F IDs.

### 5.2 Public Surface & Crawler Policy

Public URL intended: https://kuya-hermes.vercel.app and https://kuya-hermes.vercel.app/dashboard. Source: https://github.com/polsalarm/kuya-hermes

As of 2026-10-02 this repo has no `robots.txt` and no `llms.txt`. TBD: add them if the static site should set a crawler policy. Until then, do not claim an allow or deny list.

The live agent is not a public HTTP API. It listens on `127.0.0.1`. Do not document the API key.

---

## 6. Materialization

Canonical file: `docs/build-kuya-hermes.md`. Root copy: `AGENTS.md`, marked MATERIALIZED, pointing here. Edit this file, then update the root pointer. Do not treat the root file as a second spec.

---

## Self-Check

- [x] Read order points at the locked docs
- [x] Stack pins match the file headers on 2026-10-02
- [x] Golden paths are the real commands
- [x] §5.2 states that crawler files are absent instead of inventing a policy
- [x] PRD-F1 and PRD-F4 guards are named
