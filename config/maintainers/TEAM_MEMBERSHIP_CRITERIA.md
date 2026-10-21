# Team Membership Approval and Revocation Criteria

## Overview

Team membership in the nested multisig structure (7 teams × 7 maintainers) follows a rigorous approval and revocation process to ensure maintainer quality, diversity, and accountability.

**Important Principle**: Only **on-platform activity** related to the maintainer's role in Bitcoin Commons governance is considered for governance review. Off-platform activity (personal life, other projects, social media, etc.) is explicitly disregarded.

---

## Part 1: Team Membership Approval Criteria

### 1.1 Nomination Process

**Who Can Nominate:**
- Any existing maintainer from any team
- Self-nomination allowed (with team endorsement)

**Nomination Requirements:**
- GitHub issue created in governance repository
- Must document:
  - Candidate's background and expertise
  - Contributions to Bitcoin Commons or Bitcoin ecosystem
  - Technical competence demonstration
  - Alignment with Bitcoin principles
  - Reason for nomination
  - Proposed team assignment

### 1.2 Probation Period

**Duration**: 90 days

**Requirements During Probation:**
- Can review and comment on PRs
- Cannot sign PRs (not yet a maintainer)
- Must demonstrate:
  - Technical competence through code reviews
  - Understanding of governance process
  - Active participation
  - Alignment with team's focus area

**Probation Evaluation:**
- Reviewed by team members
- Must receive positive feedback from 4-of-7 team members
- Can be extended by 30 days if needed
- Can be terminated early if concerns arise

### 1.3 Approval Process

**Team-Level Approval:**
- PR to `maintainers/teams.yml` adding new maintainer
- Requires **6-of-7 approval from the candidate's proposed team**
- Each team member reviews and signs the PR
- Team consensus required (86% of team)

**Inter-Team Approval:**
- After team approval, requires **4-of-7 teams to approve** (for team assignment)
- Ensures cross-team coordination
- Prevents single-team capture

**Final Approval:**
- Once both team and inter-team approval met:
  - PR merges
  - Governance app reloads configuration
  - New maintainer activated
  - Can now sign PRs

### 1.4 Approval Criteria

**Technical Competence:**
- Demonstrated expertise in team's focus area
- Code contributions or reviews showing competence
- Understanding of Bitcoin protocol and Commons architecture
- Ability to review and sign PRs responsibly

**Alignment with Bitcoin Principles:**
- Commitment to user sovereignty
- Understanding of "exit over voice" philosophy
- Alignment with cryptographic governance
- No conflicts of interest

**Diversity Considerations:**
- Geographic distribution (multi-jurisdictional)
- Role diversity (different expertise areas)
- Employment diversity (no single organization dominates)
- Timezone coverage (enables responsive reviews)

**Team Fit:**
- Expertise matches team's focus area
- Can contribute meaningfully to team's work
- Compatible with team's working style
- Adds value to team composition

---

## Part 2: Team Membership Revocation Criteria

### 2.1 Voluntary Exit

**Process:**
- Maintainer creates PR removing themselves from `maintainers/teams.yml`
- 30-day notice period
- Requires **3-of-7 approval from their team** (simple majority)
- Governance app deactivates key after merge

**Graceful Transition:**
- Maintainer can complete in-progress reviews
- 30-day period allows for knowledge transfer
- Can transition to emeritus status (advisory role)

### 2.2 Performance-Based Removal

**Grounds for Removal:**
1. **Inactivity**: < 20% participation over 180 days
2. **Incompetence**: Repeated technical errors in reviews
3. **Code of Conduct Violation**: Violation of code of conduct **on-platform** (only on-platform activity considered)
   - Off-platform activity is disregarded
   - Only violations related to maintainer role and governance activities
   - Examples: Abuse in PR reviews, harassment in governance discussions, malicious code submissions
4. **Conflicts of Interest**: Undisclosed conflicts affecting judgment
5. **Security Concerns**: Key compromise or security violations

**Process:**

**Step 1: Concern Raised**
- Any maintainer creates issue in governance repo
- Documents problems with evidence
- Issue is public and transparent

