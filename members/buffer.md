# Buffer Member (Storage)

**Status:** Draft — seeking input · **Editors:** TBD · **Source:** [RFC #1](../rfcs/grid-2-rfc-1.pdf), Protocol Interactions table

The key words MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are to be interpreted as described in RFC 2119 / RFC 8174.

**Associated physical asset:** Grid battery / storage asset — behind-the-meter or front-of-meter — acting as the domain's buffer.

## Broadcasts (via G2P)

- **Offer to be a source or use**: − discharge / + charge. A Buffer sits on *either side* of the ledger and may switch roles per interval.

## Listens for

- Its Allocator's **committed dispatch** — which is cleared **before any load is curtailed** ([GCAP](../specs/gcap/spec.md) §3, step 2).

## Intelligence — at the edge

- When to discharge vs. hold charge for a later peak
- When to charge on surplus
- Protecting a coupled asset (e.g., a co-located Use Member)
- Its defining job: **reduce how often Grid 2 load goes unmet**

## Role in the system

Buffers are Grid 2's shock absorber. Network-directed storage-based buffers reduce the need to call on load flexibility by adding it from new, rapidly connected assets; over time, buffers added to a domain shrink the unmet/deferred share for Classes B and C. A companion G2TF document on network-directed storage (anticipatory, dynamic movement of energy in space and time) is planned.

## Obligations

- MUST honor committed dispatch within agreed ramp rates.
- MUST report verified self-dispatch (G2P §3.4).

## Failsafe

- Reverts to its **standalone Grid 1 schedule**; carries **no Grid 2 support commitment** while in fallback; follows allowed ramp rates.

## Open items

- State-of-charge disclosure: how much SoC visibility does the Allocator need for step-2 clearing?
- Priority among multiple Buffers (proportional? merit order by round-trip efficiency?)
- Investment-decision framing when a new battery is needed to support new Grid 2 loads (Discussion: Commercial terms)
