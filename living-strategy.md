# Lily

> Coverage Gap Advisor turns VIU's existing bank and credit union embeds into an active insurance acquisition channel by surfacing AI-flagged coverage gaps at account opening, now — before Microsoft's Copilot for Financial Services makes this a bundled feature banks get for free.

---

## Strategy at a Glance

| Component | Module | Status | Key Artifact |
|-----------|--------|--------|-------------|
| **The Bet** | M1 | [x] | `01-the-bet/` |
| **The Moat** | M2 | [x] | `02-the-moat/` |
| **The Margin** | M3 | [x] | `03-the-margin/` |
| **The Contract** | M4 | [x] | `04-the-contract/` |
| **The Guardrails** | M5 | [x] | `05-the-guardrails/` |
| **The Pitch** | M6 | [x] | `06-the-pitch/` |

---

## The Bet (M1)

**What we're building, for whom, why now.**

- **Product:** Lily
- **AI Value Archetype:** Oracle
- **Vulnerability Scores:** _(add: Moat _/5 · Data _/5 · Platform _/5)_
- **Top Risk:** Domain Context is a rented advantage, not an owned one — Coverage Gap Advisor's predictions run on proxy signals from bank transaction data instead of real risk data, and Microsoft can neutralize that entire loop in one Verisk licensing deal bundled into Copilot for Financial Ser…
- **Confidence:** H
- **Prototype:** (https://advisor-lead-gen.lovable.app)
- **Kill Criteria:** Kill the bet if, after a real pilot with one bank partner, the flagged-gap-to-bind conversion rate doesn't beat the baseline (unprompted policy purchases from the same partner's existing customer base) by a meaningful margin — if brokers are chasing AI-flagged leads that convert …

→ Details: [`01-the-bet/`](01-the-bet/)

---

## The Moat (M2)

**Why this won't get copied in 6 months.**

