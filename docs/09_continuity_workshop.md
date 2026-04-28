# Continuity Workshop: Rug-Pull Protection, Escrow, Renter Migration & Regulatory Posture

**Date:** 2026-04-27 (v0 initial draft); **Rev-1 amendments 2026-04-27** (same day, §9); **Rev-1 rubber-duck findings 2026-04-27** (same day, §10)
**Facilitator Input:** Legal & Operations Expert (lead), Trust & Safety Architect, Marketplace Economics Analyst, Domain Owner / Supply Advocate
**Status:** **Rev-1 — controlling layer; Rev-2 rework PENDING.** Rev-1 (§9) supersedes specific v0 design decisions in response to rubber-duck findings B1–B5 and M1–M8 (§8). A second rubber-duck pass on Rev-1 itself returned **MAJOR-REWORK** (5 new blockers + 12 mediums recorded in §10), most importantly B5-Rev1 (an inter-workshop conflict with W4 forwarding-only). Where v0 and Rev-1 conflict, **Rev-1 controls** until Rev-2 supersedes it. Sections of v0 superseded by Rev-1 are tagged inline with `→ SUPERSEDED BY §9.X`. v0 content is preserved for traceability. Reserve numerics from v0 §3.1 remain PLACEHOLDER pending W7 reconciliation.

> ### Scope inherited from upstream workshops
>
> - **W1 (Demand) closed**: Surname-Match `.com` ICP, "Claim your name" frame.
> - **W2 (Supply) closed**: Owner contract anatomy partially specified (W2 §2j: 90-day owner exit, 10% rolling reserve, succession clause, "owner keeps registrar account control"). Sale-escape clause for the Long-Tail Portfolio segment is **explicitly deferred to W5 for legal sign-off** (W2 §2c, §2k(iv)).
> - **W3 (Economics) closed**: Migration reserve as a balance-sheet line item; escrow opportunity cost is not yet modeled.
> - **W4 (Deliverability) Rev-2.2 conditionally locked**: hands three launch blockers to W5 — (a) indemnification posture for blacklist + impersonation harms, (b) owner-pull-during-active-incident protocol, (c) owner-vs-renter abuse arbitration path. Plus the Rev-2.2 sending-bridge dependency has minor migration implications.
>
> ### What this workshop must establish
>
> 1. A complete **rug-pull taxonomy** (every way a domain can disappear from the marketplace) with specified mitigations.
> 2. The **owner lease contract** in enforceable form (or in close-to-final form pending external counsel).
> 3. The **renter-side protection guarantee**: notice, grace, migration, refund — what we promise renters at signup.
> 4. **Escrow and reserve mechanics**: amounts, holding periods, what each reserve covers, who controls it.
> 5. **Regulatory posture**: CAN-SPAM, GDPR (and CCPA/CPRA/state privacy), trademark/impersonation, marketplace tax (sales tax / VAT), COPPA, money-transmitter analysis for the 60/40 split.
> 6. **Indemnification structure** for the W4 launch-blocker.
> 7. **Sale-escape clause** legal review (W2 hand-off).
> 8. Hand-offs to W6 (Red Team) and W7 (Go/No-Go).

---

## Executive Summary

### Problem Statement

The marketplace creates a **structural three-way fragility**:

