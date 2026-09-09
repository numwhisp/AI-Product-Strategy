<!-- Governance Policy, Coverage Gap Advisor -->

## Governance Policy

**Scope:** AI-driven coverage-gap detection and flagging surfaced to licensed brokers at partner bank/credit union account-opening events, including broker-facing summary and talking-points generation. Excludes: Underwriting decisions, policy pricing, claims processing, and any customer-facing automated communication — all customer contact remains human-broker-initiated.

**Autonomy boundaries:** Surface a high-confidence (>90%) flag to the broker queue, auto. Surface a medium-confidence (50–90%) flag with hedged language, no pre-drafted customer copy, human approval required. Send any customer-facing communication, never auto. Retrain the model on accumulated broker corrections — 🟡 human approval (AI/ML lead signs off before a retrained version ships), human approval required.

**Escalation triggers:** Escalation triggers (1) Confidence score <90% on any flag (2) Customer has dismissed 2+ prior AI flags as incorrect (3) Flag involves a joint-account or identity-ambiguity signal (4) Customer has opted out of insurance marketing contact — suppresses the flag entirely, doesn't just escalate it (5) Weekly hallucination-rate audit exceeds 2%

**Audit cadence:** Real-time, Latency (p95) against the <800ms target (Platform/SRE on-call). Weekly, 150-row golden dataset — accuracy, hallucination rate, broker reason-code dismissals (PM: rotating VIU product/ops reviewer). Monthly, Retrain trigger review, once 5+ new golden-set rows have accumulated from real production misses (AI/ML lead). Quarterly, Full Responsible AI Maturity re-score, partner-level drift review, Shadow AI Audit refresh (Head of Product, VIU).

**Regulatory exposure (EU AI Act / other):** State insurance AI regulations (NAIC model act / Colorado SB21-169-style algorithmic bias testing), GLBA (financial data privacy, since this runs on bank account data), and EU AI Act framing noted for future-proofing even though this is currently a US-only product.. Risk tier: limited. Controls: Human-in-the-loop for all sub-90%-confidence flags, mandatory reason-code capture and audit trail, golden-dataset accuracy/bias monitoring, compliance-override suppression for opted-out customers, no autonomous customer contact..

## Agent Topology

One system, not a multi-agent topology: the detection-and-draft assistant. Can do: detect gaps, draft explanations and broker talking points. Can't do: contact customers directly, override compliance suppression, or retrain itself without sign-off. Approval owner: AI/ML lead for retraining; the claiming broker for any customer-contact decision.
