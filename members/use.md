# Use Member (Load)

**Status:** Draft — seeking input · **Editors:** TBD · **Source:** [RFC #1](../rfcs/grid-2-rfc-1.pdf), Protocol Interactions table

The key words MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are to be interpreted as described in RFC 2119 / RFC 8174.

**Associated physical asset:** Flexible large load — capable datacenter sites (any combination of flex-capable load and/or on-site power resources) and electrified industry.

## Broadcasts (via G2P)

- Per-class **request to consume** (+): one signed position per service class over a forward time vector.
- Positions MAY be reclassified each interval per [DESP](../specs/desp/spec.md).

## Listens for

- Its Allocator's per-class **commit-%** for the coming interval.

## Intelligence — at the edge

The Use Member owns all decisions about its own operation:

- How to map internal workloads onto service classes (see DESP §3 informative mapping)
- Which demand is deferrable, and when
- Anticipating its own forward load

The Allocator never sees or directs internal workloads; it clears class-level positions only. This is the "scale without singular operator" principle: every asset runs the same algorithm against the same observable signals.

## Obligations

- MUST self-dispatch within its per-class commit-% for the interval, within parameters agreed with its host utility.
- MUST report verified self-dispatch (G2P §3.4).
- MUST respect agreed ramp rates on all transitions.

## Failsafe

- On loss of peers/context or a stale Commitment: MUST revert to Grid 1 baseline (firm load limit) or manual curtailment, following allowed ramp rates. See [failsafe-model.md](../architecture/failsafe-model.md).

## Open items

- Standard workload→class mapping guidance per facility type
- Minimum telemetry for commit-% compliance verification
- Behavior when actual load undershoots requested+committed amounts (does unused allocation return to the pool mid-interval?)
