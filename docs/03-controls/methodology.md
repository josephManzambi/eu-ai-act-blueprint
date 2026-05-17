# Controls Catalog Methodology

> **Purpose:** This document explains how the controls catalog (`data/controls.csv`) was derived from the EU AI Act and cross-mapped to six supporting frameworks. It exists so that any user — auditor, engineer, CISO, contributor — can understand *why* each control exists, *how* the count was determined, and *how* to extend or critique the catalog defensibly.
>
> **TL;DR:** Controls are derived bottom-up from EU AI Act obligations. One control represents one independently testable obligation. The total count is the natural result of applying the granularity rule below — it is not a target.

---

## 1. Why a methodology document

A controls catalog without a documented methodology is just an opinion. Anyone can list "79 controls" and claim coverage. What makes a catalog **defensible** is the ability to answer four questions for every control:

1. **What regulatory obligation does this control implement?**
2. **Why is this a separate control instead of being merged with another?**
3. **What would have to be true for an organization to claim this control is implemented?**
4. **How would an auditor verify this claim?**

This document defines the rules that make those questions answerable. The rules are deliberately explicit so that disagreements about the catalog can be productive: critics must engage with the *rules*, not with the resulting count.

---

## 2. Scope and boundaries

### 2.1 In scope

The catalog covers:

- **EU AI Act (Regulation 2024/1689)** obligations as adopted on 21 May 2024, as amended by the **AI Omnibus** political agreement of 7 May 2026 (pending formal adoption).
- Obligations for two AI Act actor roles: **Provider** (Art. 16) and **Deployer** (Art. 26).
- Obligations across all four risk tiers: **Prohibited** (Art. 5), **High-Risk** (Art. 6 + Annex III + Annex I), **Limited Risk / Transparency** (Art. 50), and **GPAI** (Art. 51–55).
- Cross-framework mappings to: **NIST AI RMF 1.0**, **ISO/IEC 42001:2023**, **OWASP Top 10 for LLM Applications (2025)**, **MITRE ATLAS**, **GDPR (2016/679)**, **DORA (2022/2554)**.

### 2.2 Out of scope

The catalog deliberately excludes:

| Excluded | Reason |
|----------|--------|
| Importer obligations (Art. 23) | Importers are intermediaries; their core duty is to verify Provider compliance. Adding them would duplicate Provider controls. Add in a future version if a use case requires it. |
| Distributor obligations (Art. 24) | Same rationale as importers. |
| Notified Body obligations (Art. 28–39) | Notified Bodies are regulators, not regulated entities. Out of scope for a builder's catalog. |
| National competent authority obligations (Art. 70+) | Same rationale. |
| Member State-specific implementation rules | These vary by jurisdiction and change over time. Catalog stays at EU level. |
| Voluntary codes of conduct (Art. 95) | Not legally binding. Catalog focuses on legal obligations. |
| Generic information-security controls (e.g., "encrypt data at rest") | Already covered by ISO 27001, NIST CSF, SOC 2. Catalog focuses on **AI-specific** controls, not infrastructure baseline controls. |
| Process-only ISO 42001 clauses with no AI Act counterpart | Mapped where overlap exists; not duplicated as standalone controls. |

### 2.3 Geographic and temporal scope

- **Geographic:** EU-wide obligations only. National-level guidance (e.g., from CNIL, ANSSI, BSI) is referenced in supplementary docs but not treated as a primary source.
- **Temporal:** The catalog reflects the regulation as of **15 May 2026**, including the AI Omnibus political agreement. Each control is versioned (see §7); when the regulation changes, controls are amended with explicit changelog entries rather than silently rewritten.

---

## 3. The unit of analysis: what is "one control"?

**A control is one independently testable obligation.**

This is the core rule. Everything else flows from it. To be a single control, a requirement must satisfy three tests:

### Test 1: Independent implementation

A control must be something an organization can build, document, or test **on its own**, without simultaneously implementing other controls. If two requirements always have to be implemented together as a single artifact, they should be one control.

> **Example:** AI Act Art. 10(3) requires training data to be (a) relevant, (b) sufficiently representative, and (c) free of errors. These are three different properties, but they are verified through the **same data quality pipeline**. So they are one control: **AISEC-DG-002 Training Data Quality and Relevance**.

### Test 2: Independent verification

A control must be something an auditor can verify is implemented through **distinct evidence**. If two requirements would produce overlapping evidence — the same document, the same test output, the same log — they should be merged.

