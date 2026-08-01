# Investigation Protocol and Remediation Checklist

---

## Investigation Protocol

The investigation answers three questions: What happened? Why did it happen? Who was affected?

### Phase 1 — Reconstruct the Incident (Days 1–3)

**What happened:**
- Pull the complete Audit Log for the affected model and time period
- Reconstruct every decision made — what input the model received, what it output, what confidence score it produced
- Identify the exact point where outputs diverged from expected behaviour
- Map the divergence to a specific model version, training data batch, or configuration change

**Key data to extract from the Audit Log:**
```
- Decision ID
- Timestamp
- Input features (hashed)
- Model version
- Output and confidence score
- Key factors driving the decision
- Human escalation decision (if any)
- Consumer notification sent (if any)
```

**Why it happened:**
Investigate these causes in order:

1. **Data cause** — did the training data contain bias, gaps, or errors that produced this outcome?
2. **Model cause** — is the model architecture or calibration producing systematic errors?
3. **Scope cause** — was the model applied to a population or use case outside its validated scope?
4. **Integration cause** — did a change in upstream data, a connected system, or infrastructure affect model inputs?
5. **Drift cause** — has the real-world population changed in ways the model was not prepared for?

### Phase 2 — Scope Assessment (Days 3–5)

Determine who was affected and to what extent:

- Total number of decisions made by the affected model in the incident period
- Number of decisions that appear incorrect or biased based on investigation findings
- Demographic breakdown of affected decisions (using proxy analysis, not direct protected class data)
- Financial impact — what products, accounts, or transactions were affected?
- Can affected consumers be identified? Can decisions be reversed?

### Phase 3 — Root Cause Documentation (Days 5–7)

Write the root cause analysis:

```
ROOT CAUSE ANALYSIS

Incident ID: [reference]
Root cause category: DATA | MODEL | SCOPE | INTEGRATION | DRIFT

Root cause description:
[Specific, technical, honest description of what caused the failure]

Contributing factors:
[List of conditions that allowed the root cause to produce an incident]

Detection gap:
[Why did this incident occur before monitoring detected it?
What monitoring improvement would have caught it earlier?]

Scope of impact:
[Confirmed number of affected consumers and decisions]

Reversibility:
[Can affected decisions be reviewed and reversed? Process for doing so.]
```

---

## Remediation Checklist

Remediation is the process of fixing the underlying cause and preventing recurrence. It must be completed before the affected model is redeployed.

### Immediate Remediation

- [ ] Affected consumers identified and notified where required (see Regulatory Notification Guide)
- [ ] Adverse decisions subject to reversal reviewed and corrected where warranted
- [ ] Affected model removed from production — not paused, removed
- [ ] Fallback confirmed to be operating correctly

### Root Cause Remediation

**If data cause:**
- [ ] Biased or erroneous training data identified and isolated
- [ ] Corrected dataset prepared
- [ ] Data quality controls updated to prevent same data issue recurring
- [ ] Corrected dataset validated independently before use in retraining

**If model cause:**
- [ ] Model architecture or calibration issue identified specifically
- [ ] Model retrained or recalibrated with corrected approach
- [ ] New model version validated fully per Model Validation Standards
- [ ] Fairness metrics re-run on new version before redeployment

**If scope cause:**
- [ ] Use cases outside validated scope identified and stopped
- [ ] Model scope documentation updated explicitly
- [ ] Deployment controls implemented to prevent out-of-scope application

**If integration cause:**
- [ ] Upstream change that caused the issue identified
- [ ] Integration contract updated to protect against the change
- [ ] Monitoring added to detect future upstream changes

**If drift cause:**
- [ ] Population or economic shift quantified
- [ ] Model retrained on data reflecting current conditions
- [ ] Monitoring cadence increased to catch drift earlier

### Governance Remediation

- [ ] Model Registry updated with full incident documentation
- [ ] Validation Standards updated if this incident revealed a gap
- [ ] Bias Monitoring Protocol updated if this incident was not caught by monitoring
- [ ] Model Validation checklist updated if this incident could have been caught at validation
- [ ] Team debrief completed — what did we learn?

### Redeployment Gate

Before the remediated model is redeployed to production:

- [ ] Full re-validation completed per Model Validation Standards
- [ ] Compliance officer sign-off obtained
- [ ] Fair lending officer sign-off obtained (if credit or access decision model)
- [ ] Phased rollout plan documented — not immediate full deployment
- [ ] Increased monitoring cadence confirmed for first 90 days post-redeployment
- [ ] Incident closed formally in incident log

---

## Regulatory Notification Guide Summary

*(Full guide in [regulatory-notification-guide.md](regulatory-notification-guide.md))*

**When notification may be required:**
- Evidence of systematic fair lending violation (ECOA, FHA, CFPB)
- Consumer financial harm above materiality threshold
- Cybersecurity incident component (if AI was compromised)
- Operational incident reportable under bank regulatory requirements

**Key regulatory contacts:**
- CFPB: Consumer financial protection violations
- OCC / FDIC / Federal Reserve: For bank-regulated institutions
- NCUA: For credit unions
- State banking regulators: For state-chartered institutions

**Documentation to prepare for regulatory response:**
- Complete incident log from identification through remediation
- Root cause analysis
- Scope assessment — number of consumers affected
- Remediation steps taken
- Monitoring improvements implemented

Regulatory notification decisions must involve legal counsel. This framework provides the documentation structure; the notification decision itself is a legal determination.
