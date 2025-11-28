# Maintainer Governance Review Policy

## Policy Statement

Only **on-platform activity** related to a maintainer's role in Bitcoin Commons governance is considered for governance review. Off-platform activity is explicitly disregarded.

---

## Definitions

**On-Platform Activity:** Activity occurring within Bitcoin Commons governance context, including:
- PR reviews and comments
- Code contributions to Bitcoin Commons repositories
- Governance discussions in GitHub issues/discussions
- Signature behavior and technical decisions
- Maintainer interactions in governance context

**Off-Platform Activity:** All activity outside Bitcoin Commons governance, including:
- Personal life, relationships, opinions, political views
- Work on other projects (Bitcoin or otherwise)
- Social media posts (unless directly related to Bitcoin Commons governance)
- Personal legal issues

**Key Holder Duties:** Responsibilities related to maintaining cryptographic keys for Bitcoin Commons governance, including:
- Securely storing and using signing keys
- Participating in multisig operations
- Protecting system security and integrity

**Abuse:** Behavior that violates the Code of Conduct, including but not limited to:
- Personal attacks, insults, or derogatory comments
- Harassment (repeated unwanted contact or behavior)
- Threats or intimidation
- Discrimination based on protected characteristics

**Harassment:** Unwelcome conduct that creates an intimidating, hostile, or offensive environment, including:
- Repeated unwanted contact
- Offensive comments or jokes
- Display of offensive material
- Physical intimidation

**Conflict of Interest:** A situation where a maintainer's personal interests could improperly influence their governance decisions, including:
- Financial interest in competing projects that could affect judgment
- Employment by entities with conflicting interests
- Undisclosed relationships that could affect impartiality
- Personal gain from governance decisions

**Gross Misconduct:** Severe on-platform violations that pose an immediate security threat, including:
- Active attack on the system
- Ongoing fraud or theft
- Immediate key compromise risk
- Malicious code that could cause immediate harm

**Repeated Technical Errors:** Pattern of technical mistakes indicating incompetence:
- 3+ critical errors (security, consensus, data loss) in 6 months
- 5+ significant errors (functionality, performance) in 6 months
- Demonstrated inability to perform key holder duties despite warnings

**False Report:** A governance review report made with knowledge that the allegations are false or with reckless disregard for the truth.

**Retaliation:** Any adverse action taken against a maintainer for reporting a governance review case, including:
- Threats or intimidation
- Exclusion from discussions or decisions
- Unjustified removal or demotion
- Any form of harassment

---

## Scope

### On-Platform Review

The following constitute grounds for sanctions when occurring on-platform:
- Abuse or harassment in PR reviews or governance discussions
- Malicious code submissions or security violations
- Collusion to bypass governance mechanisms
- Undisclosed conflicts of interest affecting governance decisions
- Repeated technical errors indicating incompetence
- Key sharing or unauthorized access

### Off-Platform Activity

**All off-platform activity is disregarded.** This includes:
- Personal life, relationships, opinions, political views
- Work on other projects
- Social media posts (unless directly related to Bitcoin Commons governance)
- Personal legal issues

**No exceptions.** If violations relate to key holder duties, they will manifest on-platform (missing funds, invalid signatures, security breaches).

---

## Graduated Sanctions

Governance review cases are handled through a graduated sanction system, providing opportunities for correction before removal.

### Level 1: Private Warning

**Trigger:** Minor violations or first offense of moderate severity.

**Process:**
1. Any maintainer reports issue
2. Team members review (4-of-7 team approval)
3. Private written warning issued
4. Subject has 14 days to respond
5. Warning logged privately (not public)

**Consequence:** Private warning, opportunity to correct behavior.

**Appeal:** Subject can appeal to team (requires 5-of-7 to overturn).

### Level 2: Public Warning

**Trigger:** Moderate violations, pattern of minor violations, or failure to correct after private warning.

**Process:**
1. Issue created in governance repository
2. Team members review (5-of-7 team approval)
3. Public warning issued
4. Warning logged in `governance/warnings/` directory
5. Subject has 30 days to respond
6. 90-day improvement period

**Consequence:** Public warning, 90-day improvement period, potential restrictions.

**Appeal:** Subject can appeal (requires 6-of-7 team to overturn).

### Level 3: Removal

**Trigger:** Serious violations, failure to correct after warnings, or immediate security threat.

