# Governance

## The Grid 2.0 Task Force

The G2TF is a working group of individuals with deep electric grid and market development experience across multiple organizations, formed at the publication of RFC #1 (August 2026). It maintains this repository and shares progress at [g2tf.org](https://www.g2tf.org).

The G2TF was inspired by the Internet Engineering Task Force (IETF) and its predecessors: a small group of motivated industry leaders and researchers solving infrastructure problems beyond organizational boundaries and within existing regulations.

## Roles

- **Editors** — maintain specific documents, judge rough consensus on threads affecting their documents, merge PRs. Each normative document lists its editors in its header.
- **Contributors** — anyone participating via Discussions, Issues, or PRs. Standing is earned by the merit of contributions.
- **Task Force** — resolves cross-document conflicts, appoints editors, sets milestone dates, and approves publication of new RFCs.

## Document lifecycle

```
Draft (seeking input) → Proposed (rough consensus on scope & approach)
    → Stable vXX.Y (implementable; changes require compatibility statement)
    → RFC (immutable snapshot published to rfcs/)
```

Protocol versions follow a **YY.N** scheme (e.g., 26.0 = first 2026 release). G2P, GCAP, and DESP version independently; the README carries the compatibility matrix.

## Rough consensus

Decisions are made by rough consensus as judged by the responsible editor: the question is not whether everyone agrees, but whether all objections have been considered and addressed or explicitly overruled with recorded rationale. Sustained objections are documented in the decision log even when overruled.

## Decision log

| Date | Decision | Rationale | Thread |
|---|---|---|---|
| 2026-08 | Publish RFC #1; decompose into living specs (this repo structure) | Separate immutable narrative from evolving normative text; give the community focused surfaces for comment | — |

## Trademarks

"Grid 2.0"™, "G2TF"™, "G2P"™, "GCAP"™, and "DESP"™ are trademarks of the Grid 2.0 Task Force (see [NOTICE.md](NOTICE.md)). A trademark usage policy governing how the marks may describe conformant implementations is forthcoming from the Task Force and will be published in this repository.

## Relationship to formal standards bodies and regulators

Grid 2 is voluntary and sits inside existing Grid 1 rules. The G2TF coordinates with, but does not supersede, NERC, FERC, utility, and TSO/ISO requirements. Alignment work with IEEE 2030.5 and related standards is tracked in Discussions. A companion document incorporating detailed regulatory and engineering concerns is in development with focused stakeholder outreach (hyperscalers/utilities/state regulators under committed contracts; research labs including EPRI, Purdue, Duke, Emerald.ai, GridCare, Nvidia; ERCOT, SPP, PJM, MISO; NERC, FERC, DOE; and the international community via the World Economic Forum).
