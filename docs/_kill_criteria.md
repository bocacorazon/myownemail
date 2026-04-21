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

---

## Workshops 3–7 — Placeholders (to be populated by each workshop)

| ID | Criterion | Threshold | Trigger action | Source | Owner |
|---|---|---|---|---|---|
| K-W3-1 | Blended platform-side renter CAC (trailing 3-month window, past month 6) | > $180 → KILL; $120–$180 → PIVOT (cut paid, triple SEO/referral investment); ≤ $120 → PROCEED | KILL / PIVOT / PROCEED | Internal marketing spend vs. paid-renter conversions; pre-launch proxy via W1 LP test (§2g-2) | W3 |
| K-W3-2 | LTV / CAC ratio (trailing 3-month window, past month 12) | < 1.3× → KILL; 1.3–1.8× → PIVOT (raise price, cut cost, tighten target segment); ≥ 1.8× → PROCEED (target ≥ 2.5×) | KILL / PIVOT / PROCEED | Cohort analysis on first 200+ paying renters | W3 |
| K-W3-3 | Renters per active domain at liquidity | Per-domain: < 12 renters after 18 months live → DELIST; ≥ 20 at 24 months = target. Marketplace: < 50 live domains AND < 1,000 paying renters by month 36 → KILL or PIVOT to platform-owned inventory (W2 §2k-i) | DELIST / KILL / PIVOT | Production metrics | W3 |
| K-W3-4 | Cohort 12-month renter retention | < 55% → KILL; 55–65% → PIVOT (price / cost / ICP refinement); ≥ 65% → PROCEED | KILL / PIVOT / PROCEED | First cohort to reach month 12 | W3 |
| K-W3-5 | Cumulative contribution at month 24 (Lean plan) | < –$300k → KILL; –$300k to –$200k → PIVOT (throttle, cut ops); better than –$200k → PROCEED | KILL / PIVOT / PROCEED | Monthly financials | W3 |
| K-W3-6 | Net platform contribution per renter-month (trailing 6 months, months 18+) | < $4.00 → KILL; $4.00–$5.50 → PIVOT (cost cut or price increase); ≥ $5.50 → PROCEED | KILL / PIVOT / PROCEED | Monthly unit-economics tracking | W3 |
| K-W3-7 | Owner-floor subsidy burn (Y1) | > $4,000 cumulative → listing threshold is too loose; PIVOT to require larger waitlist before signing new domains | PIVOT | Quarterly | W3 / W2 |
| K-W3-8 | Capital runway (months of cash at current burn) | < 6 months AND Phase-2 raise not closed → RAISE EMERGENCY BRIDGE or WIND DOWN | EMERGENCY / WIND-DOWN | Monthly treasury | W3 / W7 |
| K-W4-1 | Domain blacklist incident rate under chosen architecture | TBD | TBD | W4 | W4 |
| K-W5-1 | Rug-pull exposure per $ of renter revenue | TBD | TBD | W5 | W5 |
| K-W6-1 | Ranked residual failure-mode count after closures | TBD | TBD | W6 | W6 |

---

*Last updated: Workshop 3 close (K-W3-1 filled at $120 PIVOT / $180 KILL; K-W3-2 filled at 1.8× floor / 2.5× target / 1.3× KILL; K-W3-3 filled at 20 target / 12 floor per-domain, 50 domains × 1,000 renters marketplace; added K-W3-4 through K-W3-8).*
