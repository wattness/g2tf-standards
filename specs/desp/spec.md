# DESP — Differential Electric Service Protocol

**Version:** 26.0-draft · **Status:** Draft — seeking input · **Editors:** TBD
**Role in stack:** Service classification and prioritization — the service-class taxonomy and priority ordering used by [GCAP](../gcap/spec.md) clearing, carried in [G2P](../g2p/spec.md) Service Descriptors.

The key words MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are to be interpreted as described in RFC 2119 / RFC 8174.

## 1. Scope

DESP defines the tiered classes of non-firm service through which Grid 2 Members express differential flexibility tolerance, and the ordering Allocators MUST honor when constraints bind. Classification is **dynamic**: a Member MAY reclassify its request buckets **each interval**.

## 2. Service classes

Grid 2 stratifies demand above the traditional Grid 1 firm layer:

| Class | Name | Position | Semantics |
|---|---|---|---|
| — | **Traditional Firm (Grid 1)** | Base | Outside Grid 2; served per existing firm service. Never curtailed by GCAP. |
| **A** | **Assured** | Highest non-firm | Curtailed last among Grid 2 classes; intended for latency-sensitive, hard-to-defer demand. |
| **B** | **Preferred** | Middle | Curtailed after C, before A; deferrable-with-constraints demand. |
| **C** | **Best Efforts** | Lowest | Curtailed first; unmet or deferred most frequently; the internet-like statistical-multiplexing tier. |

Classes A, B, and C together represent traditional non-firm demand (RFC #1, Figure 2). In G2P Service Descriptors these appear as one signed position per class (Firm / Semi-Firm / Flex naming in the interaction table maps to A / B / C; naming reconciliation is an open item).

- Class ordering for curtailment MUST be C → B → A.
- Buffer committed dispatch MUST clear before any class is curtailed (GCAP §3).
- Within a class, curtailment MUST be proportional (GCAP §3).

## 3. Mapping workloads to classes (informative)

Field evidence from data-center flexibility research suggests a practical mapping, aligned with Emerald AI's field-validated Flex 0/1/2/3 tier schema and ERCOT's CLR/PCLR constructs:

- **Class A — firm/latency-sensitive** (≈ Flex 0, ERCOT LPC-aligned firm portion): real-time inference, interactive services. Sub-second SLAs; flexibility only via spatial routing, cooling, behind-the-meter storage, bounded power-capping (~20% headroom on inference without deferring requests).
- **Class B — semi-flexible** (≈ Flex 1–2, CLR/PCLR dispatchable portion): training with checkpointing, deadline batch. Minutes-to-hours deferral via checkpoint pause, throttling, GPU frequency-capping; 10–25% throttle sustained 3–6 h is field-proven. The primary flex reservoir.
- **Class C — highly interruptible** (≈ Flex 3): opportunistic/spot compute, non-urgent batch. Pausable hours-to-days; shed first; deep temporal and spatial shifting.

Empirical anchors informing class design: 25% sustained facility power reduction for 3 hours demonstrated in production (Emerald AI, 256 GPUs, 15-minute ramps); curtailing 0.25–1.0% of annual load unlocks 76–126 GW of US headroom (Duke, *Rethinking Load Growth*). See [RFC #1](../../rfcs/grid-2-rfc-1.pdf), §Industry Analysis Informing Grid 2.0.

## 4. Class policy

- A domain MAY constrain the mix of classes a Member can declare (e.g., minimum Class C share for expedited interconnection); such limits are commercial-terms matters expressed in the domain agreement, not in the protocol. See Discussion: Commercial terms.
- Whether the standard should provide guidance or limits on differential service classes is an explicit open question from RFC #1.

## 5. To be specified / open

- Reconciliation of naming (Assured/Preferred/Best-Efforts vs. Firm/Semi-Firm/Flex)
- Whether class count is fixed at three or extensible per domain
- Per-class performance expectations (target unmet-frequency envelopes per class, à la SLA)
- Ramp-rate and snap-back limits per class (research suggests 15-minute ramp discipline)
- Enforcement and verification of declared class behavior (ties to G2P §3.4 verified self-dispatch)
