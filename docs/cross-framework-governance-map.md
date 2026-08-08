# Cross-Framework Governance Map

## Overview

This document maps the AI governance and incident response standards in this framework across the full ecosystem of open-source fintech frameworks published at github.com/sujiyer. Together these frameworks form a connected architecture — each addressing one layer of the financial technology stack, with shared governance standards ensuring consistency across layers.

The governance map answers a practical question for any financial institution using more than one of these frameworks: **how do the AI governance requirements apply to each framework, and how do the frameworks connect?**

---

## The Framework Ecosystem

```
┌─────────────────────────────────────────────────────────────────────┐
│              FINTECH AI GOVERNANCE & INCIDENT RESPONSE              │
│                    (This Framework)                                 │
│   Model Validation │ Bias Monitoring │ Explainability │ Audit Trail │
│   Incident Classification │ Investigation │ Regulatory Notification │
└──────────┬───────────────┬──────────────────┬────────────────┬──────┘
           │               │                  │                │
           ▼               ▼                  ▼                ▼
┌──────────────┐  ┌─────────────────┐  ┌──────────────┐  ┌──────────────────┐
│  KYC API     │  │ RESEARCH        │  │ RECONCILIA-  │  │ FINANCIAL        │
│  FRAMEWORK   │  │ WORKSPACE       │  │ TION BREAK   │  │ LITERACY &       │
│              │  │ FRAMEWORK       │  │ FRAMEWORK    │  │ ACCESSIBILITY    │
│ Identity     │  │ AI Research     │  │ AI-assisted  │  │ Plain-language   │
│ verification │  │ Assistant       │  │ break        │  │ explanations     │
│ Document AI  │  │ Risk scoring    │  │ classification│  │ Onboarding UX   │
│ Risk scoring │  │ Recommendations │  │ Resolution   │  │ Financial        │
│ Fraud flags  │  │ Factor models   │  │ suggestions  │  │ inclusion AI     │
└──────────────┘  └─────────────────┘  └──────────────┘  └──────────────────┘
```

The AI Governance framework is the **horizontal layer** that applies to all frameworks below it. Every AI component in every framework is governed by the same standards: the same model validation checklist, the same bias monitoring protocol, the same audit trail specification, and the same incident response playbook.

---

## KYC API Framework — Governance Application

**Repository:** github.com/sujiyer/kyc-api-framework

**AI components requiring governance:**

| AI Component | Risk Tier | Governance Requirements |
|---|---|---|
| Identity confidence scoring | **High** | Full model validation; bias monitoring monthly; explainability Level 2 and 3 |
| Document authenticity scoring | **High** | Full model validation; hallucination risk assessment; confidence threshold required |
| Sanctions screening match scoring | **High** | Full model validation; false positive rate monitoring; human review for all matches |
| Risk tier assignment | **High** | Full model validation; demographic parity monitoring; fair lending review |
| Progressive verification trigger | **Medium** | Validation of trigger logic; escalation rate monitoring |

**Key governance connections:**

**Bias monitoring in KYC:**
The identity confidence score is the primary exclusion mechanism in onboarding. If the model systematically produces lower confidence scores for applicants from specific demographic groups — recent immigrants, rural residents, people without traditional credit files — it is replicating exclusion algorithmically. The bias monitoring protocol's KYC and identity verification metrics table must be applied monthly.

**Explainability in KYC adverse actions:**
ECOA requires adverse action notices for credit-related denials. Where KYC denial triggers ECOA coverage, the explainability requirements' Level 3 consumer explanation standard must be met. The consumer explanation must name specific reasons — not "we could not verify your identity" but "the address on your ID does not match the address you provided."

**Incident response for KYC failures:**
A KYC model systematically failing identity verification for a demographic group is a Level 1 incident — it is causing demonstrable harm to consumers' access to financial services. The 4-hour containment protocol applies. Progressive verification must be activated immediately as the fallback while the model is investigated.

**Audit trail in KYC:**
Every identity verification decision, progressive verification trigger, and sanctions screening result must be logged per the Audit Trail Specification. KYC audit logs are retained for 5 years minimum per BSA requirements.

---

## Research Workspace Framework — Governance Application

**Repository:** github.com/sujiyer/research-workspace-framework

**AI components requiring governance:**

| AI Component | Risk Tier | Governance Requirements |
|---|---|---|
| AI Research Assistant — summaries | **Medium** | Validation; confidence threshold; human review queue for low-confidence outputs |
| AI Research Assistant — recommendations | **High** | Full validation; Reg BI disclosure requirements; explainability Level 2 |
| Risk metrics AI components | **High** | Full validation; outcome monitoring; context-linked explainability |
| Factor model AI components | **Medium** | Validation; performance monitoring; calibration review quarterly |
| News aggregator NLP tagging | **Low** | Basic validation; accuracy monitoring semi-annually |

