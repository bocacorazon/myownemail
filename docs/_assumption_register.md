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
| A-pre-1 | Forwarding-only is the safest architecture candidate. | **conditionally locked (W4 Rev-2.1)** | `04_deliverability_workshop.md`. Re-validated compatible with Surname-Match ICP in W1 §2c. Rev-2 §1 keeps it. W4 Rev-2.1 (2026-04-27) downgrades from "locked" to "conditionally locked" pending: (i) Gate 0 send-as deliverability proof against Gmail/Outlook/Yahoo/Apple/M365 (A-W4-6), (ii) Mailgun/Gmail/Stripe Connect AUP confirmation in writing (now an MVP launch blocker, not a long-term risk), (iii) K-W2-4 — re-open if > 40% of owner refusals cite architecture. | W4 |
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
| A-W2-12 | Decentralized OSINT Bounty (Rev-2): a public $1,000 success-fee bounty produces ≥ 4 verified signed leases per quarter at effective CAC ≤ $1,200 once internal verification overhead is included. | open | Channel added to W2 §2f Rev-2. Untested — requires bounty ops design (verification, anti-fraud, payment terms) before launch. Gated by K-W2-9. | W2 |
| A-W2-13 | Parking Platform Integration (Rev-2): a Sedo/Bodis/ParkingCrew partnership is closeable within 6 months and converts ≥ 2% of in-portal impressions to listing inquiries at effective CAC $100–$300/signed domain. | open (Y2 only) | Channel added to W2 §2f Rev-2. Requires BD capability the team does not yet have. Not in Y1 plan; modeled as Y2 lever. | W2 |
| A-W2-14 | Programmatic Drop-Catching (Rev-2): automated sweeps of top-5,000 surnames on DropCatch/SnapNames yield ≥ 3 captures per quarter at average winning price ≤ $500 once an inventory budget is live. | open | Channel added to W2 §2f Rev-2. Introduces a *capex* line (vs. CAC) and a second inventory class (owned, not leased) — see W3 §2b-bis. Gated by K-W2-10. | W2 / W3 |
| A-W2-15 | "Digital Legacy" / charity-routing pitch variant (Rev-2): A/B test against the "$1,800/yr passive income" pitch lifts Dormant Holder response rate ≥ 1.3× without degrading downstream signing rate. | open | Pitch variant in W2 §2g(v) Rev-2. Tested as a sub-cohort inside exp-1; no incremental cost. | W2 |
| A-W2-16 | Fractional / Syndicate Buyouts (Rev-2): crowdfunded outright purchase of a single flagship surname domain via ~500 lifetime-membership pre-sales at $500 is legally structurable as a non-securities co-op AND demand-clearable on a single surname before the 90-day escrow window. | open (Phase-2 only) | Strategic optionality item in W2 §2k(v). High regulatory complexity (SEC). Requires W5 legal sign-off before any pre-sale outreach. Out of scope for MVP economics. | Phase 2 / W5 |
| A-W2-17 | TLD expansion (Rev-2): adding `.org` and `.net` to the surname-match supply pool meaningfully expands inventory (≥ 30% lift in addressable holders) without collapsing the W1 "Claim your name" premium-identity frame or WTP. Pricing differentiation across TLDs (`.com` premium, `.net`/`.org` discounted) clears unit economics on the cheaper tiers. | open (Phase-2 hypothesis) | Founder hypothesis raised 2026-04-26. **Risk:** `.net`/`.org` surname domains may read as inferior compromises rather than legitimate identity claims, eroding the premium WTP that makes the marketplace defensible. Test via W1 LP variant (split landing page traffic between `bill@johnson.com` and `bill@johnson.net` mockups; measure relative deposit conversion). Out of scope for MVP supply pool until tested. | W1 / W2 |

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
| A-W3-13 | Drop-catching (W2 A-W2-14, Rev-2) introduces a second inventory class with no owner payout; per-renter platform contribution rises from $5.54/mo to ~$12.14/mo on owned domains. A Y1 capex budget of $10k clears 20–30 captured domains at average ≤ $500 and is recouped within ≤ 24 months at 12-renter liquidity. | open | W3 §2b-bis (Rev-2 addendum). Coupled to A-W2-14. Capex line added to §2h capital plan. | W3 / W2 |

