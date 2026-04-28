# Kill Criteria Ledger

Numeric thresholds that end the project cleanly, or force a pivot, rather than allowing sunk-cost drift. Each criterion names the workshop that owns it and the evidence source that will trigger a check.

**Action legend:**
- `KILL` — stop the project (or stop the current beachhead thesis)
- `PIVOT` — beachhead is not dead but current execution path is; reset ICP, frame, or pricing
- `PROCEED` — pass; continue to next workshop or phase

---

## Workshop 1 — Demand & Positioning

| ID | Criterion | Threshold | Trigger action | Source of evidence | Owner (Workshop) |
|---|---|---|---|---|---|
| K1 | Landing-page email capture rate on surname-targeted cold traffic | < 1.5% → KILL; 1.5–3% → PIVOT messaging; ≥ 3% → PROCEED | KILL / PIVOT / PROCEED | LP test (§2g-2) | W1 |
| K2 | $25 deposit / pre-order conversion from email-captured leads | < 5% → KILL; ≥ 5% → PROCEED | KILL / PROCEED | LP test (§2g-2) | W1 |
| K3 | Interviews showing WTP at $15/mo | < 25% of 20 interviewees willing → KILL | KILL / PROCEED | Interviews (§2g-1) | W1 |
| K4 | Survey preference for own-domain + Workspace over us *when the desired surname is hypothetically available* | > 70% → KILL | KILL / PROCEED | Survey (§2g-4) | W1 |
| K5 | Concierge MVP 60-day retention | < 60% → KILL | KILL / PROCEED | Concierge (§2g-3) | W1 |
| K6 | Blended median WTP from interviews | Median < $8/mo → KILL | KILL / PROCEED | Interviews (§2g-1) | W1 |
| K7 | Year-1 beachhead traction (post-launch, if we launch) | < 150 paying renters OR < $1,500 MRR at month 12 → KILL or PIVOT ICP | KILL / PIVOT | Production metrics | W1 / W7 |

---

## Workshop 2 — Supply Acquisition

| ID | Criterion | Threshold | Trigger action | Source of evidence | Owner (Workshop) |
|---|---|---|---|---|---|
| K-W2-1 | Concierge outreach conversion in 90-day exp-1 (signed LOI from 100 qualified Dormant/Resigned holders) | < 5% → KILL marketplace thesis or PIVOT to §2k-(i) platform-owned inventory; 5–8% → PROCEED with caution; ≥ 8% → PROCEED | KILL / PIVOT / PROCEED | `06_supply_acquisition_workshop.md §2h-exp-1` | W2 |
| K-W2-2 | Blended supply-side CAC per signed domain over exp-1 | > $1,500 → KILL; $1,000–$1,500 → PIVOT channel mix; ≤ $1,000 → PROCEED | KILL / PIVOT / PROCEED | Exp-1 tracking | W2 |
| K-W2-3 | Owner 12-month churn rate at steady state | > 25%/yr → PIVOT owner incentive model (higher split, longer term, larger floor) | PIVOT | Production cohort data | W2 / W5 |
| K-W2-4 | Share of "interested but declined" owners citing forwarding-only architecture as primary refusal reason | > 40% → REOPEN W4 architecture decision | REOPEN | Exp-1 interview notes | W2 / W4 |
| K-W2-5 | Year-1 signed-and-live domains | < 10 by month 12 → KILL marketplace thesis or PIVOT to §2k-(i); 10–15 → PIVOT (reduce renter targets); ≥ 15 → PROCEED | KILL / PIVOT / PROCEED | Production metrics | W2 |
| K-W2-6 | Legal-review cost amortized per signed domain | > $300/domain → SIMPLIFY lease template or absorb via subsidy; re-evaluate at exp-1 close | SIMPLIFY / SUBSIDIZE | Exp-1 legal spend log | W2 / W5 |
| K-W2-7 | Realized owner Y1 payout vs. quoted $1,500–$2,500 range (first 10 owners) | Realized < 50% of quoted low end → referral channel dies; PIVOT rev share or extend floor subsidy | PIVOT | First 10 owner cohort | W2 / W3 |
| K-W2-8 | Sale-escape clause invocation rate on Rev-1 Long-Tail Portfolio contracts | > 2 per 100 domain-years of live sale-escapable inventory → SUSPEND new sale-escape contracts, migrate at-risk renters | SUSPEND / MIGRATE | Portfolio contract tracking | W2 / W5 |
| K-W2-9 | OSINT Bounty effective CAC per signed domain (Rev-2: payout + verification overhead, trailing 6 months) | > $1,200/domain → SUSPEND bounty channel; re-tune prize structure or retire | SUSPEND | Bounty payment ledger + verification labor log | W2 |
| K-W2-10 | Drop-catching auction yield (Rev-2) | Average winning price > $750/domain *or* < 3 successful captures per quarter on top-500 surnames once budget is live → SUSPEND drop-catching capex; redirect to ops | SUSPEND / REDIRECT | Quarterly auction log + capex drawdown | W2 / W3 |

---

## Workshops 3–7 — Placeholders (to be populated by each workshop)

