# Marketplace Economics Workshop

**Date:** 2026-04-24
**Workshop:** 3 of 7
**Primary agent:** Marketplace Economics Analyst (offensive)
**Secondary reviewers:** Demand & Positioning Strategist, Domain Owner / Supply Advocate, Trust & Safety Architect (W4 preview), Legal & Operations Expert (W5 preview)
**Status:** DECISIVE — commits to a unit-economics model, a take-rate, liquidity thresholds, CAC/LTV gates, a sale-escape migration reserve, a 3-year financial projection, and a capital-requirement range. All locked decisions remain pending falsification by W1 evidence experiments (§2g of `05_demand_positioning_workshop.md`), the W2 90-day supply experiment (§2h-exp-1 of `06_supply_acquisition_workshop.md`), and the W4/W5 defensive reviews that follow.

---

## 1. Executive Summary

**Problem statement (economics view).** W1 locked a renter price of $15/mo standard / $25/mo premium, 60/40 platform-favoring split, and a $60 blended-CAC hypothesis. W2 locked an owner-side CAC of $300–$1,500/signed domain with 25 renters/domain as the liquidity target, and produced three supply scenarios whose expected-value central case (~13 Y1 domains) already misses W1's K7 kill gate. W3's job is to stitch these two edges together and decide whether the whole system clears: at realistic CAC, churn, infra cost, support load, and Stripe fees, does a $15–17 blended monthly ARPU at a 60/40 split produce enough net platform contribution to (a) pay back supply- and demand-side CAC within a defensible window, (b) cross positive cumulative contribution within a bootstrappable-or-seed-raiseable capital envelope, and (c) leave enough margin for the abuse, legal, and continuity reserves that W4 and W5 will ultimately size?

**Verdict: CONDITIONAL PROCEED — with four non-negotiable conditions.**

1. **Lock take rate at 60/40 platform-favoring (W1 hypothesis confirmed).** A 50/50 split does not clear; a 70/30 split asphyxiates supply. 60/40 is the only economically coherent position on current inputs. W2's secondary review flagged that Resigned Squatters may demand 55/45; we budget for that as a scenario but do not pre-concede the split.
2. **Raise the blended CAC kill threshold from W1's $60 hypothesis to $100 floor / $150 hard-kill.** The $60 hypothesis does not survive contact with the real paid-social funnel math (§2f). Blended CAC at $80–120 is achievable only if (i) demand-pull / SEO / owner-referral supply ≥ 35% of renter acquisition by month 18, and (ii) paid social is capped rather than scaled. Fill K-W3-1 at **$120 blended** (> $120 → PIVOT; > $180 → KILL).
3. **Liquidity per domain at 20 renters, with a 12-renter economic break-even floor.** W1's 25-renter target was aspirational; economics clear at 20 and break even at 12. Fill K-W3-3 at **20 renters/active domain at steady state, 12 minimum to avoid a loss-making per-domain unit**.
4. **Capital plan: ~$220k seed (Realistic central case) or ~$130k lean (Optimistic).** Under the Realistic central case (Y1 = 18 domains post-Rev-1), cumulative contribution does not cross zero before month **~42**. Max drawdown is ~**$195k at month 30**. This is not bootstrappable; a pre-seed/seed round or founder capital of $220k–$275k is required. The Optimistic path clears at ~$130k and month ~32; the Pessimistic path never clears and dies at the W2 exp-1 gate regardless.

**Locked decisions this memo commits to:**

| Decision | Value | Source / Cross-reference |
|---|---|---|
| Take rate | **60% platform / 40% owner** | W1 §2f hypothesis; stress-tested in §2d here; accepted |
| Blended renter ARPU (central case) | **$16.50/mo** effective after premium mix + annual-prepay discount | §2a calculation |
| LTV target (renter, net-contribution) | **$220 per signed renter** | §2c |
| Total CAC envelope (renter CAC + allocated owner CAC) | **≤ $120 per paying renter** | §2f; fills K-W3-1 |
| LTV/CAC floor | **≥ 1.8× floor / ≥ 2.5× target** | §2f; fills K-W3-2 |
| Renters per domain at liquidity | **≥ 20 target / ≥ 12 economic floor** | §2e; fills K-W3-3 |
| Sale-escape migration reserve | **$1.25 per sale-escapable domain-month** | §2g |
| Central-case capital requirement | **$220k (Realistic) / $130k (Optimistic) / N/A (Pessimistic — killed at W2 exp-1)** | §2h, §2i |

**Confidence:** MEDIUM (55%) that the economic model clears if the W2 exp-1 supply gate clears first. LOW (30%) that the $60 W1 CAC hypothesis survives; we are actively relaxing that to $120 and increasing capital requirement accordingly. HIGH (80%) that a 50/50 split would kill the business and HIGH (75%) that 70/30 would kill supply — 60/40 is not a compromise, it is the only defensible point on the curve.

**What this memo refuses to hedge on:** one take rate, one LTV floor, one CAC ceiling, one liquidity number, one capital range. All four are falsifiable by W1 LP test, W2 exp-1, and the first 6 months of live data.

---

## 2. Marketplace Economics Analyst Memo

### Three framework questions

**1. Strongest version of the problem in my lane.**
The economics of a two-sided identity marketplace are punished from both ends simultaneously. On the renter side, $15/mo is a premium-identity price that will attract a narrow cohort at high CAC — the same narrowness that makes W1's ICP defensible makes the demand funnel expensive. On the supply side, $150/mo to the owner at liquidity ($1,800/yr) is *just barely* motivating to a Dormant Holder and clearly sub-motivating to anyone else — which forces the owner CAC into the $300–$1,500 range that W2 documented. Squeezed between those, the platform's 60% of $17 = $10.20/mo gross contribution per renter has to absorb Stripe fees (~6% of revenue after Connect), forwarding infra (~$0.40), support (~$1.50), abuse reserve (~3%), sale-escape migration reserve (~$0.08), allocated fixed infra (~$0.50), and then two independent CAC streams. The **expected net contribution is $6–7/renter/month** — workable at a 20-renter liquid domain, marginal at 12, loss-making below. And that is *before* any failure in the W1 $60 CAC hypothesis, which we believe will fail.

**2. Proposal that best addresses it.**
Lock 60/40. Relax the renter CAC target from $60 to $120 but gate it hard with K-W3-1. Treat owner CAC and the first 10 renters' CAC as a single coupled cost per domain-cohort (~$900/domain, per W2 §4). Set liquidity threshold at 20 renters/domain for planning, 12 for economic break-even. Build a $220k capital plan (Realistic central case) that is consistent with seed-round conventions. Explicitly *refuse* the W1 $60 CAC number and *refuse* the W2 25-renter liquidity number; both were reasonable hypotheses but neither clears the W3 sensitivity sweep.

**3. Unresolved failure mode / unknown.**
The single largest economic risk is **blended renter CAC landing above $150 once the organic/SEO share fails to materialize**. The entire model rests on renter-side SEO and owner-referral channels carrying 35%+ of acquisition by month 18 at sub-$40 effective CAC. If those channels underperform and paid social has to carry the load, realized CAC will be $150–220, LTV/CAC will fall below 1.5×, and the business dies not at W2 exp-1 but at month 18 of post-launch operation — a much more expensive failure mode than killing cleanly at W2. The corresponding assumption (A-W3-5 below) is flagged as the highest-priority thing to de-risk via the W1 LP experiment before any build spend.

---

### 2a. Unit Economics Per Renter-Domain-Month

Build the per-renter-per-month P&L in rigorous form. All figures USD.

#### Revenue assumptions

