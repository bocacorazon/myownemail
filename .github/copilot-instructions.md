# Copilot Instructions

## Project Overview

**Vanity Email Marketplace** — a two-sided platform where domain owners (e.g., `johnson.com`) list their domains, and end-users rent vanity email addresses (e.g., `bill@johnson.com`). Revenue is split 50/50 via Stripe Connect.

This repository is currently in the **pre-code, system design phase**. The philosophy is "System-first, execution later": all existential business risks must be solved on paper before any technical implementation begins.

## Current Phase

The 7-step validation workshop defined in `docs/02_feasibility_validation.md`. Offensive (demand/supply/economics) workshops run before defensive (safety/continuity/red-team) workshops — "demand before defense."

1. **Demand & Positioning** — ICP, WTP, positioning, substitutes, pricing hypotheses
2. **Supply Acquisition** — owner ICP, listing policy, acquisition channels
3. **Marketplace Economics** — unit economics, take rate, liquidity thresholds
4. **Deliverability** — abuse prevention and email architecture (provisional draft exists at `04_deliverability_workshop.md`; revisit after W1–W3)
5. **Continuity** — rug-pull protection, escrow, regulatory posture
6. **Red Team Assault** — stress-test the full system against adversarial behavior
7. **Go / No-Go Decision** — final evaluation before moving to technical execution

No code exists yet. Contributions at this stage are design documents.

## Key Concepts & Terminology

- **Domain Reputation Problem**: A renter sending spam blacklists the entire domain for all users. A primary technical risk.
- **Rug Pull Risk**: A domain owner stops renewing their domain or pulls it, stranding all renters. A primary supply-side risk.
- **Demand Risk**: No one wants this enough to pay for it at a price that clears unit economics. A primary customer-side risk.
- **Liquidity / Matching Risk**: Demand is fragmented across very specific (domain × local-part) pairs. Most domains will have thin demand; most renters will want a tiny subset of domains.
- **Forwarding-only**: Candidate architecture — no outbound SMTP, just inbound forwarding + user's existing mailbox (e.g., Gmail send-as). Currently a **hypothesis**, not a decision.
- **Full outbound SMTP**: Higher user value, much higher abuse risk. Viable only post-MVP with strict controls.

## Architecture Candidates (Documented in `docs/01_initial_feasibility_discussion.md`)

Architecture choice is downstream of the winning offer. Do not treat any option as "recommended" until the Demand Workshop picks the buyer.

| Option | Approach | Status |
|--------|----------|--------|
| A | API/Headless (Mailgun, Postmark, SES) | Candidate |
| B | White-label reseller (Titan Email, ResellerClub) | Candidate |
| C | Forwarding-only (ForwardEmail.net, Cloudflare) | Candidate — provisional draft in `04_` |

## Agent Framework (`docs/03_agent_framework.md`)

Design decisions are stress-tested using six advisory AI agent personas, split offensive/defensive:

**Offensive (build the business):**
- **Demand & Positioning Strategist** — ICP, WTP, positioning, substitutes
- **Marketplace Economics Analyst** — unit economics, take rate, liquidity
- **Domain Owner / Supply Advocate** — owner acquisition, listing policy, owner churn

**Defensive (protect the business):**
- **Trust & Safety Architect** — domain reputation and abuse prevention
- **Legal & Operations Expert** — rug-pull risk, continuity, regulatory posture
- **Red Teamer** — adversarial stress-testing across the full system

When proposing solutions, consider all six lenses. The founder's decision rule rejects proposals that lack a validated ICP, fail unit economics, depend on fragile third-party platforms, or cannot solve marketplace liquidity — in addition to defensive failure modes.

## Documentation Conventions

- Docs are numbered sequentially: `docs/01_`, `docs/02_`, `docs/03_`, …
- Each doc covers a single topic: feasibility, validation plan, or agent framework
- Obsidian is used as the local editor (`.obsidian/` config present)
- SpecStory CLI (`.specstory/`) tracks AI coding session history
