# Contributing to Fintech AI Governance and Incident Response Framework

This framework exists because AI governance standards in financial services are underdeveloped relative to the speed at which AI is being deployed. Every contribution that improves the framework's practical usefulness for financial institutions — especially smaller institutions with limited compliance resources — is a direct contribution to financial fairness in the United States.

---

## Who Should Contribute

**Compliance and BSA professionals:** Your experience with regulatory examinations, fair lending reviews, and BSA audits is exactly what makes this framework defensible in practice rather than just technically correct. If something in this framework would not survive an examiner's scrutiny, tell us.

**AI and data science practitioners:** If the model validation standards, bias monitoring metrics, or incident classification criteria reflect unrealistic assumptions about how AI systems actually work in production financial environments, correct them.

**Community bank and credit union technologists:** This framework is explicitly designed for institutions with limited engineering resources. If the implementation guidance is too complex, too expensive, or too dependent on infrastructure that smaller institutions do not have, that feedback is critical.

**Legal and regulatory experts:** Regulatory requirements change. If a referenced regulation has been updated, if notification requirements have changed, or if new agency guidance affects this framework's recommendations, please flag it immediately.

---

## What We Welcome

**Additions:**
- New use case examples for institution types not yet covered
- Additional regulatory body guidance for state-level requirements
- International equivalents (FCA, ESMA, MAS, RBI) for global applicability
- Template additions — additional pre-deployment checklists, monitoring dashboards, incident report formats
- Cross-framework integration patterns connecting this framework to other open-source fintech frameworks

**Corrections:**
- Regulatory inaccuracies — flag with the `compliance-correction` label, highest priority
- Technical inaccuracies in model validation or bias monitoring guidance
- Outdated regulatory references

**Improvements:**
- Simplification for smaller institutions — if something requires resources a $500M credit union does not have, suggest the appropriate alternative
- Plain-language rewrites of sections that are too technical for compliance audiences

---

## What We Do Not Accept

- Content that weakens governance requirements without regulatory justification
- Vendor-specific promotional content
- Proprietary or employer-confidential implementation details
- Content that advises institutions to avoid regulatory notification when it is required

---

## How to Contribute

1. **Open an issue first** for any significant addition or change. Describe what you want to add and why. This prevents duplicated effort and allows discussion before implementation.
2. **Fork the repository** and create a branch for your contribution.
3. **Cite your sources.** Every regulatory claim must link to a primary source — CFR, Federal Register notice, or agency guidance document. Do not cite secondary sources for regulatory requirements.
4. **Write for the practitioner.** The audience for this framework is a compliance officer or BSA professional at a community bank, not an academic or a regulator. Plain language, specific examples, and actionable checklists are the standard.
5. **Submit a pull request** with a clear description of what you changed and why.

---

## Reporting Compliance Errors

If you find content that could mislead a financial institution about its regulatory obligations — including outdated notification requirements, incorrect regulatory thresholds, or inaccurate descriptions of agency jurisdiction — open an issue immediately with the label `compliance-correction`.

Compliance errors are treated with the highest priority. An institution acting on incorrect guidance in this framework could face regulatory consequences. If you are uncertain whether something is an error, flag it anyway — we would rather investigate a false alarm than miss a real problem.

---

## Questions

Open an issue with the `question` label. Questions from practitioners at community institutions are especially welcome — your real-world implementation experience is what makes this framework useful rather than theoretical.