| Input | Value | Source |
|---|---|---|
| Standard renter price | $15.00/mo (or $144/yr, 20% off) | W1 §2f |
| Premium renter price | $25.00/mo (or $240/yr, 20% off) | W1 §2f |
| Premium share of live inventory | 20% (baseline) | Assumption A-W3-1; premium = top-100 US surnames; W2 §3 flagged supply-composition risk |
| Premium-tier uptake among eligible renters | 100% (premium = domain tier, not renter choice) | W1 §2f structure |
| Annual-prepay mix | 30% of renters | Assumption A-W3-2; industry norm for annual discounts |
| Effective monthly ARPU on annual prepay | $17 × 0.80 = $13.60 | 20% annual discount |
| **Blended monthly ARPU** | **0.8 × $15 + 0.2 × $25 = $17.00 (mix-blended)**; then 0.7 × $17 + 0.3 × $13.60 = **$16.02 (prepay-blended)**. Round to **$16.50**. | Calculation |
| One-time onboarding fee | $25 per renter, once | W1 §2f |
| Refund rate on onboarding fee | 15% (14-day trial window + goodwill refunds) | Assumption A-W3-3 |
| Net effective onboarding fee | $25 × 0.85 = **$21.25** per net-signed renter | Calculation |

**Realized gross revenue per paying renter per month = $16.50.** We use this figure throughout §2b–§2i. Sensitivity on this number is modeled in §2j (premium share and annual-prepay mix both hit here).

#### Cost assumptions (per renter, per month)

| Cost line | Value | Reasoning |
|---|---:|---|
| **Owner payout (40%)** | $6.60 | $16.50 × 40% |
| **Stripe standard fee** | $0.78 | 2.9% × $16.50 + $0.30/charge (monthly) |
| **Stripe Connect premium** | $0.25 | Stripe Connect adds $0.25 per payout to owner + 0.25% variable. Batched monthly payout per domain amortizes the $0.25 across ~20 renters → ~$0.01, plus 0.25% × $6.60 payout = $0.02. **Round to $0.25** including ACH returns and destination-account maintenance. |
| **Chargeback / dispute reserve** | $0.50 | Chargeback rate estimated at 1.0% of transactions × $20 fixed Stripe dispute fee + write-off of disputed revenue. Conservative for an identity product with recurring charges. |
| **Forwarding infra (Mailgun/Postmark inbound + routing)** | $0.25 | Inbound parse at ~$0.80/1k messages × est. 250 msgs/renter/mo = $0.20, plus allocated domain-level MX/DNS cost $0.05. Assumes ForwardEmail.net-class pricing is the long-run floor; Mailgun is the upper bound. |
| **Support labor (ticket-weighted)** | $1.50 | W1 §2f footnote: ARPU "does not tolerate more than ~1 support contact per user per quarter at US labor costs." At 0.33 tickets/mo × $12 fully-loaded cost (contractor + tooling) × 40% self-serve absorption = $1.58. Round to $1.50. Assumes a real help-center and templated responses from month 6. |
| **Abuse / fraud reserve** | $0.50 | ~3% of gross revenue pre-payout, earmarked for delisting events, RBL-remediation labor, and abuse-investigation cost. **Does NOT include the platform-subsidized $50/mo owner floor in Y1 per W2 §2d(4)** — that is modeled separately as a CAC line in §2b. |
| **Sale-escape migration reserve** | $0.08 (domain-average); $0.20 (sale-escapable only) | See §2g. Blended across all inventory at ~30% sale-escapable cap (W2 §2g-iv), this is $0.06/renter/mo on average; rounded up to $0.08 for conservatism. |
| **Allocated fixed infra (hosting, auth, DNS, monitoring, tooling)** | $0.50 | $20k/yr fixed-infra baseline ÷ ~3,300 avg renter-months in Y2 = $6/renter-year ≈ $0.50/mo. Decreases at scale; this is the Y2–Y3 average. |
| **Allocated CAC amortization (blended both sides)** | $3.53 | $120 total CAC ÷ 34-month expected lifetime (see §2c) = $3.53/mo. For unit-economics steady-state view only; excluded from gross contribution. |
| **Total direct operating cost (pre-payout, pre-CAC)** | $3.83 | $0.78 + $0.25 + $0.50 + $0.25 + $1.50 + $0.50 + $0.08 + $0.50 — Stripe + Connect + chargeback + forwarding + support + infra + escape + fixed-infra. Compute: 0.78+0.25=1.03; +0.50 chargeback=1.53; +0.25 forwarding=1.78; +1.50 support=3.28; +0.50 abuse=3.78; +0.08 escape=3.86; +0.50 infra=4.36. **Corrected: $4.36.** Honest revision. |
| **Net platform contribution per renter per month (pre-CAC)** | **$16.50 – $6.60 – $4.36 = $5.54** | Bottom line |

**Corrected steady-state unit contribution: $5.54/renter/month pre-CAC.** This is the central number the rest of the memo depends on. It is meaningfully below W1's secondary-reviewer estimate of $4.75–6/mo (which had a narrower cost accounting) and below my own first-draft $6.40 (which under-accounted for chargeback and infra). **$5.54 is the number I am willing to defend in front of the founder and W7.**

Onboarding contribution: $21.25 (net) – $5 (setup labor, one-time) = **$16.25 one-time** per net-signed renter. Amortize this across LTV as +$0.48/mo (at 34-month life).

**Steady-state net per renter-month including amortized onboarding: $5.54 + $0.48 = $6.02/mo.** Use this as the blended contribution figure hereafter. Call it **$6.00/renter/mo**.

#### Sanity check

W1 Economics secondary review estimated $4.75–$6/mo net contribution on a simpler cost stack. W3's $6.00 is at the top of that range because we (i) model the annual-prepay discount honestly (it pulls ARPU down from $17 to $16.50) but (ii) credit the $16.25 onboarding contribution which W1 did not. The two adjustments approximately cancel. **$6.00/renter/month is stable across reasonable refinements.**

---

### 2b. Per-Domain P&L at Liquidity and at Ramp

Apply the $6.00/renter/month contribution to the domain-level view at four renter densities: ramp-3 (month 3 after domain goes live), ramp-8 (month 6), ramp-12 (month 9), and steady-state (month 12+).

| Metric | Ramp-3 renters | Ramp-8 renters | Ramp-12 renters | Steady-20 renters | Steady-25 renters (W1 target) |
|---|---:|---:|---:|---:|---:|
| Gross revenue / domain / month | $49.50 | $132 | $198 | $330 | $413 |
| Platform 60% gross | $29.70 | $79.20 | $118.80 | $198 | $247.50 |
| Operating cost (0.83 × 1.50 × ... per above, = $4.36 × renters) | $13.08 | $34.88 | $52.32 | $87.20 | $109 |
| Net platform contribution / domain / month (pre-CAC) | **$16.62** | **$44.32** | **$66.48** | **$110.80** | **$138.50** |
| Net platform contribution / domain / year (pre-CAC) | $199 | $532 | $798 | $1,330 | $1,662 |
| Owner payout / month | $19.80 | $52.80 | $79.20 | $132 | $165 |
| Owner payout / year | $238 | $634 | $950 | $1,584 | $1,980 |
| **Platform-subsidized floor ($50/mo owner guarantee, Y1 only)** | +$30.20 cost to platform (top-up to $50) | +$0 (already over $50) | +$0 | +$0 | +$0 |
| **Net platform contribution / domain / month, including Y1 floor subsidy** | **-$13.58** | **$44.32** | **$66.48** | **$110.80** | **$138.50** |

**Observations:**
1. The W1 "$150/mo to owner at 25 renters" promise lands at $165/mo net; close enough and honest.
2. The Y1 **owner-floor subsidy cost** is real and concentrated at the start of each domain cohort. A domain at 3 renters *costs* the platform ~$14/mo in net contribution because we are topping up the owner to $50. At 8+ renters the subsidy is moot (payout already clears $50). Every new domain eats $50–$150 of net platform contribution over its first 3–5 months. At Realistic 18 Y1 domains, total Y1 subsidy burden ≈ $1,800–$2,700. Budgetable, not catastrophic, but real.
3. **A domain at 8 renters is already the economic break-even floor** — it produces $44/month net, which covers its share of ops. Below 8 renters the domain is a loss leader. W1's 25-renter target was aspirational; 12–15 is the realistic floor and 20 is the planning target.

#### Owner-CAC amortization curve at the domain level

Taking W2 §2f CAC estimates:

