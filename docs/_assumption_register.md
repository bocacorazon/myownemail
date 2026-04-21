# Assumption Register

Living list of hypotheses across workshops. Each row carries a status (`open` / `validated` / `killed`), a pointer to current evidence (or lack of), and the workshop that owns its resolution.

**Status legend:**
- `open` — unverified hypothesis, project proceeds assuming it holds
- `validated` — evidence supports the assumption
- `killed` — evidence contradicts the assumption; dependent decisions must be re-examined

---

## Workshop 1 — Demand & Positioning

| ID | Assumption | Status | Evidence / Pointer | Owner (Workshop) |
|---|---|---|---|---|
| A1 | Top-500 US surnames cover ~40% of the US adult population, producing a TAM of 1M+ surname-match buyers after narrowing by age and behavior. | open | First-principles estimate only (`05_demand_positioning_workshop.md §2a.4`). Needs surname-frequency table cross-check. | W1 / W3 |
| A2 | ≥ 20% of top-100 US surname `.com` domains are held by individuals or small businesses reachable via direct outreach. | open (refined) | W2 §2a estimates ~25% of top-500 are Dormant + Resigned holders based on reasoned WHOIS/parking signals. Real measurement pending exp-0 WHOIS audit (`06_supply_acquisition_workshop.md §2h-exp`). | W2 |
| A3 | Surname-Match buyers tolerate forwarding-only + Gmail send-as because recipients never see the plumbing. | open | Architecture–positioning matrix argues it (§2c). Concierge MVP will test it. | W1 / W4 |
| A4 | WTP for an identity-grade email anchors to "what is identity worth per month," not to Workspace pricing, supporting $15/mo. | open | Interview + LP deposit experiments planned (§2g-1, §2g-2). | W1 |
| A5 | Blended CAC is achievable at ≤ $60 once surname-SEO contributes alongside paid acquisition. | open | Flagged by Economics reviewer as aggressive. LP test §2g-2 is first data point. | W3 |
| A6 | Domain owners accept a 60/40 platform-favoring split as long as per-domain passive income clears ~$1,500+/yr. | open (refined) | W2 §2e and §4 argue defensible at steady state; untested with real owners. Resigned Squatters may demand 50/50. First real data point from exp-1. | W2 / W3 |
| A7 | Retention for identity purchases is high (≥70% at 12 months) vs. utility-purchase baselines. | open | Concierge 60-day retention is the early proxy (§2g-3). | W1 / W3 |
| A8 | The "Claim your name" framing does not generate unmanageable trademark or impersonation legal exposure. | open | No legal review yet. | W5 |
| A9 | ≥ 20 willing surname-domain owners can be signed within year 1 at a commercially reasonable acquisition cost. | open (at risk) | W2 Realistic scenario projects ~13 signed domains in Y1, Optimistic ~22. A9 now treated as ~50/50 likelihood pending exp-1 (`06_supply_acquisition_workshop.md §2i`). | W2 |
| A10 | Renters accept a lease structure (not ownership) with disclosed rug-pull protections without killing conversion below K2. | open | LP deposit test indirectly probes this; Workshop 5 defines the actual terms. | W1 / W5 |

---

## Workshop 1 — Placeholders carried forward from earlier docs (to be reviewed)

| ID | Assumption | Status | Evidence / Pointer | Owner (Workshop) |
|---|---|---|---|---|
| A-pre-1 | Forwarding-only is the safest architecture candidate. | open (refined) | `04_deliverability_workshop.md`. Re-validated compatible with Surname-Match ICP in W1 §2c. W2 added K-W2-4 kill: if > 40% of owner refusals cite architecture, re-open W4. | W4 |
| A-pre-2 | Platform dependencies (Gmail send-as, Mailgun AUP, Stripe Connect) remain policy-compatible. | open | `04_deliverability_workshop.md` flags this as a standing risk. | W6 |
| A-pre-3 | Revenue-share default of 50/50 is the right starting point. | **killed** | Challenged in W1 §2f. New hypothesis: 60/40 platform favor. | W1 → W3 |

---

## Workshop 2 — Supply Acquisition