> **Example:** Art. 12(2) lists four items that must be logged: (a) period of use, (b) reference database, (c) input data, (d) human verification results. These produce **different evidence** (different log fields, different retention concerns, different access patterns), so they are split into AISEC-LG-002, LG-003, and LG-004. AISEC-LG-001 is the meta-control for "you have logging at all."

### Test 3: Independent failure mode

A control must be something that can fail on its own. If two requirements always succeed or fail together, they are one control.

> **Example:** Art. 15(5) requires resilience against (a) data poisoning, (b) adversarial inputs, and (c) confidentiality attacks. These have **completely different failure modes**, different attack vectors, different mitigations — so they are three controls (AISEC-CS-002, CS-003, CS-004), not one "cybersecurity" control.

### When to split vs. merge

| Situation | Decision | Why |
|-----------|----------|-----|
| One sentence in the regulation, one artifact, one test | **One control** | Atomic |
| Multiple sentences, same artifact, same test | **One control** | Cohesive |
| One sentence, multiple distinct artifacts | **Split into multiple controls** | Each artifact needs its own evidence |
| One article, multiple distinct failure modes | **Split into multiple controls** | Each failure mode needs its own test |
| Different actor roles for the same requirement | **Split into Provider + Deployer controls** | Different obligations, different evidence |

This is judgment, not formula. Two reasonable people may split or merge differently. The methodology's job is to make the split *explicit* and *consistent within the catalog*.

---

## 4. Control ID format

```
AISEC-{DOMAIN}-{SEQ}
       ↑       ↑
       │       └─ Three-digit sequence (001, 002, ...) within domain
       └─ Two-letter domain code (see §4.1)
```

### 4.1 Domain codes

The 15 domains are derived from **structural groupings in the AI Act itself**, not from a generic security taxonomy. Each domain maps to a specific obligation cluster:

| Code | Domain | Primary AI Act articles | Why a separate domain |
|------|--------|------------------------|----------------------|
| **RM** | Risk Management | Art. 6, 9 | Risk classification + Art. 9 risk management system are the entry point to compliance |
| **DG** | Data Governance | Art. 10 | Art. 10 is the longest and most prescriptive article; data-specific controls cluster here |
| **TD** | Technical Documentation | Art. 11 + Annex IV | Annex IV defines the structure; one control per Annex IV section |
| **LG** | Logging | Art. 12, 19 | Art. 12 has four explicit log-content requirements; split per requirement |
| **TR** | Transparency | Art. 13, 50 | Provider-side (Art. 13) and externally-facing (Art. 50) transparency are merged into one domain |
| **HO** | Human Oversight | Art. 14, 26(2) | Human oversight is a design property (Art. 14) and an operational practice (Art. 26) |
| **AC** | Accuracy | Art. 15(1) | Accuracy is one of the three Art. 15 dimensions; isolated for clarity |
| **RB** | Robustness | Art. 15(3)(4) | Robustness is structurally separate from cybersecurity in Art. 15 |
| **CS** | Cybersecurity | Art. 15(5) | Cybersecurity has its own subsections in Art. 15(5)(a)(b)(c); split per attack class |
| **PM** | Post-Market Monitoring | Art. 20, 72, 73 | Post-market is a separate lifecycle phase with distinct obligations |
| **CA** | Conformity Assessment | Art. 17, 43, 47, 48, 49 | Conformity assessment is procedurally distinct from technical controls |
| **DP** | Deployer Obligations | Art. 26, 27 | Deployer duties are legally distinct from Provider duties; separated for clarity even when content overlaps |
| **GP** | GPAI | Art. 53, 55 | GPAI is a structurally separate regime in the regulation |
| **PH** | Prohibited Practices | Art. 5 | Prohibitions are negative obligations ("don't do this") and need different evidence (a "did not occur" demonstration) |
| **GV** | Governance | Art. 4, 21, 22 + cross-framework | Catch-all for org-level obligations and cross-regulation alignment (GDPR, DORA) |

### 4.2 Why these 15 domains and not 10 or 20

A different methodology could group "AC + RB + CS" into one "Art. 15 Trustworthy AI" domain (10 domains total), or split CS into "data attacks / model attacks / supply chain attacks" (17+ domains). Both would be defensible.

This catalog uses **15 domains** because:

1. Each domain maps to a **structural unit of the regulation** (article-level or Annex-level), making cross-reference unambiguous.
2. Each domain has **at least 2 controls** (no singleton domains), justifying its existence.
3. No domain has **more than 9 controls**, keeping cognitive load manageable.

If a future version needs a 16th domain (e.g., for AI assurance under upcoming harmonized standards), it can be added without renumbering existing controls.

---

## 5. The control schema

