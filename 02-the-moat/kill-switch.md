# Kill Switch Audit

## Vendor Dependency Assessment

| Dimension | Current State | Risk Level | 48-Hour Action |
|-----------|--------------|------------|---------------|
| **Provider** |Single-provider — Azure OpenAI, the default choice given bank partners are frequently already Microsoft shops. | H  | Not fixable in 48 hours — this is the audit's core finding, not a quick patch.|
| **Abstraction** |Direct API calls in product code — gap-detection logic and broker-facing copy generation both call the provider SDK directly. | H | Stand up a thin internal interface (generateGapFlag(), draftBrokerSummary()) so product code stops calling the SDK directly — decouples the call site without needing a new provider yet.|
| **Routing** |No routing layer — one model handles both gap-detection inference and broker-copilot text generation, no fallback path. | H |Identify one lower-cost/open-weight model as a documented fallback candidate — a manual failover plan beats none. |
| **Eval** |Informal — spot-checked broker feedback, no automated quality bar. | H | Pull 20–30 recent flagged gaps and their broker outcomes into a starter golden set — the seed of a real eval harness.|

## Portability Score
Locked

## If [Azure] doubles pricing tomorrow:
<!-- No real 48-hour response exists yet — that's the finding, not a plan to soften it. Margin compresses immediately since M3's cost assumptions were built on current pricing with no negotiating leverage and no qualified fallback provider to threaten switching to. Given Coverage Gap Advisor already runs on thin per-lead economics, several bank partnerships likely go unprofitable before the next contract renewal even arrives. The honest 48-hour move is damage control, not a switch: pull usage-volume reporting to see which partner relationships are most exposed, and open a pricing conversation with Microsoft from a position of having nowhere else to go. -->

## If [Azure OpenAI] ships a competing product:
This isn't hypothetical — it's the exact scenario already war-gamed as the 90-Day Encroachment Plan, where Microsoft is the named attacker bundling Verisk-backed coverage insight into Copilot for Financial Services. What's defensible and can't be replicated by bundling a model into a suite: the licensed-broker relationship and the compliance/regulatory standing that comes with actually being a licensed insurance agency — Microsoft has no interest in owning that regulatory surface. The sharper way to say it out loud in the room: VIU would be running its product on the infrastructure of the same company positioned to make that product obsolete, and the only thing that survives a Copilot bundle is proof — measurably better bind rates from the human-broker handoff — not the AI layer itself.
