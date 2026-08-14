# Grid 2.0 Standards Repository

**An open standard for grid service access and allocation.**

Grid 2.0 ("Grid 2") is a voluntary, protocol-based orchestration plane that sits on top of the existing physical grid ("Grid 1"). It allocates surplus grid capacity headroom to participating loads, storage, and clean-energy supply in near real-time, one-minute dispatch windows — enabling rapid interconnection, higher utilization of existing infrastructure, and downward pressure on electricity rates, while guaranteeing that grid constraints are never breached.

> Grid 2 is an overlay network — coordinated by protocol, embedded throughout Grid 1, verified by its aggregate footprint, with no perimeter and no central operator.

This repository is maintained by the **Grid 2.0 Task Force (G2TF)** — [g2tf.org](https://www.g2tf.org) — and is the canonical home of the Grid 2 specifications, open for community comment and contribution in the spirit of the IETF.

## Repository map

| Path | Contents | Status |
|---|---|---|
| [`rfcs/`](rfcs/) | Immutable, archival RFCs. [RFC #1](rfcs/grid-2-rfc-1.pdf) is the August 2026 launch document. | Published |
| [`architecture/`](architecture/) | The Grid 2 system model: [overview](architecture/overview.md), [temporal position](architecture/temporal-position.md), [allocation domains](architecture/allocation-domains.md), [federation](architecture/federation.md), [failsafe model](architecture/failsafe-model.md), [design principles](architecture/design-principles.md) | Draft |
| [`specs/`](specs/) | The three normative protocols: [G2P](specs/g2p/spec.md), [GCAP](specs/gcap/spec.md), [DESP](specs/desp/spec.md) | Draft — seeking input |
| [`members/`](members/) | Behavioral specifications per member type: [Use](members/use.md), [Buffer](members/buffer.md), [Source](members/source.md), [Allocator](members/allocator.md) | Draft — seeking input |

## The protocol stack at a glance

```
Grid 1   Market Dispatch Domain (nodal pricing, forward dispatch)          ~5 minutes
─────────────────────────────────────────────────────────────────────────────────────
Grid 2   DESP — Differential Electric Service Protocol                      1 minute
         (service classification and prioritization)
         GCAP — Grid Capacity Allocation Protocol
         (fair service allocation and scheduling)
         G2P — Grid 2.0 Protocol
         (addressing, service configuration, and response)
─────────────────────────────────────────────────────────────────────────────────────
Grid 1   Fast Operational Domain (frequency response, AGC, reserves)        seconds
```

Grid 2 commits only above the timescales where Grid 1's primary controls operate, and below the market clearing domain. All participating assets continue to meet all NERC, FERC, utility, and TSO/ISO requirements in their existing Grid 1 context.

## Versioning

Each protocol specification is versioned independently (current line: **26.x**, reflecting the 2026 launch year). A compatibility matrix will be maintained here as the specs diverge in maturity. RFCs are never modified after publication; evolution happens in the living specs.

## How to comment

- **Technical questions and design alternatives** → [GitHub Discussions](../../discussions), organized by the technical open-question areas from RFC #1 (see [CONTRIBUTING.md](CONTRIBUTING.md))
- **Proposed spec text** → Pull requests against `specs/`, `members/`, or `architecture/`
- **Errata against RFC #1** → Issues labeled `errata`

## License

© 2026 The Grid 2.0 Task Force. Specification text is licensed under [CC BY 4.0](LICENSE); code in this repository is licensed under [Apache-2.0](LICENSE-CODE). See [NOTICE.md](NOTICE.md) for contribution and trademark terms. "Grid 2.0"™, "G2TF"™, "G2P"™, "GCAP"™, and "DESP"™ are trademarks of the Grid 2.0 Task Force; no trademark rights are granted by either license.