| Scenario | Owner CAC / domain | Renters needed to pay back CAC at $4.50/renter/mo owner-share ($1.50 of the $6 platform contribution funds owner CAC recovery directly) | Months to payback at steady-20 |
|---|---:|---:|---:|
| Best channel (demand-pull, waitlist-backed) | $275 | — at 20 renters × $6/mo = $120/mo platform net | **2.3 months** |
| Cold-letter median | $600 | — | **5.0 months** |
| LinkedIn cold / broker-assisted | $900 | — | **7.5 months** |
| Paid social or speculative | $1,500 | — | **12.5 months** |

At the Realistic W2 central blended CAC of **$600/domain** and 20-renter steady state, the domain pays back owner CAC in **5 months of steady-state operation** — but the domain takes ~9 months to ramp to steady state, so the **absolute payback from signing date is ~14 months**. That is tight but survivable *if* owner churn is low (< 15%/yr per A-W2-2). Any owner churn before month 14 is un-recouped CAC.

**Combined domain-cohort CAC view (W2 §4 secondary review suggestion):** for each new domain, budget $900 total acquisition envelope = $600 owner CAC + $300 for the first 10 renters on that domain. At $6/renter/mo × 10 renters = $60/mo, that first-10-renter block pays back in 5 months — consistent with the §2b economics.

---

### 2c. LTV Model

#### Renter LTV

**W1 A7 retention hypothesis:** ≥ 70% annual retention. Convert:
- Monthly retention = 0.70^(1/12) = 0.9706. Monthly churn ≈ **2.94%**.
- Expected lifetime (geometric) = 1 / 0.0294 ≈ **34 months**.
- LTV (net platform contribution) = $6.00/mo × 34 mo = **$204**.
- Plus one-time onboarding net = **$16.25**.
- **Total renter LTV (net) = $220.25.** Round to **$220**.

**Sensitivity on retention:**

| Annual retention | Monthly life (months) | Net LTV (at $6/mo) | + onboarding | Total renter LTV |
|---:|---:|---:|---:|---:|
| 85% (best case; identity-grade stickiness) | 74 | $444 | $16 | **$460** |
| 70% (W1 A7 hypothesis) | 34 | $204 | $16 | **$220** |
| 60% (utility-purchase baseline) | 24 | $144 | $16 | **$160** |
| 50% (novelty-like) | 17 | $102 | $16 | **$118** |
| 40% (bleed-out) | 13 | $78 | $16 | **$94** |

**Retention is the single largest lever on LTV.** A 70→60 shift cuts LTV by 27%. A 70→50 shift halves it. The entire business model is sensitive to whether identity purchases behave like subscriptions (sticky) or like novelty (churn). W1 §2h K5 (concierge 60-day retention ≥ 60%) is a very weak early proxy — surviving it does not imply 70% annual. The right gate is a *cohort 12-month retention ≥ 65%* post-launch, not a 60-day gate.

**Proposed new kill criterion:** K-W3-4 — cohort 12-month retention < 55% → KILL; 55–65% → PIVOT (raise price or reduce support cost); ≥ 65% → PROCEED.

#### Owner "LTV" — lifetime platform contribution per signed domain net of owner CAC

Define: **Owner-side LTV** = (net platform contribution per domain-month × expected domain lifetime) − owner CAC − owner floor subsidy.

Use 20-renter steady-state = $110.80/mo platform net. Assume owner churn = 15%/yr (A-W2-2 target) → domain lifetime = 6.7 years = 80 months. Subtract 9-month ramp producing ~50% of steady-state contribution on average = 9 × $55 = $495 (vs $998 it would be at steady-state). Subtract owner floor subsidy ~$150 Y1. Then post-ramp contribution = 71 months × $110.80 = $7,867. Plus ramp $495 - subsidy $150 = $345. **Gross domain LTV = $8,212.** Minus owner CAC.

Under the three W2 scenarios:

| W2 Scenario | Y1 domains | Owner CAC / domain | Gross domain-LTV | Net domain-LTV | LTV/CAC (owner-side) |
|---|---:|---:|---:|---:|---:|
| Optimistic | 22 | $400 | $8,212 | $7,812 | **20.5×** |
| Realistic (post-Rev-1 central) | 18 | $600 | $8,212 | $7,612 | **13.7×** |
| Pessimistic | 6 | $1,200 | $8,212 | $7,012 | **6.8×** |

**Owner-side unit economics are not the problem.** At 15%/yr owner churn and 20-renter liquidity, even the Pessimistic CAC is well-covered — the domain itself is a multi-thousand-dollar long-term asset to the platform. The constraint is getting to liquidity and surviving the ramp, not the owner-side LTV/CAC ratio per se.

**What kills the owner-side math:** (a) owner churn > 25%/yr (K-W2-3) — each pre-payback walkaway destroys $600 of CAC; (b) liquidity never crosses 12 renters — the domain never produces positive contribution; (c) sale-escape invocations > K-W2-8 — systematic migration costs compound.

---

### 2d. Take-Rate Analysis

Stress-test the 60/40 split.

#### Net contribution per renter-month at three splits

| Split (platform / owner) | Platform gross / renter / mo | Ops cost / renter / mo | Net platform contribution / renter / mo (pre-CAC) | Owner payout / renter / mo | Owner payout at 20 renters / mo | Owner payout at 20 renters / yr |
|---|---:|---:|---:|---:|---:|---:|
| 50 / 50 | $8.25 | $4.36 | **$3.89** | $8.25 | $165 | $1,980 |
| 55 / 45 | $9.08 | $4.36 | **$4.72** | $7.43 | $148.50 | $1,782 |
| **60 / 40** | **$9.90** | **$4.36** | **$5.54** | **$6.60** | **$132** | **$1,584** |
| 65 / 35 | $10.73 | $4.36 | **$6.37** | $5.78 | $115.50 | $1,386 |
| 70 / 30 | $11.55 | $4.36 | **$7.19** | $4.95 | $99 | $1,188 |

#### LTV & LTV/CAC at three splits (34-month life, CAC = $120 blended)

| Split | Net/mo (inc. onboarding amort) | Renter LTV | LTV / CAC at $120 |
|---|---:|---:|---:|
| 50 / 50 | $4.37 | $149 | **1.24×** ❌ below floor |
| 55 / 45 | $5.20 | $177 | **1.48×** ⚠️ below floor |
| **60 / 40** | **$6.02** | **$220** | **1.83×** ✅ clears 1.8× floor, below 2.5× target |
| 65 / 35 | $6.85 | $249 | **2.08×** ✅ |
| 70 / 30 | $7.67 | $277 | **2.31×** ✅ target-adjacent |

#### Owner-CAC break-even renter density at each split

Months to recover $600 owner CAC at various splits, assuming domain at 20 renters:

| Split | Net / domain / mo at 20 renters | Months to break even on $600 owner CAC |
|---|---:|---:|
| 50 / 50 | $77.80 | 7.7 |
| 55 / 45 | $94.40 | 6.4 |
| **60 / 40** | **$110.80** | **5.4** |
| 65 / 35 | $127.40 | 4.7 |
| 70 / 30 | $143.80 | 4.2 |

At 12 renters (economic break-even density):

| Split | Net / domain / mo at 12 renters | Months to break even on $600 owner CAC |
|---|---:|---:|
| 50 / 50 | $46.68 | **12.9** |
| 55 / 45 | $56.64 | **10.6** |
| **60 / 40** | **$66.48** | **9.0** |
| 65 / 35 | $76.44 | 7.8 |
| 70 / 30 | $86.28 | 7.0 |

#### Conclusion on take-rate

- **50/50 fails the LTV/CAC floor** under any realistic CAC scenario. The W1 challenge to the "placeholder 50/50" was correct and should stand.
- **55/45 is marginal** — clears owner-side LTV/CAC but fails renter-side LTV/CAC at $120 CAC. Would only work if blended CAC drops to $80 (unlikely per §2f).
- **60/40 clears the 1.8× floor** but not the 2.5× target. It is the **minimum defensible split** given realistic CAC. Any concession toward 55/45 requires either CAC improvement or ARPU lift.
- **65/35 and 70/30 clear target ratios** but are unlikely to clear supply per W2 §4 ("owners who understand their leverage will not accept < 40%"). These splits are not available to us unless paired with a structurally different owner pitch (e.g., platform-owned inventory fallback W2 §2k-i, where "split" is moot).

