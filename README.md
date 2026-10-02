<div align="center">

<img src="assets/kuya-hermes-fullbody.png" alt="Kuya Hermes mascot" width="220">

# Kuya Hermes

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Status: Rapid Production](https://img.shields.io/badge/Status-Rapid%20Production-green)](docs/index.md)
[![Stack: Hermes + Python](https://img.shields.io/badge/Stack-Hermes%20%2B%20Python-black)](https://hermes-agent.nousresearch.com/docs)
[![Docs: FMD](https://img.shields.io/badge/Docs-FMD-333)](docs/index.md)

CAMP / RUN Hermes Agent hackathon, 2 October 2026, Avtica Office. Track: Open Innovation.

</div>

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

**Kuya Hermes, explained in simple words.**

## The problem

Picture a grocery store chain called **Suki Mart** with **12 stores** around Metro Manila. Every store has to keep track of a lot at once:

- What's on the shelves and what has run out
- What it has ordered from suppliers
- Which suppliers actually deliver on time
- Who is working each shift, and who called in sick
- Complaints and questions from customers

The trouble is that each of these lives in its **own separate notebook**. Nobody can see all of them together, so problems slip through:

- **47 items are sold out.** The Ermita store alone has 14 empty shelf spots, and nobody has ordered more.
- **Some items were ordered more than once.** The BGC store ordered the same calamansi juice **4 times**. That's wasted money.
- **One supplier promises delivery in 5 days but really takes about 11.** Stores trust the promise and run out.
- **46 customer tickets were never answered.** Some shifts also don't have enough workers.

When shelves are empty, customers leave without buying anything, and the store loses money.

## What we built

We built a helper called **Kuya Hermes**. Think of a reliable older brother who knows every store well.

It's one AI assistant you can reach in two places:

1. **On the boss's computer at the head office.** The boss presses one button, **"Run full sweep,"** and Kuya checks all 12 stores. It ranks them from worst to best, so the boss can see right away which store needs help first.
2. **On Telegram, for store managers.** A manager can send a quick message the way they normally talk, even in Taglish, like *"di pumasok si John Soriano bukas ng 7am sa Alabang"* ("John Soriano isn't coming in tomorrow at 7am in Alabang"). Kuya finds that shift and suggests a good replacement: someone who's free and rarely misses work.

Kuya always works in the same five steps:

> **Notice → Check → Suggest → Ask "I-file ko na ba?" → Do it**

The most important step is the fourth one. **Kuya never changes anything until a real person says "yes."** It also refuses to place an order if one for the same item is already waiting, so double orders can't happen.

## Why it's valuable

| Before Kuya | With Kuya |
|---|---|
| You dig through 5 separate notebooks to find problems | One button shows every problem, ranked |
| Empty shelves go unnoticed | Kuya spots them and offers to reorder |
| The same item gets ordered twice | Kuya blocks the duplicate order |
| You trust supplier promises | Kuya plans with how long deliveries actually take |
| A sick worker means calling around to find a fill-in | One message gets you a suggested fill-in |
| The head office and the stores see different information | Both use the same assistant and the same facts |

**In one sentence:** Kuya Hermes helps a grocery chain spot problems early, fix them fast, and stay safe by always asking a human before it acts. That means fuller shelves, less wasted money, and fewer missed shifts.

One honest note: Suki Mart is made up for the hackathon. All the numbers above come from practice data, not a real company.

## Why Hermes

| Piece of Hermes | What Kuya uses it for |
|---|---|
| Desktop, the face | The boss's page and the **Run full sweep** button. |
| Skill, the playbook | The five steps, Taglish messages, and the question before any change. |
| MCP tools, the hands | They read the store notebooks and, only after a yes, place an order or book a fill-in. A second order for an item already on order is refused. |
| Telegram | Store managers send a message from the floor. |
| One agent | Head office and the stores talk to the same Kuya and the same facts. |

## The three layers

The challenge is to build all three layers and connect them.

| Layer | What we built |
|---|---|
| MCP server, the hands | `mcp-server/server.py`, server name `suki`. Seven domain tools: `network_sweep`, `branch_pulse`, `check_restock`, `create_purchase_order`, `find_staff_shifts`, `find_shift_cover`, `assign_cover`. SQL stays inside the tools. `describe_sandbox` and `list_branches` are starter helpers and are not part of the seven. |
| Skill, the playbook | `skills/kuya-hermes-ops`. Workflows: full sweep, branch pulse, fix stockouts, cover an absence. Reads Taglish. Asks before every write. |
| Desktop plugin, the face | `desktop-plugin/kuya-hermes-hq`. Sidebar page, Run full sweep, live risk badges, 12-branch picker, branch pulse, fix stockouts, cover shift gaps, Ask Kuya. |

Telegram uses the same skill and the same tools from the floor. It is not a fourth required layer.

## Competition requirements

| Criterion | Points | Where we meet it |
|---|---:|---|
| MCP Server | 20 | The seven tools above. Not a generic SQL passthrough. |
| Skill | 20 | Those workflows, triggered from a normal message, including Taglish. |
| Desktop Plugin GUI | 20 | Kuya Hermes HQ inside Hermes Desktop. |
| End-to-End Integration | 10 | A button or a Telegram message goes through the skill and the MCP tools to `data/store.db`, then the answer comes back in the same chat. Only an order and a shift cover write, and only after a yes. |
| Relevance | 15 | The four practice-data problems in The problem. Track: Open Innovation. |
| Uniqueness | 10 | One agent, two places, real delivery time instead of the supplier promise, and a refusal of a second order. Not the upstream starter. |
| Demo and Pitch | 5 | Five minutes: problem, then how Hermes is used, then working output. |

This is our own MCP on `data/store.db`. `python data/seed.py` restores the data.

## How to run

**Prerequisites:** Hermes Agent, Hermes Desktop, a configured `hermes model`, `uv`, Python 3.10+, and this repo.

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

`python data/seed.py` rebuilds the same file.

Local website:

```powershell
uv run web/app.py
```

Open http://localhost:8787. Dashboard: http://localhost:8787/dashboard. For live chat, set `API_SERVER_ENABLED=true` and `API_SERVER_KEY` in the Hermes `.env`, then restart the gateway. The key stays on the server.

Optional public tunnel: set `SITE_PASSWORD`, run the site, then `cloudflared tunnel --url http://localhost:8787`. Before that, lock the API-server agent to the suki tools with `hermes config set platform_toolsets.api_server '["mcp-suki"]'` and disable any other MCP servers.

Static Vercel snapshot: `uv run web/build_static.py`, then deploy `web/dist`.

**Pre-flight:** gateway up, `store.db` still at the sandbox date, plugin reloaded, Telegram session ready. Presenter: any of the six teammates.

## Team

CAMP / RUN, 2 October 2026.

- [Carlos Jerico Dela Torre](https://www.linkedin.com/in/delatorrecj)
- [Fathi Mahad](https://www.linkedin.com/in/fathimahad/)
- [Gerald Berongoy](https://www.linkedin.com/in/geraldberongoy/)
- [Keanu Agustin](https://www.linkedin.com/in/keanuagustin31/)
- [Paul Dacalan](https://www.linkedin.com/in/paul-dacalan/)
- [Xander Dacillo](https://www.linkedin.com/in/lord-xander-dacillo-ba627b329/)

## Docs

[Index](docs/index.md) · [IDEA](docs/idea-kuya-hermes.md) · [Scrutiny](docs/scrutiny-kuya-hermes.md) · [PRD](docs/prd-kuya-hermes.md) · [SDD](docs/sdd-kuya-hermes.md) · [QAD](docs/qad-kuya-hermes.md) · [DSD](docs/dsd-kuya-hermes.md) · [Judging](docs/JUDGING.md) · [BRAND.md](BRAND.md) · [DESIGN.md](DESIGN.md)

## License

MIT. See [LICENSE](LICENSE). Suki Mart and every person in the sandbox are fictional.