---

## Workshop 4 — Deliverability

| ID | Assumption | Status | Evidence / Pointer | Owner (Workshop) |
|---|---|---|---|---|
| A-W4-1 | ID verification at signup (Stripe Identity / Persona / Veriff, ~$1.00–$1.50/signup) raises identity-acquisition cost enough that 50-account abuse rings on a single domain become uneconomical at Rev-2 pricing. | open | W4 §2.5.2 + Rev-2 §8.3. Measurable via duplicate-identity audit on first 100 paid signups; coupled to A-Rev2-9. | W4 / Rev-2 |
| A-W4-2 | Standard-tier 200/day and Premium-tier 500/day **forwarding throughput limits** (platform-mediated forwarding, not Gmail send-as outbound) accommodate ≥ 95% of legitimate identity-email use without false-positive Tier 1 pauses. | open | W4 §Forwarding Throughput Limits (Rev-2.1 scope clarification). Concierge MVP cohort first probe; live cohort confirms once 100+ paid signups exist. K-W4-2a measures the false-positive rate. | W4 |
| A-W4-3 | Daily RBL monitoring (SpamHaus / SORBS / Barracuda) provides ≥ 24h lead time between first listing and catastrophic deliverability collapse, sufficient to pause forwarding and notify domain owner before broad recipient-side impact. | open | W4 §2 monitoring flow + Rev-2 §8.4. Measurable only with live incidents; relies on industry priors until then. | W4 / W6 |
| A-W4-4 | The 3-slot-per-ID-per-domain cap (with 20% surcharge on slots 2+) is acceptable to ≥ 90% of legitimate compound-slot renters. Family / household sharing of IDs is < 5% of intake (low collusion noise). | open | W4 §2.5.1. Measurable from first 100 paid signups; flag if intake patterns show >10% multi-slot per ID. | W4 |
| A-W4-5 | Annual forwarding-destination re-verification (renter must re-confirm Gmail destination once per year) catches ≥ 80% of compromised destinations with renter-acceptable friction (i.e., re-verification completion rate ≥ 90%). | open | W4 Red Team Vector 2 mitigation. Measurable from first 12-month cohort; concierge MVP can probe friction earlier. | W4 |
| A-W4-6 | Consumer Gmail send-as on a non-Google `.com` domain (with our SPF + DKIM + DMARC records) reaches inbox at Gmail, Outlook, Yahoo, Apple Mail, and Microsoft 365 with no "via gmail.com" sender mismatch and no DMARC quarantine/reject in aggregate reports. | **launch-blocking — open** | W4 Rev-2.1 Gate 0. Rubber-duck pass (2026-04-27) flagged that all of W4 + W3 + the Surname-Match ICP rest on this assumption being technically true at consumer-Gmail send-as fidelity. Empirical proof task to run before code build commences. **Failing this kills A-pre-1 and reopens W3 economics.** Coupled to K-W4-4. | W4 / pre-MVP technical proof |
| A-W4-7 | Mailgun forwarding reputation can be sufficiently isolated (per-domain subaccounts, per-cohort sending pools, or quarantine on incident) such that renter-induced reputation contamination on one rented domain does not cascade to delivery degradation on adjacent domains at >1.5× background rate. | **launch-blocking — open** | W4 Rev-2.1 §2.6. Mailgun account topology determination is a pre-launch blocker. If Mailgun does not support adequate isolation on our plan tier, mitigation cost lands in W7 risk reserve. Coupled to K-W4-5. | W4 / W6 |

---

## Rev-2 — Pricing & Namespace (2026-05-06)

Supersedes selected W1/W3 assumptions as noted. See `docs/08_pricing_namespace_rev2.md` for full memo.

