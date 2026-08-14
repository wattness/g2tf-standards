# GCAP — Grid Capacity Allocation Protocol

**Version:** 26.0-draft · **Status:** Draft — seeking input · **Editors:** TBD
**Role in stack:** Fair service allocation and scheduling — the clearing logic executed by Allocators each interval, over messages carried by [G2P](../g2p/spec.md), across classes defined by [DESP](../desp/spec.md).

The key words MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are to be interpreted as described in RFC 2119 / RFC 8174.

## 1. Scope

GCAP defines how an Allocator computes per-class allocations from Member requests and Grid 1 constraints. GCAP is **deterministic**: given identical inputs, any conformant implementation MUST produce identical allocations. The Allocator holds **no internal intelligence or discretion** — all intelligence lives at the edge, in Member Elements.

## 2. Inputs

Each interval, the Allocator clears against:

1. **Grid 1 constraints** provisioned by the domain's custodians: zone power production capacity, transmission constraints, target reserves; optionally power distribution factors and dynamics from Dynamic Line Ratings.
2. **Member Service Descriptors** in-zone (per G2P §3.1).
3. **Peer-Allocator announcements** across coupled zones (per G2P §3.3), which MAY add boundary headroom but MUST NOT relax local constraints.

## 3. Clearing algorithm

The Allocator alleviates constraints by redispatching deterministically and proportionally, in strict order:

1. **Headroom first.** Compute surplus network capability (grid capacity headroom) available to the domain for the interval.
2. **Buffers second.** Clear Buffer committed dispatch to absorb shortfall or surplus — **Buffers are cleared before any load is curtailed.**
3. **Ramp down tiered requests third.** If constraint relief is still required, reduce Use allocations by service class in DESP class order — Best Efforts (C) first, then Preferred (B), then Assured (A) — never touching traditional Firm (Grid 1) service.

Within a class, curtailment MUST be **proportional**: equitable dispatch proportional to connection size and differential request size, mirroring the flow-control fundamentals of other constrained networks.

## 4. Outputs

- Per-class **commit-%** to each Use Member; **committed dispatch** to each Buffer; **committed take** from each Source (per G2P §3.2).
- Allocations apply to the coming interval only and expire with it.

## 5. Determinism and verifiability

- The clearing computation MUST be reproducible by any party holding the same inputs; Allocators SHOULD publish (within the domain) the input digest each Commitment was computed against.
- The Allocator MUST NOT clear on stale constraint inputs; on staleness or partition it MUST withhold clearing and let Members fall back (see [failsafe-model.md](../../architecture/failsafe-model.md)).

## 6. Pool and ramp safety

- The Allocator MUST bound total cleared participation such that simultaneous member fallback stays within manageable aggregate ramp limits for the domain.
- Per-member allocation deltas between consecutive intervals MUST respect each member's agreed ramp rates.

## 7. To be specified / open

Exact proportionality formula (connection size vs. request size weighting) · treatment of indivisible loads · multi-constraint (nodal) allocation vs. single-zone headroom · fairness across intervals (does deferred Class C accrue priority?) · interaction with market dispatch instructions mid-interval. Contributions welcome via PR.
