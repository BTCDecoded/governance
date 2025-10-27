# BTCDecoded Governance Scope

## Overview

BTCDecoded governance operates on two distinct levels:

1. **Repository Governance** (Binding) - What we control
2. **Protocol Governance** (Advisory) - What we influence

This document clarifies the scope and limitations of BTCDecoded's governance system.

## Repository Governance (Binding Authority)

### What We Control

**Code Repository Access:**
- Merge permissions to BTCDecoded repositories
- Code quality standards and review processes
- Release creation and versioning
- Maintainer selection and removal

**Development Process:**
- Pull request review requirements
- Signature thresholds for different change types
- Review periods and waiting times
- Emergency response procedures

**Technical Standards:**
- Code style and formatting requirements
- Testing and documentation standards
- Security audit requirements
- Performance benchmarks

### What We Don't Control

**Bitcoin Network Consensus:**
- Bitcoin's consensus rules (immutable by design)
- Network upgrade activation mechanisms
- User adoption decisions
- Miner signaling and hash power

**User Sovereignty:**
- Which software users choose to run
- Node operator configuration choices
- Economic decisions and market behavior
- Fork creation and maintenance

## Protocol Governance (Advisory Influence)

### What We Influence

**Code Quality for Consensus Changes:**
- Maintainers can approve high-quality consensus change code
- Provide technical specifications and audit requirements
- Ensure mathematical correctness and security

**User Education:**
- Document the implications of proposed changes
- Provide clear upgrade paths and migration guides
- Explain technical trade-offs and considerations

**Community Coordination:**
- Facilitate discussion between stakeholders
- Provide neutral technical analysis
- Coordinate with other Bitcoin implementations

### What We Cannot Do

**Force Network Adoption:**
- No amount of maintainer signatures forces users to upgrade
- Cannot prevent users from running alternative software
- Cannot control economic incentives or market forces

**Override User Choice:**
- Users remain sovereign over their node software
- Economic majority determines network rules
- Users can fork, reject, or modify any changes

## Practical Examples

### Example 1: Consensus Rule Change

**What We Can Do (Repository Governance):**
- Require 6-of-7 maintainer signatures for consensus code changes
- Mandate 365-day review period for consensus changes
- Require BIP specification, test vectors, and security audit
- Approve high-quality code for release

**What We Cannot Do (Protocol Governance):**
- Force users to upgrade to new consensus rules
- Control when or if the change activates on the network
- Prevent users from running software that rejects the change
- Override economic majority decisions

**User Process:**
1. Maintainers approve code (6-of-7 signatures, 365 days)
2. Code released as optional upgrade
3. Users evaluate and choose whether to run it
4. Economic coordination determines activation
5. Users who disagree can fork or reject

### Example 2: Emergency Security Fix

**What We Can Do (Repository Governance):**
- Activate emergency tier for critical vulnerabilities
- Reduce review period to 0 days for network-threatening bugs
- Require 4-of-5 signatures for emergency patches
- Coordinate with security researchers

**What We Cannot Do (Protocol Governance):**
- Force immediate network-wide adoption
- Prevent users from running vulnerable software
- Control how quickly users upgrade
- Override user risk assessments

**User Process:**
1. Maintainers release emergency patch
2. Users evaluate severity and upgrade timeline
3. Economic coordination determines adoption speed
4. Users who disagree can choose different responses

### Example 3: New RPC Method

**What We Can Do (Repository Governance):**
- Require 4-of-5 signatures for new features
- Mandate 30-day review period
- Require technical specification
- Ensure backward compatibility

**What We Cannot Do (Protocol Governance):**
- Force users to use the new RPC method
- Control how users integrate with the new feature
- Prevent users from implementing alternatives
- Override user preference for different APIs

## Economic Node Role

Economic nodes (mining pools, exchanges, custodians) provide:

**Veto Power (Repository Governance):**
- Can veto Tier 3+ changes (consensus-adjacent, emergency, governance)
- 30%+ hashpower or 40%+ economic activity threshold
- Binding authority over repository merges

**Advisory Input (Protocol Governance):**
- Signal preferences for consensus changes
- Provide economic analysis and impact assessment
- Coordinate with user community on adoption

**Important:** Economic node vetoes affect repository access, not user choice. Users remain free to run any software they prefer.

## Governance Fork Capability

If users disagree with maintainer decisions:

**Repository Fork:**
- Users can fork BTCDecoded repositories
- Maintain their own governance rules
- Compete for user adoption

**Protocol Fork:**
- Users can create alternative Bitcoin implementations
- Maintain different consensus rules
- Compete in the market for adoption

**Exit Strategy:**
- Users always retain the option to exit
- No single point of failure or control
- Market forces determine success

## Safeguards and Limitations

### Built-in Safeguards

**Multi-Signature Requirements:**
- No single maintainer can make decisions
- Higher layers require more consensus
- Emergency procedures have time limits

**Transparency:**
- All governance decisions are public
- Cryptographic audit trail of all actions
- Community oversight and accountability

**User Protection:**
- Users control their own software
- Economic coordination prevents capture
- Exit options always available

### System Limitations

**Cannot Override Bitcoin's Design:**
- Bitcoin's consensus rules are immutable by design
- Users are sovereign over their node software
- Economic incentives drive adoption, not authority

**Cannot Force Coordination:**
- Cannot control user upgrade decisions
- Cannot prevent alternative implementations
- Cannot override market forces

**Cannot Guarantee Adoption:**
- Code quality doesn't guarantee user adoption
- Technical merit doesn't ensure economic success
- Maintainer approval doesn't force network changes

## Conclusion

BTCDecoded governance provides:

1. **High-quality code** through rigorous review processes
2. **User education** through clear documentation and analysis
3. **Community coordination** through transparent decision-making
4. **Emergency response** through structured crisis management

But it cannot and does not attempt to:

1. **Control Bitcoin's consensus rules** (users remain sovereign)
2. **Force network adoption** (economic coordination required)
3. **Override user choice** (exit options always available)
4. **Replace market forces** (competition drives innovation)

**The fundamental principle:** We govern the codebase commons (repository access), not the network commons (Bitcoin protocol). Users govern the network through voluntary adoption and economic coordination.

## Related Documentation

- [GOVERNANCE.md](GOVERNANCE.md) - Main governance process
- [LAYER_TIER_MODEL.md](LAYER_TIER_MODEL.md) - How layers and tiers work
- [Configuration Files](config/README.md) - Technical configuration
- [Economic Node Guide](guides/ECONOMIC_NODE_GUIDE.md) - Economic node role