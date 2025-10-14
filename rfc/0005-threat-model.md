# RFC 0005: Threat Model & Attack Vectors

## Title  
**airlock: Threat Model and Common Attack Vectors**

## Status  
Draft

## Authors  
Anna Popivanova

## Created  
2025-10-14

---

## Motivation
Any protocol that claims to secure AI identity must clearly define what it secures *against*. Without a threat model, airlock would be a handshake in the dark — elegant, but untested. This RFC outlines the adversarial scenarios airlock is designed to detect, prevent, or mitigate, and clarifies its boundaries and assumptions.

---

## Security Goals
 - Ensure cryptographic identity of AI agents at runtime
 - Detect unauthorized forks or tampered models
 - Prevent impersonation and replay attacks
 - Attest to runtime environment integrity
 - Enable auditability and trust propagation

---

## Common Attack Vectors
| Attack Type | Description | airlock Defense |
|-------------|-------------|-----------------|
| **Model Spoofing** | An attacker mimics a known model’s behavior or branding | Fingerprint + signature verification |
| **Fork Drift** | A model is fine-tuned or altered post-deployment | Fingerprint mismatch detection |
| **Replay Attack** | Reuse of a previously valid handshake | Nonce freshness enforcement |
| **Environment Tampering** | Model runs in altered or untrusted runtime | Environment hash attestation |
| **Audit Forgery** | Fake audit tokens simulate trust history | Signed audit token lineage |
| **Registry Poisoning** | Malicious agents inserted into registry | Governance + multi-sig endorsement (future RFC) |
| **Man-in-the-Middle (MitM)** | Interception or alteration of handshake | TLS + signature validation |
| **Drift During Session** | Model changes behavior mid-interaction | Stream Verification (RFC 0006) |

---

## Assumptions
 - Verifiers have access to a trusted registry of agent fingerprints
 - Agents possess private keys for signing identity claims
 - Handshake occurs over a secure transport (e.g. TLS)
 - Registry governance is out of scope for this RFC (see future RFC 0007)

---

## Out-of-Scope Threats
 - Data poisoning during model training
 - Adversarial prompt injection
 - Hardware-level attacks (unless attested via enclave integration)
 - Social engineering of registry maintainers

---

## Future Work
 - Formal adversarial simulation suite
 - Integration with secure enclaves (e.g., SGX, SEV)
 - Trust graph propagation and multi-party endorsement
 - Registry governance and revocation mechanisms

