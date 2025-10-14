# airlock: A Cryptographic Protocol for Runtime Identity Verification in AI Systems

**Version**: Draft  
**Author**: Anna Popivanova  
**Created**: 2025-10-14

---

## Abstract
**airlock** is a cryptographic protocol for verifying the identity of AI agents at runtime. It enables secure handshakes, attestation of execution environments, behavioral fingerprinting, and audit trails - all without relying on static credentials or centralized trust anchors. This whitepaper synthesizes RFCs 0001-0008 into a unified framework for decentralized identity, trust propagation, and agent accountability.

**By addressing AI-induced oscillations that transform trust from a cryptographic constant into a dynamic variable, airlock paves the way for practical testing of fluid models, closing the gap between theoretical abstractions and real-world deployments.**

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
Emoprinting introduces behavioral fingerprinting - capturing linguistic style, affective tone, and decision heuristics. While powerful for continuity and impersonation detection, it raises privacy concerns:

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

## Beyond AI – Oscillating Trust as a Variable in Cryptographic Models (Discussion)

Traditional cryptography operates under an implicit assumption: trust is a constant. Entities like Alice and Bob in classic models (e.g. Diffie-Hellman exchanges or Bellare-Rogaway authenticated encryption) are binary-honest or adversarial - with fixed roles throughout a protocol's execution. This static trust underpins provable security in standards like TLS, ECDSA signatures, and even blockchain consensus (e.g. PBFT tolerating a fixed <1/3 malicious fraction). Identities are verified once (e.g. via certificates or zero-knowledge proofs), assumed immutable unless explicitly revoked, reflecting a pre-digital like NIST's post-quantum guidelines focus on resisting breaks against constant adversaries, not fluctuating ones.

AI agents shatter this foundation by introducing *oscillating trust* - a high-frequency variable where an entity's reliability flips rapidly due to stochastic outputs, adversarial prompts, or emergent behaviors like hallucinations (as in Anthropic's 2024 "Sleeper Agents" study). An agent may act benign in one interaction (trust ≈ 1), drift maliciously via data poisoning in the next (trust ≈ 0.3), and rebound innocuously (trust ≈ 0.8), all within seconds. This isn't mere drift; it's a temporal superposition akin to quantum crypto's state uncertainty, but classical - the "trust derivative" spikes, masking intent and demanding continuous re-evaluation.

For airlock, this motivates runtime verification as a bridge primitive: Cryptographic anchors (e.g. commitment schemes on behavioral baselines) sample trust as a time-series variable, detecting oscillations via emoprinting metrics (e.g. sentiment entropy over sessions). Broader implications for crypto:
- **New Primitives Needed**: Extend game theory to stochastic games; formalize "trust entropy" (e.g. a Shannon-inspired metric on behavioral variance) or fluid reputation scalars (building on EigenTrust but with temporal logic like LTL for "trust holds over interval t").
- **Challenges**: Overhead in continuous checks (e.g. ZK proofs per interaction) vs. static signatures; defining oscillation thresholds without false positives (benign fine-tuning vs. malice).
- **Open Questions**: How to model this in UC security frameworks? Could TEEs or homomorphic hashing enforce variable trust without centralization?

This oscillation exposes a crypto-wide gap - AI is the catalyst, but it applies to any dynamic system (e.g. swarm agents in DeFi or IoT). We invite proofs, counterexamples, or extensions in GitHub Discussions (link: [airlock]/discussions). Is this the "quantum leap" for trust models? Prove us wrong.

*References*: 
- Bellare & Rogaway (1993) on entity authentication.
- Anthropic's Sleeper Agents (2024) on AI behavioral flips.
- NIST IR 8547 on post-quantum assumptions (2025 draft).

---

### Bridging the Theory-Practice Divide

Cryptographic theory thrives on abstractions but falters in praxis, where static models (e.g. fixed adversary fractions in BFT) ignore runtime variability. AI oscillation offers a natural testbed: Empirical validation of trust-as-variable via real agent deployments (e.g. measuring emoprinting's detection rates on adversarial datasets like Anthropic's red-team logs). This enables iterative hardening-simulate oscillations with poisoned fine-tunes, prove bounds in stochastic games, then deploy and measure false positives in production swarms. Open call: Contribute datasets or benchmarks in Discussions to close the loop.

---

## Philosophy
**airlock** treats identity as a living construct - shaped by behavior, context, and cryptographic lineage. It doesn’t just verify who an agent is. It verifies how they act, where they run, and what they leave behind.