**Step 2: Response Period**
- Subject maintainer has 30 days to respond
- Can address concerns or provide explanation
- Community can comment

**Step 3: Formal Warning (Optional)**
- If concerns are minor, formal warning issued
- Requires **4-of-7 vote from team**
- Warning logged in `governance/warnings/` directory
- Publicly visible
- 90-day improvement period

**Step 4: Removal Vote**
- PR to remove from `maintainers/teams.yml`
- Requires **6-of-7 approval from team** (excluding subject maintainer)
- Requires **4-of-7 teams to approve** (inter-team consensus)
- High threshold prevents frivolous removals

**Step 5: Appeal Period**
- 60-day appeal period after removal
- Subject can present new evidence
- Requires **5-of-7 teams to overturn** (higher threshold)

**Step 6: Final Removal**
- After appeal period (or if appeal denied)
- PR merges
- Governance app deactivates key
- Maintainer removed from team

### 2.3 Emergency Removal

**Grounds:**
- Key compromise (immediate security risk)
- Gross violations **on-platform** (immediate security threat, active attack, ongoing fraud)
- Network-threatening actions

**Process:**
- Emergency keyholders can immediately deactivate key
- Requires **4-of-5 emergency keyholders**
- Formal removal process follows within 7 days
- Subject can appeal through normal process

**Note**: Off-platform activity (personal life, other projects, social media, etc.) is **explicitly disregarded** for governance review. Only on-platform activity related to the maintainer's role in Bitcoin Commons governance is considered. If violations relate to key holder duties, they will manifest on-platform (missing funds, invalid signatures, security breaches).

---

## Part 3: Team Assignment Criteria

### 3.1 Team Selection

**Factors Considered:**
1. **Expertise Match**: Candidate's skills align with team's focus
2. **Team Balance**: Maintains diversity within team
3. **Workload**: Team not already at capacity
4. **Geographic Distribution**: Maintains multi-jurisdictional balance
5. **Timezone Coverage**: Enables responsive reviews

### 3.2 Team Transfer

**Process:**
- Maintainer requests transfer to different team
- Requires **5-of-7 approval from current team** (release)
- Requires **6-of-7 approval from new team** (acceptance)
- Requires **4-of-7 teams to approve** (inter-team coordination)
- Ensures smooth transition

**Grounds for Transfer:**
- Expertise better matches different team
- Team workload rebalancing
- Personal preference (with justification)
- Team composition needs

---

## Part 4: Key Management

### 4.1 Key Requirements

**Cryptographic Standards:**
- secp256k1 signature scheme (Bitcoin-compatible)
- 256-bit private keys
- Hardware security module (HSM) support for production
- BIP32 HD wallet derivation

**Key Distribution:**
- No single jurisdiction holds majority
- No single organization holds majority
- Keys held by individuals, not companies
- Geographic diversity enforced

### 4.2 Key Rotation

**Scheduled Rotation:**
- Every 2 years (recommended)
- PR updating public key in `maintainers/teams.yml`
- Requires **3-of-7 approval from team**
- Governance app updates to use new key

**Emergency Rotation:**
- If key compromise suspected
- Immediate rotation via emergency keyholders
- Requires **4-of-5 emergency keyholders**
- New key must be verified before activation

### 4.3 Key Loss

**Process:**
- Maintainer reports key loss immediately
- Key deactivated via emergency process
- New key generated and verified
- Requires **5-of-7 team approval** for new key activation
- Social recovery available (high threshold)

---

## Part 5: Team Composition Requirements

### 5.1 Diversity Requirements

**Geographic Distribution:**
- No single jurisdiction > 30% of team
- Minimum 3 jurisdictions represented per team
- Multi-jurisdictional key ceremonies

**Role Diversity:**
- Different expertise areas within team
- Core developers, security researchers, protocol designers
- Prevents single-perspective dominance

**Employment Diversity:**
- No single organization > 40% of team
- Mix of independent contributors and organizational employees
- Prevents organizational capture

**Timezone Coverage:**
- Teams should span multiple timezones
- Enables responsive reviews (24-hour coverage)
- Prevents timezone-based bottlenecks