Every row in `controls.csv` has the same 17 columns. Each column is defined in `controls-schema.json`. Here is the rationale for each:

| Column | Purpose | Defensibility test |
|--------|---------|-------------------|
| `control_id` | Stable identifier | Pattern-matched against regex; unique across catalog |
| `control_name` | Short name (≤100 chars) | Must be descriptive enough that the ID alone isn't required to understand |
| `description` | Full obligation statement in plain language | Must paraphrase the regulation, not quote it; must be implementable |
| `ai_act_article` | Source article(s) | Every control must trace to at least one article (or be marked as a cross-framework "Recommended" control with `—`) |
| `ai_act_obligation` | Mandatory / Recommended / Prohibited | "Mandatory" = explicitly required by the Act; "Recommended" = derived from cross-framework analysis; "Prohibited" = negative obligation |
| `actor_role` | Provider / Deployer / both | Determined by which article applies (Provider duties: Art. 8–22, Deployer duties: Art. 26–27, joint duties: Art. 4, 50) |
| `risk_category` | Which risk tier | Determined by where the obligation appears in the regulation |
| `nist_ai_rmf` | NIST AI RMF function and subcategory | Must reference at least one of GOVERN/MAP/MEASURE/MANAGE with subcategory number |
| `iso_42001` | ISO 42001 clause and/or Annex A control | Must reference clause number or "A.{N}" |
| `owasp_llm_top10` | OWASP LLM Top 10 (2025) risk addressed | Format: "LLMNN:Name". Use "—" if no LLM-specific applicability |
| `mitre_atlas` | ATLAS technique mitigated | Format: "AML.TNNNN". Use "—" if no adversarial-ML applicability |
| `gdpr_article` | GDPR overlap | Use "—" if no GDPR overlap |
| `dora_article` | DORA overlap | Use "—" if no DORA overlap |
| `implementation_evidence` | Path to the artifact in the project that implements this control | Must point to a file/directory under `project/` |
| `maturity_level` | Implementation maturity (1–3) | 1 = Documented (specification exists in writing); 2 = Implemented (working code/process exists); 3 = Tested (automated tests verify the implementation). Collapsed from a 5-level CMMI scale in v0.1.3 to match what this project can honestly demonstrate. |
| `status` | Implementation status in this project | One of: `planned`, `documented`, `implemented`, `tested`. Distinct from maturity_level: status describes *this project's current state*; maturity_level describes the *target maturity* for a well-implemented control regardless of project state. |
| `phase` | Build phase in the roadmap | When this control is implemented in the demo project |

### 5.1 Mapping rigor

Cross-framework mappings (`nist_ai_rmf`, `iso_42001`, `owasp_llm_top10`, `mitre_atlas`, `gdpr_article`, `dora_article`) follow this rule:

> **A mapping is included only if the framework's control directly addresses the same security or compliance objective. Loose thematic connections are not mappings.**

Three examples to illustrate the difference:

- **Direct mapping (included):** AISEC-CS-005 (Prompt Injection Defense) → OWASP LLM01 (Prompt Injection). Same threat, same mitigation.
- **Direct mapping (included):** AISEC-DG-003 (Bias Detection and Mitigation) → NIST AI RMF MEASURE 2.7 (which explicitly covers bias measurement). Same objective.
- **Loose connection (excluded):** AISEC-RM-002 (Risk Management System) → OWASP LLM01 (Prompt Injection). Risk management *includes* defending against prompt injection, but the OWASP item is a specific threat, not a risk management practice. Mapping these would dilute both frameworks.

When in doubt, the catalog **errs toward fewer mappings**. A mapping should be the answer to "if I implement this control, am I also satisfying that framework requirement?" — not "is this control related to that topic?"

---

## 6. How the count was determined

The total of **79 controls** as of catalog version 0.1.1 is the natural result of applying §3 (granularity rule) and §4 (domain structure) to the in-scope obligations defined in §2.

### 6.1 Derivation walk-through

To make this concrete, here is how the count for each domain was derived:

