## Feedback Loops

| Loop | Input | Output | Compounds? | Status |
|------|-------|--------|-----------|--------|
| Recursive Learning | Broker dismissal/reason-code data on flagged gaps (accurate, already insured, bad match, not actionable) | Improved flag precision via periodic retraining | N | broken |
| Cross-Domain Transfer | Proxy account signals used separately for auto, home, and life gap types | Intended: a pattern learned improving auto-gap detection also sharpens home/life detection | N | missing |
| Network Intelligence | Aggregate flag/outcome data across all bank and credit union partners | A shared baseline detection model that improves as partner count grows | Y | active |

**Broken loop identified by partner:** Recursive Learning — this is the same loop that let the loan-refinance false-positive ship in the first place (Module 4's red-team finding). The capture mechanism exists; it just doesn't feed anywhere yet.
**Fix plan:** Wire the already-designed broker reason-code capture into the weekly golden-set review as an automated pipeline step instead of a manual one, and turn on the monthly retrain trigger once 5+ new rows accumulate — the threshold was already specified in M4's HITL Architecture, it just needs to actually fire.

## Context Connectivity
<!-- How does knowledge flow across teams and domains? Where does it silo? -->

**How knowledge flows:** Broker feedback currently reaches VIU's product/ops team only through the weekly golden-set review, and that review updates the dataset manually.

**Where it silos:** Between bank partners — an edge case one partner's data surfaces (like the refinance miss) doesn't propagate to other partners' live models until a human manually adds it to the shared golden set and ships a new version. It also silos across gap types — auto, home, and life detection don't share a domain-context layer, so nothing learned in one improves the others.
