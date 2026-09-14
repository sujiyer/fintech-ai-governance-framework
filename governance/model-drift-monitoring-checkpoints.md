# Model Drift Monitoring Checkpoints

A model that passes pre-deployment testing does not stay valid indefinitely. The real world changes. Customer populations shift. Economic conditions move. The data a model was trained on becomes less representative of the data it encounters in production. This is called model drift, and it is one of the most common and least-monitored sources of AI failure in financial services.

This document defines named, schedulable monitoring checkpoints that catch model drift before it causes harm to consumers or creates regulatory exposure. Each checkpoint has a specific trigger, a measurable test, and a defined escalation path.

---

## Why Scheduled Checkpoints Matter

Ad-hoc monitoring — checking a model only when someone notices something wrong — catches problems after consumers have already been harmed. Scheduled checkpoints catch problems at a defined frequency regardless of whether anyone has noticed a problem yet.

Your monitoring calendar for each production AI model should have these checkpoints scheduled from the day of deployment. They do not require a data science team to run. They require data access and someone who can compare numbers against thresholds.

---

## Checkpoint 1 — Data Distribution Check

**Schedule:** Monthly for High-tier models. Quarterly for Medium-tier.

**What it checks:** Whether the inputs arriving at the model in production look like the inputs the model was trained on. If the real-world data has shifted away from the training distribution, the model's predictions may be less reliable.

**How to run it:**
For each key input variable, compare:
- The mean and standard deviation of values in the training dataset
- The mean and standard deviation of values in the past month of production data

**Pass threshold:** No key variable has shifted by more than 2 standard deviations from its training distribution mean.

**Flag threshold:** Any key variable has shifted by more than 2 standard deviations.

**Escalation on flag:** Notify model owner. Investigate whether the shift reflects a real population change (acceptable but requires documentation) or a data pipeline problem (requires immediate fix).

---

## Checkpoint 2 — Prediction Confidence Distribution Check

**Schedule:** Monthly for High-tier. Quarterly for Medium-tier.

**What it checks:** Whether the model's confidence scores are staying in the same range they were during testing. A model that was producing confidence scores averaging 0.82 at deployment but is now averaging 0.68 has changed its behavior.

**How to run it:**
Calculate the mean and 10th percentile of confidence scores for the past month. Compare against the baseline established during pre-deployment testing.

**Pass threshold:** Mean confidence score within 10 percentage points of deployment baseline. 10th percentile confidence within 15 percentage points of deployment baseline.

**Flag threshold:** Mean confidence drops more than 10 percentage points from baseline.

**Escalation on flag:** Notify model owner. A significant drop in confidence often means the model is encountering inputs it was not prepared for. Investigate input data before escalating to model retraining.

---

## Checkpoint 3 — Outcome Accuracy Check

**Schedule:** Quarterly for all tiers where outcomes are observable.

**What it checks:** Whether the model's decisions are proving correct based on observable outcomes. For a credit model, this means tracking whether applicants who were approved are actually repaying. For a fraud model, this means tracking whether flagged transactions were confirmed as fraudulent.

**How to run it:**
Sample approved credit applications from three to six months ago. Calculate the delinquency rate among model-approved applicants and compare against the expected rate established at deployment. For fraud models, calculate the confirmed fraud rate among flagged transactions.

**Pass threshold:** Outcome accuracy within 15% relative change from deployment baseline.

**Flag threshold:** Outcome accuracy has degraded by more than 15% relative to baseline.

**Escalation on flag:** This is a significant finding. Notify model owner and compliance officer. Investigate whether training data no longer reflects current population behavior. Consider retraining with more recent data.

---

## Checkpoint 4 — Fairness Drift Check

**Schedule:** Quarterly for High-tier models. Semi-annually for Medium-tier.

**What it checks:** Whether the model's fairness properties have changed since deployment. A model can pass fairness testing at deployment and develop disparate impact over time as population mix changes.

**How to run it:**
Rerun the demographic parity and equal opportunity checks from the pre-deployment testing protocol using the past quarter's production decisions. Compare results against deployment baseline.

**Pass threshold:** No demographic group's approval rate has shifted more than 10 percentage points relative to its rate at deployment.

**Flag threshold:** Any demographic group's approval rate has shifted more than 10 percentage points.

**Escalation on flag:** Notify model owner, compliance officer, and fair lending officer. Investigate before the next scheduled check. Do not wait for the next quarterly cycle.

---

## Checkpoint 5 — Human Override Rate Check

**Schedule:** Monthly for all tiers.

**What it checks:** Whether human reviewers are frequently overriding the model's recommendations. A high override rate is a signal that the model's outputs are diverging from what reviewers consider correct.

**How to run it:**
Calculate the percentage of model-recommended decisions that were changed by a human reviewer in the past month.

**Pass threshold:** Override rate below 20%.

**Flag threshold — elevated:** Override rate 20% to 30%.

**Flag threshold — critical:** Override rate above 30%.

**Escalation on elevated flag:** Notify model owner. Convene a review with the human reviewers to understand what is driving the overrides. Document findings.

**Escalation on critical flag:** Notify model owner and compliance officer. Consider suspending model pending investigation. Override rates above 30% suggest the model is no longer aligned with institutional judgment.

---

## Checkpoint 6 — Training Data Staleness Check

**Schedule:** Semi-annually for all tiers.

**What it checks:** Whether the training data is becoming outdated relative to the current environment. This is different from the data distribution check — it assesses whether the time since training is long enough to warrant retraining regardless of observed drift.

**Thresholds by model type:**

| Model Type | Retraining Recommended | Retraining Required |
|---|---|---|
| Fraud detection | 12 months | 18 months |
| Credit scoring | 18 months | 24 months |
| KYC identity | 12 months | 18 months |
| Research / recommendation | 6 months | 12 months |

**Escalation:** When retraining is recommended, notify model owner and schedule retraining within the next quarter. When retraining is required, suspend deployment pending retraining unless a business exception is approved and documented by the compliance officer.

---

## Monitoring Calendar Template

For each production AI model, maintain a monitoring calendar with these checkpoints scheduled:

```
**_Model: [Model ID and Name]
Deployed: [Date]
Risk Tier: [High / Medium / Low]

Monthly checkpoints (1st week of each month):
  □ Data Distribution Check
  □ Prediction Confidence Distribution Check
  □ Human Override Rate Check

Quarterly checkpoints (1st month of each quarter):
  □ Outcome Accuracy Check
  □ Fairness Drift Check

Semi-annual checkpoints (January and July):
  □ Training Data Staleness Check

Annual:
  □ Full model re-validation per Model Validation Standards_**
```

The monitoring calendar is stored in the Model Registry alongside the model documentation. Completion of each checkpoint is logged with date, results, and any flags raised.

---

## When Drift Becomes an Incident

If three or more checkpoints flag in the same quarter for the same model, treat this as a Level 2 incident under the Incident Response framework regardless of whether individual flags would each be treated as lower severity. Multiple simultaneous drift signals in a single model indicate a systemic problem that requires formal investigation, not routine monitoring responses.
