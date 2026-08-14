# Design Principles

**Status:** Informative · **Source:** [RFC #1](../rfcs/grid-2-rfc-1.pdf), §Key Design Principles; G2TF design imperatives

Grid 2.0 was designed with proven principles from the world's highest-growth infrastructures — the Internet and data centers — which deliver higher reliability and higher utilization than the grid with less central planning and regulation.

## Objectives

1. Enable faster connections
2. Increase grid and generation utilization
3. Equal or better reliability
4. Cost neutral or better for Grid 2 participants
5. Downward pressure on rates for others

## Principles

| Objective | Approach | Rationale |
|---|---|---|
| **Coexist with physical grid** | Overlay network architecture | Members are embedded throughout Grid 1, not topologically separate; verified by aggregate footprint |
| **Coordination without prices** | Protocol-based coordination | Technical protocols handle real-time coordination; current commercial settlements stay decoupled on a slower clock |
| **Scale without singular operator** | Edge intelligence at every Member Element; extensible design allows organic growth | Every asset runs the same algorithm against the same observable signals; collective behavior emerges |
| **No surprises** | Failsafe defaults with status quo Grid 1 | An element losing context or peers reverts to baseline behavior; managed to local and regional ramp limits |
| **Bet on current grid physics** | Grid 2 commits only above timescales where Grid 1's primary controls work | Grid 1's ancillaries absorb errors without modification; NERC CPS1/BAL remain the measures; ancillary sizing can be tuned over time |

## Approach characteristics

- **Voluntary pool** with an abstracted boundary — Grid 2 on top of Grid 1; adoption requires no capital deployment and no multi-stakeholder consensus, fitting within existing rules as a transmission-owner "connect and manage" standard.
- **Protocol standard and topology** that meets Grid 1 requirements at the edge and in balancing-authority parallel sub-domains.
- **Software-defined topology**, dynamically managed — "path-making" rather than routing per se, with network-directed storage and large loads participating.
- **Autonomous domains** with BGP-style cross-awareness across connected systems.
- **Phased adoption** for 80/20 quick wins locally first; broader (e.g., FERC-level) recognition pursued after the path is proven. See [RFC #1](../rfcs/grid-2-rfc-1.pdf), §Phased Adoption (Phase 0 Shadow Mode → Phase 1 Local Vertical Integration → Phase 2 Regional Federation).

## The verification analogy

The overlay proves its value the way a CDN proves its value to ISPs: not "inspect our internal routing" but "your backbone traffic dropped 30% — here are the measurements." Grid 1 custodians verify Grid 2 by its measurable aggregate footprint (frequency stability, ACE excursions, transmission flows, peak shaving), never by inspecting a member's internal operation.
