# Grid 2 Architecture Overview

**Status:** Draft — seeking input · **Editors:** TBD · **Source:** [RFC #1](../rfcs/grid-2-rfc-1.pdf), §The Grid 2.0 Proposal

## One-line definition

Grid 2 is an **overlay network** — coordinated by protocol, embedded throughout Grid 1, verified by its aggregate footprint, with no perimeter and no central operator.

## System model

Grid 2 adds a voluntary **orchestration plane** on top of the existing physical grid ("Grid 1"). The plane consists of two element kinds:

- **Member Elements** — digital representatives of real grid components: **Use** (flexible load), **Buffer** (storage), and **Source** (clean-energy supply). See [`/members`](../members).
- **Allocators** — clearing agents for a constraint domain, informed by Grid 1 capabilities and constraints supplied by the transmission owner and regional system operator. See [members/allocator.md](../members/allocator.md).

Every minute, Members broadcast differential service requests (buckets of load classed by priority), production intent, and buffer capabilities. Allocators aggregate these within the Grid 1 constraints context and return a **percentage dispatch per class of service**, proportional to requested amounts. Members then **self-dispatch** their allocations within parameters agreed with their host utility.

Equitable dispatch is proportional to connection size and differential request size, mirroring the flow control fundamentals of other constrained networks (TCP/IP congestion control, datacenter resource scheduling à la Kubernetes).

## Objectives

Grid 2 is designed to deliver, simultaneously:

1. Faster connections (rapid time-to-power for large loads and supply)
2. Increased grid and generation utilization
3. Equal or better reliability
4. Cost neutrality or better for Grid 2 participants
5. Downward pressure on rates for non-participants

## The guarantee model

Grid 2's reliability guarantee is not a promise made by a central operator. It is three properties working together:

1. **Local good-citizenship.** Each Grid 2 asset, at its specific point of interconnection, behaves according to the protocol — providing locally beneficial response to locally observable conditions.
2. **Protocol-ensured consistency.** Every member runs the same algorithm against the same observable signals, so good citizenship is uniform and predictable across the system; collective behavior emerges.
3. **Aggregate observability.** Grid 1 can measure system-wide effects — frequency stability, ACE excursions, transmission flows, peak shaving — and verify that the overlay is collectively net-positive, without inspecting any individual member's internal operation. The overlay is verified by its footprint, not by its internals.

## Membership without a perimeter

A consequence of the guarantee model: Grid 2 has **no admission process**. Anyone running the protocol at a qualifying point of interconnection, within a domain whose transmission-owner constraints are provisioned to an Allocator, *is* a member. Membership is defined by spec compliance, not by registration. The spec is published; vendors build to it; Grid 2 grows by deployment rather than by central permission. Commercial and authority relationships are addressed in [allocation-domains.md](allocation-domains.md).

## Relationship to Grid 1

Grid 2 does not replace, modify, or bypass any Grid 1 mechanism:

- All participating assets **continue to meet all NERC, FERC, utility, and TSO/ISO requirements** in their Grid 1 context.
- Commercial settlements remain on Grid 1's slower clock; Grid 2 protocols coordinate operation, not prices ("coordination without prices").
- Grid 2 commits only above the timescales where Grid 1's primary controls work; Grid 1's ancillary services absorb errors without modification (see [temporal-position.md](temporal-position.md)).
- On any fault or partition, members revert to Grid 1 baseline behavior (see [failsafe-model.md](failsafe-model.md)).

## Scope of version 26.0

Version 26.0 is focused on **units of energy consumed and provided within the one-minute window** on the bulk power system. Future versions will incorporate other goal-seeks (e.g., voltage support), distribution-scale devices (building on IEEE 2030.5), and routing through advanced power electronics (SSTs, HVDC).
