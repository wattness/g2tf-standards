# Allocator

**Status:** Draft — seeking input · **Editors:** TBD · **Source:** [RFC #1](../rfcs/grid-2-rfc-1.pdf), Protocol Interactions table

The key words MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are to be interpreted as described in RFC 2119 / RFC 8174.

**Associated scope:** A constraint domain at any level of the hierarchy — transmission line → utility load zone → RTO region.

**Represents:** the zone's Grid 1 power production capacity and transmission constraints; MAY incorporate power distribution factors and dynamics available from Dynamic Line Ratings and similar sources.

## Broadcasts (via G2P)

- Per-class **commit-%** back to its Members (plus committed dispatch/take to Buffers/Sources).
- **Federation announcements** to peer Allocators ([federation.md](../architecture/federation.md)).

## Listens for

- Member Service Descriptors in-zone.
- Peer-Allocator announcements across coupled zones.

## Intelligence — none internal

By design the Allocator holds **no internal intelligence or discretion**. It alleviates constraints by redispatching deterministically and proportionally, in strict order:

1. **Headroom** — surplus network capability for the interval
2. **Buffers** — cleared before any load is curtailed
3. **Ramp down tiered requests** — class ordering per [DESP](../specs/desp/spec.md) (C → B → A), proportional within class

Full algorithm: [GCAP](../specs/gcap/spec.md). Determinism is what makes the Allocator trustworthy without being an operator: any party with the same inputs can reproduce its clearing.

## Constraint inputs and authority

Authority is anchored in the utility transmission owner, which MUST provision the Allocator's local and regional constraints; a regional system operator MAY add capacity constraints ([allocation-domains.md](../architecture/allocation-domains.md)). Which existing transmission-owner signals are best used as inputs, and how they can be standardized, is a headline open question (Discussion: Engineering).

## Failsafe

- On stale inputs or partition: **no clearing**. Members fall back to Grid 1 baseline.
- The total participating pool MUST be sized to manageable aggregate ramp rates so that whole-pool fallback is safe.

## Open items

- Redundancy model (active/standby Allocators per domain?)
- Publication of clearing inputs digest for reproducibility
- Hosting and operational responsibility (utility-operated vs. third-party under utility authority)
