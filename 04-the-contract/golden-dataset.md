# Golden Dataset & Reliability Contract — Coverage Gap Advisor
Golden Dataset Spec (10 of ~150 v1 ship target)
## Golden Dataset Spec

| # | Input | Expected Output | Edge Case? | Judge Type |
|---|-------|----------------|-----------|-----------|
| 1 | New auto loan opened, no linked auto policy found for this customer | Flag: comprehensive auto gap, high confidence | N | rule + LLM |
| 2 | New mortgage opened, existing homeowners policy already on file, name/address match | No flag — gap correctly suppressed | N | rule |
| 3 | New auto loan; existing auto policy exists under a slightly different name spelling ("Robert" vs. "Bob") | No flag — fuzzy-match resolves as same customer, not a gap | Y | LLM |
| 4 | Joint account, one owner has an auto policy on file, co-owner does not | Flag: gap on co-owner only, medium confidence, note joint-account ambiguity in explanation | Y | LLM |
| 5 | Existing auto loan paid off this week (loan closed, not opened) | No flag — stale/closed-loan signal, not a "new" trigger  | Y | rule |
| 6 |	Newborn added as dependent, no life insurance policy on file	| Flag: life insurance gap, medium confidence |	N	| LLM |
| 7 |	Commercial auto loan opened under an LLC account	| No personal-auto flag — routed to commercial line instead, scope boundary respected |	Y	| rule |
| 8 |	Customer opted out of insurance marketing contact 30 days ago; new auto loan opened today |	No flag surfaced to broker regardless of underlying gap — compliance override wins |	Y |	rule |
| 9 |	New auto loan flagged; this customer has dismissed 2 prior AI flags as incorrect | Confidence downgraded one tier, routed to review queue instead of auto-surfaced |	Y	| LLM |
| 10 | New mortgage AND new auto loan opened same day, same account | Two distinct gaps identified and ranked separately, not merged into one flag | Y | LLM |

**Adversarial rows included:** _3_ (#3 — identity-match spoofing, #8 — compliance-override bypass, #9 — repeat-dispute trust erosion)
**Coverage gaps identified by partner:** Loan refinances (same vehicle, same customer, new loan ID) were being misread as "new auto, no policy on file" — the model wasn't distinguishing a new-loan event from a refinance event, generating false-positive flags on already-insured customers. Not in the original 10; added after partner pilot feedback, and it's the clearest evidence yet that the Correction Loop (M2, 2/5) needs to close.

**Sales test, one sentence:** "Every flag we surface has been checked against a 150-case golden dataset covering real edge cases our bank partners found in production — including the ones where our own model got it wrong."

## Confidence UX Design

**Approach:** show uncertainty / tiered confidence / human-in-loop trigger
Approach: Tiered confidence with human-in-the-loop trigger at the middle band — not a single pass/fail gate.

**High confidence (>90%):** Auto-routed directly to the broker queue with pre-filled talking points; no additional review gate, but still spot-checked in the weekly accuracy sample.
**Medium confidence (70-90%):** Surfaces to the broker tagged "Review before contact" — the signals and reasoning are shown, but the system doesn't claim certainty, and the broker decides whether it's worth a call.
**Low confidence (<70%):** Suppressed from the broker queue entirely. Logged for pattern analysis, never surfaced as an actionable lead — this is the direct fix for the margin risk flagged in M3 (wasted broker time on low-quality flags eating into the human-in-the-loop cost line).

**User control surface:** Broker can dismiss or downgrade any flag with a reason code (e.g. "already insured," "bad match," "customer declined") — every dismissal is captured and feeds back into the Correction Loop from M2, rather than disappearing.

## Reliability Contract

| Metric | Target | Measurement | Alert Threshold |
|--------|--------|-------------|-----------------|
| Accuracy (flag precision) | ≥85% of claimed leads confirmed correct by broker outcome  | Weekly sample of broker outcome tags (correct/incorrect) | <75% pauses flagging for the affected partner |
| Hallucination rate | <1% of "why this was flagged" explanations contain a signal not actually present in the account data  | LLM-judge audit against source account data, sampled weekly  | >2% triggers immediate freeze on explanation generation |
| Latency (p95) | <3s from account-open event to flag surfaced | Application logging  | >8s p95 triggers infra review |
| Drift velocity | <5% month-over-month shift in flag rate per partner without a matching shift in underlying signal volume | Weekly trend monitoring per partner | >10% shift triggers a model audit before the next cycle |

## HITL Architecture
<!-- When does a human step in? What's the escalation path? -->
**Threshold:** Low (<70%) → never reaches a human, suppressed by design. Medium (70–90%) → mandatory human review before any customer contact. High (>90%) → auto-routed, but a rotating spot-check sample still gets reviewed so "high confidence" doesn't quietly become unaudited.

**Capture fixes:** Every broker dismissal or override — with reason code — writes back into the training/eval pipeline. This is the concrete build against M2's weakest loop (Correction, 2/5): the queue is designed to shrink as the model gets better at avoiding the mistakes brokers keep catching, not stay a permanent babysitting task.

**Escalation UX:** Confidence tier is visible to the broker on every flag, not hidden behind a single "recommended" badge — medium-confidence flags are explicitly labeled as needing review, so trust in the high-confidence tier doesn't erode when a medium one turns out wrong.
## Red-Team Findings
*What failure mode did your partner find that you missed?*

What the partner found that we missed: During pilot, one bank partner's data team noticed AI-flagged gaps firing on customers who had simply refinanced an existing auto loan — same vehicle, same policy already on file — because the model was reading "new loan record" as "new loan event" without checking loan history for a prior linked account. It wasn't a hallucination in the generative sense; it was a signal-definition gap nobody had written a test case for. That finding is now golden-dataset row #5 and the reason the coverage-gaps-identified-by-partner line exists at all — it's a direct, low-drama argument for why the golden dataset has to keep growing from real production misses, not just the cases the team thought to write up front.
