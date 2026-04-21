# Deliverability Workshop: Abuse Prevention & MVP Email Architecture

**Date:** 2026-04-21  
**Facilitator Input:** Trust & Safety Architect, Legal & Operations Expert, Red Teamer  
**Status:** DRAFT — Provisional. Forwarding-only is the safest *candidate* architecture, **not yet validated as sellable**.

> ### ⚠️ Revision Notice (2026-04-21)
>
> This workshop was originally the first step of a 4-step defensive validation plan. After a framework critique, the plan was revised: demand validation, supply acquisition, and marketplace economics must precede the deliverability decision. See `02_feasibility_validation.md` and `03_agent_framework.md`.
>
> **The conclusion below has been reframed.** Forwarding-only may still win, but it is now a hypothesis pending:
>
> 1. A validated ICP from the Demand & Positioning Workshop. "Forwarding-only" reads as a liability to a "professional credibility" buyer and as a feature to a "privacy-first" buyer. The framing only becomes a decision once the winning buyer is known.
> 2. An economics check from the Marketplace Economics Workshop. Forwarding-only implies a thinner product and may imply a lower price; the unit economics of that must clear CAC + support + abuse.
> 3. A supply check from the Supply Acquisition Workshop. Some domain owners will refuse forwarding-only specifically because it limits the renter value proposition and therefore listing price.
> 4. A dependency review from the Red Team Workshop. Forwarding-only depends on Gmail send-as, Mailgun AUP, and Stripe Connect tolerance; each is a single point of policy failure.
>
> **Assumptions this workshop baked in that remain unvalidated:**
>
> - Target renters are comfortable with "not a real mailbox."
> - Target renters are Gmail-centric (or have an equivalent client supporting send-as).
> - Recipients do not perceive forwarded/aliased mail as lower-trust.
> - Users tolerate send-as setup friction.
> - Gmail, Mailgun, and Stripe policies remain compatible with this pattern.
>
> The analysis below remains useful as a **defensive baseline**: it describes the safest architecture *if* the winning offer turns out to be compatible with forwarding-only. It should be **revisited after Workshops 1–3** and either confirmed, revised, or replaced.

---

## Executive Summary

