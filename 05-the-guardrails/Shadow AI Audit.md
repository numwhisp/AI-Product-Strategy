Shadow AI Audit (user-side), Module 5

## Discover, User-Side Workarounds
- Broker manually cross-checks flagged customer against own CRM notes before acting | source: User interview | signal: Trust gap | freq: H | spend: $$525/mo | decision: Build
- Bank ops team pastes flagged-gap output into ChatGPT to rewrite customer outreach | source: Support ticket | signal: Capability gap | freq: M | spend: $$400/mo | decision: Partner
- Broker runs "why this was flagged" explanation through CRM's built-in AI summarizer | source: User interview | signal: Workflow gap | freq: M | spend: $$0/mo | decision: Ignore
- Ops team manually exports flagged-lead lists to a spreadsheet to track claim status | source: Support ticket | signal: Workflow gap | freq: H | spend: $$420/mo | decision: Build
- Smaller partner's IT team builds a Zapier flow piping flagged leads into their own ticketing system | source: Zapier/Make | signal: Pricing gap | freq: L | spend: $350/mo | decision: TBD

## Pattern Assessment
- Workarounds found: 5
- Build candidates: 2
- Partner candidates: 1
- Ignore decisions: 1
- Adjacent spend: $1695/mo
- Dominant signal: Workflow gap

## Action Plan
### Build
Claim-tracking view across brokers, so ops teams stop maintaining their own spreadsheet — sequence this first, it's the highest-frequency gap. Confidence-score and "why flagged" explanation UI comes second — it's lower urgency than the tracking gap but addresses the highest-trust-risk workaround.

### Partner
Integrate with whatever CRM/comms tool brokers and ops teams already draft in — likely entry point is a lightweight export/webhook so flagged-gap data and "why flagged" context land inside their existing CRM instead of requiring a copy-paste into ChatGPT or a CRM summarizer. Auth and data flow need explicit scoping given this crosses the same compliance boundary flagged in the M5 governance audit.

### Ignore + Monitor
CRM-native AI summarizer restating existing explanations — redundant effort, not a strategic or compliance risk, so no action needed unless usage patterns shift. Re-evaluate the partner Zapier flow next quarter — low frequency today, but it's a pricing-avoidance and data-handling signal worth watching as partner count grows.

## Roadmap Brief
Based on your audit: 5 user-side workarounds discovered.
Decisions: 2 build · 1 partner · 1 ignore · 1 TBD.
Estimated adjacent spend: $1695/mo across surveyed users.
Dominant signal: Workflow gap.

Recommended next step: Workflow gaps dominate, your users are stitching your product into multi-step pipelines. Strongest near-term move is partner integrations with the AI tools they already chain in.

Sequence the Build column by frequency × strategic relevance. Confirm Partner candidates with the external tools' partnership teams. Re-run this audit each quarter, workarounds shift fast.
