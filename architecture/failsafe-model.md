# Failsafe Model: "No Surprises"

**Status:** Draft — seeking input · **Editors:** TBD · **Source:** [RFC #1](../rfcs/grid-2-rfc-1.pdf), §Protocol Interactions, §Key Design Principles

The key words MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are to be interpreted as described in RFC 2119 / RFC 8174.

## Principle

The design objective is **no surprises**: any Grid 2 element that loses context or peers reverts to Grid 1 baseline behavior — what otherwise might have happened under prior curtailment regimes — managed within local and regional ramp limits. Failure of the orchestration plane can never leave the physical grid worse off than the pre-Grid 2 status quo.

## Normative fallback behaviors

| Element | On loss of Allocator / peers / fresh context |
|---|---|
| **Use** (load) | MUST revert to its Grid 1 baseline (firm load limit) or manual curtailment; MUST follow allowed ramp rates while transitioning |
| **Buffer** (storage) | MUST revert to its standalone Grid 1 schedule; carries **no Grid 2 support commitment** while in fallback; MUST follow allowed ramp rates |
| **Source** (supply) | MUST revert to Grid 1 baseline interconnection behavior; MUST follow allowed ramp rates |
| **Allocator** | If its constraint inputs are stale or the domain is partitioned, it MUST NOT clear; Members detecting a missed clearing fall back per the rows above |

## System-level requirements

- **Pool sizing.** The total participating pool in a domain MUST be sized such that simultaneous fallback of all Members produces aggregate ramps within manageable Grid 1 system ramp limits. *(This is the binding constraint on domain growth; sizing methodology is an open engineering question.)*
- **Staleness.** Allocations are valid for their interval only. A Member that has not received a commit-% for the current interval MUST treat itself as in fallback. Explicit staleness timers to be specified in [G2P](../specs/g2p/spec.md).
- **Ramp discipline.** All transitions — into fallback, out of fallback, and between interval allocations — MUST respect the ramp rates agreed with the host utility.
- **Determinism.** Fallback behavior MUST be locally determinable from the Member's own state and last-known configuration; it MUST NOT depend on reaching any remote element.

## Security posture

Grid 2 communications and systems will be built with industry best practices for cybersecurity and are expected to be implemented on **private networks for transmission-level assets**. NERC CIP applicability, key management, and message authentication requirements are open items tracked in Discussion: Engineering, and will be specified in G2P.

## Open items

- Quantitative staleness thresholds (missed intervals before fallback)
- Re-entry procedure and hysteresis after fallback
- Coincidental-fallback stability analysis (see Discussion: Reliability assurance)
- Audit/telemetry requirements to verify fallback compliance
