# GitHub Issues — Paste-ready

These are draft issues to populate the eu-ai-act-blueprint repo's Issues tab. Each one has a title, suggested labels, and a body. Paste them into GitHub one at a time (or use the GitHub CLI / API for bulk creation).

The grouping below reflects the phase structure from the original roadmap, but each issue stands alone. Close them in any order that makes sense for your bandwidth.

---

## Foundation cleanup (Phase 1 leftovers)

### Issue 1
**Title:** Add LICENSE file (Apache 2.0)
**Labels:** `chore`, `phase-1`, `good-first-issue`
**Body:**

The repo references Apache License 2.0 throughout (README, LICENSING.md), but the canonical `LICENSE` file is not yet committed. Add the full Apache 2.0 license text at the repo root. Source: https://www.apache.org/licenses/LICENSE-2.0.txt

### Issue 2
**Title:** Add LICENSE-docs.txt (CC BY-SA 4.0)
**Labels:** `chore`, `phase-1`
**Body:**

The prose documentation is licensed under CC BY-SA 4.0 per `LICENSING.md`, but the license text file is not yet committed. Add `LICENSE-docs.txt` containing the full CC BY-SA 4.0 legal text. Source: https://creativecommons.org/licenses/by-sa/4.0/legalcode.txt

### Issue 3
**Title:** Add CONTRIBUTING.md
**Labels:** `chore`, `phase-1`
**Body:**

Contributors need guidance on how to propose changes. CONTRIBUTING.md should cover:

- How to propose a new control (link to methodology.md §8)
- How to propose a new framework mapping
- Translation contribution guidelines (when French translations begin)
- PR checklist (regenerate any derived files, update CHANGELOG, etc.)
- Code of conduct reference

Keep it brief — under 200 lines.

### Issue 4
**Title:** Write Chapter 3: Actor Roles (`docs/01-overview/actor-roles.md`)
**Labels:** `documentation`, `phase-1`
**Body:**

Cover Article 3 actor definitions in depth:

- Provider (Art. 3(3)) — including the substantial-modification reclassification under Art. 25
- Deployer (Art. 3(4))
- Importer (Art. 3(6)) — out of catalog scope but explained for completeness
- Distributor (Art. 3(7))
- Authorized representative (Art. 3(5), Art. 22)
- Product manufacturer (Art. 3(8))

For each role: definition, key obligations, relationship to other roles, and worked examples mapping to the CV-screening use case.

### Issue 5
**Title:** Write Chapter 4: High-Risk Requirements (`docs/01-overview/high-risk-requirements.md`)
**Labels:** `documentation`, `phase-1`
**Body:**

Walk through Articles 8-15 one by one:

- Art. 8: Compliance with requirements
- Art. 9: Risk management system
- Art. 10: Data and data governance
- Art. 11: Technical documentation
- Art. 12: Record-keeping (logs)
- Art. 13: Transparency and information for deployers
- Art. 14: Human oversight
- Art. 15: Accuracy, robustness, cybersecurity

For each: what the article requires, which AISEC-* controls implement it, and how the CV-screening demo will demonstrate compliance.

### Issue 6
**Title:** Write Chapter 5: GPAI Obligations (`docs/01-overview/gpai-obligations.md`)
**Labels:** `documentation`, `phase-1`
**Body:**

Articles 51-56 — General-Purpose AI model obligations.

- Definition of GPAI (Art. 3(63))
- Threshold for systemic-risk classification (Art. 51)
- Provider obligations (Art. 53): technical documentation, copyright policy, downstream provider information, training data summary
- Systemic-risk provider obligations (Art. 55): safety frameworks, evaluations, incident reporting, cybersecurity
- GPAI Code of Practice and its role
- How GPAI obligations interact with high-risk system obligations when the GPAI model is a component of a high-risk system (the LLM summarizer in our demo)

### Issue 7
**Title:** Write Chapter 6: Timeline and Penalties (`docs/01-overview/timeline-and-penalties.md`)
**Labels:** `documentation`, `phase-1`
**Body:**

Render the contents of `data/timeline.yaml` as a long-form chapter. Include:

- All milestones with full descriptions and AI Omnibus context
- Penalty regime (Art. 99): tier-by-tier with examples of who pays what
- SME mitigation (Art. 99(6))
- Enforcement actors: AI Office, national competent authorities, market surveillance authorities

### Issue 8
**Title:** Write Chapter 7: AI Omnibus 2026 Deep-Dive (`docs/01-overview/ai-omnibus-2026.md`)
**Labels:** `documentation`, `phase-1`
**Body:**

