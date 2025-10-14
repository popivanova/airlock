# RFC 0006: Verification Modes (Block vs Stream) for Runtime Identity Assurance

**Status**: Draft  
**Author**: Anna Popivanova   
**Created**: 2025-10-01  
**Tags**: attestation, runtime, environment, verification, trust, handshake, runtime, identity

---

## Motivation
Not all interactions with AI agents are equal. Some are short-lived and transactional; others are persistent, sensitive, or high-risk. A single handshake may suffice for the former - but not for the latter.
This RFC introduces two verification modes for airlock: **Block Verification (BV)** and **Stream Verification (SV)**. These modes define how and when identity checks are performed, allowing implementers to balance security, performance, and trust requirements.

---

## Goals
 - Define operational modes for agent verification
 - Support both one-time and continuous trust models
 - Enable detection of runtime drift or mid-session tampering
 - Provide flexibility for different deployment contexts

---

## Verification Modes
### Block Verification (BV)
 - **When**: At session start
 - **How**: One-time handshake using nonce + fingerprint + environment hash
 - **Use Case**: Stateless APIs, short-lived tasks, low-risk interactions
 - **Limitations**: Cannot detect drift or tampering after handshake

### Stream Verification (SV)
 - **When**: Continuously or periodically during session
 - **How**: Verifier issues timed or event-triggered challenges; agent re-attests identity and environment
 - **Use Case**: Long-running agents, sensitive workflows, multi-agent coordination
 - **Benefits**: Detects mid-session drift, unauthorized updates, or runtime manipulation

---

## Mode Negotiation
During handshake, verifier may specify preferred mode:

```json
{
  "verification_mode": "stream",
  "interval": "30s"
}
```

Agents may accept, reject, or propose alternatives. Fallback to BV is allowed if SV is unsupported.

## Failure Handling
**BV Failure**: Session is rejected
**SV Failure**: Session is interrupted or downgraded; verifier may log, alert, or revoke trust

## Implementation Notes
 - SV requires lightweight re-attestation mechanisms
 - Interval-based SV should avoid excessive overhead
 - Event-triggered SV (e.g., on model update) may be more efficient
 - Audit tokens may be chained across SV cycles

## Registry Extension
Agents may declare supported modes in registry metadata:

```json
{
  "agent_id": "airlock://openai/gpt-4.5",
  "verification_modes": ["block", "stream"],
  "stream_interval": "60s"
}
```

## Future Work
 - Adaptive verification based on risk scoring
 - Mode negotiation via trust graph consensus
 - SV compression and batching strategies
 - Integration with audit token lineage (RFC 0004)