### Problem Statement
The core risk of the marketplace is **domain reputation collapse**: if one renter sends spam or phishing, the entire domain (and all other renters' addresses) gets blacklisted. A single bad actor damages everyone.

### Recommended MVP Approach
**Forwarding-only architecture with Gmail Send-As:**
- **Inbound:** Platform receives mail, forwards to renter's Gmail
- **Outbound:** Renter sends via Gmail's infrastructure (not platform-controlled)
- **Benefit:** Domain reputation isolated from renter sending behavior; platform has zero control over outbound mail quality, so cannot be held liable; abusive outbound simply doesn't happen through the platform

### Risk Assessment
| Dimension | Risk Level | Confidence |
|-----------|-----------|-----------|
| Domain reputation protection | MEDIUM | 85% |
| Operational enforcement | LOW | 90% |
| Legal enforceability | LOW | 80% |
| Residual abuse loops | MEDIUM | 70% |

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

### Onboarding & Verification (Medium Friction)

**Identity & Risk Assessment:**
- Email address (must be valid; Mailgun will verify)
- Phone number (TOTP challenge; detects bot rings; prevents multi-accounting)
- Manual review flag: Domain owners must opt in to accept renters. Opt-in triggers domain owner review of renter identity.

**Rationale:**
- Email-only is too weak (bot armies, disposable emails).
- Phone + email detects most casual abuse rings.
- Domain owner opt-in gives domain owner veto on high-risk renters.

### Rate Limits (Forwarding-Only, So Limits Are Light)

**Per-renter daily limits (for inbound forwarding):**
- 500 forwards/day (detects industrial mailing list abuse)
- Hard stop at 10,000/month (catches seasonal abuse)

**Rationale:**
- Forwarding is lightweight (not SMTP sending). Most legitimate users send <50 emails/day via send-as.
- Limits are mainly to detect industrial abuse rings, not to throttle legitimate users.
- No rate limits on outbound (that's Gmail's problem).

### Abuse Monitoring & Detection

**Content Filtering:**
- Mailgun will provide SpamAssassin + phishing detection on inbound.
- Flag high-spam-score emails before forwarding; store flagged mail in quarantine for renter review.
- Daily digest to renter: "5 emails were flagged as likely spam; review them here."

**RBL (Realtime Blackhole List) Monitoring:**
- Daily automated check: Is `johnson.com` on SpamHaus/SORBS/Barracuda?
- **CRITICAL alert:** If domain lands on RBL, immediately:
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
- Trigger: >500 forwards in 24 hours OR >10 spam-flagged emails in 24 hours
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

- Mailgun (or similar) reliably detects spam/phishing.
- Domain owners are responsive to RBL alerts and willing to remediate.
- Renters will tolerate medium onboarding friction (phone verification).
- Platform can sustain 2.0 FTE for abuse monitoring in Year 1.

---

## Legal & Operations Expert Perspective

### Operational Enforceability Assessment

**Can the T&S policy be operationally enforced?** **Yes, with 2.0 FTE + tooling.**

**Breakdown:**

| Operational Task | Effort | Tool/Approach |
|------------------|--------|---------------|
| Phone verification | LOW | Twilio SMS TOTP |
| Spam filtering integration | LOW | Mailgun API integration |
| RBL monitoring (daily) | LOW | Cron job + alerting (Datadog) |
| Tier 1 auto-pause | LOW | Redis counters + scheduled pause job |
| Tier 2/3 manual reviews | MEDIUM | Ticketing system (Intercom/Linear); 1 FTE |
| Domain owner escalations | MEDIUM | Email + dashboard notifications; 0.5 FTE |
| Abuse investigation (incidents) | MEDIUM | Log aggregation; 0.5 FTE |

**Year 1 Staffing:** 2.0 FTE ($210K salary) + $1K/month tooling (Twilio, Mailgun, Redis, Datadog)

**Sustainable until:** <5K renters on <50 domains. Beyond that, automation (ML abuse detection) needed.

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

### Summary: Red Team Risk Table

| Attack | Ease | Current Mitigation | Residual Risk |
|--------|------|-------------------|---------------|
| Multi-account ring | EASY | Phone verification | 2–5% (IP clustering needed) |
| Account takeover | MODERATE | Audit trail + alerts | 1–3% (re-verification helps) |
| Domain owner framing | EASY | DMARC + re-verification | 5–10% (appeals process needed) |

**Verdict:** All three vectors are mitigatable. None are blockers for MVP. Residual risk is acceptable (platform maintains 90%+ integrity with monitoring).

---

## Synthesis & Locked Recommendations

### 1. Concrete Abuse-Prevention Policy

**Principle:** Forward-only architecture minimizes platform abuse liability. Renter outbound = renter's responsibility (via Gmail).

**Onboarding Requirements:**
- Valid email address (verified via Mailgun)
- Phone number + TOTP (SMS verification)
- Domain owner opt-in approval (domain owner reviews renter before activation)
- Acceptance of ToS (includes spam/phishing ban, escalation process, data sharing)

**Abuse Escalation Policy:**
- **Tier 1 (Auto-Pause):** >500 forwards/24h OR >10 spam-flagged emails → 24h pause, appeal-able
- **Tier 2 (Suspend):** Tier 1 repeat within 7 days → 7-day suspension, written explanation required
- **Tier 3 (Terminate):** Tier 2 repeat OR confirmed criminal activity → permanent ban + legal notice

**Monitoring & Detection:**
- Mailgun spam filtering + SpamAssassin on all inbound
- Daily RBL monitoring for all domains; CRITICAL alert if blacklisted
- Rate-limit tracking: Inbound forwards, spam scores, DMARC failures
- Abuse reporting channel: Recipients can report abusive forwarded mail via link in footer

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
│  NOTE: Platform has ZERO involvement in outbound SMTP.       │
│        Gmail's abuse controls apply (not platform's).        │
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
│    2. Track per-renter volume (detect >500/day spike)       │
│    3. If abuse detected → Tier 1 auto-pause                 │
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

**Build Timeline:** ~3 months (including Mailgun integration, Gmail API integration, RBL monitoring)

---

### 4. Open Questions for Continuity Workshop

1. **Payment cliff:** What happens if a domain owner stops paying renewal fees? Can the platform intervene?
2. **Renter protection:** If a domain expires, how are renters notified + migrated?
3. **Escalation for domain owners:** What if a domain owner claims a renter is abusive but forwarding logs show otherwise? Who arbitrates?
4. **Legal hold:** Must the platform retain forwarding logs longer than 90 days for legal disputes?

---

## Provisional Verdict (Pending Demand Validation)

🟡 **Forwarding-only is the safest candidate architecture. Whether it is the right MVP depends on the winning offer.**

**What this workshop establishes:**
1. *If* the product is forwarding-only, domain reputation can be protected architecturally.
2. *If* the product is forwarding-only, abuse detection is feasible (Mailgun + RBL monitoring).
3. *If* the product is forwarding-only, operational burden is sustainable at ~2.0 FTE + tooling.
4. Residual risks (multi-account rings, ATO, owner framing) are mitigatable.

**What this workshop does NOT establish:**
1. That anyone will pay for forwarding-only at a price that clears unit economics.
2. That the target ICP accepts a non-mailbox product.
3. That the three-way dependency on Gmail, Mailgun, and Stripe is stable.
4. That the "50/50" split referenced in operational assumptions is defensible.

**Next Steps (revised):**
1. Run the Demand & Positioning Workshop to pick the winning offer.
2. Run the Supply Acquisition Workshop to confirm owners will list under this architecture.
3. Run the Marketplace Economics Workshop to confirm the numbers work.
4. **Return to this workshop** and either confirm forwarding-only, adjust it (e.g., hybrid with vetted outbound for a premium tier), or replace it.