The AI Omnibus is significant enough to warrant its own chapter. Cover:

- Background: why simplification, what triggered the package
- Political agreement of 7 May 2026 — all changes
- Status of formal adoption
- Impact on Provider/Deployer planning
- What did *not* change (clarifies persistent obligations)

Update this chapter when formal adoption occurs.

### Issue 9
**Title:** Define risk register YAML schema (`project/risk_management/risk_register.yaml`)
**Labels:** `code`, `phase-1`
**Body:**

Specify the schema for the Article 9 risk register. Should cover:

- Risk ID, description, source article reference
- Likelihood, impact, residual risk
- Mitigation control reference (links to AISEC-* IDs)
- Owner, review date, status

This is the data structure underlying control AISEC-RM-002.

### Issue 10
**Title:** Implement prohibited practice checks (`project/risk_management/prohibited_checks.py`)
**Labels:** `code`, `phase-1`
**Body:**

Implements controls AISEC-PH-001 through AISEC-PH-008. A simple Python module that takes a system specification (intended purpose, deployment context, capabilities) and returns whether the system falls into any Art. 5 prohibition. Output: pass/fail per prohibition with explanation.

### Issue 11
**Title:** Deployer FRIA template (`project/risk_management/deployer_fria.md`)
**Labels:** `documentation`, `phase-1`
**Body:**

Article 27 Fundamental Rights Impact Assessment template. Required for deployers using high-risk AI in specific areas (public services, creditworthiness, insurance, law enforcement, migration, justice, employment — our use case applies). Should be a fillable template with placeholders + worked example for the NordBank-deploying-CV-screening scenario.

### Issue 12
**Title:** DORA alignment guide (`project/risk_management/dora_alignment.md`)
**Labels:** `documentation`, `phase-1`
**Body:**

For financial sector deployers, AI Act obligations stack on top of DORA. Document:

- ICT risk management overlap (DORA Art. 5-15 ↔ AI Act Art. 9)
- Third-party AI vendor due diligence (DORA Art. 28-30)
- Threat-led penetration testing (DORA Art. 24-27) applied to AI systems
- Incident reporting alignment (DORA Art. 19 ↔ AI Act Art. 73)

References controls AISEC-GV-004 through AISEC-GV-006.

### Issue 13
**Title:** GDPR DPIA for AI template (`project/risk_management/gdpr_dpia_ai.md`)
**Labels:** `documentation`, `phase-1`
**Body:**

GDPR Article 35 Data Protection Impact Assessment, extended with AI-specific risk considerations. Should integrate with the AISEC-DG-* (data governance) and AISEC-DP-001 (deployer FRIA) controls so that organizations can run a single integrated assessment instead of three separate processes.

---

## Phase 2 — Data Governance (next deliverable)

### Issue 14
**Title:** Generate synthetic CV dataset with documented bias injection
**Labels:** `code`, `phase-2`
**Body:**

The demo needs a CV dataset to run against. Real CVs trigger GDPR issues; synthetic data avoids them while creating a stronger bias-detection demonstration.

Implementation:

- Generate ~1000 synthetic CVs with realistic structure (experience, education, skills, free-text descriptions)
- Inject controlled bias along documented protected attributes:
  - Gender (via name distribution)
  - Age (via graduation year distribution)
  - Ethnicity proxy (via name origin distribution)
- Bias rates should be configurable parameters
- Output: dataset + `dataset_card.md` (Annex IV §2 compliant) + bias-injection log

Document this as a feature, not a workaround. The bias-detection demo (Issue 16) will then show the gap between injected-vs-detected bias.

### Issue 15
**Title:** Data governance framework document (`project/data_governance/governance_framework.md`)
**Labels:** `documentation`, `phase-2`
**Body:**

The narrative document covering Article 10(2) data governance obligations:

- Data collection and selection rationale
- Data preparation operations (annotation, labelling, cleaning)
- Identification of relevant data gaps
- Examination for biases
- Measures to detect, prevent, and mitigate biases

Implements control AISEC-DG-001.

### Issue 16
**Title:** Implement bias detection module (`project/data_governance/bias_detection.py`)
**Labels:** `code`, `phase-2`
**Body:**

Using Fairlearn:

- Compute demographic parity, equal opportunity, and equalized odds across protected attribute groups
- Compare detected bias against the injected bias rates from Issue 14
- Generate bias report (PDF or HTML) with metrics, visualizations, and remediation recommendations
- Implements controls AISEC-DG-003 and AISEC-CS-002

