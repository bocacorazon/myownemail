# Continuity Workshop: Rug-Pull Protection, Escrow, Renter Migration & Regulatory Posture

**Date:** 2026-04-27 (v0 initial draft — **major rework pending** per rubber-duck findings)
**Facilitator Input:** Legal & Operations Expert (lead), Trust & Safety Architect, Marketplace Economics Analyst, Domain Owner / Supply Advocate
**Status:** **v0 Draft — not locked. Major rework pending.** A rubber-duck pass on this draft (2026-04-27) returned a MAJOR-REWORK verdict with 5 blocking findings and 8 medium findings. See §8 below. None of the design decisions in this document should be treated as locked until Rev-1 addresses the blockers (registrar/DNS control enforceability, reserve reconciliation against Rev-2 economics, sale-escape enforcement mechanism, indemnification/insurance reality check, and dispute-default safe-mode redesign).

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

1. **Registrar-control model: "Owner-controlled, platform-monitored."** The platform never holds the registrar account. The owner retains full domain control at their existing registrar. Platform integrates via DNS records (SPF, DKIM, DMARC, MX) which the owner authorizes us to manage via NS delegation **on a subdomain** (`mail.<domain>`) where structurally possible, or via direct record management with TOTP-protected change auditing. Inherited and reaffirmed from W2 §2j.
2. **Two-tier domain product.** **Premium tier** (sale-free, full-term commitment, signed lease, no sale-escape) and **Standard / Sale-Escapable tier** (sale-escape clause permitted, must be disclosed at signup, capped at ≤ 30% of live inventory). Renter pricing reflects the risk asymmetry (Premium-tier renter slots can carry a small premium; documented under K-W5-1 below).
3. **Renter Protection Guarantee (RPG)** — locked, customer-facing:
   - **Minimum 90-day notice** before any planned domain withdrawal (sale, lease termination, owner exit). For Premium-tier renters: 180 days.
   - **Migration assistance** — concierge-grade handoff to an alternate surname domain (where available) or to a personal-domain setup ($15 ICANN registration credit + free 3-month forwarding-only setup).
   - **Pro-rated refund** for unused term, plus a **migration credit** (1 month of equivalent service) if migration is involuntary.
   - **No surprise withdrawals** outside RBL-pause emergencies — emergency carve-out spelled out separately.
4. **Reserve & escrow architecture** (locked at the structural level; numeric tuning open):
   - **10% rolling reserve** on all owner payouts for first 180 days of each domain's listing (per W2 §2j item 7).
   - **Migration reserve fund** at platform level: $X/renter-month accrued into a segregated account, sized per K-W5-2.
   - **Stripe Connect Custom** flow holds funds 7 days minimum before payout to owner; chargeback window extends this to 90 days for first-time owners.
   - **Indemnification reserve** (W4 hand-off): platform-side reserve to absorb impersonation/blacklist harms below stated caps; above caps, push-to-renter via ToS + insurance backstop.
5. **Regulatory posture (locked positioning, external counsel sign-off pending):**
   - US Delaware C-corp; California operating presence assumed for tax-nexus modeling.
   - **CAN-SPAM:** platform is a "sender" or "service provider" for inbound forwarding only; renters are senders for outbound (their Gmail/bridge). ToS push to renters; no commercial-bulk-mail authorization on rented addresses (enforced by §2.1 below).
   - **GDPR / UK GDPR / CCPA / CPRA / state privacy:** platform is data controller for renter PII (name, payment, ID-verification result), data processor for inbound forwarded mail content (transit only, no storage beyond logs). DPA template required per renter; SCCs for non-EU platform processing.
   - **Trademark / impersonation:** mandatory ID-verification at signup (W4 §2.5.2) provides a registrant-of-record identity; same-domain impersonation (W4 §2.5.3) handled by canonicalization spec + complaint takedown (UDRP-adjacent process internally; no claim of UDRP equivalence).
   - **Money transmitter:** the 60/40 split processed via Stripe Connect Custom is structured to keep us **outside money-transmitter classification** in all 50 states (Stripe is the regulated party, we are a marketplace facilitator). External counsel must confirm.
   - **Sales tax / marketplace tax:** SaaS-tax states (currently ~20+) require collection on rentals at the renter side; platform collects and remits. Owner side is service-revenue (1099-K threshold tracking).
6. **Sale-escape clause structure (W2 hand-off, locked at design level pending counsel):** owner option to pull on bona-fide third-party offer ≥ floor price, 180-day notice, owner pays exit fee into migration reserve, capped at ≤ 30% of live inventory (per W2 §2k(iv)). External counsel must confirm enforceability and absence of UCC Article 2 / consumer-product implications.

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

**Scenario:** A domain owner asserts that a renter's behavior is damaging their domain (commercial mail blowback, disputed content, third-party complaints to the owner directly). Forwarding logs may or may not corroborate.

**Resolution path (locked):**

