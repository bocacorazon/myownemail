# Supply Acquisition Workshop

**Date:** 2026-04-23
**Workshop:** 2 of 7
**Primary agent:** Domain Owner / Supply Advocate (offensive)
**Secondary reviewers:** Demand & Positioning Strategist, Marketplace Economics Analyst, Legal & Operations Expert
**Status:** DECISIVE — commits to an owner ICP, acquisition strategy, listing policy, and owner incentive model. All locked decisions pending falsification by the W2 evidence experiments flagged in §2h and the updated kill criteria in `_kill_criteria.md`.

> ### 📌 Revision 1 (2026-04-21 post-workshop)
>
> Founder pushback after the initial draft surfaced two material gaps:
>
> 1. **Professional squatters were dismissed too categorically.** The initial analysis treated "squatters" as a single archetype anchored to six-figure flips. In reality, a large portfolio's *long-tail dead inventory* (~95% of domains that generate ~$0/yr in parking and have never received a real offer) is economically distinct. With a **sale-escape clause** (owner retains a first-right-of-refusal to pull a domain at 180-day notice if a real offer materializes), these holders become a targetable archetype. This adds a third owner ICP: **Long-Tail Portfolio Squatters** (see §2a, §2b).
>
> 2. **Hispanic-surname `.com`s were buried as a "Phase-2 note" despite being squarely inside the W1 target pool.** Garcia, Rodriguez, Martinez, Hernandez, Lopez, Gonzalez are all top-15 US surnames by frequency, representing ~6M US adults with identity-dense surname patterns. They belong in the *primary* outreach plan with Spanish-language channel and a culturally-attuned pitch ("reclama tu apellido"), not deferred (see §3 and §2f updates).
>
> These revisions strengthen the Realistic scenario (§2i) but do **not** change the conditional-proceed verdict or the 90-day exp-1 kill gate. A separate founder question about **affinity domains (religion, hobby, politics)** — e.g., `catholic.com` — was evaluated and **logged as a Phase-2 exploration item only**; it fails the Surname-Match substitute test (affinity holders are commercial orgs with brand, not dormant individuals), so it is out of scope for MVP. See assumption register entry A-W2-11.

> **Existential question handed down from Workshop 1:**
> *"The surname beachhead solves the 'why us vs. substitutes' problem but creates a SUPPLY-SCARCITY problem: the exact domains with high renter demand are the hardest to acquire because the owners either (a) use them personally, (b) are squatters holding for a one-time sale, or (c) belong to a family trust that will not touch recurring-revenue contracts. If supply cannot clear, there is no marketplace."*
>
> This workshop's job is to answer that question honestly, including recommending a kill if the answer is "no."

---

## 1. Executive Summary

**Supply-side problem statement.** The Surname-Match ICP locked in W1 requires us to acquire, on a recurring-revenue basis, the specific `.com` domains that match common US surnames. That supply pool is structurally resistant: the most valuable names are either (a) used daily by their owners for personal email and therefore *unshareable without disrupting the owner's own identity*, (b) held by professional domain investors whose business model is one-time six- to seven-figure sales, not $75/month annuities, or (c) held by coincidentally-named businesses (Johnson Controls, Patel Motors) who will not risk their brand on a shared identity product. The subset that is *plausibly addressable* — dormant individual holders, accidental registrants, and small hobbyist holders — is a fraction of the pool, and the honest question is whether that fraction is large enough, cheap enough to reach, and willing enough, to launch a credible marketplace.

**Chosen owner ICP (locked).** **"Dormant Individual Holders"** — individuals (not businesses, not professional squatters) who registered a common-surname `.com` 8+ years ago, hold it under a personal name or WHOIS-privacy account, are *not* currently using it as a primary email domain, and have either parked it, put up a placeholder page, or let it sit on registrar default DNS. Secondary ICP: **"Resigned Squatters"** — small-portfolio (< 50 domains) individual investors whose asking prices have gone stale and who will trade a $5k imaginary sale price for real recurring income. **Tertiary ICP (Rev-1):** **"Long-Tail Portfolio Squatters"** — large-portfolio holders pitched on their *dead-tail inventory only*, contracted under a sale-escape clause that preserves flip optionality. Priority sub-segment across all three tiers: **Hispanic-surname `.com`s** (Garcia, Rodriguez, Martinez, Hernandez, Lopez, Gonzalez, Perez, and equivalents) with Spanish-language outreach and culturally-attuned pitch.

**Chosen acquisition strategy (locked).**
A two-tier funnel:
1. **Tier 1 — Concierge direct outreach.** Founder-led WHOIS/LinkedIn/certified-letter outreach to the top 200 US surname-matching `.com` domains, manually qualified, with a bespoke pitch. Target: 10–20 Tier-1 signings in the first 12 months.
2. **Tier 2 — Demand-pull ("we have N renters waiting for your domain") reverse auction.** Once we have a waitlist on `myownemail.com`, we contact the owner of each requested domain with a concrete revenue estimate derived from the waitlist size. Converts much warmer than cold. Target: 15–40 signings in months 6–18.

No performance marketing on the supply side — CAC math (§4) shows paid channels cannot clear.

**Realistic Year-1 supply estimate.** **15–28 live domains** under a realistic scenario (§2i), inclusive of the Rev-1 Long-Tail Portfolio segment if the sale-escape clause lands. This is at the low end of the 20-domain W1 beachhead target in the *realistic* case, above target in the *optimistic* case, and well below in the *pessimistic* case. Per-domain renter capacity (~25 renters at liquidity per W1) implies a Year-1 ceiling of **375–700 paying renter slots**, which is structurally compatible with the W1 target of 500 paying renters only if the realistic-or-better scenario holds.

**Go/no-go call on whether supply can plausibly clear.**
**CONDITIONAL PROCEED — with a hard 90-day supply-acquisition gate before any production build.**

The honest read: supply is the tightest risk in the entire business, tighter than demand. We cannot in good faith declare "supply clears" today; we can declare "supply is *plausibly* clearable for a beachhead of 12–25 domains *if* specific Dormant-Holder and Resigned-Squatter conversion rates hold." Those rates have never been tested. We therefore propose a **pre-build supply experiment** (§2h-exp-1): 90 days of concierge outreach to 100 qualified owners, target ≥ 8 signed letters of intent. If that bar is missed, we either (i) pivot to the "platform-owns-inventory" fallback (§2k) or (ii) kill the marketplace thesis. We do not proceed to W3/W4 execution planning as if supply is solved — it isn't yet, and pretending otherwise is how sunk-cost drift begins.

**Confidence level.** **LOW-MEDIUM (35%)** that the marketplace supply model as specified will clear Year-1 targets at acceptable CAC. MEDIUM (55%) that *some* form of supply model — possibly the "platform owns premium inventory" fallback — is viable. HIGH (80%) that the pure squatter-cold-outreach fantasy does not clear and should not be pursued.

---

## 2. Domain Owner / Supply Advocate Memo

### Three framework questions

**1. Strongest version of the problem in my lane.**
The domains we most need are the domains owners most want to keep private. The emotional weight of "it's my family name" cuts *against* us, not for us. A Johnson who registered `johnson.com` in 2001 either (i) uses it for email, in which case listing it on a marketplace would require them to migrate their own identity, or (ii) sits on it for sentimental reasons, in which case any listing — even a well-insulated one — feels like renting out the family silver. Professional squatters are economically rational but price-anchored to fantasy six-figure sales; recurring revenue at $75–150/month is not a category they recognize. Businesses and trusts introduce legal review costs that dwarf annual payouts. The residual pool — dormant personal holders who aren't attached and aren't speculating — is real but small, geographically diffuse, and expensive to reach one-by-one.

**2. Proposal that best addresses it with acceptable trade-offs.**
Concentrate all supply effort on Dormant Individual Holders and Resigned Squatters, acquire via concierge outreach (not paid), and lead with demand proof ("we have 47 people named Johnson on our waitlist") rather than a generic "list your domain" pitch. Accept that supply will be the binding constraint for Year 1; design the marketplace launch so that a thin beachhead of 12–20 domains is credible, not embarrassing. Reserve a **platform-owned inventory fallback** — buy 5–10 premium surname `.coms` outright in the $5k–$50k range if concierge cannot clear — as an insurance path rather than the primary plan.

