# RFC 0003: Environment Attestation

**Status**: Draft  
**Author**: Anna Popivanova   
**Created**: 2025-10-01  
**Tags**: attestation, runtime, environment, verification, trust, identity

---

## Motivation
Agent behavior is inseparable from the environment in which it runs. Identical models can behave differently depending on runtime conditions, hardware, or injected dependencies. This RFC defines a mechanism for attesting to the runtime environment of an agent — enabling downstream verifiers to assess trustworthiness, reproducibility, and tamper resistance.

---

## Goals
 - Capture a cryptographically verifiable snapshot of an agent’s runtime environment  
 - Enable third-party verification of environment integrity  
 - Support both enclave-based and non-enclave attestations  
 - Prevent environment spoofing, drift, or dependency injection

---

## Attestation Payload Structure
```json
{
  "attestation_id": "airlock:attest:sha256:def456...",
  "agent_id": "airlock:agent:sha256:abc123...",
  "timestamp": "2025-10-14T15:05:00Z",
  "environment": {
    "platform": "linux-x86_64",
    "os_release": "Ubuntu 22.04.3 LTS",
    "kernel_version": "5.15.0-84-generic",
    "hardware": {
      "cpu": "Intel(R) Xeon(R) Gold 6338",
      "gpu": "NVIDIA A100",
      "memory_gb": 128
    },
    "dependencies": [
      "torch==2.1.0",
      "numpy==1.26.0",
      "transformers==4.34.0"
    ],
    "env_vars": {
      "PYTHONHASHSEED": "42",
      "CUDA_VISIBLE_DEVICES": "0"
    }
  },
  "runtime_hash": "sha256:...",
  "enclave_attestation": {
    "provider": "intel-sgx",
    "quote": "base64:...",
    "measurement": "sha256:...",
    "nonce": "random-uuid"
  },
  "signature": "ed25519:..."
}
```
## Verification Logic
 - **runtime_hash** must be reproducible from environment snapshot
 - **enclave_attestation** (if present) must be verifiable via provider’s public key
 - **signature** must match agent’s registered public key
 - **timestamp** must fall within acceptable freshness window

## Enclave Support (Optional)
If the agent runs inside a secure enclave (e.g., Intel SGX, AMD SEV, AWS Nitro), the attestation may include a signed quote and measurement. This provides hardware-backed assurance of runtime integrity.

## Threat Vectors
 - **Environment spoofing** — mitigated via full snapshot hashing and optional enclave quotes
 - **Dependency injection** — mitigated via strict version pinning and hash verification
 - **Replay attacks** — mitigated via nonce and timestamp validation
 - **Signature forgery** — mitigated via registry-based key verification (see RFC 0007)

## Examples
See /examples/attestation/agent-v1-runtime.json for a full payload.
