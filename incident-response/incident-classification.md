# Incident Response — Classification and Containment

When an AI system in a financial institution makes a wrong, biased, or a decision with serious consequences, the response must be structured, fast, and documented. This document defines how to classify the severity of an AI incident and how to contain it immediately.

---

## Incident Classification

Not all AI failures are equal. Classification determines the speed and scale of response required.

### Severity Level 1 — Critical
**Definition:** AI system is causing or has caused demonstrable financial harm, fair lending violation, or regulatory breach. Immediate action required.

**Examples:**
- AI credit model is systematically denying applications from a protected class at statistically significant rates
- Fraud detection AI is blocking legitimate transactions for a large number of customers
- KYC AI is incorrectly failing identity verification for customers who should pass, resulting in account opening denial
- AI model is operating outside its validated scope

**Response time:** Contain within 4 hours. Escalate to executive leadership and compliance immediately.

### Severity Level 2 — High
**Definition:** AI system is producing incorrect or potentially biased outputs at a rate that poses material risk, but immediate financial harm is limited or not yet confirmed.

**Examples:**
- Bias monitoring flags a metric above threshold; investigation confirms the disparity is real
- Model confidence scores are systematically lower than calibration suggests
- Human override rate exceeds 30% — reviewers are consistently disagreeing with the model
- Audit log gaps discovered — decisions being made without complete logging

**Response time:** Escalation within 24 hours. Investigation within 5 business days.

### Severity Level 3 — Medium
**Definition:** AI system is underperforming or showing early warning signs. No confirmed consumer harm but risk is elevated.

**Examples:**
- Performance metrics declining trend over three consecutive monitoring periods
- Bias monitoring approaching threshold but not yet crossed
- Isolated complaints from consumers about unexplained adverse decisions
- Vendor notification of known model issue in a third-party AI component

**Response time:** Investigation within 10 business days. Document and monitor.

### Severity Level 4 — Low
**Definition:** Minor operational anomaly with no consumer impact or regulatory risk.

**Examples:**
- Temporary latency spike in model inference
- Individual data quality issue in training pipeline
- Documentation gap identified in model records

**Response time:** Addressed in normal operational cycle within 30 days.

---

## Containment Playbook

### Level 1 — Critical Containment (4 hours)

**Minute 0–15: Assess and confirm**
- Confirm the incident is real and not a data artifact
- Identify the specific model and use case affected
- Estimate the number of consumers potentially affected
- Identify the date range of affected decisions

**Minute 15–60: Execute kill switch**
- Activate the model's kill switch — suspend AI-assisted decisions immediately
- Confirm fallback is operational — decisions continue through rule-based or human review path
- Notify operations team that manual review volume will increase
- Document the time of kill switch activation

**Hour 1–4: Notify**
- Notify Chief Risk Officer and Chief Compliance Officer
- Notify legal counsel
- Assess regulatory notification obligation — see [Regulatory Notification Guide](regulatory-notification-guide.md)
- Begin incident log — every action and decision timestamped

**After containment: Preserve**
- Export and preserve all Audit Log records for the affected period — do not modify
- Preserve the model version that caused the incident — do not overwrite
- Preserve training data and configuration — do not modify

### Level 2 — High Containment (24 hours)

- Reduce model traffic — route a portion of decisions to human review while investigation proceeds
- Notify Compliance Officer
- Begin formal investigation — see [Investigation Protocol](investigation-protocol.md)
- Increase monitoring frequency to daily

### Level 3 and 4 — Standard Response

- Document in the incident log
- Assign to model owner for investigation
- Track to resolution in the next monitoring cycle

---

## Incident Log Structure

Every AI incident — at any severity level — must be documented:

```
INCIDENT LOG ENTRY

Incident ID: [auto-generated]
Date identified: [ISO8601]
Identified by: [name and role]
Model affected: [model ID and version]
Severity classification: [1 / 2 / 3 / 4]
Classification rationale: [why this severity]

Description of the incident:
[Plain language description of what went wrong]

Estimated scope:
- Number of consumers potentially affected: [number or range]
- Date range of affected decisions: [start] to [end]
- Products affected: [list]

Immediate actions taken:
[Timestamped list of every action taken]

Kill switch activated: [Yes / No / Partial]
Kill switch activation time: [ISO8601 if activated]
Fallback operational: [Yes / No]

Regulatory notification required: [Yes / No / Under assessment]
Notification deadline: [if applicable]

Current status: [CONTAINED / UNDER INVESTIGATION / REMEDIATED / CLOSED]
Last updated: [ISO8601]
Updated by: [name]
```