1. **Tier 0: ops review.** Ops reviews forwarding logs, Mailgun complaint data, RBL status. If there is clear evidence of renter AUP violation → renter Tier-2/3 path per W4 §Abuse Escalation. If clear no-evidence → owner notified; resolution to non-action with explanation.
2. **Tier 1: ambiguous evidence.** If logs are ambiguous (no Mailgun complaints, no RBL listing, but owner reports third-party complaints reaching them), invoke a 14-day investigation window. Renter forwarding continues unless the owner posts a $500 good-faith bond against frivolous complaint.
3. **Tier 2: contested adjudication.** If after Tier-1 the dispute remains unresolved, escalate to the **Adjudicator of Record**. MVP default: in-house Tier-3 review (founder + counsel of record). Post-MVP: third-party arbitration vendor (e.g., NAM, AAA) with marketplace experience. Adjudicator decision is binding under both contracts (renter ToS arbitration clause; owner lease arbitration clause).
4. **Outcome paths.** (a) Renter found in violation → Tier 2/3 abuse path per W4. (b) Owner found vexatious → bond forfeit to renter; platform note on owner record; second offense raises owner-side reserve to 25% indefinitely. (c) Genuine ambiguity → renter migrates to alternate domain at platform expense; owner not penalized.

**Defaults during dispute:** the renter's slot remains active unless ops has independent abuse evidence. We do not pause renters on owner accusation alone — that creates a structural eviction lever for owners who decide they don't like a renter.

### 1.6 Indemnification Architecture (W4 launch blocker resolution)

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

The drop-catching pool (W2 A-W2-14, W3 §2b-bis) doubles as the migration-destination pool. Implication: when a renter on `johnson.com` migrates to platform-owned `johnston.com`, the platform is the *owner* of the migration target — there is no second owner relationship to manage, no sale-escape risk, and a 100% gross-margin renter slot. Net effect: migration cost decreases for migrations into owned inventory; the owned-inventory class becomes structurally important not just for economics (W3) but for continuity insurance.

---

## §3. Marketplace Economics Analyst — Secondary Review

### 3.1 Reserve Sizing

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

A rubber-duck critique was run against this v0 draft on 2026-04-27. **Verdict: MAJOR-REWORK.** The findings below must be resolved (or explicitly accepted-with-rationale) in a Rev-1 pass before any element of W5 is treated as locked. None of the v0 design decisions above survive into W6/W7 as locked until that pass completes.

### §8.1 Blocking findings (must resolve in Rev-1)

**B1. Registrar/DNS control model is not enforceable.** Lease clauses cannot stop an owner from changing nameservers, removing apex MX, transferring the domain, or letting it expire. Also a technical bug: the proposed `mail.<domain>` NS delegation does not give the platform control over `@domain.com` email (apex MX + apex DKIM/DMARC selectors required). Rev-1 must specify a real control architecture: registrar transfer-lock + registry lock, platform-visible auto-renew status, contractual platform-paid-renewal-with-recoupment right, apex-DNS authority sufficient for `@domain.com`, and for Premium either escrowed registrar access or downgrade "sale-free" → "enhanced notice + damages-backed best-efforts."

**B2. W5 reserve burden ($74–82k/yr at Y2 ceiling) likely breaks Rev-2 economics and is not reconciled.** Rev-2 central case is already tight (~$245k max drawdown, breakeven month 48–52). The v0 draft also confuses *annual expected loss* with *balance-sheet target reserve*, and may double-count Rev-2's existing abuse and sale-escape lines while under-accounting legal-defense cash needs. Rev-1 must (a) separate balance-sheet target vs. annual expected loss, (b) build per-incident-type EV loss model, (c) compute per-renter/month cost impact by tier, (d) update capital requirement under base + 1 major migration event + 1 indemnity claim hitting deductible, and (e) make an explicit pricing/share/inventory/capital decision. This work belongs in W7 reconciliation; until done, all reserve numbers in §3.1 are placeholders.

**B3. Sale-escape and Premium "sale-free" are soft promises without enforcement.** No anti-avoidance against LLC-membership-interest sale; no seasoning period; exit fee is rounding error vs. high-value sales (50 renters × $500 = $25k, weak vs. six-figure flips); only $2.5–7.5k at early liquidity. RoFR was rejected without an alternative escrow/buyer-assumption mechanism. Rev-1 must add: (a) anti-avoidance clauses (asset sale, equity sale, change of control, beneficial-ownership transfer, registrar transfer, DNS transfer, encumbrances), (b) 12-month seasoning, (c) exit fee = greater-of {per-renter, months-of-gross-revenue, % of sale proceeds above floor}, (d) sale-proceeds escrow or broker closing instructions, (e) for Premium either registrar-level escrow or relabeling away from "sale-free."