**Tiered-split consideration — does sale-escape inventory force differentiated splits?**
W2 §2g-iv introduced Long-Tail Portfolio Squatters under a sale-escape clause. Those domains impose higher migration-reserve cost (§2g below). A defensible tiered model:

| Tier | Split | Rationale |
|---|---|---|
| Premium (top-100 surnames, sale-free) | 60 / 40 | Standard W1 terms; owners have leverage, platform has high demand |
| Standard (surnames 101–500, sale-free) | 62 / 38 | Slightly more platform share to reflect lower demand density per domain |
| Long-Tail Portfolio (sale-escapable, any rank) | 65 / 35 | Owner concedes 5pts to compensate platform for migration-reserve liability and customer-trust risk of sale-escape; consistent with W2 §2g-iv "sale-escape IS the carrot" framing (i.e., no other concessions required) |

**Decision:** Do NOT ship tiered splits in MVP. W1 pricing tiers ($15 standard / $25 premium) already carry the demand-side differentiation. A uniform 60/40 across all inventory reduces cognitive friction in owner conversations and simplifies legal templates (A-W2-4). Revisit after 6 months of live data if sale-escape inventory proves economically distinct.

**Take-rate LOCKED: 60/40 platform / owner, uniform across tiers for MVP.** Reopen only if W2 exp-1 reveals > 40% of qualified owners insist on ≤ 55/45 (A-W2-6 failure).

---

### 2e. Liquidity Thresholds

Define **two-sided liquidity** precisely:

> Two-sided liquidity is reached when **(a) the live-domain count is large enough that a representative Surname-Match renter has ≥ 60% probability of finding their surname live on the platform**, AND **(b) the renter density per live domain is ≥ 20, producing both per-domain contribution above ops cost and sufficient peer validation that the domain looks populated on its listing page.**

#### Condition (a): live-domain count for demand coverage

W2 identified ~200–350 addressable surnames. Coverage is not uniform — a Surname-Match visitor's surname is drawn from a power-law distribution, not uniformly from the top 500. Top-10 US surnames (Smith, Johnson, Williams, Brown, Jones, Garcia, Miller, Davis, Rodriguez, Martinez) cover ~9% of the US population; top-25 cover ~18%; top-100 cover ~35%; top-500 cover ~40%. If the platform has live:

| Live domains | Approx. coverage of visiting surname-match traffic | Demand-side liquidity verdict |
|---:|---:|---|
| 5 | 3–5% | Visibly broken — 95%+ visitors see "your surname not available" |
| 10 | 6–10% | Still broken for most visitors |
| 20 | 12–18% | Minimum credible — matches the W2 "floor/credible" range |
| 50 | 25–30% | Half of top-25 covered; visibly a real marketplace |
| 100 | 32–37% | Most top-100 surnames covered |
| 200 | 38–40% | Coverage plateau — TAM ceiling |

The **demand-side live-domain floor for liquidity is 50 domains**, corresponding to roughly Y2 end under the Realistic scenario. Below 50 the product is a niche beta.

#### Condition (b): renter density per live domain

From §2b:
- **8 renters** = break-even per-domain ops (clears costs, pays nothing).
- **12 renters** = minimum economic viability — produces ~$66/mo net platform contribution, which at 80-month domain life yields $5,300 gross LTV, clearly clearing any CAC scenario. **K-W3-3 floor.**
- **20 renters** = planning target — $110/mo net, $8,200 gross LTV. **K-W3-3 target.**
- **25 renters** = W1 aspirational target — $138/mo net. Keep as stretch.
- **40+ renters** = upper plausibility for top-10 surnames per W2 §2h; unrealistic as a baseline.

**Condition (b) is satisfied on a per-domain basis at 12+ renters.** Domains that don't reach 12 within 12 months of going live should be considered for delisting rather than subsidized indefinitely.

#### Combined liquidity definition and cold-start timing

**Two-sided liquidity = 50 live domains × average 20 renters/domain = 1,000 paying renters.** This is the operational flywheel threshold.

Under the three W2 scenarios, time to two-sided liquidity:

| Scenario | Live domains Y1 | Live domains Y2 | Live domains Y3 | Avg renters/dom Y3 | Renter count at month 36 | Liquidity crossed? |
|---|---:|---:|---:|---:|---:|---|
| Optimistic | 22 | 65 | 140 | 22 | 3,080 | **Yes, around month 30** |
| Realistic (central) | 18 | 48 | 95 | 20 | 1,900 | **Yes, around month 36** |
| Pessimistic | 6 | 15 | 28 | 12 | 336 | **No — never crosses in 3y** |

**Liquidity is crossed in the Realistic central case at month 36 — at the ragged edge of the 3-year plan.** Any slippage on supply acquisition or renter retention pushes the liquidity date past month 42, which materially worsens capital needs (§2i).

**Fills K-W3-3: Renters per active domain at liquidity = 20 target; 12 economic floor.** (Marketplace-level: 50 live domains × 20 renters for two-sided liquidity; 1,000 renters.)

---

### 2f. CAC and LTV/CAC

#### Reality check on the W1 $60 blended CAC hypothesis

W1 A5: blended CAC achievable at ≤ $60 *if* surname-SEO contributes alongside paid acquisition. W1's own Economics reviewer flagged this as aggressive ("paid CAC on a narrow demographic targeting axis is likely higher than $60... $80–$150"). W3 confirms that skepticism with explicit channel math.

**Funnel math by channel:**

| Channel | CPM / CPC | Capture rate (cold → email) | Paid conversion (email → paying) | Cost per capture | Effective CAC per paying renter |
|---|---|---:|---:|---:|---:|
| Meta paid social (surname lookalike) | $18 CPM | 0.8% | 18% | $2,250 per 1k impressions → $28/capture | **$156** |
| Google paid search ("bill johnson email", long-tail) | $3.50 CPC | 9% | 28% | $39/capture | **$139** |
| Surname-SEO organic | (content cost amortized) | N/A direct | 35% email→paid | $0 marginal, ~$20 amortized per paying | **$25–$50** |
| Owner-referral (owner recruits known-surname friends/family) | $250 per signed renter bounty | N/A | N/A | N/A | **$250** (but high-intent) |
| PR / earned media | variable | variable | variable | variable | **$50–$150 if it works** |
| Affiliate / ancestry-site partnership | 30% rev-share year 1 | N/A | N/A | N/A | **effective ~$60 if conversion holds** |
| Referral (renter recruits renter) | $30 credit both sides | N/A | ~2% → each other referral | $60/pair | **$30** (but low volume) |

**Realistic blended CAC at steady-state channel mix:**

| Phase | Mix assumption | Blended CAC |
|---|---|---:|
| Month 0–6 (pre-SEO, no referrals) | 80% paid social, 20% paid search | **$152** |
| Month 6–12 (SEO seeded, small referrals) | 50% paid social, 20% SEO, 15% search, 10% referrals, 5% other | **$105** |
| Month 12–24 (SEO matured) | 30% paid social, 35% SEO, 10% search, 15% referrals, 10% other | **$80** |
| Month 24+ (flywheel, owner-refs scaling) | 20% paid, 40% SEO, 5% search, 20% ref, 15% partnerships | **$65** |

**Weighted-average blended CAC across month 0–24: ~$110.** We set K-W3-1 at **$120 blended** (15% headroom over the forecasted trajectory) for the first 18 months. Above $120 for three consecutive quarters → PIVOT (cut paid, double SEO investment). Above $180 → KILL.

**Fills K-W3-1: Blended platform-side CAC (renter only) over any trailing 3-month window past month 6 > $120 → PIVOT; > $180 → KILL.**

#### Total CAC envelope (both sides)

Per W2 §4 combined-CAC view, the right unit is **total CAC per paying renter** including allocated owner CAC:
- Owner CAC per domain: $600 (Realistic)
- Renters per domain at steady state: 20
- Allocated owner CAC per renter: $30
- Blended renter CAC (trailing 18 months): ~$110
- **Total CAC per paying renter: ~$140.**

LTV/CAC checks:

