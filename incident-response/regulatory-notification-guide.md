# Regulatory Notification Guide

When an AI incident in a financial institution may constitute a regulatory violation, institutions face an additional obligation beyond internal remediation: notifying the appropriate regulatory body. This guide defines when notification is required, who to notify, what to include, and how to prepare.

---

## Critical Principle: Involve Legal Counsel First

This guide provides a framework for thinking about regulatory notification — it does not replace legal advice. The decision to notify a regulator, the timing of that notification, and the content of any communication must be reviewed by legal counsel before submission. Notifying a regulator without legal review can inadvertently expand liability or waive privilege.

**Before notifying any regulator:**
1. Notify General Counsel or outside legal counsel immediately
2. Document all actions taken from incident identification forward
3. Preserve all audit log records and model artifacts — do not modify
4. Wait for legal guidance on notification decision before contacting regulators

---

## Notification Decision Framework

Not every AI incident requires regulatory notification. Use this framework to assess:

```
AI Incident Confirmed
        ↓
Step 1: Consumer harm assessment
  Were consumers financially harmed? (money lost, credit denied, account restricted)
        ↓ Yes            ↓ No
  Proceed to           Continue monitoring
  Step 2              Document internally
  
Step 2: Scope assessment
  How many consumers affected?
  < 100 and limited harm → Internal remediation, monitor
  100–1,000 or material harm → Legal review, likely notification
  > 1,000 or systemic → Immediate legal review, probable notification
  
Step 3: Violation assessment
  Does the incident constitute a potential:
  - Fair lending violation (ECOA, FHA)?      → Regulator notification likely required
  - BSA/AML compliance failure?              → FinCEN notification may be required
  - Consumer protection violation (CFPB)?    → CFPB notification may be required
  - Cybersecurity / data breach component?   → State and federal notification required
  - Safety and soundness concern?            → Primary federal regulator notification
```

---

## Regulatory Body Reference

### CFPB — Consumer Financial Protection Bureau
**Jurisdiction:** Consumer financial protection violations — fair lending, unfair/deceptive/abusive acts or practices (UDAAP), ECOA violations in credit decisions

**When to notify:** AI-driven UDAAP violation, systematic fair lending violation in consumer credit products, significant adverse consumer impact from algorithmic decision-making

**How to notify:** CFPB does not have a standardised AI incident notification process as of this publication. Contact through CFPB's supervisory channel for regulated institutions. Consult legal counsel on whether voluntary disclosure is appropriate.

**Key contact:** cfpb.gov/about-us/contact-us/

---

### OCC — Office of the Comptroller of the Currency
**Jurisdiction:** National banks and federal savings associations

**When to notify:** Safety and soundness concerns, significant operational incidents affecting AI systems, fair lending violations, incidents that may affect public confidence

**Timeframe:** Serious incidents — notify within 36 hours (aligned with OCC computer security incident notification rule)

**How to notify:** Through the institution's supervisory office. OCC's Computer-Security Incident Notification Rule (12 CFR Part 53) applies to bank service providers and covers AI system failures that constitute computer-security incidents.

---

### Federal Reserve
**Jurisdiction:** State member banks, bank holding companies, foreign banking organisations

**When to notify:** Same triggers as OCC for applicable institutions. Federal Reserve's incident notification rule mirrors OCC requirements.

---

### FDIC — Federal Deposit Insurance Corporation
**Jurisdiction:** State non-member banks and state savings associations

**When to notify:** Same framework as OCC. FDIC's computer-security incident notification rule aligns with OCC and Federal Reserve.

**Timeframe:** Within 36 hours for significant computer-security incidents.

---

### NCUA — National Credit Union Administration
**Jurisdiction:** Federally insured credit unions

**When to notify:** Cybersecurity incidents, significant operational failures, potential fair lending violations in AI systems used for member-facing decisions

**Contact:** ncua.gov/regulation-supervision/regulatory-reporting/credit-union-online-reporting-system

---

### FinCEN — Financial Crimes Enforcement Network
**Jurisdiction:** BSA compliance across all financial institutions

**When to notify:** If an AI incident caused a failure in BSA/AML compliance — for example, if a fraud detection model was incorrectly suppressing Suspicious Activity Reports or if a KYC AI was systematically failing to identify high-risk customers

**Note:** FinCEN notification for AI-related BSA failures is a developing area. Legal counsel is essential.

---

### State Regulators
**Jurisdiction:** State-chartered institutions and any institution with significant consumer impact in a state

**When to notify:** Many states have their own AI and algorithmic decision-making notification or examination requirements. State data breach laws may also apply if the AI incident involved a data component.

**Action:** Check the applicable state banking regulator and state attorney general requirements for the states where affected consumers are located.

---

## What to Include in a Regulatory Notification

A regulatory notification should contain at minimum:

```
REGULATORY NOTIFICATION — AI INCIDENT

Institution: [Name, charter type, primary federal regulator]
Date of notification: [ISO8601]
Incident reference: [Internal incident ID]

Summary:
[2–3 sentence plain description of what happened]

Timeline:
- Date incident occurred: [or estimated date range]
- Date institution discovered incident: 
- Date containment actions taken:
- Date of this notification:

Scope:
- Number of consumers affected: [number or range]
- Products/services affected:
- Geographic scope:

Nature of the incident:
[Description of the AI system, what it was doing, and what went wrong]

Consumer harm:
[Specific financial harm, if any — accounts restricted, credit denied, funds impacted]

Actions taken:
[Containment, investigation findings, remediation steps completed and planned]

Consumer remediation:
[How affected consumers are being identified and made whole]

Regulatory question or request:
[What the institution is asking of the regulator, if anything — guidance, examination, etc.]

Contact:
[Name, title, phone, email of institution contact for this notification]
```

---

## Documentation to Preserve for Regulators

Begin preserving these from the moment an incident is identified — do not wait for notification:

- Complete audit log extract for the affected period
- Model Registry entry for the affected model version
- Training data documentation
- Root cause analysis (when complete)
- Scope assessment methodology
- All consumer communications sent
- Remediation plan and timeline
- Internal incident log with all timestamped actions

Regulators may request any of these during examination or in response to a notification. Having them organised and complete before notification significantly reduces examination burden.
