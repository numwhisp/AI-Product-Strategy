# Cost Curve & Pricing Strategy - Coverage Gap Advisor
Assumptions flagged where estimated — structure over false precision, per the module's own rule.
## Cost Model

| Cost Category | Per-User/Month | Notes |
|--------------|----------------|-------|
| Inference (primary model) | $0.045 | ~3 requests/user/month avg for detection + explanation |
| Inference (cascading/triage) | $0.018 | Only fires for the ~20% of leads that get claimed by a broker |
| Infrastructure | $0.025 | Hosting, vector lookups for signal matching |
| Data/storage | $0.015 | Account-signal ingestion, retention logs |
| Human-in-the-loop | $0.060 | Broker QA sampling — this is also the fix for the Correction Loop from M2 |
| **Total AI COGS** | $0.163/user/month	 | |

## Cascading Strategy
<!-- Cheap model → frontier model routing logic -->

**Triage model:**Mid-tier model handles every gap-detection pass and the plain-language explanation.
**Frontier model:**Reserved for the broker-facing summary draft — only invoked after a lead clears confidence threshold and gets claimed. 
**Routing rule:**If confidence > 70% AND broker claims the lead → escalate to Frontier for the summary. Otherwise, stay on Mid/Small.
**Expected cascade ratio:** 80% Mid/Small / 20% Frontier.

## Pricing Model

**Current pricing:** $2,500/mo platform fee + $150 per bound policy (standard embedded lead-gen commission, no AI).
**Proposed AI pricing:** Hybrid — $2,500/mo base (unchanged, keeps partner onboarding easy) + $0.75 per AI-flagged, broker-claimed lead (usage) + existing $150/bound policy commission retained.
**Model:** (seat-based / usage-based / outcome-based / hybrid) _**Hybrid (base + usage)**_

1. Strategy — Mine: Penetrate-leaning. Keep the base fee flat and low to protect the existing partner relationship and make this an easy yes, then let usage revenue grow with flagged-lead volume as partners scale — Maximize becomes the option later, once bind-rate lift is proven and the pricing conversation can shift.
2. Unit of work: A confidently-flagged coverage gap successfully routed to and claimed by a broker — not a raw inference call, so pricing tracks value delivered, not compute burned.
3. Structure: Base $2,500/mo · Usage $0.75/unit

## Stress Tests

| Scenario | Impact on Margin | Response |
|----------|-----------------|----------|
| Inference costs 3x | Total AI COGS moves from $0.163 → ~$0.29/user/month. Small relative to the $2,500 base fee, but the Frontier-tier cascade slice is where the pain concentrates. | Route the 20% cascade slice to a cheaper Mid-tier model temporarily; use bank-partner volume as leverage in an enterprise pricing renegotiation. |
| Heaviest segment doubles | COGS scales roughly linearly with usage-based revenue, so margin % mostly holds — the real bottleneck is broker capacity (human-in-the-loop), not model cost. | Add volume-tiered base pricing to recover infra/support cost, and prioritize the Correction Loop fix from M2 so broker review load doesn't grow with false positives. |
| Model provider raises prices 50% | COGS moves from $0.163 → ~$0.20/user — negligible against a $2,500 base fee, since inference is a small fraction of total cost (human-in-the-loop dominates). | Absorb it short-term; use the breathing room to fund the Kill-Switch abstraction-layer work flagged as "Locked" in M2, so a future shock isn't survived on margin alone. |

## Board One-Pager
<!-- Before/After: Old SaaS revenue vs. AI usage revenue for your product -->

**Before (traditional SaaS):**
Revenue: $2,500/mo base + $150 × 8 bound policies/mo (~$1,200) = ~$3,700/mo per partner
COGS: ~$600/mo fixed ops (no AI)
Gross margin: ~84%

**After (AI-enabled):**
Revenue: $2,500 base + $0.75 × 400 flagged/claimed leads (~$300) + $150 × 14 bound policies (better-targeted leads lift bind rate, ~$2,100) = ~$4,900/mo per partner
COGS: $600 fixed ops + $163 AI COGS (~1,000 active accounts) = ~$763/mo
Gross margin: ~84.4%

**Net margin shift:**
Net margin shift: Margin % barely moves (84% → 84.4%) — the story isn't margin expansion, it's gross dollars per partner up ~32% ($3,700 → $4,900), driven by AI improving lead quality and bind rate, not by extracting more per unit. Narrative for the board: AI doesn't make this a higher-margin product, it makes it a bigger one — script that distinction explicitly, per the module's own warning that lower margin % is fine if NRR and gross dollars are up.