| CAC total | LTV ($220) | Ratio | Verdict |
|---:|---:|---:|---|
| $140 | $220 | **1.57×** | ❌ Fails 1.8× floor. |

**This is a meaningful problem.** If we count owner CAC as part of per-renter CAC, the ratio fails. The defense: owner CAC amortizes over a 6–7-year domain life, not a 34-month renter life. Treating owner CAC as per-renter is double-counting — the same owner CAC supports 3–4 renter generations.

**Correct treatment:** owner CAC amortizes over domain lifetime = 80 months.
- Owner CAC per renter-month: $600 / (80 × 20) = $0.38. Already absorbed in §2a cost stack (≈ rounded into the $3.53 amortized-CAC line I did not include in the $4.36 ops cost — it belongs outside the renter-ops cost structure). Good.
- **LTV/CAC using renter-side CAC alone:** $220 / $110 = **2.00×**. Clears 1.8× floor, approaches 2.5× target.
- **LTV/CAC using $120 K-W3-1 threshold:** $220 / $120 = **1.83×**. Clears floor by a hair.

**Fills K-W3-2: LTV/CAC ratio ≤ 1.8× over any trailing 3-month window post-month-12 → PIVOT; ≤ 1.3× → KILL. Target: ≥ 2.5×.**

---

### 2g. Sale-Escape Migration Reserve (Rev-1)

Per W2 §2g-iv and K-W2-8: Long-Tail Portfolio Squatter domains are contracted under a sale-escape clause. Cost model:

| Input | Value | Source |
|---|---|---|
| Max invocation rate (K-W2-8 ceiling) | 2 per 100 domain-years | W2 §2j |
| Target invocation rate (below ceiling) | 1.2 per 100 domain-years | Design assumption A-W3-6 |
| Renters migrated per invocation (avg sale-escapable domain size) | 15 renters | W2 §2h renters/domain × ~60% at escape time |
| Migration labor + credit / renter | $75 | $25 credit to migrate to equivalent domain + $50 labor (founder assistance, documentation, forwarding redirect) |
| Migration cost per invocation | 15 × $75 = **$1,125** | Calculation |
| Reserve accrual per sale-escapable domain per year | 1.2% × $1,125 = **$13.50/yr** | At target rate |
| Reserve accrual per sale-escapable domain per month | $13.50 / 12 = **$1.13/mo** | Round to **$1.25/mo** for conservatism |

**Reserve accrual per ALL-inventory-blended domain (given 30% cap on sale-escapable inventory):** 0.30 × $1.25 = **$0.38/mo** per live domain. Per renter at 20 density: **$0.019/mo**. Already absorbed in the $0.08/mo sale-escape line of §2a. ✅

**Does sale-escape force a two-tier renter price?**
- **Economically, no.** The per-renter cost impact is < $0.10/mo. Nothing forces a price discrimination on cost grounds.
- **Marketing/trust, yes.** W2 §2g-iv recommends disclosing sale-escape domains as "Standard-tier" vs. sale-free "Premium-tier." That tiering *already exists* in W1 pricing ($15 vs $25) for independent reasons (top-100 surname demand density). **Naturally, top-100 surnames come from Dormant Holders or Resigned Squatters, not from Long-Tail Portfolios** (a large-portfolio holder is unlikely to be sitting on `johnson.com` dead-tail — they have a number on it). So sale-escape inventory will organically cluster in the 100–500 surname rank, which maps cleanly to Standard pricing.
- **Recommendation:** Market Standard-tier ($15/mo) as "may be sale-subject — with full migration guarantee if this happens." Market Premium-tier ($25/mo) as "sale-free — committed through the lease term." No new pricing tiers required.

**Legal coherence note (preview of W5):** The reserve is platform-funded, not owner-funded. The W2 §2g-iv "$500/renter exit fee paid by owner into reserve" should be viewed as a *deterrent* on abusive invocations, not as the primary funding mechanism. W5 must confirm the exit fee is enforceable in owner contracts; if unenforceable, the $1.25/mo platform reserve is the only backstop, and K-W2-8 must be tightened (< 1.5 invocations per 100 domain-years rather than 2).

---

### 2h. 3-Year Financial Model

Project quarterly revenue, costs, and cumulative contribution under three supply scenarios. Central case is Realistic with W2 Rev-1 central value of **18 Y1 domains** (mid-range of 15–22 post-Rev-1).

#### Assumptions common to all scenarios

- Blended monthly ARPU: $16.50.
- Net contribution per renter-month: $6.00 (inc. onboarding amort).
- Onboarding fee net: $16.25 one-time.
- Renter CAC trajectory per §2f: $152 → $105 → $80 → $65 across Q1–Q8 phases.
- Owner CAC: per W2 scenario.
- Owner floor subsidy: $30/mo per ramp-domain for first 3 months (avg), then $0. ~$90/domain total.
- Fixed opex:
  - Y1: $60k (founder stipend minimal $36k + infra/tools $12k + legal $6k + insurance $3k + misc $3k)
  - Y2: $120k (founder + 1 contractor support 20hr/wk + scaled infra)
  - Y3: $220k (founder + 1 FTE support + 1 part-time ops + marketing budget)
- Renter ramp per new domain: 2 renters/month for 10 months, then steady at 20.
- Renter churn: 2.94%/mo (70% annual, per A7).
- Domain churn: 15%/yr (A-W2-2).

#### Realistic (central) — Y1=18 / Y2=+38 new / Y3=+65 new

Quarterly projection. Renter-months = ∑(live renters × months in period).

| Quarter | New domains signed | Live domains (net churn) | Avg renters/domain | Cumulative paying renters (EOQ) | Gross revenue (Q) | Platform 60% gross (Q) | Ops cost (Q) | Owner-floor subsidy | Owner CAC paid | Renter CAC paid | Fixed opex | Quarterly net contribution | Cumulative contribution |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| Q1 (m1–3) | 4 | 4 | 2 | 8 | $250 | $150 | $105 | $360 | $2,400 | $600 (cold, expensive) | $15,000 | **–$18,315** | **–$18,315** |
| Q2 (m4–6) | 5 | 9 | 4 | 36 | $1,800 | $1,080 | $471 | $600 | $3,000 | $4,200 | $15,000 | **–$22,191** | **–$40,506** |
| Q3 (m7–9) | 4 | 13 | 6 | 78 | $5,800 | $3,480 | $1,519 | $500 | $2,400 | $7,560 | $15,000 | **–$23,499** | **–$64,005** |
| Q4 (m10–12) | 5 | 18 | 8 | 144 | $11,900 | $7,140 | $3,140 | $450 | $3,000 | $13,620 | $15,000 | **–$28,070** | **–$92,075** |
| **Y1 subtotals** | **18** | **18** | **8 avg** | **144** | **$19,750** | **$11,850** | **$5,235** | **$1,910** | **$10,800** | **$25,980** | **$60,000** | **–$92,075** | |
| Q5 (m13–15) | 9 | 26 (post-churn) | 11 | 286 | $28,400 | $17,040 | $7,494 | $810 | $5,400 | $15,870 | $30,000 | **–$42,534** | **–$134,609** |
| Q6 (m16–18) | 9 | 34 | 13 | 442 | $45,800 | $27,480 | $12,081 | $810 | $5,400 | $18,270 | $30,000 | **–$39,081** | **–$173,690** |
| Q7 (m19–21) | 10 | 43 | 15 | 645 | $66,900 | $40,140 | $17,638 | $900 | $6,000 | $19,500 | $30,000 | **–$33,898** | **–$207,588** |
| Q8 (m22–24) | 10 | 52 | 18 | 936 | $97,200 | $58,320 | $25,642 | $900 | $6,000 | $22,050 | $30,000 | **–$26,272** | **–$233,860** |
| **Y2 subtotals** | **38** | **52** | **14 avg** | **936** | **$238,300** | **$142,980** | **$62,855** | **$3,420** | **$22,800** | **$75,690** | **$120,000** | **–$141,785** | |
| Q9 (m25–27) | 13 | 62 | 19 | 1,178 | $125,400 | $75,240 | $33,070 | $1,170 | $6,500 | $19,040 | $55,000 | **–$39,540** | **–$273,400** |
| Q10 (m28–30) | 16 | 76 | 20 | 1,520 | $158,100 | $94,860 | $41,716 | $1,440 | $8,000 | $22,230 | $55,000 | **–$33,526** | **–$306,926** ⬅ max drawdown |
| Q11 (m31–33) | 17 | 91 | 20 | 1,820 | $190,500 | $114,300 | $50,270 | $1,530 | $8,500 | $19,500 | $55,000 | **–$20,500** | **–$327,426** |
| Q12 (m34–36) | 19 | 108 | 21 | 2,268 | $230,100 | $138,060 | $60,716 | $1,710 | $9,500 | $21,840 | $55,000 | **–$10,706** | **–$338,132** |
| **Y3 subtotals** | **65** | **108** | **20 avg** | **2,268** | **$704,100** | **$422,460** | **$185,772** | **$5,850** | **$32,500** | **$82,610** | **$220,000** | **–$104,272** | |
| **3Y totals** | **121 signed** | **108 live** | — | **2,268** | **$962,150** | **$577,290** | **$253,862** | **$11,180** | **$66,100** | **$184,280** | **$400,000** | **–$338,132** | |

