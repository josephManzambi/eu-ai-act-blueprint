# What This Project Is Not

Honest boundaries for the EU AI Act Blueprint. Read this before relying on anything in this repository.

---

## This is not legal advice

Nothing in this repository is legal advice. The author is an AI security architect, not a lawyer. The mappings between AI Act articles and technical controls represent one engineer's interpretation of the regulation. Where the regulation is ambiguous, this project picks a reasonable engineering interpretation — which may differ from the interpretation that a competent national authority, the European Commission, or your in-house legal team would adopt.

**If you are making compliance decisions for a real organization: consult a qualified lawyer in your jurisdiction.** This project is a starting point for engineering conversations, not a substitute for legal review.

---

## This is not a substitute for conformity assessment

The EU AI Act requires specific conformity assessment procedures (Art. 43, Annex VI, Annex VII) for high-risk AI systems. Some assessments must be performed with the involvement of a notified body. This project provides templates and reference implementations of the artifacts you would produce during conformity assessment — but the assessment itself must be performed by your organization (and, where required, by a notified body).

**Using the templates here does not produce a conformity-assessed system.** It produces *documentation that demonstrates good-faith engineering practice* — a useful but distinct thing.

---

## This is not a guarantee of compliance

Even a perfect implementation of every control in this catalog does not guarantee compliance with the EU AI Act. Compliance depends on facts specific to your organization: your actual system architecture, your data sources, your operational practices, your incident history, and decisions made by competent authorities about your specific case.

The controls in this catalog are *necessary* engineering measures for compliance. They are not *sufficient* on their own. A well-implemented catalog plus a poorly-run organization still produces non-compliance.

---

## This is not a marketing pitch for any product

This project is vendor-neutral by design. It is not endorsed by, affiliated with, or selling any specific commercial product. The implementation choices (FastAPI, PostgreSQL, sentence-transformers, OpenTelemetry, etc.) reflect what the author would build in a real engineering setting — not paid promotions or partnerships.

**If you see this project recommending a specific commercial AI governance platform, something has gone wrong.** Open an issue.

---

## This is not a complete AI risk framework

The EU AI Act addresses risks to health, safety, and fundamental rights. It does not address every meaningful AI risk: economic disruption, environmental impact, concentration of power, long-term societal effects, existential risks, or ethical questions about whether an AI system *should exist* in the first place.

This project follows the regulation's scope. It does not ask "should we build this system?" — it only asks "if we are building this system, how do we comply with EU AI Act requirements?" The first question is more important. This project does not answer it.

---

## This is not a fixed reference

The EU AI Act is being actively shaped. The AI Omnibus (May 2026) significantly changed enforcement timelines. The AI Office is publishing implementing acts. Harmonized standards from CEN-CENELEC JTC 21 are in draft. National competent authorities are issuing guidance. Court decisions interpreting the Act will begin appearing.

**Treat the version of this project you are reading as a snapshot in time.** Check the `last_verified` date in `data/timeline.yaml` and the version tag in the repository. If neither has been updated in the last 60 days, parts of this project may be stale.

---

## This is not for use cases the author has not modeled

The reference implementation targets one specific high-risk use case: CV-screening / candidate ranking under Annex III area 4 (employment). The threat model, control selection, and architectural decisions reflect that use case. They will not transfer cleanly to:

- Medical diagnosis AI (different risk profile, additional MDR requirements)
- Credit scoring (different bias-sensitivity, different appeal mechanisms)
- Critical infrastructure AI (different operational continuity requirements)
- Law enforcement AI (different fundamental rights considerations)
- Generative AI products with end-user content (different transparency obligations)

If your use case is in Annex III but is not CV-screening, this project is a *starting point*, not a *drop-in solution*. You will need to repeat the threat modeling and control selection for your specific context.

---

## This is not maintained by a team

This project is currently maintained by one person ([Joseph Manzambi](https://manzambi.com)). It is not backed by a foundation, a consortium, or a company. Maintenance commitments are best-effort and subject to one individual's bandwidth.

The maintenance cadence policy (`docs/MAINTENANCE.md`, when published) sets out explicit expectations. If those expectations are not met, the project may go stale faster than commercial alternatives.

---

## What this project *is*

A reference implementation showing how a security architect would approach EU AI Act compliance, end-to-end, for one concrete high-risk use case. A documented methodology for deriving controls from regulatory text. A threat model that justifies control selection. A starting point for teams who need to translate the AI Act into engineering decisions.

If that is what you need: welcome.
