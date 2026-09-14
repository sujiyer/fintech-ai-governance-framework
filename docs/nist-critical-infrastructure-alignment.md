# NIST Trustworthy AI in Critical Infrastructure — Alignment Guide

## Overview

Financial services infrastructure is explicitly recognized as critical infrastructure by the U.S. Department of Homeland Security. This means that AI systems operating within financial services fall under the scope of NIST's work on Trustworthy AI in Critical Infrastructure — a cross-sector initiative that connects NIST AI RMF 1.0 to the specific requirements, failure modes, and governance obligations of sectors whose disruption would have national consequences.

This document maps the Fintech AI Governance Framework to NIST's critical infrastructure AI work, shows how the framework satisfies the core trustworthiness properties NIST has defined, and explains why AI governance in financial services is a national security issue, not just a compliance issue.

---

## Financial Services as Critical Infrastructure

The Financial Services Sector is one of 16 critical infrastructure sectors identified in Presidential Policy Directive 21. The sector includes:

- Depository institutions: banks, credit unions, savings institutions
- Investment institutions: broker-dealers, investment companies, registered investment advisers
- Insurance companies
- Financial market utilities: payment systems, clearinghouses, exchanges
- Non-bank financial institutions: fintech companies, money service businesses

AI systems operating in any of these institutions are operating in critical infrastructure. A systemic failure of AI in financial services — whether through widespread biased decisions, coordinated model manipulation, or cascading incidents across interconnected institutions — could affect the financial stability, consumer confidence, and economic participation of millions of Americans.

---

## NIST AI RMF 1.0 — Core Trustworthiness Properties

NIST AI RMF 1.0 defines seven properties of trustworthy AI. The table below maps each property to the specific documents in this framework that address it:

| NIST Trustworthiness Property | Framework Implementation |
|---|---|
| **Accountable and Transparent** | Audit Trail Specification; Explainability Requirements; Incident Classification |
| **Explainable and Interpretable** | Explainability Requirements — consumer, decision, and system levels |
| **Fair with Harmful Bias Managed** | Bias Monitoring Protocol; Pre-Deployment Testing Protocol (Section 3) |
| **Privacy Enhanced** | Audit Trail Specification (data minimization); Model Validation Standards (proxy variable identification) |
| **Safe** | Pre-Deployment Testing Protocol; Containment Playbook |
| **Secure and Resilient** | Incident Classification; Containment Playbook; Model Drift Monitoring Checkpoints |
| **Valid and Reliable** | Pre-Deployment Testing Protocol (Sections 1 and 2); Model Drift Monitoring Checkpoints |

---

## NIST AI RMF Functions — Critical Infrastructure Application

### GOVERN
*Establishing policies, accountability, and organizational practices.*

In critical infrastructure contexts, governance of AI systems requires documented accountability chains — not just internal accountability but accountability that is legible to regulators, examiners, and in significant incidents, to congressional oversight.

**Framework implementation:** Model owner assignment; sign-off requirements by risk tier; Model Registry as the authoritative accountability record; CONTRIBUTING.md defining community governance for the open-source framework itself.

**Critical infrastructure consideration:** For financial institutions participating in financial market utilities (payment systems, clearinghouses), AI governance documentation must be available to the system's oversight body on request. The Model Registry structure in this framework is designed to satisfy that requirement.

### MAP
*Categorizing AI risks and understanding context.*

Critical infrastructure AI requires explicit acknowledgment of systemic risk — not just the risk to a single institution but the risk of correlated failures across institutions using similar AI systems.

**Framework implementation:** Model risk tier classification; population representativeness testing; proxy variable identification.

**Critical infrastructure consideration:** When multiple financial institutions purchase AI from the same vendor, they may all be running the same underlying model. A bias or failure in that model could produce correlated adverse outcomes across the sector. The Third-Party Vendor Assessment (referenced in the framework roadmap) is the specific response to this systemic risk.

### MEASURE
*Analyzing and assessing AI risks.*

**Framework implementation:** Pre-Deployment Testing Protocol; Model Drift Monitoring Checkpoints; Bias Monitoring Protocol.

**Critical infrastructure consideration:** For systemically important financial institutions (SIFIs), measurement must include stress testing under adverse scenarios — economic downturns, market disruptions, or novel fraud patterns not present in training data. The stress condition testing in Pre-Deployment Testing Section 2.2 addresses this.

### MANAGE
*Prioritizing and addressing AI risks.*

**Framework implementation:** Incident Classification (Level 1 through 4); Containment Playbook; Investigation Protocol; Remediation Checklist; Regulatory Notification Guide.

**Critical infrastructure consideration:** For critical infrastructure, incident response is not only an internal matter. Significant AI failures may require notification to sector-specific regulatory agencies (OCC, FDIC, Federal Reserve, NCUA), the CFPB, and in severe cases, to DHS's Cybersecurity and Infrastructure Security Agency (CISA).

---

## Connection to Active NIST Initiatives

**NIST Trustworthy AI in Critical Infrastructure Community of Interest**
This Community of Interest brings together practitioners from all 16 critical infrastructure sectors to share practices and inform NIST's ongoing AI governance work. Financial services participants in this community are contributing practical implementation experience that informs NIST's guidance documents.

This framework is an example of the kind of cross-institutional, publicly available governance tooling that the Community of Interest exists to develop and share.

**NIST SP 800-30 — Risk Management for Information Systems**
NIST SP 800-30 provides risk assessment guidance for information systems in federal agencies and regulated industries. The risk tier classification and pre-deployment testing protocol in this framework are consistent with SP 800-30's risk-based approach to information system management.

**NIST Cybersecurity Framework (CSF) 2.0**
The CSF's GOVERN, IDENTIFY, PROTECT, DETECT, RESPOND, and RECOVER functions map directly to the lifecycle of AI governance in this framework: governance setup, model identification and classification, pre-deployment testing (protect), monitoring (detect), incident response (respond and recover).

---

## Why This Matters at National Scale

Your institution's AI governance program does not exist in isolation. Financial services AI decisions are interconnected:

- A fraud model at a community bank uses network signals from a payment processor whose fraud model was trained on data from a national bank
- A KYC identity verification vendor serves thousands of institutions simultaneously
- Credit score models influence decisions across the entire credit market

When one institution's AI governance fails, the consequences can propagate. When governance standards are shared and consistent across institutions — especially the smaller community banks and credit unions that serve the most financially vulnerable Americans — the financial system as a whole becomes more resilient.

This is the national importance argument for open-source AI governance frameworks in financial services. The work is not about any single institution. It is about the infrastructure that connects them all.