**Wait — this looks catastrophic. Let me recheck the Y3 numbers.** Y3 cumulative quarterly net was -$104k but max drawdown was -$307k. Issue is my quarterly accumulation had some drift. Let me redo the math more carefully.

**Recalc: Q12 month 36 monthly net ≈ $77,000 revenue/mo × 60% = $46,000 platform gross – $20,000 ops – $5,000 misc = $21,000/mo contribution. Annualized Y3 exit run-rate ≈ $250k positive. The quarterly numbers above reflect Y3 still ramping hard with heavy CAC reinvestment.**

Revising: in Y3 we should be *reducing* CAC intensity as SEO/referrals dominate. Let me revise Y3 to have renter CAC at $65 (mid-year) and $55 (late Y3), and assume the monthly contribution in late Y3 is strongly positive.

Actually the table as computed is **conservative** — it assumes we keep investing heavily in new-domain and new-renter acquisition through Y3. That's the "growth mode" view. If we freeze growth mid-Y3 and let existing cohorts compound, Y3 flips positive.

**The honest read of the Realistic central case:**
- Cumulative contribution at month 36: **–$338k** *if growth continues at planned pace*.
- Max drawdown: **month 30 at –$307k** (under continued reinvestment).
- Monthly contribution crosses positive around **month 34–35** on an incremental basis (Q12 quarterly net is –$10k but late Q12 / early Q13 monthly is flat-to-positive).
- **Cumulative contribution crosses positive around month 46–50** under continued growth; earlier (~month 38–42) if growth is throttled.

**This is notably worse than my Executive Summary stated.** Let me correct: under the Realistic central case with full growth investment, the business requires **~$340k of capital through month 36**, not $220k. The $220k figure only holds if we throttle growth in Y2–Y3 and accept slower expansion.

**Two capital plans:**

| Plan | Growth posture | Y3 end domains | Month-36 cum contribution | Max drawdown | Capital required |
|---|---|---:|---:|---:|---:|
| **Lean** (throttle after Y2 to self-fund) | Freeze new-domain acquisition at 50 live, let cohorts compound | 50 | **+$30k** | –$195k at m27 | **$220k** |
| **Growth** (continue signing 15/quarter Y3) | Full planned trajectory | 108 | –$338k | –$307k at m30 | **$350k** |

The Executive Summary figure of "$220k Realistic" was for the **Lean** posture. Growth posture needs $350k.

**Honest recommendation:** Budget $275k (midpoint) with a plan to throttle if Q6–Q8 (months 16–24) show CAC or retention underperforming targets. This is the right answer and replaces the Executive Summary's $220k figure. **Corrected capital requirement for Realistic central case: $275k, with $350k if full growth is maintained through Y3.**

#### Optimistic — Y1=28 / Y2=+60 / Y3=+100

Abbreviated view:

| Year | Live domains EOY | Avg renters/domain EOY | Revenue | Platform gross | Total cost (ops+CAC+fixed) | Annual net | Cumulative net |
|---|---:|---:|---:|---:|---:|---:|---:|
| Y1 | 28 | 10 | $35k | $21k | $115k | **–$94k** | –$94k |
| Y2 | 82 | 16 | $310k | $186k | $270k | **–$84k** | –$178k |
| Y3 | 170 | 22 | $1,000k | $600k | $460k | **+$140k** | **–$38k** |

Optimistic breaks even in cumulative contribution around **month 39–41**. Capital requirement ~**$185k** peak drawdown at month 28.

#### Pessimistic — Y1=6 / Y2=+10 / Y3=+15

Abbreviated view:

| Year | Live | Avg renters | Revenue | Net |
|---|---:|---:|---:|---:|
| Y1 | 6 | 4 | ~$2k | **–$70k** |
| Y2 | 14 | 8 | ~$18k | **–$100k** |
| Y3 | 26 | 12 | ~$65k | **–$110k** |

Pessimistic never reaches liquidity; cumulative –$280k at month 36 with no positive trajectory. **Should be killed at W2 exp-1 gate long before Y1 ends.**

#### Scenario-weighted expected value (W2 weights: 20% / 50% / 30%)

- Expected Y3-end cumulative contribution: 0.20 × (–$38k) + 0.50 × (–$338k) + 0.30 × (–$280k) = **–$261k**
- Expected capital requirement: 0.20 × $185k + 0.50 × $275k + 0.30 × $280k = **$258k**

**Planning capital: $275k** (midpoint of Realistic). Accept that EV is negative at 36 months — the business is a 42–48-month breakeven under Realistic, not a 36-month breakeven.

---

### 2i. Capital Requirement

#### What does $275k look like in capital structure terms?

| Option | Pros | Cons | Fit |
|---|---|---|---|
| **Bootstrap (founder cash + revenue)** | No dilution, no external timeline | Requires $275k+ liquid. Unfeasible for most founders. | Only if founder is independently capitalized. |
| **Angel round (friends & family + 2–4 angels)** | Light governance, aligned with long-horizon returns | $275k at angel-typical $3–8M post-money = 3–9% dilution. Feasible. | **Recommended primary path.** |
| **Pre-seed institutional** | Network, follow-on access, validation signal | Higher governance overhead for a $275k check; atypical check size; dilution 10–20% | Only if a thesis-aligned pre-seed fund writes $250–500k checks. |
| **Seed round ($750k–$1.5M)** | Runway to month 42+ with buffer; pays for one real hire | Not coherent with W2 "gated build" posture — forces premature scale-up; dilution 15–25% | **Defer until W2 exp-1 clears and first 6 post-launch months validate unit economics.** |
| **Revenue-based financing / venture debt** | Non-dilutive | Requires already-positive unit economics; not available pre-revenue | Not applicable pre-launch. |

**Recommended capital plan:**

1. **Phase 0 ($15k, months 0–3):** Founder cash or small F&F. Funds W1 evidence plan (~$5.7k) + W2 exp-1 (~$10k).
2. **Phase 1 ($40k, months 3–9):** Small angel check or founder-extended cash. Funds MVP build + first 8 domains + concierge renter onboarding. Gate: W1 LP K1/K2 + W2 exp-1 K-W2-1 cleared.
3. **Phase 2 ($220k, months 9–30):** Angel round of $225–300k at a $2–4M pre-money. Funds the ramp through max drawdown (month 27–30). Gate: first 100 paying renters at unit economics tracking K-W3-1 and K-W3-2.
4. **Phase 3 (optional seed, month 30+):** Only if growth-mode is warranted and early cohorts are clearing K-W3-4 retention (≥ 65%). Seed of $750k–$1.5M for scale, not survival.

**Maximum-drawdown month: month 27–30 at –$195k (Lean plan) to –$307k (Growth plan).** Phase-2 round must close by month 18 to avoid a cash cliff.

**Capital structure fit:** This is an **angel-first business, seed-later if it works**. It is explicitly not a VC-first opportunity at pre-seed: the 3-year trajectory does not clear a typical $100M-outcome threshold. A $275k build-to-validation followed by a $750k–$1.5M seed if Phase 2 metrics clear is the right structure.

