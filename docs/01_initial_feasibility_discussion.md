# Initial Feasibility Discussion

> **Status note (2026-04-21):** This document was revised after a framework critique. Original conclusions have been reframed as **hypotheses pending validation**. Nothing below is a decision until explicitly validated in a workshop.

## 1. The Concept (Hypothesis)

A two-sided marketplace for vanity email addresses. Domain owners (e.g., `johnson.com`) bring their domains to the service, allowing end-users (e.g., `bill@johnson.com`) to rent/subscribe to a vanity email address. This is intended to let domain owners monetize valuable generic or family-name domains and let end-users obtain identity-grade email addresses that would otherwise be unreachable.

**This framing is supply-centric.** It describes how owners monetize assets, not what problem renters are hiring the product to solve. The demand-side "job to be done" is still unresolved and must be defined in the Demand & Positioning Workshop.

## 2. Candidate Renter Jobs-To-Be-Done (Unvalidated)

These are hypotheses about *why someone would pay* for a rented vanity address. They must be tested:

- **Identity / status** — "I want an email that signals who I am."
- **Professional credibility** — "I want to look more established than a Gmail address allows."
- **Privacy / compartmentalization** — "I want an identity layer without tying it to my real mailbox."
- **Surname / family match** — "I want `bill@johnson.com` because my name is Bill Johnson."
- **Creator / personal branding** — "I want an address that matches my public handle."
- **Novelty / fandom** — "I want `fan@[celebrity].com` because it's fun."

Each job implies a **different product, different pricing, different positioning, and possibly a different architecture.** Picking the wrong job means picking the wrong product.

## 3. Market Research & Existing Landscape

- **Mail.com model:** Platform owns premium domains and lets users pick from them. Supply is controlled, not brokered.
- **Web3 / crypto model:** Unstoppable Domains, ENS. Largely outside traditional DNS and SMTP.
- **Email aliasing / forwarding tools:** SimpleLogin, AnonAddy, Cloudflare Email Routing, ForwardEmail.net. Free or cheap; privacy-focused; not identity marketplaces.
- **Vanity domain registration:** Users just buy a domain themselves via Namecheap/Porkbun and use Google Workspace or Fastmail. This is the primary substitute and it is cheap and well-understood.
- **Hypothesized gap:** No mainstream platform lets private domain owners securely rent out addresses for a recurring revenue split to end-users.

**Unvalidated assumption:** That the "gap" is a gap because no one has done it, rather than because no viable demand exists.

## 4. Major Risk Dimensions

### 4.1 Domain Reputation Risk (Supply-side technical risk)
A renter sending spam or phishing can blacklist the entire domain, harming all other renters and the owner. *Addressed in the Deliverability Workshop.*

### 4.2 Rug-Pull Risk (Supply-side continuity risk)
A domain owner stops renewing, sells the domain, or intentionally withdraws, stranding all renters. *Addressed in the Continuity Workshop.*

### 4.3 Demand Risk (Customer-side risk)
No one wants this enough to pay for it, or willingness-to-pay is below break-even once abuse/support/CAC are factored in. *Addressed in the Demand & Positioning Workshop.*

### 4.4 Liquidity / Matching Risk (Marketplace risk)
Demand is fragmented across highly specific (domain × local-part) combinations. Most domains will have thin demand. Most renters will only want a tiny subset of domains. Classic marketplace chicken-and-egg, made worse by fragmentation. *Addressed in the Supply Acquisition and Marketplace Economics Workshops.*

### 4.5 Unit Economics Risk
Whether the offer can be priced to cover CAC, abuse handling, support, fraud, payments, and legal — with enough left over for a credible owner revenue share. *Addressed in the Marketplace Economics Workshop.*

### 4.6 Platform Dependency Risk
The forwarding-only approach leans on Gmail send-as, Mailgun deliverability, and Stripe Connect behavior. If any of those tighten policy, the product may become unviable. *Addressed throughout; flagged as a standing risk for Red Team.*

### 4.7 Privacy & Security
Domain owners must not be able to read renters' emails. Architecture must guarantee owners only point MX records, with no admin access to mailboxes. *Addressed in the Deliverability Workshop.*

### 4.8 Regulatory Risk
Email is heavily regulated: CAN-SPAM, GDPR, GLBA (if financial forwarding), COPPA (if minors), and mailbox-provider AUP. A vanity marketplace may attract impersonation and trademark disputes. *Addressed in the Continuity and Red Team Workshops.*

## 5. Candidate Implementation Architectures

These are **architecture candidates**, not a ranked recommendation. The right choice depends on the winning offer from the Demand Workshop.

- **Option A — API / Headless:** Use Mailgun, Postmark, Amazon SES for routing. Full inbound + outbound SMTP control.
- **Option B — White-label Reseller:** Partner with Titan Email, ResellerClub, etc. for standard mailboxes.
- **Option C — Forwarding-only:** Use ForwardEmail.net, Cloudflare routing, or equivalent. Outbound via user's existing mailbox (e.g., Gmail send-as).

Each option implies different positioning ("real mailbox" vs. "identity layer" vs. "privacy-first alias"), different abuse exposure, and different unit economics. Architecture must follow offer, not precede it.

## 6. Revenue Model (Hypothesis Only)

A revenue-share model, initially sketched at **50/50** between platform and domain owner, routed via Stripe Connect.

**This is a placeholder.** The 50/50 split is arbitrary and has not been economically modeled. The platform bears CAC, abuse handling, support, fraud losses, payments complexity, and legal exposure. The domain owner bears asset and reputation risk. These costs are not symmetric and there is no reason to assume a symmetric split is correct. The Marketplace Economics Workshop will produce a defended take-rate.

## 7. What This Document Is Not

- Not a commitment to forwarding-only.
- Not a commitment to a 50/50 split.
- Not a customer segmentation.
- Not a market sizing.
- Not an MVP spec.

It is a **starting frame**. The workshops will convert each hypothesis above into either a validated decision or a kill criterion.