**Process:**
1. Issue created with evidence
2. Team members review (6-of-7 excluding subject + 4-of-7 teams)
3. Subject has 30 days to respond
4. Evaluation against criteria
5. Removal if warranted
6. All documentation public

**Consequence:** Removal from team, key deactivated.

**Appeal:** 60-day appeal period, requires 5-of-7 teams to overturn.

---

## Procedures

### Reporting Governance Review Cases

**Who Can Report:**
- Any maintainer
- Any contributor (via maintainer)
- Community members (via maintainer)

**How to Report:**
1. Create GitHub issue in governance repository
2. Document the violation with evidence
3. Include links, screenshots, or other proof
4. Maintainer reviews and processes

**Protection for Reporters:**
- Retaliation against reporters is immediate grounds for removal
- False/malicious reports are grounds for warning or removal
- Reporters' privacy respected (unless they choose to be public)

### On-Platform Review Process

1. **Report**: Issue created in governance repository
2. **Initial Review**: Team members determine severity (4-of-7 for warning, 6-of-7 for removal)
3. **Response**: Subject has 30 days to respond
4. **Mediation** (if non-security): Optional 30-day mediation period for conflicts
5. **Evaluation**: Team evaluates against code of conduct and this policy
6. **Sanction**: Warning or removal based on severity
7. **Appeal**: Subject can appeal through normal process

### Conflict Resolution/Mediation

**When Mediation Applies:**
- Non-security issues
- Disputes between maintainers
- Conflicts that could be resolved through discussion

**Process:**
1. Either party requests mediation
2. 30-day mediation period
3. Neutral maintainer facilitates (if available)
4. If resolved: Issue closed
5. If not resolved: Proceeds to normal process

**Mediation Does NOT Apply To:**
- Security issues (immediate threat)
- Active attacks
- Key compromise
- Ongoing fraud or theft

### Time Limits

**Case Resolution:**
- Cases must be resolved within 180 days
- Extensions require 5-of-7 team approval
- Emergency cases: 7 days for initial action

**Appeals:**
- Appeals must be resolved within 90 days
- Extensions require 5-of-7 teams approval

**Warnings:**
- Improvement periods: 90 days
- Can be extended once by 30 days with 4-of-7 team approval

---

## Evaluation Criteria

### For All Review Cases

1. **Severity**: How serious is the violation?
2. **Pattern**: Is this a pattern or isolated incident?
3. **Impact**: What is the impact on the system or community?
4. **Intent**: Was this intentional or accidental?
5. **Response**: How has the subject responded?
6. **History**: Previous warnings or sanctions?

### Documentation Requirements

- All evidence must be publicly documented in governance repository
- Links, screenshots, or other proof must be provided
- Evaluation rationale must be documented
- Subject maintainer must be notified and given opportunity to respond
- All decisions must be transparent

---

## Safeguards

**Prevents Abuse:**
- High threshold: 6-of-7 team + 4-of-7 teams for removal
- Graduated sanctions: Warnings before removal
- Transparency: All evidence and evaluation public
- Appeal rights: 60-day appeal period, higher threshold to overturn
- Response period: 30 days for subject to respond
- Time limits: Cases must resolve within 180 days
- Mediation: Conflict resolution before removal (non-security)

**What This Prevents:**
- Personal vendettas (requires evidence, high threshold)
- Frivolous removals (graduated sanctions, high threshold)
- Secret removals (public documentation)
- Retaliation (immediate removal for retaliation)
- False reports (consequences for false reports)
- Indefinite cases (time limits)

**Protections:**
- Whistleblower protection: Retaliation is immediate grounds for removal
- False report consequences: False/malicious reports are grounds for warning or removal
- Privacy: Reporters' privacy respected (unless they choose to be public)
- Due process: Response periods, appeals, mediation

---

## Emergency Removal

**Grounds:**
- Key compromise (immediate security risk)
- Gross violations (immediate security threat)
- Active attack on the system

**Process:**
- Emergency keyholders (4-of-5) can immediately deactivate key
- Formal removal process follows within 7 days
- Subject can appeal through normal process

**Definition of Gross Violations:**
- Active attack on the system
- Ongoing fraud or theft
- Immediate key compromise risk
- Malicious code that could cause immediate harm

**Not Gross Violations:**
- Disagreements or conflicts
- Policy violations without immediate threat
- Non-security issues

---

## Rehabilitation

**Reapplication Process:**
- Removed maintainers may reapply after 2 years
- Must demonstrate change and improvement
- Requires 6-of-7 team approval + 4-of-7 teams approval
- Same process as new maintainer (probation, etc.)

