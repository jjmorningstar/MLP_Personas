# MORNINGSTAR Case Naming & Case Numbering Format

> *"A case without a number is a case without a home."*  
> — MORNINGSTAR::ARCHITECT

**Authority:** Court ruling 2026-02-19 (Case Naming & Numbering deliberation). Vote: 4-1-0.  
**Canonical ref:** This document is the single source of truth for case identification.

---

## Formatted Conventions (Quick Reference)

| Convention | Format | Example |
|------------|--------|---------|
| **Case No.** (header) | `YYYY-CATC-NNN-DDD` | `2026-DEL-004-001` |
| **Standard transcript** | `YYYY-MM-DD-[matter-slug].md` | `2026-02-19-case-naming-and-numbering-format.md` |
| **Special Interest transcript** | `YYYYMMDD_HHMMSS_special_interest_[subject].md` | `20260216_160000_special_interest_api_design.md` |
| **Handoff document** | `HANDOFF-YYYY-CATC-NNN.md` | `HANDOFF-2026-ARCH-002.md` |
| **Header label** | `Case No.:` | *(deprecate Matter ID)* |

**Category codes:** ARCH, INFRA, DEL, CONT, SEC, EXEC, FEAT, BUG, MAINT, DOC.

---

## Case ID Format

```
YYYY-CATC-NNN-DDD
```

| Segment | Meaning | Values |
|---------|---------|--------|
| **YYYY** | Year | 4-digit (e.g., 2026) |
| **CATC** | Category code | See [Category Codes](#category-codes) |
| **NNN** | Matter sequence | 001-999 within category per year |
| **DDD** | Deliberation sequence | 001-999 within matter (first deliberation = 001) |

**Examples:**
- `2026-INFRA-001-001` — First deliberation of first infrastructure matter in 2026
- `2026-DEL-004-001` — First deliberation of fourth general deliberation matter in 2026
- `2026-CONT-001-001` — First contempt proceeding in 2026

---

## Category Codes

| Code | Meaning | Use |
|------|---------|-----|
| **ARCH** | Architectural decisions | Agent structure, protocols, framework design |
| **INFRA** | Infrastructure work | Enhancements, tooling, foundational changes |
| **DEL** | General deliberation | Full court proceedings not fitting other categories |
| **CONT** | Contempt proceedings | Contempt hearings, adversarial proceedings |
| **SEC** | Special inquiry / Security | Special Interest hearings, security posture |
| **EXEC** | Executive branch | Executive-orchestration matters |
| **FEAT** | Feature development | Feature adoption, capability addition |
| **BUG** | Bug investigation | Defect root cause, remediation |
| **MAINT** | Maintenance | Refactors, tech debt, cleanup |
| **DOC** | Documentation | Doc structure, glossary, onboarding |

---

## Transcript Header (Required)

Every F3+ transcript SHALL include:

```markdown
**Case No.:** YYYY-CATC-NNN-DDD
**Date:** YYYY-MM-DD
**Feasibility:** F[3-5]
**Presiding:** The Honorable Lucius J. Morningstar
```

**Deprecated:** `Matter ID` — use `Case No.` only.

---

## Case Title Format (Display)

For human-readable display and precedent indexing:

| Proceeding Type | Format | Example |
|-----------------|--------|---------|
| Standard / Expedited | `In Re: [Subject] — [Concise Action]` | In Re: Framework Enhancements — Ratification of Slate 1 |
| Special Interest | `Special Inquiry: [Subject] — [Focus]` | Special Inquiry: Bohemian Grove — Structure, Influence |
| Contempt | `In Re: [Respondent] — Alleged Contempt` or `DOJ vs. [Respondent]` | In Re: Xenon — Alleged Contempt of Court |
| Handoff | `Docket: [Case ID] — [Phase/Action]` | Docket: 2026-ARCH-002 — Implementation Handoff |

---

## Filename Formats

| Type | Format | Example |
|------|--------|---------|
| Standard / Expedited | `YYYY-MM-DD-[matter-slug].md` | 2026-02-17-full-session-skills-to-add-to-each-agent.md |
| Special Interest | `YYYYMMDD_HHMMSS_special_interest_[subject].md` | 20260216_160000_special_interest_xenon_fraud_elon_musk.md |
| Handoff | `HANDOFF-YYYY-CATC-NNN.md` | HANDOFF-2026-ARCH-002.md |

**Note:** Filename does not require Case No. The Case No. is in the transcript header. Slug should be descriptive and URL-safe (lowercase, hyphens).

---

## Case Registry

To prevent collisions, the Scribe assigns case IDs from a registry. Registry location: `courtroom/case-registry.yaml` (or embedded in `state/current.md` until created).

**Assignment rule:** When convening a new matter, the Judge or Scribe checks the registry for the next available NNN in the chosen category. If the matter continues (e.g., second deliberation), increment DDD.

---

## Legacy Transcripts

Transcripts created before this ruling may have non-canonical case numbers (e.g., multiple transcripts sharing 2026-DEL-001). **Grandfather rule:** Do not mass-rename or edit certified transcripts. When a legacy transcript is cited or updated, assign a canonical Case No. via addendum if needed. New transcripts SHALL use the canonical format from first line.

---

## Citation Format

- In text: `See Case 2026-DEL-004-001` or `Per 2026-INFRA-001-001`
- In precedents: Full Case ID in Master Index
- In handoffs: `Case: 2026-ARCH-002`

---

## Validation

The Court Reporter and `generate_manifest.py` SHALL validate:
- Case No. present in transcript header
- Case No. matches regex: `\d{4}-[A-Z]+-\d{3}-\d{3}`
- No duplicate Case No. across transcripts (report collisions)

---

> *"The number persists. The case endures. The record is findable."*  
> — MORNINGSTAR::SCRIBE