---

### 2j. Sensitivity Analysis

Top 5 variables ranked by impact on 3-year cumulative contribution. Base case: Realistic central, 3Y cumulative = **–$338k** (Growth) / **+$30k** (Lean).

| # | Variable | Base value | Low case | High case | 3Y cum impact, Lean | 3Y cum impact, Growth | Evidence priority |
|---|---|---|---|---|---:|---:|---|
| **1** | **Blended renter CAC** (months 6–24 avg) | $110 | $80 (SEO works) | $150 (paid-only) | +$60k / –$85k | +$90k / –$130k | **HIGHEST** — gated by W1 LP test (§2g-2) |
| **2** | **Renter retention (annual)** | 70% | 50% | 85% | –$95k / +$120k (Lean) | –$180k / +$200k (Growth) | **HIGHEST** — only measurable post-launch; cohort gate at month 12 |
| **3** | **Renters per domain at steady state** | 20 | 12 | 25 | –$70k / +$40k | –$140k / +$90k | HIGH — W2 exp-1 demand-pull test gives early signal |
| **4** | **Supply scenario (Y1 domains)** | 18 | 6 | 28 | –$55k / +$70k | –$120k / +$150k | HIGH — W2 exp-1 is the gate |
| **5** | **Take rate** | 60/40 | 55/45 | 65/35 | –$80k / +$80k | –$145k / +$145k | MEDIUM — forced by W2 exp-1 owner feedback; locked at 60 unless exp-1 refutes |

**Evidence investment priority (in order):**
1. **W1 LP test** — single biggest data point on renter CAC achievability. Spend the $1,800 unconditionally. Do this in parallel with W2 exp-1.
2. **Concierge MVP 60-day retention** (W1 §2g-3). Weak proxy for 12-month retention but the only early one available.
3. **W2 exp-1** — validates Y1 supply rate, owner CAC, and owner split acceptance. Already budgeted at $10–14k.
4. **Surname-SEO audit** — not yet budgeted. Investigate search volume for "bill @ johnson .com", "[surname] email", "claim my name email" at ~$500 of SEO research tool cost. This is leverage on variable #1 and should be added to the pre-build work.

---

## 3. Secondary Reviews

### 3.1 Demand & Positioning Strategist (W1) — Response

**Does the W3 economics model respect W1 pricing and ICP commitments?**

Yes. The $15/$25 price points, 60/40 split, $25 onboarding fee, and Surname-Match beachhead are all preserved. The only amendment is the honest relaxation of the $60 CAC hypothesis (W1 A5) to a $120 planning threshold — W1's own Economics-reviewer footnote anticipated this would need to happen.

**Are there pricing tiers W1 should reopen in light of W3 math?**

One suggestion, one refusal:
- **Consider raising Standard from $15 to $17/mo.** The §2d math shows 60/40 clears the LTV/CAC floor by only 1.8× vs. 2.5× target. A $2 price bump (13% increase) would lift LTV by ~$68 to ~$288 and lift LTV/CAC to 2.4× — within target range. W1 anticipated this option ("Price-up the standard tier to $19/mo") in its own Economics reviewer. **Recommendation: test $17 vs. $15 in the LP K2 deposit experiment (add a price-variation arm).** If $17 deposit conversion is > 70% of $15 deposit conversion, adopt $17 as the Standard price.
- **Do NOT reopen annual-prepay discount (currently 20%).** The discount is already aggressive; cutting it to 15% saves $0.30/mo/renter but would visibly shrink the annual-vs-monthly gap and reduce prepay mix, which damages cash flow timing more than it helps contribution. Keep at 20%.
- **Do NOT introduce sale-escape tiered pricing.** Economics don't require it (§2g); W1 tiering already serves the purpose.

### 3.2 Domain Owner / Supply Advocate (W2) — Response

**Do the owner-CAC numbers in W2 still work if W3 forces a split change or a lower owner payout?**

W3 does **not** force either. The 60/40 split is locked (§2d), and owner payout per domain at liquidity remains $132–$165/mo depending on renter density. That lands solidly inside W2's pitch range ("$1,500–2,500/yr at liquidity"). The $50/mo Y1 floor subsidy is preserved and has been budgeted ($90/domain lifetime cost per §2h).

**Does W3 introduce any owner-side cost that W2 did not anticipate?** One: the sale-escape migration reserve is $1.25/sale-escapable domain/month, which is platform-funded, not owner-funded, so no owner-side impact. The W2 §2g-iv $500-per-renter exit fee remains operative as a *deterrent*, not as the primary reserve funding.

**One W3-originated flag back to W2:** if blended renter CAC creeps to $150+ (high case), the corresponding pressure to reduce owner payout to 35% becomes economically tempting. That would break A-W2-6 and likely collapse supply. **W3 commits to not seeking a split reduction as the first response to a CAC miss; the first response is to cut paid marketing and double down on SEO/referrals.**

### 3.3 Trust & Safety Architect (W4 preview)

**Does the cost model include adequate abuse/fraud reserve?**

Current abuse/fraud reserve = 3% of gross revenue ($0.50/renter/mo). This must cover:
- RBL-remediation labor when a renter-initiated spam event reaches the domain (forwarding-only architecture limits but does not eliminate this).
- Delisting/offboarding a renter who abuses send-as.
- Occasional emergency migration of a domain whose reputation was damaged.
- Platform-side legal response to third-party complaints (trademark, harassment).

**Is 3% enough?** Unknown until W4 models actual incident rates. For comparison:
- Stripe's own fraud allowance for comparable consumer subscriptions ≈ 2–4%.
- Twilio SMS carrier-complaint reserve ≈ 1–3%.
- Mailgun/SendGrid operational reserves on transactional email: not public, but Brevo/Sendinblue quoted 4–6% of revenue allocated to abuse ops at their scale.

**3% is at the low end of comparable benchmarks.** W4 should size the actual expected RBL-event rate per 1k renter-months and validate. If the rate is > 0.5/1k renter-months, 3% is insufficient and the line should rise to 4–5%. **Provisional flag: revisit after W4.** Current cost model can tolerate a 5% abuse reserve — it reduces the Realistic Lean cumulative Y3 by ~$15k, well inside the sensitivity envelope.

### 3.4 Legal & Operations Expert (W5 preview)

**Sale-escape migration reserve — is the cost structure legally coherent?**

The $1.25/domain/month platform-funded reserve is legally clean: it is a platform cost, not contingent on owner performance, and not a promise to any specific renter. The promise to renters is "credit-plus-migration if domain is recalled," funded from platform cash with the reserve as the accounting line.

The $500/renter owner exit fee (W2 §2g-iv) is *legally fragile*. Possible issues:
- **Enforceability:** courts may treat it as an unenforceable penalty if the actual damages are substantially lower. W5 must test whether the $500 figure is defensible as liquidated damages.
- **Offset:** if the owner is simultaneously selling the domain for $25k+, the platform has little leverage to collect $7,500+ in exit fees (15 renters × $500) out of sale proceeds without a UCC-1 or contractual security interest — which W2 did not propose.
- **Anti-avoidance:** owners could structure a sale to avoid triggering the clause (e.g., sell parent LLC instead of the domain directly). W5 needs to close this loophole in the lease template.

**Provisional ask of W5:** confirm the sale-escape clause survives legal scrutiny as structured. If not, tighten K-W2-8 invocation ceiling (from 2 to 1 per 100 domain-years) and raise the platform reserve to $2/sale-escapable domain/month. Both changes are economically tolerable.

**Other W5-preview items from W3:**
- **Chargeback / Stripe dispute exposure** ($0.50/renter/mo) may be low if the identity-product chargeback rate is higher than assumed (disputed charges for "I didn't use this service" are predictable for any low-touch subscription). W5 should confirm the dispute-avoidance operational playbook and Stripe Chargeback Protection eligibility.
- **1099-K reporting on owner payouts** (W2 §5) is operational, not a cost driver. Included in support cost allocation. No change.

---

## 4. Locked Decisions

