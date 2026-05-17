# 🏗️ EU AI Act Blueprint

**A working technical blueprint for EU AI Act compliance — for Providers and Deployers.**

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)
[![EU AI Act](https://img.shields.io/badge/EU_AI_Act-2024%2F1689-003399.svg)](https://eur-lex.europa.eu/eli/reg/2024/1689)
[![NIST AI RMF](https://img.shields.io/badge/NIST-AI_RMF_1.0-00539B.svg)](https://www.nist.gov/artificial-intelligence/executive-order-safe-secure-and-trustworthy-artificial-intelligence)
[![Python](https://img.shields.io/badge/Python-3.11+-3776AB.svg)](https://python.org)

---

## What this is

Most EU AI Act resources tell you *what* the law says. This project shows you *what to build*.

It is a **reference implementation** of the technical controls required to comply with the EU AI Act (Regulation 2024/1689), demonstrated through a concrete high-risk AI use case: a **CV-screening system** for employment (Annex III, area 4).

The project covers both **Provider** obligations (the company building the AI) and **Deployer** obligations (the company using it) — because in practice, most enterprises are both.

### Three deliverables, one coherent system

| # | Deliverable | What it does | Where it lives |
|---|-------------|-------------|----------------|
| 1 | **Technical Overview** | Plain-language walkthrough of the EU AI Act from a security architect's perspective. Scope, risk classification, actor roles, requirements, timeline, penalties. | [Live tracker →](https://manzambi.com/tracker) + chapters in [`docs/01-overview/`](docs/01-overview/) |
| 2 | **Compliance Demo** | A fully working CV-screening API with every Article 8–15 control implemented: risk management, data governance, bias detection, logging, human oversight, adversarial testing, post-market monitoring. Runs with `docker compose up`. | [`project/`](project/) |
| 3 | **Controls Mapping** | 79 technical controls, each mapped to EU AI Act articles, NIST AI RMF, ISO/IEC 42001, OWASP LLM Top 10, MITRE ATLAS, GDPR, and DORA. Machine-readable CSV + searchable web table. | [`data/controls.csv`](data/controls.csv) |

---

## Why this exists

The EU AI Act's enforcement is rolling out in phases. Transparency obligations take effect on **2 August 2026**, and — following the AI Omnibus political agreement of May 2026 — standalone high-risk AI system requirements (Annex III) apply from **2 December 2027**. Companies building or deploying AI in Europe — or selling to European customers — need to translate 180+ pages of regulation into engineering decisions.

This project is that translation.

It was built by [Joseph Manzambi](https://manzambi.com), an AI security architect, as a practical reference for teams trying to answer: *"What do we actually need to build?"*

> **Before you rely on anything here, read [WHAT_THIS_IS_NOT.md](WHAT_THIS_IS_NOT.md).** Honest boundaries about what this project is and is not — including: not legal advice, not a substitute for conformity assessment, not maintained by a team.

---

## Quick start

### Browse the controls catalog

```bash
# View all controls
cat data/controls.csv | head -5

# Filter by actor role
grep "Deployer" data/controls.csv

# Filter by framework mapping
grep "LLM01:Prompt Injection" data/controls.csv
```

### Run the compliance demo

```bash
git clone https://github.com/josephManzambi/eu-ai-act-blueprint.git
cd eu-ai-act-blueprint

# Start the full stack (API + DB + monitoring + oversight console)
docker compose up -d

# Run the compliance test suite
pytest project/tests/ -v --tb=short

# Generate a compliance report
python scripts/generate_compliance_report.py
```

### Read the technical overview

Visit the [live EU AI Act Tracker](https://manzambi.com/tracker) for the enforcement timeline, or browse the technical chapters locally:

```bash
cd docs/
# Each chapter is a standalone markdown file
ls 01-overview/
```

---

## Project structure

```
eu-ai-act-blueprint/
├── README.md
├── STATUS.md                          # ← What works today, what's next
├── CHANGELOG.md                       # ← Version history
├── WHAT_THIS_IS_NOT.md                # ← Honest boundaries
├── LICENSING.md                       # ← License-per-directory map
├── LICENSE                            # Apache 2.0
├── docs/                              # Documentation site source
│   ├── 01-overview/                   # Deliverable 1: Technical overview
│   │   ├── scope-and-jurisdiction.md  # Art. 2 — Extraterritorial reach
│   │   ├── risk-pyramid.md            # Art. 5–6 — Risk classification
│   │   ├── actor-roles.md             # Art. 3 — Provider / Deployer / Importer
│   │   ├── high-risk-requirements.md  # Art. 8–15 — The 7 core requirements
│   │   ├── gpai-obligations.md        # Art. 51–56 — GPAI models
│   │   ├── timeline-and-penalties.md  # Phased enforcement dates + fines
│   │   └── ai-omnibus-2026.md         # May 2026 simplification package
│   ├── 02-architecture/               # Reference architecture
│   │   ├── threat-model.md            # ← STRIDE + ATLAS + LINDDUN — the security justification
│   │   ├── reference-architecture.md  # C4 diagrams of the compliance stack
│   │   └── provider-vs-deployer.md    # Responsibility matrix
│   ├── 03-controls/                   # Deliverable 3: Controls mapping
│   │   ├── methodology.md             # ← How the catalog was derived
│   │   ├── catalog.md                 # Auto-rendered from controls.csv
│   │   └── mappings/                  # Per-framework deep dives
│   │       ├── nist-ai-rmf.md
│   │       ├── iso-42001.md
│   │       ├── owasp-llm-top10.md
│   │       ├── mitre-atlas.md
│   │       ├── gdpr.md
│   │       └── dora.md
│   └── 04-project/                    # Code walkthrough
│       └── architecture.md
├── data/                              # Machine-readable data
│   ├── controls.csv                   # Controls catalog (source of truth)
│   ├── controls-schema.json           # JSON Schema for controls
│   └── timeline.yaml                  # ← All EU AI Act dates (single source)
├── project/                           # Deliverable 2: Working demo
│   ├── use_case/                      # CV-screening scenario
│   ├── risk_management/               # Art. 9 — Risk management system
│   ├── data_governance/               # Art. 10 — Data quality & bias
│   ├── documentation/                 # Art. 11 — Model cards & datasheets
│   ├── logging/                       # Art. 12 — Structured event logging
│   ├── transparency/                  # Art. 13 + 50 — Disclosures
│   ├── human_oversight/               # Art. 14 — Override & intervention
│   ├── robustness_security/           # Art. 15 — Adversarial defense
│   ├── post_market_monitoring/        # Art. 72 — Drift & incidents
│   ├── conformity_assessment/         # Art. 43, 47 — DoC & CE
│   └── tests/                         # Compliance test suite
├── scripts/                           # Build & render utilities
├── site/                              # Astro site source
└── .github/workflows/                 # CI: compliance tests on every PR
```

---

## Controls catalog

The controls catalog (`data/controls.csv`) is the **single source of truth** for the entire project. Every document, every code module, and every test references it.

The catalog is derived from the EU AI Act using an explicit, documented methodology. See **[`docs/03-controls/methodology.md`](docs/03-controls/methodology.md)** for the scope decisions, granularity rules, and per-domain derivation that produced the 79 controls.

### Coverage summary

| Domain | Controls | AI Act Articles |
|--------|----------|----------------|
| Risk Management (RM) | 6 | Art. 6, 9 |
| Data Governance (DG) | 6 | Art. 10 |
| Technical Documentation (TD) | 5 | Art. 11, Annex IV |
| Logging (LG) | 5 | Art. 12, 19 |
| Transparency (TR) | 5 | Art. 13, 50 |
| Human Oversight (HO) | 5 | Art. 14, 26 |
| Accuracy (AC) | 2 | Art. 15(1) |
| Robustness (RB) | 3 | Art. 15(3)(4) |
| Cybersecurity (CS) | 6 | Art. 15(5) |
| Post-Market Monitoring (PM) | 4 | Art. 20, 72, 73 |
| Conformity Assessment (CA) | 5 | Art. 17, 43, 47, 48, 49 |
| Deployer Obligations (DP) | 5 | Art. 26, 27 |
| GPAI (GP) | 5 | Art. 53, 55 |
| Prohibited Practices (PH) | 8 | Art. 5 |
| Governance (GV) | 9 | Art. 4, 21, 22 + GDPR/DORA |
| **Total** | **79** | |

### Framework mappings

Each control is cross-referenced with:

- **NIST AI RMF 1.0** — GOVERN / MAP / MEASURE / MANAGE functions and subcategories
- **ISO/IEC 42001:2023** — AI Management System clauses and Annex A controls
- **OWASP Top 10 for LLM Applications (2025)** — LLM-specific risks addressed
- **MITRE ATLAS** — Adversarial ML techniques mitigated
- **GDPR (2016/679)** — Overlapping data protection requirements
- **DORA (2022/2554)** — Digital operational resilience requirements for financial services

---

## Implementation timeline

The EU AI Act's obligations apply in phases. The **AI Omnibus** political agreement of 7 May 2026 significantly extended the deadlines for high-risk AI systems:

| Date | What applies | Status |
|------|-------------|--------|
| 2 Feb 2025 | Prohibited practices (Art. 5) + AI literacy (Art. 4) | ✅ In force |
| 2 Aug 2025 | GPAI obligations (Art. 51–56) + Governance (Art. 64–70) | ✅ In force |
| 2 Aug 2026 | Transparency obligations (Art. 50) — chatbot disclosure, emotion recognition, biometric categorization. GPAI enforcement powers. | ⏳ Upcoming |
| 2 Dec 2026 | Watermarking/content labeling for AI systems already on market (3-month grace period). New prohibition on "nudifier" applications (non-consensual intimate imagery / CSAM). | ⏳ Upcoming |
| 2 Aug 2027 | Regulatory sandboxes — deadline for national competent authorities to establish sandboxes. | 🔜 Upcoming |
| **2 Dec 2027** | **Standalone high-risk AI systems (Annex III) — full Art. 8–15 requirements, conformity assessment, enforcement.** This is the deadline for our CV-screening demo (area 4: Employment). | 🔜 Pending adoption |
| 2 Aug 2028 | High-risk AI as products/safety components under EU product safety rules (Annex I) — medical devices, toys, vehicles, etc. Machinery Regulation AI carved out entirely. | 🔜 Pending adoption |
| 31 Dec 2030 | Large-scale IT systems (Annex X) | 🔜 Upcoming |

> **Note:** The AI Omnibus still requires formal adoption by the European Parliament and Council (expected by July 2026). Other key Omnibus changes: industrial AI under the Machinery Regulation is carved out from the AI Act; the "safety component" definition is narrowed; SME simplifications are extended to mid-caps (≤750 employees / €150M revenue); and special category data may be used for bias detection/mitigation where strictly necessary. This project tracks updates as they are published in the Official Journal.

---

## Penalties

Non-compliance carries significant financial consequences:

- **Prohibited practices:** up to €35M or 7% of global annual turnover
- **High-risk obligations:** up to €15M or 3% of global annual turnover
- **Incorrect information to authorities:** up to €7.5M or 1% of global annual turnover

For SMEs and startups, the lower of the two amounts applies.

---

## Who should use this

- **AI/ML Engineers** building systems that may be classified as high-risk
- **Security Architects** designing compliance controls into AI systems
- **CISOs and DPOs** assessing AI-related regulatory risk
- **Compliance Teams** bridging the gap between legal requirements and technical implementation
- **CTOs and Engineering Managers** planning AI governance roadmaps

---

## Languages

This project is available in:

- 🇬🇧 **English** (primary)
- 🇫🇷 **Français** (coming in Phase 6)

---

## Contributing

Contributions are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

Priority areas:
- Additional framework mappings (SOC 2, CSA CCM, BSI C5)
- Translations (Spanish, German, Italian)
- Alternative use case implementations (credit scoring, medical devices)
- Harmonized standards references (CEN-CENELEC JTC 21 drafts)

---

## License

This project is licensed under the [Apache License 2.0](LICENSE).

The technical overview content in `docs/` and `site/` is additionally available under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) for easier reuse and translation.

---

## Author

**[Joseph Manzambi](https://manzambi.com)** — AI Security Architect

*From cloud to AI, I build the defensive layer between innovation and exploitation.*

- 🌐 [manzambi.com](https://manzambi.com)
- 📧 [Contact](https://manzambi.com/contact)
- 🐙 [GitHub](https://github.com/josephManzambi)

---

## Acknowledgments

This project references and builds upon:

- [EU AI Act (Regulation 2024/1689)](https://eur-lex.europa.eu/eli/reg/2024/1689)
- [EU AI Act Explorer](https://artificialintelligenceact.eu/) by the Future of Life Institute
- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework) (AI 100-1)
- [ISO/IEC 42001:2023](https://www.iso.org/standard/81230.html) — AI Management System
- [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
- [MITRE ATLAS](https://atlas.mitre.org/)
- [GPAI Code of Practice](https://digital-strategy.ec.europa.eu/en/policies/guidelines-gpai-providers)
