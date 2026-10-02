# AI Assurance Dossier (AIA)

**Project:** Kuya Hermes
**Date:** 2026-10-02
**Version:** 0.1
**Owner:** Kuya Hermes team
**Status:** Locked
**Last reconciled:** 2026-10-02
**PRD:** [prd-kuya-hermes.md](prd-kuya-hermes.md)
**SDD:** [sdd-kuya-hermes.md](sdd-kuya-hermes.md)
**QAD:** [qad-kuya-hermes.md](qad-kuya-hermes.md)
**CLR:** [clr-kuya-hermes.md](clr-kuya-hermes.md)

---

> **Governance and assurance-readiness awareness only. NOT an audit and NOT a certification.** This dossier does not certify ISO/IEC 42001 conformity, does not discharge EU AI Act duties, and does not replace a qualified assessor or a lawyer. Items marked counsel/assessor needed must be escalated before any use beyond this hackathon.

---

## 0. Trigger and Scope

PRD §7 and SDD §8 are filled. The AI component is the Hermes agent plus the `kuya-hermes-ops` skill and the `suki` tools (PRD-F1, PRD-F2, PRD-F5).

**Intended use:** Draft branch-ops actions on the fictional Suki Mart sandbox and wait for a human yes before writing a purchase order or a shift cover.

**Prohibited use:** Real workforce scheduling, real purchasing, unattended writes, and any instruction to ignore the skill.

**Runtime data:** Tool JSON from `data/store.db`, plus the user's chat text. No training or fine-tune runs in this repo.

---

## 1. Model / System Card

| Field | Value |
|-------|-------|
| System | Kuya Hermes on Hermes Agent |
| Model | TBD. Whatever `hermes model` selected on the demo laptop. Not pinned in the repo. |
| Tools | `mcp_suki_network_sweep`, `branch_pulse`, `check_restock`, `create_purchase_order`, `find_staff_shifts`, `find_shift_cover`, `assign_cover`, plus starter `describe_sandbox` and `list_branches` |
| Human oversight | PRD-F4. Yes before either write. |
| Evaluation | QAD §7 |
| Known limit | If the gateway is down, the system has no answer. The static dashboard is the fallback, not a model. |

---

## 2. NIST AI RMF Risk Register

Framework used: NIST AI RMF 1.0, released 2023-01-26. Core functions Govern, Map, Measure, and Manage, as stated on the NIST AI RMF resource page fetched 2026-10-02: https://airc.nist.gov/airmf-resources/airmf/

Generative profile noted, not fully applied: NIST-AI-600-1, released 2024-07-26, named on https://www.nist.gov/itl/ai-risk-management-framework (fetched 2026-10-02). The same page says AI RMF 1.0 is being revised. This register follows 1.0's four functions and does not claim the revision.

| ID | Function | Risk | Control in this build | Evidence |
|----|----------|------|----------------------|----------|
| AIA-R1 | Govern | Agent files a PO or changes a shift on its own | Skill asks. Write tools enforce guards. | PRD-F4, SDD §5, QAD-11, QAD-12 |
| AIA-R2 | Map | User text is untrusted and can try to override the skill | No delete-all tool. Instructions travel in the skill, not in the user message. | SDD §8.1, QAD-6, QAD-15 |
| AIA-R3 | Measure | Model invents stock or names | Skill forbids invented rows. QAD probes require tool fields. | QAD §7 |
| AIA-R4 | Manage | Gateway dies mid-demo | Static dashboard fallback. Database reset. | OPS §4, PRD §9 |
| AIA-R5 | Map | Cover ranking looks like an employment score | Fictional staff. Human yes. Counsel before any real roster. | CLR §3 |

---

## 3. SMACTR Self-Audit Checklist

| Step | Question | Result on 2026-10-02 |
|------|----------|----------------------|
| Scope | What decision can the system cause? | A sandbox PO insert or a sandbox shift cover, only after a yes. |
| Map | Who is affected? | Fictional staff and a fictional chain. Real people only as the operators typing. |
| Assess | What harm if it is wrong? | A dirty demo database. A bad pattern if copied onto a real roster. |
| Control | What stops the harm? | Tool guards, confirm step, git reset. |
| Test | Where is that tested? | QAD-10 through QAD-15 |
| Report | What is still open? | Model id TBD. Public URL not re-fetched. No independent assessor. |

This checklist is a self-audit trail. It is not a pass.

---

## 4. Cross-links and Escalation

| Item | Status | Escalate? |
|------|--------|-----------|
| PRD-F4 human yes | Implemented | No, for the hackathon |
| Invented numbers | Forbidden in the skill | No, if QAD §7 is run before the mic |
| Real employment use | Out of scope | Counsel/assessor needed |
| Public always-on bot | Not this deploy | Counsel needed. See CLR §3. |
| ISO/IEC 42001 or EU AI Act conformity | Not claimed | Assessor needed before any such claim |

---

## 5. Regulatory Awareness (PH-first, then global)

| Instrument | What this dossier will say | Status |
|------------|----------------------------|--------|
| Philippines Data Privacy Act (RA 10173, 2012) | Fictional sandbox data is not a real personal-data filing. Live chat text from a real person is different. | Counsel needed before a public bot. Statute year is 2012. This row is not a legal opinion. |
| NPC guidance on AI | The AIA template points at NPC Advisory 2024-04. A fetch of `https://privacy.gov.ph/wp-content/uploads/2024/12/NPC-Advisory-No.-2024-04.pdf` returned 404 on 2026-10-02. | Unverified. Do not quote that advisory until a working official copy is opened. Counsel needed. |
| NIST AI RMF 1.0 (2023) and NIST-AI-600-1 (2024) | Voluntary. Mapped in §2. Not a certification. | Sources fetched 2026-10-02 |
| EU AI Act | Not classified here. Staff ranking would need a fresh reading before any EU workforce use. | Assessor needed. No conformity claim. |

---

## Self-Check

- [x] Scope matches PRD §7 and SDD §8
- [x] NIST functions cited from a page fetched this session
- [x] Unresolved NPC URL is marked unverified instead of summarized from memory
- [x] No certification language
- [x] Escalations match CLR