| Domain | Count | Derivation |
|--------|-------|-----------|
| **RM** | 6 | Art. 6 classification (1) + Art. 9 risk management system (1) + Art. 9(2) sub-obligations split by failure mode: identification, evaluation, mitigation, testing (4) |
| **DG** | 6 | Art. 10(2) governance framework (1) + Art. 10(3) data quality (1) + Art. 10(2)(f)(g) bias (1) + Art. 10(2)(b)(c) lineage (1) + Art. 10(2)(e) statistical properties (1) + Art. 10(5) PII safeguards (1) |
| **TD** | 5 | Five sections of Annex IV: §1 system description, §2 design specs, §3 monitoring, §4 testing, §6 changes log. Annex IV §5 (instructions for use) lives under TR-001 to avoid duplication. |
| **LG** | 5 | Art. 12(1) capability (1) + Art. 12(2)(a)(b)(c)(d) split per log-content requirement (3) + Art. 19/26(6) retention (1) |
| **TR** | 5 | Art. 13 instructions for use (1) + Art. 50(1) AI disclosure (1) + Art. 50(2) content marking (1) + Art. 50(4) deep fakes (1) + Art. 50(3) emotion/biometric (1) |
| **HO** | 5 | Art. 14(1)(2) design for oversight (1) + Art. 14(4)(a)(b) understanding capabilities (1) + Art. 14(4)(d)(e) override/intervention (1) + Art. 14(4)(b) automation bias (1) + Art. 26(2) deployer duty (1) |
| **AC** | 2 | Art. 15(1) metrics declaration (1) + Art. 15(1)+9(6) validation (1) |
| **RB** | 3 | Art. 15(3) design for robustness (1) + Art. 15(3) fault tolerance (1) + Art. 15(4) adversarial testing (1) |
| **CS** | 6 | Art. 15(5) general (1) + Art. 15(5)(a) data poisoning (1) + Art. 15(5)(b) adversarial inputs (1) + Art. 15(5)(c) confidentiality attacks (1) + prompt injection (specific instance) (1) + supply chain (1) |
| **PM** | 4 | Art. 72(1)(2) monitoring system (1) + Art. 72(3) drift detection (1) + Art. 73 incident reporting (1) + Art. 20 corrective action (1) |
| **CA** | 5 | Art. 43 procedure (1) + Art. 47 DoC (1) + Art. 48 CE marking (1) + Art. 49 registration (1) + Art. 17 QMS (1) |
| **DP** | 5 | Art. 27 FRIA (1) + Art. 26(1) instructions compliance (1) + Art. 26(4) input data (1) + Art. 26(5) monitoring (1) + Art. 26(6) record keeping (1) |
| **GP** | 5 | Art. 53(1)(a) docs (1) + Art. 53(1)(c)(d) copyright (1) + Art. 53(1)(b) downstream (1) + Art. 55(1) systemic safety framework (1) + Art. 55(1)(d) systemic cybersecurity (1) |
| **PH** | 8 | One per prohibition in Art. 5(1)(a) through (h) (8) — Art. 5(1)(g) biometric categorization is folded into the broader §5(1) ban set; PH-008 is the Omnibus-added nudifier prohibition (1) |
| **GV** | 9 | AI literacy (1) + authorized rep (1) + authority cooperation (1) + DORA alignment (3) + GDPR alignment (2) + unified incident management (1) |
| **Total** | **79** | |

### 6.2 What 79 means and does not mean

**What 79 means:** This is what you get when you apply the granularity rule of §3 to the in-scope articles of §2, grouped by the 15 domains of §4. If the rules are changed, the count changes — and that's the point.

**What 79 does not mean:**

- It is **not** a target. There was no goal of "around 80."
- It is **not** complete. Future versions will add controls as the AI Act is amended, as harmonized standards are published, and as new cross-framework mappings are added.
- It is **not** the same as "X compliance requirements" — one regulatory obligation can produce zero, one, or multiple controls depending on how it cuts.
- It is **not** comparable across catalogs. Other AI Act control catalogs may have 30 or 200 controls; both can be correct under different granularity rules.

### 6.3 Known omissions

The following obligations are **acknowledged but not yet implemented as controls** in the current version. They will be added in future versions:

| Obligation | Why not yet | Planned addition |
|-----------|------------|-------------------|
| Art. 25 substantial modification reclassification | Borderline: this is a *triggering condition* for becoming a Provider, not a standalone control. Documented in the scope chapter instead. | v0.2 — as RM-007 |
| Art. 5(1)(g) biometric categorization to infer sensitive attributes | Currently folded into the broader prohibition set; not assigned its own PH-* ID | v0.2 |
| Art. 65 EU AI Board cooperation | Provider-level cooperation is covered by GV-003; Board-specific duties are arguably out of scope | Under review |
| Art. 86 right to explanation of individual decision-making | New right granted to affected persons; control is "respond to explanation requests" | v0.2 — as HO-006 |
| Art. 11 / Annex IV §5 (instructions for use) as a TD control | Currently exists as TR-001; could be duplicated under TD for completeness | Under review |

This list will grow as the catalog matures. The point is that **omissions are tracked explicitly**, not silently absent.

