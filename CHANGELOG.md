# Changelog

All notable changes to the EU AI Act Blueprint are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and the project follows semantic versioning (MAJOR.MINOR.PATCH).

---

## [0.1.6] - 2026-09-29

### Fixed
- **Re-verified every dated entry in `data/timeline.yaml` against primary sources** (the OJ texts of Regulation (EU) 2024/1689 and Regulation (EU) 2026/1744, Commission pages). `last_verified` 2026-07-06 to 2026-09-29; `version` 0.1.5 to 0.1.6.
- **Council date settled.** 29 June 2026 is correct: footnote 4 of Regulation (EU) 2026/1744 records the European Parliament position of 16 June 2026 and the Council decision of 29 June 2026. 8 July 2026 is the signature date (the "of 8 July 2026" in the title, "Done at Strasbourg, 8 July 2026"), not the Council's adoption. The file now states both.
- **Code of Practice signatory deadline** moved from 22 July to 27 July 2026 (18:00 CEST), per the Commission's Q&A on signing the code. Status set to `in_force` because the date has passed; the Code itself stays voluntary.
- **2 Dec 2026 milestone:** the transition for Art. 50(2) marking is four months (2 Aug to 2 Dec 2026), not three, and covers only providers of systems placed on the market before 2 Aug 2026 (Art. 111(4)). Source now cites the adopted Regulation instead of the political agreement; "pending formal adoption" note removed.
- **Regulatory sandboxes (2 Aug 2027):** source corrected to Art. 57(1) as amended by the Omnibus (the original deadline was 2 Aug 2026).
- **2 Aug 2025 milestone:** the Commission's GPAI fines (Art. 101) were excluded from that date and apply from 2 Aug 2026; the description no longer implies otherwise.
- **2 Aug 2026 milestone** status `upcoming` to `in_force`; notes on the 20 July 2026 guidelines added.
- **Annex III and Annex I milestones:** sources now cite Art. 113 as amended; "awaiting publication" notes replaced with the OJ publication (24 July 2026) and entry into force (27 July 2026). Annex I description now separates Section A products from Section B (vehicles, aviation, marine, rail, and now machinery), which the high-risk requirements reach through sectoral law (Art. 2(2)). The legacy-system note now uses the Art. 111(2) wording and the 2 Aug 2030 public-authority deadline.
- README timeline table, `docs/01-overview/risk-pyramid.md`, `docs/01-overview/scope-and-jurisdiction.md` and `docs/03-controls/methodology.md` updated to match. The catalog itself has not been re-versioned against the adopted text yet; that is still pending.

## [0.1.5] — 2026-07-06

### Changed
- **AI Omnibus recorded as formally adopted.** `data/timeline.yaml` moved the two high-risk milestones (Annex III, 2 Dec 2027; Annex I, 2 Aug 2028) and the watermarking / nudifier-ban milestone from `pending_adoption` to `upcoming`, and updated their `source`/`notes` to cite the formal adoption (European Parliament 16 June 2026; Council of the EU final green light 29 June 2026; awaiting publication in the Official Journal). The header update-protocol comment and the top-level `sources` list were updated to match. This reconciles the open-source source of truth with the live tracker on manzambi.com/tracker, which already reflected the adoption.

### Added
- **Code of Practice signatory deadline (22 July 2026)** added as a milestone — the Commission's cut-off for submitting signatory forms to appear on the initial-signatory list for the voluntary Code of Practice on Transparency of AI-Generated Content, before Art. 50 applies. Flagged as a voluntary Code, not a statutory deadline.
- **GPAI enforcement clarified.** The 2 Aug 2026 transparency milestone now notes that Art. 50 obligations were confirmed *not* deferred by the Omnibus (only Art. 50(2) watermarking receives a grace period to 2 Dec 2026), and that from 2 Aug 2026 the Commission / AI Office may fine GPAI providers up to EUR 15 000 000 or 3% of worldwide turnover (Art. 101). A matching `penalties` tier for GPAI provider obligations (Art. 101) was added.

### Why
The credibility of a compliance tracker rests on its dates being verifiably fresh at the source. The committed timeline lagged the live site — it still marked the Omnibus `pending_adoption` / "expected July 2026" after the Council's 29 June final green light. `last_verified` bumped 2026-06-20 → 2026-07-06; `version` 0.1.4 → 0.1.5.

---

## [0.1.4] — 2026-06-22

### Fixed
- **README reconciled with what is actually in the repository.** The "Three deliverables" table, the "Run the compliance demo" quick-start block, and the project-structure tree all described an end-state repo — a runnable `project/` demo (`docker compose up`, `pytest project/tests/`), seven overview chapters, per-framework mapping files, `scripts/`, `site/`, and CI — none of which exist yet. The table now carries explicit status markers (✅ available / 🚧 in progress / 🔜 planned), the demo quick-start is labelled *planned — Phase 2* instead of presenting failing commands, and the structure tree shows the real tree today with a separate "Planned" list. `STATUS.md` was already accurate; the README front door now matches it.
- **Stale contact link.** README author link pointed to `manzambi.com/contact` (removed from the site); updated to `manzambi.com/about#contact`.

### Why
The blueprint is about to be linked from a published article, which will send first-time visitors who clone and follow the README. Broken links and quick-start commands that fail on a fresh clone are the fastest way to lose a sharp reader's trust. This pass makes the front door honest without trimming the roadmap.

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
