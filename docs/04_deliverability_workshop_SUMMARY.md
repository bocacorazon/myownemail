# Deliverability Workshop — Executive Summary

## The Core Problem
A single renter sending spam/phishing from `bill@johnson.com` blacklists the entire domain for all other renters. ISP blacklists (SpamHaus, Barracuda, Gmail, Outlook) don't distinguish between renters—they flag the whole domain.

## The Decision: Forwarding-Only MVP

| Dimension | Forwarding-Only | Full SMTP (Post-MVP) |
|-----------|-----------------|---------------------|
| **Outbound mail origin** | Gmail/Outlook (not platform) | Platform SMTP servers |
| **Domain reputation risk** | ~10% (low) | ~100% (critical) |
| **User UX** | Good (standard send-as) | Great (full mailbox) |
| **Onboarding friction** | Medium (phone TOTP) | High (ID verification) |
| **Abuse surface area** | Inbound phishing risk | Outbound spam ring risk |
| **MVP timeline** | Ready now | 6–12 months post-MVP |

## Architecture at a Glance

```
INBOUND:  Sender → DNS MX → Platform inbox → Content filter → Gmail forward ✓
OUTBOUND: Renter reply → Gmail Send-As → Gmail SMTP (not platform) ✓

KEY: Platform infrastructure never originates mail. Gmail's reputation absorbs 
any abuse, not johnson.com's reputation.
```

## Locked Decisions

1. ✅ **MVP Email Flow:** Forwarding-only + Gmail send-as (no native outbound)
2. ✅ **Onboarding:** Email verification + phone TOTP (acceptable friction)
3. ✅ **Rate Limits:** 500 forwards/day per renter (detects industrial abuse)
4. ✅ **Domain Protection:** Proactive RBL monitoring + reactive escalation

## Abuse Prevention

| Control | Status | Cost |
|---------|--------|------|
| **Rate limiting** | 500 forwards/day | Redis (~$50/mo) |
| **Content filtering** | SpamAssassin via Mailgun | $0.50/renter/mo |
| **RBL monitoring** | Daily SpamHaus check | $500/mo |
| **Account escalation** | Tier 1/2/3 (pause→suspend→terminate) | 2 FTE ops ($210K/yr) |
| **Abuse forensics** | Log headers, audit trail | Included in DB |

## Operational Overhead

**Year 1 Team:**
- Trust & Safety Manager (1.0 FTE): $80K
- Ops Engineer (on-call): $60K
- Automation Engineer: $70K
- **Total:** 2.0 FTE, $210K + infrastructure

## Red Team Findings

| Attack | Actor | Ease | Mitigation | Residual Risk |
|--------|-------|------|-----------|----------------|
| Multi-account abuse ring | Malicious renter | EASY | IP clustering (Year 1) | 2–5% renters affected |
| Phishing account takeover | Malicious renter | MODERATE | Forwarding audit trail | 1–3% accounts compromised |
| SMTP smuggling | Malicious renter | HARD | Mail forensics | <1%, low probability |
| Framing renter (domain owner) | Malicious domain owner | EASY | Renter re-verification | 5–10% false suspensions |
| Data extraction (domain owner) | Domain owner/external | MODERATE | ID verification | 1–3% renter PII leaks |
| RBL sabotage (domain owner) | Domain owner/external | HARD | Bounce monitoring | <1%, catastrophic if happens |

## Legal Enforceability

✅ **Can be enforced at scale** with:
- Clear ToS + Acceptable Use Policy (required)
- Documented escalation process (audit trail)
- Indemnification clause (domain owner accepts renter risk)
- Arbitration clause (faster than litigation)
- CDA Section 230 protection (platform not liable for user content)

## Remaining Risks (Acceptable for MVP)

1. **Renter Gmail compromise:** If 10% of renters' Gmail accounts are hacked, domain suffers (indirect). Mitigated by user education.
2. **Multi-account abuse rings:** 2–5% of renters will try. Requires Year 1 hardening (IP clustering).
3. **False suspensions (domain owner retaliation):** 5–10% of renters may be wrongly escalated. Mitigated by clear appeal process.

## Path Forward

**Next Workshop:** Continuity (Step 2) — Domain escrow, renter protection, rug-pull risk

**Success Criteria for MVP:**
- < 2% of renters escalated to Tier 2+ per month
- 0 domains added to RBL within 90 days (or < 1 if domain abuse occurs)
- Renter activation: 5–10 min median time
- Support load: < 0.5 hrs per renter per month

## Confidence Level

- **Architecture soundness:** HIGH
- **Operational feasibility:** HIGH
- **Legal enforceability:** HIGH
- **Red team mitigation:** MEDIUM (attacks 1 & 4 remain risks; fixable in Year 1)

## Verdict

**✅ PROCEED to MVP with forwarding-only architecture.** 

Abuse prevention is achievable; operational burden is sustainable; legal levers are in place. Domain reputation can be protected if discipline is maintained. No blocker identified for MVP launch after Continuity Workshop approval.