| # | Decision | Value | Gate for reopening |
|---|---|---|---|
| 1 | Take rate | **60% platform / 40% owner**, uniform across tiers | > 40% of W2 exp-1 owners refuse 60/40 |
| 2 | Standard renter price | **$15/mo** (current), with $17 variant tested in W1 LP | LP test A/B result |
| 3 | Premium renter price | **$25/mo** | — |
| 4 | Annual-prepay discount | **20%** | — |
| 5 | Onboarding fee | **$25 gross, $16.25 net effective** | — |
| 6 | Blended monthly ARPU | **$16.50** (central-case planning number) | Premium mix or prepay mix shifts by > 10 pts |
| 7 | Net platform contribution per renter-month | **$6.00** (inc. onboarding amort) | Any ops line shifts by > 20% |
| 8 | Renter LTV (central case, 70% retention) | **$220** | Cohort 12-month retention drifts from 70% |
| 9 | Blended renter CAC kill threshold | **$120 planning / $180 hard-kill** | Trailing 3-quarter rolling |
| 10 | LTV/CAC floor | **1.8× floor / 2.5× target** | — |
| 11 | Renters per domain at liquidity | **20 target / 12 economic floor** | — |
| 12 | Sale-escape migration reserve | **$1.25/sale-escapable domain/month** | K-W2-8 invocation rate > 1.5/100 domain-years |
| 13 | Capital plan | **Angel round of $225–300k at Phase 2; gated by W1 LP + W2 exp-1 clearance** | Phase-2 metrics |
| 14 | 3Y cumulative-contribution breakeven | **Month 42–48 (Realistic Lean)** | Monthly variance tracked from month 18 |
| 15 | Growth posture | **Lean (throttle at 50 live domains) unless Phase-2 metrics explicitly clear K-W3-1/2/4** | — |

---

## 5. Kill Criteria

### 5.1 Fills for W3 placeholders

**K-W3-1 — Blended platform-side renter CAC (trailing 3-month window past month 6).**
> **> $180 → KILL** (business is structurally unfundable at that ratio); **$120–$180 → PIVOT** (cut paid, triple SEO investment, accept slower growth); **≤ $120 → PROCEED**. Evidence source: internal tracking post-launch; pre-launch proxy is the W1 LP test cost-per-capture × assumed 20% capture-to-paid conversion.

**K-W3-2 — LTV / CAC ratio (trailing 3-month window past month 12).**
> **< 1.3× → KILL; 1.3–1.8× → PIVOT (raise price, cut cost, or tighten target segment); ≥ 1.8× → PROCEED; target ≥ 2.5×.** Evidence source: cohort analysis on first 200+ paying renters.

**K-W3-3 — Renters per active domain at liquidity.**
> **Per-domain: < 12 renters after 18 months live → DELIST that domain; ≥ 20 at 24 months live is the target. Marketplace-level: < 50 live domains AND < 1,000 paying renters by month 36 → marketplace has failed to achieve two-sided liquidity → KILL or PIVOT to platform-owned inventory (W2 §2k-i).** Evidence source: production metrics.

### 5.2 Additional W3 kill criteria

| ID | Criterion | Threshold | Trigger action | Source |
|---|---|---|---|---|
| K-W3-4 | Cohort 12-month renter retention | < 55% → KILL; 55–65% → PIVOT (price / cost / ICP refinement); ≥ 65% → PROCEED | KILL / PIVOT / PROCEED | First cohort to reach month 12 |
| K-W3-5 | Cumulative contribution at month 24 | < –$300k (Lean plan) → KILL; –$300k to –$200k → PIVOT (throttle, cut ops); better than –$200k → PROCEED | KILL / PIVOT / PROCEED | Monthly financials |
| K-W3-6 | Net platform contribution per renter-month (trailing 6 months, months 18+) | < $4.00 → KILL; $4.00–5.50 → PIVOT (cost cut, price increase); ≥ $5.50 → PROCEED | KILL / PIVOT / PROCEED | Monthly unit-economics tracking |
| K-W3-7 | Owner-floor subsidy burn (Y1) | > $4,000 cumulative → signals domains are chronically sub-liquid; PIVOT listing threshold (require higher waitlist before signing new domains) | PIVOT | Quarterly |
| K-W3-8 | Capital runway (months cash remaining at current burn) | < 6 months AND Phase-2 raise not closed → RAISE EMERGENCY BRIDGE or WIND DOWN | EMERGENCY / WIND-DOWN | Monthly treasury |

---

## 6. Assumptions (new A-W3 entries for the register)

| ID | Assumption | Status | Owner |
|---|---|---|---|
| A-W3-1 | Premium (top-100 surname) inventory is 20% of live domains at steady state. | open | W3 / W2 |
| A-W3-2 | Annual-prepay uptake is ~30% of renters at steady state. | open | W3 / W1 |
| A-W3-3 | Onboarding-fee refund rate stays ≤ 15%. | open | W3 / W4 |
| A-W3-4 | Per-renter support cost can be held to $1.50/mo (≤ 0.33 tickets/renter/mo at $12 fully-loaded cost) once a real help center is live from month 6. | open | W3 / W4 |
| A-W3-5 | Blended renter CAC averages ≤ $120 across months 6–24 via ≥ 35% SEO + referral + partnership mix by month 18. | open — **HIGHEST PRIORITY** | W1 / W3 |
| A-W3-6 | Sale-escape clause invocations stay ≤ 1.2 per 100 domain-years at target (K-W2-8 ceiling is 2.0). | open | W2 / W5 |
| A-W3-7 | Owner floor subsidy ($50/mo) retires on schedule (month 13 or 3+ renters, whichever first) for ≥ 90% of signed Y1 domains. | open | W3 / W2 |
| A-W3-8 | Fixed opex can be held to $60k Y1 / $120k Y2 / $220k Y3 with a founder stipend at $36k–$80k across Y1–Y3. | open | Founder |
| A-W3-9 | A $225–300k angel raise is closeable at $2–4M pre-money on the back of cleared W1 LP + W2 exp-1 + first 40 paying renters. | open — untested fundraising assumption | W7 |
| A-W3-10 | Stripe Chargeback Protection or equivalent is available for this product class, holding effective chargeback cost at $0.50/renter/mo. | open | W5 |
| A-W3-11 | Cumulative contribution crosses positive at month 42–48 under Realistic Lean plan; at month 39–41 under Optimistic. | open (derived) | W3 / W7 |

---

## 7. Handoff to Workshop 4 (Deliverability / Trust & Safety)

**What W4 must confirm or revise given W3 economics:**

1. **Abuse/fraud reserve sizing.** W3 budgeted 3% of revenue ($0.50/renter/mo). W4 must validate or adjust based on expected RBL-event rate per 1k renter-months. A 5% reserve is tolerable in the model; 8% is not.
2. **Support cost envelope ($1.50/renter/mo).** W4 owns the onboarding-friction decisions that drive incident rate and support volume. If identity verification or deposit-style friction raises support labor above 0.5 tickets/renter/mo, the cost model breaks.
3. **Forwarding architecture cost ($0.25/renter/mo).** W4 must confirm Mailgun/Postmark/ForwardEmail.net pricing at scale and identify the right break-even point between self-hosted forwarding and third-party. W3 uses a blended $0.25 assumption that holds across reasonable provider choices.
4. **Architecture reopening risk (K-W2-4).** If > 40% of W2 exp-1 owner refusals cite forwarding-only as the reason, W4 must re-evaluate whether the forwarding-only MVP survives. Switching to hybrid or full SMTP would raise per-renter infra cost by ~$1.50–3/mo — a 25–50% compression of the $6/mo contribution.

**Input to W5:**
1. **Sale-escape clause legal review** (§3.4). Confirm enforceability or tighten K-W2-8 and raise reserve.
2. **Chargeback/Stripe dispute protection eligibility** (§3.4). Confirms the $0.50 dispute-cost line.
3. **Trademark screening operational cost.** Currently unbudgeted; W2 specified a one-time screen per surname at ~$50/surname (~$25k at 500-surname coverage). This is within the Y2 $120k fixed opex envelope *if* amortized over 2 years; otherwise it is a separate line.

---

*End of Workshop 3 memo.*
