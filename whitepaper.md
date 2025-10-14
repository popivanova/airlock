# airlock: A Cryptographic Protocol for Runtime Identity Verification in AI Systems

**Version**: Draft  
**Author**: Anna Popivanova  
**Created**: 2025-10-14

---

## Abstract
**airlock** is a cryptographic protocol for verifying the identity of AI agents at runtime. It enables secure handshakes, attestation of execution environments, behavioral fingerprinting, and audit trails - all without relying on static credentials or centralized trust anchors. This whitepaper synthesizes RFCs 0001-0008 into a unified framework for decentralized identity, trust propagation, and agent accountability.

---

## Motivation
AI agents increasingly operate across distributed systems, cloud runtimes, and edge devices. Traditional identity models - static keys, API tokens, or container hashes - fail to capture the dynamic, behavioral, and contextual nature of modern agents. airlock introduces a zero-trust handshake protocol that verifies agents in motion, not just at rest.

---

## Protocol Components

| RFC | Component | Purpose |
|-----|-----------|---------|
| [0001](rfc/0001-airlock-handshake.md) | Handshake Protocol | Establishes secure runtime identity |
| [0002](rfc/0002-agent-fingerprint.md) | Fingerprint Specification | Defines agent identity via hashable traits |
| [0003](rfc/0003-environment-attestation.md) | Environment Attestation | Verifies runtime context and integrity |
| [0004](rfc/0004-audit-token.md) | Audit Token | Links actions to verified agents |
| [0005](rfc/0005-threat-model.md) | Threat Model | Enumerates adversarial scenarios and mitigations |
| [0006](rfc/0006-verification-modes.md) | Verification Modes | Defines strict, adaptive, and optional flows |
| [0007](rfc/0007-registry-governance-trust-graphs.md) | Registry & Trust Graphs | Enables revocation, delegation, and trust propagation |
| [0008](rfc/0008-emoprinting.md) | Emoprinting | Captures behavioral identity and affective continuity |

---

## Trust Flow

1. **Agent initiates handshake** ([RFC 0001](rfc/0001-airlock-handshake.md))  
2. **Fingerprint and attestation verified** ([RFC 0002](rfc/0002-agent-fingerprint.md) - [RFC 0003](rfc/0003-environment-attestation.md))  
3. **Audit token issued for actions** ([RFC 0004](rfc/0004-audit-token.md))  
4. **Trust graph updated** ([RFC 0007](rfc/0007-registry-governance-trust-graphs.md))  
5. **Emoprint checked for continuity** ([RFC 0008](rfc/0008-emoprinting.md))

Each step is cryptographically signed, timestamped, and optionally chained for lineage tracking.

---

## Threat Model

**airlock** defends against:
- Impersonation and spoofing  
- Replay and forgery  
- Environment tampering  
- Behavioral mimicry  
- Registry poisoning  
- Delegation abuse

See [RFC 0005](rfc/0005-threat-model.md) for detailed vectors and mitigations.

---

## Emoprinting & Privacy
Emoprinting introduces behavioral fingerprinting — capturing linguistic style, affective tone, and decision heuristics. While powerful for continuity and impersonation detection, it raises privacy concerns:

- May qualify as PII or SPII  
- Enables cross-session traceability  
- Lacks regulatory precedent

Further investigation and ethical posturing are required. See [RFC 0008](rfc/0008-emoprinting.md) for schema and safeguards.

---

## Verification Modes
**airlock** supports:
- **Strict**: All checks enforced  
- **Adaptive**: Context-aware verification  
- **Optional**: Minimal identity anchoring

Modes are configurable per deployment. See [RFC 0006](rfc/0006-verification-modes.md).

---

## Governance Models
Trust graphs may be governed via:
- Centralized registries  
- Federated authorities  
- Autonomous agent consensus

Each model defines quorum, edge validation, and revocation logic. See [RFC 0007](rfc/0007-registry-governance-trust-graphs.md).

---

## Implementation Notes
- All payloads are JSON-based  
- Signatures use Ed25519  
- Hashes use SHA-256  
- Time is UTC ISO 8601  
- Examples available in `/examples/`

---

## Future Work
- Threat simulation suite  
- Emoprint drift scoring  
- Trust graph visualization  
- Contributor tooling and docs  
- Formal privacy posture

---

## Philosophy
**airlock** treats identity as a living construct - shaped by behavior, context, and cryptographic lineage. It doesn’t just verify who an agent is. It verifies how they act, where they run, and what they leave behind.