1. **The platform** depends on **owner cooperation** (the owner literally controls the domain at the registrar; without their continued cooperation, every renter on the domain loses their identity).
2. **Renters** depend on **the platform** (they have no direct relationship with the registrar; their email identity is collateral to a contract they're not party to).
3. **Owners** depend on **the platform** (their payouts and abuse protection flow through us; if we go down, their domain still works but their revenue stops).

Any single one of these relationships breaking — by accident, by adversarial action, by death, by sale, by regulatory pressure, by registrar policy change — collapses the marketplace for the affected domain. **W5 is the workshop where we decide what we promise, what we guarantee, and what we explicitly disclaim.**

The forwarding-only architecture from W4 reduces *deliverability* fragility (no platform outbound SMTP, so renter abuse can't blacklist the entire domain via the platform's IPs), but it does *not* reduce *legal-control* fragility. The owner still holds the keys.

### Locked Design Decisions (this workshop)

1. **Registrar-control model: "Owner-controlled, platform-monitored."** `→ SUPERSEDED BY §9.1 (B1).` The platform never holds the registrar account. The owner retains full domain control at their existing registrar. Platform integrates via DNS records (SPF, DKIM, DMARC, MX) which the owner authorizes us to manage via NS delegation **on a subdomain** (`mail.<domain>`) where structurally possible, or via direct record management with TOTP-protected change auditing. Inherited and reaffirmed from W2 §2j.
2. **Two-tier domain product.** `→ Premium "sale-free" relabeled "Bonded Premium" by §9.1 (B1) and §9.3 (B3).` **Premium tier** (sale-free, full-term commitment, signed lease, no sale-escape) and **Standard / Sale-Escapable tier** (sale-escape clause permitted, must be disclosed at signup, capped at ≤ 30% of live inventory). Renter pricing reflects the risk asymmetry (Premium-tier renter slots can carry a small premium; documented under K-W5-1 below).
3. **Renter Protection Guarantee (RPG)** — locked, customer-facing: `→ Migration-credit framing revised by §9.9 (minor cleanup).`
   - **Minimum 90-day notice** before any planned domain withdrawal (sale, lease termination, owner exit). For Premium-tier renters: 180 days.
   - **Migration assistance** — concierge-grade handoff to an alternate surname domain (where available) or to a personal-domain setup ($15 ICANN registration credit + free 3-month forwarding-only setup).
   - **Pro-rated refund** for unused term, plus a **migration credit** (1 month of equivalent service) if migration is involuntary.
   - **No surprise withdrawals** outside RBL-pause emergencies — emergency carve-out spelled out separately.
4. **Reserve & escrow architecture** (locked at the structural level; **all numerics PLACEHOLDER pending W7 — see §9.2 (B2) and §9.6 (M2)**):
   - **10% rolling reserve** on all owner payouts for first 180 days of each domain's listing (per W2 §2j item 7).
   - **Migration reserve fund** at platform level: $X/renter-month accrued into a segregated account, sized per K-W5-2.
   - **Stripe Connect Custom** flow holds funds 7 days minimum before payout to owner; chargeback window extends this to 90 days for first-time owners.
   - **Indemnification reserve** (W4 hand-off): platform-side reserve to absorb impersonation/blacklist harms below stated caps; above caps, push-to-renter via ToS + insurance backstop.
5. **Regulatory posture (locked positioning, external counsel sign-off pending):** `→ SUPERSEDED BY §9.10 (M8): MVP is US-only; EU/UK regimes deferred to post-MVP.`
   - US Delaware C-corp; California operating presence assumed for tax-nexus modeling.
   - **CAN-SPAM:** platform is a "sender" or "service provider" for inbound forwarding only; renters are senders for outbound (their Gmail/bridge). ToS push to renters; no commercial-bulk-mail authorization on rented addresses (enforced by §2.1 below).
   - **GDPR / UK GDPR / CCPA / CPRA / state privacy:** platform is data controller for renter PII (name, payment, ID-verification result), data processor for inbound forwarded mail content (transit only, no storage beyond logs). DPA template required per renter; SCCs for non-EU platform processing.
   - **Trademark / impersonation:** mandatory ID-verification at signup (W4 §2.5.2) provides a registrant-of-record identity; same-domain impersonation (W4 §2.5.3) handled by canonicalization spec + complaint takedown (UDRP-adjacent process internally; no claim of UDRP equivalence).
   - **Money transmitter:** the 60/40 split processed via Stripe Connect Custom is structured to keep us **outside money-transmitter classification** in all 50 states (Stripe is the regulated party, we are a marketplace facilitator). External counsel must confirm.
   - **Sales tax / marketplace tax:** SaaS-tax states (currently ~20+) require collection on rentals at the renter side; platform collects and remits. Owner side is service-revenue (1099-K threshold tracking).
6. **Sale-escape clause structure (W2 hand-off, locked at design level pending counsel):** `→ SUPERSEDED BY §9.3 (B3): adds anti-avoidance, 12-mo seasoning, greatest-of exit fee, sale-proceeds escrow.` owner option to pull on bona-fide third-party offer ≥ floor price, 180-day notice, owner pays exit fee into migration reserve, capped at ≤ 30% of live inventory (per W2 §2k(iv)). External counsel must confirm enforceability and absence of UCC Article 2 / consumer-product implications.

### MVP Launch Blockers (must clear before code build commences)

1. **External counsel review of the Master Owner Lease Agreement** (incl. sale-escape clause).
2. **External counsel review of the Renter ToS** (incl. RPG, indemnification posture, money-transmitter disclaimer).
3. **External counsel review of the regulatory posture memo** (CAN-SPAM, GDPR, state privacy, money-transmitter, marketplace tax).
4. **Indemnification posture lock** (W4 launch-blocker resolved here): platform-side caps + insurance backstop + ToS push above caps. Insurance broker quote required.
5. **Owner-pull-during-active-incident protocol** (W4 launch-blocker): specified in §3.4 below; needs sign-off from external counsel before live use.
6. **Owner-vs-renter abuse arbitration** (W4 launch-blocker): adjudication path specified in §3.5 below; requires adjudicator-of-record decision (in-house Tier-3 vs. third-party arbitration vendor) before launch.

### Hard Gates (locked numeric thresholds before scaling beyond concierge MVP)

1. **K-W5-1**: Sale-escape invocation rate on Standard-tier inventory (lifts and locks K-W2-8). > 2/100 sale-escapable domain-years → SUSPEND new sale-escape contracts.
2. **K-W5-2**: Migration cost per displaced renter (incl. concierge labor + refund + credit). Sustained > $80/renter → REPRICE migration reserve into pricing OR tighten owner-exit rules.
3. **K-W5-3**: Owner-initiated rug-pull rate (any cause: exit, sale, default, abandonment). > 5/100 domain-years → architecture review.
4. **K-W5-4**: Regulatory complaint rate (CAN-SPAM, GDPR, state-AG, trademark) per 1,000 renter-months. > 1 → escalate to legal review; > 3 → architecture pause.
5. **K-W5-5**: Indemnification draw-down (claims paid + reserve depletion against caps). Cumulative draw-down > 50% of annual reserve → tighten ToS caps OR raise insurance.
6. **K-W5-6**: Stripe Connect chargeback rate on owner side (renter-disputed payouts). > 1.5% trailing 6-month → tighten owner reserve from 10% → 20%; > 3% → pause owner onboarding.

### Residual Risks (acknowledged, not eliminated)

- **Owner death without succession setup**: residual risk that despite our succession clause, an estate freezes the domain while probate runs. Mitigation: 12-month continuity arrangement (W2 §2j item 9); residual: 5–10% of estates will not cooperate. Affected renters receive RPG migration.
- **Registrar policy change (e.g., GoDaddy bans third-party DNS management on shared domains)**: cross-registrar dependency risk. No structural mitigation; tracked as a watchlist item.
- **Regulatory shift on marketplace facilitation**: state-level money-transmitter expansions, MLETR-style developments, or EU DSA-style obligations could re-classify us. Quarterly counsel review baseline.
- **Adverse selection on sale-escape**: owners contract specifically because they expect to flip soon. Mitigated by exit fee + cap + invocation-rate kill criterion (K-W5-1).
- **Rug-pull-by-coordination**: multiple owners pulling simultaneously after a competitive entry or a brand-damage event. Tail risk; no full mitigation; abuse reserve sized for ≤ 5% concurrent withdrawal.

---

## §1. Legal & Operations Expert — Primary Memo

### 1.1 Rug-Pull Taxonomy

Six structurally distinct ways a domain disappears or becomes unusable for renters:

| # | Failure mode | Trigger | Owner intent | Speed | Severity (renters affected) | Primary mitigation |
|---|---|---|---|---|---|---|
| 1 | **Planned exit** | Owner gives 90/180-day notice per lease | Cooperative | Slow | All renters on domain | RPG migration; reserve covers refund + credit |
| 2 | **Sale-escape invocation** | Bona-fide third-party offer ≥ floor price | Cooperative | 180 days | All renters on Standard-tier domain | Disclosed at signup; exit fee funds migration; capped at ≤ 30% inventory (K-W5-1) |
| 3 | **Owner default / non-cooperation** | Owner stops responding; refuses DNS changes; pulls records; transfers domain hostilely | Adversarial | Fast (hours–days) | All renters on domain | Owner contract liquidated-damages clause; reputation flag; renter migration via RPG; insurance |
| 4 | **Domain expiration / non-renewal** | Owner fails to renew at registrar | Negligent | Days (registrar-dependent) | All renters on domain | Renewal-monitoring service (we track expiry; alert at 60/30/14/7/1 days; auto-pay on owner authorization where registrar permits); backorder fallback |
| 5 | **Owner death / incapacity** | Owner dies; estate freezes; succession unclear | None | Variable (weeks–months) | All renters on domain | Succession clause (W2 §2j item 9); 12-month continuity; pre-collected estate-contact info |
| 6 | **Registrar / policy hostile takeover** | Registrar suspends domain (TOS violation, abuse complaint, government order) | Third-party | Fast | All renters on domain | Diversification across registrars; legal challenge fund; insurance |

**Cross-cutting mitigation set:**
- **Renewal-monitoring service** (engineering build): nightly WHOIS expiry check on every live domain; tier-aware alerting to owner + ops; auto-pay rights where the owner has granted them.
- **Domain-of-record diversification**: at marketplace level, cap any single registrar to ≤ 35% of live inventory once we exceed 50 domains. Reduces concentrated registrar-policy risk.
- **Migration sister-domain pool**: maintain a small pool (target: 5–10) of platform-owned drop-caught surname domains (per W2 A-W2-14 / W3 §2b-bis) reserved as **migration destinations** when an evicted renter's preferred domain isn't available. This is an explicit dual-use of the drop-catching budget.

### 1.2 Master Owner Lease Agreement — Anatomy

`→ SUPERSEDED IN PART BY §9.1 (B1) on registrar/DNS control, §9.3 (B3) on sale-escape enforcement, §9.7 (M7) on succession operations.`

Building on W2 §2j. Ten key clauses, each with the open question for external counsel:

1. **Grant of license.** Owner grants platform a non-exclusive, revocable license to operate forwarding addresses on the domain at specified subdomain(s) and to manage SPF/DKIM/DMARC/MX records as documented in Schedule A. *Counsel question: revocability scope vs. renter contract enforcement.*
2. **Term.** 1-year initial, auto-renewing in 1-year increments. *Counsel question: enforceability of auto-renewal under state law (CA SB-313 etc.).*
3. **Owner exit.** 90 days' notice for any reason (180 days for Premium tier domains). *Counsel question: liquidated-damages on early exit before initial term (legitimate pre-estimate of loss vs. unenforceable penalty).*
4. **Sale-escape (Standard tier only).** Bona-fide third-party offer ≥ floor price ($25k default; negotiable per domain), 180-day notice, exit fee = greater of (a) 6 months net platform contribution forecast or (b) $500/active renter, paid into migration reserve before the sale closes. *Counsel question: enforceability against third-party purchaser; UCC Article 2 / consumer-product implications; right of first refusal vs. exit-fee sufficient?*
5. **Reserve.** Platform holds 10% rolling reserve on owner payouts, first 180 days; covers chargebacks, abuse cleanup, owner-side disputes; released at day 180. *Counsel question: Stripe Connect Custom mechanics + state reserve laws.*
6. **Owner cooperation duty.** Owner agrees to maintain domain registration in good standing, respond to platform notices within 5 business days, and not transfer the domain without written platform notice. Breach triggers liquidated-damages clause + immediate renter migration. *Counsel question: liquidated-damages quantum; first-amendment / contract-of-adhesion concerns.*
7. **Indemnification (owner-side).** Owner indemnifies platform for harms arising from owner's wrongful withdrawal, owner-side trademark claims on the domain, and owner-initiated abuse (e.g., owner sets up phishing on a different subdomain). Platform indemnifies owner for harms arising from renter abuse not detected by our published controls. *Counsel question: cap structure; insurance coordination.*
8. **DNS authority.** Owner grants the platform authority to publish DNS records on the agreed subdomain(s) via a TOTP-audited management interface. Owner retains revocation rights per termination clause. *Counsel question: scope and revocation mechanics.*
9. **Succession.** In event of owner death/incapacity, platform continues operating the domain under a 12-month continuity arrangement with the registrar of record; payouts held in escrow for the estate; estate may terminate with 90 days' notice. *Counsel question: probate interaction; common-law jurisdictional differences.*
10. **Dispute resolution.** Binding arbitration (AAA Commercial Rules); Delaware governing law; class-action waiver. *Counsel question: enforceability of class waiver post-Lamps Plus / state-by-state.*

**Open clauses (not yet drafted):** anti-circumvention (owner cannot transact directly with a renter to bypass the platform), tax-information (W-9 / 1099-K cooperation), audit rights, force majeure carve-out for registrar/government action.

### 1.3 Renter ToS — Anatomy

Five customer-facing locks (with the legal mechanism that backs each):

1. **Renter Protection Guarantee (RPG)** — see §Executive Summary item 3. Mechanism: contractual obligation backed by migration reserve.
2. **Acceptable Use Policy (AUP)** — no commercial bulk mail, no marketing list use, no transactional mail for non-renter business identity, no impersonation, no harassment. Mechanism: ToS termination + abuse cooperation with ESPs.
3. **CAN-SPAM responsibility allocation** — renter is the "sender" of all outbound mail from their bridge mailbox; commercial messages must comply with CAN-SPAM directly. Platform is "service provider" for forwarding only. Mechanism: ToS push.
4. **Indemnification posture** — platform-side caps cover the first $5k of harm per incident from same-domain impersonation by other renters of the same domain (W4 §2.5.3), declines to cover commercial/business-loss claims, requires renter to maintain own renter's-insurance for outbound-side harms above $5k. Mechanism: ToS + insurance.
5. **Subscriber identity verification** — renter accepts that ID-verification (W4 §2.5.2) is mandatory and that misrepresentation voids the contract. Mechanism: contract + IDV vendor record.

### 1.4 Owner-Pull-During-Active-Incident Protocol (W4 launch blocker resolution)

**Scenario:** RBL pause triggered on a domain. The forwarding cohort is paused; renters are unable to receive mail. The owner, panicking about reputation damage, demands to terminate the lease immediately and pull the domain.

**Resolution path (locked):**

1. **Cooling-off period.** Lease cannot be terminated during an active RBL pause. The pause itself is a contractual stop-loss intended to *protect* the owner; terminating during it does not improve their position.
2. **Owner notification.** Within 1 business day of the RBL pause, ops sends the owner a written incident summary: cause, affected renters, expected resolution timeline, the owner's contractual options (none of which include immediate termination during the pause).
3. **Owner cure-or-exit option.** Once the RBL pause clears (delisting confirmed) OR after 30 days of unresolved pause (whichever comes first), the owner may invoke standard 90-day exit. The 30-day waiting clause prevents permanent reputation damage from a transient incident.
4. **Renter migration kicks in immediately on owner notice of exit-after-cure.** Standard RPG applies.
5. **Edge case: owner refuses cooperation during the pause** (e.g., changes nameservers to lock us out). Treated as §1.1 mode 3 (default/non-cooperation); immediate breach; liquidated-damages; renters migrated.

### 1.5 Owner-vs-Renter Abuse Arbitration (W4 launch blocker resolution)

`→ SUPERSEDED BY §9.5 (B5): graduated safe-mode replaces binary "active vs. suspended"; bond mechanics specified; symmetrical renter deposit added.`

**Scenario:** A domain owner asserts that a renter's behavior is damaging their domain (commercial mail blowback, disputed content, third-party complaints to the owner directly). Forwarding logs may or may not corroborate.

**Resolution path (locked):**

1. **Tier 0: ops review.** Ops reviews forwarding logs, Mailgun complaint data, RBL status. If there is clear evidence of renter AUP violation → renter Tier-2/3 path per W4 §Abuse Escalation. If clear no-evidence → owner notified; resolution to non-action with explanation.
2. **Tier 1: ambiguous evidence.** If logs are ambiguous (no Mailgun complaints, no RBL listing, but owner reports third-party complaints reaching them), invoke a 14-day investigation window. Renter forwarding continues unless the owner posts a $500 good-faith bond against frivolous complaint.
3. **Tier 2: contested adjudication.** If after Tier-1 the dispute remains unresolved, escalate to the **Adjudicator of Record**. MVP default: in-house Tier-3 review (founder + counsel of record). Post-MVP: third-party arbitration vendor (e.g., NAM, AAA) with marketplace experience. Adjudicator decision is binding under both contracts (renter ToS arbitration clause; owner lease arbitration clause).
4. **Outcome paths.** (a) Renter found in violation → Tier 2/3 abuse path per W4. (b) Owner found vexatious → bond forfeit to renter; platform note on owner record; second offense raises owner-side reserve to 25% indefinitely. (c) Genuine ambiguity → renter migrates to alternate domain at platform expense; owner not penalized.

**Defaults during dispute:** the renter's slot remains active unless ops has independent abuse evidence. We do not pause renters on owner accusation alone — that creates a structural eviction lever for owners who decide they don't like a renter.

### 1.6 Indemnification Architecture (W4 launch blocker resolution)

`→ SUPERSEDED BY §9.4 (B4): per-incident cap raised to $25k (= insurance deductible); annual aggregate raised to $100k; renter-insurance requirement removed for consumer renters; commercial use HARD BANNED via AUP.`

**Three-layer cap structure (locked):**

| Layer | Coverage | Cap | Funding source |
|---|---|---|---|
| **Layer 1** | First-dollar harms from platform-controlled vectors (RBL listing on platform-mediated forwarding, Mailgun-side reputation events, send-as misconfiguration causing recipient-side filtering) | Per incident: $5,000; annual aggregate: $50,000 | Platform-side indemnification reserve (line item in W3 capital plan) |
| **Layer 2** | Same-domain impersonation harms (W4 §2.5.3 residual, 6–10%) where canonicalization + complaint takedown was followed but harm occurred | Per incident: $5,000 (shared cap with L1); annual aggregate: same $50,000 | Same reserve as L1 |
| **Layer 3** | Above-cap or excluded-class claims (commercial loss, business-loss, intentional torts by renter) | Push to renter via ToS + renter's-insurance requirement; platform absorbs only counsel-cost defense for our own conduct | Renter responsibility + commercial general liability insurance ($1M policy minimum, broker quote required) |

**Insurance backstop.** Platform purchases a Cyber Liability + Tech E&O policy with a $1M aggregate, $25k deductible. Estimated premium: $4,500–$8,000/yr at marketplace scale (broker quote required for accurate number). Modeled into Rev-2 §2i fixed opex via W7 reconciliation.

**Caps test.** K-W5-5 measures cumulative draw-down against the $50k annual aggregate. > 50% → tighten ToS caps OR raise insurance.

### 1.7 Sale-Escape Clause Legal Review (W2 hand-off)

Disposition: **conditionally clear, requires external counsel sign-off pre-launch.**

**Concerns identified internally:**
- **UCC Article 2 inapplicability.** A domain license is not a "good"; UCC Art. 2 should not apply. *Counsel: confirm.*
- **Consumer-product implications.** If renters are consumers (likely), magnuson-Moss Warranty Act considerations on the implied bundle? *Counsel: confirm low risk.*
- **Adverse-selection risk.** Owners signing the Standard tier may specifically be those with active flip intent. Mitigation already built into K-W5-1 (invocation-rate kill); supplement with **pre-signing affirmation** ("Are you currently in active sale negotiations or listed for sale on Sedo/Afternic/etc.? If yes, this clause is not appropriate for you.").
- **Right-of-first-refusal vs. exit-fee.** We chose exit-fee structure (owner pays migration reserve, sale proceeds). Alternative: platform RoFR at the offered price. Trade-off: RoFR adds platform capital exposure but caps adverse-selection. *Counsel: comment.*
- **Disclosure to renters at signup** must be unmistakable. UI mock proposes a checked-box "I understand this domain may be sold during my term, with 180-day notice and migration assistance" before checkout on Standard-tier slots. UX reviewer: confirm clarity.

### 1.8 Regulatory Posture Memo

Eight regulatory regimes and the platform's defensible posture in each. **All require external counsel sign-off.**

**1. CAN-SPAM (US).** Platform = service provider for inbound forwarding; renter = sender for outbound. Renter ToS requires CAN-SPAM compliance for any commercial mail. Platform does not facilitate bulk mail tooling. **Posture: low risk if AUP enforced.**

**2. GDPR / UK GDPR.** Platform is data controller for renter PII (signup data, IDV result, payment, ToS audit trail). Platform is data processor for inbound forwarded message content (transit-only; logs retained 90 days for abuse correlation, then purged unless under legal hold). Owner contract makes owner a co-controller for "their" domain's WHOIS data and authorizes platform processing. SCCs implemented for any non-EEA platform processor (Stripe, Mailgun, etc.). DPO appointment threshold (250 EU subjects) tracked. **Posture: medium complexity; SCCs and DPA template are launch blockers if EU traffic > 0.**

**3. CCPA / CPRA (CA) / CT, CO, VA, UT, OR, TX, etc. state privacy laws.** Renter is a "consumer"; platform is a "business." Standard rights workflow (access, deletion, opt-out of sale — no sale of PII in our model). Privacy policy must enumerate categories. **Posture: standard SaaS compliance; vendor (e.g., Osano, OneTrust) recommended at scale.**

**4. COPPA.** Platform does not knowingly enroll users under 13. ID-verification at signup catches most underage cases. ToS requires age 13+. **Posture: low risk if IDV enforced.**

**5. Trademark / Lanham Act.** Same-surname domains are not trademarks (descriptive personal-name marks are weak); platform's structural risk is when a renter's local-part collides with a strong trademark (e.g., `coca-cola@smith.com`). Mitigation: **AUP prohibits use of third-party trademarks in local-parts**; complaint-driven takedown within 24 hours of notice; UDRP-adjacent process internally for owner-side disputes (no claim of UDRP equivalence). **Posture: medium risk; takedown cost factored into ops budget.**

**6. State money-transmitter laws.** The 60/40 split is processed via Stripe Connect Custom (regulated party = Stripe). Platform is a "marketplace facilitator"; we do not custody funds beyond Stripe's mechanics. **Posture: structural avoidance; counsel to confirm under MSB and state-by-state laws (NY, CA, TX, FL especially).**

**7. Sales tax / marketplace tax.** Renter side is a SaaS subscription; ~22 US states tax SaaS at consumer level. Owner side is platform-origin service revenue; 1099-K threshold tracking required. **Posture: standard SaaS tax compliance; vendor (e.g., Avalara, TaxJar) at scale.**

**8. International — EU DSA, UK Online Safety Act.** Platform is a "hosting service" for forwarded message content; transparency-reporting threshold (45M EU users for VLOP) is far above MVP scale. **Posture: monitor; not a near-term concern.**

---

## §2. Trust & Safety Architect — Secondary Review

T&S secondary review focuses on whether the W4 abuse model is preserved or weakened by W5 continuity decisions. Three notes:

### 2.1 AUP-prohibited use cases (locked into ToS)

Tightens W4 §Abuse Prevention by elevating from "discouraged" to "ToS violation":
- No transactional mail for any business identity (e.g., `noreply@smith.com` for a SaaS startup) — that's not a vanity-identity use case; it's a business-MTA use case.
- No newsletter / commercial bulk (≥ 50 recipients/day or ≥ 200/week from a single rented address triggers automatic AUP review).
- No mail to addresses on suppression lists (Mailgun integration enforces).
- No re-sale or re-licensing of the rented address to a third party.

### 2.2 Migration-during-incident edge case

If a renter is in active Tier-2/3 abuse review *and* the domain owner pulls (§1.4), the renter's migration is contingent on the abuse review concluding. Path:
- Active Tier-1 review: migration proceeds; review continues at new domain.
- Active Tier-2 review: migration paused 7 business days; Tier-2 must conclude or extend with cause.
- Active Tier-3 (suspension pending) review: migration denied; renter receives full pro-rated refund; no migration credit.

### 2.3 Sister-domain pool dual-use

`→ SUPERSEDED BY §9.8 (M4): pool is split into three explicit functions (revenue inventory / reserved migration inventory / emergency non-equivalent path) with target spare capacity defined.`

The drop-catching pool (W2 A-W2-14, W3 §2b-bis) doubles as the migration-destination pool. Implication: when a renter on `johnson.com` migrates to platform-owned `johnston.com`, the platform is the *owner* of the migration target — there is no second owner relationship to manage, no sale-escape risk, and a 100% gross-margin renter slot. Net effect: migration cost decreases for migrations into owned inventory; the owned-inventory class becomes structurally important not just for economics (W3) but for continuity insurance.

---

## §3. Marketplace Economics Analyst — Secondary Review

### 3.1 Reserve Sizing

`→ ALL NUMERICS SUPERSEDED BY §9.2 (B2) and §9.6 (M2): downgraded to PLACEHOLDER pending W7 EV-loss model and reserve-architecture appendix. The $74–82k/yr aggregate figure is a v0 estimate, not a Rev-1 commitment.`

Three reserves to size:

| Reserve | Purpose | Sizing rule | Funded from |
|---|---|---|---|
| **10% owner rolling reserve** | Per-domain, 180-day, covers chargebacks + owner-side abuse | 10% × owner payouts × 180 days | Owner-side payout (per W2 §2j) |
| **Migration reserve** | Platform-level, covers RPG migration costs across all domains | $X/renter-month accrual; sized to cover 1 month × (10% concurrent migration × $80/migration) at Y2 ceiling = ~$2,000/month → $24k/yr at ceiling | Platform-side opex, modeled into Rev-2 §2i |
| **Indemnification reserve** | Platform-level, $50k aggregate annual cap | $50k/yr (line item) plus $25k insurance deductible carve-out | Platform-side opex, modeled into Rev-2 §2i |

**Aggregate W5 annual reserve burden at Y2 ceiling: ~$74–82k/yr** (migration $24k + indemnification $50k + insurance premium $4.5–8k). This is the W7 reconciliation item: Rev-2 §2i did not explicitly carve out W5 reserves; the W3 capital plan ($245k central) absorbs Y1 partial accrual ($30–35k) but Y2 ceiling needs explicit accommodation. Flag for W7.

### 3.2 Sale-Escape Premium Pricing

Premium-tier (sale-free) renter slots could justifiably carry a 10–20% premium over Standard-tier on the same domain, given the asymmetric tail risk. Open question for W7 / Rev-3: do we implement the premium at Standard launch or hold all renters at parity until we have churn data? **Recommendation: hold at parity initially; the renter-protection guarantee already does the heavy lifting on Standard tier; revisit if K-W5-1 fires.**

### 3.3 Stripe Connect Custom — chargeback reality check

Owner-side chargeback risk (renter disputes a charge → Stripe pulls back from owner's payout) is not zero. Modeled at 0.5–1.5% of renter charges in steady state. The 10% rolling reserve is sized to absorb this comfortably; in practice the reserve binds before the chargeback rate becomes economically painful. K-W5-6 watches this directly.

---

## §4. Domain Owner / Supply Advocate — Secondary Review

### 4.1 Does W5 make signing harder?

**Yes, marginally**, but the additions are net-neutral or net-positive when framed properly to owners:

- The 180-day Premium-tier exit (vs. 90-day Standard) is a *concession to renters*, not a burden on owners — owners keep the choice between tiers.
- The succession clause is genuinely valuable to owners (and their families) and was not in the comp set; it's a positive differentiator.
- The reserve (10%, 180 days) was already in W2 §2j; W5 doesn't add to it.
- The owner-side indemnification (clause 7) is *valuable* to owners — it's protection against renter abuse, not a new burden on them. Frame as such in pitch.
- The auto-pay rights for renewal are an *opt-in* that protects the owner from accidental expiration; another carrot.

**Net effect:** the Master Owner Lease Agreement should not materially reduce signing rates. Concierge-MVP exp-1 (W2) will measure this directly.

### 4.2 Sale-escape clause is the carrot, not the friction

Long-Tail Portfolio Squatters specifically signed up *because* of the sale-escape clause. W5's exit-fee structure (vs. RoFR alternative) is owner-friendly: the owner keeps the upside if a buyer materializes, paying only a defined exit fee into the migration reserve. The 30%-of-inventory cap is a *platform-side* portfolio discipline, not an owner-side restriction.

---

## §5. Synthesis & Locked Outputs

**Locked at this workshop:**

1. **Master Owner Lease Agreement structure** (10 clauses, §1.2). External counsel review = launch blocker.
2. **Renter ToS structure** (5 customer-facing locks, §1.3). External counsel review = launch blocker.
3. **Renter Protection Guarantee** (90/180-day notice, migration assistance, refund + credit) — locked customer-facing.
4. **Two-tier domain product** (Premium sale-free, Standard sale-escapable, ≤ 30% inventory cap on Standard) — locked.
5. **Three-layer indemnification structure** (§1.6) — locked at design level; insurance broker quote required.
6. **Owner-pull-during-incident protocol** (§1.4) — locked.
7. **Owner-vs-renter abuse arbitration path** (§1.5) — locked at design level; adjudicator-of-record decision required pre-launch.
8. **Sale-escape clause structure** (§1.7) — locked at design level; external counsel sign-off required pre-launch.
9. **Regulatory posture** across 8 regimes (§1.8) — locked positioning; external counsel sign-off required pre-launch.
10. **W5 reserve architecture** (10% owner rolling + migration + indemnification + insurance) — locked structure; numeric tuning open.

**Six MVP launch blockers** (in addition to W4's six gates and six W4 launch blockers):
1. External counsel review of Master Owner Lease Agreement.
2. External counsel review of Renter ToS.
3. External counsel review of regulatory posture memo (8 regimes).
4. Insurance broker quote + binder for Cyber Liability + Tech E&O.
5. Adjudicator-of-record decision (§1.5 Tier-2): in-house Tier-3 vs. third-party vendor.
6. Renewal-monitoring service spec'd and engineered (rug-pull failure mode 4).

**Hard gates (numeric kill criteria) — six (§Executive Summary):** K-W5-1 through K-W5-6, locked into `_kill_criteria.md`.

**Residual risks** — five acknowledged (§Executive Summary). None are full mitigations; all are accepted-with-disclosure or watchlist.

---

## §6. Assumptions & Open Questions

### Key assumptions baked into this memo (carrying into `_assumption_register.md`):

- **A-W5-1**: External counsel can deliver enforceable Master Owner Lease, Renter ToS, and regulatory-posture memos within MVP-launch budget ($15–35k, internal estimate; not yet quoted).
- **A-W5-2**: Sale-escape clause is enforceable in Delaware governing law against a third-party domain purchaser (i.e., the buyer is bound by, or constructively aware of, the migration obligation). Otherwise the clause is theatre.
- **A-W5-3**: Cyber Liability + Tech E&O insurance is available to a marketplace of our profile at the modeled premium ($4.5–8k/yr, $1M aggregate, $25k deductible).
- **A-W5-4**: Stripe Connect Custom keeps the platform outside money-transmitter classification in all 50 states under the marketplace-facilitator analysis.
- **A-W5-5**: Owner death/incapacity rate among the Dormant + Resigned cohort is ≤ 2% / year; succession-clause invocation rate is therefore manageable.
- **A-W5-6**: 10% owner rolling reserve over 180 days is sufficient to absorb chargebacks + owner-side dispute costs at K-W5-6 levels.
- **A-W5-7**: ≤ 30% sale-escapable inventory cap is sufficient to keep aggregate sale-escape invocation impact below renter-trust collapse threshold (renter-side complaint rate stays inside K-W5-4).

### Open questions handed to W6 (Red Team):

1. **Owner collusion / coordinated rug-pull**: what if a competitor approaches our owners and offers them more to defect simultaneously? Architecture review trigger?
2. **Adversarial succession**: estate of a deceased owner is captured by a hostile heir who weaponizes the domain (extortion: pay or I cancel all renters).
3. **Frivolous owner-vs-renter complaints**: does the $500 bond actually deter? Test case design.
4. **Registrar policy hostile takeover** (failure mode 6) — full red-team on ICANN, registrar, and DNS-provider dependency.
5. **Regulatory shift** scenario planning: what happens if a state AG takes interest? What if EU classifies us as a hosting provider with takedown obligations on inbound?
6. **Sale-escape gaming**: owner manufactures a bona-fide offer (collusive third party) to invoke the clause cheaply.

### Open questions handed to W7 (Go/No-Go):

1. **Total launch-blocker count is large.** Across W4 + W5 we now have **18+ items** that must clear before code build (six W4 hard gates, six W4 launch blockers — including the Rev-2.2 sending-bridge dependency — and six W5 launch blockers, plus their numeric kill criteria). W7 must reconcile against the W3 capital plan and timeline.
2. **External counsel budget reconciliation.** $15–35k internal estimate vs. Rev-2 §2i fixed opex envelope. Likely requires a one-time pre-launch budget line, not opex.
3. **Insurance premium reconciliation.** $4.5–8k/yr was not in Rev-2 §2i; W7 must absorb.
4. **Reserve aggregate burden** ($74–82k/yr at Y2 ceiling) — see §3.1.

---

## §7. Handoff to W6 (Red Team)

W6 inputs from this workshop:
- Six rug-pull failure modes (§1.1) — stress-test each against adversarial scenarios.
- The Master Owner Lease (§1.2), Renter ToS (§1.3), and regulatory posture (§1.8) — find the exploit paths.
- The owner-vs-renter arbitration path (§1.5) — find the gaming.
- The sale-escape clause (§1.7) — find the manipulation.
- The indemnification cap structure (§1.6) — find the cap-blowout scenario.
- The reserves (§3.1) — find the depletion attack.
- Open questions §6 list 1–6 — adversarial scenarios specifically requested.

W6 should also revisit W4 §2.7 sending-bridge dependency (Rev-2.2) for a Gmail-policy-shift scenario; W4 §2.5 compound-slot abuse-ring economics with the new $500 owner-vs-renter bond as a new lever; and the cross-cutting question of multi-vector concurrent failure (e.g., RBL pause + owner exit + insurance claim simultaneously).

---

*End of W5 v0 draft — 2026-04-27. Status: draft, **major rework pending**; rubber-duck findings recorded in §8 below.*

---

## §8. Rubber-duck findings (2026-04-27) — Rev-1 work queue

A rubber-duck critique was run against this v0 draft on 2026-04-27. **Verdict: MAJOR-REWORK.** All B and M findings have been addressed in §9 below (Rev-1 amendments, same-day pass). Disposition status is annotated against each finding.

### §8.1 Blocking findings (must resolve in Rev-1)

**B1.** [**RESOLVED in §9.1.**] Registrar/DNS control model is not enforceable. Lease clauses cannot stop an owner from changing nameservers, removing apex MX, transferring the domain, or letting it expire. Also a technical bug: the proposed `mail.<domain>` NS delegation does not give the platform control over `@domain.com` email (apex MX + apex DKIM/DMARC selectors required). Rev-1 must specify a real control architecture: registrar transfer-lock + registry lock, platform-visible auto-renew status, contractual platform-paid-renewal-with-recoupment right, apex-DNS authority sufficient for `@domain.com`, and for Premium either escrowed registrar access or downgrade "sale-free" → "enhanced notice + damages-backed best-efforts."

**B2.** [**RESOLVED in §9.2 (deferred to W7 with placeholder downgrade).**] W5 reserve burden ($74–82k/yr at Y2 ceiling) likely breaks Rev-2 economics and is not reconciled.** Rev-2 central case is already tight (~$245k max drawdown, breakeven month 48–52). The v0 draft also confuses *annual expected loss* with *balance-sheet target reserve*, and may double-count Rev-2's existing abuse and sale-escape lines while under-accounting legal-defense cash needs. Rev-1 must (a) separate balance-sheet target vs. annual expected loss, (b) build per-incident-type EV loss model, (c) compute per-renter/month cost impact by tier, (d) update capital requirement under base + 1 major migration event + 1 indemnity claim hitting deductible, and (e) make an explicit pricing/share/inventory/capital decision. This work belongs in W7 reconciliation; until done, all reserve numbers in §3.1 are placeholders.

**B3.** [**RESOLVED in §9.3.**] Sale-escape and Premium "sale-free" are soft promises without enforcement.** No anti-avoidance against LLC-membership-interest sale; no seasoning period; exit fee is rounding error vs. high-value sales (50 renters × $500 = $25k, weak vs. six-figure flips); only $2.5–7.5k at early liquidity. RoFR was rejected without an alternative escrow/buyer-assumption mechanism. Rev-1 must add: (a) anti-avoidance clauses (asset sale, equity sale, change of control, beneficial-ownership transfer, registrar transfer, DNS transfer, encumbrances), (b) 12-month seasoning, (c) exit fee = greater-of {per-renter, months-of-gross-revenue, % of sale proceeds above floor}, (d) sale-proceeds escrow or broker closing instructions, (e) for Premium either registrar-level escrow or relabeling away from "sale-free."

**B4.** [**RESOLVED in §9.4.**] Indemnification/insurance structure relies on coverage and collectability that may not exist.** $5k incident cap sits *below* the modeled $25k insurance deductible, so insurance never responds to capped incidents. Cyber/Tech E&O policies typically exclude intentional acts of insureds' customers — exactly the spam/impersonation/phishing cases the platform claims to indemnify. Pushing above-cap losses to consumer renters via "renter's-insurance requirement" is unrealistic and uncollectible at the price point. Rev-1 must (a) get broker quotes covering email-abuse/spam/phishing exclusions, defense-costs treatment, contractual-indemnity coverage, (b) align platform caps with deductible reality (a $5k self-insured cap is *not* insurance-backed), (c) replace "renter's insurance requirement" with a realistic collectability model assuming consumer-renter recovery ≈ 0, (d) decide whether business/commercial use is fully banned (not merely excluded from indemnity). Insurance binder + coverage summary reviewed by counsel becomes a hard launch blocker.

**B5.** [**RESOLVED in §9.5.**] Dispute default ("renter active unless independent evidence") creates a Gmail-send-as abuse window.** This conflicts with W4's already-reactive complaint-driven posture, and the $500 owner bond's procedural effect is not actually defined (does posting it pause the renter? accelerate review? buy adjudicator deposit?). Rev-1 must replace binary "active vs. suspended" with graduated safe-mode: (a) Tier-1 ambiguous owner complaint → throttle forwarding, freeze send-as setup changes, increase logging, 72h triage deadline (not 14 days); (b) define exactly what owner bond buys procedurally; (c) make bond symmetrical (renter contesting may post smaller deposit); (d) emergency exception for credible third-party complaint evidence.

### §8.2 Medium findings (resolve in Rev-1 or schedule into W6/W7)

**M1.** [**ACCEPTED into §9.6 + new launch blocker LB-W5-7 (counsel + Stripe written confirmation).**] Stripe Connect / money-transmitter posture is conclusory. Connect Custom + owner reserves + migration reserves + indemnification reserves + payout-timing discretion can look like funds control, not pure marketplace facilitation. Counsel memo + Stripe written confirmation required, covering merchant of record, payout-timing control, reserve-holding location, commingling, state-by-state treatment for NY/CA/TX/FL.

**M2.** [**RESOLVED in §9.6.**] Reserve commingling and bankruptcy-remoteness are not specified.** "Segregated account" is undefined — separate bank? trust? bankruptcy-remote restricted cash? operating-account ledger entry? Rev-1 needs a reserve architecture appendix covering insolvency priority, draw approvals, and whether owner rolling reserves are owner funds or platform funds.

**M3.** [**RESOLVED by §9.10 (M8 cross-border decision = US-only MVP).**] GDPR controller/processor split is likely oversimplified. Forwarded email content contains third-party (sender) PII; spam filtering, abuse detection, quarantine, legal holds, complaint adjudication all involve platform determining purpose/means → controller activities, not processor. Privacy counsel must classify each data flow and decide whether EU/UK traffic is excluded from MVP.

**M4.** [**RESOLVED in §9.8.**] Sister-domain pool is overloaded with four conflicting functions (revenue inventory, migration insurance, drop-catch experiment, displacement fallback). Separate "revenue owned inventory" / "reserved migration inventory (priced as insurance)" / "emergency non-equivalent migration path"; define target spare capacity and surname-distance rules; if no equivalent destination exists, RPG should say so plainly.

**M5.** [**RESOLVED in §9.5 (graduated safe-mode) + §9.11 (kill-criteria absolute triggers K-W5-3a/3b/3c).**] K-W5 thresholds are not actionable enough. K-W5-3's 5/100-domain-yrs trigger waits for many customer failures before "architecture review" (a non-action). Add early absolute triggers: first owner-initiated rug-pull in first 12 months → freeze new Standard sale-escapable onboarding; any Premium owner attempted sale → suspend Premium claims; any rug-pull affecting >25 renters → immediate W7 reforecast. Replace "architecture review" with explicit actions (suspend supply, require registrar escrow, raise exit fees, reduce Standard cap, reprice reserves).

**M6.** [**RESOLVED in §9.4 (insurance) + new launch blocker LB-W5-7 (counsel scope) + revised A-W5-1.**] Counsel budget is likely understated and missing categories: privacy DPA/SCC package, payments/MSB specialist, tax/sales-tax/VAT, registrar/ICANN counsel, insurance coverage review, owner KYC/W-9/1099 workflow, probate/successor-contact playbook, foreign-owner exclusion-or-policy decision. Rev-1 must turn A-W5-1 into a quoted workplan with named counsel categories and hard budget bands; if quoted pre-build legal exceeds the envelope, that feeds W7 capital and go/no-go.

**M7.** [**RESOLVED in §9.7.**] Owner death/incapacity plan is contractual not operational. A lease clause does not guarantee registrar access after death (probate, locked accounts, expired payment cards, foreign jurisdictions). Rev-1: require successor contact at onboarding, auto-renew enabled and verified annually, platform emergency renewal right where registrar permits, consider LLC/trust ownership for high-value Premium domains, define 7/14/30-day estate-non-response escalation, exclude solo-owner foreign domains from MVP.

**M8.** [**RESOLVED in §9.10: Option A locked (US-only MVP).**] Cross-border owner/renter scope is inconsistent. W2 explicitly recommended US owners + US renters only for MVP; W5 v0 analyzes GDPR/UK GDPR/SCCs/EU DSA as if EU traffic may exist. Rev-1 must make a hard MVP scope decision: Option A (US-only — block EU/UK signups, simplify W5) or Option B (international from day one — GDPR/DPA/SCC become launch blockers). Recommend Option A to align with W2.

### §8.3 Minor findings (one-liners; can be deferred or rejected with rationale)

- K-W5-1 inherits W2's K-W2-8 placeholder but changes denominator/population (Long-Tail Portfolio → Standard sale-escapable). Add a note clarifying.
- "DPA template required per renter" (§1.8) is wrong for consumer renters; DPAs are processor-agreement artifacts, not consumer privacy notices.
- COPPA posture says ToS age 13+ but renter contracts/payments/IDV likely require 18+; align (W2 already proposed 18+).
- RPG "1-month migration credit" does not restore identity if renter was using `firstname@lostdomain.com`; reframe as compensation, not protection.
- Sales tax / VAT scope ("~22 SaaS-tax states", "VAT") needs nexus / marketplace-facilitator / digital-service flow definition.
- Owner good-faith bond mechanics (§1.5) need explicit specification: who holds it, when forfeited, refund conditions, procedural effect of posting.

### §8.4 Rev-1 pass plan

Rev-1 should consolidate B1–B5 + M1–M8 into a single revision pass. Suggested ordering: (1) registrar/DNS control architecture (B1) — feeds Premium/Standard product definition; (2) sale-enforcement mechanism (B3) — depends on B1; (3) reserve-and-economics reconciliation (B2 + M2) — feeds W7; (4) insurance reality check (B4 + M6) — depends on broker quotes; (5) dispute safe-mode (B5); (6) cross-border scope decision (M8) — gates GDPR/payment-regime depth (M1, M3); (7) operational ops items (M4, M5, M7); (8) minor cleanup. Rev-1 closure criterion: every B finding either resolved or explicitly downgraded with written rationale and accepted residual risk.

---

## §9. Rev-1 Amendments (2026-04-27)

This section is the authoritative Rev-1 design layer. Where v0 §1–§7 conflicts with §9, **§9 controls.** Each subsection resolves the correspondingly-numbered rubber-duck finding from §8. Status-of-section is recorded at the head of each subsection.

### §9.1 Registrar/DNS control architecture (resolves B1)

**Status: locked at design level pending registrar-partner technical confirmation (new launch blocker LB-W5-7).**

The v0 "owner-controlled, platform-monitored" model is downgraded. Rev-1 splits control architecture by tier and adds enforceable operational controls:

**Bonded Premium tier** (renamed from "Premium / sale-free"):
- Owner option (a) — **registrar co-management**: owner transfers domain registration to a vetted platform-partner registrar (candidates: Cloudflare Registrar, Porkbun, Hover) where the owner remains beneficial owner but the registrar account has dual-control delegation (owner + platform). Platform cannot initiate transfer-out without owner; owner cannot initiate transfer-out without platform countersign during lease term.
- Owner option (b) — **owner-retained registrar with hard controls**: owner keeps existing registrar but contractually grants (i) registry-lock + transfer-lock enabled and verified, (ii) auto-renew enabled with platform-funded backstop, (iii) platform-paid emergency renewal right with recoupment from owner payouts, (iv) read access (or scheduled WHOIS attestation) to confirm lock + renewal status quarterly.
- Either option requires: apex MX, apex `_dmarc` TXT, and DKIM selectors at apex (e.g., `selector1._domainkey.<domain>`) under platform DNS authority. The v0 `mail.<domain>` NS-delegation model is technically insufficient for `@<domain>` email and is rejected.
- "Sale-free" promise replaced with **"Bonded Premium = damages-backed continuity commitment"**: backed by (i) registrar-level controls above, (ii) liquidated damages on contractual exit attempt during term, (iii) for the highest tier, optional escrowed registrar credentials at a third-party escrow agent (release on documented platform breach or term expiration). The product label is honest: there is no absolute legal mechanism preventing a determined hostile owner from acting against the lease, but there are financial and operational controls that make hostile action costly and slow enough for renter migration.

**Standard / Sale-Escapable tier:**
- Owner retains full registrar control.
- Required: registry-lock + transfer-lock enabled, auto-renew on with verified payment method, platform emergency renewal right contractually granted with recoupment.
- Apex DNS authority requirements identical to Bonded Premium.
- Disclosed at signup: "This domain may be sold or withdrawn during your term. Standard tier."

**New launch blocker LB-W5-7**: Registrar-partner technical/legal confirmation. Platform must (i) select registrar partner(s), (ii) confirm via written statement from the registrar that the proposed dual-control / delegated-admin / lock arrangements are supported and survive owner non-cooperation scenarios, (iii) get counsel sign-off on the resulting contractual + technical model. Without this confirmation, neither tier can launch.

**Residual risk acknowledged**: even with the above, a determined hostile owner who is willing to commit registrar-account fraud or domain theft can still cause renter loss. The platform's remedy in those cases is damages + insurance + RPG migration; absolute prevention is not promised.

### §9.2 Reserve numerics deferred to W7 (resolves B2; partial M2)

**Status: numerics-pending; structural decisions locked.**

All v0 §3.1 reserve numerics ($24k migration, $50k indemnification, $74–82k aggregate) are downgraded to **PLACEHOLDER**. Rev-1 commits only to the *structure* of three reserves; sizing is a W7 deliverable.

W7 reserve-sizing inputs (required before launch):
1. Per-incident-type expected-value loss model:
   - Sale-escape invocation (frequency × per-event migration cost).
   - Owner default / non-cooperation (frequency × migration + legal cost).
   - RBL incident (frequency × pause cost + delisting cost).
   - Indemnity claim (Layer 1+2, frequency × cap or actuals).
   - Legal defense floor (counsel hourly + retainer expectations even on no-payout claims).
2. Distinction between **balance-sheet target reserve** (cash held to absorb claims when they arrive) and **annual expected loss** (P&L line). The v0 numbers conflated these.
3. Per-renter/month cost impact, broken out by tier (Bonded Premium vs. Standard).
4. Updated capital requirement under three scenarios:
   - Base W5 reserve load (steady-state).
   - One major domain migration event in Y1 (e.g., 50-renter Bonded Premium domain rug-pull).
   - One indemnity claim hitting the $25k insurance deductible + $50k legal-defense floor.
5. Explicit W7 decision among five levers: raise prices, reduce owner share, narrow Standard tier, reduce sale-escapable inventory cap below 30%, raise more capital. Status-quo Rev-2 is not assumed adequate.

Until W7 produces these numbers, **no W5 reserve figure is treated as locked.** Rev-2 §2i is *not* claimed to absorb the W5 burden.

### §9.3 Sale-escape and Premium enforcement mechanism (resolves B3)

**Status: locked at design level pending counsel sign-off.**

Replaces v0 §1.2 clause 4 + v0 §1.7. Sale-escape clause for Standard tier is rewritten with anti-avoidance + seasoning + greatest-of fee + escrow:

**Anti-avoidance triggers** (any one constitutes a "Change of Control" invoking sale-escape):
- Asset sale of the domain.
- Equity / membership-interest sale of the entity owning the domain ≥ 50% transfer.
- Beneficial-ownership change ≥ 50% (per FinCEN beneficial-ownership reporting standard).
- Registrar-of-record transfer to any non-partner registrar.
- DNS-authority transfer (change of nameservers away from platform-required configuration).
- Any encumbrance, lien, security interest, or pledge of the domain.
- Sale or assignment of the lease itself.
- Owner enters bankruptcy, receivership, or assignment for benefit of creditors.

Lease binds successors-in-interest; any purchaser/assignee acquires the domain *subject to* the lease. Sale-escape exit fee is owed on any of the above; the buyer's notice and the existence of the lease are recorded in WHOIS commentary where the registrar permits and via UCC-1-style filing where applicable (counsel to confirm appropriate mechanism for domain interests).

**12-month seasoning**: no sale-escape invocation during the first 12 months of any domain's listing (Standard or Bonded Premium). Exception: extraordinary platform-approved sale (e.g., owner medical emergency).

**Exit fee recalculated** as the **greatest of**:
- $1,000 × number of active renters at notice (was $500 — doubled to actually deter at small inventory).
- 12 months of platform's projected gross revenue from the domain at notice (vs. v0's "6 months net contribution" — uses projected gross, not net, and 12 months not 6).
- 5% of sale proceeds above a $25k floor.

Capped at $250k absolute (the cap exists so owners with extremely high-value domains don't refuse the lease).

**Sale-proceeds escrow**: closing instructions to the broker (Sedo / Afternic / GoDaddy / direct) require platform consent for proceeds release; alternatively a deposit-and-release escrow at a third-party agent. If no broker is involved (private direct sale), exit fee must be deposited with platform before the registrar transfer-out is initiated. Counsel to confirm enforceability in Delaware governing law against third-party purchaser.

**Pre-signing affirmation** (mandatory, not optional, per v0 §1.7 supplement): owner must affirm at signup that they are not currently in active sale negotiations and have no listed-for-sale presence on Sedo / Afternic / Flippa within the past 90 days. Misrepresentation = lease breach + immediate exit-fee acceleration.

**Bonded Premium sale enforcement**: Bonded Premium (renamed from "sale-free") cannot invoke sale-escape during term. Owner attempting Change of Control on a Bonded Premium domain triggers (a) immediate breach, (b) liquidated damages = 24 months of platform projected gross revenue from the domain or $50k (whichever greater), (c) registrar lock-out asserted under §9.1 controls, (d) all renters migrated under RPG with full refund + 12-month replacement service credit (raised from 1-month to recognize identity-disruption magnitude).

**RoFR** (right of first refusal) remains rejected — the platform's capital exposure and bid-management overhead outweighs the deterrent value once the greatest-of exit fee + sale-proceeds escrow are in place.

### §9.4 Indemnification and insurance reality check (resolves B4; partial M6)

**Status: locked at design level pending insurance broker quote (LB-W5-4) and counsel coverage review (LB-W5-7).**

Replaces v0 §1.6:

**Layer 1 + 2 cap raised**: per-incident cap $25,000 (was $5,000) — sized to match expected $25k insurance deductible so the insurance backstop actually responds to a claim that hits the cap. Annual aggregate $100,000 (was $50,000).

**Layer 3 redesigned**: "renter's-insurance requirement" REMOVED for consumer renters. Replaced with:
- Above-cap consumer recovery is assumed = $0 in planning (planning value).
- **Commercial / business use HARD BANNED via AUP** (not merely excluded from indemnity). Business use grounds for immediate termination + lease forfeiture, not just a coverage exclusion. Tightens v0 §2.1.
- Structural ceiling on potential damages: monthly outbound-volume cap (≤ 200 messages/day, ≤ 1,500 messages/week — already implicit in v0 §2.1, now lifted to a hard technical limit enforced at the bridge layer).
- For renter slots that breach business-use AUP and cause harm, platform retains right to seek damages from the renter, but does not budget recovery into reserves.

**Insurance binder + coverage summary review by counsel = launch blocker** (LB-W5-4 expanded). Specific scrutinies:
- Email-abuse / spam / phishing exclusion language.
- Intentional-acts-of-customer exclusion.
- Contractual-indemnity coverage (covering platform's contractual indemnity obligations to owners and renters).
- Defense-cost treatment (inside vs. outside policy limits).
- Media / personal-injury / Coverage B equivalent.
- Whether Cyber Liability + Tech E&O is the right policy stack or whether a media-liability rider is also needed.

**Insurance premium estimate revised**: $6–12k/yr for $1M aggregate / $25k deductible (was $4.5–8k). Broker quote required before launch.

**Counsel budget revised**: see §9.6 for full breakdown; insurance-coverage review adds $1–3k.

### §9.5 Dispute safe-mode (resolves B5; partial M5)

**Status: locked at design level.**

Replaces v0 §1.5:

**Tier 0 (clear evidence either way)**: unchanged from v0.

**Tier 1 (ambiguous evidence) — graduated safe-mode triggered AUTOMATICALLY** on any owner complaint with prima facie evidence (timestamped third-party email, explicit reference to the renter's address). The renter is not suspended, but the slot enters safe-mode:
- Outbound forwarding throttled to 50 messages/day (down from 200 default).
- Send-as / Gmail bridge configuration changes frozen (renter can use the slot but cannot reconfigure it during the window).
- Inbound forwarding log retention raised from 90 → 180 days for the slot.
- **72-hour initial triage deadline** (down from 14 days for full investigation). At T+72 hours, ops issues a preliminary disposition: dismiss (safe-mode lifted), escalate to Tier 2, or extend with cause for an additional 7-day investigation window.
- Renter is notified of safe-mode entry and the reason.

**Owner good-faith bond mechanics specified** (resolves minor):
- Bond amount: $500.
- Held in: Stripe Connect platform balance under owner-attributed segregated ledger entry; not commingled with operating funds.
- Buys procedurally: third-party adjudicator engagement (escalates Tier 1 → Tier 2 immediately) AND expedited 5-business-day adjudicator decision deadline.
- Forfeit conditions: adjudicator finds owner's complaint vexatious, retaliatory, or knowingly false. Forfeited bond paid to renter as compensation.
- Refund conditions: owner prevails OR dispute is resolved via mediation OR adjudicator finds genuine ambiguity (no fault on either side).
- Maximum hold window: 30 days from posting. After 30 days, bond is automatically refunded if no adjudicator decision has issued; bond posting does not extend the window.

**Symmetrical renter cost-deposit**: if a Tier-2 escalation occurs and the renter contests after the adjudicator has reviewed initial evidence, renter may post a $100 cost-deposit to require full adjudicator hearing. Same forfeit / refund mechanics, scaled to the deposit amount.

**Emergency exception**: credible third-party complaint with corroborating headers (e.g., named victim providing message-ID + DKIM signature confirming renter origin) bypasses Tier 1 to Tier 2 immediately, with safe-mode plus *throughput pause* (not just throttle) until Tier-2 decision.

**Defaults during dispute (revised)**: the renter remains operational under safe-mode; binary "fully active vs. fully suspended" is replaced with the graduated state. This protects against weaponized owner accusations while closing the abuse window the v0 default created.

### §9.6 Reserve architecture and Stripe / money-transmitter posture (resolves M2; supports M1)

**Status: locked at structural level pending counsel sign-off (LB-W5-7) and Stripe written confirmation (LB-W5-8).**

**Owner rolling reserve (10%, 180 days)**: held in Stripe Connect platform balance. Funds are owner-attributable but classified for marketplace purposes as "facilitator funds in transit" — not formal escrow, not trust funds. Platform discloses in renter ToS that these funds are *not* renter-protective; they protect against owner-side chargebacks and abuse cleanup only.

**Migration reserve**: held in a **separate platform-segregated bank account** designated FBO ("for benefit of") renter-class beneficiaries. Restricted-cash classification on financial statements. Bankruptcy-remoteness via segregation + FBO designation, not via formal trust (counsel to confirm whether this is sufficient or whether a formal trust structure is required for the size of the reserve). Insolvency-priority disclosure included in renter ToS: in platform insolvency, migration reserve is asserted as customer-benefit funds, not corporate assets; recovery position is determined by court.

**Indemnification reserve**: corporate operating-account ledger entry; treated as accrued liability per GAAP, not segregated funds. Insurance is the primary backstop; the reserve is a tactical buffer for claims under deductible.

**Reserve documentation**: financial statements include a "Marketplace Continuity Reserves" footnote enumerating all three reserves, balance, draw-down history, and replenishment policy. Reviewed annually by counsel.

**Stripe Connect / money-transmitter posture (M1 elevation)**: counsel memo + Stripe written confirmation = launch blocker LB-W5-8. Specific items requiring written confirmation:
- Merchant of record on renter charges (platform).
- Payout-timing control (platform discretion vs. Stripe-fixed).
- Whether reserve-holding location (Stripe balance vs. platform bank) changes regulatory classification.
- Whether platform discretion over migration / indemnity reserves crosses a line.
- State-by-state treatment for NY (especially), CA, TX, FL.
- Position on whether US-only MVP (per §9.10) limits VARA / state DFS interest.

If counsel finds the analysis fails in any state, the platform restricts onboarding to compliant states for MVP rather than acquire MTL.

### §9.7 Owner death / incapacity operational plan (resolves M7)

**Status: locked at design level pending counsel sign-off on probate interactions.**

Replaces v0 §1.2 clause 9:

- **Successor contact required at owner onboarding** (not optional). Owner must provide name + email + phone of a designated emergency contact who is authorized to receive notice in the event of owner incapacity.
- **Auto-renew enforced and verified annually** by platform via WHOIS expiry monitoring. If auto-renew status cannot be confirmed (e.g., owner's payment method expired), platform's emergency renewal right under §9.1 is triggered with recoupment notification.
- **Platform emergency renewal right** contractually granted: platform may pay registrar renewal fees and recoup from next owner payout. Where the registrar does not permit third-party renewal, the platform notifies the successor contact and requires successor to act within 7 days.
- **Bonded Premium domains with assessed value > $25k**: required to be held by an LLC, trust, or estate-planning entity, not a natural person. Reduces probate exposure.
- **Estate-non-response escalation**: 7-day acknowledgment, 14-day cooperation request, 30-day breach declaration. After 30 days of estate non-cooperation, lease is treated as breached (no liquidated damages against estate beyond loss of platform payouts), all renters migrated under RPG, domain status flagged "estate-frozen" until resolved.
- **Solo-owner foreign domains** (non-US owner of record): excluded from MVP per §9.10.

### §9.8 Sister-domain pool — three explicit functions (resolves M4)

**Status: locked at design level.**

Replaces v0 §2.3:

The owned-domain inventory (W2 A-W2-14, W3 §2b-bis) is split into three explicit functional pools:

1. **Revenue owned inventory**: monetized normally as platform-owned domains. Standard renter slots. 100% gross margin to platform. No special continuity treatment.
2. **Reserved migration inventory**: domains held back specifically for RPG migration destinations. Target capacity = 5% of Y2-ceiling concurrent renter count (W7 to confirm). Not offered for sale to renters during reserve period. Pricing of this insurance cost is modeled into the migration reserve under §9.2.
3. **Emergency non-equivalent migration path**: when no surname-equivalent destination exists for an evicted renter (e.g., the renter's surname is unique enough that no sister domain is in the pool), the renter receives:
   - Full pro-rated refund.
   - 12-month equivalent-service credit (raised from v0's 1 month — see §9.9 minor cleanup).
   - $15 ICANN registration credit + free 3-month forwarding-only setup on a personal domain of the renter's choice.
   - Honest framing in ToS and migration communications: **"This is compensation for disruption, not identity restoration. The platform makes no guarantee that any equivalent identity exists at any other domain."**

**Surname-distance rule** (for reserved migration inventory matching): Levenshtein distance ≤ 2 from original domain (e.g., `johnson.com` → `johnston.com` qualifies; `johnson.com` → `smith.com` does not). Renter has refusal right; refusal converts to emergency non-equivalent path.

### §9.9 Minor cleanup (resolves §8.3 minors)

**Status: locked.**

- **K-W5-1 denominator clarified**: "Standard sale-escapable inventory domain-years" — this is a marketplace-wide rate over the Standard tier, not over the W2 Long-Tail Portfolio segment. K-W2-8 placeholder is locked into K-W5-1 at this Rev-1 with the Standard tier scope.
- **"DPA template per renter" REMOVED** for consumer renters. Consumer privacy notice + cookie banner per §9.10 (US-only). DPA reserved for any future B2B product.
- **COPPA age requirement → renter age 18+** (was 13+). Aligns with W2 adult-renter scope; payments + IDV require 18+ regardless.
- **RPG migration credit reframed**: from "1-month migration credit" (v0) to "12-month equivalent-service credit when no surname-equivalent destination is available" (per §9.8) — and explicitly framed as compensation, not identity protection. ToS and signup flow must say: *"If your domain is withdrawn, you may lose the email identity you registered. The platform's protections are designed to give you notice, time, and compensation — not to guarantee that an identical identity is available elsewhere."*
- **Sales tax / VAT scope**: VAT removed (Option A US-only per §9.10). Sales-tax via Avalara or TaxJar; nexus analysis = counsel scope item under LB-W5-7. Initial nexus expected in CA + Delaware; expanded as renter footprint develops.

### §9.10 Cross-border MVP scope (resolves M8) — Option A LOCKED

**Status: locked.**

**Decision**: MVP is **US-only** for both owners and renters. EU/UK/non-US signups blocked at:
- IP-geolocation check at signup (best-effort; not a security boundary).
- Billing address verification (Stripe-side billing-address check); non-US billing addresses rejected.
- Owner onboarding requires US W-9 (citizen or US-resident entity).
- Renter onboarding requires US billing address + US-issued payment method.

GDPR, UK GDPR, SCCs, EU DSA, and UK Online Safety Act analysis is **deferred to post-MVP** and removed from launch-blocker scope. v0 §1.8 regimes 2 and 8 are downgraded to "monitor, not active."

Rationale: this aligns with W2's recommendation (W2 §legal review) and removes substantial counsel scope from MVP. International expansion is a post-MVP product decision, not a launch-blocker.

CCPA / CPRA and other US state privacy laws remain in scope (v0 §1.8 regime 3 unchanged).

### §9.11 Kill-criteria absolute triggers (resolves M5)

**Status: locked.**

Supplements K-W5-3 with three early-stage absolute triggers (see also `_kill_criteria.md`):

- **K-W5-3a**: First owner-initiated rug-pull (any cause) within first 12 months of marketplace operation → FREEZE new Standard sale-escapable onboarding pending root-cause review. Also reduces Standard cap from 30% → 20% pending review outcome.
- **K-W5-3b**: Any Bonded Premium owner attempts Change of Control (per §9.3 anti-avoidance triggers) → SUSPEND all Bonded Premium product claims in marketing; trigger immediate registrar-control architecture review under §9.1.
- **K-W5-3c**: Any single rug-pull affecting >25 renters → IMMEDIATE W7 reforecast; pause new domain onboarding until reforecast completes.

K-W5-3 (steady-state >5/100 domain-years) trigger action upgraded from vague "architecture review" to explicit decision menu: (a) suspend new sale-escapable supply, (b) require registrar escrow for new Bonded Premium, (c) raise exit fees per §9.3, (d) reduce Standard cap below 30%, (e) reprice migration reserve into renter pricing.

### §9.12 Revised launch blocker list

**Status: locked.**

Rev-1 supersedes v0 §Executive Summary "Six MVP Launch Blockers". Final list:

1. **LB-W5-1**: External counsel review of Master Owner Lease Agreement (Bonded Premium and Standard variants).
2. **LB-W5-2**: External counsel review of Renter ToS (incl. RPG, AUP, indemnification posture, US-only scope, money-transmitter disclaimer).
3. **LB-W5-3**: External counsel review of regulatory posture memo (US-only scope per §9.10).
4. **LB-W5-4**: Insurance broker quote + binder + counsel coverage-summary review (per §9.4).
5. **LB-W5-5**: Adjudicator-of-record decision (in-house Tier-3 vs. third-party vendor) per §9.5.
6. **LB-W5-6**: Renewal-monitoring service spec'd and engineered (rug-pull failure mode 4).
7. **LB-W5-7**: Registrar-partner technical/legal confirmation per §9.1 (NEW in Rev-1).
8. **LB-W5-8**: Stripe written confirmation of marketplace-facilitator posture per §9.6 (NEW in Rev-1).
9. **LB-W5-9**: Sale-proceeds escrow / UCC-1-style filing mechanism confirmed by counsel per §9.3 (NEW in Rev-1).
10. **LB-W5-10**: W7 reserve EV-loss model + capital reconciliation completed per §9.2 (NEW in Rev-1; gates Rev-2 capital plan validity).

### §9.13 Counsel budget — Rev-1 itemized estimate (resolves M6)

**Status: estimate; full quote required before commit to W7 capital line.**

Replaces A-W5-1 internal $15–35k estimate. Itemized:

| Category | Estimated band | Notes |
|---|---|---|
| Commercial contracts (Master Lease + Renter ToS, both variants) | $8–15k | Includes Bonded Premium + Standard variant work |
| Privacy / state-privacy / consumer-notice (US-only scope) | $2–4k | Reduced from v0 due to §9.10 EU exclusion |
| Payments / MSB / state money-transmitter analysis | $4–8k | NY, CA, TX, FL focus |
| Tax / sales-tax nexus | $2–4k | Avalara/TaxJar onboarding included |
| Insurance coverage review | $1–3k | Counsel reviews binder text |
| Domain / registrar / ICANN counsel | $2–4k | Confirms §9.1 control mechanisms |
| Reserve architecture / bankruptcy-remoteness | $2–4k | Confirms §9.6 segregation sufficiency |
| Sale-proceeds escrow / UCC-1 mechanism | $1–3k | Per §9.3 |
| **Total** | **$22–45k** | One-time pre-launch line, not opex |

Budgeted as **$50k pre-launch line item** with 10% contingency. Feeds W7 capital plan as a separate line from Rev-2 §2i opex. If quoted total exceeds the envelope, that is a W7 go/no-go input.

### §9.14 Rev-1 closure criteria

**Locked at this Rev-1:**
- Registrar/DNS control architecture (§9.1, pending registrar-partner confirmation).
- Reserve structure (§9.6); numerics deferred to W7.
- Sale-escape and Bonded Premium enforcement mechanism (§9.3, pending counsel sign-off).
- Indemnification cap structure raised to $25k incident / $100k aggregate (§9.4).
- Dispute graduated safe-mode (§9.5).
- US-only MVP scope (§9.10).
- Sister-domain pool three-function split (§9.8).
- Death/incapacity operational plan (§9.7).
- Kill-criteria absolute triggers K-W5-3a/3b/3c (§9.11).
- Launch-blocker list of 10 items (§9.12).

**Still open / handed to W6/W7:**
- Numeric reserve sizing (W7).
- Insurance broker quote (LB-W5-4).
- Counsel sign-off on all items (LB-W5-1/2/3/7/9).
- Stripe written confirmation (LB-W5-8).
- Registrar-partner selection and confirmation (LB-W5-7).
- Adjudicator-of-record decision (LB-W5-5).
- Adversarial scenarios from §6 — handed to W6 Red Team.

**Rev-1 is conditionally locked.** A successful W6 Red Team pass without finding a structural exploit may move Rev-1 to "fully locked." A second rubber-duck pass on Rev-1 itself is recommended before W6 opens.

---

*End of W5 Rev-1 — 2026-04-27. Next: rubber-duck pass on Rev-1 (recommended) before opening W6 Red Team.*

---

## §10. Rev-1 Rubber-Duck Findings (2026-04-27, same-day pass)

A second independent rubber-duck pass was run on §9 Rev-1 itself (not on v0 §1–§7). Verdict: **MAJOR-REWORK** — Rev-1 introduced new structural issues, including one that reintroduces a W4 architecture conflict that Rev-2.1 had previously resolved.

These findings are recorded here for traceability and will be addressed in **W5 Rev-2** (planned next, before opening W6). Rev-1 remains the controlling layer until Rev-2 is committed.

### §10.1 Blocking findings (Rev-1B)

**B1-Rev1. §9.1 Bonded Premium dual-control registrar architecture may not exist as a market product.**
§9.1 names Cloudflare Registrar / Porkbun / Hover as candidates for "dual-control delegation" where neither owner nor platform can transfer out unilaterally. That control pattern is closer to institutional / corporate-domain custody than ordinary registrar delegation. Cloudflare Registrar in particular is famously austere. Option (b) — owner-retained registrar with registry-lock + transfer-lock + auto-renew — relies on owner-controlled settings the owner can revoke at any time; quarterly attestation creates a long blind window.
*Failure mode:* Bonded Premium is marketed as control-backed but may be only contract-promise-backed.
*Rev-2 action:* Replace candidate-registrar list with a hard pre-design gate — identify at least one provider with written support for dual-approval transfer-out, non-owner revocation resistance, platform-visible audit logs, emergency renewal rights, and a defined response SLA. If none exists, downgrade Bonded Premium to "damages-backed only" and re-run W2 economics. Detection cadence must be daily / event-driven, not quarterly, if relied upon for continuity.

**B2-Rev1. §9.1 apex DNS authority is under-specified.**
"Under platform DNS authority" can mean (a) owner keeps nameservers and publishes platform-required records (no real platform authority — contractual + monitoring only), or (b) owner delegates the entire apex zone to platform NS (platform controls website, subdomains, DNSSEC posture — likely commercially unacceptable to many valuable-domain owners, especially Bonded Premium candidates). Rev-1 picks neither.
*Failure mode:* Either Bonded Premium signing rate collapses (model b) or the control claim is illusory (model a).
*Rev-2 action:* Define explicit Model A / Model B / Model C (DNS provider with scoped API/RBAC) and state which is required at each tier. Add owner-side protections (read-only access, change-approval workflow for non-mail records, web/DNS SLA, DNSSEC policy, liability allocation). Re-test W2 conversion with the chosen burden disclosed.

**B3-Rev1. §9.3 sale-escape and Bonded Premium liquidated damages are not deterrent at high domain values.**
Run the math: 50 renters × $1,000 = $50k; at $1M sale, 5% above $25k ≈ $48.75k → renter-count limb dominates at $50k. At $5M sale the $250k cap binds (~5% of value, less than typical broker friction). Bonded Premium liquidated damages = max(24mo gross, $50k) — at 50 renters × $11 ARPU × 24mo = ~$13.2k, real number is $50k. For valuable surname domains, $50k–$250k is cost-of-doing-business, not a deterrent. A flipper with a $1M+ offer can rationally breach.
*Failure mode:* B3 is not actually solved; Bonded Premium is vulnerable to economically rational breach.
*Rev-2 action:* Reframe §9.3 as "mitigates but does not prevent" high-value exits unless stronger control exists. Model deterrence by domain value bands, not renter count alone. Consider uncapped percentage limb or sliding cap tied to appraised price. Require larger pre-funded bond / standby letter / escrow for Bonded Premium domains above a value threshold. Add seasoning-abuse test (recent listing history, broker outreach, parking pages, domain-investor behavior excluded from Bonded Premium and possibly Standard).

**B4-Rev1. §9.3 enforceability depends on legally uncertain domain-security mechanisms.**
Domains occupy a legally messy space: some courts treat them as contract rights with the registrar, not Article 9 property. UCC-1 perfection on a domain may simply not be available in many jurisdictions. Sale-proceeds escrow assumes a cooperative broker / closing channel — private sales, membership-interest sales, or off-platform consideration bypass it.
*Failure mode:* If counsel says no enforceable security interest exists, sale-escape loses force against third-party buyers; A-W5-2 / LB-W5-9 are structurally determinative, not cleanup.
*Rev-2 action:* Elevate LB-W5-9 from "confirm mechanism" to a binary architecture gate. Counsel memo must address: domain as collateral / general intangible, perfection feasibility, remedies against purchaser, escrow enforceability, private-sale avoidance. Add fallback (registrar custody, third-party domain escrow, opaque-LLC restriction, platform-owned inventory pivot) for the case where enforcement fails.

**B5-Rev1. §9.4 / §9.5 reintroduce a W4 architecture conflict — platform cannot throttle Gmail send-as outbound.**
§9.5 says Tier-1 safe-mode "throttles outbound forwarding to 50 messages/day"; §9.4 references a "monthly outbound-volume cap" enforced at the bridge layer. But W4 Rev-2.1/2.2 is explicit: renter outbound goes through Gmail send-as and is **not** platform-controlled. The platform controls inbound forwarding to the renter, not outbound sent by the renter. Throttling forwarding rate-limits the alleged victim's mail receipt while doing little to stop the alleged outbound abuser.
*Failure mode:* The dispute and indemnification design relies on a control that does not exist. Wrong lever.
*Rev-2 action:* Rewrite §9.4 / §9.5 with W4-correct terminology. Replace "outbound cap" with actual enforceable controls — freeze forwarding-destination changes, suspend alias verification token / DNS records, pause inbound forwarding only where appropriate, terminate slot on confirmed abuse, require re-verification / manual review. Re-run indemnification and insurance assumptions without assuming preventive outbound rate control. **This finding reintroduces an issue Rev-2.1 of W4 had previously corrected — an inter-workshop consistency check is needed.**

### §10.2 Medium findings

**M1-Rev1 (§9.4).** "Commercial use HARD BANNED" is not operationalizable as written. Edge cases: receiving payroll/benefits, sending an invoice once, LinkedIn use, side-hustle correspondence. Either narrow to "no bulk marketing / no transactional mail for a business service / no customer-support automation" with examples, or accept enforcement-discretion litigation risk.

**M2-Rev1 (§9.5, §9.6, A-W5-4).** Stripe / banking primitives may not exist as described. "Stripe Connect platform balance under owner-attributed segregated ledger entry" is not escrow; held charges are dispute-exposed. FBO bank accounts require specific banking-product support not all startup-friendly banks offer. "Restricted cash" is an accounting classification, not bankruptcy remoteness. Reserve / bond / MTL claims may be overstated. Need written Stripe + bank confirmations before W7.

**M3-Rev1 (§9.2 ↔ §9.4 internal inconsistency).** §9.2 declares all reserve numerics PLACEHOLDER pending W7. §9.4 simultaneously locks $25k incident / $100k aggregate caps — creating a de facto minimum capital exposure W7 hasn't validated. Treat the §9.4 caps as provisional until W7. Add explicit W7 floor model (cap exposure + deductible buffer + legal-defense floor + migration reserve + dispute reserve + insurance premium). Define A-W5-9 action if need exceeds +20% tolerance (terminate / raise / lower caps / narrow MVP / inventory pivot).

**M4-Rev1 (§9.3, §9.7).** Anti-avoidance of membership-interest / beneficial-ownership transfers is contractually written but not technically monitorable — FinCEN BOI is not externally accessible; private LLC transfers are unobservable. Treat as contractual-only. Require: annual + event-driven owner certifications, operating-agreement / trust restrictions prohibiting transfer without platform consent, beneficial-owner disclosure at onboarding + annual refresh, audit rights, payout suspension for non-certification.

**M5-Rev1 (§9.7).** "Assessed value > $25k" bright line is undefined. Estibot, GoDaddy appraisal, broker opinion, and platform internal valuation diverge by order-of-magnitude. Define valuation method (independent broker opinion / latest bona fide offer / platform schedule by surname rank / acquisition cost / highest-of), or shift the entity requirement to be tier/rank-based, not dollar-appraisal-based.

**M6-Rev1 (§9.8).** Levenshtein-distance-2 surname rule is the wrong equivalence test. `johnson.com` → `johnston.com` (L=2) qualifies; `jones.com` → `jameson.com` (L=4) does not, despite arguably weaker phonetic similarity. Replace with composite: phonetic match (Soundex/Metaphone) + surname-frequency / cultural-origin match + manual approval + renter refusal right retained. Clarify whether equivalent destination must be platform-owned reserved inventory or can depend on another private owner (the latter reintroduces owner-side dependency).

**M7-Rev1 (§9.10 ↔ W1/W2).** US-only MVP creates validation contamination unless W1 LP filters traffic and W2 outreach is updated. Add US billing/residency disclosure to LP before deposit; segment LP metrics by US eligibility; update W2 outreach to exclude non-US owners without US-entity / W-9 capability; reconcile prior Spanish-language outreach with US-only eligibility.

**M8-Rev1 (§9.11).** Freeze triggers (K-W5-3a/3b/3c) lack exit criteria — review owner, deadline, required evidence, possible outcomes, conditions to resume, and whether the 30%→20% cap reduction is temporary or permanent. Without exit criteria, one early incident in a 5–10 domain MVP can freeze onboarding indefinitely (accidental shutdown path).

**M9-Rev1 (§9.12).** Launch blockers need critical-path sequencing, not a flat checklist. Dependencies: registrar feasibility → DNS/control model → sale-enforcement legal memo → Stripe/banking confirmation → insurance quote → reserve model → W7 go/no-go. Mark "must-resolve-first" blockers (those that can invalidate downstream spend).

**M10-Rev1 (§9.13).** Counsel budget bands likely understate novel-question work — registrar/ICANN $2–4k, sale-proceeds escrow / UCC-1 $1–3k, reserve / bankruptcy-remoteness $2–4k, payments / MSB $4–8k. These are opinion-like analyses, not template edits. Obtain fixed-fee or capped quotes before treating $50k as a planning number; add a $75–100k high-case to W7 sensitivity; sequence must-resolve-first opinions before full ToS / lease drafting.

**M11-Rev1 (§9.4, A-W5-3).** Insurance deductible contingency missing. If the broker quote returns $50k or $100k deductible (common at startup scale for Cyber + Tech E&O), or excludes customer intentional acts / spam / phishing / contractual indemnity, the §9.4 cap-deductible alignment breaks. Add explicit branches feeding into W7 reserve and go/no-go.

**M12-Rev1 (§9.14).** "Successful W6 pass without finding a structural exploit" is unrealistic — W6's purpose is to find exploits. Replace with severity-based closure: no unresolved Blocking findings, all High findings either mitigated or explicitly accepted by W7, reserve/capital impact modeled, customer-facing disclosures updated.

### §10.3 Minor findings

- **§9.3 encumbrance trigger may be self-referential.** If the platform itself files a UCC-1, that arguably triggers the "any encumbrance, lien, security interest, or pledge" Change-of-Control clause. Add carve-out: "other than platform-approved or platform-held security interests created under this lease."
- **§9.5 owner bond dispute risk not modeled.** A $500 card/ACH bond can be charged back; platform may lose the bond and still owe adjudicator/renter compensation. Model bond collectability as uncertain unless collected by ACH with explicit authorization, offset against owner payouts, or held through a real escrow/payment flow.
- **§9.6 "FBO without formal trust" may overstate insolvency protection.** Renter-facing language should remain conservative ("asserted as customer-benefit funds") until bank/counsel confirmation exists; do not imply bankruptcy remoteness pre-confirmation.

### §10.4 Verdict and Rev-2 plan

**Verdict: MAJOR-REWORK.** Rev-1 introduced 5 new blockers and 12 mediums. The most important new issue is **B5-Rev1**, which re-introduces a W4 architecture conflict (the platform cannot throttle Gmail send-as outbound) — this is not just a W5 issue but an inter-workshop consistency failure that the Rev-1 pass should have caught.

**Rev-2 work plan (next, before W6 opens):**
1. Re-architect §9.5 (and dependent §9.4 outbound-volume references) using W4-correct controls — freeze send-as config / suspend alias / pause inbound / terminate slot. Inter-workshop consistency check.
2. Convert §9.1 from candidate-registrar list to a binary architecture gate; specify Model A/B/C for apex DNS authority; choose detection cadence consistent with control reliance.
3. Reframe §9.3 deterrence claims by domain-value band; add seasoning-abuse exclusions; size Bonded Premium liquidated damages to value, not renter count.
4. Promote LB-W5-9 to a binary gate with named fallbacks if domain-security perfection is unavailable.
5. Mark §9.4 caps "provisional pending W7"; build the W7 reserve floor model in §9.2.
6. Operationalize commercial-use AUP with examples / non-examples (M1-Rev1).
7. Update remaining mediums (Stripe/bank primitives wording; LLC-monitoring as contractual; valuation method; phonetic distance; W1/W2 US-only reconciliation; freeze exit criteria; launch-blocker critical path; counsel budget high-case; insurance deductible branches; §9.14 closure rewording).
8. Update assumption register and shutdown criteria for any Rev-2 changes.

**Status:** Rev-1 remains the controlling layer until Rev-2 is committed. Findings recorded above are the input set for Rev-2.

---

*End of W5 §10 (Rev-1 Rubber-Duck Findings) — 2026-04-27.*
