# Economic Node Guide

Guide for economic nodes on how to participate in the BTCDecoded governance system.

## ⚠️ IMPORTANT: Phase 1 Status

**This system is currently UNRELEASED and UNTESTED in production.**

- ✅ **Infrastructure Complete**: All core components implemented
- ⚠️ **Not Yet Activated**: Governance rules are not enforced
- 🔧 **Test Keys Only**: No real cryptographic enforcement
- 📋 **Development Phase**: System is in rapid AI-assisted development

## Overview

This guide explains how economic nodes (mining pools, exchanges, custodians, etc.) will participate in the governance system once it's activated in Phase 2. Currently, the system is in development and uses test data only.

## What Are Economic Nodes?

Economic nodes are entities that have significant economic influence in the Bitcoin ecosystem:

- **Mining Pools**: Control hashpower and can influence consensus
- **Exchanges**: Handle large volumes of Bitcoin transactions
- **Custodians**: Hold significant amounts of Bitcoin for clients
- **Payment Processors**: Process large volumes of Bitcoin payments
- **Major Holders**: Hold significant amounts of Bitcoin

## Node Types and Qualifications

### Mining Pool

**Qualification Requirements:**
- **Hashpower**: 1%+ of total network hashpower
- **Proof**: Block hashes and mining statistics
- **Verification**: Cryptographic proof of hashpower

**Weight Calculation:**
- Base weight: 10.0
- Hashpower adjustment: +0.1 per percentage point
- Example: 5% hashpower = 10.0 + (5.0 × 0.1) = 10.5

### Exchange

**Qualification Requirements:**
- **Holdings**: 1,000+ BTC under management
- **Volume**: $10M+ USD daily volume
- **Transactions**: 100,000+ monthly transactions
- **Proof**: Audited financial statements and trading data

**Weight Calculation:**
- Base weight: 5.0
- Holdings adjustment: +0.001 per BTC
- Volume adjustment: +0.000001 per USD
- Example: 2,000 BTC, $20M volume = 5.0 + (2,000 × 0.001) + (20,000,000 × 0.000001) = 7.0

### Custodian

**Qualification Requirements:**
- **Holdings**: 5,000+ BTC under custody
- **Proof**: Audited custody reports and client attestations
- **Verification**: Third-party audit and verification

**Weight Calculation:**
- Base weight: 7.0
- Holdings adjustment: +0.001 per BTC
- Example: 10,000 BTC = 7.0 + (10,000 × 0.001) = 17.0

### Payment Processor

**Qualification Requirements:**
- **Volume**: $50M+ USD monthly volume
- **Proof**: Transaction volume reports and financial statements
- **Verification**: Audited financial data

**Weight Calculation:**
- Base weight: 3.0
- Volume adjustment: +0.000001 per USD
- Example: $100M volume = 3.0 + (100,000,000 × 0.000001) = 3.1

### Major Holder

**Qualification Requirements:**
- **Holdings**: 5,000+ BTC held
- **Proof**: Wallet addresses and transaction history
- **Verification**: Cryptographic proof of ownership

**Weight Calculation:**
- Base weight: 5.0
- Holdings adjustment: +0.001 per BTC
- Example: 10,000 BTC = 5.0 + (10,000 × 0.001) = 15.0

## Registration Process

### Step 1: Prepare Qualification Data

**For Mining Pools:**
```json
{
  "node_type": "mining_pool",
  "hashpower_proof": {
    "blocks_mined": ["block_hash_1", "block_hash_2"],
    "time_period_days": 30,
    "total_network_blocks": 1000,
    "percentage": 5.0
  },
  "contact_info": {
    "email": "contact@mining-pool.com",
    "website": "https://mining-pool.com",
    "social_media": "https://twitter.com/mining_pool"
  }
}
```

