# Demand & Positioning Workshop

**Date:** 2026-04-22
**Workshop:** 1 of 7
**Primary agent:** Demand & Positioning Strategist (offensive)
**Secondary reviewers:** Marketplace Economics Analyst, Domain Owner / Supply Advocate
**Status:** DECISIVE — commits to a primary ICP, positioning frame, and pricing hypothesis. All locked decisions are pending falsification by the evidence plan in §2g.

> **⚠ Rev-2 banner (2026-05-06).** The single-tier pricing hypothesis (§1, §2f: "$15/mo standard / $25/mo premium, ~25 renters/domain at liquidity") has been **reopened and superseded** on the pricing side by `docs/08_pricing_namespace_rev2.md`. Rev-2 splits the namespace into a **premium single-name tier ($25/mo, `john@smith.com`)** and a **standard compound tier ($9/mo, `john.paul@smith.com`)** with ~50 renters/domain at liquidity. Blended ARPU drops from $16.50 to ~$11; per-domain contribution rises. The LP experiment in §2g-2 should be extended to a three-variant split (A/B/C) per doc 08 §10.3 to resolve the premium-vs-standard cannibalization rate (K-Rev2-5). **A7 (70% annual retention) is superseded by tiered retention assumptions (A-Rev2-3) in doc 08 §4.** "Claim your name" frame is retained; secondary-reviewer brand notes in doc 08. Refer to doc 08 as source of truth for all pricing, ARPU, LTV, and CAC numbers going forward.

---

## 1. Executive Summary

**Problem statement (demand view):** A narrow but acute segment of consumers cannot buy the only email address that feels like *them* — `firstname@theirsurname.com` or the equivalent identity-grade local-part on a domain they will never be able to purchase. The domain is taken, parked, or held by a stranger. No amount of Gmail, Workspace, or aliasing solves this; the value is in the specific `local-part@domain` string itself. These buyers have nowhere to go, and a subset of them will pay a recurring fee for the right address if the product feels permanent, professional, and private.

**Primary ICP (locked):** **US English-speaking adults 28–55 whose legal surname matches a common-surname `.com` they do not own** (the "Surname-Match" segment). Proxy archetype: a Bill Johnson, a Sarah Patel, a Mike O'Brien — professionals or semi-professionals who have lived with `bill.johnson1974@gmail.com` long enough to resent it and who would pay to finally sign email as `bill@johnson.com`.

**Primary positioning frame (locked):** **"Claim your name."** A premium identity layer — not a privacy product, not a mailbox upgrade, not an alias tool. The product is the *address*. Everything else (forwarding, mailbox, client) is plumbing.

**Pricing hypothesis (locked):**
- Renter price: **$15/month** or **$144/year** (20% annual discount).
- One-time onboarding fee: **$25** (trust filter + covers setup labor).
- Premium-tier domains (top-100 US surnames on `.com`): **$25/month / $240/year**.
- Revenue split with domain owner: **60% platform / 40% owner** (challenges the placeholder 50/50; see §2f rationale).

**Risk level:** MEDIUM-HIGH.
**Confidence:** MEDIUM (60%) that a viable beachhead exists at this ICP and price; LOW-MEDIUM (40%) that the marketplace-liquidity math works without aggressive supply curation. The demand thesis is defensible; the liquidity thesis is the open question for Workshops 2–3.

---

## 2. Demand & Positioning Strategist Memo

### Three framework questions

**1. Strongest version of the problem in my lane.**
Every candidate buyer for a rented vanity email has a cheaper, well-understood substitute *except* for the buyer who wants a domain they cannot buy. For everyone else — creators, privacy seekers, professionals, status buyers — the dominant answer is "buy a domain for $12/yr and point Fastmail at it." A marketplace that rents addresses on domains the buyer *could have owned themselves* is a worse version of Namecheap plus Fastmail. The only defensible demand is where **domain ownership is not an available option** and the specific string has identity value. That collapses the addressable market dramatically but produces the only segment where our offer is not dominated by a $3/mo substitute.

