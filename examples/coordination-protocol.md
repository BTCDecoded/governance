# Emergency Coordination Protocol

**Purpose**: Guide for coordinating with external parties during emergencies  
**Use**: When emergency requires external coordination  
**Last Updated**: 2025-01-XX

---

## Overview

During critical emergencies (especially consensus bugs), coordination with external parties may be necessary. This protocol provides guidance for such coordination.

**Key Principle**: Coordinate, don't command. We cannot force others to act, but we can provide information and coordinate responses.

---

## Coordination Targets

### 1. Bitcoin Core Maintainers

**When to Coordinate**:
- Consensus bug that affects Bitcoin network
- Bug that could cause network fork
- Bug that affects multiple implementations

**How to Coordinate**:
- **Informal**: Direct contact with Core maintainers (if relationships exist)
- **Formal**: Public disclosure via Bitcoin-dev mailing list
- **Emergency**: Direct contact for critical issues

**What to Share**:
- Vulnerability description
- Impact assessment
- Proposed fix
- Timeline for disclosure

**What NOT to Share**:
- Exploit details (until fix is deployed)
- User data
- Private information

---

### 2. Other Bitcoin Implementations

**When to Coordinate**:
- Bug affects multiple implementations
- Bug is in shared dependency
- Bug requires coordinated disclosure

**Implementations to Consider**:
- Bitcoin Core
- btcd
- Bitcoin Knots
- Other full node implementations

**How to Coordinate**:
- Direct contact (if relationships exist)
- Public disclosure via Bitcoin-dev mailing list
- GitHub security advisories

---

### 3. Miners and Mining Pools

**When to Coordinate**:
- Bug affects mining
- Bug requires miner action
- Bug affects block validation

**How to Coordinate**:
- Direct contact with major pools (if relationships exist)
- Public disclosure
- Mining pool communication channels

**What to Share**:
- Vulnerability description
- Impact on mining
- Required actions
- Timeline

---

### 4. Exchanges and Services

**When to Coordinate**:
- Bug affects transaction validation
- Bug affects wallet functionality
- Bug requires service action

**How to Coordinate**:
- Direct contact (if relationships exist)
- Public disclosure
- Industry communication channels

**What to Share**:
- Vulnerability description
- Impact on services
- Required actions
- Timeline

---

## Coordination Timeline

### Pre-Disclosure (Private)

**T-48 to T-24 hours**:
- Contact Bitcoin Core maintainers (if critical)
- Share vulnerability details privately
- Coordinate disclosure timing

**T-24 to T-0 hours**:
- Finalize disclosure documents
- Confirm coordination timing
- Prepare public disclosure

### Disclosure (Public)

**T+0 hours**:
- Publish disclosure
- Notify all parties
- Monitor response

**T+0 to T+24 hours**:
- Answer questions
- Provide additional information
- Monitor network status

---

## Communication Templates

### Template 1: Private Disclosure to Core

**Subject**: [URGENT] Consensus Bug Disclosure - BLLVM

**Body**:
```
Dear Bitcoin Core Maintainers,

We have discovered a consensus bug in BLLVM that [description].

Impact: [impact assessment]

Proposed Fix: [fix description]

Timeline: We plan to disclose publicly on [date/time] after deploying fix.

We wanted to inform you in advance to coordinate disclosure if needed.

Best regards,
[Name]
BTCDecoded Emergency Response Team
```

---

### Template 2: Public Disclosure

**Subject**: Security Advisory: Consensus Bug in BLLVM [CVE-XXXX-XXXX]

**Body**:
```
# Security Advisory: Consensus Bug in BLLVM

## Summary

[Brief description]

## Impact

[Impact assessment]

## Affected Versions

[Version information]

## Fix

[Fix description]

## Timeline

- Discovery: [date]
- Fix: [date]
- Disclosure: [date]

## Recommendations

[Recommendations for users]

## References

[Links to fix, tests, etc.]
```

---

## Coordination Principles

### 1. Transparency

- Be transparent about the bug
- Be transparent about the fix
- Be transparent about the timeline

### 2. Responsibility

- Take responsibility for the bug
- Take responsibility for the fix
- Take responsibility for disclosure

### 3. Coordination

- Coordinate with affected parties
- Coordinate disclosure timing
- Coordinate response actions

### 4. No Command

- We cannot force others to act
- We can only provide information
- Users remain sovereign

---

## Escalation Procedures

### Level 1: Standard Coordination

**When**: Non-critical bug, standard disclosure  
**Actions**: Follow standard coordination protocol  
**Timeline**: Standard disclosure timeline

### Level 2: Enhanced Coordination

**When**: Critical bug, requires coordination  
**Actions**: Enhanced coordination with Core and others  
**Timeline**: Accelerated disclosure timeline

### Level 3: Emergency Coordination

**When**: Network-threatening bug  
**Actions**: Immediate coordination, accelerated timeline  
**Timeline**: Emergency disclosure (hours, not days)

---

## Post-Coordination

### Documentation

- [ ] Document all coordination activities
- [ ] Document responses received
- [ ] Document lessons learned
- [ ] Update coordination protocol if needed

### Follow-Up

- [ ] Follow up with coordinated parties
- [ ] Verify fix deployment
- [ ] Monitor network status
- [ ] Document outcomes

---

## Contact Information

### Bitcoin Core

- **Mailing List**: bitcoin-dev@lists.linuxfoundation.org
- **GitHub**: https://github.com/bitcoin/bitcoin
- **Security**: security@bitcoin.org (for critical issues)

### Other Implementations

- **btcd**: https://github.com/btcsuite/btcd
- **Bitcoin Knots**: https://github.com/bitcoin/bitcoin (Knots branch)

### Industry Channels

- **Bitcoin-dev Mailing List**: bitcoin-dev@lists.linuxfoundation.org
- **Bitcoin Core Dev IRC**: #bitcoin-core-dev on Libera Chat

---

## Notes

- **Informal Relationships**: If relationships exist, use them. If not, use public channels.
- **No Forced Coordination**: We cannot force others to coordinate, only invite.
- **User Sovereignty**: Users remain sovereign over their actions.

---

**Last Updated**: 2025-01-XX  
**Status**: Active

