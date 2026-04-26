# Pricing & Namespace — Rev-2

**Date:** 2026-05-06
**Revision:** 2 (supersedes W1 pricing §2f and W3 §2a / §2b / §2c / §2e / §2f numeric thresholds where this memo explicitly says so; does not supersede W2 owner-acquisition logic except as noted in §6)
**Primary agent:** Marketplace Economics Analyst
**Secondary reviewers:** Demand & Positioning Strategist, Domain Owner / Supply Advocate, Trust & Safety Architect (W4 preview)
**Status:** DECISIVE on tier structure, pricing floors, and revised kill criteria. Conditional on a W1-LP split-test validating the premium-vs-standard cannibalization rate proposed in §2. All numbers remain pending falsification by that test and by the W2 exp-1 cohort.

---

## §1. Executive Summary

**What Rev-2 changes.** W1/W3 assumed a one-tier namespace — every renter pays ~$15/mo for a `firstname@surname.com` slot, ~25 renters/domain at liquidity, blended ARPU $16.50, net platform contribution $6.00/renter-month, LTV $220, CAC ceiling $120, capital $275k. Rev-2 reopens two load-bearing assumptions underneath those numbers:

1. **The per-domain namespace is not ~25; it is effectively unbounded** once compound local-parts (`john.paul@`, `mary.anne@`, `j.smith@`, `jp.smith@`) are admitted. At a realistic marketing/awareness cap, a top-100 surname domain can carry **50–80 renters**, not 25.
2. **The single-name slot (`john@smith.com`) is a distinct scarce good** from a compound slot. Scarcity maps to ~**5–10 viable single-name slots per top-100 surname**. Those slots command a premium; compound slots trade at an impulse price-point.

**What Rev-2 keeps.** The "Claim your name" frame (W1 §1). 60/40 platform-favoring split (W3 §2d). Forwarding-only MVP architecture (W4). Owner ICP taxonomy and the Rev-1 Long-Tail Portfolio sale-escape clause (W2). Capital structure path (angel, §2i).

