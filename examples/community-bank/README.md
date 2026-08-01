# Example: Community Bank AI Governance Program

**Profile:** Community bank, $3.2B assets, serving a mixed urban/rural area including a significant first-generation banking population. The bank has deployed three AI systems: a KYC identity verification model, a fraud detection model for debit card transactions, and a loan pre-qualification model.

**Starting point:** No formal AI governance program. Models were deployed by the technology team with performance testing but no fairness validation, no bias monitoring, and no documented incident response plan.

---

## Governance Program Setup — 90 Days

### Days 1–30: Inventory and Risk Tier Classification

The compliance officer and technology lead jointly inventoried all AI systems in production:

| Model | Use Case | Risk Tier | Rationale |
|---|---|---|---|
| KYC Identity Verification | Account opening — identity check | High | Directly affects consumer access to financial services |
| Fraud Detection | Debit card transaction flagging | High | False positives directly block consumer access to their funds |
| Loan Pre-Qualification | Initial pre-qualification indicator | Medium | Assists human underwriter; does not make final decision |

### Days 30–60: Retroactive Validation

The bank commissioned retroactive validation of all three models by an independent third-party validator. Key findings:

**KYC Model:** Passed performance validation. Fairness review found the verification pass rate for applicants with non-standard address histories (proxy for recent immigrants and people experiencing housing instability) was 18 percentage points lower than the general population. This was below the 20% flag threshold — but close enough to require increased monitoring.

**Fraud Model:** False positive rate (legitimate transactions flagged as fraud) was 4.2% for transactions at international money transfer businesses — significantly higher than the 1.1% overall rate. The bank's service area includes a large immigrant population that uses these services frequently. This was flagged as a Level 2 incident and investigated.

**Loan Pre-Qualification:** Passed validation. Confidence scores well-calibrated. Human override rate 11% — within acceptable range.

### Days 60–90: Monitoring and Response Implementation

- Bias monitoring dashboards deployed for all three models
- Audit logging implemented to the Audit Trail Specification
- Incident response plan documented and distributed to compliance, technology, and operations
- Monthly monitoring schedule established for High-tier models
- Loan pre-qualification model on quarterly monitoring

---

## Fraud Model Incident Response — Worked Example

The retroactive validation finding on the fraud model was treated as a Level 2 incident.

**Investigation findings:** The model had been trained predominantly on fraud patterns from suburban retail transactions. International money transfer transactions were underrepresented in the training data — the model had learned that these transaction types were associated with fraud (because when they did appear in training data, they were often from compromised accounts) rather than learning the legitimate use pattern.

**Scope assessment:** Approximately 340 legitimate transactions had been declined over a 6-month period. The majority were from a specific demographic segment of the bank's customer base.

**Remediation:**
- Model retrained with corrected training data including legitimate international money transfer transaction patterns
- Fairness validation completed on new model version
- 340 affected customers identified and contacted with apology and account credit
- Retroactive reversal of late fees where applicable

**What changed in governance:**
- Training data review now explicitly requires assessment of transaction type representation
- International money transfer transactions added as a monitored subgroup in bias monitoring
- Customer complaint monitoring now feeds into AI incident detection — several complaints about declined transactions preceded the formal detection

---

## 12-Month Outcomes

After 12 months of operating the governance program:

- KYC model fairness gap reduced from 18 to 9 percentage points following threshold recalibration
- Fraud model false positive rate for international money transfer transactions reduced to 1.4% (from 4.2%)
- No Level 1 incidents
- One Level 2 incident (the fraud model issue above) — contained and remediated within the protocol timeline
- BSA examination: examiners reviewed AI governance documentation and found the bank's program to be more developed than peer institutions of similar size
