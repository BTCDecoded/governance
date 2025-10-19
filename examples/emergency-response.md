# Emergency Response Workflow

Guide for activating and managing emergency tiers in response to critical security issues.

## Overview

BTCDecoded's three-tiered emergency system enables rapid response to critical issues while maintaining multi-signature security and accountability.

**Key Principle:** Emergencies don't eliminate governance, they adjust parameters proportionally to threat severity.

## Emergency Tier Summary

| Tier | Name | Review Period | Signatures | Max Duration | Use Case |
|------|------|---------------|------------|--------------|----------|
| 1 | Critical | 0 days | 4-of-7 | 7 days | Network-threatening (inflation, consensus fork) |
| 2 | Urgent | 7 days | 5-of-7 | 30 days | Serious security (memory corruption, privacy) |
| 3 | Elevated | 30 days | 6-of-7 | 90 days | Important priorities (bugs, competitive response) |

**All tiers require 5-of-7 emergency keyholders to activate.**

## Tier 1: Critical Emergency

### When to Use

**Network-Threatening Vulnerabilities:**
- Inflation bugs (CVE-2010-5139 class)
- Consensus fork risks (CVE-2018-17144 class)
- P2P network DoS enabling 51% attack
- Remote code execution in consensus code
- Private key extraction vulnerabilities

**Historical Examples:**

**CVE-2010-5139 (Value Overflow Incident, 2010):**
- Bug allowed creation of 184 billion BTC in single transaction
- Discovered in block 74638
- Fixed via hard fork in ~5 hours
- Network rolled back 53 blocks
- **Would qualify as Tier 1 Critical**

**CVE-2018-17144 (Inflation Bug, 2018):**
- Bug allowed double-spend of same input in same transaction
- Discovered during code review (not exploited)
- Same-day patch released to maintainers
- Public disclosure 2 weeks after majority upgrade
- **Would qualify as Tier 1 Critical**

### Activation Process

**Step 1: Discovery and Private Disclosure (Hours)**

1. **Discover Vulnerability**
   - Security researcher or developer finds critical bug
   - Assess impact (inflation? fork? DoS?)
   - Confirm reproducibility

2. **Private Disclosure**
   - Contact BTCDecoded emergency keyholders via secure channel
   - GPG-encrypted email or Signal
   - Provide:
     - Vulnerability description
     - Proof of concept (if safe)
     - Impact analysis
     - Proposed fix

3. **Initial Assessment**
   - Emergency keyholders evaluate severity
   - Confirm Tier 1 classification
   - Begin coordination

**Step 2: Emergency Keyholder Activation (Hours)**

1. **Activation Request**
   - One keyholder submits formal activation request to governance repo
   - Private branch (not public yet)
   - Includes:
     - Evidence of vulnerability (sanitized)
     - Justification for Tier 1
     - Proposed timeline
     - Communication plan

2. **Keyholder Signatures**
   - Other keyholders review evidence
   - Each signs activation request
   - 5-of-7 required to activate
   - Cryptographic signatures logged

3. **Tier Activated**
   - Governance App activates Tier 1
   - Review period: 0 days
   - Signature threshold: 4-of-7 maintainers
   - Max duration: 7 days
   - Clock starts

**Step 3: Fix Development (Hours to Days)**

1. **Develop Patch**
   - Core developers write fix
   - Minimize code changes
   - Focus on closing vulnerability

2. **Internal Testing**
   - Test patch thoroughly
   - Verify fix works
   - Ensure no new vulnerabilities
   - Check for side effects

3. **Create Pull Request**
   - Open PR in affected repository
   - Tag: `[EMERGENCY-TIER-1]`
   - Link to keyholder activation
   - Include fix description (minimal details)

**Step 4: Maintainer Review and Approval (Hours to Days)**

1. **Expedited Review**
   - 0-day review period (can merge immediately after signatures)
   - Maintainers focus on:
     - Does fix address vulnerability?
     - Does fix introduce new issues?
     - Is fix minimal and targeted?

2. **Maintainer Signatures**
   - 4-of-7 required (lower threshold for speed)
   - Each maintainer signs PR
   - Command: `/governance-sign <signature>`
   - Governance App validates

3. **Merge**
   - Once 4 signatures received, merge enabled
   - Lead maintainer merges immediately
   - No waiting period

**Step 5: Release and Deployment (Hours)**

1. **Emergency Release**
   - Build binaries immediately
   - Version: e.g., `v1.2.1-emergency`
   - Release notes: minimal details ("critical security fix")

2. **Private Distribution**
   - Alert major node operators via secure channel
   - Provide upgrade instructions
   - Emphasize urgency
   - No public announcement yet

3. **Monitor Deployment**
   - Track node upgrade percentage
   - Target: 80%+ before public disclosure
   - Timeline: 24-72 hours typical

**Step 6: Public Disclosure (Days to Weeks)**

1. **Disclosure Timing**
   - After majority node deployment (80%+)
   - Before 7-day emergency expiration
   - Consider responsible disclosure timeline