### Issue 17
**Title:** Data quality pipeline (`project/data_governance/data_quality_pipeline.py`)
**Labels:** `code`, `phase-2`
**Body:**

Implements AISEC-DG-002 (training data quality and relevance):

- Schema validation
- Missing value handling
- Outlier detection
- Duplicate detection
- Statistical property reporting (distribution, coverage, gaps)

Output feeds into AISEC-DG-005 (statistical properties documentation).

### Issue 18
**Title:** Data lineage tracker (`project/data_governance/data_lineage.json` + code)
**Labels:** `code`, `phase-2`
**Body:**

Implements AISEC-DG-004. Tracks:

- Data origin (synthetic generation parameters)
- Each transformation applied
- Hash of dataset at each stage
- Links to the code/script that produced each transformation

Format: JSON lineage graph that can be visualized and traversed.

### Issue 19
**Title:** PII safeguards module (`project/data_governance/pii_safeguards.py`)
**Labels:** `code`, `phase-2`
**Body:**

Implements AISEC-DG-006 and supports GDPR compliance. Functions for:

- PII detection in free-text CV content (using regex + a small NER model)
- Pseudonymization (replacing names with stable IDs)
- Redaction (for LLM submissions — see also Issue 27)
- Audit logging of PII handling decisions

### Issue 20
**Title:** Deployer data validation module (`project/data_governance/deployer_data_validation.py`)
**Labels:** `code`, `phase-2`
**Body:**

Implements AISEC-DP-003 — the deployer's obligation to ensure input data is relevant and representative. A validation layer the Deployer (NordBank in our scenario) runs *before* submitting data to the AI system, checking distribution match against the Provider's documented intended use case.

---

## Phase 3 — Documentation, Logging, Transparency

### Issue 21
**Title:** Model card generator (`project/documentation/model_card_generator.py`)
**Labels:** `code`, `phase-3`
**Body:**

Generates Annex IV-compliant technical documentation from a YAML model spec. Implements AISEC-TD-001 through AISEC-TD-005. Output should be both human-readable (Markdown) and machine-readable (JSON).

### Issue 22
**Title:** Structured event logger (`project/logging/structured_logger.py`)
**Labels:** `code`, `phase-3`
**Body:**

Article 12 compliant logging. OpenTelemetry-based. Must capture:

- Period of use (start/end timestamps)
- Reference database used
- Input data identification
- Human verifier identity (for AISEC-LG-004)

Logs must be tamper-evident (hash chain or append-only storage). Implements AISEC-LG-001 through AISEC-LG-004.

### Issue 23
**Title:** Log retention manager (`project/logging/log_retention.py`)
**Labels:** `code`, `phase-3`
**Body:**

Implements AISEC-LG-005 / AISEC-DP-005. Configurable retention windows. Default: 6 months for AI Act compliance, longer if GDPR or sector-specific rules apply. Automated purging with audit trail.

### Issue 24
**Title:** Instructions for use document template (`project/transparency/instructions_for_use.md`)
**Labels:** `documentation`, `phase-3`
**Body:**

Article 13 + Annex IV §5 compliant instructions for use. Worked example for the CV-screening system covering: intended purpose, accuracy levels, known limitations, human oversight requirements, expected lifetime, maintenance. Implements AISEC-TR-001.

### Issue 25
**Title:** Transparency modules: AI disclosure, content marking, deep fake notice
**Labels:** `code`, `phase-3`
**Body:**

Three small modules implementing AISEC-TR-002, AISEC-TR-003, and AISEC-TR-004. Each demonstrates the Art. 50 transparency obligations in code form.

### Issue 26
**Title:** GPAI documentation templates
**Labels:** `documentation`, `phase-3`
**Body:**

Three templates implementing GPAI obligations:

- GPAI model card (AISEC-GP-001) — Annex XI compliant
- Training data summary (AISEC-GP-002) — using the AI Office template
- Downstream provider documentation (AISEC-GP-003)

These apply when *we* are the GPAI provider. For our demo, we are a *deployer* of someone else's GPAI (the LLM summarizer) — but providing these templates supports users who are building GPAI models themselves.

---

## Phase 4 — Core Engineering

### Issue 27
**Title:** Build the CV-screening API
**Labels:** `code`, `phase-4`, `epic`
**Body:**

FastAPI service. Endpoints:

- `POST /candidates` — submit a CV (candidate-facing, unauthenticated, rate-limited)
- `POST /score` — rank candidates against a job description (recruiter-facing, authenticated)
- `GET /candidates/{id}/explanation` — retrieve ranking explanation
- `POST /candidates/{id}/override` — recruiter override (writes to audit log)

