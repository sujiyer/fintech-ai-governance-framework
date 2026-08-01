# Explainability Requirements

Explainability in AI financial systems is not a technical feature — it is a consumer right and a regulatory expectation. When an AI system makes or informs a decision about a person's financial access, that person is entitled to understand why. This document defines what "explainable" means in practice for financial services AI.

---

## The Three Levels of Explainability

### Level 1 — System-Level Explainability
*What does this AI system do and how does it make decisions in general?*

Required for: All AI systems in production
Audience: Regulators, auditors, compliance officers
Format: Model documentation, model card

Example: "This system evaluates KYC identity verification requests using a combination of document authenticity scoring, identity data matching, and sanctions screening. Decisions below 0.75 confidence are routed to human review."

### Level 2 — Decision-Level Explainability
*Why did this specific decision happen?*

Required for: All High-tier models; recommended for Medium-tier
Audience: Compliance officers, human reviewers, internal audit
Format: Structured audit log entry with key factors

Example: "Application ID 8834 was escalated to manual review because: identity confidence score 0.61 (below 0.75 threshold); address could not be verified against provided documentation; sanctions screening returned one partial name match requiring human review."

### Level 3 — Consumer-Level Explainability
*Why did this decision happen, explained to the person it affected?*

Required for: All adverse consumer-facing decisions (denial, restriction, escalation)
Audience: The affected consumer
Format: Plain-language explanation, no jargon, specific reasons

Example: "We were unable to verify your identity automatically. This happened because we could not confirm that the address on your ID matches your provided address. You can update your address or upload a recent utility bill to complete verification."

---

## Plain-Language Explanation Standards

Consumer-facing explanations must meet these standards:

**Specific, not generic**
Not acceptable: "Your application was not approved based on our review."
Acceptable: "Your application was not approved because your credit score did not meet the minimum threshold for this product. Your score was [X]; the minimum required is [Y]."

**Actionable where possible**
Where the consumer can take action to change the outcome, that action must be clearly stated. If no action is available, the explanation must clearly state that and provide alternative options.

**Jargon-free**
No technical model terminology. "Confidence score," "threshold," "model output" — none of these should appear in a consumer explanation. Translate every technical concept into plain language.

**Reading level appropriate**
Consumer explanations should target a reading level accessible to a general audience. Avoid complex sentence structures and multi-clause sentences.

---

## The "Why This and Not That" Standard

For AI systems that select between options — recommending one product over another, ranking securities, choosing one verification path over another — the explanation must be able to answer the "why this and not that" question specifically.

**Not acceptable:** "Alphabet was recommended based on your strategy parameters."

**Acceptable:** "Alphabet was recommended over Tesla because it ranked higher on four of your five strategy criteria: momentum score (+8.3% vs -4.2%), forward P/E (23x vs 67x), analyst upgrades in the past 30 days (5 vs 2), and 30-day volatility (18% vs 42%, which exceeds your configured risk threshold of 30%). On earnings surprise, Tesla outperformed."

The explanation must cite specific, verifiable data points — not summarise a reasoning process the recipient cannot see.

---

## Explainability and Audit Logging

Every AI decision that requires Level 2 or Level 3 explainability must generate an audit log entry containing:

```json
{
  "decision_id": "uuid",
  "model_id": "string",
  "model_version": "string",
  "decision_type": "APPROVE | DENY | ESCALATE | RECOMMEND | FLAG",
  "confidence_score": "float",
  "key_factors": [
    {
      "factor_name": "string",
      "factor_value": "string",
      "factor_direction": "POSITIVE | NEGATIVE | NEUTRAL",
      "factor_weight": "float"
    }
  ],
  "consumer_explanation": "string — plain language",
  "internal_explanation": "string — technical detail",
  "alternative_considered": "string or null",
  "human_escalated": "boolean",
  "timestamp": "ISO8601"
}
```

The `key_factors` array is the foundation of both Level 2 and Level 3 explanations. It must be populated for every decision — not generated retroactively when a customer asks.
