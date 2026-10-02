<p align="center"><img src="assets/kuya-hermes-fullbody.png" alt="Kuya Hermes mascot" width="220"></p>

# Kuya Hermes

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Status: Rapid Production](https://img.shields.io/badge/Status-Rapid%20Production-green)](docs/index.md)
[![Stack: Hermes + Python](https://img.shields.io/badge/Stack-Hermes%20%2B%20Python-black)](https://hermes-agent.nousresearch.com/docs)
[![Docs: FMD](https://img.shields.io/badge/Docs-FMD-333)](docs/index.md)

One Hermes agent runs Suki Mart branch ops for HQ in Hermes Desktop and for branch managers on Telegram, over the same MCP tools and skill.

CAMP / RUN Hermes Agent hackathon, 2 October 2026, Avtica Office. Track: Open Innovation.

Built with the [Foundational Matrix Documents (FMD)](https://github.com/polsalarm/kuya-hermes) workflow recorded in [docs/index.md](docs/index.md). The pitch deck is separate: [Kuya Hermes Pitch](https://docs.google.com/presentation/d/1FUpL2Lwria9scJyw579aeD1j7PTHWj7t_eRVc9OhJ8Y/edit?usp=sharing).

### Links

| What | Link |
|---|---|
| Pitch deck (12 slides) | https://docs.google.com/presentation/d/1FUpL2Lwria9scJyw579aeD1j7PTHWj7t_eRVc9OhJ8Y/edit?usp=sharing |
| Website | https://kuya-hermes.vercel.app |
| Live dashboard snapshot | https://kuya-hermes.vercel.app/dashboard |
| Live demo with real Hermes chat (temporary tunnel, only while the team laptop is on) | https://packets-tract-streets-macintosh.trycloudflare.com (no login) |
| Telegram bot | https://t.me/kuyahermes_bot |
| Source | https://github.com/polsalarm/kuya-hermes |
| Hackathon starter kit | https://github.com/TadeyRuk/hermes |
| Hermes Agent docs | https://hermes-agent.nousresearch.com/docs |

The Vercel site is a static snapshot of `data/store.db` as of 2026-09-30. Live Kuya chat runs in `uv run web/app.py` and on Telegram, and only while the team laptop is running the Hermes gateway.

## Quick start

```powershell
hermes mcp add suki --command uv --args run C:\path\to\kuya-hermes\mcp-server\server.py
xcopy /E /I skills\kuya-hermes-ops %LOCALAPPDATA%\hermes\skills\kuya-hermes-ops
xcopy /E /I desktop-plugin\kuya-hermes-hq %LOCALAPPDATA%\hermes\desktop-plugins\kuya-hermes-hq
copy persona-SOUL.md %LOCALAPPDATA%\hermes\SOUL.md
hermes gateway restart
hermes desktop
```

On Windows the Hermes home is `%LOCALAPPDATA%\hermes`, not `%USERPROFILE%\.hermes`. In Desktop: Ctrl+K, Reload desktop plugins, then open **Kuya Hermes HQ**.

Reset the sandbox after a demo:

```powershell
git checkout -- data/store.db
```

`python data/seed.py` rebuilds the same file. Requirements: Hermes Agent, Hermes Desktop, a configured `hermes model`, `uv`, Python 3.10+, and this repo.

Local website:

```powershell
uv run web/app.py
```

Open http://localhost:8787. Dashboard: http://localhost:8787/dashboard. For live chat, set `API_SERVER_ENABLED=true` and `API_SERVER_KEY` in the Hermes `.env`, then restart the gateway. The key stays on the server.

Optional public tunnel: set `SITE_PASSWORD`, run the site, then `cloudflared tunnel --url http://localhost:8787`. Before that, lock the API-server agent to the suki tools with `hermes config set platform_toolsets.api_server '["mcp-suki"]'` and disable any other MCP servers.

Static Vercel snapshot: `uv run web/build_static.py`, then deploy `web/dist`.

**Pre-flight:** gateway up, `store.db` still at the sandbox date, plugin reloaded, Telegram session ready. Presenter: any of the six teammates.

## What it does

Suki Mart's branches lose sales because stock, purchase orders, suppliers, shifts, and tickets are separate. On 2026-09-30 in `data/store.db`:

- **47 items are out of stock.** Ermita has 14, and none of those have a purchase order.
- **12 branch-product pairs have duplicate open purchase orders.** BGC's Calamansi Juice 1L (SKU SM-BEV-0050) has 4.
- **Visayas Canning Corp. promises 5 days and averages 11.3.**
- **46 open or pending tickets were never answered,** on top of shifts below target.

Kuya Hermes runs one loop: detect, check, propose, confirm, act. The confirm line is "I-file ko na ba?"

| Layer | What we built | Judging |
|---|---|---|
| MCP, the hands | `mcp-server/server.py`, server name `suki`. Seven domain tools: `network_sweep`, `branch_pulse`, `check_restock`, `create_purchase_order`, `find_staff_shifts`, `find_shift_cover`, `assign_cover`. SQL stays inside the tools. `describe_sandbox` and `list_branches` are starter helpers and are not part of the seven. | MCP, 20. Deck slide 8. |
| Skill, the playbook | `skills/kuya-hermes-ops`. Workflows: full sweep, branch pulse, fix stockouts, cover an absence. Reads Taglish. Asks before every write. | Skill, 20. Deck slides 7 and 9. |
| Desktop plugin, the face | `desktop-plugin/kuya-hermes-hq`. Sidebar page, Run full sweep, live risk badges, 12-branch picker, branch pulse, fix stockouts, cover shift gaps, Ask Kuya, side pane, Ctrl+K. | Desktop plugin, 20. Deck slide 5. |
| Same path on Telegram | Hermes gateway. Floor reports use the same skill and tools. | End-to-end, 10, with the row below. Deck slides 6 and 7. |

**End-to-end:** HQ button or Telegram message, `kuya-hermes-ops`, `mcp_suki_*`, `data/store.db`, answer in the same chat, then a confirmed write, then the result. Only `create_purchase_order` and `assign_cover` write. The first refuses a duplicate open PO. The second runs only after a yes.

**Relevance:** the four sandbox facts above. Open Innovation on a business-operations problem. Deck slides 2 and 3.

**Uniqueness:** one agent, two surfaces, real lead time instead of the supplier promise, duplicate-PO refusal, Taglish field reports. Deck slide 6 and slide 9. This is not the upstream starter, and it is not the earlier single-store prototype in `sari-sari/`.

## Documentation

| Doc | Purpose |
|-----|---------|
| [Index](docs/index.md) | Manifest. Built on FMD v1.28.1. |
| [IDEA](docs/idea-kuya-hermes.md) | Spark, user, cut line |
| [Scrutiny](docs/scrutiny-kuya-hermes.md) | Gate: PROCEED WITH FIXES |
| [PRD](docs/prd-kuya-hermes.md) | Scope and PRD-F IDs |
| [SDD](docs/sdd-kuya-hermes.md) | MCP, web, security |
| [QAD](docs/qad-kuya-hermes.md) | Happy, sad, and abuse paths |
| [DSD](docs/dsd-kuya-hermes.md) | Navy and gold tokens |
| [Judging](docs/JUDGING.md) | Official 100-point rubric |

**Living design files:** [BRAND.md](BRAND.md) · [DESIGN.md](DESIGN.md)

## Demo

Deck slide 10. Three beats:

| When | What the room sees |
|---|---|
| 0:30 | HQ, Run full sweep. Ermita and Alabang rank worst. Badges fill from the tool. |
| 1:30 | Ermita, branch pulse, then fix stockouts. Open POs are skipped. A yes returns PO numbers. |
| 2:30 | Telegram: "di pumasok si John Soriano bukas ng 7am sa Alabang." Kuya finds shift 14723 and proposes Rowena Tomas (EMP-0156, fewest absences). A yes books the cover. |

Fallback if live chat dies: https://kuya-hermes.vercel.app/dashboard. Do not demo settings, a seed rebuild, or `sari-sari/`.

| Criterion | Points | Where |
|-----------|-------:|-------|
| MCP Server | 20 | Slide 8. `mcp-server/server.py` |
| Skill | 20 | Slides 7 and 9. `skills/kuya-hermes-ops/SKILL.md` |
| Desktop Plugin GUI | 20 | Slide 5. `desktop-plugin/kuya-hermes-hq` |
| End-to-End Integration | 10 | Slide 7. Button or message, skill, MCP, `store.db`, same chat |
| Relevance | 15 | Slides 2 and 3. Sandbox date 2026-09-30 |
| Uniqueness | 10 | Slides 6 and 9 |
| Demo and Pitch | 5 | Slide 10, inside a 5-minute slot: problem, then Hermes, then working output |

## Team

CAMP / RUN, 2 October 2026.

- [Carlos Jerico Dela Torre](https://www.linkedin.com/in/delatorrecj)
- [Fathi Mahad](https://www.linkedin.com/in/fathimahad/)
- [Gerald Berongoy](https://www.linkedin.com/in/geraldberongoy/)
- [Keanu Agustin](https://www.linkedin.com/in/keanuagustin31/)
- [Paul Dacalan](https://www.linkedin.com/in/paul-dacalan/)
- [Xander Dacillo](https://www.linkedin.com/in/lord-xander-dacillo-ba627b329/)

## Assets

- `assets/kuya-hermes-fullbody.png`, `assets/kuya-hermes-avatar.png`, `assets/kuya-hermes-avatar-160.png`
- `assets/icons.md`: inline SVG, `currentColor`
- `assets/ui-inspo.png`: HQ page reference

`sari-sari/` is an earlier prototype: the same persona, one sari-sari store, Telegram and Google Sheets. It is not this submission.

## Built on

This repo started from the [Camp Run with Hermes Agent starter kit](https://github.com/TadeyRuk/hermes). Mechanics and the 100-point rubric stay in [docs/JUDGING.md](docs/JUDGING.md). The starter's "how to begin from the template" pages are upstream. The layers above are the team's build.

## License

MIT. See [LICENSE](LICENSE). Suki Mart and every person in the sandbox are fictional.

---

*README materialized from FMD README_Template.md · 2026-10-02*
