# Deliverability Workshop: Abuse Prevention & MVP Email Architecture

**Date:** 2026-04-27 (Rev-2.2 — sending-bridge dependency) — Rev-2.1 rubber-duck pass 2026-04-27; Rev-2 alignment 2026-04-26; Original draft 2026-04-21
**Facilitator Input:** Trust & Safety Architect, Legal & Operations Expert, Red Teamer
**Status:** **Conditionally locked.** Forwarding-only is the MVP architecture for design purposes. Six hard gates must clear before MVP build, including a pre-build technical proof on Gmail send-as deliverability and a cost-stack reconciliation against Rev-2.

> ### ✅ Rev-2 Alignment Notice (2026-04-26) — Updated 2026-04-27 (Rev-2.1) — Updated 2026-04-27 (Rev-2.2)
>
> This workshop has been revised against the now-locked offer:
>
> - **W1 (Demand) closed**: Surname-Match `.com` ICP, "Claim your name" frame, two-tier pricing (Premium $25 single-name / Standard $9 compound).
> - **W2 (Supply) closed**: 60/40 platform-favoring split, Dormant/Resigned holder concierge, exp-1 gating live builds.
> - **W3 (Economics) closed**: 50 renters/domain at steady state, blended ARPU ~$11, $245k capital plan.
> - **Rev-2 (Pricing & Namespace) closed**: compound local-parts admitted, 50–80 renter capacity per top-100 surname domain, abuse reserve and ops cost stack adjusted.
>
> **What changed for W4 vs. the 2026-04-21 draft (Rev-2 alignment, 2026-04-26):**
>
> 1. **Forwarding-only is no longer provisional** as an architectural *direction*. W1 §2c validated it against the Surname-Match ICP ("recipients never see the plumbing; renter sends via Gmail"); Rev-2 §1 explicitly keeps it. Rev-2.1 narrows the lock: `A-pre-1` is **conditionally locked** pending send-as deliverability proof (see Gate 0 below).
> 2. **Per-domain capacity is 50 renters, not 25.** Blast radius doubles. All capacity, abuse-reserve, and migration-reserve sizing in this workshop is rebased.
> 3. **Compound slots create new abuse surfaces.** Squatting, cheaper abuse-ring economics, and same-domain impersonation are first-class concerns now. New §2.5 below.
> 4. **Rev-2 §8 hard gates are absorbed into this workshop.** Compound tier does not ship without (i) automated daily blacklist monitoring, (ii) standard-tier *forwarding throughput* limit at 200/day (not 500/day), (iii) ID verification at signup, (iv) non-waivable $25 onboarding fee, (v) 3-slot-per-person-per-domain cap with 20% surcharge on slots 2+. These are **non-negotiable**.
> 5. **K-W4 numeric kill criteria are now defined.** K-W4-1 (blacklist incident rate) lifts and locks K-Rev2-3 from the Rev-2 doc; K-W4-2a/b/c split (Tier 1 false-positive, confirmed forwarding abuse, send-as complaint) and K-W4-3 (ID-verification post-hoc abuse rate) are new.
>
> **What changed in Rev-2.1 (rubber-duck pass, 2026-04-27):**
>
> - **Added Gate 0: Pre-MVP send-as deliverability proof.** Empirical test that consumer Gmail send-as on a non-Google `.com` domain produces clean SPF/DKIM/DMARC alignment with no visible "via gmail.com" sender mismatch across major recipient providers (Gmail, Outlook, Yahoo, Apple Mail, Microsoft 365). Without this, forwarding-only is not viable and W3 economics reopen.
> - **Renamed "outbound rate limit" → "forwarding throughput limit."** The platform never sees Gmail send-as outbound traffic; the 200/day cap binds on *inbound forwarding throughput*, not on actual Gmail outbound. Send-as abuse is bounded by Gmail's own systems plus our complaint-driven response, not by platform rate limiting.
> - **Added Mailgun forwarding-reputation controls.** Forwarding inbound mail to Gmail *is* outbound mail from Mailgun; renter list-bombing or reputation contamination affects platform deliverability across domains. New controls: per-risk-cohort sending pools (if Mailgun supports), bounce/complaint/throttle monitoring, list-bomb detection, suppression handling. Mailgun AUP review is now a **pre-launch blocker**, not a W6 follow-up.
> - **Reconciled W4 staffing against Rev-2 §2i opex.** 2.0 FTE was the Y2-ceiling number, not Y1. Y1 ramp is **0.5 FTE Y1 → 1.0 FTE Y2 → 2.0 FTE at the 2,500-renter ceiling**. Most of this fits Rev-2 §2i fixed opex with a small uplift (see §Legal & Operations).
> - **Recalibrated abuse-ring economics.** With 3 slots/ID/domain, a 50-slot ring needs ~17 IDs, not 50; identity-cost band corrected from $2,500–$10,000 to ~$850–$3,400 (still material on top of $1,250 onboarding fees + $450/mo recurring).
> - **Downgraded inbound footer disclosure.** Footer is a transparency measure to inbound recipients; it does **not** reach Gmail send-as targets and is not a primary impersonation control.
> - **Added leading-indicator monitoring spec** alongside daily RBL polling (RBL listing is often *the* event, not a 24h-early warning). Added Mailgun complaints, DMARC aggregate reports, inbound spike anomalies.
> - **Split K-W4-2** into Tier 1 false-positive rate (UX risk), confirmed forwarding-abuse rate, and send-as complaint rate. Replaced K-W4-3 false-pass measure with observable post-hoc proxies (chargeback rate, near-duplicate identity rate, confirmed abuse among ID-verified cohort).
> - **Re-classified some W5/W6 hand-offs as MVP launch blockers.** Provider AUP compatibility (Gmail, Mailgun, Stripe Connect), indemnification structure for blacklist + impersonation harms, and owner-pull-during-incident protocol are blocking, not deferrable.
>
> **What changed in Rev-2.2 (sending-bridge dependency, 2026-04-27):**
>
> - **Recognized that consumer "send-as via external SMTP" is essentially a Gmail-only feature.** Outlook.com / Hotmail deprecated external-SMTP "send-as" / "Connected accounts" for consumer users in 2023; aliases are restricted to Microsoft-owned domains. Yahoo Mail does not support external-SMTP send-as on free or paid tiers; aliases are restricted to Yahoo-owned domains. Apple iCloud Mail and Microsoft 365 support custom domains only when the *user's own account/tenant* owns the domain — not workable on a shared/rented domain. Fastmail supports external send-as; Proton requires domain ownership. **Net effect:** to *reply as* `bill@johnson.com`, a non-Gmail user today must either (a) open a free Gmail account as a sending bridge or (b) use Fastmail. The "use your existing mailbox" pitch is functionally Gmail-native for the bulk of US consumers.
> - **Inbound forwarding is unaffected** — any mailbox can *receive* forwarded mail. The dependency is on outbound *sending* identity.
> - **Added §2.7 Sending-Bridge Dependency** (new section). Documents the cross-provider compatibility matrix, the Gmail-bridge fallback path, the "first-party send endpoint" question (which would re-open W4's outbound abuse model), and the mitigations.
> - **Added A-W4-8** (assumption register, launch-blocking): ≥ 70% of the Surname-Match ICP either uses Gmail today or will accept a free-Gmail sending bridge as a setup step. Coupled to **K-W4-6** in the kill-criteria ledger (LP-measured Gmail penetration in the ICP, plus concierge-MVP bridge-acceptance rate).
> - **W1 LP-test instrumentation update** (cross-cutting, doc 05 §2g experiment 2): the email-capture form now asks "what's your primary email today?" with provider buckets, so we measure ICP Gmail penetration directly rather than relying on US-population priors. Free instrumentation; meaningful data even at low LP volume.
> - **Gate 0 scope clarified.** Gate 0 already tests *recipient-side* deliverability across major providers (Gmail/Outlook/Yahoo/Apple/M365 as receivers). Rev-2.2 adds a sibling concern about *sender-side* bridge availability, which is a market/ICP question, not a deliverability question — handled in §2.7, not folded into Gate 0.
>
> **Assumptions still standing post-Rev-2.1 (formalized in `_assumption_register.md` as A-W4-1 through A-W4-7):**
>
> - Target renters tolerate forwarding-only because the architecture is invisible to recipients (W1 §2c). **Conditional on Gate 0.**
> - Gmail send-as setup friction is acceptable to the Surname-Match ICP (concierge MVP will confirm).
> - Mailgun, Gmail, and Stripe Connect AUPs remain policy-compatible (now a **pre-launch blocker**, not a long-term-only risk).
> - Daily RBL monitoring + leading-indicator stack provides sufficient detection lead time to pause forwarding before broad recipient-side impact.
> - ID verification at signup (vs. phone-only) reduces abuse-ring economics enough to make the standard-tier price point defensible.
> - Mailgun forwarding reputation can be isolated (or sufficiently quarantined) so that renter-induced contamination does not cascade across domains. **Pre-launch test required.**

---

## Executive Summary

### Problem Statement
The core risk of the marketplace is **domain reputation collapse**: if one renter sends spam or phishing, the entire domain (and all other renters' addresses) gets blacklisted. Under Rev-2 namespace expansion, a single blacklisted domain affects up to 50 innocent renters — 2.5× the W3 baseline.

### Locked MVP Architecture
**Forwarding-only with Gmail Send-As (W1 §2c, Rev-2 §1):**
- **Inbound:** Platform receives mail, forwards to renter's Gmail (or equivalent client supporting send-as).
- **Outbound:** Renter sends via Gmail's infrastructure (not platform-controlled). **Conditional on Gate 0 deliverability proof** — see below.
- **Benefit (qualified):** Domain reputation isolated from renter *outbound* sending; platform does not run outbound SMTP for renter mail. Note that Mailgun *forwarding* mail to renters' Gmail mailboxes is itself outbound from Mailgun's perspective; renter list-bombing or feedback-loop complaints can still degrade Mailgun-side reputation. See §2.6 Mailgun Forwarding Reputation Controls.

### Rev-2 Hard Gates (compound tier does not ship without all six)
0. **(Rev-2.1) Pre-MVP send-as deliverability proof.** Empirical test: a renter using Gmail send-as on a non-Google `.com` domain (with our SPF + DKIM + DMARC records) must reach inbox at Gmail, Outlook, Yahoo, Apple Mail, and Microsoft 365 with no "via gmail.com" sender mismatch and no DMARC quarantine/reject in aggregate reports. **Failing this test invalidates A-pre-1 and reopens W3 economics.**
1. **Automated daily blacklist monitoring** across SpamHaus, SORBS, and Barracuda (per Rev-2 §8.4), plus leading indicators (Mailgun complaint/bounce rates, DMARC aggregate reports, inbound spike anomalies) — see §Abuse Monitoring.
2. **Forwarding throughput limits**: 200 forwards/day on Standard tier, 500/day on Premium tier (Rev-2 §8 tightening of 2026-04-21 draft's 500/day blanket). Note: this caps *platform-mediated forwarding*, not Gmail send-as outbound; send-as abuse is bounded by Gmail's own systems plus our complaint-driven response (see §Send-As Outbound Abuse Monitoring).
3. **ID verification at signup** (not phone-only), retained even on free trial.
4. **Non-waivable $25 onboarding fee** as primary economic filter on abuse rings (Rev-2 §8.3).
5. **Compound-slot policy caps**: 3 slots/person/domain max; 20% surcharge on slots 2+; impersonation/display-name rules per §2.5.

### Risk Assessment (Rev-2 rebaseline)
| Dimension | Risk Level | Confidence | Δ vs. 2026-04-21 |
|-----------|-----------|-----------|------------------|
| Domain reputation protection | MEDIUM | 85% | unchanged (50-renter blast radius offset by tighter rate limits + ID verification) |
| Operational enforcement | LOW–MEDIUM | 85% | bumped from LOW: ID verification adds onboarding load |
| Legal enforceability | LOW | 80% | unchanged |
| Residual abuse loops | MEDIUM | 70% | unchanged (compound-slot ring economics counterbalanced by $25 fee + ID + 200/day) |
| **Compound-slot impersonation (new)** | **MEDIUM** | **65%** | new — display-name policy is partial control |

---

## Trust & Safety Architect Memo

### The Strongest Version of the Problem

**Domain reputation is a shared resource with individual abuse exposure:**

1. **Spam/phishing from one renter taints the domain for all.**
   - If `bad-actor@johnson.com` sends phishing, SpamHaus blacklists `johnson.com` MX.
   - Result: Legitimate users (`bill@johnson.com`, `jane@johnson.com`) cannot send/receive mail.

2. **No technical isolation at DNS/MX layer.**
   - Once mail enters `johnson.com` MX, there is no per-user routing at the DNS layer.
   - The domain either works for all, or fails for all.

3. **Renter incentive is misaligned with domain protection.**
   - Renter wants max outbound sending (to send newsletters, marketing, etc.).
   - Domain owner wants minimal outbound (to protect reputation).
   - Platform has no built-in way to arbitrate this.

4. **ISP reputation monitoring is opaque.**
   - We don't know when `johnson.com` is about to be blacklisted until it already happens.
   - By then, legitimate renters are already harmed.

### Proposed T&S Solution: Forwarding-Only MVP

**Architecture:**
- **Inbound flow:** Renter receives mail at `bill@johnson.com` → platform forwards to renter's personal Gmail → renter reads in Gmail
- **Outbound flow:** Renter sends via Gmail's interface using send-as alias. Mail goes through Gmail's SMTP (not platform's).
- **Key benefit:** Platform receives mail but never sends it. Gmail's infrastructure bears the reputation risk for outbound. Platform is "delivery-only," not "SMTP provider."

**Why this works:**
1. Renter sending via Gmail uses Gmail's established IP reputation (billions of users already benefit from this).
2. Platform cannot be blamed for outbound quality (renter owns that interaction).
3. If a renter sends phishing via Gmail, Gmail's abuse controls kick in, not the domain owner's.
4. Domain remains "clean" because inbound is the only platform responsibility, and inbound abuse is detectable and preventable.

### Onboarding & Verification (Rev-2: ID verification mandatory)

**Identity & Risk Assessment:**
- Email address (must be valid; Mailgun will verify)
- Phone number (TOTP challenge; detects bot rings; partial defense against multi-accounting)
- **Government-issued ID verification** (Rev-2 §8 hard gate). Vendor candidates: Stripe Identity, Persona, Veriff. Estimated cost $1.00–$1.50 per verified renter; one-time at signup. Already absorbed in Rev-2 §3.1 cost stack.
- **Non-waivable $25 onboarding fee** (Rev-2 §8.3). The fee is the primary economic filter on disposable-identity abuse rings; do **not** waive it for promotions, referrals, or trial conversions.
- Domain owner opt-in approval (domain owner reviews renter before activation on premium single-name slots; auto-approve permitted on standard compound slots if no owner-set blocklist applies).

**Rationale (Rev-2 update):**
- Email + phone alone is too weak under Rev-2 economics: $9 standard slots + VoIP phones = $450/mo to set up a 50-account ring (Rev-2 §8.3). ID verification raises the cost of identity acquisition by 10×+ and makes the per-account margin unattractive for spam.
- ID verification is not a brand asset of the platform (it is friction); it is justified strictly by abuse defense and is invisible to recipients.
- Domain owner opt-in remains the secondary filter; required for premium slots, optional for standard.

### Forwarding Throughput Limits (Rev-2: tier-differentiated, tightened; Rev-2.1: scope clarified)

**Per-renter daily *forwarding* limits** (mail moving through the platform → renter's Gmail):
- **Standard tier (compound slot)**: 200 forwards/day (Rev-2 §8 hard gate; tightened from 2026-04-21 draft's 500/day)
- **Premium tier (single-name slot)**: 500 forwards/day (unchanged; identity-grade renters with higher commitment and lower abuse probability per Rev-2 §3.1)
- **Hard monthly caps**: 3,000/month standard, 8,000/month premium (catches seasonal abuse; legitimate identity-email use is well under these)

**Inbound forwarding (uncapped but monitored):**
- No hard limit on inbound; spike detection at 5× rolling 30-day baseline triggers Tier 1 review.
- Mailgun spam/phishing scoring applied before forwarding; high-score mail quarantined for renter review.

**Scope clarification (Rev-2.1):**
- These limits bind on **platform-mediated forwarding throughput** — i.e., mail Mailgun receives at the rented domain and forwards to the renter's personal Gmail. They do **not** bind on Gmail send-as outbound (which leaves directly via the renter's Gmail account; the platform has no visibility or control).
- Standard-tier 200/day is well above legitimate identity use (median ~10 inbound forwards/day; 95th-percentile ~50/day in comparable consumer-email patterns) but bounds list-bombing, mass-subscribe, and inbound abuse.
- Premium-tier 500/day preserves headroom for legitimate edge cases (small-business operators, prolific networkers); their higher cost ($25/mo + $25 onboarding) plus lower abuse correlation justifies the wider band.

### Send-As Outbound Abuse Monitoring (Rev-2.1, new)

The platform cannot rate-limit Gmail send-as outbound directly. Outbound abuse via send-as is bounded by:

1. **Gmail's own anti-abuse systems** (account-level rate limits, content scanning, phishing detection on send) — out of platform control but a real ceiling on volume.
2. **Complaint links in inbound footer** (`report@platform`) for inbound recipients of forwarded mail. Note: footer disclosure does not reach send-as outbound recipients; it is a transparency tool for *inbound* mail only.
3. **Recipient-feedback channels we register for**: Gmail Postmaster Tools (DMARC aggregate reports for our domains), abuse@ inboxes on each rented domain monitored daily, third-party abuse-report routing (e.g., abuse.net registration).
4. **Annual destination re-verification**: each renter must re-confirm their Gmail destination address annually (TOTP + email round-trip), to catch dormant accounts being repurposed for abuse rings.
5. **Alias suspension on confirmed send-as abuse**: when complaints, DMARC aggregate evidence, or recipient reports confirm a renter is sending abusive mail via send-as, we revoke their send-as setup token (Gmail clears the alias on next refresh) and pause forwarding. This is a **complaint-driven, not preventive**, control — its lead time is recipient-complaint cycle (typically 24–72h after harm).

This is the architectural floor: send-as outbound abuse cannot be prevented platform-side, only detected and responded to. See K-W4-2c (send-as complaint rate kill criterion) and §Limitations.

### Abuse Monitoring & Detection

**Content Filtering:**
- Mailgun will provide SpamAssassin + phishing detection on inbound.
- Flag high-spam-score emails before forwarding; store flagged mail in quarantine for renter review.
- Daily digest to renter: "5 emails were flagged as likely spam; review them here."

**RBL (Realtime Blackhole List) Monitoring + Leading Indicators (Rev-2.1):**

Daily RBL polling alone is **reactive** — by the time a domain lands on SpamHaus/SORBS/Barracuda, recipient-side harm has already begun. Rev-2.1 requires a leading-indicator stack alongside RBL:

- **Daily RBL check** (SpamHaus, SORBS, Barracuda): the floor. Detects existing harm; not an early warning.
- **Mailgun complaint and bounce rates per domain**: feedback-loop complaints from major ISPs typically arrive within 1–6h of harm; complaint rate >0.1% triggers Tier 1 review on that domain.
- **Mailgun hard-bounce + spam-trap rates**: list-bombing or stale-list ingestion produces spikes hours before reputation damage.
- **DMARC aggregate reports** (Gmail Postmaster Tools, Microsoft SNDS): daily ingestion; spike in DMARC failures or quarantine/reject rates is a leading signal of either spoofing or send-as misconfiguration.
- **Inbound forwarding spike anomaly** (>5× rolling 30-day baseline): triggers Tier 1; precedes outbound abuse in many list-bomb scenarios.
- **CRITICAL alert (RBL listing event):** If domain lands on RBL, immediately:
  1. Notify domain owner (within 1 hour)
  2. Pause all forwarding on that domain (prevent further damage)
  3. Investigate which renters caused it (track email volume patterns + content flags)
  4. Escalate to domain owner for action (may need to contact ISP for delisting)

**Renter Abuse Signals:**
- Sudden spike in inbound volume (>5x normal)
- High spam/phishing content scores
- Multiple DMARC/SPF failures (may indicate spoofing attempts)
- Complaints from recipients (if platform implements abuse reporting)

### Abuse Escalation Process (3-Tier)

**Tier 1: Auto-Pause (Automated)**
- Trigger: Standard-tier renter exceeds 200 forwards in 24h, OR Premium-tier renter exceeds 500 forwards in 24h, OR any renter accumulates >10 spam-flagged emails in 24h, OR any renter's domain crosses the 0.1% Mailgun complaint-rate threshold.
- Action: Pause forwarding for that renter for 24 hours. Notify renter + domain owner.
- Renter can appeal (manual review) within 24 hours.

**Tier 2: Suspend (Manual Review)**
- Trigger: Tier 1 pause + repeated violations within 7 days
- Action: Suspend renter for 7 days. Renter must provide written explanation.
- Domain owner can escalate to permanent ban.

**Tier 3: Terminate (Permanent)**
- Trigger: Tier 2 suspension + violations continue OR confirmed phishing/criminal activity
- Action: Revoke renter access. Refund pro-rata subscription fee (if applicable). Ban from platform for 1 year.
- Legal notice to renter (if suspected criminal activity).

### Remaining Risks (Unresolved)

1. **Multi-account abuse rings:** A determined attacker with many phone numbers can bypass identity checks. Mitigation: IP clustering (Year 2 feature). Residual risk: 2–5% of renters.

2. **Phishing account takeover:** If a renter's Gmail is compromised, attacker can send phishing via the renter's send-as alias. Mitigation: Audit trail (track forwarding + send-as activity). Residual risk: 1–3% of accounts.

3. **Domain owner framing:** A domain owner could deliberately send phishing mail as a renter to frame them, or trigger RBL to evict renters. Mitigation: Renter re-verification after serious complaints. Residual risk: 5–10% false suspensions.

4. **ISP reputation lag:** Even with careful renter screening, a domain might land on RBL due to cumulative low-score emails. Mitigation: Daily RBL monitoring. Residual risk: 1–2% of domains/year.

### Required Assumptions

- Mailgun (or similar) reliably detects spam/phishing on inbound flow.
- Domain owners are responsive to RBL alerts and willing to remediate (cooperate with delisting).
- Renters tolerate Rev-2-level onboarding friction (phone TOTP + government ID + $25 onboarding fee). Concierge MVP is the first test of conversion-rate impact.
- ID-verification false-pass rate (synthetic IDs that bypass Stripe Identity / Persona / Veriff) stays ≤ 5% — gated by K-W4-3.
- Platform can sustain a 0.5 → 1.0 → 2.0 FTE T&S ramp aligned to renter-base growth, up to the Rev-2 ceiling of ~2,500 renters (50 live domains × 50 renters). Y2 ceiling staffing requires Rev-2 §2i opex revision (W7 reconciliation item).

---

## §2.5 Compound-Slot Controls (Rev-2 — new section)

Rev-2 admits compound local-parts (`john.paul@`, `mary.anne@`, `j.smith@`, `jp.smith@`) into the namespace at $9/mo standard pricing. This expands per-domain capacity from ~25 to 50–80 renters but introduces three new T&S surfaces this workshop must lock policy on. Rev-2 §8.1–§8.3 framed the risks; this section operationalizes them.

### 2.5.1 Compound-Slot Squatting / Identity Hoarding

**Risk:** A determined renter signs up for `john.smith@`, `j.smith@`, `john.p.smith@`, `johnsmith@`, `jsmith@`, `john.paul.smith@` etc. on `smith.com` — six variants of the same person — and holds them all. Defensive squatting (preventing impersonation of self) is a legitimate use case; offensive hoarding (cornering identity space, reselling) is not.

**Locked policy:**
- **3-slot-per-person-per-domain hard cap.** "Person" is defined by the ID-verification record (legal name + DOB hash). One ID = up to 3 slots on a given domain.
- **20% surcharge on slots 2 and 3** ($10.80/mo each at standard pricing). Discourages frivolous accumulation; doesn't penalize legitimate defensive registration.
- **One single-name premium slot per ID per domain** (no surcharge tier — premium is already scarce).
- **Cap is per-domain, not platform-wide.** "John Smith" can hold 3 slots on `smith.com`, 3 on `johnson.com`, etc. — that's still bounded by ID and by their willingness to pay.

**Acceptable residual risk:** family members or business partners sharing an ID could collude past the cap. Mitigation: deferred to W6 red-team review; not a structural blocker for MVP.

### 2.5.2 Cheaper Abuse-Ring Economics (Rev-2.1 — math corrected)

**Risk:** $9 standard slot × 50 accounts = $450/mo for a 50-account abuse ring on a single domain — 64% cheaper than the all-premium $1,250/mo equivalent (Rev-2 §8.3).

**Locked policy:**
- **$25 non-waivable onboarding fee** stays on every signup, including referrals, promotions, and trial conversions. A 50-slot ring now costs **$1,250 in onboarding fees + $450/mo recurring** — the upfront fee is the binding economic filter.
- **ID verification at signup** raises the cost of identity acquisition. Synthetic-ID services price clean identities at $50–$200 each. With the 3-slot-per-ID-per-domain cap (§2.5.1), a 50-slot ring on one domain needs **~17 distinct verified identities**, not 50: identity cost band is **$850–$3,400** (not the $2,500–$10,000 figure used in the 2026-04-26 draft). Total ring setup: $1,250 onboarding + $850–$3,400 identity = **$2,100–$4,650 upfront**, plus $450/mo recurring. Still material on $9 unit economics, but the abuse-ring cost is roughly 3× lower than the original Rev-2 framing implied. K-W4-2b (confirmed forwarding-abuse rate) is the kill criterion if this floor proves insufficient.
- **Forwarding throughput limit (200/day standard)** caps abuse throughput per ring account on platform-mediated forwarding. Note: this does not bind Gmail send-as outbound (see §Send-As Outbound Abuse Monitoring); send-as ring abuse is bounded by Gmail's own systems and our complaint-driven response.
- **Phone uniqueness check**: same phone number cannot back more than 1 active account platform-wide. VoIP detection (Twilio Lookup) flags VoIP-only numbers for manual review.

**Acceptable residual risk:** organized professional abuse with $5k+ combined identity + onboarding budget, clean residential IPs, and patient throughput pacing. This is the floor — beyond it, no architecture short of full outbound SMTP control changes the calculus, and we've already chosen forwarding-only.

### 2.5.3 Same-Domain Impersonation (Rev-2.1 — canonicalization spec + footer downgrade)

**Risk:** "John Paul Smith" registers `john.paul@smith.com`. An impersonator registers `j.paul@smith.com`, `johnpaul@smith.com`, `john.p.smith@smith.com`. Recipients cannot reliably distinguish them; one is a phishing vector for the other.

**Locked policy:**
- **Slot disambiguation / canonicalization rules** (engineering-enforced; MVP spec):
  - **ASCII-only.** Local-part must match `[a-z0-9.\-_]+` after lowercasing. Unicode local-parts and IDN homographs (Cyrillic `а`, etc.) are rejected at MVP.
  - **Lowercase normalization.** `John.Smith` and `john.smith` collide; the canonical form is lowercase.
  - **Punctuation collision.** Hyphens, periods, and underscores are treated as the same separator for collision detection (`j.smith`, `j-smith`, and `j_smith` all collide; only one can be assigned per domain).
  - **Whitespace stripping.** Internal whitespace is rejected (RFC 5321 already handles this in the address layer; we surface it in slot creation UX).
  - **Numeric suffix ban.** Trailing/leading digits (`john.smith2`, `2john.smith`) are not permitted on either tier in MVP. Internal digits acceptable only when part of the legal name (very rare in surname namespace).
  - **Single-letter component rules.** `j` and `john` are distinct components (no first-letter collision rule); but `john.smith`, `johnsmith`, and `john_smith` all collide via the punctuation-collision rule above.
  - **Apostrophe handling.** Names like `O'Brien` register as `obrien@` (apostrophe stripped); `o.brien@` collides with `obrien@`.
  - **Reserved local-parts.** `admin`, `postmaster`, `abuse`, `support`, `webmaster`, `noreply`, `info`, `hostmaster`, `security`, `report` are platform-reserved and not assignable.
- **Display-name policing** (operational, not engineering-enforced):
  - When sending via Gmail send-as, the display name field is renter-controlled. Platform ToS prohibits using a display name that materially impersonates another person known to be a renter on the same domain. Enforcement is reactive (complaint-driven), not proactive — Gmail does not expose display-name to platform, and the platform has no path to inspect or modify outbound send-as headers.
- **Recipient-facing disclosure (transparency only — Rev-2.1 downgrade):**
  - The platform's inbound-forwarding footer reads: "This message was forwarded from `j.paul@smith.com`. The address is leased; the platform does not verify the identity of the sender beyond ID-verified signup. To verify the sender, contact them via a channel you trust."
  - **Scope (Rev-2.1 clarification):** This footer is appended to **inbound mail forwarded to renters** — i.e., recipients of mail *to* the rented address. It does **not** reach recipients of mail *from* the rented address (those are sent via Gmail send-as and never touch our infrastructure). The footer is therefore an **inbound-transparency control**, not a same-domain impersonation control. It does not protect the impersonation target's reputation downstream of send-as outbound.
- **ToS clause**: registering a local-part on a domain confers no claim of identity match. Renter accepts that the platform makes no representation that `j.paul@smith.com` and `john.paul@smith.com` are the same person.

**Residual risk: MEDIUM-HIGH** (raised from MEDIUM in 2026-04-26 draft after rubber-duck pass). Display-name impersonation via send-as outbound has **no architectural mitigation** — only ToS, complaint-driven response, and (for the impersonation target) civil remedy. Joint W4/W5 review owns the indemnification / liability backstop; this is now flagged as an MVP launch blocker, not a deferrable hand-off (§4).

### 2.5.4 Operational Cost of Compound-Slot Policy

| Control | Cost | Already in Rev-2 cost stack? |
|---------|------|-------------------------------|
| ID verification ($1.00–$1.50/signup) | One-time at signup | Yes (Rev-2 §3.1 abuse reserve) |
| 20% surcharge ops (billing logic) | Engineering build | Out of cost stack — pricing logic |
| Slot disambiguation / canonicalization engine | Engineering build | Out of cost stack — core feature |
| Display-name complaint review + send-as suspension ops | ~0.25 FTE share of T&S (Y1: covered by 0.5 FTE allocation; see §Legal & Ops staffing ramp) | Partially — Rev-2 §2i covers Y1 fixed opex; W4 staffing ramp may need Rev-2 opex uplift at 2,500-renter ceiling (W7 reconciliation item) |
| Email-footer disclosure | Engineering build, near-zero opex | N/A |
| Mailgun forwarding-reputation monitoring (per §2.6) | Tooling + ~0.1 FTE share | Yes (Rev-2 §3.1 abuse reserve at MVP scale; reassess at ceiling) |

**Net:** controls are mostly engineering build cost (one-time) plus T&S labor that ramps with renter base. Rev-2 §2i fixed opex covers the Y1 ramp (0.5 FTE) with a small uplift; full 2.0 FTE at Y2 ceiling requires Rev-2 opex revision (flagged for W7). See §Legal & Operations.

---

## §2.6 Mailgun Forwarding Reputation Controls (Rev-2.1 — new section)

**Why this section exists:** the 2026-04-26 draft framed forwarding-only as "platform has zero outbound SMTP liability." Rubber-duck pass corrected this: Mailgun forwarding mail *to* renters' Gmail mailboxes is itself outbound SMTP from Mailgun's perspective. Renter list-bombing, reputation contamination from a single bad domain, or abuse against a renter's destination address can degrade Mailgun-side reputation across all domains we forward through Mailgun. This is a real cross-domain contamination vector that the architecture does not eliminate; it must be actively managed.

### Required controls (pre-launch)

1. **Mailgun account topology review** (pre-launch blocker). Determine whether Mailgun supports per-domain or per-risk-cohort sending pools / subaccounts on our plan tier. If yes: isolate higher-risk cohorts (new signups, recent abuse incidents) on a separate Mailgun subaccount/IP pool. If no: document this as a known cross-domain reputation risk and price the mitigation cost into the W7 risk reserve.
2. **Bounce + complaint + spam-trap rate monitoring per domain** (daily). Thresholds: complaint rate >0.1%, hard-bounce rate >5%, or any spam-trap hit triggers Tier 1 review on the offending domain.
3. **List-bomb detection on inbound**: rolling 10-minute window; >50 inbound from distinct senders to a single rented address triggers temporary forwarding pause (1h auto-resume; renter notified) and abuse-team review. Mitigates the "subscribe a target's address to 1,000 newsletters" attack which would otherwise cascade to Mailgun-side bounces and complaints.
4. **Mailgun suppression-list ingestion**: when Mailgun marks a destination as bouncing or complaining, our system pauses forwarding to that destination and prompts the renter to re-verify (TOTP + email round-trip to alternate destination).
5. **Mailgun AUP review** (pre-launch blocker). Specifically: forwarding mail-of-arbitrary-origin to consumer Gmail mailboxes. Some ESPs prohibit this pattern. If Mailgun's AUP doesn't cleanly accommodate the use case, we need either (a) provider negotiation, (b) alternative provider (AWS SES has different constraints), or (c) architecture revision. Cannot launch without provider AUP confirmation in writing.
6. **Cross-domain reputation correlation monitoring** (Y1 follow-up; not pre-launch). Quarterly review: do reputation events on one rented domain correlate with delivery degradation on adjacent domains? If yes at >1.5× background rate, escalate to architecture review.

### Hard limits that fall out of these controls

- A single domain cannot exceed 0.1% Mailgun complaint rate over a rolling 7-day window without triggering forwarding pause (regardless of which renter caused it). This protects Mailgun reputation at the cost of a small false-pause rate on legitimate renters during shared incidents — accepted trade-off.
- Mailgun account-level reputation incidents (provider warning, throttling, or AUP citation) are a **K-W4-5 kill criterion** (see `_kill_criteria.md`). More than one such incident in a rolling 12-month window kills the architecture.

---

## §2.7 Sending-Bridge Dependency (Rev-2.2 — new section)

**Why this section exists:** the W1 demand pitch and the W4 forwarding-only architecture both rest on an unstated premise — that the renter's *existing* mailbox can be configured to send *as* `bill@johnson.com`. Through Rev-2.1 this was implicitly assumed to be true at any major consumer mail provider. The 2026-04-27 review surfaced that this is now functionally a **Gmail-only capability** for consumer users. The architecture still works, but the addressable market and the onboarding flow are narrower than W1 §2c assumed.

### 2.7.1 Cross-Provider Compatibility Matrix (consumer market, 2026)

| Provider | Send `bill@johnson.com` via external SMTP from this mailbox? | Architectural impact |
|---|---|---|
| **Gmail (consumer)** | ✅ Yes — "Send mail as" with custom SMTP. The reference path. | Full forwarding-only flow as designed. |
| **Google Workspace** | ✅ Yes — same plus admin-managed aliases. | Full flow; rare in our consumer ICP. |
| **Outlook.com / Hotmail / Live** | ❌ No (effectively). External-SMTP "Connected accounts" deprecated for consumer users in 2023; aliases restricted to Microsoft-owned domains. | Renter must use a sending bridge. |
| **Microsoft 365 (business)** | ⚠️ Only if the user's own tenant adds the domain — impossible on a shared/rented domain. | Out of scope for our shared-domain marketplace. |
| **Yahoo Mail (free or paid)** | ❌ No. External-SMTP send-as not supported; aliases restricted to Yahoo-owned domains. | Renter must use a sending bridge. |
| **Apple iCloud Mail (iCloud+)** | ⚠️ Custom-domain support requires the user to own and add the domain to their own account. | Out of scope for shared-domain marketplace. |
| **Fastmail** | ✅ Yes — supports external send-as on arbitrary domains. | Full flow; small consumer share. |
| **Proton Mail** | ⚠️ Custom-domain support requires user-owned domain. | Out of scope for shared-domain marketplace. |

US consumer-mail share order of magnitude (rough, public estimates): Gmail ~55–65%, Outlook/Hotmail ~10–15%, Yahoo ~10%, Apple Mail ~5–10%, other ~5%. **The send-as bridge is natively available to roughly the Gmail slice.**

### 2.7.2 Implications

1. **Inbound forwarding is universal; outbound sending is not.** Any renter on any mailbox can *receive* mail forwarded to `bill@johnson.com`. The dependency is on the *reply / outbound* path having sender identity = `bill@johnson.com`.
2. **Without a sending bridge, non-Gmail/non-Fastmail renters cannot reply as their vanity address.** They can read forwarded mail, but their replies will go out as `bill@hotmail.com` (or Yahoo, etc.) — defeating the entire identity premise of the product.
3. **The product offer must be honest about this** before payment. Quietly assuming non-Gmail users will figure it out post-purchase is a churn and chargeback driver.
4. **The Surname-Match ICP may skew Gmail-heavy** vs. the general US population (early adopters of "claim your name" energy are likely Gmail-native and tech-comfortable), but this is a hypothesis, not data. W1 LP-test instrumentation now measures it directly.

### 2.7.3 Architectural Options

| Option | Description | Cost | Re-opens W4? |
|---|---|---|---|
| **A. Gmail-bridge fallback (locked default).** | For non-Gmail renters: setup flow guides creation of a free Gmail account configured as the send-as relay (renter still receives in their preferred mailbox via forwarding; replies route through the bridge Gmail). Renter keeps using their primary mailbox for everyday reading; the bridge is a sending-only account. | Onboarding-friction cost only. No infra cost. | No. |
| **B. First-party webmail / IMAP send endpoint.** | Platform runs a minimal "compose & send" webmail or IMAP+SMTP submission endpoint that accepts authenticated renter sends and relays via Mailgun/SES. | Real outbound SMTP from platform infrastructure. **Re-opens the entire W4 outbound abuse model** (rate limiting, content scanning, abuse-driven domain reputation isolation, the Mailgun/SES AUP question for outbound-as-renter). | **Yes — fully.** Deferred to post-MVP at earliest. |
| **C. Fastmail partnership / referral.** | For non-Gmail renters who refuse the Gmail bridge, refer to Fastmail with an affiliate-style flow. | Affiliate cost; renter pays Fastmail $5/mo. | No. |
| **D. Accept market narrowing.** | Quietly serve only Gmail-native users; let Outlook/Yahoo loyalists self-deselect. | Demand-side TAM contraction. | No (but kills A-W4-8 if rejection rate is high). |

**Locked default (Rev-2.2):** Option A (Gmail bridge) for non-Gmail renters, with Option C (Fastmail referral) as an escape hatch for renters who explicitly refuse the bridge. Option B is **not** in scope for MVP. Option D is the implicit failure mode if A-W4-8 fails.

### 2.7.4 MVP onboarding flow (Rev-2.2 — locked)

1. After payment + ID verification, ask: "Where do you want to read mail addressed to `bill@johnson.com`?"
2. If Gmail: standard send-as setup wizard (existing W4 flow).
3. If anything else: branch into "Set up your sending bridge" — short explainer ("most non-Gmail providers don't let you send as a custom address; we'll set up a free Gmail account that acts as your reply relay; you'll keep reading in your preferred mailbox") + step-by-step Gmail account creation + send-as configuration.
4. Track bridge-acceptance rate vs. drop-off-at-bridge-step rate as a K-W4-6 input.

### 2.7.5 Required validation (concierge MVP + W1 LP)

- **W1 LP test (instrumentation update):** add "what's your primary email today?" to the email-capture form (Gmail / Outlook-Hotmail / Yahoo / Apple iCloud / Other / Prefer not to say). Measures ICP Gmail penetration directly.
- **Concierge MVP bridge-acceptance:** for the first cohort of non-Gmail signups, measure the share that completes the Gmail-bridge setup vs. drops off at the bridge step.
- **Bridge-friction support load:** track Tier-1 support tickets generated by the bridge-setup step as a fraction of all onboarding tickets.

### 2.7.6 Coupled Ledger Entries

- **A-W4-8** (assumption register): ≥ 70% of the Surname-Match ICP either uses Gmail today or will accept a free-Gmail sending bridge as a setup step. Launch-blocking for the demand side; if Outlook/Yahoo loyalists won't accept the bridge, the Surname-Match TAM contracts toward the Gmail slice.
- **K-W4-6** (kill criteria): combined LP-measured ICP Gmail penetration + concierge-MVP bridge-acceptance rate. If LP-measured ICP non-Gmail share is high *and* concierge bridge-acceptance is low, the marketplace is functionally Gmail-only and ICP must narrow to match.

---

## Legal & Operations Expert Perspective

### Operational Enforceability Assessment

**Can the T&S policy be operationally enforced?** **Yes, with a 0.5 → 1.0 → 2.0 FTE ramp + tooling**, scaling with the renter base up to the Rev-2 ~2,500-renter ceiling (50 domains × 50 renters/domain).

**Staffing ramp (Rev-2.1 reconciliation against Rev-2 §2i fixed opex):**

| Stage | Renter base | T&S FTE | Approx. fully-loaded cost | Coverage in Rev-2 §2i |
|-------|-------------|---------|---------------------------|------------------------|
| Y1 launch (concierge MVP, ≤500 renters) | ≤500 | **0.5 FTE** | ~$55k | Fits Rev-2 §2i Y1 fixed opex with small uplift (Rev-2 reserved ~$30–40k for abuse-ops; +$15–25k uplift required) |
| Y2 scale (≤1,500 renters) | ≤1,500 | **1.0 FTE** | ~$110k | Fits Rev-2 §2i Y2 fixed opex with modest uplift (~$30k); reflagged for W7 reconciliation |
| Y2 ceiling (~2,500 renters) | ≤2,500 | **2.0 FTE** | ~$210k | **Exceeds current Rev-2 §2i envelope.** Requires Rev-2 opex revision OR ML-assisted automation (deferred) before approaching ceiling. **W7 must reconcile.** |

The 2.0 FTE figure used in the 2026-04-26 draft was the *ceiling* number, not the Y1 number. Y1 launch is staffed at 0.5 FTE; the ramp follows the renter base. Most of the Y1 spend fits inside Rev-2 §2i fixed opex with a small uplift. Beyond ~1,500 renters, a Rev-2 opex revision is required and is flagged as a **W7 reconciliation item**.

**Breakdown by task (effort and tooling unchanged from 2026-04-26):**

| Operational Task | Effort | Tool/Approach |
|------------------|--------|---------------|
| Phone verification | LOW | Twilio SMS TOTP + Twilio Lookup (VoIP detection) |
| **ID verification (Rev-2 hard gate)** | **LOW–MEDIUM** | **Stripe Identity / Persona / Veriff API (~$1.00–$1.50/signup)** |
| Spam filtering integration | LOW | Mailgun API integration |
| RBL monitoring (daily, Rev-2 hard gate) | LOW | Cron job + alerting (Datadog); SpamHaus DQS, SORBS, Barracuda |
| **Leading-indicator monitoring (Rev-2.1)** | **LOW–MEDIUM** | **Mailgun complaint/bounce ingest, DMARC aggregate-report parsing (Postmaster Tools, SNDS), inbound spike anomaly detection** |
| **Mailgun forwarding-reputation controls (Rev-2.1)** | **LOW–MEDIUM** | **Per-domain bounce/complaint dashboards, list-bomb detector, suppression-list ingestion, AUP review (pre-launch)** |
| Tier 1 auto-pause (tier-aware) | LOW | Redis counters keyed by tier + scheduled pause job |
| Tier 2/3 manual reviews | MEDIUM | Ticketing system (Intercom/Linear); main FTE workload |
| **Compound-slot disambiguation / canonicalization** | **LOW** | **Local-part normalization at registration per §2.5.3 spec; engineering build** |
| **Display-name complaint review + send-as alias suspension (Rev-2)** | **MEDIUM** | **Reactive ticketing; share of T&S labor budget** |
| Domain owner escalations | MEDIUM | Email + dashboard notifications |
| Abuse investigation (incidents) | MEDIUM | Log aggregation |

**Tooling cost:** ~$1.5K/month (Twilio, Mailgun, Redis, Datadog, Stripe Identity, Postmaster Tools integration). Unchanged from 2026-04-26 draft.

**Sustainable until:** ~1,500 renters at 1.0 FTE; beyond that requires either the 2.0 FTE expansion (with Rev-2 opex uplift) or ML-based abuse scoring + auto-escalation for Tier 2/3 review throughput. The choice between these is a W7 decision.

### Legal Levers for Enforcement

**Contractual:**
- Terms of Service: Ban spam, phishing, malware distribution. Specify Tier 1/2/3 escalation.
- Domain Owner Agreement: Owner is liable if their domain is used for abuse by renters. Owner must cooperate with RBL delisting.
- Renter Agreement: Renter accepts forwarding-only (no native outbound). Renter's outbound send-as use is governed by Gmail's ToS, not platform's.

**Technical:**
- Pause/suspend renter's forwarding subscription without legal notice (ToS provides cover).
- Retain access to historical forwarding logs for investigation (necessary for abuse adjudication).

**Regulatory:**
- CAN-SPAM (US): Platform is a "mail service provider," not bulk mailer. Renter (user) is responsible for compliance. Forwarding is exempt.
- GDPR (EU): Forwarding = personal data processing. Privacy policy must disclose. Renter can request deletion of forwarding logs after retention period.

### Operational Debt & Scalability Concerns

**Low operational debt (forwarding-only advantage):**
- No SMTP infrastructure to maintain (Mailgun is managed).
- No outbound IP reputation to manage (renter uses Gmail's IPs).
- No sendgrid/postmark contract negotiations.

**Scalability concern:**
- At >5K renters, manual Tier 2/3 reviews become a bottleneck.
- Solution: Move to ML-based abuse scoring + auto-escalation.

---

## Red Teamer Findings

### Attack Vector 1: Multi-Account Abuse Ring (Renter + Domain Owner Collusion)

**Scenario:**
- Attacker A registers 100 renter accounts on `spam-domain.com` using:
  - Burner email addresses (temporary email services like 10minutemail.com)
  - VoIP phone numbers (Google Voice, Twilio, Skype)
  - Different credit cards (each linked to one account)
- Each account receives forwarded mail and amplifies it (uses forwarding as a spam funnel).
- Or: Attacker A owns `spam-domain.com` and purposely onboards 100 malicious "renters" that are actually accomplices.

**Ease of exploitation:** EASY (requires only $50 in VoIP credits + knowledge of disposable email/phone services)

**Current mitigation:**
- Phone verification stops simple bot armies.
- IP clustering (future feature) would detect 100 accounts from same datacenter.

**Residual gap:**
- Phone verification via VoIP is bypassable (cost: $0.50 per account).
- Domain owner collusion is undetectable if domain owner is in on the attack.

**Recommended fix:**
- Implement IP clustering in Year 1 (detect multiple accounts from same GeoIP).
- Require credit card for all renters (already planned for payment). Aggregate analysis to detect patterns.
- Set hard limit: max 10 renters per credit card + max 5 renters per IP range (/24).

**Residual risk after fix:** 2–5% of renters (organized attackers with clean IP infrastructure)

---

### Attack Vector 2: Phishing Account Takeover (ATO)

**Scenario:**
- Attacker compromises a renter's Gmail account via credential stuffing or phishing.
- Attacker now has access to renter's forwarded mail + renter's send-as alias.
- Attacker sends phishing emails to domain's contact list (harvested from forwarded mail or public sources).
- Attacker frames the legitimate renter.

**Ease of exploitation:** MODERATE (requires compromising a single Gmail account, but Gmail's 2FA may prevent this)

**Current mitigation:**
- Forwarding audit trail: Platform logs all forwarding recipients. If compromised, logs show anomaly.
- Renter notification: Weekly digest shows "Your email is being forwarded to: [Gmail]. Doesn't look like yours? Click here."
- Domain owner alert: If spam complaints spike for a renter, domain owner is notified before escalation.

**Residual gap:**
- If renter's Gmail is compromised AND their forwarding alias is compromised, attacker controls the email.
- Audit trail is reactive, not preventive.
- No automated detection of anomalous send-as activity (that's Gmail's job).

**Recommended fix:**
- Implement forwarding-destination verification: Renter must re-verify Gmail destination annually (or if Gmail changes).
- Add anomaly detection: Flag if renter's forwarding volume spikes 10x overnight.
- Partner with Gmail on abuse reporting for compromised send-as aliases (future feature).

**Residual risk after fix:** 1–3% of accounts (for organized attackers; casual ATO unlikely with forwarding model)

---

### Attack Vector 3: Domain Owner Framing / Eviction Abuse

**Scenario:**
- Domain owner `johnson.com` wants to evict a paying renter (e.g., to free up a premium name).
- Domain owner sends phishing emails using renter's forwarding address (spoofs the From header).
- Emails get flagged; platform assumes renter is guilty.
- Platform bans renter; domain owner regains control of the name.

**Ease of exploitation:** EASY (requires knowledge of SMTP spoofing + access to the domain's MX records)

**Current mitigation:**
- DMARC/SPF checks: Platform should verify DMARC/SPF before forwarding. If check fails, flag email.
- Forwarding isolation: Forwarding is from platform → renter, not domain owner → renter. Domain owner can't directly send emails on behalf of renters.
- Renter re-verification: If serious allegations against a renter (e.g., phishing), require renter to re-verify before reinstatement.

**Residual gap:**
- If domain owner has control of SMTP (they do, via DNS), they can send mail on behalf of any renter.
- Platform can't distinguish owner-sent abuse from renter-sent abuse without detailed envelope analysis.
- Re-verification takes time; renter is wrongly suspended in interim.

**Recommended fix:**
- Mandate DMARC policy for all domains (REJECT or QUARANTINE mode). This prevents owner spoofing.
- If DMARC check fails, quarantine email and notify renter. Don't auto-escalate.
- Implement "abuse appeal" process: Renter can appeal suspension within 24 hours. If appeal is credible (e.g., no outbound activity from renter's IP), reinstate.

**Residual risk after fix:** 5–10% false suspensions (inevitable; some domain owners will claim abuse even if renter is innocent; mitigated by appeals process)

---

### Attack Vector 4: Compound-Slot Squatting (Rev-2)

**Scenario:**
- A reseller signs up for 50 compound-slot variants of common names on `smith.com` — `john.smith@`, `j.smith@`, `johnsmith@`, `jsmith@`, `john.p.smith@`, etc. — using a single ID.
- They list the slots on a secondary marketplace (Reddit, eBay, identity-tier domains) at $30–$50/mo each.
- The platform loses control of identity-tier inventory; legitimate "John Smith" candidates are blocked.

**Ease of exploitation:** MEDIUM (limited by ID verification and the 3-slot/ID/domain cap; reseller must orchestrate 17+ verified IDs to hold 50 slots).

**Current mitigation:**
- 3-slot-per-person-per-domain cap (per ID hash). 50 slots = 17 IDs minimum (corrected from 2026-04-26 draft, which framed this as 50 IDs).
- 20% surcharge on slots 2 and 3 raises the effective per-slot cost to $10.20 average — secondary-market arbitrage at $30 is positive but tight.
- ID verification at signup. Synthetic IDs at $50–$200 each erase reseller margin: 17 IDs × $50–$200 = **$850–$3,400** in identity costs (corrected from 2026-04-26 draft's $2,500–$10,000 figure).
- Forfeiture clause in ToS for resale of slots without platform consent.

**Residual gap:**
- Family / household members sharing an ID could legitimately stack slots. Hard to distinguish from collusion.
- Slow-roll squatting (1–2 slots/month over 12 months) evades volume detection.

**Recommended fix:**
- Annual ID re-verification (low-friction; same vendor flow). Catches synthetic-ID expirations.
- Audit on slots 2 and 3 within an ID: flag if both unused (no inbound activity for 60 days), surface to Tier 2 review for inactivity reclamation.
- W6 to red-team the slow-roll pattern; not blocking MVP.

**Residual risk after fix:** 2–4% of compound-slot inventory at steady state held by squatters.

---

### Attack Vector 5: Same-Domain Impersonation (Rev-2)

**Scenario:**
- Legitimate renter holds `john.paul@smith.com`.
- Attacker registers `j.paul@smith.com` (passes disambiguation; "j" and "john" are distinct).
- Attacker sets Gmail send-as display name to "John Paul Smith" and sends phishing emails impersonating the legitimate renter to recipients harvested from public sources (LinkedIn, the legitimate renter's actual contact list if obtainable).

**Ease of exploitation:** MEDIUM (requires registration of the lookalike + Gmail send-as + display-name social engineering).

**Current mitigation:**
- Slot disambiguation rules collapse the obvious collisions (`j.smith` ≡ `j-smith` ≡ `j_smith`); canonicalization spec in §2.5.3 (ASCII-only, lowercase, punctuation-collapse, no numerics, reserved local-parts) closes most cheap lookalikes.
- Display-name policing is reactive — recipient or legitimate renter complaint required to trigger review.
- ID verification at signup means the attacker has provided real identity to the platform; complaint adjudication can identify them.
- **Inbound email-footer disclosure does NOT mitigate this vector** (Rev-2.1 correction). The footer is appended to inbound mail forwarded to the legitimate renter; it never reaches recipients of the impersonator's outbound send-as mail. It is therefore an inbound-transparency tool, not a same-domain impersonation control.

**Residual gap:**
- Display name is set in Gmail, not platform — platform cannot proactively police outbound display names. There is **no architectural mitigation** for send-as outbound impersonation; only ToS, complaint-driven response, and downstream civil remedy.
- Legitimate "j paul" / "john paul" name collisions are real (different people with similar names); not all complaints are valid impersonation.
- Complaint adjudication is reactive: harm is realized before remediation.

**Recommended fix:**
- **Joint W4 / W5 review on liability backstop is now an MVP launch blocker, not a deferrable hand-off** (Rev-2.1). Indemnification structure (W5 owns) determines whether platform absorbs impersonation harms or pushes them to renters via ToS. Cannot ship without resolved indemnification posture (see §4 Open Questions).
- Annual ID re-verification (catches synthetic-ID expirations; same vendor flow as signup).
- Optional Phase-2: per-domain "verified identity" badge for premium-tier renters, displayed in inbound-mail platform UI (does not affect Gmail). Defers to W6.

**Residual risk after fix:** **6–10% of complaint-driven incidents** will involve same-domain impersonation patterns (raised from 5–8% in 2026-04-26 draft after recognizing that footer disclosure does not mitigate this vector). Acceptable for MVP **only if** the W4/W5 liability backstop is resolved pre-launch.

---

### Summary: Red Team Risk Table

| Attack | Ease | Current Mitigation | Residual Risk |
|--------|------|-------------------|---------------|
| Multi-account ring | EASY → MEDIUM (Rev-2) | Phone + ID verification + $25 fee + IP clustering | 1–3% (was 2–5%; ID verification + $25 fee narrows it) |
| Account takeover | MODERATE | Audit trail + alerts + annual destination re-verification | 1–3% |
| Domain owner framing | EASY | DMARC enforcement + appeals process | 5–10% |
| **Compound-slot squatting (Rev-2)** | **MEDIUM** | **3-slot/ID/domain cap + 20% surcharge + ID verification** | **2–4% (defensive squatting indistinguishable from offensive at intake)** |
| **Same-domain impersonation (Rev-2)** | **MEDIUM** | **Slot canonicalization (§2.5.3) + display-name ToS + complaint-driven response** | **6–10% (display-name impersonation reactive-only; footer does NOT mitigate; W4/W5 indemnification is launch blocker)** |

**Verdict:** All five vectors are mitigatable. None are blockers for MVP **so long as the Rev-2 hard gates ship**. Without ID verification and the $25 onboarding fee, the multi-account ring vector returns to EASY and the compound tier must not ship.

---

## Synthesis & Locked Recommendations

### 1. Concrete Abuse-Prevention Policy

**Principle:** Forwarding-only architecture minimizes — but does not eliminate — platform abuse liability. Renter outbound = renter's responsibility (via Gmail send-as); platform-side reputation is still exposed via Mailgun forwarding (see §2.6). Rev-2 hard gates make the standard tier defensible.

**Onboarding Requirements (Rev-2 locked):**
- Valid email address (verified via Mailgun)
- Phone number + TOTP (SMS verification, VoIP-flagged numbers manual review)
- **Government-issued ID verification** (Stripe Identity / Persona / Veriff)
- **$25 non-waivable onboarding fee**
- Domain owner opt-in approval (required for premium single-name; optional for standard compound)
- Acceptance of ToS (spam/phishing ban, escalation process, data sharing, slot policy, display-name policy)

**Compound-Slot Policy (Rev-2 locked, per §2.5):**
- 3 slots per ID per domain max
- 20% surcharge on slots 2 and 3
- One premium single-name slot per ID per domain
- Slot canonicalization rules per §2.5.3 (ASCII-only, lowercase, punctuation-collapse, no numerics, reserved local-parts, apostrophe-stripped)
- Display-name impersonation prohibited in ToS; alias suspension on confirmed send-as abuse

**Abuse Escalation Policy:**
- **Tier 1 (Auto-Pause):** Standard >200/24h OR Premium >500/24h OR >10 spam-flagged/24h → 24h pause, appeal-able
- **Tier 2 (Suspend):** Tier 1 repeat within 7 days → 7-day suspension, written explanation required
- **Tier 3 (Terminate):** Tier 2 repeat OR confirmed criminal activity → permanent ban + legal notice

**Monitoring & Detection:**
- Mailgun spam filtering + SpamAssassin on all inbound
- Daily RBL monitoring for all domains; CRITICAL alert if blacklisted
- **Leading-indicator stack (Rev-2.1):** Mailgun complaint + bounce rates per domain, DMARC aggregate reports (Gmail Postmaster Tools, Microsoft SNDS), inbound spike anomaly detection
- **Mailgun forwarding-reputation controls (§2.6):** per-domain dashboards, list-bomb detection, suppression-list ingestion
- Rate-limit tracking: Inbound forwards, spam scores, DMARC failures
- **Send-as outbound abuse monitoring (§2.5.2):** complaint links in inbound footer, abuse@ inbox monitoring, Gmail Postmaster Tools, annual destination re-verification, alias suspension on confirmed abuse

**Data Retention:**
- Forwarding logs: 90 days (sufficient for abuse investigation)
- Abuse records (Tier 1/2/3): 2 years (legal hold)
- Deleted renter data: 30-day grace period before deletion (legal compliance)

---

### 2. Recommended Email Flow (Forwarding-Only MVP)

**Architecture Diagram (Text Description):**

```
┌─────────────────────────────────────────────────────────────┐
│ INBOUND FLOW (Renter Receives Mail)                         │
├─────────────────────────────────────────────────────────────┤
│                                                               │
│  Sender → bill@johnson.com (platform MX)                     │
│           ↓                                                   │
│        Mailgun (spam filter + phishing check)                │
│           ↓                                                   │
│        [Spam?] → ✓ Forward to Gmail / ✗ Quarantine          │
│           ↓                                                   │
│        bill.johnson@gmail.com                                │
│           ↓                                                   │
│        Renter reads mail in Gmail (native interface)         │
│                                                               │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ OUTBOUND FLOW (Renter Sends Mail)                           │
├─────────────────────────────────────────────────────────────┤
│                                                               │
│  Renter → Gmail web / Gmail app                              │
│           ↓                                                   │
│        Gmail send-as: Use bill@johnson.com as sender         │
│           ↓                                                   │
│        Gmail SMTP (Gmail's IP reputation)                    │
│           ↓                                                   │
│        Recipient (mail is sent via Gmail's infrastructure)   │
│                                                               │
│  NOTE: Platform has no path to inspect or rate-limit          │
│        send-as outbound. Gmail's abuse controls apply         │
│        plus our complaint-driven response (§2.5.2,            │
│        Send-As Outbound Abuse Monitoring).                    │
│                                                               │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ MONITORING FLOW (Domain Reputation Protection)              │
├─────────────────────────────────────────────────────────────┤
│                                                               │
│  Daily (Automated):                                          │
│    1. Check johnson.com on SpamHaus/SORBS/Barracuda         │
│    2. If blacklisted → CRITICAL ALERT to domain owner      │
│    3. Pause all forwarding on johnson.com                   │
│    4. Investigate: Which renters contributed to blacklist?  │
│    5. Escalate to domain owner for remediation              │
│                                                               │
│  Real-time (On Each Forward):                               │
│    1. Check inbound spam score                              │
│    2. Track per-renter forwarding volume                    │
│       (Tier 1 trigger: Standard >200/day, Premium >500/day) │
│    3. Track Mailgun complaint/bounce rates per domain       │
│    4. If abuse detected → Tier 1 auto-pause                 │
│                                                               │
└─────────────────────────────────────────────────────────────┘
```

**Key Design Principles:**
1. **Isolation:** Renter outbound is isolated from platform infrastructure.
2. **Detectability:** Inbound abuse is detected before forwarding (via Mailgun).
3. **Reactivity:** RBL monitoring enables rapid response to reputation damage.
4. **Transparency:** Domain owner is always aware of forwarding activity + abuse status.

---

### 3. Infrastructure & Dependencies

**External Services:**
- **Mailgun** (for inbound MX + filtering)
- **Twilio** (for SMS phone verification)
- **Gmail API** (for forwarding, send-as setup)
- **SpamHaus API** (for daily RBL monitoring)

**Internal Infrastructure:**
- **Redis** (rate-limiting counters + session state)
- **Postgres** (user/domain/forwarding records + audit logs)
- **Alerting** (Datadog/PagerDuty for RBL critical alerts)

**Build Timeline:** ~3 months (including Mailgun integration, Gmail API integration, RBL monitoring) — *contingent on Gate 0 send-as deliverability proof and the five MVP launch blockers in §4 resolving first*.

---

### 4. Open Questions (Rev-2.1 — split into MVP launch blockers vs. follow-ups)

**MVP launch blockers (must resolve before code build commences; reclassified from "hand-offs" by Rev-2.1 rubber-duck pass):**

1. **Gate 0: Send-as deliverability proof.** Empirical test that consumer Gmail send-as on a non-Google `.com` produces clean SPF/DKIM/DMARC alignment to recipients at Gmail, Outlook, Yahoo, Apple Mail, and Microsoft 365 — no "via gmail.com" sender mismatch, no DMARC quarantine/reject in aggregate reports. This is the foundational technical proof for forwarding-only. **A-pre-1 cannot be locked without it.**
2. **Provider AUP confirmations in writing.** Mailgun (forwarding mail-of-arbitrary-origin to consumer Gmail), Gmail (send-as on non-Google domains for consumer marketplace use), Stripe Connect (marketplace processing identity-grade rentals + ID verification). All three must produce written or documented AUP compatibility before launch. Any one rejecting our pattern is a structural blocker.
3. **Indemnification posture for blacklist + impersonation harms** (W4/W5 joint). Without a settled stance — platform absorbs vs. push to renters via ToS vs. insurance reserve — the same-domain impersonation residual (6–10% of complaint incidents) is unbounded liability. Must lock pre-launch.
4. **Owner-pull-during-active-incident protocol** (W4/W5 joint). If RBL pause triggers and the owner wants to withdraw the domain mid-incident, the renter-protection minimum (notice, migration, refund) must be specified before the first paying cohort.
5. **Owner-vs-renter abuse arbitration** (W4/W5 joint). What if a domain owner claims a renter is abusive but forwarding logs show otherwise? Who arbitrates? The complaint adjudication path must be specified before live operations.
6. **Sending-bridge dependency validation** (Rev-2.2, §2.7). LP-measured ICP Gmail penetration + concierge-MVP bridge-acceptance rate must clear K-W4-6 thresholds before broad launch. The Gmail-bridge fallback flow (§2.7.4) must be built and friction-measured before the first non-Gmail paid signup.

**W5 Continuity follow-ups (deferrable beyond MVP launch):**
1. **Payment cliff:** What happens if a domain owner stops paying renewal fees? Can the platform intervene at the registrar level?
2. **Renter protection at sale-escape:** Migration window mechanics if a domain is sold mid-lease.
3. **Legal hold:** Must the platform retain forwarding logs longer than 90 days for legal disputes?

**W6 Red Team follow-ups:**
1. Slow-roll squatting attack pattern (1–2 slots/month over 12 months).
2. **Cross-domain reputation correlation** (Y1 quarterly review per §2.6.6). If reputation events on one rented domain correlate >1.5× background with delivery degradation on adjacent domains, escalate to architecture review.
3. Family / household ID-sharing edge case in the 3-slot cap.
4. Long-term policy stability of Gmail send-as, Mailgun AUP, and Stripe Connect (re-review annually).

**W7 Go/No-Go reconciliation items:**
1. **Rev-2 §2i opex revision** to absorb T&S staffing ramp at 2.0 FTE ceiling (Y2; ~$210k vs current §2i envelope). Y1 ramp at 0.5 FTE fits with small uplift; ceiling does not.
2. ML-assisted abuse scoring vs. linear FTE scaling decision at the ~1,500-renter threshold.

---

## Conditionally Locked Verdict (Rev-2.1, 2026-04-27) — Updated Rev-2.2 (2026-04-27)

🟡 **Forwarding-only is the locked MVP architecture for design purposes. The Rev-2 compound tier is *conditionally* locked pending resolution of six pre-build hard gates and six MVP launch blockers.** Downgraded from "Locked" (2026-04-26) after rubber-duck pass surfaced unproven technical assumptions and unbudgeted launch dependencies. Rev-2.2 added the sending-bridge dependency (§2.7) as a sixth launch blocker and an additional kill criterion (K-W4-6).

**What this workshop establishes (locked at the design level):**
1. Domain reputation can be protected architecturally under forwarding-only at 50 renters/domain — *conditional on Gate 0 send-as deliverability proof*.
2. Abuse detection design is sound (Mailgun spam scoring + daily RBL + leading indicators + tier-aware forwarding throughput limits + Mailgun forwarding-reputation controls + send-as complaint-driven response).
3. Operational burden is sustainable at a 0.5 → 1.0 → 2.0 FTE ramp + tooling up to ~2,500 renters, with the caveat that the 2.0 FTE ceiling exceeds Rev-2 §2i fixed opex (W7 reconciliation item).
4. Residual risks across all five attack vectors (multi-account ring, ATO, owner framing, compound-slot squatting, same-domain impersonation) are mitigatable to acceptable levels — with same-domain impersonation residual raised to 6–10% after recognizing footer disclosure does not mitigate it.

**Six conditional pre-build gates (compound tier does not ship if any fails):**
0. **Pre-MVP send-as deliverability proof** (new, Rev-2.1) — see Gate 0 in Executive Summary.
1. Automated daily blacklist monitoring + leading-indicator stack across SpamHaus / SORBS / Barracuda + Mailgun complaint/bounce rates + DMARC aggregate reports.
2. Forwarding throughput limits: Standard 200/day, Premium 500/day; send-as outbound governed by Gmail + complaint-driven response.
3. ID verification at signup (vendor selection: Stripe Identity / Persona / Veriff).
4. Non-waivable $25 onboarding fee.
5. Compound-slot policy caps (3/ID/domain, 20% surcharge on slots 2+, canonicalization spec per §2.5.3, display-name ToS, send-as alias suspension on confirmed abuse).

**Six MVP launch blockers** (in addition to the six gates; must resolve before code build commences):
1. Provider AUP confirmations in writing (Mailgun, Gmail, Stripe Connect).
2. Indemnification posture for blacklist + impersonation harms (W4/W5 joint).
3. Owner-pull-during-active-incident protocol (W4/W5 joint).
4. Owner-vs-renter abuse arbitration path (W4/W5 joint).
5. Mailgun account topology decision (per-domain subaccounts / per-cohort pools availability) per §2.6.
6. **Sending-bridge dependency** (Rev-2.2 §2.7): LP-measured ICP Gmail penetration + concierge-MVP bridge-acceptance must clear K-W4-6; Gmail-bridge fallback flow (§2.7.4) built and friction-measured before first non-Gmail paid signup.

**Cost-stack reconciliation note (Rev-2.1):**
- Y1 launch staffing (0.5 FTE) fits Rev-2 §2i fixed opex with a $15–25k uplift.
- Y2 mid-scale (1.0 FTE) fits with a ~$30k uplift.
- Y2 ceiling (2.0 FTE at ~2,500 renters) exceeds Rev-2 §2i envelope and **requires Rev-2 opex revision OR ML-assisted automation** before approaching the ceiling. Flagged as a **W7 reconciliation item** — does not block W4 close, does block W7 Go/No-Go without resolution.

**What this workshop does NOT establish (handed to W5 / W6 / W7):**
1. Operational answer to the five MVP launch blockers above (W5 owns most; W6 owns provider AUP red-team).
2. Empirical confirmation of Gate 0 (technical-proof task; runs in parallel with W5).
3. Whether ID-verification post-hoc abuse rate clears K-W4-3 in practice (resolves only with live cohort data, ≥100 paid signups).
4. Long-term provider stability (W6 + ongoing).

**Kill Criteria locked into `_kill_criteria.md` (Rev-2.1):**
- **K-W4-1**: Per-domain blacklist incident rate (lifts and locks K-Rev2-3).
- **K-W4-2a**: Tier 1 false-positive rate among legitimate users (UX risk).
- **K-W4-2b**: Confirmed forwarding-abuse rate (per 100 renter-months, post-Tier-2/3 adjudication).
- **K-W4-2c**: Send-as outbound complaint rate (per renter, via Mailgun + Postmaster Tools + abuse@ inbox).
- **K-W4-3**: ID-verification post-hoc abuse rate (observable proxies: chargeback rate by IDV vendor, near-duplicate identity rate, confirmed abuse rate among ID-verified cohort).
- **K-W4-4** (new, Rev-2.1): Send-as deliverability proof (pass/fail at Gate 0).
- **K-W4-5** (new, Rev-2.1): Mailgun account-level reputation incidents (provider warning, throttling, AUP citation; >1 in rolling 12-month window kills architecture).
- **K-W4-6** (new, Rev-2.2): Sending-bridge dependency — combined LP-measured ICP Gmail penetration + concierge-MVP Gmail-bridge acceptance rate. Threshold spec in `_kill_criteria.md`.

**Next Steps:**
1. **Gate 0 technical-proof task** — run empirical send-as deliverability test against Gmail/Outlook/Yahoo/Apple/M365. Required before A-pre-1 fully locks.
2. **Provider AUP outreach** — Mailgun, Gmail, Stripe Connect. Required before code build.
3. **W5 Continuity** — opens with the five MVP launch blockers as primary scope.
4. **W6 Red Team** — full system stress test against W1–W5 outputs, including provider AUP red-team.
5. **Concierge MVP cohort** (parallel) is the operational validator for ID-verification friction, $25 onboarding fee conversion impact, send-as setup friction, and standard-tier abuse-ring detection.