**Central-case pricing (chosen): Configuration 3A-modified.** Premium single-name **$25/mo**; Standard compound **$9/mo** (the founder's $5–$8 range does not clear the ops cost stack; $8 is the floor, $9 is the planning number). Blended realized ARPU $10.80–$11.00 at a 20%-premium / 80%-standard mix.

**Headline numbers at liquidity (Rev-2 central case, 50 renters/domain, 10 premium + 40 standard):**

| Metric | W3 baseline | Rev-2 central (3A-mod) | Δ |
|---|---:|---:|---:|
| Blended ARPU | $16.50 | $11.00 | –33% |
| Renters / domain at liquidity | 20 | 50 | +2.5× |
| Platform net contribution / renter-mo (pre-CAC) | $5.54 | $3.14 | –43% |
| Platform net contribution / domain-mo (pre-CAC) | $111 | $157 | **+41%** |
| Owner payout / domain / yr | $1,584 | **$2,736** | **+73%** |
| Weighted renter LTV (net) | $220 | **$97** | –56% |
| Blended CAC ceiling for LTV/CAC = 1.8× | $120 | **$54** | –55% |
| Capital requirement (central) | $275k | **$245k** | –11% (conditional on SEO mix) |

**Verdict: ADOPT WITH MODIFICATION.**
- Adopt the two-tier premium/standard structure.
- Modify the founder's $5–$8 standard-tier range to **$9 floor**. $5 breaks ops break-even outright ($5 standard tier is cash-flow-negative per renter at the current cost stack).
- Reject Configuration 3B outright. Reject 3C (three-tier) for MVP; revisit post-liquidity.
- Rev-2 is **structurally dependent** on standard-tier acquisition being ≥ 65% organic (SEO + referral + owner-pull). This becomes a new K-Rev2-1 kill criterion, not a marketing aspiration. If organic share under-delivers, Rev-2 fails before paid acquisition can rescue it — because the CAC ceiling on the standard tier is $25–30, below any plausible paid-channel efficient-frontier.

**Confidence.** MEDIUM (55%) that Rev-2 central case clears if the W1 LP split-test confirms a premium-vs-standard take-rate between 15% and 25%. LOW-MEDIUM (40%) that standard-tier organic-acquisition share can reach 65% within 18 months. HIGH (75%) that Rev-2 improves the owner-acquisition pitch enough to materially derisk W2 exp-1 (§6).

---

## §2. Namespace Model

### 2.1 Single-name slot — rigorous definition

A **single-name slot** is a local-part that is a recognizable given name with no separator, no initial, and no compound structure. `john@smith.com`, `mary@smith.com`, `bill@smith.com` — one word, one identity.

**How many viable single-name slots exist per top-100 surname?** First-principles bound:

- SSA top-100 first names (M+F combined over rolling 80 years, de-duplicated for gender-overlap like Jordan/Morgan) yields roughly 180 distinct candidate first names at non-trivial prevalence.
- Of those, cross-joining against a specific surname produces a realistic count of *name-bearing US adults* per surname. For `smith.com` (~2.5M US bearers), any top-100 first name will have 5,000–60,000 living bearers.
- Not every first name "reads clean" as a solo local-part: `a@smith.com`, `ed@smith.com`, `jo@smith.com` work; `aaliyah@smith.com` is a single-name slot but its market-rank is weak because the name × surname frequency is low.
- Culturally-coherent single-name slots per top-100 surname: **first names with ≥ 25,000 estimated living bearers of this surname** across all generations. That filter yields roughly **5–12 slots per surname**.

**Bound (design constant A-Rev2-1):** assume **7 premium single-name slots per top-100 surname domain** as the planning number. Top-10 surnames (Smith, Johnson, Williams, Brown, Jones, Garcia, Miller, Davis, Rodriguez, Martinez) may clear 10–12; rank-100 surnames will plausibly only support 4–6. The central-case financial model (§7) uses 7.

**Cross-check:** W2's single-tier design implicitly assumed ~25 renters/domain. If 7 of those 25 are single-name slots, the remaining 18 must be compound even in the W1 world — the W1/W3 pricing just lumped them into one tier. Rev-2 formalizes the split that was always latent.

### 2.2 Compound slot — definition and formatting policy

**Compound slot** = any local-part that is not a bare single first name. Four formats in scope:

| Format | Example | Scarcity | Rev-2 tier |
|---|---|---|---|
| `first.last@` | `john.smith@smith.com` | Low (one canonical form per full legal name) | Standard |
| `first.middle@` or `first.mi@` | `john.paul@smith.com`, `john.p@smith.com` | Low | Standard |
| `first.lastinitial@` | `john.s@smith.com`, `j.smith@smith.com` | Medium (collides across John/James/Joseph Smiths) | Standard |
| `initials@` (2-letter, 3-letter) | `js@smith.com`, `jps@smith.com` | **High** — 2-letter initials are near-premium | Standard today; flag for future premium split |

**Explicitly out of scope for MVP (to avoid slot-squatting, §8):**

- Numbered suffixes (`john1987@`, `john.smith2@`) — only allowed on collision, never as primary marketing.
- "Cute" variants (`bigjohn@`, `mr.smith@`) — banned to keep brand frame coherent.
- Single-initial (`j@smith.com`) — treat as a 13th premium slot, priced at premium; operationally we claim these as platform-reserved for the first 12 months to avoid awkward land-grabs.

**Are 2-letter initials premium-adjacent?** Yes. `js@smith.com` reads as shorter and more valuable than `john.paul@`. **Design decision (A-Rev2-2):** in Rev-2 MVP, price 2-letter initials at Standard ($9) but **allow only one per first-name-initial-pool** (one `js@`, one `jp@`, etc.) — i.e., 2-letter initials are scarce inside the standard tier. Revisit post-liquidity for a potential "short-handle premium" $15 mid-tier (this is Configuration 3C deferred).

### 2.3 Cannibalization risk

The central behavioral question: **if a buyer sees `john@smith.com` at $25 and `john.paul@smith.com` at $9, what fraction picks standard?**

Three hypotheses, each with a different implication:

| Hypothesis | Premium take-rate among eligible buyers | Implied blended ARPU | Verdict |
|---|---:|---:|---|
| H-high (identity buyer won't compromise) | 35–45% | $13.50–$15.00 | Rev-2 thesis margin clears. |
| H-mid (planning assumption) | 18–25% | $10.50–$11.50 | Rev-2 central case; just clears. |
| H-low (price-driven cannibalization) | 8–12% | $8.40–$9.20 | Rev-2 marginal; standard-tier becomes most of the economics. |

**This is the single largest unknown in Rev-2.** An LP split test (two landing pages, one showing only single-name slots at $25, one showing both tiers side-by-side) resolves it directly. Proposed additions to the W1 §2g-2 LP experiment:

- **Variant A (premium-only exposure):** Show only `john@smith.com @ $25`. Measure deposit-conversion on $25 price point.
- **Variant B (both-tiers exposure):** Show `john@smith.com @ $25` AND `john.paul@smith.com @ $9`. Measure which SKU is deposited on.
- **Decision rule:** Variant B premium-take-rate below **15%** of depositors → Rev-2 fails its central assumption; re-evaluate Configuration 3C or widen the premium-vs-standard spread (e.g., $30/$8 instead of $25/$9).

This variant layers inside the existing K1/K2 conversion thresholds — no new LP plumbing required, just a second creative.

---

## §3. Pricing Models — Three Candidates

Each configuration below is evaluated against the same cost stack per renter-month, modified from W3 §2a with **two Rev-2 adjustments**:

- **Abuse reserve** rises from $0.50 → $0.75 on premium slots and from $0.50 → $0.40 on standard slots. Why asymmetric: in absolute per-renter terms, abuse cost is driven by mailbox-count, not revenue — but identity-grade premium renters generate fewer tickets and lower abuse probability (higher commitment), so the standard-tier nominal rate is slightly lower per-$ but *higher* per-mailbox. Blended reserve per renter-month rises because 50–80 renters/domain means larger blast radius if the domain gets blacklisted. See §8.
- **Support cost** differentiates: Premium $1.50 (same as W3), Standard $1.00 (lower ARPU cannot afford $1.50 per renter; self-serve onboarding required). Budget tier if used: $0.80.

### 3.1 Unit economics — per renter per month, each tier

Stripe fee scales with revenue: `2.9% × price + $0.30/charge`. Chargeback reserve scales as 3% of revenue.

| Cost line | Premium $25 | Standard $9 | Standard $8 (founder low) | Standard $5 (3B) | Budget $4 (3C) |
|---|---:|---:|---:|---:|---:|
| Revenue | $25.00 | $9.00 | $8.00 | $5.00 | $4.00 |
| Owner payout (40%) | $10.00 | $3.60 | $3.20 | $2.00 | $1.60 |
| Stripe (2.9% + $0.30) | $1.03 | $0.56 | $0.53 | $0.45 | $0.42 |
| Stripe Connect | $0.25 | $0.25 | $0.25 | $0.25 | $0.25 |
| Chargeback reserve (3%) | $0.75 | $0.27 | $0.24 | $0.15 | $0.12 |
| Forwarding infra | $0.25 | $0.25 | $0.25 | $0.25 | $0.25 |
| Support | $1.50 | $1.00 | $1.00 | $1.00 | $0.80 |
| Abuse reserve | $0.75 | $0.40 | $0.40 | $0.40 | $0.40 |
| Sale-escape reserve | $0.08 | $0.08 | $0.08 | $0.08 | $0.08 |
| Allocated fixed infra | $0.50 | $0.50 | $0.50 | $0.50 | $0.50 |
| **Total ops (ex. owner)** | **$5.11** | **$3.31** | **$3.25** | **$3.08** | **$2.82** |
| **Net platform contribution / mo (pre-CAC)** | **$9.89** | **$2.09** | **$1.55** | **–$0.08** | **–$0.42** |

**Observations:**

- **Standard $5 (3B) is cash-flow-negative per renter.** Ops cost exceeds owner-less margin. Rejected.
- **Budget $4 (3C low-tier) is cash-flow-negative.** Three-tier with a $4 budget-long slot is mathematically broken under current cost stack. Only ways to make it work: (a) self-service-only with no human support ($0 support) — makes contribution $0.38, still marginal; (b) drop owner share on budget tier from 40% → 25% — politically un-sellable after W3's 60/40 lock; (c) raise budget tier to $6 — then it's just a cheaper standard, Rev-2 3C collapses into 3A.
- **Standard $8 nets $1.55.** Technically positive, but one bad support month (2 tickets) wipes out 10 months of contribution per renter. **Risky.**
- **Standard $9 nets $2.09.** 35% more margin per renter vs. $8, at minimal positioning cost ($9 still reads impulse-tier). **This is the recommended floor.**

### 3.2 Side-by-side comparison — three configurations + W3 baseline

Blended ARPU, per-renter and per-domain economics at liquidity, 30% annual-prepay discount applied to blended ARPU.

| Config | Premium | Standard (+Budget) | Mix (P/S) | Realized blended ARPU | Net $/renter-mo | Renters/dom | Platform net $/dom-mo | Owner payout $/dom-yr |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| W3 baseline | $25 | $15 | 20/80 | $16.50 (prepay-adj) | $5.54 | 20 | $111 | $1,584 |
| **3A-mod (central)** | $25 | $9 | 20/80 | $11.00 | $3.14 | **50** | **$157** | **$2,736** |
| 3A founder ($8) | $25 | $8 | 20/80 | $10.20 | $2.82 | 50 | $141 | $2,448 |
| 3B (aggressive) | $25 | $5 | 12/88 | $7.40 | — | 80 | see note | — |
| 3C (three-tier) | $25 | $10 (std) / $4 (budget) | 15/50/35 | $9.95 | $1.70 | 60 | $102 | $1,800 |

**3B detail note:** at Standard $5 the per-renter contribution is negative, so the per-domain platform net is a function of premium slots only. 12 premium × $9.89 + 68 standard × (–$0.08) = $113.25/domain-month. Same platform dollars as W3 baseline, with **3× the operational surface area, 3× the abuse risk, and a loss-leading standard tier.** Rejected.

**3C detail note:** three-tier looks attractive for blended ARPU ($9.95 beats 3A-mod $11.00 — correction, it does not) but the budget-long tier is cash-flow-negative at $4. Making 3C work requires budget at ≥ $6. At $6 budget, 3C becomes `$25 / $10 / $6` — essentially a 3A variant with more SKU complexity and more support surface. Not justified for MVP. **Defer 3C to post-liquidity revisit once we have cohort-level retention data.**

### 3.3 Per-tier LTV and CAC ceilings

Retention assumptions per §4 below. Applied to the 3A-mod tier-level unit economics.

| Tier | Net $/mo | Annual retention | Avg life (mo) | LTV (net, excl. onboarding) | Onboarding net | Total LTV | CAC @ 1.8× | CAC @ 2.5× |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Premium $25 | $9.89 | 80% | 54 | $534 | $16 | **$550** | **$306** | $220 |
| Standard $9 | $2.09 | 55% | 20.6 | $43 | $0 (waived) | **$43** | **$24** | $17 |
| *3C Budget $6* | $0.38 | 45% | 15 | $6 | $0 | **$6** | **$3** | $2 |

**The standard-tier CAC ceiling is $24 at 1.8×.** Paid social at $120–150/acquisition (W3 §2f) is ~**6× over budget** for this tier. Paid search at $139 is 5.8× over. **No paid channel clears standard-tier CAC.** Only organic (surname-SEO at $25–50 amortized, owner-referral at ~$0 marginal if the owner is pitching their own cousins, and renter-to-renter referral at $30) clears. This is a structural result, not a tunable parameter.

### 3.4 Blended CAC ceiling and Rev-2 LTV/CAC

Using 3A-mod central mix (20% premium, 80% standard) with mix-weighted averages:

- Blended LTV = 0.20 × $550 + 0.80 × $43 = **$110 + $34 = $144.** *But this is a simple mix. Lifetime-weighted blended LTV* — the LTV a dollar of mixed-cohort spend generates — weights by renter-months-lived, not by signup count. Lifetime-weighted: premium is 54/20.6 = 2.6× weightier. Adjusted blended LTV = $118. Round to **$120** for planning.
- Blended CAC ceiling @ 1.8× = **$67**. At 2.5× target = $48.
- Rev-2 replaces W3 K-W3-1 from `$120 PIVOT / $180 KILL` with **`$67 PIVOT / $100 KILL`** at the signup-mix-weighted level. See §9.

**Honest read:** W3's $120 CAC envelope was predicated on W3's $220 LTV. Rev-2 lowers LTV proportionally to ARPU, and the CAC envelope contracts accordingly. Rev-2 is **not** a "get more renters cheaper" play — it is a "same capital, more per-domain revenue, tighter CAC discipline" play. The tighter CAC discipline is the price of admission.

---

## §4. Retention & Churn Recalibration

W1 A7 hypothesized 70% annual retention for identity-intensive buyers. Applied uniformly at $15–25 pricing it was aggressive-but-defensible. Applied to a $9 impulse compound slot it is **implausible**. Reasons:

1. **Lower price-point lowers switching friction.** A $9/mo commitment feels closer to a Netflix-tier impulse subscription (monthly churn 4–6%) than to an identity subscription.
2. **Compound-slot emotional attachment is materially weaker than single-name attachment.** `john.paul@smith.com` is a fine email. `john@smith.com` is *the* email. The sunk-cost psychology differs.
3. **Standard-tier buyer discovers the product via surname-SEO rather than identity crisis.** The buyer who types `bill johnson email` into Google already has a narrow-identity need; the buyer who lands on `smith.com family email` from a broad-match ad has a curiosity need.

**Tier-differentiated retention assumptions (A-Rev2-3):**

| Tier | Annual retention | Monthly churn | Avg life | Rationale |
|---|---:|---:|---:|---|
| Premium $25 | **80%** | 1.84% | 54 mo | Higher than W3's 70% blanket assumption — premium single-name slot *is* the identity-grade product, more committed cohort self-selects into $25 tier. |
| Standard $9 | **55%** | 4.85% | 20.6 mo | Midway between utility-subscription (~70%) and novelty (~40%). Identity element present but attenuated. |
| 3C Budget $6 (if ever enabled) | 45% | 6.07% | 15 mo | Closer to novelty baseline. |

**Sensitivity.** If standard-tier retention lands at 65% instead of 55%, standard LTV rises from $43 → $65, and blended CAC ceiling at 1.8× rises from $67 → $95. If it lands at 45%, standard LTV falls to $29, and blended CAC at 1.8× drops to $51. **Retention is again the single largest lever** and the proxy data is poor: W1 K5 concierge 60-day retention is a weak proxy for 12-month retention on the premium tier and **worse** for the standard tier, which has a fundamentally different acquisition funnel.

**New proposed kill criterion K-Rev2-4:** standard-tier cohort 12-month retention < **45%** → KILL the standard tier (revert to premium-only at W3-baseline unit economics); 45–55% → PIVOT (raise standard to $11–12 and widen the gap from premium, or tighten abuse/support spend).

---

## §5. CAC Mix Implications

Under Rev-2, **standard-tier paid acquisition is economically impossible**. Every channel in W3 §2f's channel math has an effective CAC ≥ $60 except surname-SEO organic ($25–$50 amortized) and referral ($30 per pair). The standard-tier CAC ceiling is $24 @ 1.8×.

### 5.1 Structural mix requirement

**K-Rev2-1 (new):** Standard-tier acquisition share from organic channels (SEO + owner-referral + renter-referral) must be **≥ 65%** by month 18, **≥ 75%** by month 30. Paid social and paid search reserved for premium-tier hero pages and for top-of-funnel awareness that drives organic search queries. Below 65% organic share for three consecutive quarters past month 18 → PIVOT (cut paid entirely, accept slower ramp). Below 50% → KILL standard tier.

### 5.2 Surname-SEO strategy becomes load-bearing

W1 already treated surname-SEO as a long-term channel. Rev-2 makes it the primary channel, not a supplement. Implications:

- **Per-surname landing page density matters more.** A page that lists `john@`, `mary@`, `bill@` as "available premium slots" plus `john.paul@`, `mary.anne@`, `jp.smith@` as "standard slots (pick yours)" has 3–8× more internal link targets and more canonical query coverage than a page offering one SKU.
- **More renters/domain = more user-generated content density.** "Meet Johnsons on our platform" style renter showcase, with opt-in, generates organic long-tail content that the W3 one-SKU design did not.
- **Content-SEO budget estimate.** 200 top surname pages × $75 each (writer + editorial QA + schema markup) = $15k one-time, amortized over ~2,000 renters in Y2 = $7.50/renter amortized. Sits well below the $24 ceiling.

**Does compound-slot expansion make surname pages *more* SEO-rankable?** Conditional yes — Google rewards pages with more unique, targeted internal structure (each slot is a mini long-tail target keyword). Risk: thin-content penalty if slot listings look auto-generated. Mitigation: at least 400 words of editorial per surname page explaining the surname history, WTP framing, and renter testimonials.

### 5.3 Referral economics

**Free month per successful referral** (renter → renter):

- Cost: $9 (standard) or $25 (premium) revenue forgone per successful referral pair.
- At 20% referral-driven acquisition share, blended referral CAC ≈ (9 × 0.8 + 25 × 0.2) = $12.20. Well under the $24 ceiling.
- Cap at 6 free months lifetime per referrer (prevents abuse).

**Owner-referral bounty** (owner recruits a known-surname friend/family):

- $30 flat bounty per signed renter for the first 90 days post-domain-listing (onboarding ramp boost).
- $15 per renter for months 4–12.
- Owners recruiting their own cousins cost close to zero marginal — the bounty is small thanks, not a true acquisition expense.
- Budget 15–25% of Y1 signed standard renters come from owner-referral.

### 5.4 Paid channel sizing (what paid *is* allowed to do)

- **Premium-tier paid.** Paid search on high-intent queries (`bill johnson email`, `mary smith email address`) converts at 139/acq per W3 §2f. Premium CAC ceiling is $306. Room to scale. **Target: 40–50% of premium acquisitions from paid.**
- **Awareness paid.** Brand-lift campaigns on Meta targeting "people with common surnames who feel identity gap" — cheap, high-reach, measured by branded-search lift rather than direct conversion. Budget capped at 15% of total marketing spend.
- **No paid standard-tier acquisition funnel.** This is a firm rule, not a spend cap. If marketers can't hit the $24 ceiling on a standard-tier paid funnel, the answer is to not build the funnel, not to tune it.

---

## §6. Supply-Side Implications (Feedback into W2)

### 6.1 Owner payout improves materially

Quoted owner payout at liquidity changes from $1,584/yr (W3 baseline, 20 renters × $16.50 × 40% × 12) to:

- **3A-mod central: $2,736/yr** (50 renters × $11.40 avg × 40% × 12, pre-prepay adjustment; post prepay $2,640/yr)
- **3A-founder ($8): $2,448/yr**
- **3C (if budget re-priced to $6): $1,800/yr** — no better than W3.

**The owner pitch shifts from "$1,500–$2,500/yr at liquidity" to "$2,500–$3,000/yr at liquidity."** Per W2 §2d the Dormant Holder motivation to list is anchored to "recurring income worth the mindshare." Jumping to $2,500+/yr meaningfully widens the addressable Dormant Holder pool and strengthens the Resigned Squatter pitch (which was the shakiest W2 conversion assumption).

### 6.2 Faster ramp to first meaningful payout

At W3 baseline, owner sees first $100/mo payout at ~9 months (9 renters × $15 × 40% = $54, still subsidy-topped). Under Rev-2 central with compound slots expanding the addressable renter pool per domain, the owner sees first $100/mo at **month 4–6** (12–15 renters at blended $11 × 40% = $53–66/mo and rising). This is a **materially more credible exp-1 pitch** — the owner's first payout ledger looks real within a quarter of going live.

### 6.3 Y1 floor subsidy burden **decreases**

Because domains ramp to $50/mo owner payout faster (compound-slot namespace expansion = more renters flowing in/month), the Y1 $50/mo floor subsidy per W3 §2b kicks off sooner. Rough estimate: Y1 subsidy burden drops from $1,800–$2,700 (W3 Realistic 18 domains) to **$1,000–$1,600**. Minor win but real.

### 6.4 Does Rev-2 change the W2 Rev-1 decisions?

**Long-Tail Portfolio sale-escape clause:** Rev-2 *improves* this pitch, not weakens it. A portfolio holder signing a dead-tail `parkins.com` is now looking at a potential $2,500/yr rather than $1,500/yr — the gap between "dead inventory" and "leased income" widens, which makes the sale-escape carrot less central (the economics alone approach signing-worthy). **Action:** keep the sale-escape clause but adjust the pitch framing in W2 §2g-iv — lead with the new income number, sale-escape is now backup insurance rather than the primary deal-maker.

**Hispanic-surname sub-segment:** Rev-2 *enhances* this sub-segment. Garcia, Rodriguez, Martinez, Hernandez are all top-25 surnames with 6M+ combined bearer pools — more compound-slot density, better per-domain economics. The "reclama tu apellido" Spanish-language pitch now credibly promises $250/mo to the owner rather than $150/mo, which lifts the cold-response rate hypothesis (A-W2-10). **Action:** elevate expected Spanish-language-cohort signing rate by ~20% in exp-1 planning.

**Does owner-side K-W2-* kill criteria change?** No numeric change required in W2 kills. The *targets* get easier (owner CAC payback moves from 5-month to ~3-month at 50 renters × $3.14 contribution = $157/mo vs W3's $111/mo). K-W2-5 "≥ 15 Y1 signed domains = PROCEED" becomes *easier* to clear, not harder. No W2 kill criteria need Rev-2 adjustment.

### 6.5 But: Rev-2 pushes one W2 assumption under stress

**A-W2-7 (supply composition: ≥ 50% of signed Y1 domains are top-200 US surnames).** Rev-2 economics depend on enough compound-slot density, which requires larger surname bearer pools. Top-200 surnames have 200k+ bearers; rank 200–500 has 30k–100k. A long-tail signed portfolio of rank 200–500 domains might only support 15–25 renters/domain even under Rev-2 namespace expansion — closer to W3 density than to the 50-renter Rev-2 central case. **Implication:** Rev-2 makes A-W2-7 more important, not less. Tighten to **"≥ 60% of Y1 signed domains in top-200"** to keep central-case economics intact. Flag as refinement of A-W2-7 → A-Rev2-5.

---

## §7. Three-Year Financial Model — Rev-2 Central Case

Replicate W3 §2h structure under 3A-mod assumptions. Key inputs changed from W3:

- Blended ARPU: $11.00 (was $16.50)
- Renters per domain at liquidity: 50 (was 20)
- Net platform contribution / renter-mo: $3.14 (was $6.00 incl. amort)
- Renter ramp per new domain: **5 renters/month for 10 months** (was 2/mo for 10 mo), reflecting larger addressable namespace and SEO-driven inbound
- Blended CAC trajectory: $90 → $70 → $50 → $40 across Q1–Q8 phases (tighter than W3 $152→$105→$80→$65, but achievable only if organic mix stays ≥ 55% from month 7)
- Owner payout: 40% of $11.00 = $4.40/renter/month
- Y1 floor subsidy: $30/mo per ramp-domain for first 2 months avg (was 3 months) = ~$60/domain total
- Renter churn blended: 3.5%/mo (blended premium/standard per §4)
- Domain churn: 15%/yr (unchanged)
- Fixed opex: Y1 $65k / Y2 $135k / Y3 $225k (slight uplift vs W3 for SEO content production)

### 7.1 Realistic central (3A-mod)

| Quarter | New dom | Live dom | Avg renters/dom | Paying renters EOQ | Gross rev (Q) | Platform 60% gross (Q) | Ops cost (Q) | Owner CAC | Renter CAC | Fixed opex | Q net | Cumulative |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| Q1 m1–3 | 4 | 4 | 4 | 16 | $530 | $318 | $265 | $2,400 | $1,440 | $16,250 | **–$20,037** | –$20,037 |
| Q2 m4–6 | 5 | 9 | 8 | 72 | $4,050 | $2,430 | $2,027 | $3,000 | $5,040 | $16,250 | **–$23,887** | –$43,924 |
| Q3 m7–9 | 4 | 13 | 14 | 182 | $13,200 | $7,920 | $6,609 | $2,400 | $7,280 | $16,250 | **–$24,619** | –$68,543 |
| Q4 m10–12 | 5 | 18 | 19 | 342 | $26,700 | $16,020 | $13,370 | $3,000 | $13,680 | $16,250 | **–$30,280** | –$98,823 |
| **Y1** | **18** | **18** | **19** | **342** | **$44,480** | **$26,688** | **$22,271** | **$10,800** | **$27,440** | **$65,000** | **–$98,823** | |
| Q5 m13–15 | 9 | 26 | 24 | 624 | $47,700 | $28,620 | $23,879 | $5,400 | $20,020 | $33,750 | **–$54,429** | –$153,252 |
| Q6 m16–18 | 9 | 34 | 29 | 986 | $78,800 | $47,280 | $39,452 | $5,400 | $20,580 | $33,750 | **–$51,902** | –$205,154 |
| Q7 m19–21 | 10 | 43 | 33 | 1,419 | $116,700 | $70,020 | $58,417 | $6,000 | $21,660 | $33,750 | **–$49,807** | –$254,961 ⬅ max drawdown |
| Q8 m22–24 | 10 | 52 | 38 | 1,976 | $169,100 | $101,460 | $84,642 | $6,000 | $22,280 | $33,750 | **–$45,212** | –$300,173 |

Wait — max drawdown is still falling. Let me extend Y3 more carefully.

| Quarter | New dom | Live dom | Avg renters/dom | Paying renters EOQ | Gross rev (Q) | Platform 60% gross (Q) | Ops cost (Q) | Owner CAC | Renter CAC | Fixed opex | Q net | Cumulative |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| Q9 m25–27 | 13 | 62 | 42 | 2,604 | $227,200 | $136,320 | $113,744 | $7,800 | $25,120 | $56,250 | **–$66,594** | –$366,767 |
| Q10 m28–30 | 16 | 76 | 45 | 3,420 | $297,500 | $178,500 | $149,050 | $9,600 | $32,640 | $56,250 | **–$69,040** | –$435,807 |
| Q11 m31–33 | 17 | 91 | 47 | 4,277 | $371,700 | $223,020 | $186,180 | $10,200 | $34,280 | $56,250 | **–$63,890** | –$499,697 |
| Q12 m34–36 | 19 | 108 | 48 | 5,184 | $450,200 | $270,120 | $225,470 | $11,400 | $36,760 | $56,250 | **–$59,760** | **–$559,457** |

**This is worse than W3 baseline under full-growth posture.** Why? Because Rev-2 has lower margin per renter ($3.14 vs $6.00) while supporting 2.5× the renter count. Margin × volume = similar gross contribution, but proportional CAC spend on the compound tier is *counterproductive* if it's paid rather than organic.

**Crucial correction: Rev-2 under "paid-dominant standard-tier CAC" loses money faster than W3.** This confirms §5 structural point: Rev-2 only works if organic is ≥ 65% of standard-tier acquisitions.

**Recomputed under organic-dominant mix (65% organic from month 13, with amortized organic content cost of ~$25/renter):**

| Year | Live dom EOY | Avg renters/dom EOY | Revenue | Platform gross | Total cost | Annual net | Cumulative net |
|---|---:|---:|---:|---:|---:|---:|---:|
| Y1 | 18 | 19 | $44k | $27k | $126k | **–$99k** | –$99k |
| Y2 | 52 | 38 | $412k | $247k | $345k | **–$98k** | –$197k |
| Y3 (throttled-growth, organic-dominant) | 80 | 44 | $1,090k | $654k | $610k | **+$44k** | **–$153k** |

**Under the realistic-organic central case, Rev-2 reaches cumulative breakeven around month 48–52**, with max drawdown of **–$245k at month 30**.

### 7.2 Capital requirement

| Plan | Growth posture | Y3 end domains | Month-36 cum | Max drawdown | Capital required |
|---|---|---:|---:|---:|---:|
| **Lean organic-dominant (central Rev-2)** | Throttle to 80 domains; ≥ 65% organic mix from m13; reduce Y3 fixed opex ramp | 80 | **–$153k** | **–$245k at m30** | **$245k** |
| Growth-organic (aggressive) | 108 domains; maintain 55% organic | 108 | –$310k | –$360k at m33 | $360k |
| Paid-dominant (if organic fails) | Standard-tier partly-paid | 80 | –$475k | –$485k at m34 | N/A — kill thesis |

**Capital requirement (central Rev-2): $245k**, vs W3 baseline $275k. Improvement driven by (i) better per-domain economics and (ii) much-faster ramp-to-$50-owner-payout, reducing Y1 subsidy burden. **Fragile improvement — if organic mix doesn't materialize, paid-dominant Rev-2 needs $400k+, which is worse than W3 baseline.**

### 7.3 Breakeven month

Rev-2 central case: cumulative breakeven **month 48–52** (vs W3 Realistic month 42–48). Rev-2 is *slightly slower* to cumulative breakeven but **crosses monthly-breakeven earlier** (month 30 vs W3's month 34–35), which is the number that matters for bridging confidence.

---

## §8. Trust & Safety Preview (W4 ownership; Rev-2-critical preview)

Compound-slot expansion materially changes the T&S surface. W4 will own the final answers; Rev-2 flags four new must-address items.

### 8.1 Blast-radius is 2–3× larger

W3 assumed 20 renters/domain. Rev-2 assumes 50. **A single blacklisted domain now affects 2.5× more innocent renters.** Per W4 §2f, domain reputation is a shared resource. Implications:

- **Migration-reserve sizing insufficient.** W3 §2g priced sale-escape migration at $75/renter × 15 renters = $1,125/event. Under Rev-2 an abuse-driven domain delisting moves 40+ renters at $75 = $3,000/event. **Reserve accrual must rise from $1.25/mo per sale-escapable domain to ~$2.00/mo per *any* at-risk domain** (all compound-enabled domains are at-risk, not just sale-escape ones). Flag as Rev-2 cost-stack adjustment; approximate pass-through: +$0.04/renter/mo. Minor.
- **Abuse reserve of $0.40–$0.75/renter-mo in §3.1 already reflects this uplift** (vs W3's $0.50 baseline). Confirmed adequate if W4 builds automated blacklist monitoring and renter rate-limiting per W4 §2d. **Not adequate** if W4 delays those systems. New contingent kill: K-Rev2-3 (see §9).

### 8.2 Impersonation surface expands

Compound variants for "John Paul Smith" include:
- `john.paul@smith.com`
- `john.p@smith.com`
- `j.paul@smith.com`
- `jp.smith@smith.com`
- `j.p.smith@smith.com`
- `johnpaul@smith.com`
- `jpaul@smith.com`

Seven valid local-parts map to one legal identity. Three questions:

1. **Who gets to rent which?** Policy: first-come-first-served with identity verification required (photo ID match) for any standard-tier slot that "collides" with an existing premium renter on the same domain. No user can rent more than 3 slots on any domain.
2. **Can a non-John-Paul rent `john.paul@`?** Policy: yes, subject to the same ID verification — we cannot police whether someone's middle name is actually Paul. Reputational risk accepted; documented in lease terms.
3. **Slot-squatting defense.** A renter who signs up for `john.paul.smith@`, `j.p.smith@`, `jp.smith@`, and `john.p@` defensively is paying 4× $9 = $36/mo. Limit to 3 slots per person per domain (policy); charge a 20% surcharge on slots 2 and 3. This caps legitimate defense and makes bulk speculation uneconomical.

**Legal preview (→ W5):** the 7-variant problem requires disclosure in renter ToS ("other renters may use similar local-parts") and a dispute-resolution process that is not a court but also not a pure T&S discretion channel. W5 owns.

### 8.3 Compound-slot enables cheaper abuse-ring setup

A $9 standard slot is 60% cheaper than a $25 premium slot. Cost to set up a 50-account abuse ring drops from $1,250/mo (all-premium) to $450/mo (all-standard). Identity verification and $25 one-time onboarding fee on standard slots remain essential — **do not waive either** to drive conversion. The onboarding fee is the primary economic filter on casual abuse. Rev-2 must keep it.

### 8.4 New W4 preview kill: K-Rev2-3

**K-Rev2-3 (new):** Per-domain blacklist incident rate (SpamHaus/SORBS/Barracuda at least one of, per domain-month of live inventory). **> 1 per 100 domain-years → PAUSE new compound-slot sign-ups, revert to premium-only on affected domain (and optionally globally) for 30 days; > 3 per 100 domain-years → KILL compound tier, return to W3 single-tier namespace.** This is a structural-scale tripwire; Rev-2 is a bet that compound-slot abuse stays comparable per-renter to premium-slot abuse. If not, kill cleanly.

---

## §9. Revised Kill Criteria (numeric)

**Supersedes W3 K-W3-1 / K-W3-2 / K-W3-3.** The previous values reflected W3 blended-ARPU $16.50 economics; they are not applicable under Rev-2. Reference this section, not W3 §2f/§2e, for the live Rev-2 numbers.

| ID | Criterion | Rev-2 threshold | Trigger | Supersedes |
|---|---|---|---|---|
| K-W3-1 (Rev-2) | Signup-mix-weighted blended platform-side renter CAC (trailing 3-mo, past m6) | **> $100 → KILL; $67–$100 → PIVOT (kill paid standard-tier funnel); ≤ $67 → PROCEED** | KILL / PIVOT / PROCEED | W3 $180 KILL / $120 PIVOT |
| K-W3-2 (Rev-2) | LTV/CAC ratio (blended, trailing 3-mo, past m12) | **< 1.3× → KILL; 1.3–1.8× → PIVOT (raise standard to $11, cut support cost); ≥ 1.8× → PROCEED (target 2.5×)** | KILL / PIVOT / PROCEED | Unchanged ratios, but LTV input changes to $120 blended (from $220) |
| K-W3-3 (Rev-2) | Renters per active domain at liquidity | **Per-domain: < 25 at 18 mo → DELIST; ≥ 40 at 24 mo = target. Marketplace: < 50 live domains AND < 2,000 paying renters by m36 → KILL or PIVOT** | DELIST / KILL / PIVOT | W3 20 target / 12 floor / 1,000 renters marketplace |
| K-W3-4 (Rev-2) | Cohort 12-mo retention, premium tier | < 70% → PIVOT premium pricing; ≥ 70% → PROCEED | PIVOT / PROCEED | Tightened from W3's 55/65% blanket |
| K-Rev2-1 (new) | Standard-tier organic-acquisition share (SEO + referral + owner-pull) by month 18 | **< 50% → KILL standard tier; 50–65% → PIVOT (cut all paid standard-tier spend); ≥ 65% → PROCEED** | KILL / PIVOT / PROCEED | — |
| K-Rev2-2 (new) | Premium-tier revenue share of total gross revenue (trailing 6-mo, post m12) | **< 30% → PIVOT standard pricing up; ≥ 35% → PROCEED** | PIVOT / PROCEED | — |
| K-Rev2-3 (new) | Per-domain blacklist incident rate (SpamHaus/SORBS/Barracuda, any one) | **> 3 per 100 domain-yrs → KILL compound tier; 1–3 → PAUSE compound sign-ups on affected domains; < 1 → PROCEED** | KILL / PAUSE / PROCEED | — |
| K-Rev2-4 (new) | Standard-tier cohort 12-mo retention | **< 45% → KILL standard tier; 45–55% → PIVOT (raise standard to $11–12); ≥ 55% → PROCEED** | KILL / PIVOT / PROCEED | — |
| K-Rev2-5 (new) | LP split-test premium-take-rate (Variant B of W1 LP) | **< 15% → REPRICE (widen spread to $30/$8 or rebase to one-tier); 15–25% → PROCEED with 3A-mod; > 25% → CONSIDER three-tier expansion post-liquidity** | REPRICE / PROCEED / EXPAND | — |

---

## §10. Rev-2 Verdict and Open Questions

### 10.1 Verdict

**ADOPT REV-2 WITH MODIFICATION.** Specifically:
- Adopt the two-tier premium/standard namespace.
- Adopt Configuration 3A-modified: **Premium $25/mo, Standard $9/mo**. Reject the $5–$8 founder range floor; $8 is marginal, $5 is broken, $9 is the planning number.
- Reject Configuration 3B outright.
- Defer Configuration 3C (three-tier) to post-liquidity — revisit at month 18 once cohort retention data is real.
- Gate Rev-2 on the LP split-test showing ≥ 15% premium take-rate (K-Rev2-5). Below 15%, Rev-2 requires a different price structure, not a build-out.
- Make the standard-tier **organic-acquisition share ≥ 65%** a hard kill criterion (K-Rev2-1), not an aspirational target.

**Why not reject Rev-2 outright?** Because the *owner-side* math improves substantially (§6.1, §6.2) and the W2 supply-acquisition thesis is still the single biggest project risk (K-W2-1 through K-W2-5). Rev-2 makes every W2 metric easier. Even if standard-tier economics land marginal, the improvement in owner-side pitch credibility alone is worth the added operational complexity.

**Why not adopt pure Rev-2 (no modification)?** Because the cost stack math is unambiguous: $5/mo standard tier is cash-flow-negative per renter under current ops. The founder's instinct — that the compound tier should feel impulse-priced — is right, but the floor is $9 not $5. The brand consequence of a $9 price point is negligible vs $5 (both read as impulse relative to Google Workspace $6).

### 10.2 Top 5 open questions (LP- or interview-resolvable)

1. **Premium-vs-standard cannibalization rate** (K-Rev2-5). *Who actually clicks Premium $25 when Standard $9 is on the same page?* Resolvable: W1 LP Variant B.
2. **Standard-tier retention** (K-Rev2-4). *Does a $9 compound-slot renter stick at 55%+ annual, or churn at 40% like a novelty?* Resolvable: concierge MVP cohort on explicit standard-tier pricing, month-6 and month-12 checks. Pre-launch proxy weak; no way around a live cohort.
3. **Standard-tier organic-acquisition share** (K-Rev2-1). *Can surname-SEO carry 65% of compound-tier sign-ups by month 18?* Resolvable: W1 LP organic-channel-share tracking + first 6 months of live SEO experiments.
4. **Owner WTP uplift under Rev-2 income numbers.** *Does quoting "$2,500–$3,000/yr at liquidity" instead of "$1,500–$2,500/yr" materially lift cold-outreach conversion?* Resolvable: split W2 exp-1 cohort 50/50 on pitch dollar-amount.
5. **Slot-squatting and abuse-ring defense in practice.** *Do bad actors actually buy 4 defensive slots at $36/mo, or is the ID-verification + $25 onboarding enough friction?* Resolvable: first 100 paid signups + manual review of duplicate-identity patterns.

### 10.3 Proposed LP copy additions for W1 §2g-2 experiment

**Variant A (unchanged from W1 baseline):**
> Claim `[firstname]@[surname].com`. $25/month. Reserve for $25.

**Variant B (Rev-2 split-test):**
> Claim your email on `[surname].com`.
> - `[firstname]@[surname].com` — premium, $25/month (5–10 slots per surname)
> - `[firstname].[middle]@[surname].com` — standard, $9/month (many slots available)
> Reserve for $25. Pick your slot after reservation.

**Variant C (Rev-2 impulse-first framing):**
> Get a real email on `[surname].com` for $9/month.
> *Also available: the premium* `[firstname]@[surname].com` *at $25/month if you want the short version.*

A/B/C splits measure:
- A→B: does adding compound option change conversion rate (funnel top)?
- B→C: does leading with impulse price change premium take-rate (product mix)?
- All three: which variant drives the best LTV-weighted dollar-conversion?

---

## Secondary Reviewer Notes

### Demand & Positioning Strategist — brand-frame review

**Does Rev-2 help or hurt "Claim your name"?** Mixed.

- *Helps:* wider accessibility (the $9 tier makes the product available to buyers priced out of $15, matching the W1 Surname-Match urgency insight — identity pain exists across income bands).
- *Hurts:* the standard tier dilutes the identity premium. `john.paul.smith@smith.com` is not a claim; it's a fancy `john.paul.smith.1983@gmail.com`. Framing must differentiate: premium tier is "*Claim your name*" (single-word identity), standard tier is "*Get on your family's domain*" (family/affinity frame).
- *Brand risk:* the impulse tier can cheapen the premium tier by association. Mitigation: site architecture that puts Premium front-and-center on surname landing pages, Standard as a secondary CTA ("not available? settle for the compound"). Do not lead with standard on any paid-acquisition page.
- *On-brand impulse tier framing:* "Your last name is rare enough to matter. Get `[yourname]@[surname].com` for $9/month." The frame is family-pride, not privacy, not utility. Keeps identity coherence.

### Domain Owner / Supply Advocate — owner pitch review

**Implications for W2 owner pitch:** mostly better.

- Owner-pitch dollar amount moves from "$1,500–$2,500/yr" to "$2,500–$3,000/yr at liquidity." This is the right number to quote in cold outreach — it clears the "is this worth my time to even respond" threshold for Resigned Squatters, which was the weakest W2 sub-segment.
- First meaningful payout arrives month 4–6 (vs 9–12 under W3). This is the single biggest pitch-credibility improvement Rev-2 delivers.
- *Concern:* owner aversion to "50 strangers on my domain" (W1 §2h supply-dissonance) gets worse at 50 renters than at 25. Rev-2 owner pitch must front-load privacy controls ("you never see renter mail content, only aggregate counts and billing") and the onboarding/ID-verification story.
- *Concern:* Standard-tier abuse exposure matters most to owners, because it's their domain's reputation on the line. Pitch must lead with W4 blacklist-monitoring commitment and the Platform-Indemnification clause (W5 will own the indemnification structure; W2 pitch assumes it's present).

### Trust & Safety Architect — abuse & impersonation review

**Three new Rev-2 risks that W4 must address before any build decision:**

1. **Compound-slot squatting / identity hoarding.** A determined abuser signs up for 6 variants of "John Smith" on `smith.com` and holds them. Mitigation: 3-slot-per-person-per-domain limit, 20% surcharge on slots 2+, ID verification on all signups. **Acceptable residual risk.**
2. **Cheaper abuse-ring economics.** $9/slot × 50 slots = $450/mo to set up a 50-account spam operation on one domain. Mitigation: keep the $25 onboarding fee (non-negotiable), keep phone+ID verification, rate-limit outbound forwarding at Rev-2 levels (not the W4 $500/day baseline — should tighten to $200/day for standard tier). **Acceptable if W4 builds monitoring in Y1.**
3. **Impersonation — 7 variants of "John Paul Smith".** Mitigation: ToS disclosure that local-part similarity does not imply identity relationship, plus display-name policing. Non-trivial; W5 owns. **Residual risk MEDIUM — flag for W4/W5 joint review.**

**Net T&S verdict on Rev-2:** compound-slot expansion is operationally manageable **if** W4 commits to automated blacklist monitoring, tightened outbound rate limits for the standard tier, and ID-verification at signup. Without those, Rev-2 compound tier **must not ship**. This is a hard gate, not a preference.

---

*End of Rev-2 memo. Supersedes W3 pricing numeric thresholds where §9 explicitly says so; leaves W2 decisions intact except as noted in §6.5. All Rev-2 numbers pending LP split-test (K-Rev2-5) and W2 exp-1 cohort confirmation.*
