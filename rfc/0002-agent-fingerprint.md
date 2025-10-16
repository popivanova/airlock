# RFC 0002: Agent Fingerprint Specification

**Status**: Draft  
**Author**: Anna Popivanova  
**Created**: 2025-10-01  
**Tags**: fingerprinting, identity, verification, attestation

---

## Motivation
In a network of autonomous agents, verifying identity is critical. Traditional identifiers (e.g., UUIDs, public keys) are insufficient when agents are mutable, composable, or cloned. This RFC defines a fingerprinting mechanism that captures both static and behavioral traits of an agent — enabling cryptographic and contextual identity assurance.

---

## Goals

- Generate reproducible fingerprints for agents  
- Support both static (code, weights) and dynamic (behavioral) traits  
- Enable attestation and verification across sessions  
- Resist spoofing, replay, and impersonation

---

## Fingerprint Structure

```json
{
  "agent_id": "airlock:agent:sha256:abc123...",
  "version": "2025.10",
  "fingerprint": {
    "static": {
      "model_hash": "sha256:...",
      "weights_hash": "sha256:...",
      "config_hash": "sha256:..."
    },
    "dynamic": {
      "emoprint_hash": "sha256:...",
      "response_profile": {
        "hedging": 0.72,
        "provocation_reflex": 0.91,
        "humor_signature": "dry-sarcastic",
        "tone_volatility": 0.18
      }
    },
    "environment": {
      "runtime_hash": "sha256:...",
      "platform": "linux-x86_64",
      "dependencies": ["torch==2.1.0", "numpy==1.26.0"]
    }
  },
  "timestamp": "2025-10-14T15:00:00Z",
  "signature": "ed25519:..."
}
```
---

## Verification Logic
 - **Static hashes** must match known agent builds
 - **Dynamic profile** must fall within expected bounds
 - **Signature must** be verifiable against registry public key
 - **Environment hash** must match attested runtime (see RFC 0003)

## Emoprint
Agents may include an emoprint, capturing affective telemetry from affective tone, sentiment patterns, and challenge-response patterns. See [RFC 0008](rfc/0008-emoprinting.md).

## Threat Vectors
 - **Hash collision spoofing** — mitigated via SHA-256 and signed payloads
 - **Behavioral mimicry** — mitigated via emoprint drift detection
 - **Environment forgery** — mitigated via attestation (RFC 0003)

## Examples
See /examples/fingerprint/agent-v1.json for a full payload.
