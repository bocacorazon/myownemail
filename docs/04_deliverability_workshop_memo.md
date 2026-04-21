# Deliverability Workshop Memo
## Vanity Email Marketplace — Trust & Safety Design

**Date:** Pre-MVP Validation Phase  
**Phase:** Systematic Risk Mitigation (Step 1 of 4)  
**Facilitator:** System Design Review  
**Status:** LOCKED RECOMMENDATIONS (ready for Continuity Workshop dependency)

---

## EXECUTIVE SUMMARY

### Problem Statement
A two-sided marketplace for vanity email addresses (e.g., `bill@johnson.com` rented from a domain owner) faces an existential trust & safety risk: **if one renter sends spam or phishing, the entire domain gets blacklisted for all renters and the domain owner.** This is not a feature bug—it's a structural property of email reputation systems (SpamAssassin, Barracuda, Microsoft, Gmail). The marketplace cannot scale if domains are routinely demolished by bad renters.

### Recommended MVP Approach
**FORWARDING-ONLY WITH GMAIL SEND-AS**
- Renters receive email forwarded to their personal Gmail/Outlook inbox.
- Renters compose replies using "Send As" (or Gmail's forwarding reply feature) from their personal email account.
- **Zero outbound mail originates from the marketplace mailbox.**
- This eliminates the primary attack vector: spammers hijacking the domain's mail infrastructure.

**Rationale:**  
- Forwarding-only cuts domain reputation risk by ~90% (outbound SMTP is where damage occurs).
- Gmail/Outlook send-as is UX-acceptable for an MVP (users are already on these platforms).
- Reduces onboarding friction vs. full identity verification for full-SMTP access.
- Defers the "full outbound SMTP" feature to post-MVP (post-continuity, post-legal review).

### Risk Assessment
- **Risk Level:** MEDIUM (with forwarding-only architecture)
- **Confidence:** HIGH (forwarding pattern is proven by ForwardEmail.net, HEY, and enterprise email)
- **Primary Residual Risk:** Domain flagging due to renter misconfiguration or compromised inbound forwarding chains.
- **Secondary Risk:** Renter using the address for credential stuffing or phishing link delivery (lower reputational impact if inbox-only).

### Key Decisions Locked In This Workshop
1. ✅ **MVP Email Flow:** Forwarding-only + Gmail send-as (no native outbound SMTP)
2. ✅ **Onboarding Friction:** Email verification + basic identity check (name, phone TOTP optional)
3. ✅ **Rate Limits:** Per-renter forwarding receive limit (500/day); no send limits (external service)
4. ✅ **Domain Protection:** Proactive monitoring + reactive abuse escalation (documented below)

---

## 1. TRUST & SAFETY ARCHITECT MEMO

### Role & Primary Question
**Trust & Safety Architect** designs guardrails that keep spammers, phishers, and high-risk users from damaging deliverability and domain reputation. Primary question: **How do we keep the product usable without creating a loophole for abuse?**

---

### 1.1 Strongest Problem Version

#### The Domain Reputation Cascade
A single renter sends phishing emails from `bill@johnson.com`. The attack vector:
1. Renter gains access to `bill@johnson.com` via the platform.
2. Renter uses the email to trick users into clicking malicious links (phishing, 419 scams, credential stuffing).
3. ISP spam filters (Gmail, Outlook, Yahoo, Barracuda) flag `johnson.com` as a phishing source.
4. **ALL renters on `johnson.com` (and the domain owner)** lose deliverability.
5. New legitimate email from `johnson.com` goes straight to spam/junk for millions of users globally.
6. The domain's reputation takes 6–12 months to recover (if at all).

#### Secondary Cascade: The Bitcoin Ransom Scenario
A compromised renter account or legitimate malicious renter:
1. Uses `bill@johnson.com` to send bulk cryptocurrency investment scams to purchased email lists.
2. The renter never meets KYC requirements, leaves no paper trail.
3. `johnson.com` gets added to RBL (Real-time Blacklist) feeds used by enterprise mail filters.
4. The domain owner cannot use the domain for their own email.
5. The domain becomes worthless (cannot be sold, re-leased, or recovered).

#### The Credential Stuffing Exploitation
A sophisticated attacker:
1. Rents 100 addresses on premium domains (e.g., `bill@johnson.com`, `bob@johnson.com`).
2. Uses them to create fake LinkedIn profiles, Apple ID accounts, or bank wire authorization aliases.
3. Sends phishing emails to employees from `@johnson.com` addresses (high trust factor).
4. Even if the renter never sends outbound mail themselves, their account credentials are hijacked by an attacker.
5. Domain reputation suffers not from the attacker's mail, but from the marketplace's failure to prevent account takeover.

**Severity:** CRITICAL. A single renter or compromised account can destroy the platform's core asset (domain availability).

---

### 1.2 Proposed Solution: Forwarding-Only MVP with Hardened Onboarding

#### Email Flow Architecture

```
┌─────────────────────────────────────────────────────────────┐
│ INBOUND FLOW (Incoming Mail)                                │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│ 1. Sender sends mail to bill@johnson.com                    │
│    ↓                                                         │
│ 2. DNS MX record points to platform's mail infrastructure   │
│    (e.g., mail.myownemail.com)                              │
│    ↓                                                         │
│ 3. Platform receives mail in secure inbox                   │
│    ↓                                                         │
│ 4. Content scan (SpamAssassin, custom filters)              │
│    - Reject if suspicious phishing/malware                  │
│    - Log all headers for forensics                          │
│    ↓                                                         │
│ 5. Forward to renter's personal Gmail/Outlook address       │
│    (encrypted tunnel via SMTPS or API)                      │
│    ↓                                                         │
│ 6. Renter receives in personal inbox                        │
│                                                              │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ OUTBOUND FLOW (Renter Replies)                              │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│ 1. Renter opens Gmail/Outlook, clicks "Reply"               │
│    ↓                                                         │
│ 2. Gmail's "Send As" feature uses renter's account          │
│    (NOT platform mail server)                               │
│    ↓                                                         │
│ 3. Reply is sent from:                                      │
│    - bill@johnson.com (From: header)                        │
│    - But mail originates from Gmail's infrastructure        │
│    - Gmail maintains its own reputation (not johnson.com)   │
│    ↓                                                         │
│ 4. Recipient gets reply                                     │
│                                                              │
│ KEY: Platform infrastructure sends ZERO bytes of outbound   │
│      mail on behalf of renters.                             │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

**Why this matters for reputation:**
- ISPs track SPF/DKIM/DMARC signing servers, not just domain names.
- If `bill@johnson.com` replies via Gmail (signed by Gmail's keys), Gmail's reputation absorbs any abuse.
- Platform infrastructure is never blamed for renter-originated spam (only for inbound forwarding infrastructure).
- A compromised renter account harms Gmail's reputation (which has spam-fighting infrastructure at scale), not `johnson.com`.

---

#### 1.2a Identity Verification & Onboarding Friction

**Goal:** Raise the cost of abuse without killing marketplace accessibility.

**Renter Onboarding Checklist:**

| Step | Requirement | Rationale | Friction Level |
|------|-------------|-----------|-----------------|
| 1 | Email verification | Confirm renter controls the email they claim | LOW |
| 2 | Legal ToS + Abuse Policy acceptance | Clear terms of service, acceptable use policy | LOW |
| 3 | Name + address on file | Match to identity verification (see step 4) | LOW |
| 4 | Phone verification (TOTP or SMS) | Confirm phone number in case of account takeover | MEDIUM |
| 5 | *(Optional) ID document scan* | Reserved for high-value addresses or post-abuse escalation | HIGH |

**Policy Details:**

- **Email Verification:** Standard double-opt-in (send verification link).
- **Phone Verification:** SMS OTP (one-time password) or TOTP app (Google Authenticator, Authy).
  - Renters can disable 2FA after initial setup, but account takeover triggers re-verification.
  - Phone number is never shared with domain owner.
- **Name & Address:** Collected at signup, matched against payment method (Stripe).
  - If mismatch detected, flag for manual review before address activation.
- **Identity Document (Post-MVP):** Required for:
  - Premium domains (>$50/month valuation).
  - High-risk categories (finance, crypto, healthcare).
  - After first abuse flag on account.
  - Addresses created via Stripe Connect (to enforce KYC on domain owner side).

**Enforcement:**
- No address is active for receiving mail until all required steps pass.
- Webhook from payment processor (Stripe) triggers final KYC check.
- Manual review is async (24–48 hour SLA) but does not delay forwarding.

---

#### 1.2b Rate Limits (Inbound Forwarding)

**Goal:** Detect mass-abuse patterns without harming normal users.

**Per-Renter Inbound Limits:**

| Limit | Threshold | Action | Rationale |
|-------|-----------|--------|-----------|
| Forwarded emails/day | 500 | Pause forwards, alert ops | Detects bulk credential stuffing |
| Unique sender addresses/day | 200 | Pause forwards, alert ops | Detects list-buying attacks |
| Bounce rate (% rejected mail) | >30% | Pause forwards, alert ops | Detects mail injection attacks |
| Same recipient repeated sends | 50+ in 1hr | Temp pause, notify renter | Rate-limit bombing |
| Domain reputation score (platform metric) | <-20 | Quarantine, escalate | Aggregate abuse signal |

**Why these numbers:**
- Normal renter: 5–50 forwards/day.
- Power user: 50–200 forwards/day.
- Bulk attacker: 1000+ forwards/day.
- Threshold of 500 gives 2–10x headroom for legitimate users while catching industrial-scale abuse.

**Enforcement Mechanism:**
- Real-time check on inbound mail delivery.
- If limit exceeded, mail is forwarded to quarantine folder (not renter inbox).
- Renter receives notification: "You've exceeded forwarding limits due to suspicious activity. Reply to confirm this is expected."
- If confirmed, limit is increased by 50% (up to 1000/day).
- If not confirmed, account is flagged for abuse review.

---

#### 1.2c Content Filtering & Abuse Signals

**Goal:** Detect phishing, scams, and credential stuffing before mail is forwarded.

**Inbound Content Scan:**

1. **SpamAssassin + Custom Rules:**
   - Run SA on all inbound mail.
   - If SA score > 5.0 (spam threshold), forward to spam folder.
   - Custom rules check for:
     - Phishing keywords (e.g., "urgent", "verify account", "confirm password").
     - Known credential stuffing domains (e.g., phishing registries like PhishTank).
     - Malware signatures (VirusTotal API check on attachments).

2. **Renter Behavior Analysis:**
   - Track: which senders are forwarding to renter, how often, what times of day.
   - If sudden spike in forwards from new senders at odd hours, flag as anomalous.
   - Example: Renter normally gets 10 forwards/day 9–5 PM. Suddenly 200 forwards 2–4 AM from new senders → abuse signal.

3. **Reputation Blacklist Monitoring:**
   - Weekly: check if domain is on SpamHaus SBL, CBL, or PBL.
   - If yes, investigate which renter accounts are receiving mail from blacklisted IPs.
   - Quarantine those accounts pending review.

4. **Callback Verification (Post-MVP):**
   - For high-risk senders (first-time senders from unrecognized domains), optionally require renter to confirm receipt before final forward.
   - UX: "New sender alert: acme-corp.com is sending to you for the first time. Confirm to receive."

---

#### 1.2d Monitoring & Detection Systems

**Real-Time Abuse Detection:**

| Signal | Detection Method | Action | Escalation |
|--------|------------------|--------|------------|
| **Domain added to RBL** | Daily SpamHaus/Barracuda check | Alert ops, investigate | Immediate |
| **Renter account compromised** | Unusual login location, forwarding destination changed, > 1000 forwards/day | Quarantine account, require re-verification | Within 1 hour |
| **Phishing mail patterns** | Content scan + URL reputation check (VirusTotal) | Quarantine mail, log pattern | Within 1 hour |
| **Credential stuffing** | 50+ forwards to same external address in 24 hours | Pause account, notify renter | Within 4 hours |
| **New payment method on old account** | Stripe webhook: card changed without KYC re-check | Require re-verification | Before next billing cycle |

**Monitoring Dashboard (Internal):**
- Real-time feed of quarantined mails, rate-limited accounts, and RBL status.
- Weekly report: top abuse signals, renter accounts needing review.
- Daily: domain reputation score for all active domains.

---

#### 1.2e Abuse Escalation & Termination

**Tier 1: Automated Pause (24-hour hold)**
- Condition: Rate limit exceeded, suspicious content detected, or anomalous behavior.
- Action: Account forwarding paused automatically. Renter receives email: "Your account is under review due to [specific reason]. Reply to confirm this activity is expected."
- Resolution: Renter confirms, OR ops approves within 24 hours.

**Tier 2: Suspension (7-day hold)**
- Condition: Renter does not respond to Tier 1, OR second offense within 30 days.
- Action: Account suspended. Forwarding disabled. Renter cannot send mail via dashboard.
- Resolution: Renter submits appeal (requires detailed explanation). Ops reviews within 48 hours.

**Tier 3: Termination (Permanent)**
- Condition: Evidence of intentional abuse (phishing, credential stuffing, crypto scams). OR third offense within 90 days. OR domain added to RBL because of renter's activity.
- Action: Account terminated. All addresses under this renter's account deleted. Refund issued (minus abuse investigation cost, per ToS).
- Resolution: No appeal. Renter banned from platform.

**Graduated Escalation Example:**
- Day 1: Renter forwards 600 emails (exceeds 500 limit). Auto-pause. Ops notified.
- Day 2: Renter confirms "yes, we're running a recruitment campaign, this is expected." Limit increased to 750. Account resumed.
- Day 3: Renter tries 1000 forwards again, but now we see 95% are from unknown senders to the same recipient. Escalate to Tier 2. Suspend pending appeal.
- Day 5: Renter does not appeal. Account terminated (Tier 3).

**Legal/Compliance Note (for Ops Expert):**
- All escalations are logged with timestamps, evidence, and decision rationale.
- If renter disputes termination, we have a audit trail for potential legal defense.
- Abuse report (including anonymized renter data) is retained for 2 years per SOC 2 requirements.

---

#### 1.2f Domain Owner Communication Protocol

**Domain owners must be informed of abuse patterns to prevent platform liability and maintain trust.**

**Escalation Protocol:**

| Severity | Renter Behavior | Domain Owner Notification | Platform Action |
|----------|-----------------|--------------------------|-----------------|
| LOW | Single rate-limit pause | Monthly digest only | Monitor |
| MEDIUM | Tier 1 suspension (account paused) | Email alert + incident report | Investigate, possible Tier 2 |
| HIGH | Tier 2 suspension + domain reputation drop | Phone call + incident report + remediation plan | Tier 3 likely |
| CRITICAL | Domain added to RBL due to renter activity | IMMEDIATE phone call + incident report + temporary forwarding pause | Account terminated + offer domain inspection/recovery service |

**Domain Owner Rights:**
- Domain owners can request to review abuse reports affecting their domain (anonymized renter identity).
- Domain owners can request renter termination if documented abuse occurs.
- Domain owners are NOT charged platform fees for months when domain is blacklisted (remediation period).

**Platform Liability Prevention:**
- All notifications include explicit language: "We are taking corrective action. If your domain is listed on blacklists, here are the steps we recommend..."
- Platform provides free delisting support (write removal requests to RBL administrators).
- If domain cannot be recovered, platform offers to move renter base to new domain or provide full refund.

---

### 1.3 Remaining Risks (After Proposed Fix)

#### Risk 1: Renter Account Takeover (Medium Severity)
**What can still go wrong:**
- Attacker gains access to renter's platform account (weak password, phishing).
- Attacker changes forwarding destination to their own email.
- Attacker receives mail intended for renter, can view sensitive information.

**Residual exposure:**
- Platform does NOT control the renter's Gmail/Outlook inbox (only forwarding destination).
- If attacker redirects forwards to `attacker@gmail.com`, they now control what the renter sees.
- This is bad for the renter but does NOT damage domain reputation (all mail still routed correctly).

**Mitigation:**
- Mandatory 2FA for all accounts.
- Email notifications when forwarding destination changes.
- Rate limits on forwarding destination changes (max 1 per 24 hours, 3 per 30 days).
- Mandatory re-verification if login from new IP address detected.

**Residual**: Sophisticated attackers may still compromise accounts. Platform is not liable for renter credential compromise (standard ISP T&C).

---

#### Risk 2: Compromised Personal Email (Gmail/Outlook) (Medium Severity)
**What can still go wrong:**
- Attacker compromises renter's Gmail account.
- Attacker uses Gmail's "Send As" to send phishing/spam from the renter's vanity address.
- Gmail's infrastructure is blamed (fine), but the vanity address (on the domain) is still associated with abuse.
- If widespread (multiple renters' Gmail accounts compromised), domain reputation suffers.

**Residual exposure:**
- Platform cannot control whether Gmail users get hacked.
- If 10% of renters' Gmail accounts are compromised in a phishing campaign, domain reputation takes a hit (indirect).
- ISPs may start throttling legitimate mail from the domain if abuse complaints spike.

**Mitigation:**
- Send security advisories to all renters: "Protect your Gmail account; if compromised, it damages our domain."
- Offer opt-in renter education: YouTube video on 2FA setup, phishing detection, etc.
- Monitor Gmail's SMTP headers on inbound mail; if suspiciously high volume, flag the renter's account.

**Residual**: Small risk, but unfixable at platform level. Acceptable for MVP.

---

#### Risk 3: Outbound Mail Escaping Forwarding-Only Model (Low Severity)
**What can still go wrong:**
- Renter uses third-party SMTP client (e.g., NodeMailer, direct SMTP) to send directly from the vanity address without Gmail send-as.
- This requires credentials (SMTP username/password), which should not exist on a forwarding-only platform.

**Residual exposure:**
- If the platform accidentally generates SMTP credentials (e.g., API token leaked, or renter social engineers ops), they could bypass the send-as model entirely.
- Direct outbound mail from the domain would then revert to platform infrastructure reputation risk.

**Mitigation:**
- Enforce architectural constraint: NO SMTP credentials issued to renters, ever.
- All outbound mail flows ONLY through Gmail/Outlook APIs (no direct SMTP).
- Quarterly audit: verify no SMTP credentials exist in production database.

**Residual**: Very low if enforced. High impact if violated. Needs code review + architecture enforcement.

---

#### Risk 4: Domain Flagging Due to Forwarding Infrastructure Abuse (Medium Severity)
**What can still go wrong:**
- Many renters are spammers (even after onboarding checks).
- They all use the platform's forwarding infrastructure to send phishing emails to recipients (not from the domain, but inbound to collect responses).
- Recipients' ISPs see mail arriving from platform infrastructure → replies from recipients → next wave of phishing.
- ISPs blame platform infrastructure (SMTP relay), not the domain.
- But if the platform is seen as a "spam relay", it gets blacklisted, and ALL domains forwarded through it get collateral damage.

**Residual exposure:**
- Platform infrastructure (forwarding servers) could be blacklisted instead of individual domains.
- This would break forwarding for all domains simultaneously.
- This is the platform's problem (not domain owner's), but still catastrophic.

**Mitigation:**
- Run forwarding servers on dedicated IP ranges with strong reputation.
- Use separate IP pools per domain owner (so one owner's abuse doesn't contaminate another).
- Aggressive spam filtering on inbound mail (described in 1.2c).
- Monitor forwarding server reputation daily (send test mail to SpamTrap addresses).

**Residual**: Mitigated but not eliminated. Requires ongoing ops burden (dedicated IP management, reputation monitoring).

---

### 1.4 Required Assumptions

For the proposed forwarding-only model to work, **all of the following must be true:**

1. **Renters use Gmail/Outlook primarily.** If renters demand native outbound SMTP (full mailbox), forwarding-only fails. Must be post-MVP.

2. **ISPs respect Gmail's reputation, not the domain's.** If ISPs flag all mail from a domain based on send-as abuse, forwarding-only doesn't help. **Assumption: gmail.com and outlook.com signatures are trusted enough that one renter's abuse doesn't tank the domain.**

3. **Phone verification is accepted friction.** TOTP adds friction. Renters must accept this as the cost of MVP. If adoption tanks, the model breaks.

4. **Platform can enforce rate limits at the forwarding layer.** If renters can bypass rate limits (e.g., using multiple accounts), the model is broken. Requires good ops tooling.

5. **Abuse reports are actioned within 24 hours.** If a domain is added to RBL and the platform doesn't react, damage cascades. Requires 24/7 ops monitoring (initially manual, later automated).

6. **Domain owners accept renter anonymity.** Platform does not disclose which renter caused an abuse incident (privacy). Domain owners must accept this (or platform loses renter trust). **If domain owners demand renter identity, legal complexity increases.**

7. **Compliance with payment processor policies.** Stripe, Wise, and other payment processors have AUP clauses. They may freeze marketplace if abuse complaints spike. Platform must monitor Stripe webhook alerts for fraud/AUP violations.

---

## 2. LEGAL & OPERATIONS EXPERT PERSPECTIVE

### Role & Primary Question
**Legal & Operations Expert** assesses whether proposed T&S policies can be operationally enforced at scale, and what legal levers exist for compliance. Primary question: **Can the T&S policy be enforced without creating operational debt, or will corner-cutting turn abuse "features" into liability?**

---

### 2.1 Operational Enforceability Assessment

#### Policy vs. Practice Gap
The Architect's proposal (Section 1.2) is **sound in design but operationally challenging in execution.** Here's the breakdown:

| Control | Policy | Enforceability | Ops Cost | Notes |
|---------|--------|-------|----------|-------|
| **Email verification** | Double-opt-in | ✅ Automated | LOW | Trivial (standard SaaS tooling) |
| **Phone TOTP** | SMS or app 2FA | ✅ Automated | LOW | Standard auth library (e.g., Twilio, Auth0) |
| **Rate limit: 500 forwards/day** | Hard limit per account | ⚠️ Needs monitoring | MEDIUM | Requires real-time counter + redis cache |
| **Content filtering (SpamAssassin)** | Run on all inbound mail | ⚠️ Automated but CPU-heavy | HIGH | SpamAssassin is slow (~1s/email); need multiple instances or outsource to third party |
| **RBL monitoring (daily check)** | Check SpamHaus/CBL daily | ⚠️ Automated but fragile | MEDIUM | Simple API call, but need alerting infrastructure |
| **Renter account compromise detection** | Monitor login anomalies + forwarding destination changes | ⚠️ Requires data science | HIGH | Needs ML model or manual rules (false positive rate?) |
| **Abuse escalation (Tier 1/2/3)** | Automated pause, then manual review | ❌ Mostly manual | VERY HIGH | Tier 2/3 requires human judgment; SLA is 24–48 hrs |
| **Domain owner notifications** | Alert via email + phone for CRITICAL incidents | ⚠️ Partially manual | HIGH | CRITICAL alerts need phone call (on-call team required) |

---

#### Operational Burden: Year 1 Estimate

**Assumptions:**
- Platform launches with 10 domains, 500 renters.
- Scales to 50 domains, 5,000 renters by end of year.
- Abuse rate: 2–5% of renters attempt abuse at some point.

**Staffing Model:**

| Role | Year 1 Headcount | Annual Cost | Key Responsibilities |
|------|------------------|-------------|----------------------|
| **Trust & Safety Manager** | 1.0 FTE | $80K | Oversee abuse escalations, set policy, review appeals |
| **Ops Engineer (on-call)** | 0.5 FTE | $60K | Monitor RBL status, respond to domain owner alerts, escalate to T&S |
| **Automation Engineer** | 0.5 FTE | $70K | Build abuse detection dashboards, rate-limit rules, alerting |
| **Total T&S/Ops** | **2.0 FTE** | **$210K** | |

**Operational Debt Risk:**
- If abuse rate is higher than expected (5%+ of renters), staffing must increase to 3–4 FTE.
- If platform does not invest in automation (dashboards, alerting), manual review becomes unsustainable.
- If domain owner complaints are handled poorly, retention suffers (revenue risk > T&S cost).

---

#### Infrastructure Dependencies

**Software Stack Needed (Year 1):**
1. **Real-time rate-limit counter:** Redis or similar (to check 500 forwards/day limit at forwarding time).
2. **Content filtering appliance:** SpamAssassin + custom rules (or outsource to Mailgun/Postmark).
3. **RBL monitoring service:** SpamHaus API + Barracuda Centralized Reputation System (subscription ~$500/month).
4. **Abuse incident logging:** PostgreSQL table with audit trail (timestamps, escalation level, renter/domain owner, action taken).
5. **Alerting + monitoring:** PagerDuty or Opsgenie (for on-call rotation on critical RBL incidents).
6. **Identity verification service:** Stripe Radar or Fintech AML service (for phone TOTP + optional ID document scanning post-MVP).

**Outsourcing vs. In-House Trade-off:**
- **Outsource content filtering to Mailgun/Postmark:** Reduces Year 1 ops cost by ~0.5 FTE but increases mail processing cost (~$0.50 per renter per month in mail fees).
- **Outsource identity verification to Stripe Radar:** Reduces Year 1 ops cost (~$10K) but reduces control over policy (locked into Stripe's rules).
- **In-house RBL monitoring:** Worth building in-house (simple API, high business impact). Outsource would be overkill.

**Recommendation:** Outsource content filtering (to Mailgun) and identity verification (to Stripe Radar) in Year 1. Invest ops headcount in abuse escalation + domain owner communication (high-touch, requires judgment).

---

### 2.2 Legal Levers for Compliance Enforcement

#### Terms of Service (ToS) Backbone
The platform's ability to enforce abuse policy depends entirely on legal enforceability. **All controls in Section 1.2 must be encoded in ToS, or they are advisory only.**

**Required ToS Sections:**

1. **Acceptable Use Policy (AUP)**
   - Explicit prohibition on phishing, spam, malware, credential stuffing, and illegal activity.
   - Explicit statement: "Use of this platform for illegal activity waives your right to arbitration; we may pursue criminal referral."
   - Explicit language: "We may share abuse reports with law enforcement and domain owners (anonymized)."

2. **Account Termination Rights**
   - Platform retains right to terminate account immediately (without refund) if ToS violated.
   - Standard language: "We may, at our sole discretion, suspend or terminate your account if we reasonably believe it violates our policies."

3. **Limitation of Liability**
   - Platform is not liable for third-party (renter) abuse. Example: "We are not liable for spam, phishing, or other malicious activity committed by renters using our service."
   - Platform is not liable for domain owner's business losses due to renter abuse (they accepted the risk by enabling renters).
   - Domain owners indemnify platform for legal claims arising from renters' actions.

4. **Dispute Resolution**
   - Arbitration clause for renter disputes (faster than court, lower cost).
   - Class action waiver (so 100 renters can't band together to sue for wrongful termination).

5. **DMCA Compliance**
   - Copyright infringement: Platform responds to DMCA takedown notices within 24–48 hours.
   - Platform discloses repeat infringers (renter accounts) to rights holders.

**Enforcement Mechanism:**
- Every renter signs ToS at account creation (digital signature).
- Renter receives copy via email (audit trail).
- ToS is versioned; platform logs which version renter agreed to.
- If dispute arises, platform cites the specific ToS clause renter violated.

---

#### Practical Enforcement Actions

**On Account Termination:**
- Platform must issue written notice (email) stating reason and ToS clause cited.
- Example: "Your account has been terminated under AUP Section 3.1 (Phishing). We detected 47 phishing emails forwarded to your account from credential-stuffing sources."
- Renter can appeal within 14 days (async process). Platform has 5 days to review and respond.
- If appeal denied, platform retains right to pursue further action (e.g., report to payment processor, law enforcement if illegal activity suspected).

**On Refund Disputes:**
- If renter paid for an address and platform terminates account, renter demands refund.
- Platform's legal position: ToS Section 9 (Termination) explicitly states "Terminated accounts forfeit all prepaid fees."
- Payment processor (Stripe) will likely side with renter if refund request is filed as "unauthorized charge" (chargeback).
- Platform's defense: Provide email trail showing renter abused ToS, coupled with citation to ToS clause 9.
- **Outcome:** 60–70% of chargebacks are won if documentation is solid. 30–40% are lost (payment processor default).

**On Criminal Referral:**
- If abuse is criminal (e.g., large-scale phishing, credential stuffing for fraud), platform should file report with FBI's IC3 (Internet Crime Complaint Center).
- Platform must preserve evidence (email logs, IP addresses, payment info) for law enforcement.
- Does not require court order; platform's decision.
- **Benefit:** Demonstrates good faith to law enforcement. Protects platform's reputation (and domain owners' reputations). May result in law enforcement action against bad actors.
- **Risk:** Law enforcement may request account holder identity, which breaks renter privacy. Platform should disclose this risk in ToS.

---

#### Compliance with Payment Processors (Stripe, etc.)

**Risk:** Stripe's Acceptable Use Policy prohibits use for "illegal activity" and "high-risk verticals" (including email reselling in some cases). If Stripe detects abuse complaints, Stripe may freeze the platform's account without warning.

**Mitigation:**
1. Disclose the business model to Stripe upfront (not a hidden risk).
2. Implement robust abuse detection + ToS enforcement (documented above).
3. Monitor Stripe webhook events for fraud alerts (e.g., `charge.dispute.created`).
4. File dispute response within Stripe's window (48–72 hours). Provide evidence of ToS enforcement + abuse detection.
5. If chargeback rate exceeds 1% monthly, Stripe may increase reserve (hold funds) or terminate account.
   - **Mitigation:** Keep chargeback rate < 0.5% by properly documenting ToS enforcement.

---

#### Liability Walls: What the Platform Can (and Cannot) Claim

**Platform CAN claim immunity for:**
- Renter-to-third-party abuse (phishing, spam). **Reason:** Platform is not the originator; third party (renter) is. CDA Section 230 protects platforms from liability for user-generated content.
- Domain owner's business losses due to renter abuse. **Reason:** Domain owner accepted risk by agreeing to participate in two-sided marketplace. ToS must explicitly state this.

**Platform CANNOT claim immunity for:**
- Platform's own negligence (e.g., not monitoring RBL, failing to escalate abuse). **Reason:** These are platform's responsibility, not renter's.
- Failure to enforce its own policy (e.g., platform knows about phishing but doesn't terminate account). **Reason:** Negligent enablement.
- Data breach of renter PII (e.g., passwords, phone numbers leaked). **Reason:** Platform's duty of care.

---

### 2.3 Operational Feasibility: Go/No-Go

**Verdict: GO.** The forwarding-only model is operationally feasible with appropriate staffing + tooling investment.

**Required conditions:**
1. ✅ Platform invests in automation (Redis rate limiter, SpamAssassin, RBL monitoring).
2. ✅ Platform hires 2 FTE ops/T&S team in Year 1 (scalable to 4 FTE by Year 2 if abuse rate high).
3. ✅ Platform outsources content filtering to Mailgun (reduces ops burden, adds $0.50/renter/month cost).
4. ✅ ToS is legally sound and includes indemnification clause for domain owners.
5. ✅ Payment processor (Stripe) is kept informed; platform commits to maintaining < 0.5% chargeback rate.

**If any of these conditions is not met, escalate to Go/No-Go decision (Section 4).**

---

## 3. RED TEAMER FINDINGS

### Role & Primary Question
**Red Teamer** stress-tests the proposed solution by attempting to break it from adversarial perspectives: malicious renter, hostile domain owner, or operational/legal failure. Primary question: **Where does the design collapse under realistic adversarial behavior?**

---

### 3.1 Top 3 Ways a Malicious Renter Bypasses Controls

#### Attack 1: Multi-Account Credential Stuffing Ring (EASY)
**Setup:**
- Attacker creates 10 renter accounts across multiple premium domains (e.g., johnson.com, smith.com, johnson.ca).
- Each account passes onboarding (email verification + TOTP).
- Total setup cost: ~$50/month for 10 premium addresses.

**Attack:**
- Account 1 (`ceo@johnson.com`) receives forwarded emails and sells the forwarding list to a spam ring.
- Account 2 (`cfo@smith.com`) receives and sells to a second spam ring.
- Attacker cycles through all 10 accounts, each hitting rate limit (500 forwards/day).
- Combined throughput: 5,000 forwards/day across all accounts, spread across multiple domains.
- No single domain reputation is damaged (abuse is distributed).
- Spam ring re-sells the renter's addresses for bulk phishing campaigns (e.g., "Verified LinkedIn profiles @ premium domains").

**Why it works:**
- Onboarding checks email + TOTP, not identity. Attacker can use fake names.
- Rate limit is per-account, not per-attacker. Attacker simply scales across multiple accounts.
- Platform has no signal to link accounts (no IP-based clustering in Architect's proposal).

**Detection gap:**
- Each account appears legitimate in isolation (500 forwards/day is within acceptable range).
- Platform does not cluster accounts by payment method, email, IP address, or device fingerprint.
- Abuse is monetized downstream (via spam ring), not by the attacker directly.

**Ease of exploitation:** **EASY** — costs $50/month, 30 minutes to set up, no technical skill required.

---

#### Attack 2: Account Takeover via Phishing (MODERATE)
**Setup:**
- Attacker sends phishing email to renter: "Confirm your vanity email access [platform-login-link]".
- Attacker owns the link (malicious domain with typo: `myownemai1.com` instead of `myownemail.com`).
- Renter clicks link, enters username + password. Attacker captures credentials.

**Attack:**
- Attacker logs into renter's account with stolen credentials.
- Attacker changes forwarding destination to attacker's own email (`attacker@gmail.com`).
- Attacker now receives all inbound mail intended for the renter.
- Attacker also changes the recovery email/phone number (if possible) to lock out the renter.
- Attacker uses the renter's account for credential stuffing (see Attack 1).

**Why it works:**
- Renter is not tech-savvy (typical vanity email user). Falls for phishing.
- Platform does not monitor for unusual login activity initially (no machine learning in Year 1).
- Platform does not require re-verification when login IP changes (assumed in Architect's proposal, but not enforced).
- Forwarding destination change is not rate-limited (assumption: domain owner should monitor this).

**Detection gap:**
- Platform receives notification: "Forwarding destination changed for renter@platform". But who reviews this? Domain owner? Renter? No one by default.
- If renter is compromised, they likely won't report the change immediately.
- By the time platform detects, attacker has 24–72 hours of access to renter's mail.

**Ease of exploitation:** **MODERATE** — requires phishing email + setup, but success rate is 5–10% (typical phishing CTR). If attacker targets 100 renters, 5–10 compromises are expected.

---

#### Attack 3: SMTP Smuggling / Mail Injection (HARD)
**Setup:**
- Attacker studies the platform's inbound mail server (MTA) to find SMTP vulnerabilities.
- Attacker sends specially crafted SMTP commands to inject mail that looks like it originated from a different renter's address.
- Example: Attacker sends mail to `bill@johnson.com`, but forges the SMTP `From:` header to be `boss@acme.com`, then sends to `phishing-target@gmail.com`.

**Attack:**
- Platform's mail server routes the mail to `bill@johnson.com` (correct).
- Mail is forwarded to `bill@gmail.com` (renter's inbox).
- Renter sees mail from `boss@acme.com` (in Gmail).
- Renter thinks it's from their real boss, clicks malicious link.
- Phishing attack succeeds because renter trusts the sender.

**Why it works:**
- SMTP allows arbitrary header forgery (by design). Attacker exploits this.
- Platform's inbound server does not validate SMTP `From:` against the `To:` recipient.
- Mail filtering (SpamAssassin) does not catch header forgery (it's not spam, it's a legitimate mail header).

**Detection gap:**
- Platform's forwarding logic is "receive on port 25, forward to renter's Gmail". No header validation.
- Gmail's spam filter might catch it, but not guaranteed.
- By the time platform detects, phishing campaign has already succeeded.

**Ease of exploitation:** **HARD** — requires SMTP knowledge, but tools exist (e.g., swaks, sendmail with custom headers). Difficulty = 6/10 for skilled attacker.

---

### 3.2 Top 3 Ways a Domain Owner Exploits the System (T&S Purposes)

#### Exploit 1: Framing a Renter to Disable Them (EASY)
**Setup:**
- Domain owner is angry at a renter (dispute over money, ToS interpretation, etc.).
- Domain owner wants to force the renter off the platform without going through appeal process.

**Attack:**
- Domain owner sends phishing email to their own domain's address (e.g., `bill@johnson.com`).
- Domain owner uses a public phishing template (credentials harvesting page).
- Domain owner's mail is forwarded to renter's inbox (by platform).
- Platform's content filter (SpamAssassin) flags it as phishing.
- Platform quarantines the mail, then investigates renter's account.
- Platform sees: "Renter received phishing mail, likely participated in phishing campaign".
- Platform suspends renter's account (Tier 2) pending appeal.

**Why it works:**
- Domain owner controls the domain. Can send mail to any address on the domain.
- Platform's content filter does not know who originated the phishing (domain owner or external attacker).
- Platform must assume renter was the target or participant.
- Appeal process is 24–48 hours, during which renter's address is disabled (revenue lost).

**Detection gap:**
- Platform does not correlate "phishing mail received" with "phishing mail sent by domain owner".
- Platform does not require domain owner to notify before taking disciplinary action against renter.
- Renter is punished first, investigated second.

**Ease of exploitation:** **EASY** — domain owner can send phishing mail to any address, costs nothing, takes 5 minutes.

---

#### Exploit 2: Extracting Renter Data via Abuse Reports (MODERATE)
**Setup:**
- Platform's T&S policy (Section 1.2f) states: "Domain owners can request to review abuse reports affecting their domain (anonymized renter identity)."
- Attacker (with access to domain registrar) temporarily takes control of a popular domain (e.g., `johnson.com`).
- Attacker is now the domain owner in platform's eyes.

**Attack:**
- Attacker requests abuse reports for domain `johnson.com`.
- Platform provides report: "Renter account at 192.168.x.x received 500 phishing emails from accounts associated with botnet Y."
- Report includes: timestamps, sender addresses, renter's forwarding destination, volume of mail.
- Attacker now has metadata about all renters on the domain (anonymized, but linked to IP/forwarding destination).
- Attacker correlates forwarding destinations with LinkedIn/Twitter profiles (social engineering followup).
- Attacker then targets renters for secondary attacks (phishing, credential stuffing, extortion).

**Why it works:**
- "Anonymized" renter identity is not truly anonymous (IP address, forwarding destination, mail volumes are PII).
- Domain owner can be impersonated if domain registrar security is weak.
- Platform assumes domain owner is trustworthy; no further verification.

**Detection gap:**
- Platform does not verify domain owner's identity beyond domain control (DNS TXT record).
- Platform shares detailed forensic data that could be re-identified.
- No audit log of which domain owner requested which reports (or when).

**Ease of exploitation:** **MODERATE** — requires domain registrar compromise or social engineering, but 10–20% of domain registrars have weak security.

---

#### Exploit 3: Driving Down Competitors' Domains via RBL Listing (HARD)
**Setup:**
- Domain owner A and Domain owner B are competitors (e.g., both rent premium domain addresses).
- Domain owner A wants to damage Domain owner B's domain reputation.

**Attack:**
- Domain owner A bribes a renter on Domain owner B's domain (or creates a fake renter account).
- Renter (or fake account) receives forwarded mail, but the mail is actually spam sent by Domain owner A (not external).
- Domain owner A sends 10,000 phishing emails to renter's forwarding destination (@gmail.com).
- Gmail flags the mail as spam; some mail bounces.
- Bounces are sent back to `johnson.com` (Domain owner B's domain).
- Volume of bounces causes mail server to be flagged by SpamHaus.
- `johnson.com` is added to RBL.
- All renters on `johnson.com` lose deliverability.
- Domain Owner B's revenue drops 80%.

**Why it works:**
- Platform's abuse detection (Section 1.2d) monitors renter behavior, not originator behavior.
- Domain Owner A's spam is forwarded through the platform, but A is external.
- Platform does not trace mail back to A (no forensics).
- By the time Domain owner B's domain is on RBL, damage is done.
- Platform's response is reactive (remove renter, delist domain), not preventive.

**Detection gap:**
- Platform does not detect that mail is being *sent to* the renter at scale, only that renter is *receiving* it.
- Platform does not correlate bounce patterns with external attack campaigns.
- RBL listing is the first signal, at which point escalation is already critical.

**Ease of exploitation:** **HARD** — requires sophisticated attack, knowledge of mail systems, and coordination with external spam ring. But possible for determined attacker.

---

### 3.3 Estimated Exploitation Rates

| Attack | Perpetrator | Ease | Likelihood (% renters/domains affected) | Detection Time | Impact |
|--------|-------------|------|----------------------------------------|-----------------|--------|
| Attack 1: Multi-account ring | Malicious renter | EASY | 2–5% | 7–30 days | Revenue leak to spam ring |
| Attack 2: Phishing takeover | Malicious renter | MODERATE | 1–3% | 1–7 days | Renter data compromise |
| Attack 3: SMTP smuggling | Malicious renter | HARD | <1% | 24–48 hours | Renter phishing |
| Exploit 1: Framing renter | Domain owner | EASY | 5–10% | <1 day | False suspension of renter |
| Exploit 2: Data extraction | Domain owner/external | MODERATE | 1–3% | 14–30 days | Renter PII leak |
| Exploit 3: RBL sabotage | Domain owner/external | HARD | <1% | 1–7 days | Domain reputation destruction |

---

### 3.4 Red Teamer Recommendation

**Verdict: The proposed architecture is vulnerable to automated abuse rings (Attack 1) and domain owner retaliation (Exploits 1–2). These must be addressed before MVP launch.**

**Required changes:**
1. **IP-based account clustering:** Link multiple renter accounts by IP address, payment method, and device fingerprint. Escalate if clustering detected.
2. **Forwarding destination audit trail:** Log all forwarding destination changes. Require re-verification if destination changes within 24 hours of account creation.
3. **Domain owner identity verification:** Require phone call + ID verification for domain owners. Re-verify annually.
4. **Renter-to-renter alerts:** Notify renter if their forwarding destination is about to be changed. Require 24-hour confirmation period.
5. **Mail originator forensics:** For high-volume abuse, trace inbound mail back to originator domain (SMTP headers). Detect if mail is coming from external attacker (not renter).
6. **RBL trend monitoring:** Instead of waiting for RBL listing, monitor bounce rates and abuse complaints *per domain*. Alert domain owner if trend is negative.

**Post-MVP roadmap:**
- Machine learning model to detect coordinated abuse (multiple accounts from same attacker).
- Advanced email forensics (DMARC/SPF/DKIM analysis) to detect mail forgery.
- Renter identity matching (cross-check against LinkedIn, TrustScore data) to reduce account creation friction while raising attacker friction.

---

## 4. SYNTHESIS & RECOMMENDATION

### 4.1 Approved Abuse-Prevention Policy

**Version:** 1.0  
**Status:** Locked (Ready for Continuity Workshop)  
**Effective Date:** MVP Launch (TBD)

---

#### MVP Email Flow (FINAL)

```
┌──────────────────────────────────────────────────────────────┐
│ RENTER SIGNS UP                                              │
├──────────────────────────────────────────────────────────────┤
│ 1. Renter provides: email, name, phone number                │
│ 2. Platform verifies: email (OTP), phone (TOTP/SMS)          │
│ 3. Renter selects: available vanity address (e.g., c-level) │
│ 4. Renter accepts: ToS + AUP + Privacy Policy                │
│ 5. Renter sets: forwarding destination (personal Gmail/Outlook)│
│ 6. Platform conducts: KYC check (name vs. payment processor) │
│ 7. Status: ACTIVE (mail forwarding enabled)                  │
└──────────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────┐
│ SENDER SENDS MAIL TO RENTER'S VANITY ADDRESS                 │
├──────────────────────────────────────────────────────────────┤
│ 1. Sender writes email to: bill@johnson.com                  │
│ 2. Sender's mail server queries DNS for johnson.com MX       │
│ 3. DNS returns: mail.myownemail.com (platform's inbox)       │
│ 4. Sender's server connects to platform SMTP relay           │
│ 5. Platform receives mail, logs headers + body               │
└──────────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────┐
│ PLATFORM FILTERS & FORWARDS MAIL                             │
├──────────────────────────────────────────────────────────────┤
│ 1. Run SpamAssassin + custom rules on mail                   │
│    - Check: phishing keywords, malware signatures            │
│    - Check: sender IP on RBL (SpamHaus)                      │
│    - Action: Quarantine if score > 5.0 (spam threshold)     │
│ 2. Check rate limits (renter account):                       │
│    - Forwards today: 523 (exceeds 500 limit!)                │
│    - Action: Pause account, send alert to renter + ops      │
│ 3. If passed: Forward mail to renter's Gmail via SMTPS       │
│    (encrypted tunnel; platform does NOT store mail)          │
│ 4. Log: timestamp, sender, recipient, forwarding status      │
└──────────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────┐
│ RENTER REPLIES VIA GMAIL SEND-AS                             │
├──────────────────────────────────────────────────────────────┤
│ 1. Renter opens Gmail, clicks "Reply" to original mail       │
│ 2. Gmail UI shows: "From: bill@johnson.com (send-as)"        │
│ 3. Renter composes reply                                     │
│ 4. Gmail signs reply with Gmail's DKIM/SPF keys              │
│ 5. Gmail sends reply from its own SMTP infrastructure        │
│    (NOT platform; NOT johnson.com servers)                   │
│ 6. Reply header: From=bill@johnson.com, DKIM-Signed by Gmail │
│ 7. Platform infrastructure: ZERO involvement in reply        │
│ 8. Recipient receives reply; Gmail's reputation intact       │
└──────────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────┐
│ KEY: Domain reputation is PRESERVED                          │
├──────────────────────────────────────────────────────────────┤
│ - johnson.com MX points to platform (inbound only)           │
│ - johnson.com SPF does NOT include platform SMTP servers     │
│   (gmail.com is NOT johnson.com; mail signed by Gmail)       │
│ - Renter abuse → Gmail reputation hit, NOT johnson.com       │
│ - Platform forwards mail correctly → johnson.com stays clean │
└──────────────────────────────────────────────────────────────┘
```

---

#### Onboarding Friction (LOCKED)

| Step | Requirement | Timeline | Who Verifies | Action on Fail |
|------|-------------|----------|--------------|----------------|
| 1 | Email verification (OTP) | <1 min | Automated | Retry, max 3 attempts |
| 2 | Phone verification (TOTP via SMS or app) | <1 min | Automated | Retry, max 3 attempts |
| 3 | Name + address provided | <1 min | Renter input | Must provide valid info |
| 4 | KYC check (name vs. Stripe) | 5–10 min | Automated | Flag for manual review |
| 5 | Manual review (if KYC mismatch) | 24–48 hrs | Ops team | Approve or request docs |
| 6 | ToS acceptance | <1 min | Renter signature | Cannot proceed without |
| 7 | Forwarding destination set | <1 min | Renter input | Must be valid Gmail/Outlook |

**Total time to activation:** 5–10 min (automated path) OR 24–48 hrs (manual review path).

**Friction level:** MEDIUM (acceptable for MVP, not a blocker for adoption).

---

#### Rate Limits (LOCKED)

**Per-Renter Inbound:**
- **500 forwards/day** (hard limit; pauses on exceeding)
- **200 unique senders/day** (soft alert at 150, pause at 200)
- **30% bounce rate** (soft alert at 20%, pause at 30%)

**Per-Renter Outbound (via Gmail Send-As):**
- **No platform-enforced limit.** Gmail's limit applies (100–300 recipients/day, Gmail's policy).

**Per-Domain Inbound:**
- **10,000 forwards/day aggregate** (soft alert, no hard limit; triggers RBL monitoring)

**Escalation:**
- Renter account paused: ops notified within 5 min.
- Ops reviews: account confirmed abusive or innocent (within 1 hr).
- Resolution: limit increased, or account escalated to Tier 2.

---

#### Abuse Escalation (LOCKED)

**Tier 1: 24-Hour Pause (Automated)**
- Condition: Rate limit exceeded OR suspicious content detected.
- Action: Forwarding paused. Renter receives email: "Your account is under review due to [reason]. Reply to confirm this activity is expected."
- Resolution: Renter confirms (increase limit), OR ops approves (resume), OR 24 hrs elapsed (auto-resume with reduced limit).

**Tier 2: 7-Day Suspension (Manual Review)**
- Condition: Renter does not respond to Tier 1 OR second offense within 30 days.
- Action: Account suspended. Renter cannot receive mail. Ops assigns case number.
- Resolution: Renter appeals within 7 days (written explanation). Ops reviews. Approve resume or escalate to Tier 3.

**Tier 3: Permanent Termination (Decision Required)**
- Condition: Confirmed phishing/phishing/credential stuffing OR third offense within 90 days OR domain blacklisted due to renter.
- Action: Account terminated. All addresses deleted. Refund issued (minus abuse investigation cost).
- Resolution: No appeal. Renter banned.

**Appeal Process (Tier 2 only):**
- Renter submits written appeal to abuse@myownemail.com.
- Ops team assigned case number. Review within 5 days.
- Decision: approve resume, or escalate to Tier 3.
- If escalated to Tier 3, no further appeal available.

---

### 4.2 Concrete Monitoring & Detection Rules

**Real-Time Rules (Trigger Tier 1 Pause):**

1. **Rate limit exceeded:** Forwards > 500/day → pause account.
2. **Phishing content:** Mail contains phishing keywords + URL shortener + credential form → quarantine, alert ops.
3. **RBL sender:** Inbound from IP on SpamHaus PBL → alert ops, quarantine mail.
4. **Credential stuffing pattern:** 50+ forwards to same external address in 1 hour → pause account.
5. **Forwarding destination changed:** Changed within 24 hrs of account creation → require re-verification.

**Daily Rules (Alert Ops):**

1. **Domain RBL status:** Check SpamHaus SBL/CBL/PBL for all active domains. If any listed, CRITICAL alert.
2. **Domain bounce rate:** If aggregate bounce rate > 10%, alert domain owner + ops.
3. **Renter account compromise:** If login from new IP + forwarding destination change within 2 hrs, Tier 1 pause + 2FA re-verification.

**Weekly Rules (Report):**

1. **Abuse pattern summary:** List top 10 abuse triggers, count, severity.
2. **Renter retention:** Which renters have escalated? Which appealed? Success rate?
3. **Domain health:** Which domains have highest abuse rate? Are they at RBL risk?

---

### 4.3 Required Operational Setup

**Staffing (Year 1):**
- Trust & Safety Manager (1.0 FTE): $80K
- Ops Engineer on-call (0.5 FTE): $60K
- Automation Engineer (0.5 FTE): $70K
- **Total:** 2.0 FTE, $210K annual

**Infrastructure:**
- Redis instance (rate limit counter): $50/month
- Mailgun (content filtering + outbound mail relaying): ~$0.50 per renter per month
- SpamHaus API + Barracuda CRS (RBL monitoring): $500/month
- PagerDuty (on-call alerting): $100/month
- PostgreSQL (abuse logging): included in main DB

**Tooling:**
- Abuse dashboard (internal): 40 engineering hours (Year 1)
- RBL alerting automation: 20 engineering hours (Year 1)
- Renter appeal portal (self-service): 30 engineering hours (Year 2)

---

### 4.4 Decision Summary: Trust & Safety

| Question | Answer | Confidence |
|----------|--------|------------|
| **Can domain reputation be protected?** | Yes, via forwarding-only architecture. | HIGH |
| **Is onboarding friction acceptable?** | Yes, email + phone TOTP is standard. | HIGH |
| **Can abuse be detected?** | Yes, with rate limits + content filtering. | MEDIUM |
| **Can abuse be escalated fairly?** | Yes, with documented appeal process. | MEDIUM |
| **Is operational feasibility justified?** | Yes, 2 FTE for Year 1 is sustainable. | HIGH |
| **Are legal levers sufficient?** | Yes, if ToS is drafted correctly. | HIGH |
| **Can red team attacks be mitigated?** | Mostly; Attack 1 (multi-account ring) and Exploit 1 (framing) remain risks. Require Year 1 hardening. | MEDIUM |

**Recommendation: PROCEED to Continuity Workshop with forwarding-only architecture locked in.**

---

## 5. OPEN QUESTIONS FOR WORKSHOPS 2–4

### Questions for Continuity Workshop (Step 2)
1. **Domain escrow:** Who holds the domain during the rental period? Can the platform force renewal if owner stops paying?
2. **Renter protection:** If domain owner pulls the domain, how are renters compensated? Is there a "domain insurance" fund?
3. **Lease term:** Should renters have minimum lease length (e.g., 12 months) to justify investment in email reputation?
4. **Revenue split enforcement:** How does Stripe Connect enforce 50/50 split? What if domain owner disputes payout?

### Questions for Red Team Assault (Step 3)
1. **Continuity attacks:** Can domain owner intentionally degrade domain reputation to force renters off, then re-lease at higher rate?
2. **Payment fraud:** Can renter create multiple accounts, dispute charges, get refunds, then repeat?
3. **Legal jurisdiction:** If renter is in country A, domain owner in country B, and platform in country C, whose laws apply?

### Questions for Go/No-Go Decision (Step 4)
1. **Market size:** How many domain owners and renters are needed for unit economics to work?
2. **Churn rate:** What's the acceptable renter churn rate? (Market benchmark: 5–10% monthly for SaaS.)
3. **Support overhead:** How much human support is needed per renter per month?
4. **Profitability timeline:** When does platform achieve positive unit economics?

---

## APPENDIX: T&S Policy Checklist (Implementation)

**Pre-MVP Launch (2–4 weeks before):**
- [ ] ToS drafted by legal counsel (indemnification, arbitration, DMCA clauses).
- [ ] Acceptable Use Policy finalized.
- [ ] Rate limit rules coded (Redis + forwarding logic).
- [ ] Spam filtering (SpamAssassin) configured and tested.
- [ ] RBL monitoring (SpamHaus API) set up.
- [ ] Abuse dashboard (internal) deployed.
- [ ] On-call rotation (T&S manager + ops engineer) scheduled.
- [ ] Renter appeal portal (basic email-based) operational.

**First Month (MVP):**
- [ ] Monitor abuse rate (target: < 2% of renters).
- [ ] Test Tier 1/2/3 escalation process with 10–20 test cases.
- [ ] Log all abuse incidents (for legal defense).
- [ ] Daily: check RBL status for all domains.
- [ ] Weekly: summarize abuse patterns to founder.

**Months 2–3 (Scale Phase):**
- [ ] If abuse rate > 2%, increase ops team to 3 FTE.
- [ ] If false positive rate on content filtering > 5%, tune SpamAssassin rules.
- [ ] If renter churn > 10%, investigate if abuse escalation too aggressive.

---

## Final Verdict

**The forwarding-only architecture with hardened onboarding is RECOMMENDED for MVP.** It reduces domain reputation risk by ~90% while maintaining acceptable UX friction. The model is operationally feasible with 2 FTE and standard tooling. Legal enforceability is high if ToS is well-drafted.

**The primary risks (multi-account abuse rings, domain owner retaliation) are real but mitigable with Year 1 hardening (IP clustering, forwarding audit trail). These should not block MVP launch.**

**Proceed to Continuity Workshop with this architecture locked in.**

---

**Memo Prepared By:** Trust & Safety Architecture Workshop  
**Ready For:** Continuity Workshop (Step 2)  
**Next Decision Point:** Go/No-Go after Step 4 (Red Team Assault + Legal Review)
