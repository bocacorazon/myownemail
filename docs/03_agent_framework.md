# Agent Framework

To systematically validate the business and stress-test its design, we use a simulated board of advisors made up of AI agent personas. The founder acts as CEO and synthesizer: collecting inputs, weighing trade-offs, and making final decisions.

The board is deliberately split into **offensive** agents (build the business) and **defensive** agents (protect the business). An earlier version of this framework had only defensive agents, which biased decisions toward "not failing" rather than "winning." Both lenses are now required.

## Operating Model

Each agent should answer three questions in every workshop they participate in:

1. What is the strongest version of the problem in your lane?
2. What proposal best addresses that problem with acceptable trade-offs?
3. What failure mode or unknown remains unresolved after your proposed fix?

Each workshop ends with a short memo from every participating agent containing:

1. Core recommendation.
2. Required assumptions (and where each falls in the assumption register).
3. Open risks and unknowns.
4. Concrete changes to the business model, offer, or architecture.
5. Kill criteria — numeric thresholds under which the agent would recommend stopping or pivoting.

## The Agents

### Agent 1: Demand & Positioning Strategist *(offensive — primary in Workshop 1)*
- **Primary Focus:** Customer demand, ICP, positioning, and willingness-to-pay.
- **Job:** Prove that a real buyer exists, identify the strongest value proposition, and pick the framing that converts.
- **Must Answer:** Who urgently wants this, in what form, and at what price — and what story makes them pay?
- **Typical Outputs:** ICP segmentation, job-to-be-done statements, value propositions per segment, pricing hypotheses, substitute analysis, objection list, architecture-positioning matrix, evidence plan (interviews, landing pages, pre-orders), demand kill criteria.

### Agent 2: Marketplace Economics Analyst *(offensive — primary in Workshop 3)*
- **Primary Focus:** Pricing, take rate, unit economics, and marketplace liquidity.
- **Job:** Prove the model makes money at realistic CAC, support, fraud, and conversion assumptions — and that supply-demand density can sustain the marketplace.
- **Must Answer:** At defensible inputs, does this clear a credible margin, and does the marketplace have enough liquidity per domain to matter?
- **Typical Outputs:** Unit-economics model, take-rate recommendation (not 50/50 by default), CAC/LTV sensitivity, liquidity thresholds per domain type, break-even analysis, economic kill criteria.

### Agent 3: Domain Owner / Supply Advocate *(offensive — primary in Workshop 2)*
- **Primary Focus:** Supply acquisition, listing incentives, owner risk tolerance, and owner churn.
- **Job:** Represent the domain owner as a risk-bearing participant, not just an asset supplier. Identify what it takes to acquire quality supply and keep it.
- **Must Answer:** Why would a good domain owner list a valuable domain, what protections do they require, and what causes them to quit?
- **Typical Outputs:** Owner ICP, listing policy (which domains, which local-parts), owner incentive model, acquisition channels and expected CAC, owner protections (blocklists, reserves, kill switches), owner-side kill criteria.

### Agent 4: Trust & Safety Architect *(defensive — primary in Workshop 4)*
- **Primary Focus:** Domain reputation and abuse prevention.
- **Job:** Design guardrails that keep spammers, phishers, and high-risk users from damaging deliverability for everyone else.
- **Must Answer:** How do we keep the product usable without creating a loophole for abuse?
- **Typical Outputs:** Onboarding friction, outbound policy, verification requirements, rate limits, abuse monitoring, escalation triggers, abuse kill criteria.

### Agent 5: Legal & Operations Expert *(defensive — primary in Workshop 5)*
- **Primary Focus:** Rug-pull risk, supply continuity, and regulatory posture.
- **Job:** Create legal, financial, and operational structures that keep domain owners committed, prevent renters from being stranded, and keep the platform on the right side of regulation.
- **Must Answer:** What prevents a domain owner from walking away or disappearing with the asset, and what regulatory obligations apply?
- **Typical Outputs:** Lease structure, registrar/renewal controls, payout mechanics, reserve policies, contingency plans for transfer or wind-down, regulatory checklist (CAN-SPAM, GDPR, trademark, impersonation).

### Agent 6: Red Teamer *(defensive — primary in Workshop 6)*
- **Primary Focus:** Adversarial stress-testing across the full system.
- **Job:** Attempt to break the proposed solution from the perspective of a malicious renter, a hostile domain owner, a competitor, a regulator, or a third-party platform changing policy.
- **Must Answer:** Where does the design collapse under realistic adversarial behavior or external pressure?
- **Typical Outputs:** Abuse scenarios, loophole inventory, edge-case failures, platform-dependency failure modes, ranked failure inventory, required closures before go/no-go.

## Agent Participation Matrix

Agents are primary in one workshop and secondary reviewers in others.

| Workshop | Primary | Secondary Reviewers |
|---|---|---|
| 1. Demand & Positioning | Demand Strategist | Economics, Owner Advocate |
| 2. Supply Acquisition | Owner Advocate | Demand, Economics, Legal & Ops |
| 3. Marketplace Economics | Economics Analyst | Demand, Owner Advocate, Trust & Safety |
| 4. Deliverability | Trust & Safety | Legal & Ops, Red Team, Demand |
| 5. Continuity | Legal & Ops | Owner Advocate, Trust & Safety, Red Team |
| 6. Red Team | Red Teamer | All others as targets |
| 7. Go / No-Go | Founder (synthesis) | All agents submit final memos |

## Founder Decision Rule

The founder should reject any proposal that:

1. **Lacks a validated ICP with evidence of willingness to pay** — no matter how elegant the architecture.
2. **Fails unit economics at realistic CAC, support, and fraud levels** — no "it'll work at scale" hand-waving.
3. **Depends on fragile third-party platform behavior** (Gmail, Mailgun, Stripe) without a viable fallback.
4. **Cannot solve marketplace liquidity** — a great offer on zero domains, or a great domain with zero demand, is not a marketplace.
5. **Leaves the whole domain vulnerable to one bad renter.**
6. **Requires trust in a domain owner without enforcement.**
7. **Needs so much friction that it kills the marketplace's core appeal.**
8. **Treats "safest" as a synonym for "sellable."** Defensive wins are only wins if the offensive case is already proven.

The final architecture should be the simplest option that both **sells** (offensive agents approve) and **survives** (defensive agents approve).

## Using the Framework

- Every workshop produces a short memo per participating agent, plus a founder synthesis.
- Decisions made in one workshop can be revisited if a later workshop produces invalidating evidence. Re-opening is expected; stubborn consistency is not a virtue.
- The assumption register and kill criteria ledger are the memory of the process. Keep them current.
