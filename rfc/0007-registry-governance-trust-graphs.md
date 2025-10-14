# RFC 0007: Registry Governance & Trust Graphs

**Status**: Draft  
**Author**: Anna Popivanova  
**Created**: 2025-10-01  
**Tags**: registry governance, trust-graph, revocation, delegation, identity-verification

---

## Motivation
Verifying agent identity at runtime is only the first step. To scale trust across decentralized systems, we need a governance layer that supports registration, revocation, delegation, and trust propagation. This RFC defines the structure and logic of the airlock registry and its associated trust graph - enabling agents to reason about identity lineage and reputational edges.

---

## Goals
 - Define a registry schema for agent fingerprints and attestations  
 - Enable revocation and delegation of verification authority  
 - Represent trust relationships as a graph with weighted edges  
 - Support federated, centralized, and autonomous governance models

---

## Registry Schema

```json
{
  "agent_id": "airlock:agent:sha256:abc123...",
  "registered_at": "2025-10-14T15:20:00Z",
  "fingerprint": "sha256:...",
  "attestation": "sha256:...",
  "public_key": "ed25519:...",
  "status": "active",
  "delegates": [
    "airlock:agent:sha256:delegate456...",
    "airlock:agent:sha256:delegate789..."
  ],
  "revoked": false,
  "trust_edges": [
    {
      "target": "airlock:agent:sha256:peer999...",
      "weight": 0.85,
      "reason": "verified audit chain"
    }
  ]
}
```

## Trust Graph Structure
 - **Nodes**: Registered agents
 - **Edges**: Directed, weighted trust relationships
 - **Weights**: Float values (0.0-1.0) representing confidence
 - **Reasons**: Optional metadata for edge provenance
 - **Propagation**: Trust may propagate via audit chains or delegation

## Verification Logic
 - **Agent status** must be active and not revoked
 - **Fingerprint and attestation** must match registry records
 - **Delegates** may verify on behalf of parent agent
 - **Trust edges** may be used to infer indirect verification

## Revocation Protocol
Agents may be revoked via:
 - Manual registry update
 - Expired or invalid attestation
 - Compromised fingerprint or key
 - Trust graph collapse (e.g. all edges fall below threshold)
Revoked agents are marked revoked: true and excluded from verification flows.

## Governance Models
 - **Centralized**: Single authority manages registry
 - **Federated**: Multiple registries with cross-verification
 - **Autonomous**: Agents self-register and verify via trust graph consensus
Each model defines its own quorum, update rules, and edge validation logic.

## Threat Vectors
 - **Sybil attacks** - mitigated via trust graph density and audit lineage
 - **Delegation abuse** - mitigated via depth limits and edge decay
 - **Registry poisoning** - mitigated via quorum-based updates and edge validation
 - **Revocation bypass** - mitigated via strict status checks and audit token invalidation

## Examples
See `/examples/registry/agent-v1-record.json` and `/examples/trust-graph/agent-v1-edges.json` for full payloads.
