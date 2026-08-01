# Model Validation Standards

These standards define the minimum requirements for validating an AI or machine learning model before it is deployed in a production financial services environment. No model should be deployed without satisfying every requirement in this document.

---

## Validation Principles

**Independence**
Model validation must be performed by a person or team independent of the model development team. The validator must have no stake in the model's approval. For smaller institutions, this may mean using an external validator for high-risk models.

**Documentation before validation**
Validation cannot begin until the model developer has produced complete documentation: purpose, training data, methodology, known limitations, and intended use cases. Undocumented models are not eligible for validation.

**Risk-proportionate depth**
Validation depth is proportionate to model risk. A low-risk model requiring limited validation is not the same as a high-risk model requiring comprehensive validation. Risk tier determines validation requirements.

---

## Model Risk Tiers

| Tier | Definition | Examples | Validation Requirement |
|---|---|---|---|
| **High** | AI makes or directly informs consequential decisions affecting consumer financial access | Credit scoring, loan approval, fraud denial, KYC identity rejection | Full independent validation — all requirements below |
| **Medium** | AI assists human decision-making but does not make final decisions | Research recommendations, risk flagging for human review | Validation of core requirements — marked below |
| **Low** | AI performs internal operational tasks with no direct consumer impact | Document classification, internal routing, data enrichment | Basic validation — model owner sign-off |

---

## Pre-Deployment Validation Checklist

### Section 1 — Documentation (All Tiers)

- [ ] Model purpose statement written in plain language
- [ ] Intended use cases documented
- [ ] Out-of-scope use cases explicitly listed
- [ ] Training data source, date range, and known gaps documented
- [ ] Methodology description — what the model does, not just its accuracy score
- [ ] Known limitations documented honestly
- [ ] Model owner named and accountable

### Section 2 — Data Validation (High and Medium Tiers)

- [ ] Training data reviewed for demographic representation
- [ ] Protected class proxies identified and assessed (zip code, name patterns, device type as proxies for race, ethnicity, gender)
- [ ] Data recency confirmed — training data reflects current population and conditions
- [ ] Data quality audit — missing values, outliers, and anomalies documented
- [ ] Hold-out test set confirmed to be independent of training data

### Section 3 — Performance Validation (All Tiers)

- [ ] Performance metrics defined before validation (not after)
- [ ] Minimum acceptable performance threshold established and documented
- [ ] Performance tested on hold-out data, not training data
- [ ] Performance tested across subgroups — is the model equally accurate for all demographic groups?
- [ ] Performance degradation scenarios identified — under what conditions does this model fail?

### Section 4 — Fairness Validation (High Tier Required, Medium Recommended)

- [ ] Fairness metrics defined — which metrics apply to this model's use case?
  - Demographic parity: similar outcomes across demographic groups
  - Equal opportunity: similar true positive rates across groups
  - Predictive parity: similar precision across groups
- [ ] Fairness thresholds established — what level of disparity is acceptable?
- [ ] Disparate impact analysis completed and documented
- [ ] Results reviewed by compliance or fair lending officer before approval

### Section 5 — Explainability Validation (High Tier Required)

- [ ] Model produces a confidence score for every output
- [ ] Confidence score is calibrated — a 0.80 confidence score is correct approximately 80% of the time
- [ ] Plain-language explanation can be generated for any model decision
- [ ] Key factors driving each decision can be identified and communicated to a non-technical audience
- [ ] "Why this decision?" question answerable with specific, verifiable data points

### Section 6 — Operational Validation (All Tiers)

- [ ] Latency tested — model responds within acceptable time under expected load
- [ ] Kill switch implemented — model can be disabled without a code deployment
- [ ] Fallback defined — what replaces the model if it is disabled?
- [ ] Audit logging implemented — every inference logged per the Audit Trail Specification
- [ ] Human escalation path confirmed — low-confidence outputs route to human review

### Section 7 — Governance Sign-Off (All Tiers)

- [ ] Model risk assessment completed — see [Model Risk Assessment Template](../templates/model-risk-assessment.md)
- [ ] Validator sign-off obtained
- [ ] Compliance officer review completed (High tier)
- [ ] Fair lending officer review completed (High tier — credit and access decisions)
- [ ] Model registered in Model Registry with all documentation attached
- [ ] Deployment approval issued with conditions documented

---

## Post-Approval Conditions

Approval to deploy is not permanent. Conditions may include:

- **Monitoring frequency** — how often bias and performance metrics are reviewed
- **Review trigger events** — conditions that automatically require re-validation (significant performance drop, regulatory change, population shift)
- **Sunset date** — date by which the model must be re-validated or retired
- **Rollout constraints** — percentage of traffic or user population for phased deployment

All conditions are documented in the Model Registry entry and tracked by the model owner.
