# G2P — Grid 2.0 Protocol

**Version:** 26.0-draft · **Status:** Draft — seeking input · **Editors:** TBD
**Role in stack:** Addressing, service configuration, and response — the transport and message layer beneath [GCAP](../gcap/spec.md) and [DESP](../desp/spec.md).

The key words MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are to be interpreted as described in RFC 2119 / RFC 8174.

## 1. Scope

G2P defines how Grid 2 elements identify themselves, describe their service configuration, exchange per-interval messages, and detect staleness. G2P carries — but does not define — the allocation semantics (GCAP) and the service-class taxonomy (DESP).

## 2. Element identity and addressing

- Every Member Element and Allocator MUST hold a stable element identifier bound to a physical point of interconnection within a provisioned Allocation Domain.
- *(Open: identifier format — recommend a domain-scoped hierarchical ID mirroring the constraint-domain nesting in [federation.md](../../architecture/federation.md).)*

## 3. Message types

G2P defines four message families. All are per-interval (one minute) unless noted.

### 3.1 Service Descriptor (Member → Allocator)

A Member's signed statement of its requests/offers for a forward time vector:

- **Use:** per-class *request to consume* (+), one signed position per service class (per DESP), over a forward time vector.
- **Buffer:** *offer to be a source or use* (− discharge / + charge); a Buffer sits on either side of the ledger.
- **Source:** *offer to supply* (−), generation available this window, over a forward time vector.

Requirements:
- Each position MUST be signed by the originating Member.
- Positions MUST be expressed in units of energy within the interval (v26.0 scope).
- A Service Descriptor MAY be reissued each interval; classes MAY change per interval (DESP dynamic reclassification).
- *(Open: forward-vector length, resolution, and revision rules.)*

### 3.2 Commitment (Allocator → Member)

- Per-class **commit-%** to Use Members; **committed dispatch** to Buffers (cleared before any load is curtailed); **committed take** to Sources.
- Commitments MUST identify the interval, the domain, and the clearing inputs version they were computed against.
- A Member MUST treat a missing or stale Commitment as fallback-triggering per the [failsafe model](../../architecture/failsafe-model.md).

### 3.3 Federation Announcement (Allocator ↔ Allocator)

- Announce-and-listen exchange across coupled zones; MUST identify announcing domain, interval, and coupled-boundary quantities. See [federation.md](../../architecture/federation.md).

### 3.4 Response / Telemetry (Member → Allocator)

- Members are responsible for **verified self-dispatch**: each Member MUST report actual per-class dispatch against its Commitment so that compliance is auditable and the overlay's aggregate footprint is measurable.
- *(Open: verification granularity, metering source of truth, attestation.)*

## 4. Timing

- All messages are bound to a one-minute interval clock (see [temporal-position.md](../../architecture/temporal-position.md)).
- *(Open: intra-interval timing budget — descriptor deadline, clearing deadline, commitment publication deadline; clock sync requirements.)*

## 5. Fault semantics

- Loss of connectivity, missed Commitments beyond the staleness threshold, or invalid clearing inputs MUST trigger the element-specific fallback behaviors in [failsafe-model.md](../../architecture/failsafe-model.md).

## 6. Security

- Transmission-level deployments are expected to run on private networks.
- All Service Descriptors and Commitments MUST be authenticated; message integrity MUST be verifiable end-to-end.
- *(Open: PKI / key management, NERC CIP mapping, replay protection — Discussion: Engineering.)*

## 7. To be specified

Wire format and encoding · state machines per element · version negotiation · conformance test vectors. Contributions welcome via PR; see [CONTRIBUTING.md](../../CONTRIBUTING.md).