**For Exchanges:**
```json
{
  "node_type": "exchange",
  "holdings_proof": {
    "btc_holdings": 2000.0,
    "audit_date": "2024-01-01",
    "auditor": "Big Four Accounting Firm"
  },
  "volume_proof": {
    "daily_volume_usd": 15000000.0,
    "monthly_transactions": 150000,
    "verification_date": "2024-01-01"
  },
  "contact_info": {
    "email": "contact@exchange.com",
    "website": "https://exchange.com",
    "social_media": "https://twitter.com/exchange"
  }
}
```

### Step 2: Submit Registration

**Phase 2+ Registration Process:**

```bash
# Register economic node (Phase 2+)
cargo run --bin register-node -- \
  --type mining_pool \
  --name "Example Mining Pool" \
  --public-key "hex-encoded-public-key" \
  --qualification-data qualification.json \
  --contact-info contact.json
```

### Step 3: Verification Process

1. **Initial Review**: Governance system reviews qualification data
2. **Verification**: Third-party verification of claims
3. **Approval**: Node is approved and activated
4. **Notification**: Node receives confirmation

## Veto Signal System

### How Veto Signals Work

Economic nodes can submit veto signals for Tier 3+ (Consensus-Adjacent) PRs:

- **Veto**: Block the PR from merging
- **Support**: Support the PR
- **Abstain**: Neutral position

### Veto Thresholds

- **Mining Veto**: 30%+ hashpower veto
- **Economic Veto**: 40%+ economic activity veto
- **Combined**: Either threshold can block the PR

### Submitting Veto Signals

**Phase 2+ Veto Process:**

```bash
# Submit veto signal (Phase 2+)
cargo run --bin submit-veto -- \
  --pr 123 \
  --signal veto \
  --rationale "This change threatens network security" \
  --signature "hex-encoded-signature"
```

### Veto Signal Format

Veto signals are submitted with:

- **PR ID**: Which PR the signal applies to
- **Signal Type**: veto, support, or abstain
- **Rationale**: Explanation of the decision
- **Signature**: Cryptographic signature proving authenticity
- **Timestamp**: When the signal was submitted

## Governance Fork Participation

### Fork Decisions

When governance changes are proposed (Tier 5), economic nodes can choose which ruleset to follow:

- **Adopt**: Adopt the new governance ruleset
- **Reject**: Reject the new governance ruleset
- **Abstain**: Neutral position

### Fork Decision Process

**Phase 2+ Fork Process:**

```bash
# Submit fork decision (Phase 2+)
cargo run --bin submit-fork-decision -- \
  --ruleset-id "governance-v1.1.0" \
  --decision adopt \
  --rationale "New ruleset improves governance" \
  --signature "hex-encoded-signature"
```

### Adoption Tracking

The system tracks adoption of different governance rulesets:

- **Node Count**: How many nodes have adopted each ruleset
- **Hashpower**: Percentage of hashpower supporting each ruleset
- **Economic Activity**: Percentage of economic activity supporting each ruleset
- **Timeline**: How adoption changes over time

## Monitoring and Alerts

### Status Monitoring

Economic nodes can monitor governance status:

```bash
# Check PR status (Phase 2+)
cargo run --bin check-pr-status -- --pr 123

# Check veto status
cargo run --bin check-veto-status -- --pr 123

# Check fork status
cargo run --bin check-fork-status -- --ruleset-id "governance-v1.1.0"
```

### Alerts

The system will send alerts for:

- **New PRs**: When Tier 3+ PRs are opened
- **Veto Deadlines**: When veto periods are expiring
- **Fork Decisions**: When governance changes are proposed
- **System Updates**: When the governance system is updated

## Best Practices

### For Economic Nodes

1. **Stay Informed**: Monitor governance status regularly
2. **Respond Promptly**: Submit veto signals within deadlines
3. **Provide Rationale**: Explain your decisions clearly
4. **Coordinate**: Work with other nodes when appropriate
5. **Document**: Keep records of your decisions

### For Veto Signals

