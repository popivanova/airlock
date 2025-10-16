![Status](https://img.shields.io/badge/status-draft-yellow)
![License](https://img.shields.io/badge/license-MIT-blue)
![Spec](https://img.shields.io/badge/spec-RFC%200001--0006-green)
![Security](https://img.shields.io/badge/security-zero--trust-critical)
![Verified Agents](https://img.shields.io/badge/agents-cryptographically%20verified-9cf)
![Stream Verification](https://img.shields.io/badge/mode-stream%20verification-blueviolet)

# airlock
**airlock** is a cryptographic zero-trust protocol for runtime identity verification of AI agents, addressing trust fractures in distributed systems. It enables real-time attestation of model provenance, environment integrity, and agent authenticity - without relying on vendor trust or static manifests.

**By addressing AI-induced oscillations that transform trust from a cryptographic constant into a dynamic variable, airlock paves the way for practical testing of fluid models, closing the gap between theoretical abstractions and real-world deployments.**

---

## Motivation
AI agents are increasingly embedded in both explicit and implicit interactions across critical domains, making AI identity verification essential. 
**airlock** introduces a lightweight cryptographic protocol that verifies AI agents' identities at runtime and at rest.
It addresses key disruptions in traditional trust models triggered by AI: identity drift, rapid impersonation, and fragile behavioral continuity — all of which can lead to sudden trust collapse.

AI identity isn't monolithic - it drifts, rendering trust fluid and fragile. It also erodes quickly yet rebuilds too readily, masking malicious patterns that would expose and red flag intent in human contexts.

airlock's runtime verification anchors agents while preserving user privacy, ensuring identity consistency and protecting inferences (emotional, behavioral, and knowledge-based) from threats. We also introduce **emoprints**, affective and emotional fingerprinting across AI interactions, as an added layer for robust identity assurance. **More fundamentally, AI's rapid oscillations turn cryptography's implicit trust constant (binary honest/adversary roles) into a dynamic variable, demanding new primitives beyond static verifications. Explored further in our [whitepaper](https://github.com/popivanova/airlock/blob/main/whitepaper.md) Discussion section.**

Unlike human interactions, where volatility is often evident and prompts proportionate emotional response, AI-mediated breakdowns are frequently obscured. These failures - whether rooded in malicious intent or benign anomalies - can go undetected, miscalibrated user trust. Any breach in trustworthiness should trigger a response governed by a threshold of acceptable untrustworthiness: a user- and context-dependent boundary that determines whether engagement continues, pauses, or terminates. That threshold must be transparent, user-governed, and tightly coupled to the domain’s risk profile - ensuring that trust decisions reflect both situational stakes and individual agency.

We welcome feedback, critiques, "prove us wrong" challenges, implementations of potential attacks, or explorations of the algorithm via GitHub issues or discussions.

---

## Core Concepts
- **Agent Fingerprint**: Hash of model weights + metadata
- **Environment Attestation**: Snapshot of runtime context
- **Signed Nonce Challenge**: Proof of liveness and integrity
- **Audit Token**: Verifiable record of interaction
- **Verification Modes**: Block vs Stream (RFC 0006)

---

## Protocol RFCs
| RFC | Title | Status |
|-----|-------|--------|
| [0001](rfc/0001-airlock-handshake.md) | **airlock** Protocol for Verifying AI Model Identity at Runtime | Draft |
| [0002](rfc/0002-agent-fingerprint.md) | Agent Fingerprint Specification | Draft |
| [0003](rfc/0003-environment-attestation.md) | Environment Attestation | Draft |
| [0004](rfc/0004-audit-token.md) | Audit Token Specification | Draft |
| [0005](rfc/0005-threat-model.md) | Threat Model & Attack Vectors | Draft |
| [0006](rfc/0006-verification-modes.md) | Verification Modes (Block vs Stream) | Draft |
| [0007](rfc/0007-registry-governance-trust-graphs.md) | Registry Governance & Trust Graphs | Draft |
| [0008](rfc/0008-emoprinting.md) | Emoprinting | Draft |

---

## Examples
 - `examples/spoofed-agent.json` - handshake failure due to fingerprint mismatch  
 - `examples/verified-agent.json` - successful handshake with audit token

---

## Get Started
Test handshake: `git clone; python examples/verified-agent.py`.

---

## Contribute
tbd

---

## Roadmap
See [ROADMAP.md](https://github.com/popivanova/airlock/blob/main/ROADMAP.md) for planned features (e.g. PoC Q4 2025)

---

## Privacy Disclaimer
**airlock** is designed to verify the identity of AI agents - not humans. The protocol does not process, transmit, or store any Personally Identifiable Information (PII) or Sensitive PII (SPII).

All identifiers (e.g., agent_id, fingerprint, environment_hash) are cryptographic or system-level artifacts that do not correspond to individuals. Audit tokens and handshake payloads are machine-verifiable and privacy-neutral by design.

---

## License
This project is licensed under the [MIT License](LICENSE).  
You may use, modify, and distribute it freely with attribution.

---

## Status
This repo is under active development. Initial RFCs are in status Draft, fully specified for community review but open to changes. Contributions welcome.
