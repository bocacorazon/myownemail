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
| K-W4-1 | Per-domain blacklist incident rate (SpamHaus / SORBS / Barracuda, any one, per 100 live domain-years) | **> 3 → KILL compound tier, revert to single-tier namespace; 1–3 → PAUSE compound sign-ups on affected domains for 30 days; < 1 → PROCEED**. *Lifts and locks K-Rev2-3 from Rev-2 doc. Coupled to A-W4-3 monitoring lead-time assumption.* | KILL / PAUSE / PROCEED | Daily automated RBL monitoring (per W4 §2 monitoring flow); investigation log per incident | W4 |
| K-W4-2a **(Rev-2.1)** | Tier 1 false-positive rate among legitimate users (renters paused by automated rules whose case-audit determines no abuse, per 100 renter-months, trailing 90-day window) | **> 8 → REVISE rate limits up (UX is being damaged); 3–8 → MONITOR + lightweight appeal flow; ≤ 3 → PROCEED**. UX-risk side of K-W4-2 split; was bundled with abuse rate in 2026-04-26 draft. | REVISE / MONITOR / PROCEED | Tier 1 auto-pause log + per-incident root-cause tagging (legitimate-user vs. confirmed-abuse) | W4 |
| K-W4-2b **(Rev-2.1)** | Confirmed forwarding-abuse rate (renters who reach Tier 2 or Tier 3 with confirmed-abuse adjudication, per 100 renter-months, trailing 90-day window) | **> 3 → REVISE rate limits down OR add detection signal (forwarding throughput limits leaking abuse); 1–3 → MONITOR; ≤ 1 → PROCEED**. Abuse side of K-W4-2 split. | REVISE / MONITOR / PROCEED | Tier 2/3 confirmed-abuse log; coupled to A-W4-2 | W4 |
| K-W4-2c **(Rev-2.1)** | Send-as outbound complaint rate (per renter, trailing 90-day window — measured via Mailgun + Gmail Postmaster Tools + abuse@ inbox + recipient reports) | **> 0.3% → SUSPEND alias + Tier 2 review; 0.1–0.3% → renter warning + monitor; ≤ 0.1% → PROCEED**. Send-as outbound is not platform-rate-limitable; this is the complaint-driven floor. | SUSPEND / WARN / PROCEED | Mailgun feedback loops, Gmail Postmaster, abuse@ ticketing | W4 |
| K-W4-3 **(Rev-2.1)** | ID-verification post-hoc abuse rate (observable proxies — chargeback rate by IDV vendor, near-duplicate identity rate detected at audit, confirmed-abuse rate among ID-verified cohort vs. baseline; trailing 6-month window past first 100 paid signups) | **Aggregate trigger: any two of: chargeback rate > 1.5%, near-duplicate identity rate > 5%, confirmed-abuse rate among IDV cohort > 1.5× baseline → SWITCH vendor or add second-factor (liveness, document re-capture); single trigger → MONITOR + add randomized manual review on 5% of signups; none → PROCEED**. Replaces 2026-04-26 "false-pass rate" formulation, which was not directly observable. | SWITCH / MONITOR / PROCEED | Vendor audit + duplicate-identity audit on first 100, then 500, then 1,000 paid signups + chargeback dashboard | W4 |
| K-W4-4 **(Rev-2.1)** | Send-as deliverability proof (Gate 0): inbox-placement rate of test mail sent via consumer Gmail send-as on a non-Google `.com` to fresh accounts at Gmail, Outlook, Yahoo, Apple Mail, Microsoft 365; SPF/DKIM/DMARC alignment; absence of "via gmail.com" sender mismatch | **All 5 providers inbox + clean alignment + no sender-mismatch label → PASS, lock A-pre-1; any provider quarantines/rejects OR shows sender mismatch → FAIL, kills forwarding-only architecture and reopens W3 economics** | PASS / FAIL | Pre-MVP technical-proof task; documented test results retained in W7 evidence | W4 (technical proof) |
| K-W4-5 **(Rev-2.1)** | Mailgun account-level reputation incidents (provider warning, throttling action, suppression-list explosion >2× baseline, AUP citation, or service degradation traceable to forwarding mix), rolling 12-month window | **> 1 → KILL forwarding-only architecture, escalate to W7; 1 incident → PAUSE compound-tier signups + Mailgun architecture review; 0 → PROCEED** | KILL / PAUSE / PROCEED | Mailgun account dashboards + provider correspondence | W4 / W6 |
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
| K-W4-6 | Sending-bridge dependency: composite of (a) LP-measured ICP Gmail-share + (b) concierge-MVP Gmail-bridge acceptance rate among non-Gmail signups (Rev-2.2 §2.7) | **(a) < 50% Gmail share AND (b) < 60% bridge acceptance → KILL forwarding-only / first-party send endpoint required (re-opens W4 outbound abuse model);** **(a) < 50% Gmail share AND (b) ≥ 60% bridge acceptance → PROCEED with bridge as default;** **(a) ≥ 50% Gmail share → PROCEED regardless of (b)** | KILL / PROCEED | W1 LP capture-form provider question (doc 05 §2g exp 2); concierge-MVP onboarding telemetry (bridge-step completion vs. drop-off) | W4 / W1 |
| K-W5-1 | Sale-escape invocation rate on Standard-tier (sale-escapable) inventory (lifts and locks W2's K-W2-8) | **> 2 per 100 sale-escapable domain-years → SUSPEND new sale-escape contracts; migrate at-risk renters preemptively** | SUSPEND / MIGRATE | Sale-escape contract tracking; quarterly review | W5 / W2 |
| K-W5-2 | Migration cost per displaced renter (concierge labor + pro-rated refund + 1-month migration credit) trailing 6-month average | **Sustained > $80/renter → REPRICE migration reserve into renter-side pricing OR tighten owner-exit rules (raise notice from 90 → 120 days; raise sale-escape exit fee)** | REPRICE / TIGHTEN | Migration ops ledger | W5 / W3 |
| K-W5-3 | Owner-initiated rug-pull rate across all causes (planned exit + sale-escape + default + non-renewal + adversarial), trailing 12-month rolling | **> 5 per 100 domain-years → architecture review (does the marketplace structurally fail at this owner-churn rate?)** | ARCHITECTURE REVIEW | Domain lifecycle ledger | W5 / W7 |
| K-W5-4 | Regulatory complaint rate (CAN-SPAM / GDPR / state-AG / trademark-takedown) per 1,000 renter-months trailing 12-month rolling | **> 1 → escalate to legal review; > 3 → architecture pause / launch-blocking re-open** | ESCALATE / PAUSE | Legal/ops complaint ledger | W5 / W6 |
| K-W5-5 | Indemnification reserve cumulative draw-down against $50k annual aggregate cap (claims paid + outstanding reserved) | **> 50% in any rolling 12-month window → tighten ToS caps OR raise insurance limit; > 80% → architecture review** | TIGHTEN / RAISE / REVIEW | Indemnification ledger; insurance broker statement | W5 / W7 |
| K-W5-6 | Stripe Connect chargeback rate on owner side (renter-disputed payouts, trailing 6-month) | **> 1.5% → tighten owner reserve from 10% → 20% AND extend hold from 180 → 270 days; > 3% → pause owner onboarding pending review** | TIGHTEN / PAUSE | Stripe Connect dispute reports | W5 / W3 |

---

*Last updated: W5 Continuity initial draft (2026-04-27) — added K-W5-1 through K-W5-6 covering sale-escape invocation, migration cost, owner rug-pull rate, regulatory complaints, indemnification draw-down, owner-side chargeback rate. K-W5-1 lifts and locks K-W2-8. Prior baseline: W4 Rev-2.2 sending-bridge dependency (2026-04-27) — added K-W4-6 (sending-bridge dependency: ICP Gmail-share + bridge-acceptance composite). Earlier: W4 Rev-2.1 rubber-duck pass (2026-04-27) — K-W4-2 split into K-W4-2a/b/c; K-W4-3 reformulated; K-W4-4 added (Gate 0); K-W4-5 added (Mailgun reputation incidents). Earlier: W4 Rev-2 alignment (2026-04-26) — K-W4-1 locked at K-Rev2-3 thresholds; K-W4-2/3 added. Earlier baseline: Rev-2 close (2026-05-06). K-W3-1 revised to $67 PIVOT / $100 KILL; K-W3-2 ratios unchanged but blended LTV input drops to $120; K-W3-3 revised to 25 floor / 40 target per-domain, 50 domains × 2,000 renters marketplace; added K-Rev2-1 through K-Rev2-5.*