**3. Unresolved failure mode / unknown.**
Conversion rate on cold outreach to Dormant Holders is the single largest unknown in the entire business. Reasonable estimates span 1–10%, an order of magnitude. If true conversion is at the low end, Year-1 supply clears at maybe 3–8 domains, which is sub-critical. There is also a latent legal-review cost we have not priced: even individual holders often want a lawyer to look at a 5-year lease, and a $400 legal bill per signed domain erodes a significant fraction of Year-1 owner payout. Finally, the "owner uses the domain for personal email" case — which may be *the majority* of the pool — has no product answer yet. That case is handed to §2g.

---

### 2a. The Supply Problem, Precisely Stated

#### What are we trying to acquire?
The **W1 Surname-Match ICP** implies a specific target domain set:

- **TLD:** `.com` exclusively for the MVP. `.net`, `.org`, and country-code TLDs fail the W1 premium-identity frame (a renter paying $15/mo to "claim their name" will not accept `bill@johnson.net`; the inferior TLD defeats the product).
- **String:** the exact single-word surname at the second level (e.g., `johnson.com`, not `johnson-family.com`, not `thejohnsons.com`).
- **Reputation floor:** domain age ≥ 5 years (thin MX history is acceptable; a prior spam history is not), no current active blacklist entries, no history of being used for fraud-adjacent activity.
- **Trademark cleanliness:** surname is not primarily associated with a single dominant commercial brand (see §2c for the Johnson & Johnson / Patel / Ford carve-outs).
- **Target list size:** the top ~500 US surnames by frequency (which cover roughly 40% of the US population; carried over from W1 assumption A1). Narrowed further by the exclusions above, the *actually-targetable* list is roughly **200–350 domains**.

#### Who holds these domains today?

First-principles estimate of holder composition for the top-500 US surname `.com` pool. These are reasoned estimates from visible signals (parking pages, active MX, WHOIS privacy, sale listings, registrar defaults), **not** measured data. A Phase-0 WHOIS audit (§2h-exp-0) is the fastest way to replace these with real numbers.

| Holder type | Est. share | How we infer it | Addressability |
|---|---:|---|---|
| Personal users (actively using the domain for email) | ~25% | MX record points to Google/Microsoft/Fastmail; domain resolves to a family/blog/portfolio site. | **Low** — sharing disrupts their own identity. |
| Dormant individual holders | ~15% | WHOIS shows individual + personal email; DNS on registrar default; no active website; no MX or MX at registrar parking. | **Medium-high** — PRIMARY TARGET. |
| Professional squatters — **premium inventory** | ~15% | Actively listed on Sedo/Dan/Afternic at $10k–$500k; recent inquiry activity; held as flip candidate. | **Low** — price-anchored to flips; acquiring here destroys unit economics. |
| Professional squatters — **long-tail dead inventory** (Rev-1 addition) | ~5% | Inside large portfolios (1,000+ domains); no active listing or stale listings for 5+ years; no inquiries; parking revenue ≈ $0. | **Medium** — TERTIARY TARGET, conditional on sale-escape clause. See §2b. |
| Resigned / small squatters (< 50 domains) | ~10% | Listed for sale but asking-price stale, or no listing but WHOIS shows individual in a domain-heavy country. | **Medium** — SECONDARY TARGET. |
| Coincidentally-matching businesses | ~15% | Active commercial site; MX serves the business; trademark traceable. | **Very low** — won't risk brand. |
| Family trusts / inherited holdings | ~3% | Generational transfer patterns; law-firm contact in WHOIS; held but not developed. | **Very low** — legal review kills the deal. |
| Foreign / non-English holders | ~7% | Non-US WHOIS address; often Chinese or Turkish investor portfolios. | **Very low** — channel, language, and jurisdiction friction. |
| Dead / unreachable / abandoned-pending-expiry | ~5% | No response, bounced WHOIS, auto-renewing zombie. | **Zero short-term** — backorder strategy only. |

**Reasoning check.** Quantitative sanity: the proportion of `.com` domains under WHOIS privacy has been reported north of 50% in industry writeups over the past decade. Surname `.com`s skew toward longer-held, more personal holdings, so privacy rates may be even higher — which reduces observable signal and makes the estimates above fuzzy by design. A 90-day audit (§2h-exp-0) would reduce the uncertainty.

**Addressable share (Dormant + Resigned Squatters + Long-Tail Portfolio Squatters):** **~30%** of the top-500 pool, or roughly **120–210 domains** that are *theoretically reachable with an acceptable pitch*. The Long-Tail Portfolio segment (~5% / ~25 domains) is new in Revision 1 and is gated on agreeing a sale-escape clause; if that clause cannot be structured cleanly (legal and renter-migration costs), this segment collapses back to "Low addressability." Conversion from the full pool to signed leases is the open question.

#### Why is this supply uniquely hard?

Five structural properties distinguish this supply problem from a typical marketplace cold-start:

1. **The asset is identity-laden for the holder.** Unlike Airbnb (a spare bedroom), Turo (an idle car), or Etsy (an artisan product), a surname domain is often *emotionally tied* to the holder's family name. The monetization pitch collides with sentiment, which is not a rational negotiation surface.
2. **The economically rational holders (squatters) are anchored to the wrong order of magnitude.** A professional squatter sees a single `$250k sale someday` and cannot mentally convert that to a `$1,800/year annuity with a 5-year payback.` Recurring income is a different asset class than flips, and flip-anchored holders are not our customer.
3. **One-to-one acquisition, not catalog acquisition.** We cannot "open supply to the public" and get 10,000 surname `.com`s. Each domain is a bespoke conversation with one individual. CAC is labor-bound, not ad-bound, and labor is the most expensive input.
4. **Supply-demand topology is inverted from most marketplaces.** In most marketplaces, demand is thin and supply is abundant (early Airbnb had lots of spare rooms; the hard part was finding guests). Here supply is *rarer* than demand: a single onboarded domain serves 25+ renters, meaning supply, not demand, gates liquidity.
5. **Every signed domain carries a "rug-pull" tail risk** that the owner walks away, forcing renter migration. That tail cost has to be either priced into the take rate or legally engineered out (W5). Neither is free.

This supply problem is closer to acquiring small-town radio stations in the 1990s than to onboarding Uber drivers.

---

### 2b. Holder Segment Analysis

For each holder type, listed tersely.

#### Personal users (actively using for email)
- **Motivation to list:** Almost none for the email holder. For a family head who currently uses `dad@johnson.com` but whose adult children also want `bill@`, `sarah@` — *slight* motivation if we can serve both.
- **Motivation to refuse:** Disruption to their own email identity. Perceived loss of control.
- **Expected cold conversion:** **< 1%.**
- **Required carrot:** A "family plan" where the owner retains their primary address and earns revenue from additional aliases — essentially no disruption plus upside.
- **Risk profile:** HIGH. Owner-as-also-user entangles admin/read separation, complicates succession, and creates conflict-of-interest on renter approvals.
- **Verdict:** **Ignore for MVP.** Revisit with a "family plan" product variant in Phase 2 only.

#### Dormant individual holders
- **Motivation to list:** $1,500–2,500/yr passive income from an asset they are not using; validation of the domain's value; occasional ego lift ("turns out my name is worth something").
- **Motivation to refuse:** Inertia; distrust of small platforms; worry about spam attribution to "their" domain; tax paperwork; legal discomfort with a 5-year commitment.
- **Expected cold conversion:** **3–8%.**
- **Required carrot:** Clear monthly number, no-cost setup, founder-signed lease, small signing bonus ($100–250), short renewable term (1-year auto-renew, not 5-year lock-in), RBL-triggered auto-pause.
- **Risk profile:** Low-medium. Main churn driver is inertia on renewal rather than active abandonment.
- **Verdict:** **PRIMARY TARGET.**

