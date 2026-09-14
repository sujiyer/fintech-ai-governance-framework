# Containment Playbook

When a Level 1 or Level 2 AI incident is confirmed, the first 24 hours determine how much harm is contained and how much evidence is preserved. This playbook provides the specific steps to execute in that window.

---

## Level 1 Incident Containment — First 4 Hours

### Hour 0 to 15 Minutes: Confirm and Scope

Do not skip this step. Acting on a false alarm wastes resources. Acting on a real incident without scoping it first creates chaos.

**Confirm the incident is real:**
- Is the problem in the AI system or in the data pipeline feeding it?
- Is this a single anomalous event or a pattern?
- Is the monitoring alert accurate or a false positive?

If you cannot confirm within 15 minutes, treat it as real and proceed.

**Scope the incident:**
- Which model is affected?
- Which product or decision type is affected?
- What is the estimated date range of affected decisions?
- Rough estimate of consumers affected?

Write down your answers. Time-stamp them. This is the start of your incident log.

### Hour 15 Minutes to 1 Hour: Kill Switch

**Activate the kill switch:**
- Locate the kill switch documentation for the affected model
- Activate per the documented procedure
- Confirm the model has stopped producing outputs
- Confirm the fallback process is operational
- Time-stamp the kill switch activation

**Do not modify the model or its configuration yet.** Preservation comes before remediation. You need the model exactly as it was for investigation.

**Notify operations:**
- The team handling manual review will see increased volume
- Brief them: expected volume increase, expected duration, any guidance on priority cases

### Hour 1 to 4: Notify and Preserve

**Internal notifications:**
- Chief Risk Officer or equivalent
- Chief Compliance Officer
- Legal counsel
- BSA Officer (if the model touches KYC or transaction monitoring)
- Fair Lending Officer (if the model affects credit or access decisions)

**Preserve evidence immediately:**
- Export all audit log entries for the affected model and the estimated incident period
- Save a copy of the model version, configuration, and thresholds in effect at the time
- Preserve training data metadata
- Do not allow any changes to these artifacts until investigation is complete

---

## Level 2 Incident Containment — First 24 Hours

Level 2 incidents do not require immediate kill switch activation but do require structured response.

**Hours 1 to 4:**
- Confirm the incident and scope it
- Notify model owner and compliance officer
- Increase monitoring cadence to daily for the affected model
- Reduce model traffic: route an increased percentage of decisions to human review

**Hours 4 to 24:**
- Begin formal investigation per the Investigation Protocol
- Document all actions taken with timestamps
- Assess whether the incident may escalate to Level 1

---

## Evidence Preservation Checklist

Complete this checklist before any remediation begins:

- [ ] Audit log exported for the incident period and secured
- [ ] Model version and exact configuration preserved
- [ ] Training data provenance documentation preserved
- [ ] Input data samples from the incident period preserved (hashed, no raw PII)
- [ ] Monitoring data showing when the problem began preserved
- [ ] All communications about the incident logged chronologically

---

---

# Regulatory Notification Guide

Not every AI incident requires regulatory notification. But when it does, the timing and content of notification matter significantly. This guide helps institutions determine when to notify, who to notify, and what to include.

---

## When Notification May Be Required

Regulatory notification for AI incidents is not universally mandated by a single rule. It arises from the intersection of several existing requirements:

**ECOA and Regulation B:** If an AI system has been producing systematically inaccurate or incomplete adverse action reasons, the CFPB and the institution's primary regulator may need to be notified, particularly if remediation requires re-notification to affected consumers.

**Bank Secrecy Act and AML:** If an AI system involved in transaction monitoring or KYC has failed in a way that may have allowed suspicious activity to go undetected or blocked legitimate activity, the BSA officer must assess notification obligations.

**Operational incident reporting:** The OCC, FDIC, and Federal Reserve each have guidance on when operational incidents — including technology incidents — must be reported. Significant AI failures that affect the institution's ability to deliver services or that affect a material number of consumers may fall within these thresholds.

**State banking regulators:** State-chartered institutions may have additional notification obligations under state banking law.

**Cyber incident reporting:** If the AI incident involves a security compromise — an adversarial attack on the model, unauthorized access to training data, or manipulation of AI outputs — CISA's cyber incident reporting requirements may apply.

---

## Decision Tree for Notification Assessment

```
Is this a Level 1 incident?
  YES → Engage legal counsel immediately for notification assessment
  NO  → Continue below

Did the incident produce systematically inaccurate adverse action reasons?
  YES → CFPB and primary regulator notification likely required
       Engage legal counsel
  NO  → Continue below

Did the incident affect a material number of consumers?
  (Material = typically 1,000 or more consumers, but institution-specific)
  YES → Primary regulator notification may be required
       Engage legal counsel
  NO  → Continue below

Did the incident involve a security compromise of AI systems?
  YES → CISA notification may be required under CIRCIA
       Engage legal and security counsel immediately
  NO  → Document incident internally, no external notification likely required
```

---

## Notification Preparation

If legal counsel determines notification is required, prepare:

**1. Incident summary**
- What happened, in plain language
- When it was first detected and when containment occurred
- Estimated number of consumers affected
- Products and decision types affected

**2. Root cause summary**
- What caused the incident
- Why it was not detected sooner
- Whether the cause has been eliminated

**3. Consumer impact assessment**
- What adverse outcomes consumers experienced
- Whether adverse action reasons were inaccurate and require correction
- Whether re-notification to consumers is required

**4. Remediation summary**
- Steps taken to contain the incident
- Steps taken or planned to remediate the root cause
- Changes to governance, monitoring, or deployment practices

**5. Timeline**
- Chronological timeline from first indication to containment to remediation
- All timestamps should come directly from the incident log

---

## Regulatory Contacts

| Regulator | When to Notify | Contact |
|---|---|---|
| CFPB | Adverse action failures; consumer financial harm at scale | consumerfinance.gov/complaint |
| OCC | National bank operational incidents | occ.gov |
| FDIC | State non-member bank incidents | fdic.gov |
| Federal Reserve | State member bank and holding company incidents | federalreserve.gov |
| NCUA | Credit union incidents | ncua.gov |
| CISA | Cyber incidents including AI system compromise | cisa.gov/report |
| State banking regulator | State-chartered institution obligations | Institution-specific |

All regulatory notifications should be reviewed by legal counsel before submission.