| ID | Assumption | Status | Evidence / Pointer | Owner (Workshop) |
|---|---|---|---|---|
| A-Rev2-1 | Viable premium single-name slots per top-100 US surname = **7 (planning); range 5–12**. Top-10 surnames support 10–12; rank-100 supports 4–6. | open | First-principles bound from SSA top-100 first names × culturally-coherent-solo-local-part filter (doc 08 §2.1). Cross-check via W1 LP Variant B sign-ups on offered single-name slots per surname. | Rev-2 / W1 |
| A-Rev2-2 | 2-letter initials (`js@`, `jp@`) are priced in the Standard tier at MVP with a scarcity cap of **one per first-name-initial-pool per domain**; short-handle-premium mid-tier deferred to post-liquidity. | open | Design decision, doc 08 §2.2. Revisit with cohort data at month 18. | Rev-2 / W1 |
| A-Rev2-3 | **Tier-differentiated 12-month retention: Premium 80%, Standard 55%** (range 45–65%), 3C-Budget 45% if ever enabled. **Supersedes W1 A7** (70% blanket). | open | Concierge MVP cohort is weak proxy; only live 12-mo cohort resolves. Doc 08 §4. | Rev-2 / W3 |
| A-Rev2-4 | Standard-tier cost stack tolerates **$9/mo floor**, not the founder-proposed $5–$8. $5 is cash-flow-negative; $8 is marginal ($1.55 net); $9 nets $2.09. | open (math-derived, sensitive to support/abuse cost inputs) | Doc 08 §3.1. Validated if live cost-stack inputs hold within ±15% of modeled values over first 6 months. | Rev-2 / W3 |
| A-Rev2-5 | **≥ 60% of Y1 signed domains in top-200 US surnames** (tightened from W2 A-W2-7's ≥ 50%) — Rev-2 compound-tier density economics require larger bearer pools. | open | Tightening of A-W2-7; measurable from W2 exp-1 outreach composition. | Rev-2 / W2 |
| A-Rev2-6 | Standard-tier acquisitions can be sustained at **≥ 65% organic share (SEO + referral + owner-pull)** by month 18, **≥ 75% by month 30**. No paid channel clears the $24-at-1.8× standard-tier CAC ceiling. | open — **HIGHEST-PRIORITY Rev-2 unknown** | Doc 08 §5. First signal from W1 LP organic-channel-share tracking and first 6 months of live SEO. | Rev-2 / W1 |
| A-Rev2-7 | Surname landing pages with compound-slot listing increase SEO rankability (more unique internal targets, more UGC density) vs. single-SKU pages. | open | Hypothesis only; testable by SEO A/B on 20 surname pages at 3-month mark post-launch. | Rev-2 / W1 |
| A-Rev2-8 | Compound-slot abuse-reserve uplift of $0.25/renter-mo (blended to $0.40–$0.75) adequately covers 2.5× blast-radius increase **if** W4 commits to automated blacklist monitoring + tightened outbound rate limits (200/day on standard tier) in Y1. | open | Doc 08 §8. Gated by W4 final architecture decision. | Rev-2 / W4 |
| A-Rev2-9 | Compound-slot policy caps (3 slots/person/domain, 20% surcharge on slots 2+, ID verification, non-waivable $25 onboarding fee) hold abuse-ring setup uneconomical at Rev-2 pricing. | open | Doc 08 §8.1, §8.3. Measurable via duplicate-identity audit on first 100 paid signups. | Rev-2 / W4 |
| A-Rev2-10 | LP split-test (Variant B, per doc 08 §10.3) will show premium take-rate in the **15–25% range** (H-mid hypothesis). Outside this band forces repricing. | open — **Rev-2 central case gate** | K-Rev2-5. Doc 08 §2.3, §10.3. | Rev-2 / W1 |
| A-Rev2-11 | Owner-pitch dollar quote of "$2,500–$3,000/yr at liquidity" (vs W2's "$1,500–$2,500/yr") materially lifts cold-outreach conversion rate (target: ≥ 20% relative lift). | open | Split W2 exp-1 cohort by pitch dollar-amount to measure. | Rev-2 / W2 |
| A-W4-8 | ≥ 70% of the Surname-Match ICP either uses Gmail as a primary mailbox today *or* will accept creating a free Gmail account as a sending bridge during onboarding (per W4 §2.7 Gmail-bridge fallback). Equivalently: the share of ICP that is non-Gmail *and* refuses the bridge is ≤ 30%, leaving the remaining 70% addressable. | **launch-blocking — open** | W4 Rev-2.2 §2.7. Consumer "send-as via external SMTP" is functionally Gmail-only in 2026 (Outlook.com / Yahoo deprecated external send-as for consumers; iCloud / M365 require user-owned domains). The locked default fallback is a free-Gmail sending bridge for non-Gmail renters; if rejection rate is high, the marketplace is functionally Gmail-only and ICP must narrow. Coupled to **K-W4-6**. Measured by W1 LP-test "primary email today?" instrumentation (doc 05 §2g experiment 2) plus concierge-MVP bridge-acceptance rate. | W4 / W1 |

### W5 — Continuity (added 2026-04-27)

| ID | Assumption | Status | Source / Test | Owner |
|---|---|---|---|---|
| A-W5-1 | External counsel can deliver enforceable Master Owner Lease, Renter ToS, and regulatory-posture memos within MVP-launch budget ($15–35k internal estimate; not yet quoted). | **launch-blocking — open** | W5 §1.2, §1.3, §1.8. Required before code build. Counsel quote required to confirm. | W5 / W7 |
| A-W5-2 | The W2 sale-escape clause is enforceable in Delaware governing law against a third-party domain purchaser (i.e., the buyer is bound by, or constructively aware of, the migration obligation). Otherwise the clause is theatre. | **launch-blocking — open** | W5 §1.7. External counsel sign-off required pre-launch. Coupled to K-W5-1. | W5 |
| A-W5-3 | Cyber Liability + Tech E&O insurance is available to a marketplace of our profile at the modeled premium ($4.5–8k/yr, $1M aggregate, $25k deductible). | **launch-blocking — open** | W5 §1.6. Broker quote required. Coupled to K-W5-5. | W5 / W7 |
| A-W5-4 | Stripe Connect Custom keeps the platform outside money-transmitter classification in all 50 states under the marketplace-facilitator analysis. | **launch-blocking — open** | W5 §1.8 regime 6. External counsel sign-off required pre-launch. | W5 |
| A-W5-5 | Owner death/incapacity rate among the Dormant + Resigned cohort is ≤ 2% / year; succession-clause invocation rate is therefore manageable at 1–4 invocations/year at 50-domain steady state. | open | W5 §1.1 mode 5 + §1.2 clause 9. Measurable only with live cohort; relies on actuarial priors until then. | W5 / W6 |
| A-W5-6 | 10% owner rolling reserve over 180 days is sufficient to absorb chargebacks + owner-side dispute costs at K-W5-6 levels (≤ 1.5% chargeback rate). | open | W5 §3.3 + W2 §2j item 7. Coupled to K-W5-6. Measurable from first 6 months of live operations. | W5 / W3 |
| A-W5-7 | ≤ 30% sale-escapable inventory cap is sufficient to keep aggregate sale-escape invocation impact below renter-trust collapse threshold (renter-side complaint rate stays inside K-W5-4 thresholds). | open | W5 §Executive Summary + §1.7. Coupled to K-W5-1, K-W5-4. Y2 measurement after sale-escape inventory exists. | W5 / W2 |

---

*Last updated: W5 Continuity initial draft (2026-04-27) — added A-W5-1 through A-W5-7 covering counsel deliverability, sale-escape enforceability, insurance availability, money-transmitter avoidance, owner mortality priors, owner-reserve sufficiency, sale-escape inventory cap. Three are launch-blocking pending external counsel + insurance broker quote. Prior baseline: W4 Rev-2.2 sending-bridge dependency (2026-04-27) — added A-W4-8 (sending-bridge dependency, launch-blocking) coupling W4 architecture to W1 LP instrumentation. Earlier: W4 Rev-2.1 rubber-duck pass (2026-04-27) — A-pre-1 downgraded from "locked" to "conditionally locked"; A-W4-2 scope-clarified to "forwarding throughput limit"; added A-W4-6 (Gate 0) and A-W4-7 (Mailgun isolation). Earlier: W4 Rev-2 alignment (2026-04-26) added A-W4-1 through A-W4-5. Earlier baseline: Rev-2 close (2026-05-06). Pricing & namespace: two-tier Premium $25 / Standard $9, 50 renters/domain, blended ARPU $11, capital $245k central. W1 A7 superseded by A-Rev2-3; W2 A-W2-7 tightened via A-Rev2-5; K-W3-1/2/3 revised in `_kill_criteria.md`.*
