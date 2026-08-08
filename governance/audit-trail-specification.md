# Audit Trail Specification

Every AI-assisted decision in a financial institution must leave a complete, tamper-proof record. This specification defines the minimum audit logging standard for all AI systems governed under this framework.

---

## Why Audit Trails Are Non-Negotiable

**Regulatory examination readiness:** BSA, ECOA, CFPB, and fair lending examinations require institutions to reconstruct specific decisions. An examiner asking "why was this application denied?" must receive a complete, timestamped answer from the audit record alone — not from the memory of the analyst who reviewed it.

**Incident investigation:** When an AI incident occurs, the audit trail is the primary evidence source. Without it, investigation is guesswork. With it, the exact inputs, model version, confidence score, and decision rationale for every affected case are reconstructable.

**Consumer rights:** ECOA and FCRA give consumers the right to understand adverse decisions. That right is only fulfillable if the decision was logged completely at the moment it was made — not reconstructed after the fact.

---

## Audit Log Entry Schema

Every AI inference must produce an audit log entry. The entry is written at the moment of decision — not batched, not delayed.

```json
{
  "log_entry_id": "uuid — system generated, globally unique",
  "institution_id": "uuid — identifies the institution",
  "model_id": "string — matches Model Registry entry",
  "model_version": "string — exact version deployed at time of inference",
  
  "decision": {
    "decision_id": "uuid",
    "decision_type": "APPROVE | DENY | ESCALATE | FLAG | RECOMMEND | RESTRICT",
    "decision_timestamp": "ISO8601 datetime — when the decision was made",
    "decision_by": "AI | HUMAN_AFTER_AI | HUMAN_OVERRIDE"
  },
  
  "subject": {
    "subject_reference": "string — internal reference ID (never PII in log)",
    "product_type": "string — product or service the decision relates to",
    "channel": "WEB | MOBILE | BRANCH | API"
  },
  
  "model_output": {
    "raw_output": "string or object — model's direct output",
    "confidence_score": "float 0.0–1.0",
    "threshold_applied": "float — confidence threshold at time of decision",
    "below_threshold": "boolean — true if confidence < threshold"
  },
  
  "key_factors": [
    {
      "factor_name": "string — name of the factor",
      "factor_value": "string — value used (no raw PII)",
      "factor_direction": "POSITIVE | NEGATIVE | NEUTRAL",
      "factor_weight": "float — relative importance 0.0–1.0"
    }
  ],
  
  "escalation": {
    "escalated_to_human": "boolean",
    "escalation_reason": "LOW_CONFIDENCE | SANCTIONS_FLAG | POLICY_RULE | MANUAL_REQUEST | null",
    "human_reviewer_id": "string or null",
    "human_decision": "CONFIRMED | OVERRIDDEN | PENDING | null",
    "human_decision_timestamp": "ISO8601 datetime or null",
    "override_rationale": "string or null"
  },
  
  "explanations": {
    "internal_explanation": "string — technical detail for compliance review",
    "consumer_explanation": "string — plain language for adverse action notice",
    "explanation_language": "ISO 639-1 language code"
  },
  
  "regulatory": {
    "adverse_action_required": "boolean",
    "adverse_action_sent": "boolean",
    "adverse_action_timestamp": "ISO8601 datetime or null",
    "ecoa_applicable": "boolean",
    "fcra_applicable": "boolean"
  },
  
  "metadata": {
    "session_id": "string",
    "api_version": "string",
    "environment": "PRODUCTION | STAGING",
    "log_schema_version": "string"
  }
}
```

---

## Immutability Requirements

The audit log must be append-only. No entry may be modified or deleted after creation.

**Implementation options:**
- Database table with INSERT-only permissions — no UPDATE or DELETE granted to any application service account
- Write-once object storage (AWS S3 Object Lock, Azure Immutable Blob Storage)
- Blockchain-anchored logging for highest-assurance environments

**Correction policy:** If a logged entry contains an error, a correction entry is written with a reference to the original entry ID. The original entry is never modified.

---

## Retention Requirements

| Log Type | Minimum Retention | Regulatory Basis |
|---|---|---|
| Credit decision logs | 25 months from decision date | ECOA / Regulation B |
| KYC / CIP verification logs | 5 years from account closure | BSA |
| Fraud decision logs | 5 years | BSA |
| Investment recommendation logs | 6 years | FINRA Rule 4511 |
| Adverse action logs | 25 months | ECOA / Regulation B |
| Human override records | 5 years | BSA / examination readiness |

Retain longer where state law or institution policy requires it. When in doubt, retain for 7 years as a conservative default.

---

## Audit Log Access Controls

| Role | Access Level |
|---|---|
| AI Model System | Write only — can create entries, cannot read or modify |
| Compliance Officer | Read — full access for examination preparation |
| Internal Audit | Read — full access |
| BSA Officer | Read — full access |
| Human Reviewer | Read — limited to their own review queue entries |
| Application Engineers | No access — engineers cannot read production audit logs |
| Regulators | Read — provided via controlled extract, not direct access |

---

## Cross-Framework Application

This audit trail specification applies across all frameworks in this ecosystem:

- **KYC API Framework** — every identity verification decision, progressive verification trigger, and sanctions screening result is logged per this specification
- **Research Workspace Framework** — every AI Research Assistant inference, confidence score, and human override is logged per this specification
- **Fintech AI Governance Framework** — this specification is the audit foundation for all governance and incident response activities

See [Cross-Framework Governance Map](../docs/cross-framework-governance-map.md) for full integration detail.