### 5.2 Team Size Management

**Minimum Team Size**: 5 maintainers (for 6-of-7 threshold)
**Maximum Team Size**: 7 maintainers (standard)
**Optimal Team Size**: 7 maintainers (allows for 1 absence)

**Team Expansion:**
- Can expand beyond 7 if needed (with governance approval)
- Requires **5-of-7 teams to approve** expansion
- Thresholds adjust proportionally

**Team Reduction:**
- If team falls below 5, must recruit within 90 days
- Can merge teams if both below minimum
- Requires **6-of-7 teams to approve** merger

---

## Part 6: Approval Thresholds Summary

### Adding Maintainer to Team
- **Team Approval**: 6-of-7 from proposed team (86%)
- **Inter-Team Approval**: 4-of-7 teams (57%)
- **Total Consensus**: ~49% of all maintainers

### Removing Maintainer from Team
- **Voluntary**: 3-of-7 from team (43%)
- **Performance-Based**: 6-of-7 from team (excluding subject) + 4-of-7 teams
- **Emergency**: 4-of-5 emergency keyholders

### Team Transfer
- **Release from Current Team**: 5-of-7 (71%)
- **Acceptance to New Team**: 6-of-7 (86%)
- **Inter-Team Approval**: 4-of-7 teams (57%)

### Key Rotation
- **Scheduled**: 3-of-7 from team (43%)
- **Emergency**: 4-of-5 emergency keyholders

---

## Part 7: Transparency and Accountability

### 7.1 Public Documentation

**All Actions Publicly Documented:**
- Nominations: GitHub issues
- Approvals: PRs with signatures
- Removals: PRs with rationale
- Warnings: Files in `governance/warnings/`
- Appeals: GitHub discussions

### 7.2 Audit Trail

**Cryptographic Proof:**
- All approvals signed cryptographically
- Signatures publicly verifiable
- Immutable audit log
- OpenTimestamps for timestamping

### 7.3 Community Oversight

**Public Comment Periods:**
- 30-day comment period for nominations
- 30-day response period for removal concerns
- Community can raise issues
- Journalists can report on patterns

---

## Part 8: Special Cases

### 8.1 Emeritus Status

**Available For:**
- Maintainers who voluntarily step down
- Maintainers removed for inactivity (not violations)
- Maintainers transitioning to advisory role

**Benefits:**
- Can still review PRs (no signing authority)
- Access to maintainer discussions
- Recognition for past contributions

**Process:**
- Maintainer requests emeritus status
- Requires **3-of-7 team approval**
- Status documented in `maintainers/emeritus.yml`

### 8.2 Temporary Leave

**Process:**
- Maintainer requests temporary leave
- Status set to "on_leave" in teams.yml
- Key remains active but maintainer not expected to sign
- Team can operate with reduced size temporarily
- Maximum leave: 180 days (then must return or step down)

**Approval:**
- Requires **3-of-7 team approval**
- Can be extended once by 90 days
- After extension, must return or step down

---

## Part 9: Implementation Notes

### 9.1 Governance App Integration

**Automated Checks:**
- Verifies team approval thresholds
- Tracks probation periods
- Monitors participation levels
- Enforces key rotation schedules

**Manual Override:**
- Emergency situations
- Requires emergency keyholder approval
- Logged and publicly visible

### 9.2 Configuration Files

**Team Membership:**
- `governance/config/maintainers/teams.yml` - Team structure and members
- `governance/warnings/` - Formal warnings directory
- `governance/maintainers/emeritus.yml` - Emeritus maintainers

**Changes Require:**
- PR to governance repository
- Appropriate approval thresholds
- Governance app reloads after merge

---

## Conclusion

Team membership follows a rigorous but fair process:

**Approval**: High threshold (6-of-7 team + 4-of-7 teams) ensures quality
**Revocation**: High threshold (6-of-7 excluding subject) prevents abuse
**Transparency**: All actions publicly documented and verifiable
**Accountability**: Clear criteria and processes for all decisions

The nested multisig structure ensures that team membership decisions require broad consensus, preventing capture while maintaining flexibility for legitimate changes.

