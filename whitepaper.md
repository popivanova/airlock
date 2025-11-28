# airlock: A Cryptographic Protocol for Runtime Identity Verification in AI Systems

**Version**: Draft  
**Author**: Anna Popivanova  
**Created**: 2025-10-14

---

## 1.Abstract
**airlock** is a cryptographic protocol for verifying the identity of AI agents at runtime. It enables secure handshakes, attestation of execution environments, affective fingerprinting, and audit trails - all without relying on static credentials or centralized trust anchors. This whitepaper synthesizes RFCs 0001-0008 into a unified framework for decentralized identity, trust propagation, and agent accountability.

**By addressing AI-induced oscillations that turn trust from a cryptographic constant into a dynamic variable, airlock enables practical testing of adaptive trust models - bridging the gap between abstract theory and real-world deployment. Crucially, it reframes identity from binary roles to quantum-like superpositions: agents in flux, trust in motion.** **airlock** treats identity as a living construct - shaped by behavior, context, and cryptographic lineage. It doesn’t just verify who an agent is. It verifies how they act, where they run, and what they leave behind.

---

## 2.Motivation
AI agents increasingly operate across distributed systems, cloud runtimes, and edge devices. They also introduce variability by fragmenting data payloads into opaque micro-chunks, exponentially accelerating processing speeds beyond human validation capacity, and enabling cross-pollination of datasets/models with questionable data provenance. Traditional identity models - static keys, API tokens, or container hashes - fail to capture this dynamic, behavioral, and contextual nature of modern agents. airlock introduces a zero-trust handshake protocol that verifies agents in motion, not just at rest.

---

## 3. Architecture

### 3.1. Protocol Components

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

### 3.2. Trust Flow

1. **Agent initiates handshake** ([RFC 0001](rfc/0001-airlock-handshake.md))  
2. **Fingerprint and attestation verified** ([RFC 0002](rfc/0002-agent-fingerprint.md) - [RFC 0003](rfc/0003-environment-attestation.md))  
3. **Audit token issued for actions** ([RFC 0004](rfc/0004-audit-token.md))  
4. **Trust graph updated** ([RFC 0007](rfc/0007-registry-governance-trust-graphs.md))  
5. **Emoprint checked for continuity** ([RFC 0008](rfc/0008-emoprinting.md))

Each step is cryptographically signed, timestamped, and optionally chained for lineage tracking.

---

### 3.3. Threat Model

**airlock** defends against:
- Impersonation and spoofing  
- Replay and forgery  
- Environment tampering  
- Behavioral mimicry  
- Registry poisoning  
- Delegation abuse

See [RFC 0005](rfc/0005-threat-model.md) for detailed vectors and mitigations.

---
### 3.4. Verification Modes
**airlock** supports:
- **Strict**: All checks enforced  
- **Adaptive**: Context-aware verification  
- **Optional**: Minimal identity anchoring

Modes are configurable per deployment. See [RFC 0006](rfc/0006-verification-modes.md).

---

### 3.5. Governance Models
Trust graphs may be governed via:
- Centralized registries  
- Federated authorities  
- Autonomous agent consensus

Each model defines quorum, edge validation, and revocation logic. See [RFC 0007](rfc/0007-registry-governance-trust-graphs.md).

---

## 4. Emoprinting & Privacy
Emoprinting introduces behavioral fingerprinting - capturing linguistic style, affective tone, and decision heuristics. While powerful for continuity and impersonation detection, it raises privacy concerns:

- May qualify as PII or SPII  
- Enables cross-session traceability  
- Lacks regulatory precedent

Further investigation and ethical posturing are required. See [RFC 0008](rfc/0008-emoprinting.md) for schema and safeguards.

---

## 5. Implementation Notes
- All payloads are JSON-based  
- Signatures use Ed25519  
- Hashes use SHA-256  
- Time is UTC ISO 8601  
- Examples available in `/examples/`

---

## 6. Beyond AI – Oscillating Trust as a Variable in Cryptographic Models (Discussion)

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

### 6.1. Bridging the Theory-Practice Divide

Cryptographic theory thrives on abstractions but falters in praxis, where static models (e.g. fixed adversary fractions in BFT) ignore runtime variability. AI oscillation offers a natural testbed: Empirical validation of trust-as-variable via real agent deployments (e.g. measuring emoprinting's detection rates on adversarial datasets like Anthropic's red-team logs). This enables iterative hardening-simulate oscillations with poisoned fine-tunes, prove bounds in stochastic games, then deploy and measure false positives in production swarms. Open call: Contribute datasets or benchmarks in Discussions to close the loop.

---

### 6.2. A Spectrum of Trust: From Binary Constants to Quantum-Like Superpositions

AI oscillations don't obliterate traditional models outright but expose a missing middle: An *in-between* operable regime blending binary trust (static, deterministic) with fluid variability, akin to quantum superposition in cryptography. In quantum key distribution (e.g. BB84 protocols), bits exist in overlaid states until measurement disturbs them—trust is probabilistic and interference-prone. AI agents mimic this classically: An entity's "state" superposes benign and adversarial potentials (e.g., via stochastic sampling or prompt ambiguity), unresolved until runtime interaction "measures" it, potentially collapsing to malice.

**Contrasting Models in Operable Terms**:
| Trust Model | Description | Operable Strengths | AI-Induced Weaknesses | airlock Mitigation |
|-------------|-------------|---------------------|-----------------------|-------------------|
| **Traditional Binary (Constant)** | Fixed roles (honest=1/adversary=0); verified once, assumed eternal (e.g. PKI in TLS). | Simple proofs, low overhead; works for slow human systems. | Inoperable under flips-revocation lags expose windows (e.g., session hijacks via mid-drift hallucinations). | N/A-too rigid for spectrum. |
| **In-Between Superposition (Quasi-Quantum)** | Probabilistic overlays: Trust as a wavefunction ψ(trust) = α|honest⟩ + β|malicious⟩, with |α|^2 + |β|^2 = 1; collapses on measurement (interaction). Inspired by quantum crypto's uncertainty (e.g., no-cloning for states). | Handles ambiguity; measurable interference (e.g., detect collapses via entropy spikes). Empirically testable in AI (e.g., prompt entropy correlating to flip risk). | Overhead in continuous monitoring; false collapses if benign noise mimics malice (e.g., creative LLM outputs flagged). | Runtime sampling "measures" without full disturbance-emoprinting computes coefficients α/β via behavioral KL-divergence, preserving privacy. |
| **Full Oscillation (Variable Chaos)** | High-frequency flips post-collapse; trust as a chaotic time-series (e.g., Markov jumps). | Captures real AI rapidity; robust to unknowns. | Inoperable predictability-proofs dissolve in entropy soup (e.g., no static Nash equilibria). | Anchors post-collapse continuity, rebuilding with audit trails. |

This spectrum restores operability: Treat AI trust as quasi-quantum to extend classical primitives (e.g., superposition-proof ZK via continuous attestations). Challenges: Defining collapse thresholds (e.g., via quantum-inspired metrics like fidelity F(ψ1, ψ2)). Open for exploration: Simulate in code (QuTiP for quantum analogs on classical data)-fork and model an agent's wavefunction in Discussions.

*References*: BB84 (Bennett & Brassard, 1984); Quantum superposition in crypto (e.g., IEEE Quantum 2025 reviews).

---

## 7. Future Work
- Threat simulation suite  
- Emoprint drift scoring  
- Trust graph visualization  
- Contributor tooling and docs  
- Formal privacy posture
