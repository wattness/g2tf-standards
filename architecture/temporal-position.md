# Temporal Position: Where Grid 2 Sits in Time

**Status:** Draft — seeking input · **Editors:** TBD · **Source:** [RFC #1](../rfcs/grid-2-rfc-1.pdf), §Proposed Scope, Figure 4

The key words MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are to be interpreted as described in RFC 2119 / RFC 8174.

## The one-minute window

Grid 2 operates in **near real-time dispatch windows of one minute**, deliberately positioned between Grid 1's two existing control regimes:

```
~5 min    Grid 1 — Market Dispatch Domain
          nodal pricing, forward dispatch scheduling
────────────────────────────────────────────────────────
 1 min    Grid 2 — DESP  (service classification & prioritization)
          Grid 2 — GCAP  (fair service allocation & scheduling)
          Grid 2 — G2P   (addressing, service configuration, response)
────────────────────────────────────────────────────────
seconds   Grid 1 — Fast Operational Domain
          frequency response, AGC, reserves
```

## Normative requirements

- Grid 2 allocations MUST apply to whole one-minute intervals; sub-minute response is out of scope for the orchestration plane.
- Grid 2 elements MUST NOT interfere with, substitute for, or assume the function of sub-second primary controls (governor response, AGC, protection).
- Grid 2 clearing MUST complete within the interval such that Members receive commit-% with time to self-dispatch before the interval opens. *(Exact timing budget: open question — see Discussion: Engineering.)*
- Grid 2 SHOULD consume, not contradict, forward information from the market dispatch domain; where a Grid 1 dispatch instruction conflicts with a Grid 2 allocation, the Grid 1 instruction prevails.

## Rationale

- **Bet on current grid physics.** By committing only above the timescales where Grid 1's primary controls operate, Grid 2 lets Grid 1's ancillary services absorb errors without modification. NERC CPS1/BAL metrics remain the measures of balancing performance; the size of ancillary services can be adjusted up or down over time to match observed need.
- **Coexist with markets.** Sitting below the five-minute clearing domain means Grid 2 can be adopted voluntarily by select participants in a domain without any market rule change, and lets stakeholders in ERCOT and PJM run these control schemes so they coexist and reinforce each other (PCLR, IRAS/PRD compliance in the minutes timeframe).

## Open items

- Interval phase alignment across federated domains (common epoch vs. per-domain clocks)
- Late-arrival and clock-skew tolerances for Member broadcasts
- Interaction with 15-minute settlement intervals in some markets
