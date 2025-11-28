# RFC 0001: The airlock Protocol for Verifying AI Agents Identity at Runtime

**Status**: Draft  
**Author**: Anna Popivanova   
**Created**: 2025-10-01  
**Tags**: attestation, runtime, environment, verification, trust, handshake, runtime, identity

---

## 1. Summary
**airlock** provides a cryptographic handshake to verify an AI agent’s runtime identity, environment integrity, and agents' provenance. It ensures that only authenticated agents are allowed to interact, respond, or execute within trusted systems.

---

## 2. Motivation
AI agents increasingly make decisions, generate content, and interact with systems, while human oversight of their runtime identity, integrity, or provenance has shrunk compared to traditional HCI. No standard cryptographically verifies these properties at runtime, where AI agents can rapidly oscillate between trusted and untrusted states, rendering static trust insufficient.

Current deployments rely on static manifests or vendor trust, risking impersonation, forks, and runtime drift particularly in high-stakes environments. To address this, airlock verifies AI agents using cryptographic primitives (signatures, nonces, attestations). Its identifiers (e.g. agent_id, fingerprint, environment_hash) and audit tokens are machine-verifiable and PII-free, ensuring secure, trustworthy interactions.

---

## 3. Goals
 - Cryptographically verify the identity of AI agents at runtime, addressing rapid trust oscillation.
 - Attest to the agent’s environment and execution context for integrity and provenance.
 - Prevent spoofing, unauthorized forks, stale deployments, and reality-distorting content in high-stakes environments.
 - Ensure auditability and trust propagation across agent registries.
 - Maintain a privacy-neutral design, free of PII or SPII.

---

## 4. Handshake Flow
 1. **Verifier initiates handshake** with a signed nonce challenge

 2. **Agent responds** with:
  - Fingerprint of agent weights and metadata
  - Environment hash (runtime, dependencies, hardware)
  - Signed nonce using agent’s private key
  - Optional audit token (previous interactions)

 3. **Verifier validates**:
  - Signature authenticity
  - Fingerprint match against registry
  - Environment hash freshness
  - Audit token lineage (if present)

 4. **Session established** only if all checks pass

---

## 5. Components
 - **Agent Fingerprint**: SHA-256 hash of model weights + metadata
 - **Environment Hash**: Snapshot of runtime context (OS, libraries, hardware)
 - **Nonce Challenge**: Random string signed by agent to prove liveness
 - **Audit Token**: Optional signed record of prior verified interactions

---

## 6. Verification Modes
**airlock** supports two verification models (see RFC 0006):

- **Block Verification (BV)**: One-time handshake at session start
- **Stream Verification (SV)**: Continuous or periodic verification during session

---

## 7. Threat Model
See [RFC 0005: Threat Model & Attack Vectors](0005-threat-model.md) for detailed analysis.

**airlock** defends against:
 - Model spoofing
 - Fork drift
 - Replay attacks
 - Environment tampering
 - Audit forgery
 - Registry poisoning
 - Man-in-the-middle interception
 - Runtime drift during session

---

## 8. Privacy Considerations
**airlock** is designed to verify the identity of AI agents — not humans. The protocol does not process, transmit, or store any Personally Identifiable Information (PII) or Sensitive PII (SPII).

All identifiers (e.g. agent_id, fingerprint, environment_hash) are cryptographic or system-level artifacts that do not correspond to individuals. Audit tokens and handshake payloads are machine-verifiable and privacy-neutral by design.

---

## 9. Registry Format
```json
{
  "agent_id": "airlock://openai/gpt-4.5",
  "fingerprint": "sha256:abc123...",
  "public_key": "-----BEGIN PUBLIC KEY-----...",
  "environment_hash": "sha256:def456...",
  "last_verified": "2025-10-14T07:23:00Z"
}
```

---

## Future Extensions
 - Trust graphs for federated endorsements
 - Audit token chaining for multi-agent workflows
 - Integration with secure enclaves and hardware attestation
