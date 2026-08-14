# Source Member (Supply)

**Status:** Draft — seeking input · **Editors:** TBD · **Source:** [RFC #1](../rfcs/grid-2-rfc-1.pdf), Protocol Interactions table

The key words MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are to be interpreted as described in RFC 2119 / RFC 8174.

**Associated physical asset:** Clean-energy / inverter-based supply — solar, wind.

## Broadcasts (via G2P)

- **Offer to supply** (−): generation available this window, over a forward time vector.

## Listens for

- Its Allocator's **committed take**.

## Intelligence — at the edge

- Forecasting available output
- Anticipating ramps

## Role in the system

Sources bring rapid renewables interconnection into the same permission-based paradigm as loads: the same protocol that protects the grid on the load side ensures protection around Grid 2-compliant supply, creating a more elegant approach to curtailment while supporting rapid interconnection. A companion G2TF document on expedited renewables interconnection within Grid 2.0 is planned.

## Obligations

- MUST self-dispatch to committed take within agreed ramp rates.
- MUST report verified self-dispatch (G2P §3.4).

## Failsafe

- Reverts to Grid 1 baseline interconnection behavior; follows allowed ramp rates.

## Open items

- Forecast accuracy expectations and how forecast error interacts with GCAP headroom
- Whether curtailed Source energy can be redirected to co-located Buffers within the same interval
- Class structure for supply offers (single class in v26.0, or mirrored A/B/C?)
