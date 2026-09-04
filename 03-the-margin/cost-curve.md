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

**Triage model:**
**Frontier model:**
**Routing rule:**
**Expected cascade ratio:**

## Pricing Model

**Current pricing:**
**Proposed AI pricing:**
**Model:** seat-based / usage-based / outcome-based / hybrid

## Stress Tests

| Scenario | Impact on Margin | Response |
|----------|-----------------|----------|
| Inference costs 3x | | |
| Heaviest segment doubles | | |
| Model provider raises prices 50% | | |

## Board One-Pager
<!-- Before/After: Old SaaS revenue vs. AI usage revenue for your product -->

**Before (traditional SaaS):**
**After (AI-enabled):**
**Net margin shift:**