| ID | Criterion | Threshold | Trigger action | Source | Owner |
|---|---|---|---|---|---|
| K-W3-1 **(Rev-2)** | Signup-mix-weighted blended platform-side renter CAC (trailing 3-month window, past month 6) | **> $100 → KILL; $67–$100 → PIVOT (cut paid standard-tier funnel entirely); ≤ $67 → PROCEED (target ≤ $48 at 2.5× LTV/CAC)**. *Rev-2 supersedes prior W3 thresholds of $180/$120 which assumed single-tier $220 LTV; Rev-2 blended LTV is $120.* | KILL / PIVOT / PROCEED | Internal marketing spend vs. paid-renter conversions; pre-launch proxy via W1 LP test (§2g-2). See `docs/08_pricing_namespace_rev2.md §9`. | W3 / Rev-2 |
| K-W3-2 **(Rev-2)** | LTV / CAC ratio (trailing 3-month window, past month 12) | < 1.3× → KILL; 1.3–1.8× → PIVOT (raise standard to $11, cut support cost); ≥ 1.8× → PROCEED (target ≥ 2.5×). *Ratios unchanged; LTV input changes to $120 blended under Rev-2 (was $220).* | KILL / PIVOT / PROCEED | Cohort analysis on first 200+ paying renters; tier-separated preferred. See doc 08 §3.4, §9. | W3 / Rev-2 |
| K-W3-3 **(Rev-2)** | Renters per active domain at liquidity | **Per-domain: < 25 renters after 18 months live → DELIST; ≥ 40 at 24 months = target (50 at steady-state).** Marketplace: **< 50 live domains AND < 2,000 paying renters by month 36 → KILL or PIVOT** to platform-owned inventory (W2 §2k-i). *Rev-2 supersedes prior W3 thresholds of 12/20/1,000 which assumed single-tier namespace.* | DELIST / KILL / PIVOT | Production metrics. See doc 08 §9. | W3 / Rev-2 |
| K-W3-4 | Cohort 12-month renter retention | < 55% → KILL; 55–65% → PIVOT (price / cost / ICP refinement); ≥ 65% → PROCEED | KILL / PIVOT / PROCEED | First cohort to reach month 12 | W3 |
| K-W3-5 | Cumulative contribution at month 24 (Lean plan) | < –$300k → KILL; –$300k to –$200k → PIVOT (throttle, cut ops); better than –$200k → PROCEED | KILL / PIVOT / PROCEED | Monthly financials | W3 |
| K-W3-6 | Net platform contribution per renter-month (trailing 6 months, months 18+) | < $4.00 → KILL; $4.00–$5.50 → PIVOT (cost cut or price increase); ≥ $5.50 → PROCEED | KILL / PIVOT / PROCEED | Monthly unit-economics tracking | W3 |
| K-W3-7 | Owner-floor subsidy burn (Y1) | > $4,000 cumulative → listing threshold is too loose; PIVOT to require larger waitlist before signing new domains | PIVOT | Quarterly | W3 / W2 |
| K-W3-8 | Capital runway (months of cash at current burn) | < 6 months AND Phase-2 raise not closed → RAISE EMERGENCY BRIDGE or WIND DOWN | EMERGENCY / WIND-DOWN | Monthly treasury | W3 / W7 |
| K-W4-1 | Domain blacklist incident rate under chosen architecture | TBD | TBD | W4 | W4 |
| K-W5-1 | Rug-pull exposure per $ of renter revenue | TBD | TBD | W5 | W5 |
| K-W6-1 | Ranked residual failure-mode count after closures | TBD | TBD | W6 | W6 |

---

---

## Rev-2 — Pricing & Namespace (2026-05-06)

See `docs/08_pricing_namespace_rev2.md §9` for derivations. Rev-2 supersedes K-W3-1/2/3 numeric thresholds (updated in the Workshops 3–7 table above); criteria below are net-new under Rev-2.

| ID | Criterion | Threshold | Trigger action | Source of evidence | Owner (Workshop) |
|---|---|---|---|---|---|
| K-Rev2-1 | Standard-tier organic-acquisition share (SEO + renter-referral + owner-referral) by month 18 | **< 50% → KILL standard tier; 50–65% → PIVOT (cut all paid standard-tier spend); ≥ 65% → PROCEED (target ≥ 75% by month 30)** | KILL / PIVOT / PROCEED | Marketing-attribution data; pre-launch proxy via W1 LP organic-channel-share tracking | Rev-2 / W1 |
| K-Rev2-2 | Premium-tier share of total gross revenue (trailing 6-month window, past month 12) | **< 30% → PIVOT standard pricing up (raise to $11–12); ≥ 35% → PROCEED** | PIVOT / PROCEED | Revenue mix tracking | Rev-2 / W3 |
| K-Rev2-3 | Per-domain blacklist incident rate (SpamHaus / SORBS / Barracuda, any one, per 100 live domain-years) | **> 3 → KILL compound tier, revert to single-tier namespace; 1–3 → PAUSE compound sign-ups on affected domains for 30 days; < 1 → PROCEED** | KILL / PAUSE / PROCEED | Daily automated RBL monitoring (per W4 §2d) | Rev-2 / W4 |
| K-Rev2-4 | Standard-tier cohort 12-month retention | **< 45% → KILL standard tier; 45–55% → PIVOT (raise standard to $11–12, widen spread from premium); ≥ 55% → PROCEED** | KILL / PIVOT / PROCEED | First standard-tier cohort reaching month 12 | Rev-2 / W3 |
| K-Rev2-5 | LP split-test premium take-rate (Variant B of W1 LP §2g-2, per doc 08 §10.3) | **< 15% → REPRICE (widen to $30/$8 or revert single-tier); 15–25% → PROCEED with 3A-mod; > 25% → CONSIDER three-tier expansion post-liquidity** | REPRICE / PROCEED / EXPAND | W1 LP experiment | Rev-2 / W1 |

---

*Last updated: Rev-2 close (2026-05-06). K-W3-1 revised to $67 PIVOT / $100 KILL; K-W3-2 ratios unchanged but blended LTV input drops to $120; K-W3-3 revised to 25 floor / 40 target per-domain, 50 domains × 2,000 renters marketplace; added K-Rev2-1 through K-Rev2-5.*
