# Wrap & Next Steps (WRAP)

**Project:** Kuya Hermes
**Date:** 2026-10-02
**Version:** 0.1
**Owner:** Kuya Hermes team
**Status:** Locked
**Last reconciled:** 2026-10-02
**IDEA:** [idea-kuya-hermes.md](idea-kuya-hermes.md)
**PITCH:** N/A as a markdown file. Deck: https://docs.google.com/presentation/d/1FUpL2Lwria9scJyw579aeD1j7PTHWj7t_eRVc9OhJ8Y/edit?usp=sharing

---

## 1. Outcome Snapshot

**Event / sprint:** CAMP / RUN Hermes Agent hackathon, 2 October 2026, Avtica Office. Open Innovation.

**Result:** TBD. Judging had not posted a placement when this wrap was written.

**What shipped:** `suki` MCP server, `kuya-hermes-ops` skill, `kuya-hermes-hq` plugin, Telegram on the same agent, local web app, static snapshot, and this doc suite.

---

## 2. Keep / Cut / Borrow

| Keep | Cut | Borrow |
|------|-----|--------|
| Confirm before write | Generic SQL | Hermes gateway, Desktop SDK, starter sandbox |
| Real versus promised lead time | `sari-sari/` as the submission | FastMCP v1 pin |
| Taglish field reports | Unattended writes | Vercel for the static snapshot only |
| One skill for both surfaces | A second database | |

---

## 3. Learnings (blameless)

- The demo dies when the laptop gateway dies. The static dashboard is the spare, and it cannot file a PO.
- Duplicate-PO refusal has to live in the tool, not only in the prompt. The skill can be talked past. The INSERT guard cannot.
- Windows Hermes home is `%LOCALAPPDATA%\hermes`. Documenting the Unix path wastes the first ten minutes.
- Staff cover ranking is a good demo and a bad default if anyone points it at a real roster.

---

## 4. Scale & Continuation

If the team continues after the event:

1. Record the placement in this section.
2. Pin the Hermes model id that actually won the demo.
3. Add `robots.txt` only if the public snapshot should state a crawler policy.
4. Keep writes behind a yes if a real store is ever connected.
5. Talk to counsel before any real staff ranking. See [clr-kuya-hermes.md](clr-kuya-hermes.md) §3.

Archive is also fine. The repo already runs the demo without further scope.

---

## 5. Production Readiness Gate (final check)

| Check | Status on 2026-10-02 |
|-------|----------------------|
| Security reviewed | Partial. Write guards and key handling are in the SDD. No external pentest. |
| Data and compliance mapped | CLR exists. Counsel still needed before a public bot. |
| AI assurance | AIA exists. Not a certification. Model id TBD. |
| Tests cover Must-Haves | QAD lists them. They are manual plus SQL, not a CI suite. |
| Observability | Terminal logs and a pre-mic checklist. No metrics vendor. |
| Rollback | `git checkout -- data/store.db` or `python data/seed.py`. |
| Deploy reproducible | `uv run` plus the README copy steps. No CI. |
| Frontend quality | DSD §8 audit was not run. Scores not invented. |
| Context hygiene | Skill versus user text is split in SDD §8.1. |
| Docs validated | See the session log after `check.py`. |

The hackathon demo can run on this bar. A real chain cannot, until the counsel and test rows close.

---

## 6. Owned Next Steps

| Step | Owner | When |
|------|-------|------|
| Fill placement | Kuya Hermes team | When judges announce it |
| Reset `store.db` after the demo | Person at the laptop | Same day |
| Leave the deck as the pitch | Kuya Hermes team | Done. Do not add a pitch markdown file. |

---

## Engine feedback (field report)

Session friction is in [log-kuya-hermes.md](log-kuya-hermes.md) §2. If that section stays "No friction this session", no field report is filed.

---

## Self-Check

- [x] Result is honest about the unknown placement
- [x] Learnings name systems, not people
- [x] Continuation does not pretend the demo is a production chain
- [x] Pitch pointer is the deck, not a missing markdown file