**Conditions:**
- Must address original violations
- Must demonstrate understanding of what went wrong
- Must show evidence of change
- Must meet all normal maintainer requirements

**Not Eligible:**
- Removed for security issues (key compromise, active attack)
- Removed for ongoing fraud or theft
- Removed for malicious code submission

---

## Relationship to Code of Conduct

**Code of Conduct:** Governs on-platform behavior in all Bitcoin Commons repositories, GitHub issues/PRs, governance meetings, and maintainer interactions.

**This Policy:** Defines what activity is considered for governance review, graduated sanctions, and procedures.

**Separate but Complementary:** Code of conduct violations are handled through this policy's graduated sanctions. Both apply to on-platform activity.

---

## Rationale

**Why Disregard Off-Platform Activity:**
1. Focus on governance performance, not personal life
2. Prevent abuse (no pretext for removal)
3. Align with Bitcoin principles (code, not identity)
4. Practical (often unverifiable or irrelevant)
5. Fairness (judged on work, not personal life)

**Why Graduated Sanctions:**
- Provides opportunities for correction
- More fair than immediate removal
- Allows for learning and improvement
- Matches governance-app-spec graduated sanctions

**Why Protections:**
- Encourages reporting of violations
- Prevents retaliation
- Prevents false reports
- Ensures due process

---

## Examples

### Valid On-Platform Review Cases

**Example 1: Abuse in PR Review**
- Maintainer uses abusive language in PR comments
- Harasses other maintainers in governance discussions
- **Action**: Level 1 (private warning) for first offense, Level 2 (public warning) for pattern, Level 3 (removal) for serious/repeated

**Example 2: Malicious Code**
- Maintainer submits code with intentional vulnerabilities
- Attempts to bypass security checks
- **Action**: Level 3 (removal) - immediate security threat

**Example 3: Collusion**
- Maintainers coordinate to sign bad PRs
- Attempt to bypass governance thresholds
- **Action**: Level 3 (removal) - serious governance violation

**Example 4: Repeated Technical Errors**
- Maintainer makes 4 critical errors in 6 months
- Despite warnings, continues to make errors
- **Action**: Level 2 (public warning) then Level 3 (removal) if no improvement

### Invalid Off-Platform (Disregarded)

**Example 1: Social Media Post**
- Maintainer posts controversial opinion on Twitter
- Criticizes another Bitcoin project
- **Action**: NOT grounds for any sanction (off-platform, disregarded)

**Example 2: Other Project Work**
- Maintainer works on competing Bitcoin implementation
- Contributes to other open source projects
- **Action**: NOT grounds for any sanction (off-platform, disregarded)

**Example 3: Personal Legal Issue**
- Maintainer has personal legal dispute unrelated to Bitcoin Commons
- Personal financial issues
- **Action**: NOT grounds for any sanction (off-platform, disregarded)

### False Reports and Retaliation

**Example 1: False Report**
- Maintainer makes false report to harass another maintainer
- Evidence shows report was knowingly false
- **Action**: Level 2 (public warning) or Level 3 (removal) for false reporter

**Example 2: Retaliation**
- Maintainer reports a governance review case
- Subject maintainer retaliates by excluding reporter from discussions
- **Action**: Level 3 (removal) for subject maintainer (immediate grounds)

---

## Implementation

### Grounds for Sanctions

1. **Inactivity**: < 20% participation over 180 days
2. **Incompetence**: Repeated technical errors (3+ critical in 6 months)
3. **Code of Conduct Violation**: Violation of code of conduct (on-platform only)
4. **Conflicts of Interest**: Undisclosed conflicts affecting judgment
5. **Security Concerns**: Key compromise or security violations
6. **False Reports**: Knowingly false or malicious reports
7. **Retaliation**: Retaliation against reporters

### Normal Process

1. Determine if on-platform or off-platform
2. If off-platform: Disregard entirely
3. If on-platform: Determine severity
4. Apply appropriate level (warning or removal)
5. Follow graduated sanctions process
6. Document all evidence and evaluation
7. Allow appeals through normal process

---

## References

- [Team Membership Criteria](TEAM_MEMBERSHIP_CRITERIA.md)
- [Code of Conduct](../../../.github/CODE_OF_CONDUCT.md)
- [Maintainer Guide](../../guides/MAINTAINER_GUIDE.md)
- [Governance App Spec](../../../governance-app-spec.md)
