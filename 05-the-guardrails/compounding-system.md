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

## Governance Policy

**Scope:**
**Autonomy boundaries:**
**Escalation triggers:**
**Audit cadence:**
**Regulatory exposure (EU AI Act / other):**

## Agent Topology
<!-- If using agents: what can each agent do? What can't it do? Who approves what? -->

## Shadow AI Audit

| Tool | Owner | Risk Level | Decision |
|------|-------|-----------|----------|
| | | H / M / L | keep / govern / kill |
| | | H / M / L | keep / govern / kill |
| | | H / M / L | keep / govern / kill |

**Total tools found:**
**Tools after triage:**
**Estimated hidden spend:**
