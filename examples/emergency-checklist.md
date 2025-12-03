# Emergency Response Checklist

**Purpose**: Quick reference for emergency response  
**Use**: Follow step-by-step during emergency  
**Last Updated**: 2025-01-XX

---

## Tier 1: Critical Emergency

**Activation**: 5-of-7 emergency keyholders  
**Review Period**: 0 days  
**Signatures**: 4-of-7 maintainers  
**Max Duration**: 7 days

---

## Discovery Phase

- [ ] **Confirm Vulnerability**
  - [ ] Reproduce bug
  - [ ] Assess impact (inflation? fork? DoS?)
  - [ ] Document evidence
  - [ ] Create proof of concept (if safe)

- [ ] **Classify Severity**
  - [ ] Network-threatening? → Tier 1
  - [ ] Serious security? → Tier 2
  - [ ] Important priority? → Tier 3

**Time Estimate**: 1-2 hours

---

## Private Disclosure Phase

- [ ] **Contact Emergency Keyholders**
  - [ ] Use GPG-encrypted email or Signal
  - [ ] Include vulnerability description
  - [ ] Include proof of concept (if safe)
  - [ ] Include impact analysis
  - [ ] Include proposed fix

- [ ] **Wait for Acknowledgment**
  - [ ] Confirm receipt
  - [ ] Coordinate response

**Time Estimate**: 2-4 hours

---

## Emergency Activation Phase

- [ ] **Review Vulnerability**
  - [ ] Emergency keyholders review
  - [ ] Confirm severity classification
  - [ ] Assess impact

- [ ] **Activate Emergency Tier**
  - [ ] Collect 5-of-7 emergency keyholder signatures
  - [ ] Activate Tier 1/2/3
  - [ ] Adjust governance parameters
  - [ ] Log activation in governance repository

**Time Estimate**: 2-4 hours

---

## Fix Development Phase

- [ ] **Identify Root Cause**
  - [ ] Locate bug in codebase
  - [ ] Understand why it exists
  - [ ] Document root cause

- [ ] **Develop Fix**
  - [ ] Implement fix
  - [ ] Add regression test
  - [ ] Code review (4-of-7 maintainers)

**Time Estimate**: 4-8 hours

---

## Testing Phase

- [ ] **Verify Fix**
  - [ ] Run all existing tests
  - [ ] Run new regression test
  - [ ] Verify with differential testing (if available)
  - [ ] Test with historical blocks
  - [ ] Check for regressions

**Time Estimate**: 2-4 hours

---

## Release Phase

- [ ] **Create Release**
  - [ ] Tag release
  - [ ] Create release notes
  - [ ] Document fix

- [ ] **Notify Stakeholders**
  - [ ] Node operators
  - [ ] Miners (if applicable)
  - [ ] Exchanges (if applicable)
  - [ ] Community

- [ ] **Deploy Fix**
  - [ ] Deploy to production
  - [ ] Monitor network
  - [ ] Verify fix is working

**Time Estimate**: 12-24 hours

---

## Public Disclosure Phase

- [ ] **Prepare Disclosure**
  - [ ] Write disclosure document
  - [ ] Include vulnerability details
  - [ ] Include fix details
  - [ ] Include impact assessment

- [ ] **Coordinate Disclosure**
  - [ ] Coordinate with Bitcoin Core (informal)
  - [ ] Coordinate with other implementations
  - [ ] Schedule disclosure time

- [ ] **Publish Disclosure**
  - [ ] Publish to GitHub
  - [ ] Publish to mailing list
  - [ ] Publish to social media
  - [ ] Monitor response

**Time Estimate**: 24-48 hours

---

## Post-Emergency Phase

- [ ] **Post-Mortem** (within 90 days)
  - [ ] Document timeline
  - [ ] Document bottlenecks
  - [ ] Document lessons learned
  - [ ] Document process improvements
  - [ ] Update emergency procedures

- [ ] **Deactivate Emergency Mode**
  - [ ] Verify fix is deployed
  - [ ] Verify network is stable
  - [ ] Deactivate emergency tier
  - [ ] Restore normal governance

---

## Contact Information

### Emergency Keyholders

**Location**: `governance/config/maintainers/emergency.yml`

**Contact Methods**:
- GPG-encrypted email
- Signal (if available)
- Secure communication channel

### Maintainers

**Location**: `governance/config/maintainers/`

**Contact Methods**:
- GitHub
- Email
- Communication channels

---

## Time Estimates Summary

| Phase | Minimum | Maximum | Notes |
|-------|---------|---------|-------|
| Discovery | 1h | 2h | Depends on bug complexity |
| Private Disclosure | 2h | 4h | Depends on keyholder availability |
| Emergency Activation | 2h | 4h | Depends on signature collection |
| Fix Development | 4h | 8h | Depends on bug complexity |
| Testing | 2h | 4h | Depends on test coverage |
| Release | 12h | 24h | Depends on deployment complexity |
| Public Disclosure | 24h | 48h | Depends on coordination |
| **Total** | **47h** | **94h** | **~2-4 days** |

---

## Quick Reference

**Emergency Tier Activation**: 5-of-7 emergency keyholders  
**Fix Approval**: 4-of-7 maintainers (Tier 1)  
**Max Duration**: 7 days (Tier 1)  
**Post-Mortem**: Required within 90 days

**Key Documents**:
- [Emergency Response Workflow](./emergency-response.md)
- [Emergency Drill Scenario](./emergency-drill-scenario.md)
- [Coordination Protocol](./coordination-protocol.md)

---

**Last Updated**: 2025-01-XX  
**Status**: Active

