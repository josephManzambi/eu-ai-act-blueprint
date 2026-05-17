# Changelog

All notable changes to the EU AI Act Blueprint are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and the project follows semantic versioning (MAJOR.MINOR.PATCH).

---

## [0.1.3] — 2026-05-15

### Fixed
- **OWASP LLM Top 10 mappings corrected to 2025 edition.** Previous mappings (12 controls) used a mix of 2023 names with self-contradictory IDs (e.g., LLM05 was used for two different risks; "Excessive Agency" appeared as both LLM06 and LLM08). All 12 affected controls updated to the canonical 2025 list: LLM01 Prompt Injection, LLM02 Sensitive Information Disclosure, LLM03 Supply Chain, LLM04 Data and Model Poisoning, LLM05 Improper Output Handling, LLM06 Excessive Agency, LLM07 System Prompt Leakage, LLM08 Vector and Embedding Weaknesses, LLM09 Misinformation, LLM10 Unbounded Consumption.
- **Penalty percentage corrected.** The "incorrect information to authorities" tier (Art. 99(5)) was previously documented as 1.5% in README and `timeline.yaml`. The regulation specifies 1%. Both files corrected.
- **Internal version metadata.** `timeline.yaml` version field updated from 0.1.2 to 0.1.3; methodology version history now includes the 0.1.2 entry; methodology self-citation updated; column count in methodology §5 corrected (16 → 17, reflecting the `status` column added earlier in this version).
- **Stale references.** `LICENSING.md` no longer lists `ROADMAP.md` (superseded by `STATUS.md` + `CHANGELOG.md`). README link to `CONTRIBUTING.md` no longer broken (file now exists).

### Added
- **Threat model** (`docs/02-architecture/threat-model.md`) — STRIDE + MITRE ATLAS + LINDDUN applied to the reference CV-screening system. Identifies 46 distinct threats and maps each to one or more AISEC controls. Achieves 100% threat-to-control coverage; introduces the project's security justification layer.
- **Timeline as single source of truth** (`data/timeline.yaml`) — All EU AI Act enforcement dates consolidated into one YAML file. Documents 9 milestones, 3 penalty tiers, and countdown anchors. References Regulation 2024/1689 and the AI Omnibus political agreement (7 May 2026).
- **`status` column** on the controls catalog — Tracks per-control implementation state (`planned` / `documented` / `implemented` / `tested`). Distinct from `maturity_level`, which describes target maturity regardless of project state.
- **`WHAT_THIS_IS_NOT.md`** — Eight explicit scope boundaries (not legal advice, not conformity assessment, not a compliance guarantee, etc.).
- **`LICENSING.md`** — Per-directory license map and practical reuse examples.
- **`CONTRIBUTING.md`** — Contribution guidelines, PR checklist, code of conduct.

### Changed
- **Maturity scale collapsed from 5 levels to 3.** The original CMMI-style 1-5 scale was never going to use levels 4 (Quantitatively Managed) or 5 (Optimizing) for this project. Replaced with: 1 = Documented, 2 = Implemented, 3 = Tested. Existing values remapped (old 1-2 → new 1; old 3 → new 2; old 4-5 → new 3). Distribution after remap: 57 controls at level 1, 19 at level 2, 3 at level 3.
- **Methodology document** updated to reflect the new maturity scale, the new `status` column, the corrected column count, and the OWASP fix.

---

## [0.1.2] — 2026-05-15

### Added
- **Controls catalog methodology** (`docs/03-controls/methodology.md`) — Formal documentation of how the catalog was derived. Defines the granularity rule ("one control = one independently testable obligation"), scope boundaries, the 15-domain structure, the cross-framework mapping precision rule, and a per-domain derivation table showing exactly how the count was reached.

### Why
The catalog without a methodology was just an opinion. With one, it is a falsifiable position. The methodology document inverts the usual posture of documentation — instead of asking readers to trust the work, it tells them how to productively challenge it (§8: "How to critique or extend the catalog").

---

## [0.1.1] — 2026-05-14

### Added
- **AISEC-PH-008** — New control covering the AI Omnibus prohibition on AI systems that generate non-consensual intimate imagery of real persons or child sexual abuse material (CSAM). Effective 2 December 2026.

### Changed
- **All enforcement timelines updated** to reflect the AI Omnibus political agreement of 7 May 2026:
  - Standalone high-risk AI systems (Annex III) — postponed by 16 months from 2 August 2026 to **2 December 2027**.
  - AI as products or safety components (Annex I) — postponed by 12 months from 2 August 2027 to **2 August 2028**.
  - Watermarking grace period for existing systems set at 3 months (compliance due 2 December 2026).
  - Machinery Regulation AI carved out entirely from the AI Act's direct application.
- **Scope chapter** updated to reflect the Machinery Regulation carveout in the cross-regulation table.
- **README implementation timeline** restructured and chronologically sorted.

---

## [0.1.0] — 2026-05-13

### Added
- **Initial controls catalog** (`data/controls.csv`) — 78 controls covering 15 domains derived from EU AI Act Articles 4-73 and Annexes III-XI. Mapped to NIST AI RMF, ISO/IEC 42001, OWASP LLM Top 10 (2025), MITRE ATLAS, GDPR, and DORA.
- **JSON Schema** (`data/controls-schema.json`) — Formal validation contract for the catalog.
- **README.md** — Project elevator pitch, structure tree, deliverables table.
- **Chapter 1: Scope and Jurisdiction** (`docs/01-overview/scope-and-jurisdiction.md`) — Art. 1-3 coverage including extraterritorial reach, actor categories, exclusions, and the open-source trap.
- **Chapter 2: Risk Classification** (`docs/01-overview/risk-pyramid.md`) — Four-tier risk pyramid, decision tree (Mermaid), Annex III table, edge cases.
- **Roadmap** (`ROADMAP.md`, now superseded by `STATUS.md` + GitHub Issues) — Initial 6-phase build plan.

### Project decisions
- **Use case:** CV-screening / candidate ranking system (Annex III area 4: Employment).
- **Actor scope:** Provider and Deployer (most realistic for enterprises building or buying AI).
- **Languages:** English (primary) + French (planned).
- **License:** Apache 2.0 for code and data; CC BY-SA 4.0 for prose documentation.
- **Hosting:** GitHub repo + separate Astro site for the technical overview.

---

## Versioning policy

The project uses semantic versioning with these conventions:

- **MAJOR** — Reserved for incompatible changes to the controls catalog schema or major scope changes (e.g., adding a new actor role).
- **MINOR** — New controls, new framework mappings, new chapters, new methodology refinements.
- **PATCH** — Corrections, clarifications, regulatory update integration that does not change control content.

Each version is tagged in git so historical compliance reports remain reproducible.

## Source of truth for dates

All regulatory dates referenced in this changelog are anchored to `data/timeline.yaml`. When the AI Omnibus is formally adopted (expected July 2026), that file will be updated and a new version released.
