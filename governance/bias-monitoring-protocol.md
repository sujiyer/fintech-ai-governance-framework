# Bias Monitoring Protocol

Bias in AI financial systems is not a deployment problem alone — it is an ongoing operational risk. A model that passes fairness validation at deployment can develop disparate impact over time as population characteristics shift, economic conditions change, or the model is applied to populations it was not trained on. This protocol defines how to monitor AI systems for bias continuously after deployment.

---

## Why Ongoing Monitoring Is Required

**Population drift:** The people applying for credit, opening accounts, or using financial products today may be demographically different from the population the model was trained on. As population characteristics shift, a model's fairness properties can degrade without any change to the model itself.

**Economic condition shift:** A fraud model trained during stable economic conditions may behave differently during a recession. A credit model trained in a low-interest environment may produce systematically different outputs as rates change.

**Usage scope creep:** Models often get applied to use cases beyond their original scope. A KYC identity verification model trained on standard retail accounts may be applied to business accounts without re-validation. Monitoring detects when a model is being used outside its validated scope.

**Compounding errors:** A single biased decision is a problem. A model making thousands of biased decisions per week is a systemic harm. Monitoring catches compounding errors before they become regulatory violations.

---

## Monitoring Metrics by Model Type

### Credit and Access Decision Models

| Metric | Definition | Flag Threshold |
|---|---|---|
| Approval rate disparity | Ratio of approval rates between demographic groups | > 20% disparity between any two groups |
| Denial reason distribution | Are certain denial reason codes applied disproportionately to any group? | > 15% disparity in denial code frequency |
| Confidence score distribution | Are confidence scores systematically lower for any demographic group? | Mean confidence gap > 0.10 between groups |
| Manual review rate | Are some groups sent to manual review more frequently? | > 25% disparity in escalation rate |

### Fraud Detection Models

| Metric | Definition | Flag Threshold |
|---|---|---|
| False positive rate by group | Are legitimate transactions being flagged as fraud at higher rates for some groups? | > 15% disparity in false positive rate |
| Transaction decline rate | Are transactions declined at disproportionate rates for any demographic? | > 20% disparity |
| Geographic concentration | Are fraud flags concentrated in specific geographic areas (proxy for demographic)? | Flag for manual review |

### KYC and Identity Verification Models

| Metric | Definition | Flag Threshold |
|---|---|---|
| Verification pass rate by group | Are some demographic groups passing verification at lower rates? | > 20% disparity |
| Document rejection rate | Are documents from some groups rejected at higher rates? | > 15% disparity |
| Alternative verification trigger rate | Are some groups disproportionately routed to progressive/alternative verification? | > 25% disparity |

---

## Monitoring Cadence

| Model Risk Tier | Minimum Monitoring Frequency | Additional Trigger |
|---|---|---|
| High | Monthly | Any regulatory change, any population shift > 10% |
| Medium | Quarterly | Annual re-validation |
| Low | Semi-annually | Significant change in use case or volume |

---

## Monitoring Process

### Step 1 — Data Collection

At each monitoring interval, extract from the Audit Log:
- All inferences made in the period
- Outcomes associated with those inferences (approvals, denials, flags)
- Confidence scores
- Escalation decisions

Do not use protected class attributes directly. Use proxy analysis — geographic, behavioral, and product-level variables that may correlate with protected characteristics.

### Step 2 — Metric Calculation

Calculate each applicable metric from the table above. Document the calculation methodology — a metric is only defensible if it can be reproduced.

### Step 3 — Threshold Comparison

Compare calculated metrics against the flag thresholds established at validation. Any metric exceeding its threshold requires a formal response — it does not require immediate model shutdown, but it does require documented investigation.

### Step 4 — Trend Analysis

Metrics at a single point in time are less informative than trends. Plot each metric over time. A metric approaching a threshold over three consecutive monitoring periods is a warning sign even if it has not yet crossed the threshold.

### Step 5 — Documentation and Sign-Off

Monitoring results are documented in a Monitoring Report. The model owner reviews and signs off. For High tier models, the compliance officer also signs off. Reports are retained in the Model Registry.

---

## Responding to a Flagged Metric

A flagged metric does not automatically require model shutdown. The response is proportionate to the severity and confirmed nature of the bias.

```
Metric exceeds threshold
        ↓
Level 1 — Initial investigation (5 business days)
  Is the disparity real or a data artifact?
  Is it statistically significant given sample size?
        ↓
  ┌─────────────────┬──────────────────────────────┐
  │ Data artifact   │ Confirmed disparity           │
  │ Document and    │ → Level 2 response            │
  │ close           │                               │
  └─────────────────┴──────────────────────────────┘
        ↓
Level 2 — Escalation (10 business days)
  Notify compliance officer
  Notify fair lending officer (credit models)
  Assess scope: how many people affected?
  Assess severity: what decisions were impacted?
        ↓
Level 3 — Response options
  Recalibrate model thresholds
  Retrain model with corrected data
  Suspend model and revert to fallback
  Notify regulators if required (see Regulatory Notification Guide)
```
