![Status](https://img.shields.io/badge/status-draft-yellow)
![License](https://img.shields.io/badge/license-MIT-blue)
![Spec](https://img.shields.io/badge/spec-RFC%200001--0006-green)
![Security](https://img.shields.io/badge/security-zero--trust-critical)
![Verified Agents](https://img.shields.io/badge/agents-cryptographically%20verified-9cf)
![Stream Verification](https://img.shields.io/badge/mode-stream%20verification-blueviolet)

# airlock
**airlock** is a cryptographic handshake protocol for verifying AI model identity at runtime.
It enables real-time attestation of model provenance, environment integrity, and agent authenticity - without relying on vendor trust or static manifests.

---

## Motivation
AI agents are increasingly autonomous, but we lack a standard for verifying *who* they are.  
**airlock** introduces a lightweight, cryptographically grounded protocol to ensure that only trusted models are allowed to speak.

---

## Core Concepts
- **Agent Fingerprint**: Hash of model weights + metadata
- **Environment Attestation**: Snapshot of runtime context
- **Signed Nonce Challenge**: Proof of liveness and integrity
- **Audit Token**: Verifiable record of interaction
- **Verification Modes**: Block vs Stream (RFC 0006)

---

## RFC Index
| RFC | Title |
|-----|-------|
| [0001](rfc/0001-airlock-handshake.md) | **airlock** Protocol for Verifying AI Model Identity at Runtime |
| [0002](rfc/0002-agent-fingerprint.md) | Agent Fingerprint Specification |
| [0003](rfc/0003-environment-attestation.md) | Environment Attestation |
| [0004](rfc/0004-audit-token.md) | Audit Token Specification |
| [0005](rfc/0005-threat-model.md) | Threat Model & Attack Vectors |
| [0006](rfc/0006-verification-modes.md) | Verification Modes (Block vs Stream) |
| [0007](rfc/registry-governance-trust-graphs.md) | Registry Governance & Trust Graphs |

---

## Examples
- `examples/spoofed-agent.json` — handshake failure due to fingerprint mismatch  
- `examples/verified-agent.json` — successful handshake with audit token

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
This repo is under active development.  
Initial RFCs are being drafted and refined. Contributions welcome once public.