Uses sentence-transformers for the matching model, calls an LLM for résumé summarization. All trust boundaries from the threat model enforced. Implements the core implementation evidence for ~30 controls.

### Issue 28
**Title:** Human oversight console
**Labels:** `code`, `phase-4`, `epic`
**Body:**

Streamlit app implementing Article 14 oversight:

- Recruiter reviews each candidate's score and explanation before action
- Override workflow with reason capture (writes to audit log per AISEC-LG-004)
- Visual indication of low-confidence rankings
- "Stop" button to disable the AI scoring entirely (AISEC-HO-003)

Implements AISEC-HO-001 through AISEC-HO-005.

### Issue 29
**Title:** Adversarial robustness test suite
**Labels:** `code`, `phase-4`
**Body:**

Using ART (Adversarial Robustness Toolbox):

- Evasion attacks against the sentence-transformer model
- Test the system against the ML4-ML15 threats from the threat model
- Generate robustness report mapped to AISEC-RB-001 through AISEC-RB-003

### Issue 30
**Title:** Prompt injection defense harness
**Labels:** `code`, `phase-4`
**Body:**

Test the LLM summarizer against direct and indirect prompt injection attacks. Use Garak or build a custom harness. Cover threats ML13, ML14, ML15 from the threat model. Implements AISEC-CS-005.

### Issue 31
**Title:** Docker Compose for the full stack
**Labels:** `code`, `phase-4`
**Body:**

`docker-compose.yml` bringing up: API, PostgreSQL, oversight console, Prometheus/Grafana for monitoring. One command (`docker compose up`) gives reviewers a fully working demo.

### Issue 32
**Title:** Provider/Deployer split: restructure `project/`
**Labels:** `code`, `phase-4`, `refactor`
**Body:**

Reorganize `project/` to physically separate Provider artifacts from Deployer artifacts (`project/provider/` and `project/deployer/` subdirectories). Each gets its own README and compliance evidence trail. Addresses Q4 from the project review — makes the "Provider + Deployer" framing real instead of fictional.

### Issue 33
**Title:** Provider vs. Deployer responsibility matrix
**Labels:** `documentation`, `phase-4`
**Body:**

`docs/02-architecture/provider-vs-deployer.md`. For every AISEC control, who owns what artifact. Maps the seam between the two actor roles — the exact place where most real-world compliance fails.

### Issue 34
**Title:** Reference architecture document
**Labels:** `documentation`, `phase-4`
**Body:**

`docs/02-architecture/reference-architecture.md`. C4-style diagrams (context, container, component) of the compliance stack. Annotated with which AISEC controls live in which component.

---

## Phase 5 — Compliance Assurance

### Issue 35
**Title:** Pytest compliance test suite
**Labels:** `code`, `phase-5`, `epic`
**Body:**

`project/tests/` — one test file per AISEC domain. Each test verifies that the corresponding control's implementation evidence exists, is correctly structured, and produces expected outputs. This is the test suite that will let the README claim "every control is testable."

### Issue 36
**Title:** GitHub Actions CI for compliance tests
**Labels:** `chore`, `phase-5`
**Body:**

`.github/workflows/compliance.yml`. On every PR:

1. Lint the controls CSV (schema validation)
2. Run pytest compliance suite
3. Generate compliance report artifact
4. Comment on PR with pass/fail summary

This is the killer portfolio detail: the project visibly enforces its own compliance.

### Issue 37
**Title:** Compliance report generator
**Labels:** `code`, `phase-5`
**Body:**

`scripts/generate_compliance_report.py`. Reads controls.csv + test results + timeline.yaml + status from each control's implementation_evidence path. Produces:

- HTML report (for humans)
- JSON report (for machines / GRC tool ingestion)
- PDF report (for auditors)

### Issue 38
**Title:** Controls renderer (CSV → Markdown)
**Labels:** `code`, `phase-5`
**Body:**

`scripts/render_controls.py`. Reads controls.csv and produces `docs/03-controls/catalog.md` — a human-readable, filterable, searchable rendering of the catalog. Runs in CI; the generated file is committed.

### Issue 39
**Title:** Post-market monitoring components
**Labels:** `code`, `phase-5`
**Body:**

Implements AISEC-PM-001 through AISEC-PM-004:

- Drift detector (data drift + concept drift)
- Performance monitor
- Incident report template
- Corrective action procedure
- Unified incident process (AI Act + GDPR + DORA)

### Issue 40
**Title:** Conformity assessment artifacts
**Labels:** `documentation`, `phase-5`
**Body:**

