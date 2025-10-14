# Contributing to airlock
Thanks for your interest in improving **airlock** - a protocol for cryptographically verifying AI model identity at runtime.

## What We're Building
**airlock** is an open specification for:
- Agent fingerprinting
- Runtime attestation
- Cryptographic handshakes
- Audit token lineage
- Stream and block verification modes

## How to Contribute
### RFCs
- RFCs live in `/rfc/`
- Follow the format of `0001-airlock-handshake.md`
- Propose new RFCs via pull request with a clear motivation section

### Schemas
 - JSON Schemas live in `/schemas/`
 - Validate using [json-schema.org](https://json-schema.org/) or your favorite tool
 - Keep them modular and versioned

### Examples
 - Sample payloads live in `/examples/`
 - Use real-looking hashes and timestamps
 - Avoid any PII/SPII (see Privacy Disclaimer in README)

## Testing
Coming soon: simulation suite for handshake validation and threat modeling.

## License
MIT — see `LICENSE.md`

## Questions?
Open an issue or start a discussion in the repo. We welcome feedback, forks, and federated extensions.