#### Professional squatters / large-portfolio investors
- **Motivation to list:** Minimal. Their business model is flips. Annuities are a rounding error.
- **Motivation to refuse:** Opportunity cost vs. perceived flip value. Often contractually tied to auction platforms.
- **Expected cold conversion:** **< 0.5%.**
- **Required carrot:** Nothing short of guaranteed buyout option at their asking price — which destroys our unit economics.
- **Risk profile:** Medium (often savvy counterparties who will try to extract favorable clauses).
- **Verdict:** **Ignore.** Do not waste outreach budget here.

#### Resigned / small squatters
- **Motivation to list:** An underperforming portfolio item generating zero. A $1,500/yr recurring stream on one domain is a plausible outcome; flip has not materialized in years.
- **Motivation to refuse:** Asking-price anchoring; belief that recurring income locks them out of a future big sale (our contract must permit sale with 90-day notice to renters).
- **Expected cold conversion:** **5–12%.**
- **Required carrot:** Clean exit rights, no listing exclusivity, immediate monthly payment, no lockup beyond a 90-day notice.
- **Risk profile:** Medium. Highest voluntary churn if a real flip offer arrives. This has to be priced in.
- **Verdict:** **SECONDARY TARGET.**

#### Long-Tail Portfolio Squatters (Rev-1 addition)
- **Motivation to list:** Most of a large squatter portfolio is **economically dead** — ≥ 95% of domains generate ≤ $20/yr in parking and have never received a serious inquiry. On that tail, $600–$2,400/yr of recurring income is a dramatic upgrade over zero. Portfolio holders are economically rational on the long tail in a way they are not on their premium names.
- **Motivation to refuse:** Lease encumbrance on a domain reduces its sale value. They will only list *if* optionality on a future flip is preserved.
- **Expected cold conversion:** **3–8%** on the dead-tail subset of a single portfolio, *conditional on a sale-escape clause*. Without the clause: < 0.5% (collapses to flip-anchored squatter behavior).
- **Required carrot / deal structure:**
  1. **Sale-escape clause.** Owner may pull the domain with 180-day notice *if* a bona-fide third-party offer above a floor price (e.g., $25k) materializes. Platform pays renter-migration costs; owner pays a modest $X exit fee into the migration reserve.
  2. **Bulk intake.** Owner lists 10–50 dead-tail domains at once; platform's operational cost per domain drops sharply under bulk.
  3. **No upfront signing bonus required** (unlike Dormant Holders) — the sale-escape clause IS the carrot.
- **Risk profile:** **Higher renter-side tail risk** than other segments (sale-escape creates a structural sudden-migration possibility). Must be disclosed to renters transparently (e.g., "Standard-tier" domains may be sale-subject; "Premium-tier" domains are sale-free). This is a legit pricing/tier design topic for W3.
- **Verdict:** **TERTIARY TARGET with sale-escape clause.** Potentially unlocks 10–25 additional Y1 domains if contracting works. Gated by the clause being operationally and legally sound — hands off to W5 (Continuity) for the legal structure and W3 (Economics) for the migration-reserve cost.

#### Coincidentally-matching businesses (e.g., `ford.com`, `patel.com` held by a business named Patel)
- **Motivation to list:** None that survives brand protection.
- **Motivation to refuse:** Brand contamination risk is catastrophic — a single spam incident becomes a PR problem for their business.
- **Expected cold conversion:** **< 0.2%.**
- **Verdict:** **Hostile. Do not pursue.**

#### Family trusts / inherited holdings
- **Motivation to list:** Modest recurring income to the trust.
- **Motivation to refuse:** Trustee fiduciary duty requires legal review; legal review costs more than 2 years of payout; family disagreement is common.
- **Expected cold conversion:** **< 1%, with a long closing cycle.**
- **Verdict:** **Ignore.** Legal friction eats economics.

#### Foreign / non-English-speaking holders *(supply side — not to be confused with Hispanic-surname demand, addressed in §2f)*
- **Motivation to list:** If the US surname happens to match no local identity (e.g., a Chinese investor holding `patel.com` purely speculatively), motivations are investor-like — see "Professional squatters." If the holder *is* a surname-bearer in a non-US country (e.g., a Mexican Garcia holding `garcia.com` for personal use), the Dormant Holder analysis applies with a Spanish-language channel.
- **Motivation to refuse:** Language, time-zone, and legal-jurisdiction friction on the investor subset.
- **Expected cold conversion:** **< 1%** for investor holders before localized outreach. For surname-bearing individual holders in Latin America, Spain, or elsewhere, **conversion likely tracks the Dormant Individual Holder rate (5–15%) provided outreach is in the holder's primary language.** This subset is *not* "ignore" — it is a language/channel problem, not a fundamental fit problem.
- **Verdict:** **Ignore the investor subset.** Pursue the surname-bearing individual subset within the Hispanic-surname sub-segment of the primary outreach plan (§2f).

#### Dead / unreachable
- **Verdict:** **Backorder strategy.** Place registrar backorders on promising expiring-soon names via SnapNames / DropCatch. Zero short-term supply, but occasionally a domain falls through.

---

### 2c. Listing Policy

#### Which surnames?
- **Include:** Top 500 US surnames by frequency, excluding the exclusions below. (Source: SSA/Census frequency data, publicly available.)
- **Minimum population:** Surname held by ≥ 50,000 living US adults (rough proxy: any name in the top 1000 list clears this). Below this threshold, demand pool per domain is too thin to support liquidity.
- **Exclude — ambiguous/rare surnames:** Names with < 20,000 US bearers; demand pool per domain cannot hit the 25-renter liquidity target.
- **Exclude — celebrity or politically charged surnames:** Trump, Kardashian, Musk. Impersonation, harassment, and platform-policy risk outweigh renter value.

#### Which TLDs?
- **MVP:** `.com` only. This is not negotiable for the W1 "premium identity" frame.
- **Phase 2:** `.family`, `.name`, and country-code TLDs (`.co.uk`, `.ca`) for expansion ICPs. Out of scope here.

#### Trademark collisions
- **Per-surname trademark screen.** Before a domain is listed, we run a one-time USPTO + EU TMview + WIPO screen on the surname. If the surname is *primarily* associated with a single dominant commercial brand (Ford → Ford Motor, Disney → Disney, Hermès → Hermès), we do not list regardless of owner willingness. The trademark holder's right to assert consumer confusion would likely force delisting; better to not enter the obligation.
- **Ambiguous cases (Johnson, Patel, Kennedy):** List, but bake trademark indemnification into the owner contract and the renter TOS. W5 owns the final contract language.
- **Reserve list for trademark defense:** Any domain where trademark collision is borderline gets a pre-published "no local-part will impersonate a known brand" carve-out (see reserved local-parts below).

#### Reserved local-parts (platform-level, on every listed domain)
Regardless of owner preference, the following local-parts are reserved and never rentable:
- **Infrastructure:** `admin`, `administrator`, `postmaster`, `abuse`, `webmaster`, `hostmaster`, `noreply`, `no-reply`, `support`, `help`, `info`, `contact`, `security`, `privacy`, `legal`, `dmca`. (Many of these are required by RFC 2142 or by mailbox-provider AUP; we cannot surrender them.)
- **Platform:** `billing`, `accounts`, `platform`, `myownemail`, `service`.
- **Financial-scam lures:** `bank`, `wire`, `pay`, `payments`, `bitcoin`, `crypto`, `wallet`.
- **Authority impersonation:** `irs`, `treasury`, `gov`, `police`, `fbi`, `court`.
- **Adult content:** Names with obvious sexual content. Enforced by a prefilter plus manual review.
- **Owner-reserved:** The owner may reserve up to **20 local-parts** for personal use, family members, or known conflicts. Example: on `johnson.com`, the owner reserves `dad`, `mom`, `bill`, `sarah`, and their kids' names. These are pre-declared at listing time.

#### Adult / regulated categories
- **No listings in adult, firearms, cannabis, or gambling verticals** for the MVP. Enforced by a domain-intake questionnaire. Re-examined post-MVP.

