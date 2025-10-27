# Economic Nodes Architecture

## Overview

Economic nodes represent the economic interests of Bitcoin users and provide a veto mechanism for consensus-adjacent changes. This system ensures that governance decisions align with the economic incentives of Bitcoin's stakeholders.

## Purpose

Economic nodes serve as a **user protection mechanism** by:
- Representing mining pools, exchanges, and custodians
- Providing veto power over consensus-adjacent changes
- Ensuring governance decisions consider economic impact
- Maintaining alignment with Bitcoin's economic incentives

## Node Types

### Mining Pools

**Qualification Criteria:**
- Minimum 1% of network hash rate
- Publicly verifiable hash rate
- Established operational history (6+ months)
- Transparent fee structure

**Responsibilities:**
- Monitor consensus-adjacent changes
- Vote on economic impact
- Maintain operational transparency
- Report hash rate changes

### Exchanges

**Qualification Criteria:**
- Minimum $100M daily trading volume
- Established operational history (12+ months)
- Regulatory compliance in jurisdiction
- Transparent trading practices

**Responsibilities:**
- Assess market impact of changes
- Vote on user experience impact
- Maintain trading transparency
- Report volume changes

### Custodians

**Qualification Criteria:**
- Minimum $1B assets under custody
- Established operational history (24+ months)
- Regulatory compliance in jurisdiction
- Insurance and security audits

**Responsibilities:**
- Assess custody impact of changes
- Vote on security implications
- Maintain custody transparency
- Report asset changes

## Registration Process

### Application

1. **Submit Application**: Complete registration form with:
   - Organization details
   - Qualification evidence
   - Contact information
   - Public keys for signing

2. **Verification**: Maintainers verify:
   - Qualification criteria
   - Operational history
   - Regulatory compliance
   - Technical capabilities

3. **Approval**: Requires 4-of-5 maintainer signatures
4. **Onboarding**: Technical setup and key distribution

### Ongoing Requirements

- **Quarterly Reports**: Operational status and metrics
- **Annual Renewal**: Re-verification of qualifications
- **Incident Reporting**: Security or operational issues
- **Transparency**: Public disclosure of relevant metrics

## Veto Mechanism

### Veto Power

Economic nodes can veto **Tier 3 (Consensus-Adjacent)** changes by:
- Submitting veto signals within 30 days
- Requiring 60% of registered nodes to veto
- Providing justification for veto decision
- Maintaining public veto registry

### Veto Process

1. **Change Notification**: 30-day notice of consensus-adjacent change
2. **Analysis Period**: 15 days for economic impact assessment
3. **Veto Window**: 15 days for veto signal submission
4. **Threshold Check**: Count veto signals against threshold
5. **Decision**: Block change if veto threshold met

### Veto Signals

```json
{
  "type": "veto_signal",
  "node_id": "mining_pool_1",
  "node_type": "mining_pool",
  "change_id": "pr_123_consensus_adjacent",
  "veto_reason": "Economic impact on mining profitability",
  "justification": "Detailed analysis of impact...",
  "signature": "ed25519_signature_hex",
  "timestamp": "2024-01-15T10:30:00Z"
}
```

## Node Registry

### Registry Structure

```json
{
  "version": "2024-01",
  "timestamp": "2024-01-15T10:30:00Z",
  "nodes": [
    {
      "id": "mining_pool_1",
      "type": "mining_pool",
      "name": "Example Mining Pool",
      "jurisdiction": "United States",
      "qualification_metrics": {
        "hash_rate_percentage": 2.5,
        "operational_months": 18,
        "transparency_score": 0.95
      },
      "public_key": "ed25519_public_key_hex",
      "contact": "contact@example.com",
      "status": "active",
      "registered_at": "2023-07-15T10:30:00Z",
      "last_verified": "2024-01-15T10:30:00Z"
    }
  ],
  "thresholds": {
    "veto_threshold": 0.6,
    "minimum_nodes": 10,
    "quorum_required": true
  }
}
```

### Registry Updates

- **Monthly Updates**: New registrations and status changes
- **Quarterly Reviews**: Qualification re-verification
- **Annual Renewals**: Complete re-registration process
- **Emergency Updates**: Immediate status changes

## Veto Thresholds

### Current Thresholds

- **Minimum Nodes**: 10 active economic nodes
- **Veto Threshold**: 60% of active nodes must veto
- **Quorum Required**: 80% of nodes must participate
- **Time Window**: 30 days for veto signal submission

### Threshold Adjustment

Thresholds can be adjusted through:
- **Governance Process**: Tier 5 change (6-of-7 maintainers)
- **Economic Analysis**: Impact assessment required
- **Community Input**: 90-day public comment period
- **Gradual Changes**: Phased implementation over 6 months

## Monitoring and Compliance

### Node Monitoring

- **Hash Rate Tracking**: For mining pools
- **Trading Volume**: For exchanges
- **Custody Assets**: For custodians
- **Operational Status**: Uptime and availability
- **Transparency Metrics**: Public disclosure compliance

### Compliance Enforcement

- **Warning System**: Automated alerts for non-compliance
- **Grace Periods**: 30 days to address issues
- **Suspension**: Temporary removal for non-compliance
- **Revocation**: Permanent removal for serious violations

## Integration with Governance

### Pull Request Processing

1. **Tier Classification**: Identify consensus-adjacent changes
2. **Node Notification**: Alert all economic nodes
3. **Analysis Period**: 15 days for impact assessment
4. **Veto Window**: 15 days for veto signal submission
5. **Decision**: Block or allow based on veto threshold

### Status Reporting

Economic node status is reported in:
- **GitHub Status Checks**: Veto status on PRs
- **Nostr Events**: Real-time status updates
- **Monthly Registries**: Comprehensive status reports
- **Audit Logs**: Complete veto history

## Security Considerations

### Node Security

- **Key Management**: Hardware security modules for signing keys
- **Access Control**: Multi-factor authentication for systems
- **Incident Response**: Rapid response to security issues
- **Audit Requirements**: Regular security audits

### Veto Security

- **Signature Verification**: All veto signals cryptographically verified
- **Replay Protection**: Nonces prevent replay attacks
- **Timestamp Validation**: Prevent old veto signals
- **Threshold Verification**: Multiple independent verifications

## Economic Incentives

### Alignment Mechanisms

- **Stake Requirements**: Significant economic stake required
- **Transparency Incentives**: Better transparency = more influence
- **Long-term Thinking**: Annual renewal encourages stability
- **Reputation System**: Good behavior increases influence

### Disincentives

- **Veto Abuse**: Excessive vetoes reduce influence
- **Non-compliance**: Violations result in suspension
- **Poor Performance**: Inactive nodes lose status
- **Reputation Damage**: Public disclosure of violations

## Future Enhancements

### Advanced Features

- **Delegated Voting**: Allow users to delegate veto power
- **Weighted Voting**: Influence based on economic stake
- **Cross-Protocol**: Extend to other Bitcoin protocols
- **Automated Analysis**: AI-assisted impact assessment

### Integration Improvements

- **Real-time Updates**: Instant veto signal processing
- **Mobile Apps**: Mobile interfaces for node management
- **API Access**: Programmatic access to veto data
- **Analytics Dashboard**: Comprehensive veto analytics

## References

- [Economic Node Guide](../guides/ECONOMIC_NODE_GUIDE.md)
- [Economic Node Configuration](../config/economic-nodes.yml)
- [Veto Examples](../examples/economic-node-veto.md)
- [Maintainer Guide](../guides/MAINTAINER_GUIDE.md)