| ID | Assumption | Status | Evidence / Pointer | Owner (Workshop) |
|---|---|---|---|---|
| A-W2-1 | Cold outreach conversion to Dormant Individual Holders clears ≥ 5% with a founder-signed pitch plus $100–$250 signing bonus. | open | Exp-1 (90-day concierge outreach to 100 qualified owners) is the first test. `06_supply_acquisition_workshop.md §2h-exp`. | W2 |
| A-W2-2 | Owner 12-month churn on signed domains stays below 15% at liquidity. | open | No early proxy; only measurable once cohorts age. Gated by K-W2-3. | W2 / W5 |
| A-W2-3 | Demand-pull ("N renters on your waitlist for your domain") pitches convert 2–3× better than pure cold pitches once a waitlist exists. | open | Requires waitlist first; testable month 6+. | W2 |
| A-W2-4 | Standardized 1-page lease is acceptable to ≥ 80% of individual owners without lawyer review; amortized legal-review cost stays under $300/domain. | open | Gated by K-W2-6. Drafting template is a W5 dependency. | W2 / W5 |
| A-W2-5 | ≥ 80% of targeted owners can successfully transfer MX control during onboarding without founder-assisted registrar credential recovery. | open | Observable during exp-1 onboarding. Operational friction risk. | W2 |
| A-W2-6 | Platform-owned inventory fallback (buy 5–10 premium surname `.coms` outright) is capital-raisable at $50k–$250k if the marketplace thesis fails exp-1. | open | Fundraising test deferred; informational only unless fallback triggers. | W2 / W7 |
| A-W2-7 | Supply composition — at least 50% of signed Y1 domains are top-200 US surnames (not the long tail of 200–500). Demand Strategist (W2 §3) concern. | open | Depends on exp-1 outreach prioritization. | W2 |
| A-W2-8 | Architecturally isolated forwarding-only satisfies Trust & Operations review for trademark/impersonation exposure at listing. | open | Depends on W5 trademark-screen operational design. | W2 / W5 |
| A-W2-9 | Long-Tail Portfolio Squatters (Rev-1) convert at ≥ 3% bulk-contract rate under a sale-escape clause; sale-escape invocations stay ≤ K-W2-8 threshold. | open | Gated by W5 legal sign-off on the sale-escape clause and by exp-1 portfolio-holder cohort (5–8 contacted holders). | W2 / W5 |
| A-W2-10 | Spanish-language outreach on Hispanic-surname `.com`s (Rev-1) lifts conversion ≥ 1.5× vs. English-language cold outreach on the same surname cohort, and the resulting renter cohort densities match or exceed English-surname baseline. | open | Gated by the ≥ 25-contact Spanish-language sub-cohort inside exp-1. | W2 / W1 |
| A-W2-11 | Affinity-domain marketplace (religion/politics/hobby — e.g., `catholic.com`, `golf.com`) is a viable Phase-2 expansion once MVP clears, **not** an MVP concern. Out of scope for W1–W7. | open (Phase-2 only) | Noted from founder question at Rev-1. Affinity-domain holders are overwhelmingly commercial organizations with active brand use, failing the Surname-Match substitute test. Revisit only if MVP clears Year-2 kill gates. | Phase 2 |

---

## Workshop 3 — Marketplace Economics

| ID | Assumption | Status | Evidence / Pointer | Owner (Workshop) |
|---|---|---|---|---|
| A-W3-1 | Premium-tier (top-100 surname) inventory is ~20% of live domains at steady state; blended ARPU computation depends on this mix. | open | W3 §2a. Supply composition tracked via W2 exp-1 and K-W2 composition criteria. | W3 / W2 |
| A-W3-2 | Annual-prepay uptake settles around 30% of renters at steady state (drives effective monthly ARPU to $16.50). | open | W3 §2a; W1 LP test can probe annual willingness. | W3 / W1 |
| A-W3-3 | Onboarding-fee refund rate stays ≤ 15% (from 14-day trial + goodwill refunds). | open | W3 §2a; measurable from first 100 paid signups. | W3 / W4 |
| A-W3-4 | Per-renter support cost holds at $1.50/mo (≤ 0.33 tickets/renter/mo × ~$12 fully-loaded) once a help center is live from month 6. | open | W3 §2a. Gated by W4 onboarding-friction design. | W3 / W4 |
| A-W3-5 | **Blended renter CAC averages ≤ $120 across months 6–24**, requiring ≥ 35% SEO + referral + partnership mix by month 18. Paid social alone produces $150+ CAC. | open — **HIGHEST PRIORITY** | W3 §2f channel math. First signal from W1 LP test (§2g-2). | W1 / W3 |
| A-W3-6 | Sale-escape clause invocations stay ≤ 1.2 per 100 domain-years at target (K-W2-8 ceiling at 2.0). Reserve sizing depends on this rate. | open | W3 §2g; gated by W5 legal review and portfolio-holder exp-1 cohort. | W2 / W5 |
| A-W3-7 | Owner floor subsidy ($50/mo Y1 guarantee) retires on schedule for ≥ 90% of signed Y1 domains (i.e., most domains cross 3 renters within 12 months or age off the subsidy). | open | W3 §2b, §2h; Y1 cohort will test. | W3 / W2 |
| A-W3-8 | Fixed operating expense can be held to $60k Y1 / $120k Y2 / $220k Y3 at a founder stipend of $36k–$80k across the period. | open | W3 §2h. Founder-controlled. | Founder |
| A-W3-9 | A $225–300k angel round is closeable at $2–4M pre-money post-W1 LP clearance + W2 exp-1 clearance + first 40 paying renters. | open — untested fundraising assumption | W3 §2i. | W7 |
| A-W3-10 | Stripe Chargeback Protection (or equivalent) is available for this product class, holding effective chargeback-plus-dispute cost to $0.50/renter/mo. | open | W3 §2a; W5 to confirm. | W5 |
| A-W3-11 | Cumulative contribution crosses positive month 42–48 (Realistic Lean) / 39–41 (Optimistic); Pessimistic never crosses and dies at W2 exp-1 gate. | open (derived) | W3 §2h. Tracked from monthly financials post-launch. | W3 / W7 |
| A-W3-12 | 60/40 take rate is the minimum defensible split; 50/50 fails LTV/CAC, 70/30 fails supply. Tiered splits not required for MVP. | open (design decision, not empirically tested) | W3 §2d. Gated by W2 exp-1 owner feedback on split. | W3 / W2 |

---

*Last updated: Workshop 3 close (W3 marketplace economics: blended ARPU, 60/40 lock, $120 CAC ceiling, 20/12 liquidity floor, $275k capital plan, sale-escape reserve; W1 A5 $60-CAC hypothesis relaxed to $120 via A-W3-5).*
