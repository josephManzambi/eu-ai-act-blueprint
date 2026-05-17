# Scope and Jurisdiction

> **Relevant articles:** Art. 1, Art. 2, Art. 3  
> **Related controls:** AISEC-RM-001, AISEC-GV-002  
> **Key takeaway:** The EU AI Act applies to any company whose AI system produces effects in the EU — regardless of where the company is headquartered.

---

## Who is in scope

The EU AI Act (Regulation 2024/1689) does not just apply to EU-based companies. Its jurisdictional reach is deliberately modeled on GDPR's approach: what matters is where the **effects** of the AI system are felt, not where the code was written.

Article 2 defines four categories of actors that fall under the regulation:

### 1. Providers established in the EU

Any company or person established in the Union that develops an AI system or a general-purpose AI model — or has one developed on their behalf — and places it on the market or puts it into service under their own name or trademark.

**Example:** A French SaaS company that builds a CV-screening tool and sells it to European employers.

### 2. Providers established outside the EU — placing systems on the EU market

Any non-EU company that places an AI system on the Union market or puts it into service in the Union.

**Example:** A US enterprise software vendor whose hiring platform includes an AI-based candidate ranking module. If European companies use it, the vendor is a Provider under the AI Act — even if the company has no legal entity, office, or server in Europe.

### 3. Deployers established in the EU

Any company or person established in the Union that uses an AI system under its authority. This is the most common category for European enterprises: they buy or integrate third-party AI into their workflows.

**Example:** A German bank deploying a third-party AI tool for transaction monitoring. The bank is the Deployer and has its own set of obligations — separate from and in addition to the Provider's.

### 4. Non-EU actors whose system outputs are used in the EU

Providers and Deployers of AI systems that are established in a third country, where the **output produced by the system is used in the Union**.

**Example:** A company headquartered in Singapore operates an AI system that scores European citizens' creditworthiness for a partnership with a European lender. Even if the system runs on Singaporean infrastructure, the output is used in the EU — so the AI Act applies.

---

## What counts as an "AI system"

Article 3(1) defines an AI system as:

> A machine-based system that is designed to operate with varying levels of autonomy and that may exhibit adaptiveness after deployment and that, for explicit or implicit objectives, infers, from the input it receives, how to generate outputs such as predictions, content, recommendations, or decisions that can influence physical or virtual environments.

This definition is broad by design. It covers:

- Traditional ML models (classification, regression, ranking)
- Deep learning systems (neural networks, transformers, diffusion models)
- LLM-based applications (chatbots, retrieval-augmented generation, agentic systems)
- Rule-based systems that exhibit autonomy and adaptiveness
- Hybrid systems combining statistical methods with symbolic reasoning

What it does **not** cover:

- Simple rule-based software with no learning or inference capability (e.g., if/else business logic)
- Traditional databases and search engines without AI-driven ranking
- Basic statistical tools (spreadsheet formulas, standard analytics)

### The "adaptiveness" nuance

The phrase "may exhibit adaptiveness after deployment" is important for security architects. A model that continues learning in production (online learning, reinforcement learning from human feedback) has additional risk characteristics: its behaviour can drift or be manipulated post-deployment. This directly affects how you implement controls AISEC-PM-002 (drift detection) and AISEC-RB-003 (adversarial robustness testing).

---

## Exclusions

Article 2 carves out several explicit exclusions:

- **Military and defense:** AI systems placed on the market, put into service, or used exclusively for military purposes.
- **Non-EU international organizations:** AI systems used by public authorities of third countries or international organisations under international agreements with the EU for law enforcement and judicial cooperation.
- **Research and development:** AI systems or models specifically developed and put into service for the sole purpose of scientific research and development. **Caveat:** this exclusion does not apply once the system is placed on the market or put into service for a non-research purpose.
- **Personal non-professional activity:** Natural persons using AI systems in the course of a purely personal non-professional activity.
- **Open-source models (with limits):** Free and open-source AI models are exempt from most GPAI obligations *unless* they are GPAI models with systemic risk. Open-source high-risk AI systems are still subject to Article 8–15 requirements.

### The open-source trap