**2. Proposal that best addresses it.**
Ship a beachhead product that targets the Surname-Match segment exclusively, frames itself as an identity claim (not a mailbox, not privacy), prices at $15/mo — clearly above hobby alias tools and clearly below Google Workspace + dedicated domain + loss-of-identity — and recruits supply on the ~500 most common US surname `.com` domains held by individuals rather than squatters. Architecture follows the offer: forwarding-only is acceptable *if* send-as renders cleanly, because recipients never see the forwarding. A "real mailbox" upsell can come later.

**3. Unresolved failure mode / unknown.**
The surname beachhead solves the "why us vs. substitutes" problem but creates a **supply-scarcity problem**: the exact domains with high renter demand (common-surname `.com`s) are the hardest to acquire because the owners either (a) use them personally, (b) are squatters holding for a large one-time sale, or (c) belong to a family trust that will not touch recurring-revenue contracts. If supply cannot clear, there is no marketplace. This is the first-class risk handed to Workshop 2.

---

### 2a. Candidate ICP segments — comparative analysis

All size estimates are **ballpark first-principles estimates**, not sourced figures. Reasoning shown.

#### Segment 1: Identity / Status ("I want an email that signals who I am")
- **Who:** Mixed — overlaps with every other segment. Pure "status" buyers without a narrower reason are rare.
- **Size:** Effectively zero as a standalone segment. Estimated < 50k US addressable; mostly re-categorizes into Surname, Creator, or Professional once you ask "status as what?"
- **Urgency:** LOW. Status without a concrete job is a luxury purchase that competes with a thousand other luxuries.
- **WTP:** $5–15/mo, but unreliable.
- **Substitute quality:** HIGH. A custom domain + Workspace already confers "status" and is cheaper.
- **Architecture sensitivity:** Low; status is about the string, not the plumbing.
- **Acquisition:** No clean channel.
- **Verdict:** **Weak.** Not a segment, a halo effect.

#### Segment 2: Professional Credibility ("look more established than Gmail")
- **Who:** Solo consultants, freelancers, small-business owners, job-seekers 30–55.
- **Size:** Large in principle — estimated 5–15M US freelancers/solopreneurs who care about presentation. But addressable-to-us is a tiny slice because the dominant solution is already trivial: buy `yourname-consulting.com` for $12/yr + Workspace $6/mo.
- **Urgency:** MEDIUM. Real pain, but well-served.
- **WTP:** $6–15/mo, capped by Workspace price.
- **Substitute quality:** VERY HIGH. Own-domain + Workspace is the near-perfect substitute and the buyer ends up with an asset they own.
- **Architecture sensitivity:** HIGH. This segment wants a real mailbox, send-as will feel amateurish, and forwarding-only will feel like a downgrade.
- **Acquisition:** LinkedIn, freelancer marketplaces — but CAC will compete with Workspace's own marketing.
- **Verdict:** **Weak.** We are structurally dominated by own-domain + Workspace unless the local-part is irreplaceable (which collapses back to Segment 4).

#### Segment 3: Privacy / Compartmentalization
- **Who:** Privacy-conscious users, often tech-literate.
- **Size:** Large interest, small paying population. Estimated 2–5M US addressable for paid privacy email; already heavily served.
- **Urgency:** MEDIUM in the abstract, LOW in willingness to pay specifically for vanity.
- **WTP:** $1–5/mo. Privacy buyers are price-sensitive and expect free or freemium.
- **Substitute quality:** VERY HIGH. SimpleLogin, AnonAddy, Fastmail masked, iCloud Hide My Email, DuckDuckGo Email Protection. All free or nearly free. All better at privacy than we can be (because the domain is *shared with other renters*, which is the opposite of privacy).
- **Architecture sensitivity:** Very high — forwarding/aliasing is the *product*.
- **Acquisition:** Privacy-focused newsletters, HN, Mastodon. Reachable but unprofitable.
- **Verdict:** **Weak.** We can't out-privacy SimpleLogin at $2/mo, and we make their privacy *worse* by putting them on a shared-domain.

