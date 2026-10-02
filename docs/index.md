# Documentation Index: Kuya Hermes

**Project slug:** `kuya-hermes`
**Maintained by:** Kuya Hermes team
**Last updated:** 2026-10-02

Built on FMD v1.28.1.

---

## 1. Document Suite

| Document | File | Version | Status | Last Updated | Last Reconciled |
|----------|------|---------|--------|--------------|-----------------|
| IDEA · Idea Brief | [idea-kuya-hermes.md](idea-kuya-hermes.md) | 0.1 | Locked | 2026-10-02 | 2026-10-02 |
| SCRUTINY · Scrutiny Gate | [scrutiny-kuya-hermes.md](scrutiny-kuya-hermes.md) | 0.1 | Locked | 2026-10-02 | 2026-10-02 |
| PRD · Product Requirements | [prd-kuya-hermes.md](prd-kuya-hermes.md) | 0.1 | Locked | 2026-10-02 | 2026-10-02 |
| DSD · Design System | [dsd-kuya-hermes.md](dsd-kuya-hermes.md) | 0.1 | Locked | 2026-10-02 | 2026-10-02 |
| SDD · System Design | [sdd-kuya-hermes.md](sdd-kuya-hermes.md) | 0.1 | Locked | 2026-10-02 | 2026-10-02 |
| QAD · QA & Test Plan | [qad-kuya-hermes.md](qad-kuya-hermes.md) | 0.1 | Locked | 2026-10-02 | 2026-10-02 |
| BUILD · Build Guide | [build-kuya-hermes.md](build-kuya-hermes.md) | 0.1 | Locked | 2026-10-02 | 2026-10-02 |
| CLR · Compliance & Legal | [clr-kuya-hermes.md](clr-kuya-hermes.md) | 0.1 | Locked | 2026-10-02 | 2026-10-02 |
| AIA · AI Assurance Dossier | [aia-kuya-hermes.md](aia-kuya-hermes.md) | 0.1 | Locked | 2026-10-02 | 2026-10-02 |
| OPS · Ops & Observability | [ops-kuya-hermes.md](ops-kuya-hermes.md) | 0.1 | Locked | 2026-10-02 | 2026-10-02 |
| WRAP · Next Steps | [wrap-kuya-hermes.md](wrap-kuya-hermes.md) | 0.1 | Locked | 2026-10-02 | 2026-10-02 |
| LOG · Session log | [log-kuya-hermes.md](log-kuya-hermes.md) | 0.1 | Locked | 2026-10-02 | 2026-10-02 |
| Hackathon mechanics | [JUDGING.md](JUDGING.md) | N/A | N/A | 2026-10-02 | N/A |

**Materialized at project root (not in `docs/`):** `README.md`, `BRAND.md`, `DESIGN.md`, `AGENTS.md`. No `MODEL_CARD.md`.

Skipped on purpose: VALIDATION, BRD, UES, GTM, RFC, SAD, and a markdown PITCH. The pitch is the Google Slides deck linked from the README and from [wrap-kuya-hermes.md](wrap-kuya-hermes.md).

### RFCs (one per major feature)

No RFCs. The architecture is the one already in the repo.

### 1.1 Traceability Matrix

| PRD-F# | Feature (short) | Priority | In SDD | In QAD | In RFC |
|--------|-----------------|----------|--------|--------|--------|
| PRD-F1 | Domain MCP tools | Must-Have | yes | yes | N/A |
| PRD-F2 | Ops skill | Must-Have | yes | yes | N/A |
| PRD-F3 | HQ desktop plugin | Must-Have | yes | yes | N/A |
| PRD-F4 | Confirm before write | Must-Have | yes | yes | N/A |
| PRD-F5 | Telegram field channel | Must-Have | yes | yes | N/A |
| PRD-F6 | Read-only web snapshot | Should-Have | yes | yes | N/A |
| PRD-F7 | Generic SQL and sari-sari | Won't-Have (v1) | yes | yes | N/A |

---

## 2. Change Log

No change records. These docs were locked together on 2026-10-02 against the shipped code.

| CR ID | Date | Summary | Trigger doc | Docs touched | File |
|-------|------|---------|-------------|--------------|------|
| none | 2026-10-02 | Initial lock. No CR file. | IDEA | suite | none |

---

## 3. Incident Log (Postmortems)

No P0 or P1 incidents recorded.

| PM ID | Incident date | Severity | Summary | Action items closed? | File |
|-------|---------------|----------|---------|----------------------|------|
| none | 2026-10-02 | none | No incident file. | N/A | none |

---

## 4. Health Check

- [x] Every Locked doc's **Last Reconciled** date is 2026-10-02, the day the code was read for this suite.
- [x] No doc is sitting in Draft.
- [x] No open Change Record.
- [x] PRD-F IDs cited by the SDD and QAD are defined in the PRD.
- [x] §1.1 matches the Must-Have set PRD-F1 through PRD-F5.
- [x] No BRD, so no BRD-M# metrics. PRD §5.6 says analytics are none.
- [x] No revenue model. UES skipped.
- [x] No SAD. No agent roster files to match.
- [x] BUILD §3 pins were checked against the script headers on 2026-10-02.
- [x] No open postmortems.
- [x] Production readiness is recorded in [wrap-kuya-hermes.md](wrap-kuya-hermes.md) §5. The demo can run. A real chain is not claimed.
- [x] Validator green: `python scripts/check.py` on this repo, 2026-10-02, 0 failures and 0 warnings, including `--scale rapid`.

---

## 5. Notes

Presenter is still TBD. Placement is still TBD. The Hermes model id is still TBD. Those three are the scrutiny carry-forward items.
