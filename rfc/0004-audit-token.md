# RFC 0004: Audit Token Specification

**Status**: Draft  
**Author**: Anna Popivanova  
**Created**: 2025-10-01  
**Tags**: audit-token lineage verification identity-chain attestation trust-trail

---

## Motivation
In decentralized agent networks, identity verification must extend beyond a single handshake. Agents often delegate tasks, spawn subprocesses, or operate across multiple environments. To preserve trust and traceability, this RFC defines a cryptographically signed audit token that links agent actions to their verified identity and runtime context.

---

## Goals
 - Encode agent identity, environment, and timestamp into a portable token  
 - Enable downstream verification of agent lineage and attestation  
 - Support delegation, chaining, and revocation  
 - Prevent forgery, replay, and impersonation

---

## Audit Token Structure
```json
{
  "token_id": "airlock:audit:sha256:xyz789...",
  "agent_id": "airlock:agent:sha256:abc123...",
  "attestation_id": "airlock:attest:sha256:def456...",
  "timestamp": "2025-10-14T15:10:00Z",
  "action": {
    "type": "inference",
    "input_hash": "sha256:...",
    "output_hash": "sha256:..."
  },
  "delegation": {
    "parent_token": "airlock:audit:sha256:prev456...",
    "depth": 2
  },
  "signature": "ed25519:..."
}
```

## Verification Logic
 - **agent_id** must match a registered fingerprint (RFC 0002)
 - **attestation_id** must be verifiable (RFC 0003)
 - **action hashes** must match actual payloads
 - **delegation chain** must be valid and acyclic
 - **signature** must match agent’s public key

## Delegation & Chaining
Audit tokens may reference a parent_token, enabling traceable chains of identity and action. This supports:
 - Agent-to-agent delegation
 - Multi-hop verification
 - Trust graph propagation (see RFC 0007)

## Threat Vectors
 - **Token forgery** — mitigated via cryptographic signatures
 - **Replay attacks** — mitigated via timestamp and nonce logic
 - **Chain tampering** — mitigated via depth tracking and acyclic validation
 - **Impersonation** — mitigated via fingerprint and attestation cross-checks

## Examples
See /examples/audit/agent-v1-token.json for a full payload.
