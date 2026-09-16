# Three-Horizon Roadmap & Board Pitch

## Roadmap

### Horizon 1 — Now (0-3 months)
*Quick wins. Ship with existing capabilities.*

| Initiative | Metric | Confidence |
|-----------|--------|-----------|
| Wire broker reason-code capture into an automated weekly golden-set pipeline (closes the Recursive Learning loop, still broken since M2/M5) | Correction Loop score moves from 2/5 → 4/5 by next quarterly re-score | H |
| Fix the loan-refinance false-positive pattern found in red-teaming (M4) | Flag precision on refinance events reaches parity with new-loan events  | H |
| Ship a native claim-tracking view for ops teams (top Build candidate from Shadow AI Audit) | Eliminates the ~$420/mo per-partner labor drag from manual spreadsheet tracking | H  |
| Name the literal data pipeline from broker dismissal → retrain trigger (the fix flagged in the feedback-loop self-audit) | Closes the unlabeled-data-class gap before it becomes a real Samsung-path incident | H |



### Horizon 2 — Next (3-9 months)
*Bets. Requires new capabilities or integrations.*

| Initiative | Metric | Confidence |
|-----------|--------|-----------|
| License comparable risk data (Verisk-tier or equivalent) to fix Domain Context — the single biggest vulnerability from M1/M2 | Domain Context score moves from 2/5 → 4/5; gap-detection accuracy improves independent of proxy-signal quality | M |
| CRM integration for flagged-gap delivery (Partner path from Shadow AI Audit) | Reduces the ChatGPT-rewrite workaround to near-zero usage | M |
| Build the shared Cross-Domain Transfer layer so auto/home/life detection inform each other | Cross-Domain loop moves from Missing → Active | M |

### Horizon 3 — Bet (9-18 months)
*Moonshots. High uncertainty, high potential.*

| Initiative | Metric | Confidence |
|-----------|--------|-----------|
| Extend Broker Copilot (the M1 dependency) across the full five-bet portfolio as shared infrastructure, turning Network Intelligence into a real proprietary data asset rather than an informal effect | Network Loop moves from 3/5 → 5/5; becomes the actual data moat Microsoft/Verisk can't buy off the shelf  | L |

## Board Pitch

**Thesis (1 sentence):** Coverage Gap Advisor turns VIU's existing bank and credit union embeds into an active insurance acquisition channel — but the AI itself isn't the moat, the licensed-broker relationship and the embed are, and we need to close the Domain Context gap before that becomes the whole story instead of a warning.

**The case:**
We're sitting on 4/5 contextual moat and 4/5 platform exposure protection — genuinely hard for a platform to replicate because it requires being inside a regulated financial institution's actual account-opening flow, not just intelligence. But Data Advantage sits at 3/5, and that's the exact seam a real, named competitor can exploit faster than we can out-innovate them.

1. Why now: Microsoft's Copilot for Financial Services is a plausible 90-day threat, not a hypothetical one — bundling Verisk-backed coverage insight into a suite our own bank partners already pay for turns this from a competitive question into a budget-line consolidation question at their next renewal. We have a real window before that pitch exists.
2. What's defensible: The regulated, licensed-broker handoff and the compliance relationship — Microsoft has no interest in owning that regulatory surface, and it's the one part of this product a Copilot bundle genuinely can't replicate.
3. The economics: Gross margin holds at ~86% even under 3x inference-cost stress, because AI COGS is a small fraction of total cost against a hybrid base-plus-usage pricing model — the margin story isn't AI expansion, it's ~32% more gross dollars per partner from better-targeted leads, and that's the number worth leading with.

**The risks:**
Domain Context is a rented advantage, not an owned one. If we don't move on data licensing, our "proprietary" gap-detection is only as good as a proxy signal a competitor with real risk data can beat on day one.
1. Trust / failure modes: Tiered confidence with mandatory human review below 90%, a golden dataset that already caught a real production miss (loan refinances misread as new-loan events), and a hallucination-rate contract with an auto-rollback trigger — not a page — because a fabricated "why this was flagged" reaching a broker is a compliance exposure, not just a bad UX moment.
2. Scale / governance: Responsible AI Maturity currently sits at 15/25 — "Developing." Three separate audits this quarter (M2's flywheel, M5's compounding system, M5's feedback-loop self-audit) all converged on the same root cause: one review channel doing the job of three, with no named data pipeline connecting broker correction to model retrain. That's the fix that closes the most gaps at once.
3. Competitive: Ranked by urgency — Verisk (6–12 months, ~40% of value at risk) first, Google's agentic shopping (12–18 months, ~30%) second, core banking vendors like Q2/Jack Henry (18–24 months, ~50% if it lands) third but highest ceiling.

**The ask:** Fund the Horizon 1 data-pipeline fixes now — they're cheap and close real exposure — and greenlight a data-licensing evaluation for Horizon 2 before a competitor's procurement conversation makes the decision for us.

## M1 Baseline vs. Now
*Your 3-sentence AI strategy from Module 1 vs. what you'd say now:*

**M1 baseline:** We don't really have one — we have a quoting engine with a chatbot on top of it... 'AI strategy' at VIU right now means 'automate the parts of the broker's job that don't require a license,' and we haven't said out loud where that stops.

**Now:** We have a specific product, a scored vulnerability profile, a named attacker with a dated 90-day plan, a margin model that survives 3x stress, a reliability contract with real thresholds, and a governance policy that's already caught its own gap. The line I'd change from M1: it's not that we haven't said where automation stops — it's that we now know exactly where it stops (never-auto customer contact, mandatory human review under 90% confidence) and exactly where our real advantage sits (the license and the embed, not the model). That's the actual gap this course closed.
