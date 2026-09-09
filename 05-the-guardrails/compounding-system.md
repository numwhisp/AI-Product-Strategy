# Compounding System Design

## Feedback Loops

| Loop | Input | Output | Compounds? | Status |
|------|-------|--------|-----------|--------|
| Recursive Learning | Broker dismissal/reason-code data on flagged gaps (accurate, already insured, bad match, not actionable)  | Improved flag precision via periodic retraining | N | broken - Improved flag precision via periodic retraining |
| Cross-Domain Transfer | Proxy account signals used separately for auto, home, and life gap types | Intended: a pattern learned improving auto-gap detection also sharpens home/life detection | N | missing - no shared representation exists yet; each gap type is scored off its own logic in isolation, so nothing learned in one domain transfers to another.  |
| Network Intelligence | Aggregate flag/outcome data across all bank and credit union partners | A shared baseline detection model that improves as partner count grows | Y | active - informal, but real. This is the one loop already doing work (scored 3/5 as the Network Loop back in M2).  |

**Loops mapped: 3**
**Loops that actually compound: 1**
**Active / Broken / Missing: 1 / 1 / 1**

**Freeze test:** Probably yes, we'd survive a 3-month freeze — but only on the strength of Network Intelligence's informal effect and the underlying B2B embed moat, not because the product is genuinely learning. That's the honest read: one compounding loop out of three, and it's the weakest kind of compounding — informal, not engineered. The real moat right now is distribution (being inside the bank's flow), not intelligence that improves with use. That's consistent with the "Developing" band from the Maturity Scorer — it's not a coincidence, it's the same underlying gap showing up twice.

**Broken loop identified by partner:** Recursive Learning — this is the same loop that let the loan-refinance false-positive ship in the first place (Module 4's red-team finding). The capture mechanism exists; it just doesn't feed anywhere yet.
**Fix plan:** Wire the already-designed broker reason-code capture into the weekly golden-set review as an automated pipeline step instead of a manual one, and turn on the monthly retrain trigger once 5+ new rows accumulate — the threshold was already specified in M4's HITL Architecture, it just needs to actually fire.

## Context Connectivity
<!-- How does knowledge flow across teams and domains? Where does it silo? -->
**How knowledge flows:** Broker feedback currently reaches VIU's product/ops team only through the weekly golden-set review, and that review updates the dataset manually.

**Where it silos:** Between bank partners — an edge case one partner's data surfaces (like the refinance miss) doesn't propagate to other partners' live models until a human manually adds it to the shared golden set and ships a new version. It also silos across gap types — auto, home, and life detection don't share a domain-context layer, so nothing learned in one improves the others.

## Governance Policy

**Scope:**
*Covers:* AI-driven coverage-gap detection and flagging surfaced to licensed brokers at partner bank/credit union account-opening events, including broker-facing summary and talking-points generation.
*Excludes:* Underwriting decisions, policy pricing, claims processing, and any customer-facing automated communication — all customer contact remains human-broker-initiated.

**Autonomy boundaries:**
    (1) Surface a high-confidence (>90%) flag to the broker queue — 🟢 auto
    (2) Surface a medium-confidence (50–90%) flag with hedged language, no pre-drafted customer copy — 🟡 human approval
    (3) Send any customer-facing communication — 🔴 never auto
    (4) Retrain the model on accumulated broker corrections — 🟡 human approval (AI/ML lead signs off before a retrained version ships)

**Escalation triggers:**
    (+) Confidence score <90% on any flag
    (+) Customer has dismissed 2+ prior AI flags as incorrect
    (+) Flag involves a joint-account or identity-ambiguity signal
    (+) Customer has opted out of insurance marketing contact — suppresses the flag entirely, doesn't just escalate it
    (+) Weekly hallucination-rate audit exceeds 2%
    
**Audit cadence:**
| Cadence |	What we review | Owner |
| ------ | ------------------ | ----------- |
|Real-time |	Latency (p95) against the <800ms target |	Platform/SRE on-call |
| Weekly |	150-row golden dataset — accuracy, hallucination rate, broker reason-code dismissals |	PM: rotating VIU product/ops reviewer |
| Monthly |	Retrain trigger review, once 5+ new golden-set rows have accumulated from real production misses |	AI/ML lead |
| Quarterly |	Full Responsible AI Maturity re-score, partner-level drift review, Shadow AI Audit refresh |	Head of Product, VIU |

**Regulatory exposure (EU AI Act / other):**
*Regimes:* State insurance AI regulations (NAIC model act / Colorado SB21-169-style algorithmic bias testing), GLBA (financial data privacy, since this runs on bank account data), and EU AI Act framing noted for future-proofing even though this is currently a US-only product.
*Risk tier:* 🟡 Limited — a decision-support system with a mandatory human broker in the loop before any customer contact, not a fully autonomous high-risk system, but it touches regulated financial data.
*Controls in place:* Human-in-the-loop for all sub-90%-confidence flags, mandatory reason-code capture and audit trail, golden-dataset accuracy/bias monitoring, compliance-override suppression for opted-out customers, no autonomous customer contact.

## Agent Topology
<!-- If using agents: what can each agent do? What can't it do? Who approves what? -->
One system, not a multi-agent topology: the detection-and-draft assistant. Can do: detect gaps, draft explanations and broker talking points. Can't do: contact customers directly, override compliance suppression, or retrain itself without sign-off. Approval owner: AI/ML lead for retraining; the claiming broker for any customer-contact decision.
## Shadow AI Audit

| Tool | Owner | Risk Level | Decision |
|------|-------|-----------|----------|
|Broker's personal CRM cross-check habit (verifying flagged customers before acting) | Signal source: individual brokers, no formal owner | L | keep — low risk, and it's actually a useful trust-building bridge until the confidence UI earns full reliance |
| ChatGPT used by bank ops teams to rewrite VIU's flagged-gap output into customer outreach | Signal source: partner bank ops teams  |  M | govern — not dangerous today, but customer account data is leaving VIU's compliance boundary once it's pasted into an external tool; needs an explicit policy line, not a ban |
| Broker's CRM-native AI summarizer restating VIU's "why flagged" explanation | Signal source: individual brokers | L | keep — redundant effort, not a compliance or trust risk on its own |
| Ops team's manual spreadsheet export to track flagged-lead claim status across brokers | Signal source: partner bank ops teams | M  | govern — workable as a stopgap, but it's untracked customer-lead data living outside VIU's system of record; worth a lightweight data-handling guideline until the real claim-tracking feature ships |
| Smaller partner's Zapier flow piping flagged leads into their own ticketing system, bypassing VIU's broker queue UI | Owner: partner's internal IT team | H | govern — this one's the sharpest: flagged customer account data flowing through an unreviewed third-party automation is the actual Samsung-path risk named in the self-audit, and it needs a real data-handling clause in the partner agreement, not an informal "we noticed" conversation |

**Total tools found:** 5
**Tools after triage:** 3 — the two "Keep" rows (broker CRM cross-check, CRM-native summarizer) drop out of active tracking since they're low-risk individual habits, not systemic exposure. The three "Govern" rows carry forward: ChatGPT-based outreach rewriting, the manual spreadsheet export, and the partner's Zapier flow — each needs an actual data-handling clause, not just a watch-and-wait.
**Estimated hidden spend:** Unknown — none of these are paid tools VIU is billing for, so there's no license cost to total up. The real hidden cost isn't spend, it's exposure: customer account data moving through three unreviewed channels outside VIU's compliance boundary. Worth saying that plainly in the room rather than forcing a dollar figure that doesn't exist — the honest finding here is a governance gap, not a budget line.
