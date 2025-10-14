# RFC 0003: Environment Attestation

**Status**: Draft  
**Author**: Anna Popivanova   
**Created**: 2025-10-14  
**Tags**: attestation, runtime, environment, verification, trust

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
