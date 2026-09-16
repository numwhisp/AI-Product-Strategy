# My AI Product Strategy

> A living strategy built across 6 sessions. Each module adds one component. By Module 6, this repo IS your strategy — version-controlled, board-ready, portable.

---

## Strategy at a Glance

| Component | Module | Status | Key Artifact |
|-----------|--------|--------|-------------|
| **The Bet** | M1 | [✅] | `01-the-bet/`|
| **The Moat** | M2 | [✅] | `02-the-moat/`|
| **The Margin** | M3 | [✅] | `03-the-margin/`|
| **The Contract** | M4 | [✅] | `04-the-contract/`|
| **The Guardrails** | M5 | [✅] | `05-the-guardrails/`|
| **The Pitch** | M6 | [✅] | `06-the-pitch/`|

---

## The Bet (M1)

**What we're building, for whom, why now.**

- **Product:** Coverage Gap Advisor — AI-flagged insurance coverage gaps surfaced at bank/credit union account opening, routed to a licensed broker for handoff.
- **AI Value Archetype:** surfaces a prediction for a human to act on; doesn't execute autonomously.
- **Vulnerability Scores:** Moat _4_/5 · Data _3_/5 · Platform _4_/5 (Composite 11/15 — Medium)
- **Top Risk:** Domain Context is a rented advantage, not an owned one — predictions run on proxy bank-transaction signals instead of real risk data, and a competitor can neutralize this loop with a single data-licensing deal.
- **Confidence:**  M 
- **Prototype:** [https://advisor-lead-gen.lovable.app/]
- **Kill Criteria:** If a real partner pilot shows flagged-gap-to-bind conversion doesn't beat the baseline (unprompted purchases from the same customer base), kill it — the underlying signal is failing, not just under-marketed.

→ Details: [`01-the-bet/`](01-the-bet/)

---

## The Moat (M2)

**Why this won't get copied in 6 months.**

- **Data Flywheel Score:** _9_/20
- **Weakest Loop:** Domain Context (2/5) — exploitable by an outside data vendor without needing anything from VIU.
- **Competitive Position:** [describe axes + placement] Contextual Moat and Platform Exposure both strong (4/5) — defensible because it requires being embedded inside a regulated bank's actual account-opening flow. Data Advantage is the seam: Verisk (6–12mo, ~40% value at risk), Google agentic shopping (12–18mo, ~30%), core banking vendors like Q2/Jack Henry (18–24mo, ~50% if it lands).
- **Encroachment Defense:** Licensed-broker relationship and compliance/regulatory standing — the part no platform bundle can replicate. War-gamed 90-day plan names Microsoft (Copilot for Financial Services + Verisk data) as the sharpest near-term threat, attacking via budget-line consolidation rather than a switching decision.
- **Vendor Portability:** Locked — single-provider (Azure OpenAI), no abstraction layer, no routing, informal eval only. The uncomfortable finding: running on the infrastructure of the same company positioned to make this product obsolete.

→ Details: [`02-the-moat/`](02-the-moat/)

---

## The Margin (M3)

**Will this make money or bleed it?**

- **Gross Margin (current):** ~84% (traditional commission model, no AI)
- **Gross Margin (AI-adjusted):** ~84% (traditional commission model, no AI)
- **Pricing Model:** Hybrid — $2,500/mo base + $0.75 per AI-flagged, broker-claimed lead + existing $150/bound-policy commission. Outcome-based alternative modeled (Intercom-style, $300/AI-attributed bind, $0 base) as a stronger sales pitch with a materially higher revenue-risk profile.
- **Cascading Strategy:** 80/20 split — Small/Mid tier handles detection and explanation; Frontier tier reserved for broker-claimed leads only. Chosen for margin, not for cutting quality on leads a human already decided were worth pursuing.
- **Break-even at:** Well below current volume — AI COGS ($0.163–$0.18/user/month) is a small fraction of the $2,500 base fee; the real cost driver is human-in-the-loop review, not inference.

→ Details: [`03-the-margin/`](03-the-margin/)

---

## The Contract (M4)

**Why users will trust a probabilistic system.**

- **Reliability Target:** Accuracy 90–95% · Hallucination rate <1% · Latency (p95) <800ms · Drift velocity <0.5%/4wk
- **Golden Dataset:** 10 rows drafted (v1 ship target ~150), 3 adversarial (identity-match spoofing, compliance-override bypass, repeat-dispute trust erosion)
- **Confidence UX:** [approach] Tiered — >90% auto-surfaces full flag with pre-drafted talking points; 50–90% surfaces hedged, review-required; <50% suppressed entirely, logged for pattern analysis only.
- **HITL Architecture:** Human review triggered below 90% confidence, on joint-account ambiguity, or on repeat-dispute customers. Every broker dismissal (with reason code) feeds back into the golden-set audit and a monthly retrain trigger — the mechanical fix for M2's weakest flywheel loop.
- **Failure Mode Coverage:** Red-team found a live gap — loan refinances misread as new-loan events, generating false positives on already-insured customers. Now golden-dataset row #5; the clearest evidence the Correction Loop needed closing.

→ Details: [`04-the-contract/`](04-the-contract/)

---

## The Guardrails (M5)

**What breaks when this scales — and what compounds.**

- **Compounding System:** [describe feedback loops] 3 loops mapped, only 1 (Network Intelligence) actually compounds. Recursive Learning is Broken — capture exists, but no automated pipeline connects broker corrections to a retrain. Cross-Domain Transfer is Missing entirely (auto/home/life detection don't share learning). Freeze test: we'd probably survive 3 months frozen, which is the problem — the moat right now is distribution, not intelligence that improves with use.
- **Governance Posture:** [approach] Human approval required for medium-confidence flags and any model retrain; customer contact is never auto. Risk tier: Limited (EU AI Act framing) — decision-support with mandatory human-in-the-loop, but touching regulated financial data (GLBA).
Shadow AI Status: 5 workarounds found (hypothesized, pending real validation), 2 Build · 1 Partner · 1 Ignore · 1 TBD. Dominant signal: workflow gap — VIU's output doesn't yet live where brokers and ops teams already work. Estimated adjacent labor drag: ~$595/mo per typical partner, mostly absorbed staff time rather than license spend.
- **Shadow AI Status:** 2 tools found, _5_ triaged. 5 workarounds found (hypothesized, pending real validation), 2 Build · 1 Partner · 1 Ignore · 1 TBD. Dominant signal: workflow gap — VIU's output doesn't yet live where brokers and ops teams already work. Estimated adjacent labor drag: ~$595/mo per typical partner, mostly absorbed staff time rather than license spend.
- **Agent Boundaries:** Single system (detection + draft), not a multi-agent topology. Can detect and draft; cannot contact customers directly, override compliance suppression, or retrain without AI/ML lead sign-off.
- **Regulatory Exposure:** State insurance AI regulations (NAIC/Colorado SB21-169-style), GLBA, EU AI Act noted for future-proofing. Responsible AI Maturity: 15/25 — "Developing," flat across all five dimensions (Compliance, Transparency, Fairness, Privacy, Accountability at 3/5 each).

→ Details: [`05-the-guardrails/`](05-the-guardrails/)

---

## The Pitch (M6)

**How will you get this funded, shipped, and adopted.**

- **Horizon 1 (Now):** Close the Recursive Learning loop (automate the broker-correction → golden-set pipeline), fix the refinance false-positive, ship native claim-tracking (kills the highest-labor-cost workaround), name the literal data-flow for corrections before it becomes a compliance incident.
- **Horizon 2 (Next):** License comparable risk data to fix Domain Context — the single biggest named vulnerability — plus CRM integration and a Cross-Domain Transfer layer across auto/home/life detection.
- **Horizon 3 (Bet):** Extend Broker Copilot as shared infrastructure across the full five-bet portfolio, turning Network Intelligence into a real proprietary data asset instead of an informal effect.
- **Board Narrative:** [1-sentence thesis] Coverage Gap Advisor's moat is the license and the embed, not the AI — and we have a real but closing window to fix the one data gap (Domain Context) before Microsoft or Verisk make that decision for us.
- **Key Metric:** Domain Context flywheel score, 2/5 → 4/5, tracked at each quarterly re-score — the single number that determines whether this bet stays defensible or becomes a feature Microsoft bundles for free.

→ Details: [`06-the-pitch/`](06-the-pitch/)
