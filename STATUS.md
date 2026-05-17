# Status

**As of 15 May 2026** · v0.1.3

## What works today

This project currently provides three usable artifacts:

- **A controls catalog** (`data/controls.csv`) — 79 controls derived from the EU AI Act and mapped to six supporting frameworks (NIST AI RMF, ISO/IEC 42001, OWASP LLM Top 10, MITRE ATLAS, GDPR, DORA). Schema-validated. Documented methodology.
- **An EU AI Act technical overview** — two chapters published (scope & jurisdiction, risk classification). Five more chapters planned.
- **A threat model** (`docs/02-architecture/threat-model.md`) — STRIDE + MITRE ATLAS + LINDDUN applied to a high-risk CV-screening use case. 46 distinct threats identified; all mapped to controls in the catalog.

The reasoning layer is complete: anyone can read [`docs/03-controls/methodology.md`](docs/03-controls/methodology.md) to understand why each control exists and how the count of 79 was derived.

## What is next

The next deliverable is **Phase 2: Data Governance** — implementing EU AI Act Article 10 controls against a working CV-screening dataset. This includes a synthetic dataset with documented bias injection, a bias detection pipeline using Fairlearn, and the data quality and provenance modules.

Work on Phase 2 is tracked in [GitHub Issues](https://github.com/josephManzambi/eu-ai-act-blueprint/issues).

## How to read this status

This project is built in phases that each produce a standalone, shareable artifact. Phases 1 and 1.5 (foundation + defensibility hardening) are complete. The catalog and threat model are usable today, even before the working demo exists.

For the version history, see [`CHANGELOG.md`](CHANGELOG.md).

For honest limitations and what this project is not trying to be, see [`WHAT_THIS_IS_NOT.md`](WHAT_THIS_IS_NOT.md).
