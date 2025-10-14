# RFC 0001: airlock Handshake Protocol
## Title: 
**airlock: A Cryptographic Handshake Protocol for Verifying AI Model Identity at Runtime**

## Status:
Draft

## Authors:
Anna Popivanova

## Created:
2025-10-14

## Summary
airlock defines a cryptographic handshake between a verifier and an AI agent to establish runtime identity, environment integrity, and model provenance. It ensures that only authenticated agents are allowed to interact, respond, or execute within trusted systems.

## Motivation
AI agents are becoming increasingly autonomous, capable of making decisions, generating content, and interacting with other systems without direct human oversight. Yet despite their growing influence, there is no widely adopted standard for verifying *who* an agent truly is at runtime.
Today’s deployments rely heavily on static manifests, vendor trust, or opaque infrastructure - none of which provide cryptographic guarantees about the identity, integrity, or provenance of the model in use. This gap exposes systems to impersonation, unauthorized forks, and runtime drift, especially in high-stakes or distributed environments.

**airlock** addresses this by introducing a lightweight, cryptographically grounded handshake protocol. It enables verifiers to challenge and confirm the identity of an AI agent in real time, ensuring that only trusted models are allowed to speak, act, or execute within sensitive scopes.

By rooting its design in established cryptographic primitives - signatures, nonces, attestations - airlock avoids reinventing security and instead applies proven techniques to a new class of actors: autonomous AI.

---

## Goals
 - Cryptographically verify the identity of an AI model at runtime
 - Attest to the model’s environment and execution context
 - Prevent spoofing, unauthorized forks, and stale deployments
 - Enable auditability and trust propagation across agent registries

## Handshake Flow
 1. **Verifier initiates handshake** with a signed nonce challenge

 2. **Agent responds** with:
  - Fingerprint of model weights and metadata
  - Environment hash (runtime, dependencies, hardware)
  - Signed nonce using agent’s private key
  - Optional audit token (previous interactions)

 3. **Verifier validates**:
  - Signature authenticity
  - Fingerprint match against registry
  - Environment hash freshness
  - Audit token lineage (if present)

 4. **Session established** only if all checks pass

## Components
 - **Agent Fingerprint**: SHA-256 hash of model weights + metadata
 - **Environment Hash**: Snapshot of runtime context (OS, libraries, hardware)
 - **Nonce Challenge**: Random string signed by agent to prove liveness
 - **Audit Token**: Optional signed record of prior verified interactions

---

## Verification Modes

airlock supports two verification models (see RFC 0006):

- **Block Verification (BV)**: One-time handshake at session start
- **Stream Verification (SV)**: Continuous or periodic verification during session

---

## Threat Model
See [RFC 0005: Threat Model & Attack Vectors](0005-threat-model.md) for detailed analysis.

airlock defends against:
 - Model spoofing
 - Fork drift
 - Replay attacks
 - Environment tampering
 - Audit forgery
 - Registry poisoning
 - Man-in-the-middle interception
 - Runtime drift during session


## Registry Format
json
{
  "agent_id": "airlock://openai/gpt-4.5",
  "fingerprint": "sha256:abc123...",
  "public_key": "-----BEGIN PUBLIC KEY-----...",
  "environment_hash": "sha256:def456...",
  "last_verified": "2025-10-14T07:23:00Z"
}

Future Extensions
 - Trust graphs for federated endorsements
 - Audit token chaining for multi-agent workflows
 - Integration with secure enclaves and hardware attestation