---

## 7. Versioning and change management

The catalog is versioned at the same cadence as the project (semver). When the EU AI Act, the AI Omnibus, or supporting standards are amended:

1. **The change is recorded in the catalog changelog** (`docs/03-controls/changelog.md` — to be created).
2. **Affected controls are amended in `controls.csv`** with a comment in the description indicating the source of the change.
3. **The methodology document is updated** if the change affects the granularity rule, scope, or domain structure.
4. **A new version tag is created** (e.g., `controls-v0.2`) so previous compliance reports remain reproducible.

### 7.1 Already-recorded amendments

| Version | Date | Source | Change |
|---------|------|--------|--------|
| 0.1.0 | 13 May 2026 | Initial drafting from Regulation 2024/1689 | 78 controls created |
| 0.1.1 | 14 May 2026 | AI Omnibus political agreement (7 May 2026) | Added AISEC-PH-008 (nudifier prohibition). Timelines updated in documentation but no control content changed. |
| 0.1.2 | 15 May 2026 | Methodology documentation | Authored this methodology document. Documented scope decisions, granularity rule, domain rationale, per-domain control derivation. No catalog content changed. |
| 0.1.3 | 15 May 2026 | Phase 1.5 defensibility hardening + OWASP correction | Corrected OWASP LLM Top 10 mappings to the 2025 edition (12 controls updated; previous values were a mix of 2023 names with self-contradictory IDs). Collapsed maturity_level from 5-level CMMI scale to 3 levels (Documented / Implemented / Tested). Added `status` column tracking implementation progress within this project. Added threat model justification (`docs/02-architecture/threat-model.md`). Added timeline as single source of truth (`data/timeline.yaml`). |

When the AI Omnibus is formally adopted (expected July 2026), the catalog will be re-versioned to 0.2.0 to reflect the formal text rather than the political agreement.

---

## 8. How to critique or extend the catalog

This methodology exists to make the catalog **falsifiable**. If you disagree with the catalog, the productive form of disagreement is one of:

1. **"This control should be split."** — Argue that the obligation has multiple independent failure modes (Test 3) or distinct verification artifacts (Test 2) that justify splitting.

2. **"These controls should be merged."** — Argue that the obligations always succeed or fail together, share the same evidence, and cannot be independently implemented.

3. **"This obligation is missing."** — Point to a specific article or paragraph in the AI Act, the Omnibus, or a harmonized standard that is in-scope per §2 but has no corresponding control.

4. **"This mapping is wrong."** — Argue that the cross-framework reference does not address the same objective per §5.1.

5. **"The scope is wrong."** — Argue that something currently excluded in §2.2 should be in scope (or vice versa).

Disagreements about "the count should be different" without one of the above forms are not productive — the count is downstream of the rules.

---

## 9. Limitations

This methodology has known limitations that should be transparent to anyone using the catalog:

1. **Provider-Deployer biased.** The catalog deliberately covers only two actor roles. Real-world AI value chains have more actors (importers, distributors, product manufacturers integrating AI). Future versions may address this; current version does not.

2. **EU-centric.** The catalog covers EU obligations only. It does not address overlapping requirements from the US (EO 14110, state laws), UK, Canada, or APAC. Where global organizations need a multi-jurisdiction catalog, this is a starting point, not a complete solution.

3. **Static at a point in time.** The catalog reflects the regulation as of 15 May 2026 + the May 2026 Omnibus political agreement. Harmonized standards (CEN-CENELEC JTC 21) are not yet published; when they are, additional controls will likely be derived from them.

4. **Mapping recall vs. precision tradeoff.** Per §5.1, the catalog prioritizes precision (only direct mappings) over recall (catching every related framework reference). This makes the catalog easier to defend but means some legitimate cross-framework relationships are absent.

5. **No notified-body perspective.** The catalog is written from the regulated entity's perspective (what to build), not from the regulator's perspective (what to check). A complete compliance program would need both.

6. **Maturity levels are aspirational.** The `maturity_level` column reflects the *target* maturity for a well-implemented control; it is not a measurement of any specific organization's current state.

---

## 10. Citing this methodology

If you reference or extend this catalog in your own work, please cite:

> Manzambi, J. (2026). *EU AI Act Compliance Controls Catalog: Methodology v0.1.3*. eu-ai-act-blueprint. https://github.com/josephManzambi/eu-ai-act-blueprint

The catalog itself (`controls.csv`) is available under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) to encourage reuse, translation, and adaptation.

---

*Related: [Threat Model →](../02-architecture/threat-model.md)*
