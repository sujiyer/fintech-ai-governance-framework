# Pre-Deployment AI Testing Protocol

This protocol defines the specific tests a financial institution must run before any AI system goes into production. It is written for compliance officers and risk managers who may not have a data science background. Every test has a clear pass or fail result. A model that does not pass every required test for its risk tier does not deploy.

---

## How to Use This Protocol

**Step 1:** Identify the model's risk tier using the classification in the Model Validation Standards document.

**Step 2:** Run every test marked as required for that tier. Tests marked "recommended" are strongly encouraged but not blocking.

**Step 3:** Record every test result in the Model Risk Assessment template.

**Step 4:** A qualified reviewer signs off on the results before deployment is approved.

No exceptions. No partial passes.

---

## Test Suite — Section 1: Data Quality Tests

*Required for all tiers.*

These tests verify that the data used to train the model is complete, current, and representative of the population the model will serve.

### Test 1.1 — Training Data Completeness
**What to check:** Count the records in the training dataset. Identify any fields with more than 5% missing values.
**Pass:** No critical field has more than 5% missing values. Critical fields are those used directly in the model's decision.
**Fail:** Any critical field has more than 5% missing values.
**Action on fail:** Impute missing values with a documented methodology or exclude the field and retrain.

### Test 1.2 — Training Data Recency
**What to check:** Identify the date range of records in the training dataset.
**Pass:** The most recent training record is no more than 18 months old for credit and access decision models. No more than 12 months old for fraud detection models.
**Fail:** Training data is older than the required window.
**Action on fail:** Refresh the training dataset before deployment.

### Test 1.3 — Population Representativeness
**What to check:** Compare the demographic distribution of the training dataset against the institution's current customer population and the population the model will serve.
**Pass:** No demographic group present in the intended service population is absent from the training data. No demographic group represents less than 3% of training records if that group represents more than 5% of the service population.
**Fail:** Material underrepresentation of any group in the service population.
**Action on fail:** Augment training data or document the limitation and implement compensating monitoring.

### Test 1.4 — Proxy Variable Identification
**What to check:** Review all input features for variables that may serve as proxies for protected class characteristics.
**Common proxies to check:** Geographic identifiers (zip code, census tract), surname patterns, device type, language preference, session timing patterns.
**Pass:** All identified proxy variables are documented and their inclusion is justified with evidence that they do not introduce disparate impact.
**Fail:** Proxy variables are present but not documented or justified.
**Action on fail:** Remove proxy variables or document their necessity and implement monitoring.

---

## Test Suite — Section 2: Performance Tests

*Required for all tiers.*

### Test 2.1 — Accuracy on Hold-Out Data
**What to check:** Run the model on a test dataset that was not used in training. Measure accuracy, precision, recall, and F1 score as appropriate to the model type.
**Pass:** Performance meets or exceeds the minimum thresholds established before testing began. Thresholds must be documented in advance — not set after seeing results.
**Fail:** Performance falls below pre-established thresholds.
**Action on fail:** Investigate underperformance. Retrain or adjust model before deployment.

### Test 2.2 — Performance Under Stress Conditions
**What to check:** Test the model on edge cases and adversarial inputs — thin-file applicants, unusual transaction patterns, ambiguous document types, applicants from underrepresented geographic areas.
**Pass:** Model does not produce significantly degraded or erratic outputs on stress inputs. Degraded outputs are flagged for human review rather than resulting in automatic adverse decisions.
**Fail:** Model produces confident outputs on stress inputs that contradict expected behavior.
**Action on fail:** Add stress inputs to training data or implement hard rules to catch these cases.

### Test 2.3 — Confidence Calibration
**What to check:** Compare the model's expressed confidence scores against actual outcome accuracy. A model that says it is 80% confident should be correct approximately 80% of the time.
**Pass:** Confidence scores are calibrated within 10 percentage points of actual accuracy across deciles.
**Fail:** Confidence scores are systematically overconfident or underconfident.
**Action on fail:** Apply calibration techniques before deployment. Adjust human review thresholds accordingly.

### Test 2.4 — Latency Under Load
**What to check:** Run the model at 150% of expected peak transaction volume. Measure response time.
**Pass:** Response time stays within acceptable limits at peak load. For synchronous consumer-facing decisions, this means under 3 seconds at the 95th percentile.
**Fail:** Latency exceeds acceptable limits under load.
**Action on fail:** Optimize model serving infrastructure before deployment.

---

## Test Suite — Section 3: Fairness Tests

*Required for High-tier models. Recommended for Medium-tier.*

### Test 3.1 — Demographic Parity Check
**What to check:** Run the model on test data segmented by demographic group (using proxy analysis, not direct protected class data). Compare approval rates, denial rates, and escalation rates across groups.
**Pass:** No demographic group has an approval rate more than 20 percentage points below the overall average for models making access decisions.
**Fail:** Any group falls more than 20 percentage points below the average.
**Action on fail:** Investigate the source of disparity. Adjust model or thresholds before deployment.

### Test 3.2 — Equal Opportunity Check
**What to check:** Among qualified applicants (those who would be approved by a manual review), compare the model's approval rate across demographic groups.
**Pass:** The model approves qualified applicants at similar rates regardless of demographic group. Disparity of less than 15 percentage points is acceptable.
**Fail:** The model systematically misclassifies qualified applicants from a specific demographic group.
**Action on fail:** This is a significant finding. Retrain or apply threshold adjustments with documented justification.

### Test 3.3 — Adverse Action Reason Review
**What to check:** For a sample of model-generated adverse decisions, verify that the adverse action reason codes accurately describe why the model declined or escalated the application.
**Pass:** Reason codes are accurate and specific for 95% or more of sampled adverse decisions.
**Fail:** Reason codes are generic, inaccurate, or inconsistent with the actual model factors.
**Action on fail:** Fix the adverse action explanation logic before deployment. This is a regulatory requirement under ECOA.

---

## Test Suite — Section 4: Governance Readiness Tests

*Required for all tiers.*

### Test 4.1 — Kill Switch Verification
**What to check:** Activate the model's kill switch in a staging environment. Verify that the model stops producing outputs and that the fallback process activates correctly.
**Pass:** Kill switch disables the model within 60 seconds without requiring a code deployment. Fallback is operational.
**Fail:** Kill switch requires engineering involvement or fallback does not activate.
**Action on fail:** Fix the kill switch before deployment.

### Test 4.2 — Audit Logging Verification
**What to check:** Run 100 test inferences and verify that all 100 are logged to the audit trail with the required fields per the Audit Trail Specification.
**Pass:** 100% of inferences are logged. No required fields are missing.
**Fail:** Any inference is not logged or any required field is missing.
**Action on fail:** Fix audit logging before deployment.

### Test 4.3 — Human Escalation Path Test
**What to check:** Submit 20 test inputs designed to produce low-confidence outputs. Verify that all 20 are routed to the human review queue rather than auto-decided.
**Pass:** All 20 low-confidence inputs are escalated. Human review queue receives them with complete information.
**Fail:** Any low-confidence input is auto-decided or the human review queue does not receive complete information.
**Action on fail:** Fix escalation routing before deployment.

---

## Pre-Deployment Sign-Off

Before any model deploys to production, the following sign-offs are required:

| Tier | Required Sign-Offs |
|---|---|
| High | Model owner, independent validator, compliance officer, fair lending officer |
| Medium | Model owner, compliance officer |
| Low | Model owner |

Sign-off means: "I have reviewed the test results for this model and confirm they meet the required standards for the model's risk tier."

Sign-off must be documented with name, title, date, and the model version being approved. It must be stored in the Model Registry.