The open-source exemption is narrower than it first appears. If you are a company that downloads an open-source model from Hugging Face, fine-tunes it for candidate screening, and deploys it internally — you are a **Provider** of a high-risk AI system under the Act. The open-source exemption applied to the *original model author*, not to you. Your fine-tuned system must meet all high-risk requirements.

This is a critical point for enterprises that rely on open-source foundation models as the basis for internal AI applications.

---

## Extraterritorial reach in practice

For companies operating internationally, the AI Act's extraterritorial provisions create obligations similar to GDPR's global reach but applied to AI-specific risks. The practical implications:

### If you are a US/UK/APAC company selling to European customers

- You are a **Provider** for any AI system placed on the EU market
- You must appoint an **authorized representative** established in the EU (Art. 22) before making your system available — see control AISEC-GV-002
- You must comply with all applicable requirements for your system's risk category
- You face the same penalty regime as EU-based companies (up to €35M or 7% of global turnover)
- You must register high-risk systems in the EU database (Art. 49)

### If you are a European company using third-party AI

- You are a **Deployer** with your own set of obligations
- You cannot outsource compliance to your vendor — even if the vendor is fully compliant as a Provider, you still have Deployer duties
- You must conduct a fundamental rights impact assessment for certain use cases (Art. 27)
- You must monitor the system's performance, retain logs, and report incidents
- If you significantly modify the AI system, you may become a Provider yourself (Art. 25)

### The "significant modification" reclassification

Article 25 introduces a critical concept: if a Deployer makes a **substantial modification** to a high-risk AI system — one that changes its intended purpose or affects its compliance with Article 8–15 requirements — that Deployer becomes a Provider and assumes all Provider obligations.

What counts as a substantial modification is context-dependent, but examples include:
- Fine-tuning a model on new data that changes its performance characteristics
- Changing the intended purpose of the system (e.g., from candidate ranking to automated rejection)
- Modifying the system's architecture in ways that affect accuracy, robustness, or cybersecurity
- Integrating additional data sources that alter the system's behavior

The July 2025 Commission guidelines provide practical criteria for when modifications trigger reclassification. As a security architect, the safe default is: **if you're modifying a high-risk system's model or data pipeline, assess whether you've crossed the Provider threshold.**

---

## Relationship with other regulations

The EU AI Act does not operate in isolation. Several other EU regulations interact with it, creating overlapping (but not duplicating) obligations:

| Regulation | Interaction with AI Act | Controls |
|-----------|------------------------|----------|
| **GDPR (2016/679)** | AI systems processing personal data must comply with both. DPIA required for high-risk AI. Automated decision-making safeguards (Art. 22) overlap with human oversight. | AISEC-GV-007, AISEC-GV-008 |
| **DORA (2022/2554)** | Financial sector AI systems are subject to both AI Act and DORA ICT risk management, incident reporting, and third-party risk requirements. | AISEC-GV-004, AISEC-GV-005, AISEC-GV-006 |
| **Product safety (2023/988)** | AI systems that are safety components of products must meet both AI Act and General Product Safety Regulation requirements. | — |
| **Machinery Regulation (2023/1230)** | Under the AI Omnibus (May 2026), AI subject to the Machinery Regulation is **carved out entirely** from the AI Act's direct application. AI-related safety measures for machinery will be handled via delegated acts under the Machinery Regulation itself. | — |
| **Medical Devices (2017/745)** | AI-based medical devices are high-risk under both the AI Act and MDR. Existing MDR conformity assessment can be leveraged. | — |
| **NIS2 Directive (2022/2555)** | Cybersecurity requirements under Art. 15 align with NIS2 obligations for essential and important entities. | AISEC-CS-001 |

The controls catalog (Deliverable 3) maps these intersections explicitly, allowing you to build **one unified compliance program** rather than siloed efforts per regulation.

---

## Practical first step: Classification

Before anything else, every AI system in your portfolio needs to be classified. This is where the entire compliance journey starts, and it is codified as control **AISEC-RM-001**.

The next chapter — [Risk Classification](risk-pyramid.md) — provides the decision tree for performing this classification, walking through Article 6, Annex III, and the practical edge cases that trip most teams up.

---

*Next: [Risk Classification →](risk-pyramid.md)*
