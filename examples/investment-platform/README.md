# Example: Investment Research Platform AI Governance

**Profile:** Large-scale investment research platform serving more than 500 investment professionals across equity, fixed income, and quantitative research teams. Assets under management exceed five trillion dollars. The platform includes AI systems that process research notes, answer analyst queries, and surface relevant information in real time.

**AI systems in scope:** AI-powered document insight and query system; AI-assisted research summarization; automated research distribution workflow.

---

## The AI Systems

### System 1 — Document Insight and Query Engine

**What it does:** Accepts plain-language questions from investment professionals and returns summaries and relevant excerpts from the research note corpus. Example: "What did our analysts say about semiconductor supply chains in Q3?" The system retrieves relevant notes and produces a synthesized answer.

**Risk tier:** Medium — assists human researchers but does not make investment decisions. Outputs are reviewed by the requesting analyst before use.

**Key governance consideration:** Every output is tied to need-to-know access controls. An analyst in the equity research group cannot query notes restricted to the fixed income team. The AI system must enforce these access boundaries in its retrieval layer, not just in the display layer.

**Model validation approach:**
- Accuracy tested on a curated set of 200 research questions with known correct answers
- Access control tested by attempting to retrieve restricted documents through query variants
- Output quality reviewed by senior analysts for a 30-day shadow period before full deployment
- Human review required: all outputs are labeled as AI-assisted; analysts confirm before citing

### System 2 — Research Summarization

**What it does:** Generates structured summaries of long-form research documents, earnings call transcripts, and analyst reports. Reduces the time analysts spend on initial document review.

**Risk tier:** Medium — summary assists the analyst but the analyst reads the source document before acting on it.

**Key governance consideration:** Summarization models can introduce subtle distortions — emphasizing certain themes, omitting caveats, or misrepresenting quantitative data. The governance program specifically monitors for summarization errors that could lead to investment decisions based on inaccurate information.

**Monitoring:** Senior analysts review a random sample of 20 AI-generated summaries per month against the source documents. Any material inaccuracy is logged as a Level 3 incident.

### System 3 — Automated Research Distribution Workflow

**What it does:** Routes newly published research notes to relevant distribution lists based on content classification. An equity research note on semiconductor companies is automatically routed to analysts covering the technology sector.

**Risk tier:** Low — affects internal operations, not consumer-facing decisions.

**Key governance consideration:** Misrouting research notes is operationally disruptive but not directly harmful to consumers. Governance focuses on accuracy monitoring rather than fairness testing.

---

## Governance Program Structure

### Model Owners

| System | Model Owner | Tier |
|---|---|---|
| Document Insight and Query | Head of Research Technology | Medium |
| Research Summarization | Head of Research Technology | Medium |
| Distribution Workflow | Research Operations Manager | Low |

### Monthly Monitoring (Medium-tier systems)

**Data Distribution Check:** Verify that the queries arriving at the document insight system are within the distribution expected based on research activity patterns. Unusual query volumes or patterns may indicate system misuse.

**Override Rate Equivalent:** Track the rate at which analysts dismiss or override AI-generated summaries when they choose to rely on the source document instead. Target: analysts engage with the AI summary as a useful starting point at least 70% of the time.

**Access Control Audit:** Monthly verification that no restricted documents were returned to unauthorized users. Zero tolerance — any access control failure is a Level 2 incident.

### Quarterly Review

**Summarization accuracy sample:** 60-document sample reviewed by senior analysts. Flag rate above 5% triggers model review.

**Query-answer accuracy review:** 50-question evaluation set re-run quarterly. Performance must stay within 10% of deployment baseline.

**User feedback review:** Analyst satisfaction survey distributed quarterly. Declining satisfaction scores investigated before next cycle.

---

## The Legacy System Modernization Dimension

Many investment research platforms have legacy publishing and distribution systems that were built before AI was a consideration. Modernizing these systems while maintaining the functions analysts depend on is itself a governance challenge.

**Design principles for AI-integrated legacy modernization:**

**Preserve first, then augment.** Every function the legacy system performs must work correctly in the new system before AI augmentation is added. AI features are layered on top of confirmed functional equivalence, not built as part of the initial migration.

**Document the undocumented.** Legacy systems often encode institutional knowledge that is not written anywhere. Before modernization, invest time in documenting how the current system behaves, including edge cases that experienced analysts know about but that are not in any specification. These behaviors must be preserved.

**Shadow period for AI features.** New AI capabilities run in shadow mode — producing outputs but not displaying them to users — for at least 30 days before full deployment. Shadow mode outputs are reviewed by senior users who compare them against what they would expect. Only features that pass shadow review are deployed.

**Rollback plan.** At every stage of modernization, the previous state must be restorable within four hours. This is especially important for research distribution systems where analysts have time-sensitive workflows.

---

## What This Example Demonstrates

Investment research platforms are among the most complex environments for AI governance because they combine high-stakes institutional decision-making, strict access control requirements, regulated investment advice obligations, and legacy infrastructure that cannot simply be replaced.

The governance practices described here — access control enforcement in the AI retrieval layer, shadow period validation, summarization accuracy monitoring, and legacy system modernization principles — are generalizable to any institutional platform serving professional users in a regulated environment.

They represent the same discipline applied at scale that this framework makes available to smaller institutions that are beginning to deploy AI in their own research and advisory workflows.