#### Segment 4: Surname / Family Match
- **Who:** US adults 28–55 whose legal surname is a common `.com` they cannot buy. Professionals, parents naming family-member addresses, diasporas with surname-heavy identity.
- **Size:** Estimated addressable. The top 500 US surnames cover roughly 40% of the population (~130M people). Not all will care; not all will pay. Narrowing to adults 28–55 who (a) use email heavily, (b) resent their current `firstname.lastname1983@gmail.com`, (c) would pay $15/mo — guess 1–3% of that 130M, i.e., **1.3M–4M US TAM**. SAM (realistically reachable in year 1) is a small fraction of that, maybe **50k–200k**.
- **Urgency:** MEDIUM-HIGH. Emotional, identity-driven. Not burning, but long-simmering.
- **WTP:** $10–25/mo is defensible. The address is not available at any price elsewhere, so the only anchor is "what is identity worth to you per month."
- **Substitute quality:** LOW. Own-domain doesn't work because the surname `.com` is taken. `bill-johnson.com` or `billjohnson.net` feels worse than Gmail, not better. This is the one segment where substitutes genuinely do not compete.
- **Architecture sensitivity:** MEDIUM. The recipient never sees the architecture. Forwarding-only is acceptable if send-as is clean. A real mailbox is a premium upsell, not a gate.
- **Acquisition:** Targetable. Surname-match Facebook/IG lookalikes, ancestry-adjacent communities, LinkedIn retargeting on common-surname cohorts, SEO for "`[surname]` email address." Clean channels exist.
- **Verdict:** **STRONG. This is the beachhead.**

#### Segment 5: Creator / Personal Branding
- **Who:** Newsletter writers, streamers, podcasters, small-audience creators.
- **Size:** US addressable ~1–3M active creators earning anything from side income upward. But creators who care about email branding overwhelmingly already own their brand domain.
- **Urgency:** MEDIUM.
- **WTP:** $5–15/mo, capped by Workspace.
- **Substitute quality:** VERY HIGH. Creators buy their brand domain as item one. They control the string on their own domain.
- **Architecture sensitivity:** HIGH. They need to send newsletters, which means SMTP, which means domain reputation, which is the worst case for us.
- **Acquisition:** Creator-economy channels, doable.
- **Verdict:** **Weak.** Structurally dominated, and worst-case on abuse.

#### Segment 6: Novelty / Fandom
- **Who:** Fans, joke-gift buyers, teenagers.
- **Size:** Noisy long tail.
- **Urgency:** LOW — impulse, not durable.
- **WTP:** $2–5/mo, one-time feel.
- **Substitute quality:** HIGH — mail.com, free alias services.
- **Architecture sensitivity:** Low.
- **Acquisition:** Viral/social, cheap but untargeted.
- **Verdict:** **Weak.** Low LTV, high churn, attracts abuse (fan@celebrity.com = impersonation risk).

**Ranking:** Surname-Match (strong) >> Professional (medium, dominated by substitutes) > Privacy (medium, dominated by better substitutes) > Creator (weak) > Novelty (weak) > Status (not a segment).

---

### 2b. Substitute analysis

| Substitute | Monthly cost | Who it serves well | Where it fails | Why we win (for Surname-Match) |
|---|---|---|---|---|
| Own-domain + Google Workspace | ~$6/mo + $12/yr domain | Anyone who can get a suitable domain name | Cannot provide `surname.com` if taken | **The desired domain is not buyable at any price.** We are the only supplier. |
| Own-domain + Fastmail / Proton | ~$3–5/mo + $12/yr | Same | Same | Same as above. |
| SimpleLogin / AnonAddy (aliasing) | Free–$3/mo | Privacy-seeking alias users | Domains are generic/ugly; shared pools; not identity-grade | We offer a specific identity string; they offer disposable strings. Different product. |
| Cloudflare Email Routing | Free (on owned domain) | Owners of their own domain | Not applicable if you don't own the domain | We supply the domain; they don't. |
| "Just use my Gmail" | Free | Most people most of the time | Does not solve identity pain; `firstname.lastname1983@gmail.com` is the exact complaint | Our buyer has already decided Gmail is insufficient; that's the trigger for seeking us. |
| Web3 / ENS handles | $5–50/yr | Crypto-native identity | Not interoperable with normal email; not a real mailbox; signals crypto rather than professionalism | Works with any SMTP recipient; no wallet required; reads as normal professional email. |
| Mail.com premium | $1–5/mo | Novelty seekers | Generic domains, reputation baggage, no surname match | We focus on a specific, meaningful string; they offer a catalog of leftover generics. |

