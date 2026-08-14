# Contributing to the Grid 2.0 Standards

The G2TF works with an ethos modeled on the IETF:

- **Start small, stay focused**
- **Open participation, individual merit**
- **Time-limited milestones**
- **Get rough consensus, publish, then run**

Participation is open to individuals. You do not need to represent an organization, and organizational affiliation confers no additional standing.

## Where things happen

| Channel | Use it for |
|---|---|
| **GitHub Discussions** | Open technical questions, design alternatives, implementation reports |
| **Issues** | Concrete defects: ambiguities, contradictions, errata against RFC #1, missing normative requirements |
| **Pull requests** | Proposed specification text against `specs/`, `members/`, `architecture/` |
| **G2TF WhatsApp Community** | Cross-organization real-time news, policy debate |

## Discussion categories

Discussions are organized around the select technical open-question areas from RFC #1:

1. **Commercial terms** — enforcement of flexible capabilities, limits on differential service classes, congestion-solving investment decisions, rate structure impacts
2. **Reliability assurance** — coincidental load shedding and system stability, materialization of flexibility commitments at scale, compliance incentives
3. **Engineering** — headroom sufficiency for coincident swings, cybersecurity / NERC CIP, standardization of transmission-owner input signals

## The comment cycle

1. **Raise** — open a Discussion (question/alternative) or Issue (defect).
2. **Converge** — editors summarize positions; when a direction has rough consensus, an editor or the proposer opens a PR with spec text.
3. **Review** — PRs against normative documents require review by two spec editors. Normative changes must use RFC 2119 keywords and state their compatibility impact.
4. **Record** — merged decisions are logged in `GOVERNANCE.md`'s decision log with a one-paragraph rationale and links to the originating thread. Consensus is judged by the responsible editor ("rough consensus"), not by vote.
5. **Run** — implementations (Phase 0 shadow mode and beyond) report experience back via Discussions; running code informs the next revision.

## Writing conventions

- Normative documents (`specs/`, `members/`, and `architecture/` files not marked `Status: Informative`) use **MUST / MUST NOT / SHOULD / SHOULD NOT / MAY** per IETF [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119) / [RFC 8174](https://www.rfc-editor.org/rfc/rfc8174).
- Informative documents (those carrying `Status: Informative`) avoid RFC 2119 keywords.
- Every normative file carries a status header: `Status: Draft — seeking input`, `Status: Proposed`, or `Status: Stable (vXX.Y)`.
- One sentence per line is preferred for new or substantially revised normative text, to keep diffs reviewable.
- RFCs in `rfcs/` are immutable. Corrections are filed as `errata` issues and resolved in living specs.

## Acknowledgment

Substantive contributors are acknowledged in subsequent RFC publications, following the model of RFC #1's acknowledgments section.
