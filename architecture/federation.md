# Federation: Allocator ↔ Allocator Interoperation

**Status:** Draft — seeking input · **Editors:** TBD · **Source:** [RFC #1](../rfcs/grid-2-rfc-1.pdf), §Extensible System-Wide Architecture, Figure 6

The key words MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are to be interpreted as described in RFC 2119 / RFC 8174.

## Model

Grid 2 is extensible from a single local domain to a federated regional system. All protocol interactions follow exactly two patterns:

1. **Member ↔ Allocator** — Members advertise requests; Allocators clear; Members perform verified self-dispatch. (Specified in [G2P](../specs/g2p/spec.md) and [GCAP](../specs/gcap/spec.md).)
2. **Allocator ↔ Allocator** — an **announce-and-listen federation**: peer Allocators exchange announcements across coupled zones; each sets its allocation decisions from information provided by its Grid 1 custodians (zone capacity, target reserves, etc.).

Constraint domains nest hierarchically:

```
Regional Constraint Domain ──────────────── Allocator(s)
├── Utility "A" Constraint Domain ───────── Allocator(s)
│   └── Local Constraint Domain ─────────── Allocator(s)
│       ├── Large Load A1 (Use Member)
│       ├── Large Load A2 (Use Member)
│       └── Storage A1 (Buffer Member)
├── Utility "B" Constraint Domain ───────── Allocator(s)
│   └── Local Constraint Domain ─────────── Allocator(s)
│       ├── Large Load B1 (Use Member)
│       └── Storage B1 (Buffer Member)
├── Supply (Source Member, regional)
└── Storage (Buffer Member, regional)
```

The federation style is intentionally analogous to inter-domain routing on the Internet: **autonomous domains with BGP-style cross-awareness** across connected systems. Domains do not command one another; they announce, listen, and clear locally.

## Normative requirements (initial)

- An Allocator MUST clear only against constraints provisioned by its own domain's Grid 1 custodians; peer announcements inform but never override local constraints.
- Federation announcements MUST be carried via G2P and MUST identify the announcing domain, interval, and coupled-boundary quantities. *(Message schema: to be specified in G2P.)*
- An Allocator that has not received required peer announcements for a coupled boundary MUST clear conservatively as if the boundary contributes no additional headroom.
- Federation MUST degrade to independent local operation: partition between peer Allocators MUST NOT prevent local clearing, and MUST NOT trigger member fallback in unaffected domains (see [failsafe-model.md](failsafe-model.md)).

## Open items

- Announcement content: boundary headroom only, or per-class aggregates?
- Loop prevention and path attributes in multi-level hierarchies
- Inter-domain policy expression (who may import whose headroom)
- Phase 2 (Regional Federation) milestone criteria (see [RFC #1](../rfcs/grid-2-rfc-1.pdf), §Phased Adoption)