**B4. Indemnification/insurance structure relies on coverage and collectability that may not exist.** $5k incident cap sits *below* the modeled $25k insurance deductible, so insurance never responds to capped incidents. Cyber/Tech E&O policies typically exclude intentional acts of insureds' customers — exactly the spam/impersonation/phishing cases the platform claims to indemnify. Pushing above-cap losses to consumer renters via "renter's-insurance requirement" is unrealistic and uncollectible at the price point. Rev-1 must (a) get broker quotes covering email-abuse/spam/phishing exclusions, defense-costs treatment, contractual-indemnity coverage, (b) align platform caps with deductible reality (a $5k self-insured cap is *not* insurance-backed), (c) replace "renter's insurance requirement" with a realistic collectability model assuming consumer-renter recovery ≈ 0, (d) decide whether business/commercial use is fully banned (not merely excluded from indemnity). Insurance binder + coverage summary reviewed by counsel becomes a hard launch blocker.

**B5. Dispute default ("renter active unless independent evidence") creates a Gmail-send-as abuse window.** This conflicts with W4's already-reactive complaint-driven posture, and the $500 owner bond's procedural effect is not actually defined (does posting it pause the renter? accelerate review? buy adjudicator deposit?). Rev-1 must replace binary "active vs. suspended" with graduated safe-mode: (a) Tier-1 ambiguous owner complaint → throttle forwarding, freeze send-as setup changes, increase logging, 72h triage deadline (not 14 days); (b) define exactly what owner bond buys procedurally; (c) make bond symmetrical (renter contesting may post smaller deposit); (d) emergency exception for credible third-party complaint evidence.

### §8.2 Medium findings (resolve in Rev-1 or schedule into W6/W7)

**M1. Stripe Connect / money-transmitter posture is conclusory.** Connect Custom + owner reserves + migration reserves + indemnification reserves + payout-timing discretion can look like funds control, not pure marketplace facilitation. Counsel memo + Stripe written confirmation required, covering merchant of record, payout-timing control, reserve-holding location, commingling, state-by-state treatment for NY/CA/TX/FL.

**M2. Reserve commingling and bankruptcy-remoteness are not specified.** "Segregated account" is undefined — separate bank? trust? bankruptcy-remote restricted cash? operating-account ledger entry? Rev-1 needs a reserve architecture appendix covering insolvency priority, draw approvals, and whether owner rolling reserves are owner funds or platform funds.

**M3. GDPR controller/processor split is likely oversimplified.** Forwarded email content contains third-party (sender) PII; spam filtering, abuse detection, quarantine, legal holds, complaint adjudication all involve platform determining purpose/means → controller activities, not processor. Privacy counsel must classify each data flow and decide whether EU/UK traffic is excluded from MVP.

**M4. Sister-domain pool is overloaded** with four conflicting functions (revenue inventory, migration insurance, drop-catch experiment, displacement fallback). Separate "revenue owned inventory" / "reserved migration inventory (priced as insurance)" / "emergency non-equivalent migration path"; define target spare capacity and surname-distance rules; if no equivalent destination exists, RPG should say so plainly.

**M5. K-W5 thresholds are not actionable enough.** K-W5-3's 5/100-domain-yrs trigger waits for many customer failures before "architecture review" (a non-action). Add early absolute triggers: first owner-initiated rug-pull in first 12 months → freeze new Standard sale-escapable onboarding; any Premium owner attempted sale → suspend Premium claims; any rug-pull affecting >25 renters → immediate W7 reforecast. Replace "architecture review" with explicit actions (suspend supply, require registrar escrow, raise exit fees, reduce Standard cap, reprice reserves).

**M6. $15–35k counsel budget is likely understated** and missing categories: privacy DPA/SCC package, payments/MSB specialist, tax/sales-tax/VAT, registrar/ICANN counsel, insurance coverage review, owner KYC/W-9/1099 workflow, probate/successor-contact playbook, foreign-owner exclusion-or-policy decision. Rev-1 must turn A-W5-1 into a quoted workplan with named counsel categories and hard budget bands; if quoted pre-build legal exceeds the envelope, that feeds W7 capital and go/no-go.

**M7. Owner death/incapacity plan is contractual not operational.** A lease clause does not guarantee registrar access after death (probate, locked accounts, expired payment cards, foreign jurisdictions). Rev-1: require successor contact at onboarding, auto-renew enabled and verified annually, platform emergency renewal right where registrar permits, consider LLC/trust ownership for high-value Premium domains, define 7/14/30-day estate-non-response escalation, exclude solo-owner foreign domains from MVP.

**M8. Cross-border owner/renter scope is inconsistent.** W2 explicitly recommended US owners + US renters only for MVP; W5 v0 analyzes GDPR/UK GDPR/SCCs/EU DSA as if EU traffic may exist. Rev-1 must make a hard MVP scope decision: Option A (US-only — block EU/UK signups, simplify W5) or Option B (international from day one — GDPR/DPA/SCC become launch blockers). Recommend Option A to align with W2.

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
