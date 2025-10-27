# Cryptographic Governance Architecture

## Overview

The BTCDecoded governance system applies the same cryptographic enforcement to governance that Bitcoin applies to consensus. This document details the cryptographic primitives, signature schemes, and verification mechanisms that ensure governance integrity.

## Core Principles

1. **Cryptographic Enforcement**: All governance actions require cryptographic proof
2. **Multisig Security**: Multiple maintainers must sign critical actions
3. **Transparency**: All signatures and actions are publicly verifiable
4. **Tamper Evidence**: Any attempt to modify governance state is detectable
5. **Key Rotation**: Regular key rotation prevents long-term compromise

## Signature Schemes

### Maintainer Signatures

Each maintainer has a unique cryptographic keypair used for:
- Approving pull requests
- Adding/removing other maintainers
- Emergency actions
- Governance rule changes

**Key Requirements:**
- Ed25519 signature scheme (same as Bitcoin's Taproot)
- 256-bit private keys
- Deterministic key derivation from seed phrases
- Hardware security module (HSM) support for production

### Multisig Thresholds

Different governance actions require different signature thresholds:

| Action Type | Required Signatures | Total Maintainers | Time Lock |
|-------------|-------------------|------------------|-----------|
| Routine Maintenance | 3-of-5 | 5 | 7 days |
| Feature Changes | 4-of-5 | 5 | 30 days |
| Consensus-Adjacent | 5-of-5 | 5 | 90 days |
| Emergency Actions | 4-of-5 | 5 | 0 days |
| Governance Changes | 6-of-7 | 7 | 180 days |

### Signature Verification

All signatures are verified using the following process:

1. **Key Validation**: Verify the public key is in the authorized maintainer set
2. **Message Validation**: Verify the message hash matches the expected content
3. **Signature Validation**: Verify the cryptographic signature using Ed25519
4. **Timestamp Validation**: Verify the signature timestamp is within valid range
5. **Nonce Validation**: Verify the signature nonce prevents replay attacks

## Key Management

### Key Generation

Maintainer keys are generated using:
- Cryptographically secure random number generation
- BIP39 mnemonic seed phrases (24 words)
- BIP32 hierarchical deterministic key derivation
- BIP44 coin type for governance keys

### Key Storage

**Development/Testing:**
- Keys stored in encrypted configuration files
- Password-protected with strong passphrases
- Separate key files for each maintainer

**Production:**
- Hardware security modules (HSMs) for key storage
- Air-gapped key generation and signing
- Multi-party computation for key ceremonies
- Regular key rotation schedules

### Key Rotation

Keys are rotated:
- Every 6 months for routine maintainers
- Every 3 months for emergency keyholders
- Immediately upon suspected compromise
- Before major governance changes

## Cryptographic Audit Trail

### Hash Chain

All governance actions are recorded in a tamper-evident hash chain:

```
Action 1: hash1 = SHA256(action1_data + previous_hash)
Action 2: hash2 = SHA256(action2_data + hash1)
Action 3: hash3 = SHA256(action3_data + hash2)
...
```

### Merkle Trees

Monthly governance registries use Merkle trees for efficient verification:

- Root hash anchored to Bitcoin blockchain via OpenTimestamps
- Individual action proofs can be verified without full registry
- Tamper detection through hash mismatch
- Efficient synchronization of governance state

### Timestamping

All governance actions are timestamped using:
- OpenTimestamps for Bitcoin blockchain anchoring
- Multiple timestamping services for redundancy
- Regular anchoring (monthly) of governance state
- Public verification of timestamp proofs

## Signature Formats

### Pull Request Approval

```json
{
  "type": "pr_approval",
  "pr_number": 123,
  "maintainer_id": "maintainer_1",
  "signature": "ed25519_signature_hex",
  "timestamp": "2024-01-15T10:30:00Z",
  "message_hash": "sha256_hash_of_pr_content"
}
```

### Maintainer Addition

```json
{
  "type": "maintainer_add",
  "new_maintainer": {
    "id": "maintainer_6",
    "public_key": "ed25519_public_key_hex",
    "jurisdiction": "United States",
    "contact": "maintainer6@example.com"
  },
  "approving_maintainers": ["maintainer_1", "maintainer_2", "maintainer_3"],
  "signatures": {
    "maintainer_1": "ed25519_signature_hex",
    "maintainer_2": "ed25519_signature_hex",
    "maintainer_3": "ed25519_signature_hex"
  },
  "timestamp": "2024-01-15T10:30:00Z"
}
```

### Emergency Action

```json
{
  "type": "emergency_action",
  "action": "block_merge",
  "pr_number": 456,
  "reason": "Critical security vulnerability",
  "emergency_keyholders": ["emergency_1", "emergency_2", "emergency_3", "emergency_4"],
  "signatures": {
    "emergency_1": "ed25519_signature_hex",
    "emergency_2": "ed25519_signature_hex",
    "emergency_3": "ed25519_signature_hex",
    "emergency_4": "ed25519_signature_hex"
  },
  "timestamp": "2024-01-15T10:30:00Z"
}
```

## Verification Process

### Public Verification

Anyone can verify governance actions by:

1. **Downloading the governance registry**
2. **Verifying maintainer public keys** against the authorized set
3. **Checking signature validity** using Ed25519 verification
4. **Validating the hash chain** for tamper evidence
5. **Verifying timestamps** against blockchain proofs

### Automated Verification

The governance-app automatically verifies:
- All incoming signatures on pull requests
- Maintainer key validity
- Signature threshold compliance
- Time lock requirements
- Hash chain integrity

## Security Considerations

### Attack Vectors

1. **Key Compromise**: Mitigated by multisig and key rotation
2. **Replay Attacks**: Prevented by nonces and timestamps
3. **Man-in-the-Middle**: Prevented by signature verification
4. **Insider Threats**: Mitigated by transparency and multiple maintainers
5. **Quantum Attacks**: Future migration to post-quantum cryptography planned

### Defense Mechanisms

1. **Multisig Requirements**: No single maintainer can act alone
2. **Time Locks**: Prevent rushed decisions
3. **Transparency**: All actions are publicly auditable
4. **Economic Node Veto**: Additional layer of protection
5. **Governance Fork**: Users can choose different rulesets

## Implementation Details

### Developer SDK

The cryptographic primitives are implemented in the developer-sdk:

- `KeyManager`: Key generation, storage, and rotation
- `SignatureManager`: Signing and verification
- `HashChain`: Tamper-evident logging
- `MerkleTree`: Efficient verification structures
- `Timestamping`: Blockchain anchoring

### Governance App Integration

The governance-app uses these primitives for:
- PR signature verification
- Maintainer management
- Emergency response
- Audit log maintenance
- Registry generation

## Future Enhancements

### Post-Quantum Cryptography

Migration to post-quantum signature schemes:
- Dilithium for signatures
- Kyber for key encapsulation
- Gradual migration strategy
- Backward compatibility during transition

### Advanced Features

- Zero-knowledge proofs for privacy-preserving governance
- Threshold signatures for improved efficiency
- Cross-chain governance for multi-protocol coordination
- Formal verification of governance rules

## References

- [Bitcoin Core Development Process](https://github.com/bitcoin/bitcoin/blob/master/CONTRIBUTING.md)
- [Ed25519 Signature Scheme](https://ed25519.cr.yp.to/)
- [BIP39 Mnemonic Seeds](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki)
- [OpenTimestamps Protocol](https://opentimestamps.org/)
- [Developer SDK Documentation](../developer-sdk/README.md)
