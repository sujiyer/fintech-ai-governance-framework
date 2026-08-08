# Incident Report Template

Copy this template when documenting an AI incident. Complete every field — blank fields are themselves a governance gap. This report is the primary documentation for regulatory examination, internal audit, and model improvement purposes.

---

```
═══════════════════════════════════════════════════════════════
AI INCIDENT REPORT
Fintech AI Governance and Incident Response Framework
═══════════════════════════════════════════════════════════════

SECTION 1 — INCIDENT IDENTIFICATION
──────────────────────────────────────────────────────────────
Incident ID:              [Auto-generated or sequential number]
Report Date:              [ISO8601 date]
Report Prepared By:       [Name and title]
Report Reviewed By:       [Compliance Officer name and date]

SECTION 2 — INCIDENT CLASSIFICATION
──────────────────────────────────────────────────────────────
Severity Level:           [ ] Level 1 — Critical
                          [ ] Level 2 — High
                          [ ] Level 3 — Medium
                          [ ] Level 4 — Low

Classification Rationale:
[Why this severity level — be specific about consumer harm,
 scope, and regulatory risk that informed the classification]

SECTION 3 — AFFECTED AI SYSTEM
──────────────────────────────────────────────────────────────
Model ID:                 [From Model Registry]
Model Version:            [Exact version deployed at time of incident]
Model Risk Tier:          [ ] High   [ ] Medium   [ ] Low
Use Case:                 [What the model was doing]
Framework:                [ ] KYC API Framework
                          [ ] Research Workspace Framework
                          [ ] Reconciliation Break Framework
                          [ ] Other: _______________

Deployment Date:          [When this model version was deployed]
Last Validation Date:     [When this model version was last validated]

SECTION 4 — INCIDENT DESCRIPTION
──────────────────────────────────────────────────────────────
Date Incident Occurred:   [ISO8601 date or estimated range]
Date Discovered:          [ISO8601 date]
Discovered By:            [Role — not individual name for privacy]
How Discovered:           [ ] Monitoring alert
                          [ ] Consumer complaint
                          [ ] Regulatory inquiry
                          [ ] Internal audit
                          [ ] Bias monitoring flag
                          [ ] Other: _______________

Plain Language Description:
[2–4 sentences describing what happened in language that a
 non-technical compliance officer can understand and relay
 to a regulator if needed]

Technical Description:
[More detailed technical explanation of the failure — what
 inputs the model received, what it output, why that was
 wrong, and what evidence confirms the failure]

SECTION 5 — SCOPE ASSESSMENT
──────────────────────────────────────────────────────────────
Date Range of Affected Decisions:
  From: _______________  To: _______________

Estimated Number of Affected Consumers:     _______________
Confirmed Number of Affected Consumers:     _______________
Method Used to Identify Affected Consumers: _______________

Products/Services Affected:
[ ] KYC / Account Opening
[ ] Credit / Loan Decision
[ ] Fraud Detection
[ ] Investment Recommendation
[ ] Sanctions Screening
[ ] Other: _______________

Potential Financial Harm to Consumers:
[ ] None confirmed
[ ] Minimal (< $1,000 aggregate)
[ ] Moderate ($1,000 – $50,000 aggregate)
[ ] Significant ($50,000 – $500,000 aggregate)
[ ] Material (> $500,000 aggregate or unknown)

Description of Harm:
[Specific description — accounts restricted, credit denied,
 funds blocked, etc. Be concrete, not general]

SECTION 6 — CONTAINMENT ACTIONS
──────────────────────────────────────────────────────────────
Kill Switch Activated:    [ ] Yes   [ ] No   [ ] Partial
Activation Timestamp:     _______________
Fallback Operational:     [ ] Yes   [ ] No
Fallback Method:          _______________

Containment Actions Taken (timestamped):
  [Time]: [Action]
  [Time]: [Action]
  [Time]: [Action]

Time from Discovery to Containment: _______________ hours

SECTION 7 — ROOT CAUSE ANALYSIS
──────────────────────────────────────────────────────────────
Root Cause Category:
[ ] Data — training data bias, gaps, or errors
[ ] Model — architecture or calibration failure
[ ] Scope — model applied outside validated use case
[ ] Integration — upstream data or system change
[ ] Drift — population or economic condition shift

Root Cause Description:
[Specific, honest, technical description of what caused
 the failure. Vague descriptions ("model error") are not
 acceptable root cause statements]

Contributing Factors:
[Conditions that allowed the root cause to produce an
 incident — monitoring gap, validation gap, etc.]

Detection Gap:
[Why did monitoring not catch this earlier?
 What would have caught it sooner?]

SECTION 8 — CONSUMER REMEDIATION
──────────────────────────────────────────────────────────────
Affected Consumers Notified:     [ ] Yes  [ ] No  [ ] Partial
Notification Method:             _______________
Notification Date:               _______________

Adverse Decisions Reversed:      [ ] Yes  [ ] No  [ ] Partial
Number of Reversals:             _______________
Financial Remediation Provided:  [ ] Yes  [ ] No  [ ] N/A
Amount of Remediation:           _______________

SECTION 9 — REGULATORY NOTIFICATION
──────────────────────────────────────────────────────────────
Legal Counsel Consulted:         [ ] Yes  [ ] No
Date Consulted:                  _______________

Regulatory Notification Required:
[ ] No — rationale: _______________
[ ] Under assessment — decision deadline: _______________
[ ] Yes — notify the following:

  [ ] CFPB      Notification Date: _______________
  [ ] OCC       Notification Date: _______________
  [ ] FDIC      Notification Date: _______________
  [ ] Fed       Notification Date: _______________
  [ ] NCUA      Notification Date: _______________
  [ ] FinCEN    Notification Date: _______________
  [ ] State: _______________  Date: _______________

SECTION 10 — REMEDIATION PLAN
──────────────────────────────────────────────────────────────
Remediation Actions Completed:
  [ ] Model suspended from production
  [ ] Root cause addressed (describe below)
  [ ] Model retrained / recalibrated
  [ ] Re-validation completed
  [ ] Monitoring protocol updated
  [ ] Validation checklist updated

Root Cause Remediation Description:
[How was the root cause specifically addressed?]

Governance Improvements:
[What changes to validation standards, monitoring protocol,
 or incident detection will prevent recurrence?]

Redeployment Plan:
  Planned re-validation date: _______________
  Compliance officer sign-off obtained: [ ] Yes  [ ] No
  Fair lending officer sign-off (if applicable): [ ] Yes  [ ] No
  Phased rollout plan documented: [ ] Yes  [ ] No

SECTION 11 — INCIDENT CLOSURE
──────────────────────────────────────────────────────────────
Incident Status:
[ ] Open
[ ] Contained — investigation in progress
[ ] Remediated — monitoring in progress
[ ] Closed

Closure Conditions Met:
[ ] Root cause addressed and documented
[ ] Consumer remediation completed
[ ] Regulatory notifications completed
[ ] Governance improvements implemented
[ ] Model redeployed with phased rollout
[ ] 90-day post-redeployment monitoring initiated

Closed By:               _______________
Closed Date:             _______________
Compliance Officer Sign-Off: _______________  Date: _______________

═══════════════════════════════════════════════════════════════
END OF INCIDENT REPORT
═══════════════════════════════════════════════════════════════
```