**Key governance connections:**

**Explainability in investment AI:**
The "Why Google and not Tesla?" explainability standard — where every AI recommendation must cite specific, verifiable data points rather than summarising a reasoning process — is the Level 3 explainability requirement applied to investment AI. This is not optional where Regulation Best Interest applies to retail-facing outputs.

**Fiduciary AI governance:**
AI-assisted research that reaches retail clients through relationship managers or adviser platforms sits at the intersection of NIST AI RMF and Regulation Best Interest. The governance framework's model validation checklist includes a Reg BI compliance gate — legal review before any AI component is deployed in a retail-client-facing context.

**Hallucination risk as an incident trigger:**
An AI Research Assistant that produces a confident but incorrect recommendation — a hallucinated ticker symbol, a misremembered historical pattern — is a potential Level 2 or Level 3 AI incident if it reaches a portfolio decision. The incident classification protocol applies. The investigation must determine whether the hallucination was isolated or systematic.

**Audit trail in research AI:**
Every Research Assistant inference is logged per the Audit Trail Specification. Investment audit logs are retained for 6 years minimum per FINRA Rule 4511. The model version, input data, confidence score, and key factors are all required fields — supporting both regulatory examination and the "explain this decision" right of investment professionals.

---

## Reconciliation Break Framework — Governance Application

**Repository:** github.com/sujiyer/reconciliation-break-framework

**AI components requiring governance:**

| AI Component | Risk Tier | Governance Requirements |
|---|---|---|
| Break classification AI | **Medium** | Validation; accuracy monitoring; human review for high-value breaks |
| Resolution suggestion AI | **Medium** | Validation; acceptance rate monitoring; override logging |
| Root cause identification AI | **Medium** | Validation; false positive rate monitoring |

**Key governance connections:**

**Operational AI incidents:**
A break classification model that systematically misclassifies breaks — routing high-severity breaks to low-priority queues — is a Level 3 AI incident under this framework. The investigation protocol applies: what caused the misclassification, how many breaks were affected, and what was the financial impact of the incorrect routing?

**Audit trail in reconciliation:**
AI-assisted break classification and resolution suggestions are logged per the Audit Trail Specification. When a human reviewer overrides an AI suggestion, the override and rationale are logged. This creates an accountability record for the operations team and an improvement signal for the model.

---

## Financial Literacy and Accessibility — Governance Application

**Referenced in:** KYC API Framework (docs/financial-literacy-integration.md, docs/mobile-accessibility-design.md)

**AI components requiring governance:**

| AI Component | Risk Tier | Governance Requirements |
|---|---|---|
| Plain-language explanation generation | **Medium** | Validation for accuracy; hallucination monitoring; multi-language accuracy review |
| Reading level calibration AI | **Low** | Basic validation; accuracy testing by reading level |
| Contextual help recommendation | **Low** | Basic validation; relevance monitoring |

**Key governance connections:**

**Hallucination in consumer-facing explanations:**
An AI system generating plain-language adverse action explanations must not hallucinate. A consumer receiving an incorrect explanation of why they were denied account access — or an incorrect statement of their rights — is not just a UX failure. It may constitute a UDAAP violation. Plain-language AI components require hallucination monitoring as a specific bias monitoring metric.

---

## Shared Governance Infrastructure

These elements of the AI Governance framework apply identically across all frameworks:

| Element | Applies To |
|---|---|
| Audit Trail Specification | All AI components in all frameworks |
| Model Registry | All AI components in all frameworks |
| Incident Classification | All AI failures in all frameworks |
| Regulatory Notification Guide | All incidents with potential regulatory implications |
| CONTRIBUTING.md standards | All framework repositories |

---


The cross-framework governance map represents a practical contribution that goes beyond any single framework. By publishing a governance standard that applies consistently across KYC, research platforms, reconciliation systems, and financial literacy tools, this ecosystem provides financial institutions — particularly smaller institutions without dedicated AI governance teams — with a coherent, interoperable governance infrastructure.

This is the "standardisation" problem named in current AI policy discussions: not a shortage of AI governance guidance, but a shortage of practical, implementable, institution-specific governance standards that connect across a financial technology stack.

This framework ecosystem is a direct, open-source response to that gap.

*For the full framework ecosystem, see github.com/sujiyer*
