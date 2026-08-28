# Data Flywheel Map

> Score each loop 1-5. Your weakest loop is where competitors attack first.
> The four loops below are the M2 starting point - adapt if your product has 2 or 6 loops instead of 4.

## Flywheel Loops

| Loop | What It Measures | Score 1 | Score 5 | Score |
|------|------------------|---------|---------|-------|
| **Correction** | Do users fix AI outputs? Is that signal captured and reused? | No capture | Automated retraining | 2/5 |
| **Preference** | Does the product learn individual / team preferences over time? | Stateless | Deep personalization | 2/5 |
| **Domain Context** | Does usage in one area improve quality in adjacent areas? | Siloed | Cross-domain transfer | 2/5 |
| **Network** | Does each new user / team make the product better for everyone? | Isolated | Strong network effects | 3/5 |

### Correction Loop - 2/5
**What you capture today:** When a broker overrides a flagged gap (e.g. "customer already has coverage elsewhere"), that override closes the case — it doesn't route anywhere for reuse.
**How it compounds:** Without capture, every broker relearns the same false positives their peers already found. With capture, false-positive rate should drop every quarter instead of staying flat.

### Preference Loop - 2/5
**What you capture today:** Some conversion data exists (which offers got accepted) but it isn't fed back into how future households get scored or which gaps surface first.
**How it compounds:** A real loop means each bank partner's customer base starts getting recommendations tuned to what actually converts for that partner's demographics, not a generic model.

### Domain Context Loop - 2/5
**What you capture today:** Relies on the bank's raw account signals (new mortgage, new auto loan) as a proxy for risk — not a proprietary risk corpus.
**How it compounds:** This is the crack a competitor can exploit without needing anything from VIU — they can just buy better risk data (Verisk) elsewhere. The model's accuracy ceiling is set by proxy signal quality, not anything VIU owns.

### Network Loop - 3/5
**What you capture today:** Gap-detection patterns from one bank partner likely inform the model used across other partners, even if informally.
**How it compounds:** More embedded partners should mean better pattern detection for everyone — this is the one loop where scale itself is already doing real work.

**Total Flywheel Score: 9/20**
**Weakest Loop:** Domain Context (tied with Correction and Preference at 2, but Domain Context is the one directly exploitable by an outside data vendor rather than an internal capture fix)
**Fix for weakest loop:** License comparable risk data directly (or negotiate exclusive access to something Verisk-tier data providers don't offer competitors), since this is the only weak loop VIU doesn't fully control the timeline on.

---

## Encroachment Threat Assessment

### 1. Platform Encroachment
**Attacker:** Google (Gemini agentic shopping)
**Vector:** Consumer-facing discovery layer — an agent scans likely coverage gaps from public/inferred signals and pulls live quotes directly, sidestepping any bank's UI.
**Time-to-threat:** 12–18 months
**% of value at risk:** ~30% (erodes the B2C/direct-discovery layer, not the embedded B2B moat)

### 2. Vertical Competitor
**Attacker:** Verisk (or a startup licensing Verisk-tier data)
**Vector:** Domain Context — real household/property risk models (e.g. LightSpeed-style scoring) vs. VIU's proxy signals from bank transaction data.
**Time-to-threat:** 6–12 months
**% of value at risk:** ~40% (erodes prediction accuracy, the actual product)

### 3. Adjacent Expansion
**Attacker:** Q2 / Jack Henry (core banking platform vendors)
**Vector:** Distribution — already the system of record inside the bank's account-opening flow; adding a native coverage nudge costs them almost nothing incremental and removes the bank's reason to pay a third party.
**Time-to-threat:** 18–24 months
**% of value at risk:** ~50% if it happens (replaces VIU's entire embed slot, not just a layer of it)

---

## 90-Day Encroachment Plan

*Your partner played the Big Tech attacker. What was their plan to kill you?*

**Attacker:** Microsoft (Head of Product, Copilot for Financial Services)
**Attack vector (target the weakest loop):** Domain Context — bundling Verisk-backed coverage insight into a product banks already license.
**Weeks 1-4 - what they ship:** Partner with Verisk directly (a deal structure Microsoft already runs in other verticals) and ship a "coverage insight" module inside Copilot for Financial Services. Pilot with two or three existing Microsoft banking customers already on Dynamics 365.
**Weeks 5-8 - how they poach users:** Not users — partners. The pitch to a bank isn't "switch from VIU," it's "you already pay for Copilot, this is one more module, zero new vendor." Easier internal sell than justifying a separate VIU contract, targeted at any bank partner up for renewal in this window.
**Weeks 9-12 - why users don't come back:** It was never a switching decision — it's budget-line consolidation. Once coverage insight lives inside a suite the bank already pays for, there's no annual re-evaluation moment where VIU gets reconsidered; it just falls off the shortlist next renewal cycle.
**Your defense:** Fix the Domain Context loop before this stops being hypothetical — license comparable risk data, or make the case to bank partners now, before their renewal windows, that VIU's advantage is the licensed-broker handoff and the compliance relationship Microsoft has no interest in owning. If Broker Copilot usage can be shown to produce measurably better bind rates than a bare nudge, that's proof a procurement team can't consolidate away.
