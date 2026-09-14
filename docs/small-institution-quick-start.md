# Small Institution Quick-Start Guide

## 30 Days to a Defensible AI Governance Baseline

This guide is written for financial institutions that do not have a dedicated AI risk team, a data science department, or an existing AI governance program. If you have two developers and a compliance officer, this guide is written for you.

The goal is not perfection. The goal is a defensible, documented baseline that you can show a regulator, build on over time, and actually maintain with the staff you have.

---

## Before You Start — Take Inventory

Spend one hour answering these questions. Write down the answers.

**Question 1:** What AI systems are currently running in your institution?
Include any system where a computer is making or recommending decisions automatically. This includes:
- Identity verification vendors (Socure, Alloy, Experian, others)
- Fraud detection systems (whether built or bought)
- Credit scoring models (whether from a bureau or a vendor)
- Loan pre-qualification tools
- Chatbots or automated customer service systems
- Any system your core banking vendor describes as "AI-powered"

**Question 2:** For each system, who is responsible for it?
Name a specific person at your institution who is accountable for each AI system. If no one is currently accountable, assign someone now. This person becomes the model owner.

**Question 3:** For each system, do you have documentation from the vendor?
Collect whatever you have: user agreements, product documentation, model cards, validation reports. Put it all in one folder.

This inventory is Day 1. Everything else builds on it.

---

## Week 1 — Classify and Prioritize

Not all AI systems need the same level of attention. Use these questions to classify each system:

**High risk — address first:**
- Does this system make or recommend decisions that affect whether a consumer gets access to a financial product?
- Does this system decide whether a transaction is fraudulent, potentially blocking a consumer from their own money?
- Could a wrong decision by this system cause financial harm to a consumer?

If yes to any of these, the system is high risk. Start here.

**Medium risk — address second:**
- Does this system assist a human who makes the final decision?
- Does a wrong decision cause operational problems but not direct consumer harm?

**Low risk — address last:**
- Does this system only affect internal operations with no consumer-facing impact?

Write your classification next to each system in your inventory.

---

## Week 2 — Document What You Have

For each high-risk AI system, complete this one-page summary. Use the information you collected from vendors and your own team:

```
SYSTEM: [Name]
VENDOR OR BUILDER: [Who built this]
MODEL OWNER: [Name and title at your institution]
WHAT IT DOES: [One sentence, plain language]
WHAT DATA IT USES: [List the inputs]
WHAT IT DECIDES OR RECOMMENDS: [Specifically]
HOW OFTEN IT IS USED: [Daily / weekly / per transaction]
WHO REVIEWS ITS DECISIONS: [Name or role of human reviewer]
CAN IT BE TURNED OFF QUICKLY: [Yes / No / Unknown]
FALLBACK IF IT IS TURNED OFF: [What happens to that process]
LAST VALIDATED: [Date or "Unknown"]
VENDOR DOCUMENTATION ON FILE: [Yes / No]
FAIR LENDING REVIEW COMPLETED: [Yes / No]
```

If you cannot answer a question, write "Unknown." Unknown answers are the gaps you will work to close. They are not a reason to stop.

---

## Week 3 — Run Three Quick Tests

These three tests do not require a data scientist. They require access to your systems and a few hours.

**Quick Test 1: The Kill Switch Test**
For each high-risk AI system, identify the process for disabling it immediately if something goes wrong. Test it in a non-production environment if possible. Document: who can disable it, how long it takes, and what the fallback is.

**Quick Test 2: The Explanation Test**
Take five recent adverse decisions made or recommended by each high-risk AI system. For each one, ask: can a compliance officer explain in plain language why this decision was made? If the answer is no for any of them, document that gap.

**Quick Test 3: The Override Rate Estimate**
Ask your human reviewers: in the past 30 days, approximately what percentage of AI recommendations did you change? If the answer is above 20%, that is a flag worth investigating.

Document the results of all three tests. Flags are not failures. They are the starting point for improvement.

---

## Week 4 — Establish Ongoing Monitoring

Set a recurring calendar event for each high-risk AI system. This is your monitoring cadence:

**Monthly — 30 minutes per system:**
- Review the human override rate for the past month
- Review any consumer complaints that mention AI-assisted decisions
- Confirm the system is still operating as documented

**Quarterly — 2 hours per system:**
- Run the fairness drift check from the Model Drift Monitoring Checkpoints document
- Review vendor communications for any model updates or known issues
- Update the system documentation if anything has changed

**Annually — half day per system:**
- Full review of the system documentation
- Request updated validation documentation from vendors
- Confirm that the model owner is still the right person
- Confirm the fallback is still operational

---

## What to Do With Vendor AI

Most small institutions use AI built by vendors, not built in-house. This does not reduce your governance responsibility. Under ECOA, the CFPB, and fair lending laws, your institution is responsible for the decisions made by AI you deploy, regardless of who built it.

When working with AI vendors, request:
- A model card or validation summary for any AI product you use for consumer decisions
- Information about how the model was tested for fairness and disparate impact
- Notification when the vendor updates the model
- Ability to disable the AI component without ending the vendor relationship entirely

Document what the vendor provides and what they do not provide. Both are important information for your governance records.

---

## Your 30-Day Deliverables

At the end of 30 days you should have:

- [ ] AI system inventory with one page per high-risk system
- [ ] Model owners named for every high-risk system
- [ ] Kill switch documentation for every high-risk system
- [ ] Results of the three quick tests with flags documented
- [ ] Monitoring calendar established with quarterly and annual events scheduled
- [ ] Vendor documentation collected and filed

This is your baseline. It is not everything the full framework requires. It is enough to demonstrate to a regulator that your institution takes AI governance seriously, has identified your AI systems, knows who is responsible for them, and has a plan for ongoing monitoring.

Build from here.
