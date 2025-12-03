# Emergency Response Workflow

## Overview

Three-tiered emergency system enables rapid response to critical issues while maintaining multi-signature security and accountability. **Key Principle**: Emergencies don't eliminate governance, they adjust parameters proportionally to threat severity.

## Emergency Tier Summary

| Tier | Name | Review Period | Signatures | Max Duration | Use Case |
|------|------|---------------|------------|--------------|----------|
| 1 | Critical | 0 days | 4-of-7 | 7 days | Network-threatening (inflation, consensus fork) |
| 2 | Urgent | 7 days | 5-of-7 | 30 days | Serious security (memory corruption, privacy) |
| 3 | Elevated | 30 days | 6-of-7 | 90 days | Important priorities (bugs, competitive response) |

**All tiers require 5-of-7 emergency keyholders to activate.**

## Tier 1: Critical Emergency

### When to Use

**Network-Threatening Vulnerabilities**: Inflation bugs (CVE-2010-5139), consensus fork risks (CVE-2018-17144), P2P network DoS enabling 51% attack, remote code execution in consensus code, private key extraction.

**Historical Examples**:
- **CVE-2010-5139**: 184 billion BTC created, fixed via hard fork in ~5 hours
- **CVE-2018-17144**: Double-spend bug, same-day patch, 2-week disclosure

### Activation Process

1. **Discovery and Private Disclosure** (Hours)
   - Discover vulnerability, assess impact, confirm reproducibility
   - Contact emergency keyholders via secure channel (GPG/Signal)
   - Provide: vulnerability description, PoC (if safe), impact analysis, proposed fix

2. **Emergency Keyholder Activation** (Hours)
   - One keyholder submits activation request (private branch)
   - 5-of-7 keyholders sign activation request
   - Governance App activates Tier 1 (0-day review, 4-of-7 maintainers, 7-day max)

3. **Fix Development** (Hours to Days)
   - Develop patch (minimize changes, focus on closing vulnerability)
   - Internal testing (verify fix, ensure no new vulnerabilities)
   - Create PR (tag `[EMERGENCY-TIER-1]`, link to keyholder activation)

4. **Maintainer Review and Approval** (Hours to Days)
   - Expedited review (0-day period, can merge immediately after signatures)
   - 4-of-7 maintainer signatures required
   - Merge once signatures received

5. **Release and Deployment** (Hours)
   - Emergency release (build binaries immediately, version `v1.2.1-emergency`)
   - Private distribution (alert major node operators via secure channel)
   - Monitor deployment (target 80%+ before public disclosure, 24-72 hours typical)

6. **Public Disclosure** (Days to Weeks)
   - After majority node deployment (80%+)
   - Before 7-day emergency expiration
   - Publish full vulnerability details, CVE assigned, timeline, credit researchers

7. **Post-Activation Requirements**
   - Post-mortem required (30-day deadline)
   - Security audit required (60-day deadline)

### Example Timeline (Tier 1)

**Hour 0**: Vulnerability discovered  
**Hour 2**: Emergency keyholders notified  
**Hour 4**: 5-of-7 keyholders sign activation  
**Hour 6**: Tier 1 activated, fix development begins  
**Hour 12**: PR opened with fix  
**Hour 18**: 4-of-7 maintainers sign, merged and released  
**Hour 24-72**: Private deployment to major nodes  
**Day 3**: Public disclosure (80% upgraded)  
**Day 7**: Emergency expires  
**Day 30**: Post-mortem published  
**Day 60**: Security audit completed

## Tier 2: Urgent Security Issue

### When to Use

**Serious Security Issues (Not Network-Threatening)**: Memory corruption, privacy leaks, crash exploits, privilege escalation, data corruption bugs.

**Historical Example**: BIP66 Consensus Fork (2015) - strict DER enforcement, required urgent coordination over hours/days.

### Differences from Tier 1

| Aspect | Tier 1 | Tier 2 |
|--------|--------|--------|
| Review Period | 0 days | 7 days |
| Signatures | 4-of-7 | 5-of-7 |
| Max Duration | 7 days | 30 days |
| Extensions | Not allowed | 1 extension (30 days, 6-of-7) |
| Post-Mortem | 30 days | 60 days |
| Security Audit | Required (60 days) | Recommended |

