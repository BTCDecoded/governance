# Economic Node Guide

## ⚠️ Phase 1 Status

**This system is currently UNRELEASED and UNTESTED in production.**
- ✅ Infrastructure Complete: All core components implemented
- ⚠️ Not Yet Activated: Governance rules are not enforced
- 🔧 Test Keys Only: No real cryptographic enforcement

## Overview

Economic nodes (mining pools, exchanges, custodians, major holders, commons contributors) participate in governance by providing veto power over consensus-adjacent changes.

## Node Types and Qualifications

| Type | Qualification Requirements | Weight Formula | Example |
|------|---------------------------|----------------|---------|
| **Mining Pool** | ≥1% network hashpower, 6+ months operational | `hashpower_percentage / 100.0` (capped by phase) | 5% hashpower = 0.05 weight (Early: capped at 0.10) |
| **Exchange** | ≥10,000 BTC holdings, ≥100 BTC daily volume | `0.7 × (holdings/10K) + 0.3 × (volume/100)`, cap 1.0 | 10,000 BTC, 100 BTC = 0.70 + 0.30 = 1.0 |
| **Custodian** | ≥5,000 BTC under custody | `(holdings/10K)`, cap 1.0 | 10,000 BTC = 1.0 |
| **Major Holder** | ≥5,000 BTC held | `(holdings/5K)`, cap 1.0 | 10,000 BTC = 2.0 (capped at 1.0) |
| **Commons Contributor** | On-chain contributions (merge mining, fee forwarding, zaps, BIP70) | `√(total_contribution_btc)` (quadratic weighting) | 1.0 BTC = 1.0 weight |

**Code**: ```343:363:blvm-commons/src/economic_nodes/registry.rs```

## Registration Process

### Step 1: Prepare Qualification Data

**Mining Pool**:
```json
{
  "node_type": "mining_pool",
  "hashpower_proof": {
    "blocks_mined": ["block_hash_1", "block_hash_2"],
    "time_period_days": 30,
    "total_network_blocks": 1000,
    "percentage": 5.0
  },
  "contact_info": { "email": "contact@pool.com", "website": "https://pool.com" }
}
```

**Exchange**:
```json
{
  "node_type": "exchange",
  "holdings_proof": { "addresses": ["bc1..."], "total_btc": 2000.0, "signature_challenge": "sig..." },
  "volume_proof": { "daily_volume_btc": 150.0, "monthly_volume_btc": 4500.0, "transaction_hashes": ["tx1", "tx2"] },
  "contact_info": { "entity_name": "Exchange", "contact_email": "contact@exchange.com", "website": "https://exchange.com" }
}
```

### Step 2: Submit Registration

```bash
# Register economic node (Phase 2+)
cargo run --bin register-node -- \
  --type mining_pool \
  --name "Example Mining Pool" \
  --public-key "hex-encoded-public-key" \
  --qualification-data qualification.json \
  --contact-info contact.json
```

### Step 3: Verification

1. Initial review (governance system reviews qualification data)
2. Verification (third-party verification of claims)
3. Approval (4-of-5 maintainer signatures required)
4. Notification (node receives confirmation)

**Code**: ```46:107:blvm-commons/src/economic_nodes/registry.rs```

## Veto Signal System

### How Veto Signals Work

Economic nodes can submit veto signals for **Tier 3+** PRs: **Veto** (block PR), **Support** (support PR), **Abstain** (neutral).

### Veto Thresholds

| Tier | Mining Threshold | Economic Threshold | Logic |
|------|------------------|---------------------|-------|
| 3 | 30%+ | 40%+ | AND (both required) |
| 4 | 25%+ | 35%+ | AND (both required) |
| 5 | 50%+ | 60%+ | AND (both required) |

**Code**: ```113:379:blvm-commons/src/economic_nodes/veto.rs```

### Submitting Veto Signals

```bash
# Submit veto signal (Phase 2+)
cargo run --bin submit-veto -- \
  --pr 123 \
  --signal veto \
  --rationale "This change threatens network security" \
  --signature "hex-encoded-signature"
```

**Veto Signal Format**: PR ID, signal type (veto/support/abstain), rationale, cryptographic signature, timestamp.

## Governance Fork Participation

When governance changes are proposed (Tier 5), economic nodes can choose: **Adopt** (new ruleset), **Reject** (current ruleset), **Abstain** (neutral).

```bash
# Submit fork decision (Phase 2+)
cargo run --bin submit-fork-decision -- \
  --ruleset-id "governance-v1.1.0" \
  --decision adopt \
  --rationale "New ruleset improves governance" \
  --signature "hex-encoded-signature"
```

**Adoption Tracking**: Node count, hashpower percentage, economic activity percentage, timeline.

## Monitoring and Alerts

### Status Monitoring

```bash
# Check PR status (Phase 2+)
cargo run --bin check-pr-status -- --pr 123

# Check veto status
cargo run --bin check-veto-status -- --pr 123

# Check fork status
cargo run --bin check-fork-status -- --ruleset-id "governance-v1.1.0"
```

### Alerts

System sends alerts for: new Tier 3+ PRs, expiring veto deadlines, proposed governance changes, system updates.

## Best Practices

| For Economic Nodes | For Veto Signals | For Fork Decisions |
|-------------------|------------------|-------------------|
| Monitor governance status regularly | Understand the PR before signaling | Evaluate what the new ruleset changes |
| Submit veto signals within deadlines | Consider impact on operations | Think about impact on operations |
| Provide clear rationale | Explain why vetoing/supporting | Coordinate with other nodes |
| Coordinate with other nodes | Submit signals within deadline | Keep records of decisions |
| Keep records of decisions | Be consistent with principles | Monitor adoption and outcomes |

## Security Considerations

| Aspect | Requirements |
|--------|--------------|
| **Key Security** | Never share private keys, use secure storage, plan rotation, backup safely |
| **Signal Security** | Verify context, check content, understand impact, coordinate with others |
| **System Security** | Trust the system, report issues, stay updated, follow procedures |

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Registration rejected | Check qualification data and requirements |
| Signal not recognized | Check signature format and permissions |
| Veto not counted | Verify signal was submitted correctly |
| Fork decision not recorded | Check ruleset ID and format |

### Debug Commands

```bash
# Debug node registration
cargo run --bin debug-registration -- --node-id 123

# Debug veto signal
cargo run --bin debug-veto -- --signal-id 456

# Debug fork decision
cargo run --bin debug-fork -- --decision-id 789
```

## Economic Impact

| Power | Responsibility |
|-------|---------------|
| **Veto Power**: Mining pools (30%+ hashpower), exchanges (40%+ economic activity) | **Consider Impact**: Think about decision consequences |
| **Governance Influence**: Veto signals, fork decisions, adoption tracking | **Be Transparent**: Explain reasoning |
| **Blocking Authority**: Either threshold can block PRs | **Coordinate**: Work with other nodes |
| | **Stay Informed**: Keep up with governance developments |

## ⚠️ Final Warning

**This system is currently in development. Do not use real keys or deploy in production until Phase 2 activation.**