**Conclusion:** Against every segment *except* Surname-Match, at least one substitute is cheaper, more permanent, and better than our product. Against Surname-Match, **no substitute competes on the one axis that matters** (the specific string). That is the only defensible position.

---

### 2c. Architecture–positioning matrix

| ICP | Forwarding-only | Full SMTP (real mailbox) | Hybrid (inbound full, outbound rate-limited) |
|---|---|---|---|
| Surname-Match | **Neutral-to-positive** if framed as "works with the Gmail you already use." Recipient never sees it. | Positive but not required. Upsell path. | Overkill for MVP. |
| Professional | **Negative.** Feels second-class; send-as in Gmail looks amateurish to informed recipients. | Required to compete with Workspace. | Acceptable. |
| Privacy | **Positive.** Forwarding is the feature. | Negative — more data surface to protect. | Negative. |
| Creator | **Negative.** Can't send newsletters. | Required — but catastrophic abuse risk. | Mandatory; high-ops. |
| Novelty | Neutral. | Overbuilt. | Overbuilt. |

**Winning combination:** **Surname-Match × Forwarding-only × "Claim your name" framing.**

The key insight: for the Surname-Match buyer, the *value is on the envelope*, not in the mailbox. Recipients read `From: Bill Johnson <bill@johnson.com>` — the architecture beneath is invisible. Forwarding-only is therefore a product-market fit, not a compromise, **for this ICP**. (Same architecture would be a liability for Professional or Creator — which is exactly why we don't pick those ICPs.)

---

### 2d. Primary ICP decision

**Locked: Surname-Match — US adults 28–55 whose legal surname matches a common-surname `.com` they do not and cannot own.**

**Why this segment first (not the others):**
1. **Only segment where substitutes don't dominate us.** Every other segment can be served by a $3–6/mo combo the buyer already understands.
2. **Emotional durability.** Identity tied to one's name is not an impulse; churn should be lower than novelty or status segments.
3. **Targetable acquisition.** Surnames are a demographic facet you can literally buy targeting on.
4. **Price elasticity favorable.** When the desired object is unavailable elsewhere, the reference price is "how much does identity cost me," not "what does Workspace cost." This is the only ICP where we can credibly price above Workspace.
5. **Compatible with the safest architecture.** Forwarding-only MVP works for this ICP specifically, which lowers execution risk.
6. **The other ICPs are *downstream* markets we can expand into later** if (and only if) we win the beachhead first.

**What "winning the beachhead" looks like (12-month targets, for go/no-go at end of year one):**
- **500 paying renters** across **20+ live surname domains.**
- **Average 25 renters per active domain** (liquidity proof point).
- **$6,000 MRR / ~$72k ARR** (at $15 blended ARPU).
- **Landing-page conversion ≥ 3%** on cold surname-targeted traffic (see kill criteria).
- **Cohort month-12 retention ≥ 70%** (identity purchases should be sticky).
- **Blended CAC ≤ $60** (4-month payback at $15 × 60% platform take = $9/mo contribution).

**Architecture that best serves them:** **Forwarding-only MVP** (per `04_deliverability_workshop.md`, pending re-confirmation after Workshops 2–4). Send-as via the user's existing Gmail / Outlook / iCloud. Real-mailbox upgrade available as a $10/mo add-on in a later phase.

**Positioning story that wins:** "Claim your name." Permanent. Personal. Professional. The address the internet forgot to give you.

---

### 2e. Value proposition & messaging

**One-sentence positioning statement:**
> For people whose surname is already a `.com`, *myownemail* is the only way to finally use `firstname@surname.com` as your everyday email — rented from the owner, forwarded to the inbox you already use.

**Landing page headline + subhead:**

> # Your name. Your email. Finally.
> Use `bill@johnson.com` — or the exact address that matches *your* name — even if the domain isn't for sale. We rent it from the owner, forward it to your Gmail, and you sign email as yourself.

**Top 3 proof points:**
1. **Works with your existing inbox.** Keep Gmail. Send-as is configured in minutes; recipients see only your vanity address.
2. **Permanent as long as you want it.** Long-term lease terms with escrow protection against the domain owner walking away. (Detail resolved in Continuity Workshop.)
3. **Not a mass-pool alias.** You get the specific address. No one else gets it while you hold it. No generic `@mail.com` fallback.

**Top 3 objections and responses:**

| Objection | Response |
|---|---|
| "Why don't I just buy my own domain?" | Because `johnson.com` (or your surname) is already taken and has been for 25 years. For $15/mo you get the address you actually want instead of `bill-johnson-email.net`. |
| "What happens if the domain owner disappears?" | Long-term lease with escrowed payments and a contractual notice period; if the domain is ever withdrawn, you get a free migration window and a pro-rated refund. *(Exact mechanics: Continuity Workshop.)* |
| "Can the domain owner read my email?" | No. The owner points MX records at our platform; they have no mailbox access, no forwarding control, and no admin read. The architecture guarantees it. |

---

### 2f. Pricing hypotheses

**Proposed structure for the beachhead:**

| Item | Standard surname | Premium surname (top-100 US) |
|---|---|---|
| Monthly | **$15/mo** | **$25/mo** |
| Annual | **$144/yr** (20% off) | **$240/yr** (20% off) |
| One-time onboarding fee | **$25** | **$25** |
| Trial | 14-day free trial, credit-card required |  |
| Real-mailbox upgrade (future) | +$10/mo | +$10/mo |

**Revenue split with domain owner — challenging the placeholder 50/50:**

Proposed: **60% platform / 40% owner.**

Rationale:
- **Platform bears:** CAC (both sides), payment processing, Stripe Connect fees (~3%), hosting, forwarding infra, support, trust & safety labor, legal, abuse reserves, chargebacks, Workshop-2-level supply acquisition effort, Workshop-5-level continuity guarantees.
- **Owner bears:** Domain registration ($12/yr), reputation risk (mitigated by forwarding-only), MX-record config (one-time).
- The asymmetry is large. A 50/50 split under-compensates the platform's operating load and over-compensates a largely passive asset. 60/40 still leaves a surname domain with 25 renters generating **~$1,800/year passive** to the owner, which is materially attractive vs. parking or unused.
- A 70/30 split is economically cleaner for the platform but risks supply-side refusal. 60/40 is the defensible compromise; Workshop 3 should stress-test it.

**Pricing rationale grounded in substitutes:**
- Google Workspace sits at ~$6/mo. Our price *must* exceed it — we are not competing on mailbox features, we are charging an identity premium. Pricing at or below Workspace would cue the buyer to just buy Workspace.
- Aliasing tools at $0–3/mo anchor the low end; we position firmly above them to avoid being compared on "email feature" axes.
- $15/mo is **2.5× Workspace**, which maps to "premium but not luxury." Anchoring research (assumption — see §6) suggests identity purchases tolerate 2–5× commodity pricing.
- $25 onboarding fee is a **trust filter**, not a revenue line: it discards tire-kickers and lowers downstream support cost per active user.

---

### 2g. Evidence plan — how we'll validate

| Experiment | Cost | Duration | Validates / Kills |
|---|---|---|---|
| **1. Customer interviews.** Target 20 people with top-50-US surnames found via LinkedIn outreach. 30-min calls. Ask: do they resent their current email, have they tried to buy their surname `.com`, would they pay $15/mo for `firstname@surname.com`, what would make them not pay. | ~$600 (incentives + tool) | 3 weeks | **Validate** if ≥8/20 express unprompted interest and ≥5/20 commit to a pre-order. **Kill** if ≤2/20 would pay. |
| **2. Landing-page test.** Single page at `myownemail.com` (or proxy). Headline + email capture + optional $25 refundable deposit. Drive traffic via Meta ads targeted to lookalikes of common US surname holders 28–55, US. Budget $1,500 ad spend. | ~$1,800 | 2–3 weeks | **Validate** if cold-traffic email-capture ≥ 3% AND deposit conversion ≥ 0.5%. **Kill** if capture < 1% or deposit < 0.1%. |
| **3. Concierge MVP / pre-order.** Manually acquire 2–3 common-surname domains (rent from a consenting owner, or buy outright for the test). Sell 5–10 real addresses to interview/LP leads. Configure forwarding + send-as by hand. | ~$500–$2,000 | 4–6 weeks | **Validate** if ≥5 paying concierge users for ≥2 months with < 1 support ticket per user per month. **Kill** if users churn within 30 days or setup takes > 2 hours per user. |
| **4. Secondary research.** Scrape surname `.com` WHOIS data (where legal) to estimate what fraction of top-500 US surname domains are held by individuals vs. squatters vs. companies vs. trusts. Run a 200-response paid survey (Prolific, US adults, surname filter). | ~$800 | 1 week | **Validate** supply feasibility (hand-off to Workshop 2) and WTP distribution. No kill trigger — informational. |

**Total evidence-plan budget: ~$5,700. Total duration: ~8 weeks serial; ~4–5 weeks parallel.**

---

### 2h. Kill criteria (numeric)

The project stops, pivots, or returns to the drawing board if any of the following fire:

| # | Criterion | Threshold |
|---|---|---|
| K1 | Landing-page email capture on surname-targeted cold traffic | **< 1.5%** → kill; 1.5–3% → pivot messaging; ≥3% → proceed |
| K2 | $25 deposit / pre-order conversion from captured leads | **< 5%** of email-captured leads → kill |
| K3 | Interview expressed WTP at $15/mo | **< 25% of 20 interviewees** willing → kill |
| K4 | Survey substitute preference (own-domain + Workspace over us) when desired surname is hypothetically available | **> 70%** → kill |
| K5 | Concierge 60-day retention | **< 60%** → kill |
| K6 | Blended WTP from interviews | **Median < $8/mo** → kill |
| K7 | Year-1 beachhead check (post-launch, if we launch) | **< 150 paying renters or < $1,500 MRR** by month 12 → stop or pivot ICP |

These are duplicated into `docs/_kill_criteria.md`.

---

## 3. Marketplace Economics Analyst — Secondary Review

**1. Strongest version of the problem in this lane.** At $15/mo renter price and 60/40 platform split, the platform grosses $9/mo per renter. Subtract ~$0.75 Stripe Connect, ~$0.50 forwarding infra, ~$1–2 support blended, ~$1 abuse/chargeback reserve. **Net contribution ≈ $4.75–6/mo per renter.** At a $60 target CAC, payback is ~10–13 months; LTV at 24-month expected life is $114–144; LTV/CAC ≈ 1.9–2.4×. Tight but not broken. The danger: CAC on a 1–3% landing-page conversion funnel against Meta-ad CPMs to common-surname lookalikes realistically runs $80–150, not $60. **That would kill LTV/CAC below 1.** Organic / referral / surname-SEO becomes the only viable scaling channel.

**2. Proposal.** Price-up the standard tier to **$19/mo** or hold $15 but require annual prepay to the default path. Drive CAC down by making surname-SEO (pages like "get `bill@johnson.com`") the primary channel rather than paid social. Add a referral kickback to the domain owner: owners who recruit their own surname-matches earn 50% of that renter's revenue for year one, converting owners into a zero-CAC acquisition channel.

**3. Unresolved failure mode.** Marketplace liquidity per domain. At 25 renters per active surname domain target, we need ~20 domains to hit 500 renters. That implies tight concentration: each active domain must find 25 buyers who want *that specific surname*. For top-25 US surnames this is plausible; below the top-100 it falls off fast. **Liquidity cliff risk** is the open economics question. Workshop 3 must model renter density per surname rank and identify the cutoff below which a domain isn't worth onboarding.

**Red flags:**
- Paid CAC on a narrow demographic targeting axis is likely higher than $60.
- $15/mo ARPU does not tolerate more than ~1 support contact per user per quarter at current US labor costs.
- 60/40 split may be insufficient to attract owners of *high-demand* surnames who understand their leverage; price discrimination (premium tier) partially addresses this but invites negotiation.

**Verdict on §2f pricing:** Acceptable as hypothesis. Needs Workshop 3 sensitivity analysis on CAC and churn before lock.

---

## 4. Domain Owner / Supply Advocate — Secondary Review

**1. Strongest version of the problem in this lane.** The ICP choice *determines* which supply we need, and the Surname-Match ICP creates the **hardest supply problem possible**: we need individual humans (not companies, not squatters) who own their own surname `.com` and are willing to enter a long-term revenue-share on their identity asset. These owners are rare, emotionally attached to the domain, and skeptical of strangers putting email addresses on "their" name. Squatter-held surname domains are easier to reach but bring reputational and legal baggage (trademark, typosquatting perception, parked-domain SEO penalties).

**2. Proposal.** Two supply tiers:
- **Tier A — individual owners** (the Johnsons of the world who own `johnson.com` personally). Pitch: "passive income from your family name, $1,800+/yr per 25 renters, you keep full control, end anytime with 90 days' notice." Small number of these exist but they are the quality supply.
- **Tier B — small-business owners** (a `johnson-plumbing.com` type who owns the cleaner `johnson.com` but doesn't use it for business). More pragmatic; easier to close.
- **Explicitly refuse** squatter-held domains at launch. Squatters want lump-sum sales and will not commit to long-term leases; attempting to rent from them creates rug-pull exposure that breaks the core promise to renters.

**3. Unresolved failure mode.** The "Claim your name" framing creates a **supply-side dissonance**: the same framing that attracts renters ("my name, my identity") may repel owners ("strangers wearing my name online"). An owner named Johnson may feel queasy about 25 unrelated Johnsons sending professional email on their domain. This is a first-class Workshop-2 problem.

**Red flags:**
- The intersection {owns surname `.com`} × {willing to commercialize it} × {understands forwarding-only} is narrow. Workshop 2 must estimate actual supply population, not TAM.
- Domain owners who *do* use their domain personally (owner@johnson.com as their own email) cannot list without first migrating themselves off. That's a real switching cost and an objection to surface early.
- Privacy framing from renter side may be required to close owner objections ("owners can never read your mail"), which slightly dilutes the identity-first positioning. Messaging must hold both truths.

**Verdict:** The chosen ICP produces the right *demand* but the *hardest* supply. Not a veto; a warning. Workshop 2 owns the resolution.

---

## 5. Synthesis & Locked Decisions

| Decision | Locked value | Confirmation required from |
|---|---|---|
| **Primary ICP** | Surname-Match (US adults 28–55 whose legal surname is an unbuyable common `.com`) | Evidence plan §2g |
| **Primary positioning frame** | "Claim your name." — premium identity layer | Landing-page test K1 |
| **Pricing hypothesis** | $15/mo standard / $25/mo premium / $144 annual / $25 onboarding / 60-40 platform-favoring split | Workshop 3 unit economics |
| **Architecture preference** | Forwarding-only MVP with Gmail/Outlook/iCloud send-as | **Provisional — pending Workshops 3–4 re-confirmation** |
| **Evidence plan status** | Ready to execute (~$5.7k, ~4–5 weeks parallel) | Founder approval to spend |
| **Revenue-share default** | 60/40 platform (challenges original 50/50) | Workshop 3 |

**What this memo refuses to hedge on:** one ICP, one frame, one architecture preference, one pricing level. All four can be falsified by evidence; none are hedged as "could be any of these."

---

## 6. Assumptions & Open Questions

### Key assumptions baked into this memo (all carry into `_assumption_register.md`)

1. **A1 — Top-500 US surnames cover a large enough population (~40%) that even narrow conversion (1–3%) produces a viable TAM of 1M+.** First-principles; unvalidated against actual surname frequency tables.
2. **A2 — A meaningful fraction (target: ≥ 20%) of top-100 surname `.com` domains is held by individuals or small businesses reachable via direct outreach, not by squatters or major corporations.** Testable via WHOIS scraping (experiment §2g-4).
3. **A3 — Surname-Match buyers tolerate forwarding-only plus Gmail send-as because recipients never see it.** Testable in concierge MVP.
4. **A4 — WTP for an identity-grade email is anchored to "what is my identity worth per month" rather than "what does Workspace cost," supporting a $15/mo price point.** Testable in interviews and LP deposit conversion.
5. **A5 — CAC on surname-targeted lookalike ads is achievable at ≤ $60 blended once surname-SEO contributes.** Flagged by Economics reviewer as aggressive; open question.
6. **A6 — Domain owners will accept a 60/40 split (platform favor) as long as passive income clears ~$1,500+/yr per active domain.** Testable in Workshop 2 owner outreach.
7. **A7 — The surname-match segment's churn behaves like an identity purchase (high retention, ≥70% at 12 months) rather than like a utility purchase.** Unvalidated; concierge 60-day retention is an early proxy.
8. **A8 — "Claim your name" framing does not generate unmanageable trademark/impersonation legal exposure.** Hand-off to Workshop 5.
9. **A9 — Supply of 20+ willing surname-domain owners is achievable within year 1 at commercially reasonable acquisition cost.** Hand-off to Workshop 2.
10. **A10 — Renters will accept a lease structure (not outright ownership) with disclosed rug-pull protections, and this will not kill conversion below K2 threshold.** Joint with Workshop 5.

### Open questions for subsequent workshops

1. **Supply feasibility:** How many top-500 surname `.com`s are actually reachable and willing? (**Workshop 2**)
2. **Liquidity cliff:** Below what surname-frequency rank does renter demand thin out so much that a listed domain is not worth operating? (**Workshop 3**)
3. **CAC reality check:** Is blended CAC achievable below the $60 target, or does the funnel only clear with organic/SEO scaling? (**Workshop 3**)
4. **Architecture confirmation:** Does forwarding-only still win once supply-side owner objections and economics are priced in, or does a partial-SMTP hybrid raise ARPU enough to change the calculus? (**Workshops 3–4**)
5. **Legal exposure of "Claim your name":** Does this framing attract trademark or impersonation actions that would force a repositioning? (**Workshop 5**)

---

## 7. Handoff to Workshop 2 (Supply Acquisition)

**What Workshop 2 must verify given this ICP:**

1. **Confirm supply population.** For the top 500 US surname `.com` domains, estimate the distribution across: (a) individual owners actively using them, (b) individual owners not using them, (c) small-business owners whose primary business isn't email, (d) squatters / parking portfolios, (e) corporations holding defensively. Only buckets (b) and (c) are realistically convertible; size that pool.
2. **Test owner pitch.** Run 10–20 direct owner outreach conversations. Offer: $1,500–3,000/yr passive at 25 renters, 60/40 split, owner retains domain ownership and has a 90-day kill switch. Measure acceptance rate, objections, and counter-offers on the split.
3. **Resolve the framing conflict.** "Claim your name" works for renters. Owners will hear "strangers using your family name." Find the honest owner-side framing that doesn't break the renter-side one (likely: "monetize your domain, keep full control, never surrender the asset").
4. **Define listing policy.** Which surnames are in/out at launch? (Assumption: exclude surnames that are also strong trademarks — e.g., `ford.com`, `ferrari.com` style — and exclude surnames with high impersonation risk for public figures.)
5. **Estimate owner-side CAC.** Cold outreach to individual domain owners is labor-intensive. What does it cost to close one quality owner?

**Domain profile Workshop 2 should prioritize:**

- **Core target:** Top-100 most common US surnames on `.com`, held by individuals or small businesses not using the domain as a primary public brand.
- **Secondary target:** Common surname `.com` variants with strong regional resonance (e.g., Patel, O'Brien, Nguyen, Garcia) held by similar profiles.
- **Explicitly deprioritize:** Squatter portfolios, trademarked names, public-figure names, adult/regulated categories, and single-letter or three-letter `.com`s (different market, different buyers, different risk).
- **Success criterion for Workshop 2:** A validated path to ≥ 20 signed owners within 6 months of go-live at an owner-CAC that keeps total platform-side CAC (both sides, amortized) within the unit-economics envelope Workshop 3 defines.

---

*End of Workshop 1 memo.*
