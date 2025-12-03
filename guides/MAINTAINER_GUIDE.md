# Maintainer Guide

## ⚠️ Phase 1 Status

**This system is currently UNRELEASED and UNTESTED in production.**
- ✅ Infrastructure Complete: All core components implemented
- ⚠️ Not Yet Activated: Governance rules are not enforced
- 🔧 Test Keys Only: No real cryptographic enforcement

## Key Management

### Generating Real Keys (Phase 2+)

**⚠️ DO NOT GENERATE REAL KEYS UNTIL PHASE 2 ACTIVATION**

```bash
# Generate new keypair using developer-sdk
cargo run --bin generate-keypair -- --output maintainer-keys.json
```

**Key Security**: Store private keys securely, never share. Share public keys with governance system. Create secure backups. Plan for key rotation.

**Key Format**:
```json
{
  "private_key": "hex-encoded-private-key",
  "public_key": "hex-encoded-public-key",
  "key_id": "unique-key-identifier",
  "created_at": "2024-01-01T00:00:00Z"
}
```

## Signature Process

### How to Sign PRs

```bash
# Sign a PR (Phase 2+)
cargo run --bin sign-pr -- --pr 123 --message "I approve this change"
```

**Signature Format**: Post as GitHub comment: `/governance-sign <signature-hex>`

**Code**: ```34:110:blvm-commons/src/webhooks/comment.rs```

### Signature Verification

The system will:
1. Extract signature from comment
2. Verify signature cryptographically
3. Check maintainer is authorized
4. Update PR governance status
5. Log event in audit log

**Code**: ```blvm-commons/src/validation/signatures.rs```

## PR Classification

### Automatic Classification

System classifies PRs based on: file changes, PR title, PR body, repository.

**Code**: ```1:200:blvm-commons/src/validation/tier_classification.rs```

**Verify**: `gh api repos/BTCDecoded/<repo>/pulls/<pr>/statuses | jq '.[] | select(.context | contains("governance-tier"))'`

### Manual Override

```bash
# Override PR classification (Phase 2+)
cargo run --bin override-tier -- --pr 123 --tier 4 --rationale "Emergency security fix"
```

### Tier Requirements

| Tier | Signatures | Review Period | Economic Veto |
|------|------------|---------------|---------------|
| 1 (Routine) | 3-of-5 | 7 days | No |
| 2 (Feature) | 4-of-5 | 30 days | No |
| 3 (Consensus-Adjacent) | 5-of-5 | 90 days | Yes (30%+ hashpower AND 40%+ economic) |
| 4 (Emergency) | 4-of-5 | 0 days | No |
| 5 (Governance) | 5-of-5 | 180 days | Yes (50%+ hashpower AND 60%+ economic) |

**Code**: ```63:125:blvm-commons/src/validation/threshold.rs```

## Emergency Procedures

### Emergency Activation (Tier 4)

1. Automatic classification as Tier 4
2. Immediate notification to all maintainers
3. 4-of-5 signatures required within 24 hours
4. Economic node oversight
5. Post-mortem required within 30 days

### Emergency Extension

```bash
# Extend emergency (Phase 2+)
cargo run --bin extend-emergency -- --pr 123 --days 7 --rationale "Additional time needed"
```

## Economic Node Interaction

### Veto Signals

Economic nodes can submit: **Veto** (block PR), **Support** (support PR), **Abstain** (neutral).

### Veto Thresholds

| Tier | Mining Threshold | Economic Threshold | Logic |
|------|------------------|---------------------|-------|
| 3 | 30%+ | 40%+ | AND (both required) |
| 4 | 25%+ | 35%+ | AND (both required) |
| 5 | 50%+ | 60%+ | AND (both required) |

**Code**: ```113:379:blvm-commons/src/economic_nodes/veto.rs```

### Veto Response

If veto active: PR blocked, status updated, maintainers notified, PR cannot merge until resolved.

## Governance Changes (Tier 5)

Requires: 180-day review period, economic node signaling (50%+ hashpower, 60%+ economic activity), special process, fork capability.

## Monitoring and Alerts

### Status Monitoring

```bash
# Check PR status (Phase 2+)
cargo run --bin check-status -- --pr 123

# Check system status
cargo run --bin system-status
```

### Alerts

System sends alerts for: signature requirements, expiring review periods, veto signals, system issues.

## Best Practices

| For Maintainers | For PR Authors |
|-----------------|---------------|
| Monitor governance status regularly | Use appropriate labels and titles |
| Sign PRs promptly when requirements met | Explain changes and rationale |
| Understand tier requirements | Respect governance process |
| Coordinate with other maintainers | Respond to maintainer questions |
| Provide clear rationale for decisions | Don't bypass governance |

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Signature not recognized | Check key format and permissions |
| PR not classified | Verify file changes and content |
| Status not updating | Check webhook delivery and permissions |
| Veto not clearing | Verify economic node signals |

### Debug Commands

```bash
# Debug PR classification
cargo run --bin debug-classification -- --pr 123

# Debug signature verification
cargo run --bin debug-signature -- --signature <signature>

# Debug veto status
cargo run --bin debug-veto -- --pr 123
```

## Security Considerations

| Aspect | Requirements |
|--------|--------------|
| **Key Security** | Never share private keys, use secure storage, plan rotation, backup safely |
| **Signature Security** | Verify context, check content, understand impact, coordinate with others |
| **System Security** | Trust the system, report issues, stay updated, follow procedures |

## ⚠️ Final Warning

**This system is currently in development. Do not use real keys or deploy in production until Phase 2 activation.**