### Example Timeline (Tier 2)

**Day 0**: Vulnerability discovered  
**Day 1**: Emergency keyholders notified  
**Day 2**: 5-of-7 keyholders sign activation  
**Day 3**: Tier 2 activated  
**Day 5**: PR opened with fix  
**Day 10**: 5-of-7 maintainer signatures (7-day review elapsed), merged  
**Day 20**: Majority deployment  
**Day 21**: Public disclosure  
**Day 30**: Emergency expires (or extended)  
**Day 60**: Post-mortem published

## Tier 3: Elevated Priority

### When to Use

**Important But Not Critical**: Competitive response, important bug fixes (non-security), performance degradation, ecosystem compatibility, user experience issues affecting adoption.

### Differences from Tier 2

| Aspect | Tier 2 | Tier 3 |
|--------|--------|--------|
| Review Period | 7 days | 30 days |
| Signatures | 5-of-7 | 6-of-7 |
| Max Duration | 30 days | 90 days |
| Extensions | 1 extension | 2 extensions (30 days each, 6-of-7) |
| Post-Mortem | 60 days | 90 days |
| Security Audit | Recommended | Not required |

### Example Timeline (Tier 3)

**Week 0**: Issue identified  
**Week 1**: 5-of-7 keyholders sign activation  
**Week 2**: Tier 3 activated, PR opened  
**Week 6**: 30-day review complete  
**Week 7**: 6-of-7 maintainer signatures, merged  
**Week 13**: Emergency expires (or extended)  
**Week 26**: Post-mortem published

## Extension Process

| Tier | Extensions Allowed | Duration | Threshold | Justification |
|------|-------------------|----------|-----------|---------------|
| 1 | Not allowed | N/A | N/A | Resolve within 7 days or use new emergency |
| 2 | 1 extension | 30 days | 6-of-7 | Required |
| 3 | 2 extensions | 30 days each | 6-of-7 | Required (stronger for second) |

**Valid Reasons**: Issue more complex than assessed, fix requires more testing, dependent changes needed, coordination taking longer.

**Invalid Reasons**: Poor planning, insufficient urgency, scope creep, avoiding normal process.

## Safeguards Against Abuse

| Safeguard | Mechanism |
|-----------|-----------|
| **Transparency** | All activations logged, public disclosure required, signatures verified, immutable audit trail |
| **Accountability** | Post-mortem required, security audit (Tier 1), deadline enforcement, community oversight |
| **Automatic Expiration** | Fixed maximum durations, extensions require higher thresholds, multiple extensions discouraged |
| **Graduated Response** | Start with appropriate tier, can escalate if worsens, cannot downgrade without resolution |

## Anti-Patterns to Avoid

| Anti-Pattern | Wrong | Right |
|--------------|-------|-------|
| **Emergency for Convenience** | "Normal process takes too long" | Use only for genuine urgencies |
| **Scope Creep** | "While in Tier 1, let's fix other issues" | Fix only specific emergency issue |
| **Inadequate Evidence** | "Trust us, this is critical" | Provide concrete evidence, reproducible demonstration |
| **Indefinite Extension** | Repeatedly extending Tier 3 | Complete work within initial duration |

## Communication Best Practices

| Phase | Do | Don't |
|-------|-----|-------|
| **Private Phase** | Use encrypted channels (GPG, Signal), limit to need-to-know, coordinate with major operators, prepare disclosure | Post public hints, discuss on public forums, create PR until ready |
| **Public Disclosure** | Provide full technical details, include timeline, credit researchers, explain impact | Minimize severity, blame others, avoid accountability, rush before majority deployed |
| **Post-Mortem** | Include: how discovered, why existed, how fixed, process improvements, lessons learned | Focus on blame, avoid mistakes, avoid improvements |

## Conclusion

Emergency tiers enable rapid response while maintaining: multi-signature security (no single point of failure), proportional response (severity matches process), accountability (post-mortem and audit), transparency (public disclosure and logging), automatic expiration (no indefinite emergencies).