Templates for AISEC-CA-001 through AISEC-CA-005:

- Conformity assessment procedure (internal control under Annex VI)
- EU Declaration of Conformity (Annex V)
- CE marking guide
- EU database registration guide
- Quality Management System framework (Art. 17)

### Issue 41
**Title:** Per-framework mapping deep-dives
**Labels:** `documentation`, `phase-5`
**Body:**

Six documents in `docs/03-controls/mappings/`:

- `nist-ai-rmf.md`
- `iso-42001.md`
- `owasp-llm-top10.md`
- `mitre-atlas.md`
- `gdpr.md`
- `dora.md`

Each one: how this catalog maps to that framework, with bidirectional coverage analysis (what we cover that they don't, what they cover that we don't).

---

## Phase 6 — Site, Translation, Polish

### Issue 42
**Title:** Astro site for the technical overview
**Labels:** `web`, `phase-6`, `epic`
**Body:**

Build the standalone Astro site at `eu-ai-act-blueprint.manzambi.com` (or similar). Pages: landing, all 7 overview chapters, controls explorer (searchable table from CSV), architecture, contact. Matches the existing manzambi.com aesthetic. i18n-ready.

### Issue 43
**Title:** French translations of overview chapters
**Labels:** `documentation`, `phase-6`
**Body:**

Translate the 7 overview chapters to French. Use `.fr.md` suffix convention. Add a `translated_from_version` field at the top of each French file with a CI check that warns when the English file has been updated more recently.

### Issue 44
**Title:** Demo GIFs and screenshots
**Labels:** `documentation`, `phase-6`
**Body:**

Record GIFs of: the oversight console in action, the compliance report generation, the adversarial robustness test running, a CI pipeline showing compliance pass. Embed in README and Astro site landing.

---

## Cross-cutting / deferred

### Issue 45
**Title:** Coverage comparison vs. ISO 42001 Annex A
**Labels:** `documentation`, `enhancement`
**Body:**

(Phase 1.75 — deferred but high-value.) Map each AISEC control to its closest ISO 42001 Annex A counterpart, with paraphrased one-line objectives so users can verify the mapping without paying for the standard. Identify gaps in both directions.

### Issue 46
**Title:** Coverage comparison vs. GPAI Code of Practice
**Labels:** `documentation`, `enhancement`
**Body:**

(Deferred to v0.2.) Once the GPAI Code of Practice has a stable final version, compare AISEC controls against it. Document overlap and gaps.

### Issue 47
**Title:** MAINTENANCE.md — update cadence policy
**Labels:** `documentation`, `enhancement`
**Body:**

(Phase 1.75 — deferred.) Publish explicit commitment to update cadence: "Updated within 30 days of any AI Act or AI Omnibus change. Stale after 60 days if no update." Include `last_verified` dates on every chapter and a CI check that flags stale documents.

### Issue 48
**Title:** Secondary catalog indexing: control_type and lifecycle_phase
**Labels:** `enhancement`
**Body:**

(Phase 1.75 — deferred.) Add two columns to controls.csv: `control_type` (preventive / detective / corrective) and `lifecycle_phase` (design / build / operate / monitor / retire). Makes the catalog auditor-friendly without disrupting the primary 15-domain structure.

### Issue 49
**Title:** NIS2 mapping
**Labels:** `enhancement`, `deferred-v0.3`
**Body:**

Add NIS2 column to controls.csv where cybersecurity controls overlap with NIS2 obligations for essential and important entities. Especially relevant for AI in critical infrastructure (Annex III area 2).

### Issue 50
**Title:** Cyber Resilience Act mapping
**Labels:** `enhancement`, `deferred-v0.3`
**Body:**

Add CRA column for products with digital elements that contain AI. Relevant from 2027.

---

## How to use this file

1. Create the issues in GitHub (web UI, GitHub CLI `gh issue create`, or API).
2. Apply the suggested labels (you'll need to create the label set first if it doesn't exist).
3. Group issues into a Project board with columns: Backlog / Next / In Progress / Done.
4. Delete this file from the repo once issues are created — its purpose is one-time bootstrap.

## Label set to create first

- `chore` — Maintenance, infrastructure
- `code` — Implementation work
- `documentation` — Prose documentation
- `web` — Astro site work
- `enhancement` — Improvement to existing artifact
- `refactor` — Restructuring
- `epic` — Multi-step issue, may spawn sub-issues
- `good-first-issue` — Welcoming label for contributors
- `deferred-v0.3` — Scope, but not in next minor
- `phase-1` through `phase-6` — Phase tagging (optional)