2. **Public Announcement**
   - Publish full vulnerability details
   - CVE assigned
   - Timeline of discovery and fix
   - Credit to researchers

3. **Post-Mortem Required**
   - Deadline: 30 days after activation
   - Must include:
     - Full vulnerability analysis
     - Timeline of events
     - Lessons learned
     - Process improvements

4. **Security Audit Required**
   - Deadline: 60 days after activation
   - Professional audit of affected code
   - Verify no similar vulnerabilities
   - Report published

**Step 7: Emergency Expiration (7 Days Max)**

- Tier 1 automatically expires after 7 days
- No extensions allowed
- If issue not resolved, escalate to normal process or activate new emergency

### Example Timeline (Tier 1)

**Hour 0:** Vulnerability discovered
**Hour 2:** Emergency keyholders notified privately
**Hour 4:** 5-of-7 keyholders sign activation
**Hour 6:** Tier 1 activated, fix development begins
**Hour 12:** PR opened with fix
**Hour 18:** 4-of-7 maintainers sign
**Hour 18:** Merged and released
**Hour 24-72:** Private deployment to major nodes
**Day 3:** Public disclosure (80% upgraded)
**Day 7:** Emergency expires
**Day 30:** Post-mortem published
**Day 60:** Security audit completed

## Tier 2: Urgent Security Issue

### When to Use

**Serious Security Issues (Not Network-Threatening):**
- Memory corruption vulnerabilities
- Privacy leaks (transaction linkage)
- Crash exploits (non-DoS)
- Privilege escalation
- Data corruption bugs

**Historical Example:**

**BIP66 Consensus Fork (2015):**
- Strict DER signature encoding enforcement
- Non-upgraded miners accepted invalid block
- Required urgent coordination over hours/days
- Not immediately catastrophic but required fast response
- **Would qualify as Tier 2 Urgent**

### Activation Process

Similar to Tier 1 but with differences:

**Differences from Tier 1:**
- **7-day review period** (not 0)
- **5-of-7 maintainer signatures** (not 4)
- **30-day max duration** (not 7)
- **1 extension allowed** (30 more days, requires 6-of-7)
- **Public disclosure after majority deployment** (not specific timing)

**Timeline:** Days to weeks, not hours

**Post-Activation:**
- Post-mortem required (60-day deadline)
- Security audit not required (but recommended)

### Example Timeline (Tier 2)

**Day 0:** Vulnerability discovered and reported
**Day 1:** Emergency keyholders notified
**Day 2:** 5-of-7 keyholders sign activation
**Day 3:** Tier 2 activated
**Day 5:** PR opened with fix
**Day 10:** 5-of-7 maintainer signatures received (7-day review elapsed)
**Day 10:** Merged and released
**Day 20:** Majority deployment achieved
**Day 21:** Public disclosure
**Day 30:** Emergency expires (or extended)
**Day 60:** Post-mortem published

## Tier 3: Elevated Priority

### When to Use

**Important But Not Critical:**
- Competitive response (other implementations advancing)
- Important bug fixes (non-security)
- Performance degradation issues
- Ecosystem compatibility problems
- User experience issues affecting adoption

**Example Scenarios:**

**Competitive Response:**
- Bitcoin Core releases major feature
- BTCDecoded needs to match to stay relevant
- Normal 180-day review too slow
- Not a security issue, but strategic priority

**Important Bug:**
- Sync issues causing user frustration
- Not security-critical but affecting adoption
- Fix available but stuck in normal review
- Elevated priority warranted

### Activation Process

**Differences from Tier 2:**
- **30-day review period** (not 7)
- **6-of-7 maintainer signatures** (not 5)
- **90-day max duration** (not 30)
- **2 extensions allowed** (30 days each, requires 6-of-7)
- **Immediate public disclosure**

**Timeline:** Weeks to months

**Post-Activation:**
- Post-mortem required (90-day deadline)
- No security audit required
- Focuses on process evaluation, not vulnerability

### Example Timeline (Tier 3)

**Week 0:** Issue identified, elevated priority proposed
**Week 1:** Emergency keyholders review, 5-of-7 sign activation
**Week 2:** Tier 3 activated, PR opened
**Week 6:** 30-day review period complete
**Week 7:** 6-of-7 maintainer signatures received
**Week 7:** Merged and released
**Week 13:** Emergency expires (or extended)
**Week 26:** Post-mortem published (90-day deadline)

## Extension Process

### When Extensions Are Needed

**Valid Reasons:**
- Issue more complex than initially assessed
- Fix requires more testing than expected
- Dependent changes needed
- Coordination with ecosystem taking longer

**Invalid Reasons:**
- Poor planning
- Insufficient urgency
- Scope creep
- Avoiding normal process

### Extension Request

**Tier 1:** Not allowed (resolve within 7 days or use new emergency)

**Tier 2:** 1 extension allowed
- Duration: 30 days
- Threshold: 6-of-7 keyholders (higher than activation)
- Justification required