1. **Understand the PR**: Read and understand the proposed changes
2. **Consider Impact**: Think about the impact on your operations
3. **Provide Rationale**: Explain why you're vetoing or supporting
4. **Be Timely**: Submit signals within the deadline
5. **Be Consistent**: Align your signals with your principles

### For Fork Decisions

1. **Evaluate Changes**: Understand what the new ruleset changes
2. **Consider Impact**: Think about the impact on your operations
3. **Coordinate**: Work with other nodes when appropriate
4. **Document**: Keep records of your decisions
5. **Stay Informed**: Monitor adoption and outcomes

## Security Considerations

### Key Security

- **Never Share Private Keys**: Keep private keys secure
- **Use Secure Storage**: Store keys in secure locations
- **Regular Rotation**: Plan for key rotation
- **Backup Safely**: Create secure backups

### Signal Security

- **Verify Context**: Ensure you're signaling the right PR
- **Check Content**: Review PR content before signaling
- **Understand Impact**: Know what the PR changes
- **Coordinate**: Work with other nodes when appropriate

### System Security

- **Trust the System**: The governance system is designed to be secure
- **Report Issues**: Report any security concerns
- **Stay Updated**: Keep up with system updates
- **Follow Procedures**: Use established procedures

## Troubleshooting

### Common Issues

1. **Registration Rejected**: Check qualification data and requirements
2. **Signal Not Recognized**: Check signature format and permissions
3. **Veto Not Counted**: Verify signal was submitted correctly
4. **Fork Decision Not Recorded**: Check ruleset ID and format

### Debug Commands

```bash
# Debug node registration
cargo run --bin debug-registration -- --node-id 123

# Debug veto signal
cargo run --bin debug-veto -- --signal-id 456

# Debug fork decision
cargo run --bin debug-fork -- --decision-id 789
```

### Getting Help

1. **Check Documentation**: Review this guide and other docs
2. **Ask Questions**: Use GitHub discussions
3. **Report Issues**: Use GitHub issues for bugs
4. **Community**: Engage with the development community

## Economic Impact

### Veto Power

Economic nodes have significant veto power:

- **Mining Pools**: Can veto with 30%+ hashpower
- **Exchanges**: Can veto with 40%+ economic activity
- **Combined**: Either threshold can block PRs

### Governance Influence

Economic nodes influence governance through:

- **Veto Signals**: Blocking or supporting PRs
- **Fork Decisions**: Choosing governance rulesets
- **Adoption Tracking**: Influencing which ruleset becomes dominant
- **Community**: Shaping the governance process

### Responsibility

With power comes responsibility:

- **Consider Impact**: Think about the impact of your decisions
- **Be Transparent**: Explain your reasoning
- **Coordinate**: Work with other nodes when appropriate
- **Stay Informed**: Keep up with governance developments

## Future Developments

### Phase 2 Features

- **Real Enforcement**: Actual governance enforcement
- **Production Keys**: Real cryptographic keys
- **Security Audit**: Completed security audit
- **Community Validation**: Community-tested system

### Phase 3 Features

- **Mature System**: Battle-tested in production
- **Advanced Features**: Additional governance capabilities
- **Integration**: Better integration with Bitcoin ecosystem
- **Community**: Full community adoption

## Contact and Support

### Development Team

- **GitHub Issues**: Report bugs and feature requests
- **GitHub Discussions**: Ask questions and provide feedback
- **Pull Requests**: Contribute code and improvements

### Security

- **Security Issues**: Report privately to maintainers
- **Vulnerabilities**: Follow responsible disclosure
- **Audit Results**: Will be published when available

## ⚠️ Final Warning

**This system is currently in development. Do not use real keys or deploy in production until Phase 2 activation.**

---

**Remember**: This system is designed to make Bitcoin governance more transparent, accountable, and resistant to capture. But it's still in development. Stay informed, provide feedback, and wait for the official release.