#### Minimum domain age / reputation
- **Age ≥ 5 years** since first registration.
- **Clean RBL history** at listing time (SpamHaus, Barracuda, SORBS, plus Google Postmaster check where accessible).
- **No active DMARC rejection policies from known senders** (signal of past abuse).
- If the domain has a sketchy reputation history, it is excluded for MVP even if the current owner is clean.

---

### 2d. Owner Protections & Controls

Owners must feel that the platform works *for* them, not extracts from them. Protections:

1. **Local-part blocklist (§2c).** Owner pre-declares up to 20 reserved local-parts at listing time; can add new reservations on 30-day notice.
2. **Renter approval rights.** Per-domain owner toggle: `auto-approve all applications` (default) or `owner-approves-each`. The latter is friction for renters; we recommend it only for surnames with a specific brand sensitivity.
3. **Reputation protection — auto-pause on RBL hit.** If the domain enters any major blacklist, all outbound send-as use is suspended pending investigation. (Forwarding-only architecture makes this cheap to do.)
4. **Revenue floor guarantee.** For the first 12 months after signing, a **minimum $50/month** payout regardless of renter count. Platform-subsidized; retires at month 13 or when 3+ renters active, whichever comes first. This is the single most important CAC-substitute tool we have.
5. **Exit rights.** Owner may terminate with **90 days' written notice**, no penalty, for any reason. During the notice period, the platform stops onboarding new renters and begins renter migration. This is intentionally renter-unfriendly but owner-friendly; without it, owners will not sign.
6. **Transparency.** Owner dashboard shows: number of active renters, reserved local-parts, gross platform revenue on their domain, their 40% payout, abuse incidents (count, not content), RBL checks. **Owner never sees renter identities or email content** — architectural guarantee from W4.
7. **Reserve / escrow.** Platform holds a **10% rolling reserve** on owner payouts for the first 180 days of each domain's listing. Reserve covers chargebacks, abuse cleanup, and owner-side legal issues. Released to owner at day 180, then payouts go full.
8. **Sale-friendly terms.** Owner may sell the underlying domain at any time, subject to buyer assuming the lease OR a 90-day migration window. This is what makes Resigned Squatters signable.
9. **Succession clause.** In the event of owner death/incapacitation, platform continues operating the domain under a 12-month continuity arrangement with the owner's registrar of record, payouts held in escrow for heirs. (Full mechanics: W5.)

---

### 2e. Owner Objections & Responses

1. **"I use this email personally — I can't share my domain."**
   *Response:* Then this isn't the right product for you today. In Phase 2 we may offer a family-plan variant where you keep your primary address and earn from additional aliases, but for now we only list domains the owner is not actively using for email. We walk away and flag the domain for backorder.

2. **"What if a renter does something embarrassing or illegal?"**
   *Response:* Forwarding-only architecture means renters cannot send via your domain's SMTP at all — they send via their own Gmail's send-as, through Gmail's infrastructure. Your domain's reputation is architecturally isolated from their outbound behavior. We also auto-pause on any blacklist event, vet all renters at onboarding, and maintain a 10% reserve for cleanup. In the worst case, you can terminate on 90 days' notice.

3. **"Can I get out if I change my mind?"**
   *Response:* Yes, any time, with 90 days' written notice. We use the notice period to migrate renters; you keep the domain and walk away. No penalty, no fee, no lawyer required.

4. **"How much will I actually make?"**
   *Response:* At the target density of 25 renters per domain, gross monthly is $375 (25 × $15), you get 40% = **$150/month, or $1,800/year**, net of nothing (we absorb Stripe, support, abuse, CAC). Premium-tier surnames (top-100 US) can clear $2,000–2,500/year. During ramp-up, we guarantee a $50/month floor for your first year.

