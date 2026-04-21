# Feasibility Validation Plan

## Philosophy: System First, Execution Later — But Demand Before Defense

Before writing code or building infrastructure, the existential risks of the business model must be solved on paper. **And before solving risk, we must prove there is a business worth defending.**

The original plan was defensively sequenced (deliverability → continuity → red team → go/no-go). That order optimizes for *not failing* rather than *winning*. A safer email architecture for a product nobody wants is still a dead product. The revised plan validates demand, supply, and economics first, then hardens the winning offer.

## Validation Outputs

The validation phase should produce the following artifacts:

1. An Ideal Customer Profile (ICP) with evidence of willingness to pay.
2. A primary value proposition and positioning story.
3. A pricing hypothesis with defensible take-rate and unit economics.
4. A supply acquisition plan with owner ICP and listing policy.
5. A marketplace liquidity model (how many owners, how many renters per domain, density thresholds).
6. A recommended MVP architecture matched to the winning offer.
7. A minimum acceptable trust & safety policy.
8. A continuity and legal operating model.
9. A ranked failure-mode inventory after red-teaming.
10. A go / no-go recommendation with explicit risks and kill criteria.

Each workshop also maintains a shared **assumption register** — a living list of hypotheses with status (open / validated / killed) and the evidence that moved them.

## The 7-Step Systematic Workshop Plan

### Step 1: Demand & Positioning Workshop
*Focus: Prove there is a buyer and a story before optimizing anything else.*
- Primary question: Who urgently wants this, in what form, and at what price?
- Define ICP segments (identity, professional, privacy, surname, creator, novelty).
- Define the primary job-to-be-done and the value proposition per segment.
- Map substitutes (own-domain + Workspace, aliasing tools, free forwarding, "just use Gmail") and state why the product wins against each.
- Produce pricing hypotheses per segment.
- Define architecture-positioning matrix: how the same technical architecture (e.g., forwarding-only) can be framed as a liability, a privacy benefit, or a premium identity layer — and pick the winning frame.
- Define the evidence plan: interviews, landing-page tests, concierge offers, pre-orders.
- Define kill criteria: what WTP or conversion rate would kill the idea.
- Output: ICP memo, positioning memo, pricing hypothesis, objection list, evidence plan, kill criteria.

### Step 2: Supply Acquisition Workshop
*Focus: Prove quality domain supply is acquirable at a cost the model can bear.*
- Primary question: Why would a good domain owner list a valuable domain, and what will they require in return?
- Define owner ICP (family-name owners, surname holders, legacy personal domains, category-specific owners).
- Map owner acquisition channels and expected cost.
- Define listing criteria and policy (which domains are too risky to expose, trademark collisions, adult/regulated categories).
- Define owner protections and controls (blocklists on local-parts, revenue floors, reserve accounts, termination rights).
- Define owner objections and the responses to each.
- Output: Owner ICP, listing policy, owner incentive model, supply acquisition plan, expected conversion and churn.

### Step 3: Marketplace Economics Workshop
*Focus: Prove the model makes money at realistic assumptions.*
- Primary question: At realistic CAC, support, fraud, and conversion rates, does this clear a credible margin?
- Build a unit-economics model (per renter, per domain, per month).
- Stress-test the 50/50 split against alternatives (e.g., 70/30 to platform, flat listing fee, tiered).
- Model marketplace liquidity: how many domains, how many renters per domain, what density is needed before churn becomes terminal.
- Model CAC for both sides and LTV sensitivity to abuse, support, and refund rates.
- Define break-even thresholds and go/no-go economic triggers.
- Output: Unit-economics sheet, take-rate recommendation, liquidity model, CAC/LTV sensitivity analysis, economic kill criteria.

### Step 4: Deliverability Workshop
*Focus: Prevent spam and protect domain reputation — for the winning offer.*
- Primary question: Can a single renter damage the whole domain, and what architecture minimizes that risk for the chosen offer?
- Decide whether the MVP is forwarding-only, hybrid, or supports outbound sending — **based on what the Demand Workshop said sells**, not on what is simply safest.
- Define onboarding friction (identity checks, deposits, limits, review).
- Define abuse monitoring, escalation, and delisting mechanics.
- Output: Abuse-prevention policy, minimum viable email flow, onboarding policy, escalation matrix.
- **Note:** An initial pass of this workshop has already been completed (`04_deliverability_workshop.md`) assuming forwarding-only. It must be revisited and, if necessary, revised after the Demand Workshop picks the winning offer.

### Step 5: Continuity Workshop
*Focus: Lock in domain supply and protect renters.*
- Primary question: What keeps a domain owner from abandoning the marketplace, and what protects renters if they do?
- Explore registrar controls, escrow, payment holds, lease terms, renewal locks.
- Define what happens if a domain is sold, expires, or is intentionally withdrawn.
- Define renter notification, grace period, and migration paths.
- Define regulatory posture (CAN-SPAM, GDPR, trademark disputes, impersonation).
- Output: Continuity policy with ownership, renewal, and renter protection rules; regulatory checklist.

### Step 6: Red Team Assault
*Focus: Break the whole system — offer, supply, economics, and architecture — before users do.*
- Primary question: How does a malicious renter, hostile owner, competitor, or regulator break this?
- Attack the offer (positioning collapse, brand damage scenarios).
- Attack the supply model (owner collusion, listing fraud).
- Attack the economics (CAC blowup, refund storms, chargeback abuse).
- Attack the deliverability model (bypass routes for abuse).
- Attack the continuity model (legal escape hatches, jurisdiction gaming).
- Attack the platform dependencies (what if Gmail / Mailgun / Stripe changes policy?).
- Output: Ranked failure-mode inventory; required closures before go/no-go.

### Step 7: Go / No-Go Decision
*Focus: Decide whether the idea is worth executing.*
- Primary question: Is the business still attractive after every safeguard, friction point, and economic adjustment identified above?
- Weigh user friction, operational burden, legal complexity, supply scarcity, and dependency risk against revenue potential.
- Decide whether to proceed to technical execution, narrow scope (pick one ICP beachhead), or stop.
- Output: Final decision memo with the recommended path forward, residual risks, kill criteria that carry into execution, and a staged execution plan if green-lit.

## Cross-Cutting Artifacts

- **Assumption Register:** a shared table of every hypothesis across all workshops, each with status (open / validated / killed) and a pointer to the evidence.
- **Evidence Log:** raw outputs of interviews, landing-page tests, concierge runs, and quantitative checks.
- **Kill Criteria Ledger:** numeric thresholds that end the project cleanly rather than allowing sunk-cost drift.

## Workshop Dependencies

```
1. Demand & Positioning
        ↓
2. Supply Acquisition
        ↓
3. Marketplace Economics
        ↓
4. Deliverability  (revise existing draft against the winning offer)
        ↓
5. Continuity
        ↓
6. Red Team  (attacks outputs of 1–5)
        ↓
7. Go / No-Go
```

Earlier workshops may be re-opened if later ones surface invalidating evidence. That is a feature, not a regression.
