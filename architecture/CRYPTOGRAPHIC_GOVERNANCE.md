# Cryptographic Governance Architecture

## Overview

The Bitcoin Commons governance applies the same cryptographic enforcement to governance that Bitcoin applies to consensus. All governance actions require cryptographic proof, multiple maintainers must sign critical actions, and all signatures are publicly verifiable.

## Core Principles

1. **Cryptographic Enforcement**: All governance actions require cryptographic proof
2. **Multisig Security**: Multiple maintainers must sign critical actions
3. **Transparency**: All signatures and actions are publicly verifiable
4. **Tamper Evidence**: Any attempt to modify governance state is detectable
5. **Key Rotation**: Regular key rotation prevents long-term compromise

## Signature Schemes

### Maintainer Signatures

Each maintainer has unique cryptographic keypair for: approving pull requests, adding/removing maintainers, emergency actions, governance rule changes.

**Key Requirements**: secp256k1 signature scheme (same curve as Bitcoin), 256-bit private keys, deterministic key derivation from seed phrases, HSM support for production.

### Multisig Thresholds

| Action Type | Required Signatures | Total Maintainers | Time Lock |
|-------------|-------------------|------------------|-----------|
| Routine Maintenance | 3-of-5 | 5 | 7 days |
| Feature Changes | 4-of-5 | 5 | 30 days |
| Consensus-Adjacent | 5-of-5 | 5 | 90 days |
| Emergency Actions | 4-of-5 | 5 | 0 days |
| Governance Changes | 6-of-7 | 7 | 180 days |

### Signature Verification

1. Key validation (verify public key in authorized maintainer set)
2. Message validation (verify message hash matches expected content)
3. Signature validation (verify cryptographic signature using secp256k1)
4. Timestamp validation (verify signature timestamp within valid range)
5. Nonce validation (verify signature nonce prevents replay attacks)

**Code**: ```blvm-commons/src/validation/signatures.rs```

## Key Management

### Key Generation

Maintainer keys generated using: cryptographically secure random number generation, BIP39 mnemonic seed phrases (24 words), BIP32 hierarchical deterministic key derivation, BIP44 coin type for governance keys.

### Key Storage

| Environment | Storage Method |
|-------------|----------------|
| **Development/Testing** | Encrypted configuration files, password-protected, separate key files per maintainer |
| **Production** | Hardware security modules (HSMs), air-gapped key generation, multi-party computation, regular rotation |

### Key Rotation

Keys rotated: every 6 months (routine maintainers), every 3 months (emergency keyholders), immediately upon suspected compromise, before major governance changes.

## Cryptographic Audit Trail

### Hash Chain

All governance actions recorded in tamper-evident hash chain:
```
Action 1: hash1 = SHA256(action1_data + previous_hash)
Action 2: hash2 = SHA256(action2_data + hash1)
Action 3: hash3 = SHA256(action3_data + hash2)
```

### Merkle Trees

Monthly governance registries use Merkle trees: root hash anchored to Bitcoin blockchain via OpenTimestamps, individual action proofs verifiable without full registry, tamper detection through hash mismatch, efficient synchronization.

### Timestamping

All governance actions timestamped using: OpenTimestamps for Bitcoin blockchain anchoring, multiple timestamping services for redundancy, regular anchoring (monthly) of governance state, public verification of timestamp proofs.

## Signature Formats

### Pull Request Approval

```json
{
  "type": "pr_approval",
  "pr_number": 123,
  "maintainer_id": "maintainer_1",
  "signature": "secp256k1_signature_hex",
  "timestamp": "2024-01-15T10:30:00Z",
  "message_hash": "sha256_hash_of_pr_content"
}
```

### Maintainer Addition

```json
{
  "type": "maintainer_add",
  "new_maintainer": { "id": "maintainer_6", "public_key": "secp256k1_public_key_hex", "jurisdiction": "United States" },
  "approving_maintainers": ["maintainer_1", "maintainer_2", "maintainer_3"],
  "signatures": { "maintainer_1": "ed25519_signature_hex", ... },
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
  "signatures": { "emergency_1": "ed25519_signature_hex", ... },
  "timestamp": "2024-01-15T10:30:00Z"
}
```

## Verification Process

### Public Verification

Anyone can verify by: downloading governance registry, verifying maintainer public keys, checking signature validity (secp256k1), validating hash chain, verifying timestamps against blockchain proofs.

### Automated Verification

Governance-app automatically verifies: incoming signatures on pull requests, maintainer key validity, signature threshold compliance, time lock requirements, hash chain integrity.

**Code**: ```blvm-commons/src/validation/signatures.rs```

## Security Considerations

| Attack Vector | Mitigation |
|---------------|------------|
| **Key Compromise** | Multisig and key rotation |
| **Replay Attacks** | Nonces and timestamps |
| **Man-in-the-Middle** | Signature verification |
| **Insider Threats** | Transparency and multiple maintainers |
| **Quantum Attacks** | Future migration to post-quantum cryptography |

### Defense Mechanisms

1. Multisig requirements (no single maintainer can act alone)
2. Time locks (prevent rushed decisions)
3. Transparency (all actions publicly auditable)
4. Economic node veto (additional layer of protection)
5. Governance fork (users can choose different rulesets)

## Implementation Details

### Developer SDK

- `KeyManager`: Key generation, storage, rotation
- `SignatureManager`: Signing and verification
- `HashChain`: Tamper-evident logging
- `MerkleTree`: Efficient verification structures
- `Timestamping`: Blockchain anchoring

### Governance App Integration

Governance-app uses these primitives for: PR signature verification, maintainer management, emergency response, audit log maintenance, registry generation.

**Code**: ```blvm-commons/src/crypto/```
