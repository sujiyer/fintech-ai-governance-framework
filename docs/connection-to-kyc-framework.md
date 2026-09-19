# How These Two Frameworks Connect

## Two Tools, One Purpose

This repository contains one of two open-source frameworks built together as a connected system for American financial institutions:

**Framework 1 — KYC API Framework for Financial Inclusion**
`github.com/sujiyer/kyc-api-framework`

A reference architecture for identity verification onboarding — the API design, data models, progressive verification pathways, and compliance alignment that let a financial institution build a KYC system that works for thin-file applicants without starting from scratch.

**Framework 2 — Fintech AI Governance and Incident Response Framework**
`github.com/sujiyer/fintech-ai-governance-framework`

The governance layer that ensures any AI component operating within a financial institution — including those built using the KYC framework — is validated before deployment, monitored for bias and drift during operation, and investigated and remediated when it fails.

These two frameworks are designed to work together. Neither is complete without the other.

---

## Why They Need Each Other

Modern KYC and onboarding systems increasingly use AI components at multiple decision points:

- **Identity confidence scoring** — a model that scores how likely it is that an applicant is who they say they are
- **Document authenticity assessment** — a model that evaluates whether an uploaded ID document is genuine
- **Risk tier assignment** — a model that classifies an applicant as low, medium, or high risk to determine the verification path
- **Fraud signal scoring** — a model that flags potentially fraudulent applications before they proceed

Each of these AI components is a point where a biased or poorly validated model can systematically exclude the exact populations the KYC framework is designed to serve — thin-file applicants, recent immigrants, gig economy workers, people rebuilding financially.

A KYC system built on the API framework without AI governance can produce fair-looking architecture that still denies access to underserved populations because of unchecked model bias. The AI governance framework is what prevents that.

---

## How They Work Together in Practice

**At deployment:**

An institution builds its KYC onboarding system using the KYC API Framework architecture. Before the system goes live, every AI component within it — the identity confidence model, the document authenticity model, the risk tier classifier — is validated using the Pre-Deployment Testing Protocol from the AI Governance Framework.

The test results are filed in the Model Registry. The model owners are named. The kill switches are confirmed. The audit logging is verified. Only then does the system deploy.

**During operation:**

The KYC system processes applications. Each AI-assisted decision is logged to the audit trail per the Audit Trail Specification. The bias monitoring protocol runs monthly on the identity confidence model — checking whether verification pass rates are consistent across demographic groups. The model drift checkpoints run quarterly — catching whether the training data is becoming outdated.

**When something goes wrong:**

A monitoring flag shows the identity confidence model's pass rate for applicants with non-standard address histories has dropped 18 percentage points below the general population average. Under the Incident Classification guide, this is a Level 2 incident. The containment playbook is followed. The investigation protocol reconstructs what happened. The remediation checklist ensures the model is fixed before it returns to production. The regulatory notification guide helps the institution assess whether the CFPB or primary regulator needs to be informed.

---

## The Shared Goal

Both frameworks exist because the same gap is real at two different levels.

At the product level: financial institutions — especially smaller ones — are rebuilding the same onboarding infrastructure from scratch because there is no shared starting point. The KYC API Framework provides that starting point.

At the governance level: financial institutions are deploying AI in consequential decisions without a shared standard for how to test it, monitor it, or respond when it fails. The AI Governance Framework provides that standard.

Together, they are an attempt to give any financial institution in America — including a community bank with two developers or a CDFI serving an agricultural community — the infrastructure and the accountability layer to build systems that actually work for the people they are meant to serve.

---

## Contributing to Both

Contributions that improve either framework are welcome. Contributions that explicitly address how the two frameworks interact — how AI governance applies to specific KYC system components, how the audit trail specification should be adapted for high-volume KYC processing, how the incident response playbook applies when a KYC AI fails during peak onboarding season — are especially valuable.

Open an issue on either repository or reach out directly.