**Tier 3:** 2 extensions allowed
- Duration: 30 days each
- Threshold: 6-of-7 keyholders
- Stronger justification for second extension

### Extension Approval

1. **Request Submission**
   - Current emergency keyholder submits extension request
   - Must include:
     - Justification for extension
     - Progress update
     - Timeline for completion

2. **Keyholder Review**
   - Higher threshold (6-of-7 vs 5-of-7)
   - Discourages frivolous extensions
   - Can reject if insufficient justification

3. **Extension Approved**
   - Governance App extends expiration
   - New deadline set
   - Extension count incremented

## Safeguards Against Abuse

### Transparency

- All emergency activations logged in governance repo
- Public disclosure required (timing varies by tier)
- Signatures cryptographically verified
- Audit trail immutable

### Accountability

- Post-mortem required for all tiers
- Security audit required for Tier 1
- Deadline enforcement
- Community oversight

### Automatic Expiration

- No indefinite emergencies
- Fixed maximum durations
- Extensions require higher thresholds
- Multiple extensions discouraged

### Graduated Response

- Start with appropriate tier
- Can escalate if situation worsens
- Cannot downgrade active emergency without resolution

## Anti-Patterns to Avoid

### ❌ Emergency Tier for Convenience

**Wrong:**
- "Normal process takes too long, let's use Tier 3"
- No actual urgency or priority
- Just impatient

**Right:**
- Use emergency tiers only for genuine urgencies
- Plan ahead to avoid artificial emergencies

### ❌ Scope Creep During Emergency

**Wrong:**
- "While we're in Tier 1, let's also fix these other issues"
- Adding unrelated changes
- Expanding scope beyond vulnerability

**Right:**
- Fix only the specific emergency issue
- Minimal, targeted changes
- Other improvements through normal process

### ❌ Inadequate Evidence

**Wrong:**
- "Trust us, this is critical"
- No proof of vulnerability
- Vague claims

**Right:**
- Provide concrete evidence
- Reproducible demonstration
- Clear impact analysis

### ❌ Indefinite Extension

**Wrong:**
- Repeatedly extending Tier 3
- Never completing work
- Using emergency as excuse

**Right:**
- Complete work within initial duration
- If truly can't finish, let emergency expire and use normal process

## Communication Best Practices

### During Private Phase (Pre-Disclosure)

**Do:**
- Use encrypted channels (GPG, Signal)
- Limit information to need-to-know
- Coordinate with major node operators
- Prepare public disclosure ahead of time

**Don't:**
- Post public hints or breadcrumbs
- Discuss on public forums
- Create PR until ready to disclose
- Leave evidence attackers could find

### During Public Disclosure

**Do:**
- Provide full technical details
- Include timeline of events
- Credit researchers appropriately
- Explain impact and mitigation

**Don't:**
- Minimize severity
- Blame others
- Avoid accountability
- Rush disclosure before majority deployed

### Post-Mortem

**Include:**
- How vulnerability was discovered
- Why it existed (root cause)
- How it was fixed
- Process improvements
- Lessons learned

**Tone:**
- Honest and transparent
- Focus on learning, not blame
- Acknowledge mistakes
- Commit to improvements

## Comparison to Historical Bitcoin Responses

### Value Overflow (2010)

**What Happened:**
- 184 billion BTC created in transaction
- Discovered after confirmed in block
- Required hard fork to rollback

**Response Time:**
- ~5 hours from discovery to fix deployment
- Community coordination
- Hard fork activated

**BTCDecoded Tier 1 Equivalent:**
- 0-day review, 4-of-7 signatures
- Could respond in similar timeframe
- Maintains multi-sig security even in crisis

### Inflation Bug (2018)

**What Happened:**
- Consensus bug allowing double-spend
- Discovered during code review (not exploited)
- Same-day patch to maintainers

**Response Time:**
- Hours to patch
- Days to majority deployment
- 2 weeks to public disclosure

**BTCDecoded Tier 1 Equivalent:**
- Same rapid response capability
- Structured process instead of ad-hoc
- Formal post-mortem and audit requirements

### BIP66 Fork (2015)

**What Happened:**
- Soft fork to enforce strict DER signatures
- Invalid block accepted by non-upgraded miners
- Coordination needed over hours/days

**Response Time:**
- Hours to coordinate
- Days to resolve fully
- Not immediately catastrophic

**BTCDecoded Tier 2 Equivalent:**
- 7-day review appropriate
- 5-of-7 signatures
- Public disclosure after resolution

## Conclusion

Emergency tiers enable rapid response while maintaining:

1. **Multi-signature security:** No single point of failure
2. **Proportional response:** Severity matches process
3. **Accountability:** Post-mortem and audit requirements
4. **Transparency:** Public disclosure and logging
5. **Automatic expiration:** No indefinite emergencies

**Key Insight:** Bitcoin's history shows some vulnerabilities require hour/day responses. BTCDecoded formalizes this capability without sacrificing security or accountability.

---

*For questions or to report security vulnerabilities, see SECURITY.md in the governance-app repository.*


