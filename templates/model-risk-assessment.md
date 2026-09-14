# Model Risk Assessment Template

Complete this template for every AI model before pre-deployment validation begins. The completed template, together with pre-deployment test results, forms the documentation package required for deployment approval.

---

```
MODEL RISK ASSESSMENT

Date completed: _______________
Completed by: _______________  Title: _______________
Model ID (assigned by Model Registry): _______________

---

SECTION 1: MODEL IDENTIFICATION

Model name: _______________
Model version: _______________
Vendor (if third-party) or internal team (if built in-house): _______________
Date model was developed or last updated: _______________

---

SECTION 2: PURPOSE AND USE

What does this model do? (Plain language, one paragraph):




What decisions does it make or assist with?
  [ ] Credit approval or denial
  [ ] Identity verification
  [ ] Fraud detection or transaction flagging
  [ ] Investment recommendation
  [ ] Research synthesis or summarization
  [ ] Internal workflow routing
  [ ] Other: _______________

Which consumers or users are affected by this model's outputs?




What product or service does it support?




---

SECTION 3: RISK TIER CLASSIFICATION

Answer each question. Circle your answer.

Does this model make or directly inform decisions that affect consumer access
to a financial product or service?                                    YES / NO

Could an error by this model cause direct financial harm to a consumer?
                                                                      YES / NO

Does this model operate without a human reviewing its outputs before
they affect a consumer?                                               YES / NO

If you answered YES to any of the above, this model is HIGH RISK.

Does this model assist a human decision-maker but not replace them?   YES / NO

Could an error cause operational problems but not direct consumer harm?
                                                                      YES / NO

If you answered YES to either of the above and NO to all HIGH RISK questions,
this model is MEDIUM RISK.

If this model only affects internal operations with no consumer impact,
it is LOW RISK.

ASSIGNED RISK TIER: _______________

---

SECTION 4: DATA

What data was used to train this model?
Source: _______________
Date range of training data: _______________ to _______________
Approximate number of records: _______________

Is the training data representative of the population this model will serve?
  [ ] Yes — documentation attached
  [ ] No — explain: _______________
  [ ] Unknown — note this as a gap

Are there known gaps, biases, or limitations in the training data?




---

SECTION 5: KNOWN LIMITATIONS

What are the known failure modes of this model?




In what circumstances is this model known to perform less accurately?




What populations or scenarios is this model not appropriate for?




---

SECTION 6: GOVERNANCE CONTROLS

Is there a kill switch that disables this model without requiring a code deployment?
  [ ] Yes — describe: _______________
  [ ] No — this must be implemented before deployment

Is there a fallback process that operates when this model is disabled?
  [ ] Yes — describe: _______________
  [ ] No — this must be defined before deployment

Is audit logging implemented per the Audit Trail Specification?
  [ ] Yes — tested and confirmed
  [ ] No — this must be implemented before deployment

Is there a defined human review process for low-confidence outputs?
  [ ] Yes — describe: _______________
  [ ] No — this must be defined before deployment

---

SECTION 7: ASSIGNED MODEL OWNER

Name: _______________
Title: _______________
Department: _______________
Contact: _______________

The model owner is the named individual responsible for:
- Ensuring pre-deployment testing is completed
- Ensuring ongoing monitoring is conducted per schedule
- Responding to incidents involving this model
- Maintaining the accuracy of this document

---

SECTION 8: SIGN-OFF

Pre-deployment testing completed: [ ] Yes  [ ] No
Test results attached: [ ] Yes  [ ] No
All required governance controls confirmed: [ ] Yes  [ ] No

Model Owner sign-off:
Name: _______________  Date: _______________  Signature: _______________

Compliance Officer sign-off (required for High and Medium tier):
Name: _______________  Date: _______________  Signature: _______________

Fair Lending Officer sign-off (required for High tier credit models):
Name: _______________  Date: _______________  Signature: _______________

Independent Validator sign-off (required for High tier):
Name: _______________  Date: _______________  Signature: _______________

DEPLOYMENT APPROVED: [ ] Yes  [ ] No  [ ] Conditional (conditions listed below)

Conditions for deployment (if conditional approval):




---

This completed form must be filed in the Model Registry before deployment.
Retain for a minimum of five years after the model is retired from production.
```
