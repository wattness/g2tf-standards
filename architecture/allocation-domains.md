# Allocation Domains, Membership, and Basis of Authority

**Status:** Draft — seeking input · **Editors:** TBD · **Source:** [RFC #1](../rfcs/grid-2-rfc-1.pdf), §Grid 2.0 Membership and Basis of Authority

The key words MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are to be interpreted as described in RFC 2119 / RFC 8174.

## Definition

A **Grid 2 Allocation Domain** is the set of Member Elements cleared by a common Allocator (or Allocator hierarchy) against a common set of Grid 1 constraints. Domains nest: local transmission congestion zone → utility / balancing authority → regional RTO/ISO (see [federation.md](federation.md)).

## Minimum viable domain

The smallest Grid 2 Allocation Domain is **a host utility and a single flexible load customer**. This is the deliberate on-ramp: no capital deployment, no multi-stakeholder consensus process, fits within existing rules as a transmission-owner "connect and manage" standard.

## Basis of authority

- Authority for Grid 2 is **anchored in the utility transmission owner**. The transmission owner MUST provision the Allocator with the local and regional constraints that bound clearing for Member Elements in its domain (see [members/allocator.md](../members/allocator.md) for the input set).
- A regional system operator MAY additionally provision capacity constraints to a regional Allocator.
- No Grid 2 element derives authority from the protocol itself; the protocol carries and enforces constraints whose authority comes from Grid 1 custodians.

## Voluntariness

- Membership in a Grid 2 Allocation Domain is **voluntary** and can exist distinct from other grid and market requirements, just as emerging "connect and manage" schemes have.
- The Grid 2 design assumes willingness of parties to agree on connect-and-manage principles; with the same or less willingness to flex and accept flex than these bespoke arrangements require, Grid 2 produces better outcomes.
- Grid 2 does not need to be universally applied. It serves and sits inside the Grid 1 context at any scale or scope.

## Membership semantics

- A Member is any asset running a conformant protocol implementation at a point of interconnection covered by a provisioned domain, under commercial terms with its host utility.
- Technical membership is defined by **spec compliance** (see [overview.md](overview.md), "Membership without a perimeter"); commercial participation terms (enforcement of flex capabilities, class limits, charging for Grid 2-enabled use) are domain-level agreements outside the protocol — see Discussion: Commercial terms.

## Open items

- Certification / conformance test criteria for "spec compliance"
- Whether domains publish a machine-readable domain descriptor (constraint scope, class policy, ramp limits)
- Treatment of a Member present in overlapping domains (local + regional)