- **Data Flywheel Score:**
- **Weakest Loop:** Domain Context (tied with Correction and Preference at 2, but Domain Context is the one directly exploitable by an outside data vendor rather than an internal capture fix)
- **Top Encroachment Threat:** Google (Gemini agentic shopping)
- **Encroachment Defense:** License comparable risk data directly (or negotiate exclusive access to something Verisk-tier data providers don't offer competitors), since this is the only weak loop VIU doesn't fully control the ti…
- **Vendor Portability:** Locked

→ Details: [`02-the-moat/`](02-the-moat/)

---

## The Margin (M3)

**Will this make money or bleed it?**

- **Gross Margin (current):**
- **Gross Margin (AI-adjusted):**
- **Pricing Model:** (seat-based / usage-based / outcome-based / hybrid) _**Hybrid (base + usage)**_
- **Pricing Today → Tomorrow:** $2,500/mo platform fee + $150 per bound policy (standard embedded lead-gen commission, no AI). → Hybrid — $2,500/mo base (unchanged, keeps partner onboarding easy) + $0.75 per AI-flagged, broker-claimed lead (usage) + existing $150/bound policy commission retained.
- **Total AI COGS / unit:**
- **Cascading Strategy:** Triage: Mid-tier model handles every gap-detection pass and the plain-language explanation.; frontier: Reserved for the broker-facing summary draft — only invoked after a lead clears confidence threshold and gets claimed.; ratio 80% Mid/Small / 20% Frontier.
- **Net Margin Shift:** Net margin shift: Margin % barely moves (84% → 84.4%) — the story isn't margin expansion, it's gross dollars per partner up ~32% ($3,700 → $4,900), driven by AI improving lead quality and bind rate, n…
- **Break-even at:**

→ Details: [`03-the-margin/`](03-the-margin/)

---

## The Contract (M4)

**Why users will trust a probabilistic system.**

- **Reliability Target:**
- **Golden Dataset:** 10 rows, __ adversarial
- **Confidence UX:** show uncertainty / tiered confidence / human-in-loop trigger
- **HITL Architecture:** **Threshold:** Low (<70%) → never reaches a human, suppressed by design. Medium (70–90%) → mandatory human review before any customer contact.…
- **Failure Mode Coverage:** *What failure mode did your partner find that you missed?*

→ Details: [`04-the-contract/`](04-the-contract/)

---

## The Guardrails (M5)

**What breaks when this scales, and what compounds.**

- **Compounding System:** | Loop | Input | Output | Compounds? | Status | |------|-------|--------|-----------|--------| | Recursive Learning | Broker dismissal/reason-code data on flagged gaps (accurate, already insured, bad match, not actionabl…
- **Governance Posture:** *Covers:* AI-driven coverage-gap detection and flagging surfaced to licensed brokers at partner bank/credit union account-opening events, including broker-facing summary and talking-points generation.
- **Autonomy Boundaries:** (1) Surface a high-confidence (>90%) flag to the broker queue — 🟢 auto
- **Escalation Triggers:** (+) Confidence score <90% on any flag
- **Audit Cadence:** | Cadence | What we review | Owner |
- **Shadow AI Audit (user-side):** 5 workarounds found · 3 — the two "Keep" rows (broker CRM cross-check, CRM-native summarizer) drop out of active tracking since they're low-risk individual habits, not systemic exposure. The three "Govern" rows carry forward: ChatGPT-based outreach rewriting, the manual spreadsheet export, and the partner's Zapier flow — each needs an actual data-handling clause, not just a watch-and-wait. build candidates · adjacent spend Unknown — none of these are paid tools VIU is billing for, so there's no license cost to total up. The real hidden cost isn't spend, it's exposure: customer account data moving through three unreviewed channels outside VIU's compliance boundary. Worth saying that plainly in the room rather than forcing a dollar figure that doesn't exist — the honest finding here is a governance gap, not a budget line.
- **Agent Boundaries:** One system, not a multi-agent topology: the detection-and-draft assistant. Can do: detect gaps, draft explanations and broker talking points.…
- **Regulatory Exposure:** *Regimes:* State insurance AI regulations (NAIC model act / Colorado SB21-169-style algorithmic bias testing), GLBA (financial data privacy, since this runs on bank account data), and EU AI Act framing noted for future-p…

→ Details: [`05-the-guardrails/`](05-the-guardrails/)

---

## The Pitch (M6)

**How you get this funded, shipped, and adopted.**

- **Horizon 1 (Now):** Wire broker reason-code capture into an automated weekly golden-set pipeline (closes the Recursive Learning loop, still broken since M2/M5) · Fix the loan-refinance false-positive pattern found in red-teaming (M4) · Ship a native claim-tracking view for ops teams (top Build candidate from Shadow AI Audit) · Name the literal data pipeline from broker dismissal → retrain trigger (the fix flagged in the feedback-loop self-audit)
- **Horizon 2 (Next):** License comparable risk data (Verisk-tier or equivalent) to fix Domain Context — the single biggest vulnerability from M1/M2 · CRM integration for flagged-gap delivery (Partner path from Shadow AI Audit) · Build the shared Cross-Domain Transfer layer so auto/home/life detection inform each other
- **Horizon 3 (Bet):** Extend Broker Copilot (the M1 dependency) across the full five-bet portfolio as shared infrastructure, turning Network Intelligence into a real proprietary data asset rather than an informal effect
- **Board Narrative:** Coverage Gap Advisor turns VIU's existing bank and credit union embeds into an active insurance acquisition channel — but the AI itself isn't the moat, the licensed-broker relationship and the embed are, and we need to close the Domain Context gap before that becomes the whole st…
- **Ask:** Fund the Horizon 1 data-pipeline fixes now — they're cheap and close real exposure — and greenlight a data-licensing evaluation for Horizon 2 before a competitor's procurement conversation makes the decision for us.
- **Key Strategic Change:**

→ Details: [`06-the-pitch/`](06-the-pitch/)