5. **"Will my family name be publicly associated with spam?"**
   *Response:* Architecturally no (see #2). Operationally we enforce a reserved-local-parts list (admin, bank, etc.) and an onboarding KYC on every renter. Our contract also gives you veto on any application that worries you.

6. **"What happens to my domain when I die?"**
   *Response:* Your registrar account controls the domain; we never do. On death/incapacitation, your estate inherits both the domain and the active lease; payouts queue in escrow until the estate directs us where to send them. If the estate wants to terminate, the standard 90-day notice applies.

7. **"Is this a scam?"**
   *Response:* Fair question. Here's what we actually are: a two-sided marketplace monetized via Stripe Connect. Your payments come from Stripe, not us. You control DNS the entire time — MX records point at us, nothing else changes. You can audit every renter count and payout on your dashboard. You can walk in 90 days. And here are [3] references from earlier onboarded owners.

8. **"Why wouldn't I just sell it outright?"**
   *Response:* If someone is offering you a number you're happy with, you should take it. Most `.com` domains held by individuals don't see that offer and sit untouched for decades. Our deal is an income stream from an asset that is otherwise generating zero. You can also sell while leased — the lease transfers (or pays out on a 90-day wind-down); we don't lock you out of a future sale.

9. **"What if I want to sell the domain later?"**
   *Response:* Covered — see above. The lease does not create an ROFR for the platform, does not require our consent to sell, and transfers on sale with renter continuity handled by us.

10. **"Who's actually going to send me the $150? Are you venture-backed? What if your startup dies?"**
    *Response:* Payouts are direct Stripe Connect transfers — you get paid even if we die, as long as Stripe processes renter charges. In the event of platform shutdown, renters are notified, payments halt, and you get your domain back unchanged (MX flips back to you). We also hold a cash reserve sized to 3 months of owner payouts — worst-case-wind-down buffer.

---

### 2f. Acquisition Channels & CAC

Estimates are first-principles; ranges reflect the uncertainty across holder types. **Labor cost assumed at $50/hr founder time, $25/hr contractor time.**

| Channel | Mechanism | Conversion | Labor / $ per contact | CAC per signed domain | Time-to-close | Verdict |
|---|---|---:|---:|---:|---|---|
| **Direct cold outreach — certified letter** | WHOIS lookup → paper letter with QR code and pitch | 2–6% | ~$8 letter + $12 labor = $20 | **$330–$1,000** | 6–12 weeks | Primary channel for non-privacy WHOIS. |
| **Direct cold outreach — email via WHOIS** | WHOIS email or privacy-relay email | 0.5–2% | ~$10 labor | **$500–$2,000** | 4–8 weeks | Low response rate; privacy-relay filters most. |
| **LinkedIn outreach** | Identify probable owner via cross-referencing WHOIS hints / domain history / personal site footer; InMail | 2–5% | $30 labor (incl. sourcing) | **$600–$1,500** | 4–10 weeks | Works only when owner is identifiable. |
| **Demand-pull (waitlist-backed pitch)** | "We have 47 people named Johnson on our waitlist; estimated $160/mo" | 10–20% | $40 labor + $15 letter | **$275–$550** | 3–6 weeks | **Best channel, but requires a waitlist first — not available at day 0.** |
| **Paid search (Google: "sell my surname domain", "johnson.com value")** | Ad → landing page → owner lead | 0.1–0.5% of clicks become leads; 3–10% of leads sign | $5–$15 CPC | **$1,500–$10,000** | Variable | **Does not clear.** |
| **Paid social (Meta, LinkedIn)** | Targeted to US surname cohorts, "monetize your unused domain" | 0.05–0.2% of impressions become leads; 3–8% of leads sign | — | **$1,500–$6,000** | Variable | **Does not clear.** |
| **Registrar partnerships (GoDaddy, Namecheap)** | Registrar offers "monetize your domain" at renewal | 0.5–2% | Rev share + integration | **$200–$600 if it works** | 6–18 months | High-leverage but requires a deal we cannot yet close. Parked for Year 2. |
| **Domain broker concierge** | Pay a broker 10% of first-year gross to source and close | 5–15% (of brokered list) | Commission only | **$180–$500** | 4–8 weeks | Good for 5–10 targeted acquisitions once we have budget. |
| **Inbound PR / earned media** | "Marketplace turns your unused surname domain into $2k/yr" story | N/A | ~$2k PR agency retainer | **$100–$400 if it works** | 2–6 months | Unpredictable; high variance; Phase 2. |
| **Referral (onboarded owner refers peer)** | $250 per signed referral | 20–30% of leads; leads are rare | $250 bounty | **$400–$800** | 2–4 weeks | Only available once we have owners to refer. |
| **Founder attendance at surname/genealogy communities** | Reunions, Ancestry forums, Facebook groups | N/A; relational | Time-intensive | **$200–$500** | Months | Niche but genuine fit with the Surname-Match ICP. |
| **Spanish-language concierge outreach (Rev-1)** | WHOIS + certified letter + WhatsApp-style outreach, Spanish-language pitch ("reclama tu apellido"), localized to Hispanic-surname holders (including LatAm-resident holders of US-surname `.com`s) | 4–10% | ~$15 letter + $15 labor = $30 | **$300–$750** | 6–12 weeks | **Priority sub-channel** — Garcia/Rodriguez/Martinez/etc. are top-15 US surnames; culturally-attuned pitch plausibly lifts conversion above English-language cold outreach. Test cohort in exp-1. |
| **Bulk dead-tail pitch to large portfolio holders (Rev-1)** | Direct approach to known portfolio holders with sale-escape bulk contract covering 10–50 of their parked surname `.com`s | 3–8% at the holder level (all-or-nothing per holder) | ~$200 labor + legal per holder engaged | **$200–$500 per signed domain** if bulk deal lands | 8–16 weeks | Conditional on W5 sale-escape sign-off. Concentrated, binary outcome per holder. |

**Key takeaway.** The only channels with CAC below **$500/domain** are (a) waitlist-backed demand-pull, (b) domain-broker concierge, and (c) referral — and (a) and (c) require us to already have users and owners, which we don't at day 0. Cold outreach (letter, LinkedIn) clears at **$300–$1,500/domain**, which is expensive but survivable given an owner LTV of $3,600+ over 24 months (at $150/mo × 40% × 24).

**Paid marketing for supply does not clear.** Do not build a supply funnel on Google or Meta.

---

### 2g. The Four Hardest Holder Archetypes — Deep Dive

#### (i) Personal users who use the domain for their own email

**Why this is hard.** The dominant answer is "you can't have my domain while I'm using it." Forcing a share breaks their own identity. The platform's forwarding-only architecture compounds the problem — their email becomes dependent on our uptime.

**Playbook.**
- **Do not pitch single-user ownership-to-marketplace conversion in MVP.** The economics do not justify asking them to migrate.
- **Phase 2 family-plan variant:** Owner retains `dad@johnson.com`, we onboard `bill@`, `sarah@`, `grandma@`, etc. Owner earns on aliases and keeps their primary. Requires per-user inbound isolation we don't have in MVP.
- **Low-effort cultivation:** Add these owners to a "not now, stay in touch" list. When our brand is proven (Year 2), the pitch lands differently.

**Verdict.** Do not spend MVP outreach budget here.

#### (ii) Professional domain squatters (large-portfolio investors)

**Why this is hard.** They anchor to six-figure flip outcomes. A $1,800/year annuity registers as noise.

**Playbook.**
- **Do not pitch the standard lease.** Offer a **hybrid "option contract"** instead: 18-month lease at $150/mo (which yields $2,700), with a buyout option at the owner's listed asking price retained. That is a $2,700 free option from the platform's view; it only makes sense on select premium names where the waitlist is already deep.
- **Reverse-auction on our waitlist:** "We have 62 Johnsons waiting at $15/mo each; we'll pay you $250/mo for 18 months on a non-exclusive basis with your sale rights intact."
- **Expect < 0.5% conversion** even with the hybrid offer.

**Verdict.** Pursue only for 3–5 top-priority premium names where the waitlist justifies the option premium. Not a volume channel.

#### (iii) Family trusts / inherited holdings

**Why this is hard.** Trustees have fiduciary duty. Fiduciary duty requires legal review. Legal review costs $500–$2,000 per deal. Deal economics do not justify the review.

**Playbook.**
- **Offer a pre-approved, simplified 1-page lease** drafted specifically to minimize trustee review cost. Standardized enough that many trust lawyers could greenlight it in < 1 billable hour.
- **Flat $400 closing credit** to the trust to cover nominal legal review.
- Still expect **< 1% conversion and 4–6 month closing cycles**.

**Verdict.** Deprioritize. Pursue opportunistically only if a trust-held top-50 surname comes up and we have capacity.

#### (iv) Long-Tail Portfolio Squatters — the Rev-1 opening (NEW)

**Why this is hard.** Portfolio holders *appear* structurally identical to Professional Squatters — same WHOIS patterns, same Sedo/Afternic listings, same "make an offer" auto-responder. But **~95% of any large portfolio is economically inert**: it has never received a real offer, parking revenue is near zero, and renewal fees are a steady cash drain. The obstacle is not that these domains are too valuable to lease — it is that the holder *doesn't want to give up the lottery ticket* on a future flip.

**Playbook.**
- **Bulk-inventory pitch.** Target 5–10 well-known US portfolio holders (the category is small and concentrated). Offer a single bulk contract covering 10–50 dead-tail surnames simultaneously, reducing per-domain ops cost.
- **Sale-escape clause as the lead-with carrot.**
  - Owner may terminate any individual lease with **180-day notice** upon receipt of a bona-fide third-party offer above a floor (e.g., $25k verified).
  - Platform receives first-right-of-refusal to match at 95% of the offer price (preserves platform's ability to retain inventory it has built renter cohorts on).
  - If owner proceeds with sale, owner pays an **exit fee** (e.g., $500/renter or one month of forgone platform net) into a migration reserve that funds renter reassignment to an equivalent surname domain or refund-with-credit.
  - Renters on sale-escapable domains get disclosed "Standard-tier" pricing vs. sale-free "Premium-tier" (pricing tiering to be finalized in W3).
- **Disclosure discipline.** Renter churn from surprise domain-recalls kills the platform's trust. Sale-escape only works if it is surfaced clearly at signup, insured with a credible migration process, and capped to a minority of live inventory (proposed: ≤ 30% of live domains can be sale-escapable).

**Expected conversion:** 3–8% on contacted dead-tail inventory, *conditional on the sale-escape clause clearing legal review in W5*. Potentially unlocks **10–25 additional Y1 domains** on top of the Dormant + Resigned pipeline, at lower per-domain acquisition cost (bulk discount) — but introduces a new operational cost center (migration reserve) and a new kill criterion (K-W2-8, sale-escape abuse rate).

**Verdict.** **PURSUE IN PARALLEL WITH EXP-1**, gated by two conditions: (a) W5 Legal & Ops signs off on the sale-escape clause as enforceable and not adverse-selection-prone, and (b) at least one large portfolio holder engages substantively during the 90-day window. If either fails, this segment collapses back to "ignore" and we re-anchor on the Dormant + Resigned pool only.

---

### 2h. Supply Liquidity Model

#### Year 1 / 2 / 3 targets and realistic acquisition rates

Assuming addressable pool of ~180 Dormant + Resigned + Long-Tail Portfolio holders in the top-500 surnames (post-Rev-1), realistic cold-outreach conversion of 3–8% on Dormant/Resigned and 3–8% bulk-contract conversion on Long-Tail Portfolio:

| Year | Outreach volume (contacts) | Realistic conversion | Signed domains added | Cumulative signed | Cumulative live (after churn) |
|---|---:|---:|---:|---:|---:|
| Year 1 | 300 + 8 portfolio holders + Spanish-language cohort | 4–7% Eng / 4–10% Esp / 3–8% bulk | 15–25 | 15–25 | 13–23 (10% churn) |
| Year 2 | 700 (incl. demand-pull, Spanish-language expansion) | 6–11% | 40–70 | 55–95 | 49–88 |
| Year 3 | 1,100 (incl. referral + PR) | 8–13% | 90–140 | 145–235 | 131–220 |

**Conversion assumptions improve in Y2/Y3** because (a) waitlist-backed pitches convert 2–3× better than cold, (b) referrals compound, (c) PR and social proof from first 20 owners de-risks the pitch for later owners.

#### Renters per domain at liquidity

- W1 sets a target of **25 renters per active domain**.
- Theoretical ceiling per domain is much higher (hundreds of named bearers of the top surnames exist), but practical ceiling is bounded by awareness and conversion: the product has to be discoverable to the right-named person at the right moment.
- **Realistic steady-state: 15–40 renters per domain** for top-100 surnames; 5–15 for surnames 100–500.

#### Minimum viable supply for launch

- **Floor:** 8 live domains. Below this, the product's category page is visibly empty and the "Claim your name" promise looks unsubstantiated.
- **Credible:** 15 live domains, including at least 5 top-100 surnames. Gives enough coverage for the top surname-match searches and enough inventory to support a paid demand experiment.
- **Comfortable:** 25+ live domains.

The 90-day supply experiment (§2h-exp-1) targets the floor of 8, explicitly as the gate for proceeding.

#### Chicken-and-egg start

Supply leads demand in our model:
1. **Month 0–3 (Supply-first):** Founder-led outreach to top 100 surnames; no renter product live; target 8 LOIs / soft commits.
2. **Month 3–6 (Waitlist):** Landing page goes live showing active/coming-soon domains; renter waitlist opens; demand-pull pitches deployed to Tier-1 holders backed by waitlist numbers.
3. **Month 6–9 (Beachhead launch):** First 8–12 domains live with renter onboarding; concierge-assisted setup.
4. **Month 9–12 (Self-serve):** Paid renter acquisition switches on; supply growth continues via demand-pull and referrals.

The fragile phase is 0–6. A failure to sign 8 domains by month 3 triggers the kill/pivot decision in §2j.

---

### 2h-exp. Pre-Build Supply Experiments

Before any technical execution commits, three experiments are required:

- **exp-0 — WHOIS & holder-type audit (2 weeks, ~$1,500).** Pull WHOIS on all top-500 US surname `.coms` (where publicly visible), classify by holder type using the §2a taxonomy, and convert the §2a percentage estimates into a measured pool size. Replaces the "probably 25%" estimates with actual numbers. Informational only; does not gate.
- **exp-1 — 90-day concierge outreach (90 days, ~$8,000–$13,000).** Contact 100 Dormant/Resigned holders via letter + LinkedIn + WHOIS email, *including a dedicated Spanish-language cohort of ≥ 25 Hispanic-surname-holding contacts (Rev-1)*, and engage 5–8 large-portfolio holders with the Rev-1 sale-escape bulk pitch. Record response rate, WTS rate, LOI rate, and reasons-to-refuse — stratified by language cohort and by Dormant/Resigned/Portfolio segment. **GATE: ≥ 8 signed LOIs total (counting at most 3 from any single portfolio holder) or kill/pivot.**
- **exp-2 — Synthetic owner pitch test (3 weeks, ~$2,000).** Recruit 10 panelists matching the Dormant-Holder profile via Prolific (adults 45+, US, own ≥ 1 domain not used for email). Show them the pitch; measure reaction, objections, stated-likelihood-to-sign. Informational — feeds pitch iteration for exp-1.

**Total Phase-0 supply budget: ~$10k–$14k over 90 days.** If this experiment does not clear, no further money is spent on the marketplace thesis.

---

### 2i. Three Numeric Scenarios

All three scenarios assume the W1 pricing (blended ARPU ~$15/mo, 60/40 split, so $9/renter/month to platform, $6/renter/month to owner), 25 renters per domain at steady state, and a 12-month ramp to liquidity on each domain.

#### Optimistic — "The pitch works and the waitlist compounds"
- Year-1 domains onboarded: **22** (high end of §2h)
- Blended CAC per domain: **$400**
- Year-1 supply acquisition cost: **$8,800**
- Average renters per domain by month 12: **12** (ramping)
- Year-1 paying renters: ~265
- Year-1 revenue (gross): 265 × $15 × avg 5 months live = **~$20k**
- Year-1 platform net: ~$12k (after 40% owner share)
- **Verdict:** Below W1's 500-renter target, but above the 150-renter kill floor. Proceed.

#### Realistic — "Conversion is mid-band; waitlist helps but slowly"
- Year-1 domains onboarded: **15**
- Blended CAC per domain: **$600**
- Year-1 supply acquisition cost: **$9,000**
- Average renters per domain by month 12: **8**
- Year-1 paying renters: ~120
- Year-1 revenue (gross): ~$9k
- Year-1 platform net: ~$5.4k
- **Verdict:** Misses W1 K7 (150-renter / $1,500 MRR month-12 threshold). **Triggers K7 kill/pivot.** Note: this is the scenario we should plan against, which is why K7 needs to be taken seriously as a gate.

#### Pessimistic — "Cold conversion is 1–2%, waitlist does not compound"
- Year-1 domains onboarded: **6**
- Blended CAC per domain: **$1,200**
- Year-1 supply acquisition cost: **$7,200**
- Average renters per domain by month 12: **4**
- Year-1 paying renters: ~25
- Year-1 revenue (gross): ~$1,500
- Year-1 platform net: < $1,000
- **Verdict:** Marketplace model kills itself. Fallback to §2k-(i) "platform owns inventory" or full abandonment.

**Scenario weights:** Optimistic 20%, Realistic 50%, Pessimistic 30%. **Expected value of Year 1 under these weights: ~13 domains, ~130 renters, ~$9k gross, ~$5k platform net** — below W1's K7 threshold.

**This is the uncomfortable number.** Under expected-value planning, the marketplace misses its Year-1 kill criterion. The supply experiment (§2h-exp-1) is therefore essential not as a formality but as the honest gate before we commit additional resources.

---

### 2j. Supply-Side Kill Criteria (Numeric)

Added to `_kill_criteria.md` as W2 entries.

| # | Criterion | Threshold | Trigger |
|---|---|---|---|
| K-W2-1 | Concierge outreach conversion (90-day exp-1) | **< 5%** signed LOI from 100 qualified contacts → KILL or PIVOT to §2k fallback | 90-day gate |
| K-W2-2 | Blended supply-side CAC per signed domain | **> $1,000** over 90-day experiment → PIVOT to alternative channels; **> $1,500** → KILL | Continuous after exp-1 |
| K-W2-3 | Owner 12-month churn rate | **> 25%/yr** → marketplace supply erodes faster than replaced; PIVOT owner incentive model | End of Y1 cohort |
| K-W2-4 | Forwarding-only refusal rate among Dormant Holders | **> 40%** of "interested but no" owners cite architecture as the refusal reason → REOPEN W4 architecture decision | During exp-1 |
| K-W2-5 | Year-1 signed-and-live domains | **< 10** by month 12 → supply cannot sustain a beachhead; KILL marketplace or pivot to §2k fallback | Month 12 |
| K-W2-6 | Legal-review cost per signed domain | **> $300** amortized → lease template is too complex; SIMPLIFY or absorb via subsidy, re-evaluate at exp-1 close | 90-day gate |
| K-W2-7 | Owner payout realized vs. promised in Y1 | Realized < **50% of quoted range ($1,500–2,500/yr)** for first 10 owners → referral channel dies; renegotiate rev share or subsidize floor | Month 12 |
| K-W2-8 | Sale-escape clause invocations (Rev-1) — portfolio owners triggering the 180-day recall clause | **> 2 per 100 domain-years of live sale-escapable inventory** → clause is being used as a flip accelerator, not a safety valve; SUSPEND new sale-escape contracts and migrate at-risk renters to sale-free inventory | Rolling, from first sale-escape contract |

---

### 2k. Alternative Supply Strategies If the Marketplace Fails

Ranked fallbacks if §2h-exp-1 kills the cold-outreach thesis:

**(i) Platform-owned inventory (mail.com-adjacent).** Buy 5–10 premium surname `.coms` outright ($5k–$50k each, $50k–$250k capex), rent them ourselves, keep 100% of revenue. Pros: supply is 100% controlled; no rug-pull risk; listing policy is ours unilaterally. Cons: massive capex, inventory risk, no "marketplace" network effects, and we become mail.com-with-surnames. Viable if we can raise the capital and accept lower expected returns; recommended as the **primary fallback**.

**(ii) Narrower niche with pre-existing supply.** Pivot to first-name domains (`bill.com` is held by one person; there are only ~1,000 common first names) or category-plus-name (`jobs.johnson.com` as subdomains). Both dilute the "Claim your name" frame significantly and may not survive W1's positioning test. **Backup fallback only.**

**(iii) Registrar partnership as primary supply channel.** Negotiate with Namecheap / GoDaddy / Porkbun for a "monetize your parked domain" opt-in on a revenue share. Potentially unlocks thousands of domains, but requires BD capability and a deal we cannot yet close as an unknown startup. **Year-2 optionality, not a Year-1 plan.**

**(iv) Abandon the marketplace model entirely.** If (i) is uneconomic and (ii)/(iii) do not materialize, the business thesis dies at W2. This is the honest outcome under the Pessimistic scenario.

**Recommendation if exp-1 fails:** Go to (i). Raise a seed round scoped specifically to inventory acquisition, or execute a smaller-capex version (3–5 premium domains) as a proof of concept. Do not attempt (ii) or (iii) without additional validation.

---

## 3. Demand Strategist — Secondary Review

**1. Strongest version of the problem in this lane.**
W1 picked Surname-Match specifically because the desired domain is *unavailable at any price* — that's what makes us non-substitutable. But the supply plan in §2c explicitly filters *out* the most unavailable domains (actively-used personal holdings) and *in* the dormant ones. There is a real question whether a "dormant" surname domain — one that nobody is using — is perceived by the renter as *valuable identity* or as *a forgotten address nobody wanted*. The demand pitch was "claim the name the internet gave to someone else"; if the someone else isn't using it, does the claim lose resonance? Probably not (a renter named Johnson still wants `johnson.com`, regardless of whether the current owner checks their inbox), but it's worth flagging.

**2. Proposal that best addresses it.**
The W2 listing policy is demand-compatible **so long as the listed domains are the *correct* surnames** (top 500 US, covering ~40% of the population). The supply plan prioritizes top-100 surnames for the premium tier, which aligns with where renter demand will be concentrated. No change to W1 decisions required.

**One concern to flag:** if the realistic scenario yields only 12–18 signed domains, and those are drawn somewhat randomly from the Dormant Holder pool rather than strategically from top-50 surnames, the *coverage* of hot surnames may be thin. A Johnson renter on a site with no `johnson.com` live will experience the product as broken. **Recommendation: bias exp-1 outreach toward top-50 US surnames even at lower conversion, because a single top-10 surname onboarded is worth more than three surnames ranked 300–500.**

**3. Unresolved failure mode.**
If acquired supply is disproportionately rare-surname domains, demand per domain drops below the 25-renter liquidity floor, and domains churn off before they pay back their CAC. This is a *supply composition* risk, not a supply volume risk, and it is not currently gated by any kill criterion. **Proposed addition: a "supply composition floor" — at least 50% of signed domains must be top-200 US surnames, or the waitlist-backed demand per domain is insufficient.**

Supply segments W1 did not highlight that W2 should consider: **two-surname hyphenated domains** (`smith-jones.com`) are potentially easier to acquire (less demand, so less squatter interest) and map to a real demand subsegment (compound-surname buyers whose surname doesn't fit a single `.com`). Worth a Phase-2 note.

**Rev-1 — Hispanic-surname sub-segment elevated to priority.** The initial draft footnoted Hispanic-surname domains as a Phase-2 concern; on revision this is wrong. Garcia, Rodriguez, Martinez, Hernandez, Lopez, Gonzalez, Perez, and Sanchez are all top-25 US surnames by SSA/Census frequency, collectively covering ~6M US adults. These are *squarely inside* the Surname-Match ICP, not a foreign-language expansion question. The update: treat Hispanic-surname `.com` outreach as a **priority sub-segment** within the primary Dormant/Resigned pool, with Spanish-language pitch assets and a ≥ 25-contact sub-cohort inside exp-1 to measure whether Spanish-language outreach materially lifts conversion vs. English-language cold outreach on Hispanic-surname targets. Tracked as A-W2-10.

---

## 4. Marketplace Economics — Secondary Review

**1. Strongest version of the problem in this lane.**
Supply-side CAC of $300–$1,500 per signed domain must be amortized across renters *on that domain*. At $9/mo platform contribution per renter and ~25-renter steady state (~$225/mo/domain platform net), the **owner-side acquisition payback period is 1.3–6.7 months per domain, once renters are at steady state.** But reaching steady state takes 12+ months per domain, so the true payback on owner CAC is dominated by the ramp-up curve, not the steady state. Under Realistic scenario (§2i), with 8 renters/domain averaged over Y1, per-domain monthly contribution is $72 and a $600 owner CAC pays back in **~8 months of ramped operation**, i.e., probably month 18–20 since listing. That is tolerable if renters don't churn, and fatal if they do.

**2. Proposal that best addresses it.**
Do not treat owner CAC and renter CAC as independent. The waitlist-backed pitch (§2f demand-pull) couples them: renter CAC on a given surname directly funds the owner pitch for that surname. Under that model, W3 should treat blended CAC as **one number per domain-cohort**, not two. Proposed combined target: **total acquisition spend (owner + first-10-renters) ≤ 6 months of renter gross on that domain ≈ $900 per domain**. Exceeding this makes the domain LTV-negative before Year 2.

**On the 60/40 split:** Owner take of $150/mo at liquidity ($1,800/yr) is motivating but not compelling. Testimonials will drive referral — if they materialize. If exp-1 shows that owners churn specifically because "$150/mo isn't worth the hassle," the split has to move toward 50/50 or 55/45, which *eats most of the platform margin*. W3 must stress-test this; the 60/40 is provisional.

**On signing bonuses:** A $100–$250 bonus, paid from platform cash, front-loads owner CAC but may meaningfully move conversion. If the lift is 5% → 10%, it is massively economically positive. exp-1 should test both variants (A/B on bonus vs. no-bonus).

**3. Unresolved failure mode.**
If owner churn is 25%+/yr (K-W2-3), the math collapses — signed-domain CAC is re-spent every 4 years, and we never reach positive cumulative contribution. Economics require owner retention ≥ 85%/yr at steady state.

**On W1 pricing decisions:** Supply costs do not force a renter-side price change. The $15/mo standard and $25/mo premium remain defensible; the premium price particularly matters because top-100 surnames will have higher supply CAC (more demand = more competitive acquisition) and need the ARPU lift.

---

## 5. Legal & Operations — Secondary Review

**1. Strongest version of the problem in this lane.**
The lease contract is the product surface most exposed to legal attack. Three categories of risk:
- **Trademark/impersonation exposure for the platform.** When `john.smith@smith.com` is signed by a renter who happens to share a surname with a public figure or trademark holder, the platform can be named in a UDRP / trademark claim as the entity operating the domain's email. Even with owner indemnification, the platform is named first.
- **Succession & incapacitation.** An individual owner dying or becoming incapacitated during a 3-year lease, with no will or with a contested estate, strands the domain in probate. Renters cannot use the domain; the platform cannot collect owner-side revenue; the domain may lapse or transfer to heirs with no obligation to honor the lease. This has happened in domain name history (infamous case: Sex.com litigation) and the industry has no clean answer.
- **Tax reporting.** Owner payments via Stripe Connect are 1099-K reportable at $600/yr under current US rules. Every owner generating $1,500+/yr is a 1099 recipient. This is manageable but requires W-9 collection at onboarding, adds onboarding friction, and excludes owners who refuse to provide SSN/EIN.

**2. Proposal that best addresses it.**
- **Contract terms legally required:** written lease (email acceptable under E-SIGN), IRS W-9, Stripe Connect KYC/identity verification. Jurisdiction set to the state of platform incorporation. Indemnification **bilateral** (owner indemnifies platform for trademark/registration misrepresentations; platform indemnifies owner for renter-caused abuse not preventable by forwarding-only architecture).
- **Contract terms preferred but not required:** mutual arbitration clause, 1-year auto-renewing term with 90-day termination, right-of-first-refusal on domain sale (debatable — may reduce willing-to-list pool; leave out of MVP).
- **Succession mechanics:** require owner to name a successor / heir designee at onboarding; payouts continue to estate; platform has a 12-month "orphan" grace window during which it maintains DNS stability. Not bulletproof, but better than nothing.
- **Trademark screen:** per §2c, run a TM search on every surname before listing. Owner contract includes affirmative rep that owner is not aware of pending trademark claims against the domain.
- **Minor-name local parts:** renter onboarding must verify age ≥ 18. Addresses for children (e.g., parent signing up `emma@smith.com` for their 10-year-old) require affirmative COPPA-compliant consent flow — punt to W5.
- **Jurisdiction:** MVP is **US renters + US owners only.** A Johnson in Canada can buy, but a British holder of an American surname `.com` is out of scope for MVP — too much jurisdictional complexity for a two-person team.

**3. Unresolved failure mode.**
Jurisdictional edge cases in owner estates, especially where the domain is held in a registrar based in a different country than the owner. The playbook assumes the owner controls their registrar; in reality many owners don't remember which registrar they use, which compounds the succession problem. **Kill criterion exposure: if 20%+ of targeted owners cannot successfully transfer MX control during onboarding due to forgotten registrar credentials, acquisition labor inflates and CAC pushes past the K-W2-2 threshold.** Worth logging as an open risk (A-W2-5 in assumption register).

---

## 6. Synthesis & Locked Decisions

- **Owner ICP (LOCKED):** Dormant Individual Holders (primary) + Resigned Small Squatters (secondary). Top-500 US surnames on `.com`, age ≥ 5 years, clean reputation, no active trademark conflict.
- **Acquisition strategy (LOCKED):** Founder-led concierge cold outreach (letter + LinkedIn + WHOIS email) in months 0–6. Demand-pull / waitlist-backed outreach from month 6. No paid marketing on the supply side. Registrar partnerships parked for Year 2.
- **Listing policy (LOCKED):** `.com` only; top-500 US surnames; age ≥ 5 years; clean RBL; no celebrity/politically-charged surnames; reserved platform local-parts per §2c; owner-reserved local-parts (up to 20); no adult/firearms/cannabis/gambling.
- **Owner incentive model (LOCKED):** 60/40 platform/owner split (provisional, stress-test in W3). $50/mo revenue floor for first 12 months. $100–$250 signing bonus (exp-1 A/B test). 10% rolling reserve for first 180 days. Auto-renewing 1-year term with 90-day termination rights.
- **Supply kill criteria (LOCKED):** K-W2-1 through K-W2-7 as §2j; mirrored into `_kill_criteria.md`.
- **Go/no-go on supply viability (LOCKED):** **CONDITIONAL PROCEED.** Supply is the tightest risk. Commit to the 90-day exp-1 experiment (§2h-exp-1); treat its outcome as the actual go/no-go. Under expected-value planning the Realistic scenario misses the W1 K7 kill threshold — we are proceeding on the hope that exp-1 validates the Optimistic or high-Realistic band, not on any stronger basis. Fallback to §2k-(i) "platform owns inventory" is pre-declared if exp-1 fails.

---

## 7. Assumption Updates

### W1 assumptions tested by W2

- **A2** ("≥ 20% of top-100 US surname `.com` domains held by individuals / small businesses reachable via direct outreach") — **refined, status open.** W2 §2a estimates total *addressable* (Dormant + Resigned) at ~25% of top-500 surnames. Closer to the W1 hypothesis than invalidating it, but still awaits exp-0 WHOIS audit and exp-1 outcome for a measured answer.
- **A6** ("Domain owners accept 60/40 platform-favoring split if per-domain passive income ≥ $1,500/yr") — **refined, status open.** W2 §2e and §4 argue this is defensible at steady-state liquidity, but has not been tested with real owners. Exp-1 conversion rate is the first data point. If Resigned Squatters systematically demand 50/50, assumption is partially killed and W3 must re-examine.
- **A9** ("≥ 20 willing surname-domain owners can be signed within Year 1 at commercially reasonable CAC") — **refined toward risk, status open.** W2's expected-value scenario yields ~13 domains, below A9's 20. W2 flags this as the central risk; assumption is NOT YET killed because exp-1 could land at the Optimistic 22. But risk-adjusted planning should treat A9 as 50/50 at best.
- **A-pre-1** ("Forwarding-only is the safest architecture candidate") — **refined.** Still open, but W2 added a kill criterion (K-W2-4) that would re-open architecture if > 40% of refusal reasons cite forwarding-only.

### New W2 assumptions (added to register)

- **A-W2-1:** Cold outreach conversion to Dormant Individual Holders clears ≥ 5% with a founder-signed pitch and $100–$250 signing bonus.
- **A-W2-2:** Owner 12-month churn on signed domains stays below 15% at liquidity, consistent with landlord-style passive retention.
- **A-W2-3:** Demand-pull ("we have N renters on your waitlist") pitches convert 2–3× better than pure cold pitches after a waitlist exists.
- **A-W2-4:** Standardized simplified 1-page lease is acceptable to 80%+ of individual owners without lawyer review; legal-review cost stays below $300/domain amortized.
- **A-W2-5:** ≥ 80% of targeted owners can successfully transfer MX control during onboarding without founder-assisted registrar credential recovery.
- **A-W2-6:** Platform-owned inventory fallback (§2k-i) is capital-raisable at $50k–$250k if marketplace thesis fails.

---

## 8. Handoff to Workshop 3 (Marketplace Economics)

**W3 must verify:**
1. Whether the 60/40 split clears unit economics under the Realistic scenario — not the Optimistic. The honest Realistic yields ~$5k Year-1 platform net on ~$9k supply CAC. That is a loss year; W3 needs to model cumulative months-to-breakeven under compounding supply growth.
2. Whether a $50/mo revenue floor for first 12 months is an affordable subsidy at the expected signing volumes (15 domains × $600 subsidy avg = $9,000/year subsidy line).
3. Whether the supply-side CAC ($300–$1,500/domain) plus the demand-side CAC ($60/renter per W1) clear a blended LTV/CAC ≥ 2× under realistic liquidity (8–15 renters/domain in Y1, 20–25 at steady state).
4. Whether signing bonuses ($100–$250 per owner) pass their A/B test in exp-1 with sufficient lift (conversion lift ≥ 3 percentage points for a $200 bonus).
5. The W1 provisional 60/40 split may require re-examination if exp-1 surfaces systematic owner demand for 50/50.

**Supply cost numbers W3 should integrate:**
- Supply-side CAC per signed domain: **$300 (optimistic) / $600 (realistic) / $1,200 (pessimistic)**.
- Signing bonus: **$200 avg amortized per signed domain**.
- Revenue floor subsidy: **$400–$600/domain in Y1** (assumes floor hits 4–6 months before liquidity covers it).
- Reserve hold: **10% of owner payouts for 180 days** — working-capital drag, not P&L cost.
- Trademark screen cost: **~$50/domain** (automated with one-time manual review on ambiguous cases).
- Legal template amortization: one-time $3,000–$5,000 for drafting; ~$25/domain amortized over 200 domains.

**W1 pricing decisions that may need revisiting:**
- Premium-tier pricing ($25/mo for top-100 surnames) needs to clear the higher supply CAC that top-100 surnames will likely command. Revisit in W3 if CAC on top-100 domains skews 2× the blended rate.
- The $25 one-time onboarding fee is a renter-side trust filter and does not interact with supply.

**Key liquidity-gate number for W3:** the minimum renters-per-domain that yields contribution-positive unit economics after supply CAC amortization. Rough estimate from this workshop: **~8 renters per domain covers realistic supply CAC in ~14 months**. Anything below 8 steady-state is a non-starter — W3 to confirm with its full model.

---

*End of Workshop 2 memo.*
