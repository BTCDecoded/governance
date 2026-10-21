# Maintainer Governance Review Policy

## Policy Statement

Only **on-platform activity** related to a maintainer's role in Bitcoin Commons governance is considered for governance review. Off-platform activity is explicitly disregarded.

**Related:** Automated or AI-assisted *code review* norms for Bitcoin Commons implementations (alternative vs Core fork, consensus flags, Compact alignment) live in **[guides/REVIEW_INTELLIGENCE.md](../../guides/REVIEW_INTELLIGENCE.md)**. That document is distinct from this policy, which covers maintainer conduct review only.

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
- `issue_private_warning` compares `approvals.len()` with `PRIVATE_WARNING_THRESHOLD` (4). It does not count a team of 7.
- It inserts a SQLite row in `governance_review_warnings`. It does not write a warning file. The tests are the only caller.
- `src` has no 14-day response on that function.

**Consequence:** Private warning, opportunity to correct behavior.

**Appeal:** `review_appeal` compares a caller-supplied integer with `APPEAL_OVERTURN_THRESHOLD` (5). It does not count a team of 7. Nothing calls it.

### Level 2: Public Warning

**Trigger:** Moderate violations, pattern of minor violations, or failure to correct after private warning.

**Process:**
- `issue_public_warning` compares `approvals.len()` with `PUBLIC_WARNING_THRESHOLD` (5). It does not count a team of 7. Nothing calls it.
- It stores a caller-supplied `warning_file_path`. `create_warning_file` returns a filename and does not write a file. `warnings/` contains `.gitkeep` only.
- It sets `improvement_deadline` to now plus `IMPROVEMENT_PERIOD_DAYS` (90). It does not set a 30-day response.

**Consequence:** Public warning, 90-day improvement period, potential restrictions.

**Appeal:** The overturn count is 5, not 6-of-7. `review_appeal` has no caller.

### Level 3: Removal

**Trigger:** Serious violations, failure to correct after warnings, or immediate security threat.

**Process:**
- `remove_maintainer` counts a caller-supplied list against `REMOVAL_TEAM_THRESHOLD` (6) and a caller-supplied team count against `REMOVAL_TEAMS_THRESHOLD` (4). It does not exclude the subject. The tests are the only caller.
- It does not read `RESPONSE_DEADLINE_DAYS`. It does not open a GitHub issue.
- It sets `active` to false. The HTTP routes do not publish that row.

**Consequence:** Removal from team, key deactivated.

**Appeal:** `submit_appeal` sets the deadline to the earlier of 60 days from submission and the case resolution deadline. Nothing calls it. `review_appeal` does not count teams.

---

## Procedures

### Reporting Governance Review Cases

**Who Can Report:**
- `/governance-review-case` returns an error unless the commenter is a registered maintainer. The subject must also be a registered maintainer.
- `src` has no contributor-report path and no community-report path.

**How to Report:**
- The command calls `create_case`, which inserts a SQLite row. The handler returns JSON.
- `create_case_issue` returns an error and has no caller. It does not open a GitHub issue.

**Protection for Reporters:**
- `report_retaliation` inserts a row with status `open`. `confirm_retaliation` sets `active` to false if the caller passes at least 4 ids. Nothing calls either function.
- `report_false_report` inserts a row with `sanction_applied` set to `none`. It does not warn or remove. Nothing calls it.
- `src` has no privacy check. The case row stores `reporter_maintainer_id`.

### On-Platform Review Process

1. **Report**: `/governance-review-case` calls `create_case`, which inserts a SQLite row. `create_case_issue` returns an error and has no caller.
2. **Initial Review**: The comment passes the caller's `severity` string. `issue_private_warning` counts a list against 4 and is called from tests. `remove_maintainer` counts a list against 6 and a team count against 4. Neither counts a team of 7.
3. **Response**: `create_case` sets `response_deadline` to now plus `RESPONSE_DEADLINE_DAYS` (30).
4. **Mediation**: `start_mediation` sets a deadline of `MEDIATION_PERIOD_DAYS` (30). Nothing calls it. The expired-check binary only calls `check_expired_mediations`.
5. **Evaluation**: `src` has no code-of-conduct string. `create_case` stores the caller-supplied `case_type` and `severity`.
6. **Sanction**: `issue_public_warning` has no caller. `remove_maintainer` is called from tests. Neither function reads `severity`.
7. **Appeal**: `submit_appeal` and `review_appeal` have no caller.

### Conflict Resolution/Mediation

**When Mediation Applies:**
- `start_mediation` takes a case id and an optional mediator id. It does not read the case type. Nothing calls it.

**Process:**
- It sets `mediation_deadline` to now plus `MEDIATION_PERIOD_DAYS` (30) and sets the case status to `mediation`.
- `resolve_mediation` sets the case status to `resolved`. It does not close a GitHub issue. Nothing calls it.
- `fail_mediation` sets the case status to `under_review`. The expired-check binary reaches it only through `check_expired_mediations`.

**Mediation Does NOT Apply To:**
- `start_mediation` does not reject a security case, an attack, a key compromise, or fraud. `src` has no fraud string.

### Time Limits

**Case Resolution:**
- `create_case` sets `resolution_deadline` to now plus `RESOLUTION_DEADLINE_DAYS` (180).
- `extend_time_limit` stores one `extension_approved_by` id and rejects a date past the original deadline plus `MAX_EXTENSION_DAYS` (90). It does not count a team. Nothing calls it.
- `get_tier_review_period` returns 7 for tier 1 and 0 for tier 4. That is not a 7-day emergency case limit.

**Appeals:**
- `submit_appeal` sets the deadline to the earlier of `APPEAL_DEADLINE_DAYS` (60) and the case resolution deadline. It is not 90 days.
- `extend_time_limit` does not count teams. Nothing calls it.

**Warnings:**
- `issue_public_warning` sets `improvement_deadline` to now plus `IMPROVEMENT_PERIOD_DAYS` (90). Nothing calls it.
- `IMPROVEMENT_EXTENSION_DAYS` is 30 and nothing reads it. `src` has no 4-of-7 extension count.

---

## Evaluation Criteria

### For All Review Cases

`create_case` stores the caller-supplied `case_type`, `severity`, `description`, and `evidence`. `src` has no pattern, impact, intent, or history check.

### Documentation Requirements

- `create_case` stores `evidence` in SQLite. `create_case_issue` returns an error and has no caller.
- `create_case` sets `response_deadline` to now plus `RESPONSE_DEADLINE_DAYS` (30). `notify_case_deadline` posts a comment only when `github_issue_number` is already set.
- The HTTP routes do not publish the case row.

---

## Safeguards

**Prevents Abuse:**
- `remove_maintainer` counts a caller-supplied list against 6 and a caller-supplied team count against 4. It does not read a prior warning. The tests are the only caller.
- `create_case` stores evidence in SQLite and sets a 30-day response deadline and a 180-day resolution deadline. The HTTP routes do not publish the row.
- `submit_appeal` sets a 60-day deadline and has no caller. `review_appeal` compares a caller-supplied integer with 5. That is not a higher team threshold.
- `start_mediation` has no caller. `remove_maintainer` does not call it.

**What This Prevents:**
- `src` has no vendetta string. `remove_maintainer` does not require evidence.
- `confirm_retaliation` and `report_false_report` have no caller. A false-report row stores `sanction_applied` as `none`.

**Protections:**
- `report_retaliation` inserts an open row. Nothing calls it.
- `src` has no privacy check. The case row stores `reporter_maintainer_id`.

---

## Emergency Removal

**Grounds:**
- `emergency_remove` stores the caller-supplied `reason` and writes `security_violation`. It does not classify key compromise, an attack, or fraud.
- `src/governance_review` has no attack string and no fraud string.

**Process:**
- It returns unless the caller passes at least 4 ids. It does not check that those ids are emergency keyholders, and it does not check a set of 5.
- Nothing calls it. `src` has no 7-day follow-up. `submit_appeal` has no caller.

**Definition of Gross Violations:**
- `malicious_code` is a `CASE_TYPES` name. `emergency_remove` does not read it.

**Not Gross Violations:**
- `emergency_remove` does not read the case type, so it does not reject a disagreement or a non-security case.

---

## Rehabilitation

`src` has no rehabilitation string and no reapplication path.

- `review_appeal` sets `active` to true when the caller passes `granted`. Nothing calls it. It does not wait 2 years, and it does not count a 6-of-7 team.
- `sign-pr` prints an `INSERT INTO maintainers` statement. It does not check a prior removal reason. `src` has no probation field.

---

## Relationship to Code of Conduct

`src` has no code-of-conduct string. This repository has no code-of-conduct file.

- `gross_misconduct` is a `SEVERITY_LEVELS` name. `/governance-review-case` stores the caller-supplied severity. It does not read a code of conduct.
- `issue_private_warning` is called from tests. The review-case command does not call `issue_public_warning` or `remove_maintainer`.

---

## Rationale

**Why Disregard Off-Platform Activity:**
- `create_case` returns if `on_platform` is false. `/governance-review-case` always passes `true`. It does not classify personal life.

**Why Graduated Sanctions:**
- `remove_maintainer` does not read a prior warning. `issue_public_warning` has no caller.
- `docs/governance-app-spec.md` has no graduated-sanctions string.

**Why Protections:**
- `report_retaliation`, `confirm_retaliation`, and `report_false_report` have no caller.

---

## Examples

### Valid On-Platform Review Cases

- `abuse`, `harassment`, `malicious_code`, `collusion`, and `technical_errors` are `CASE_TYPES` names. `create_case` stores the caller-supplied type.
- `issue_private_warning` is called from tests. `issue_public_warning` has no caller. `remove_maintainer` does not read the case type.
- `src/governance_review` has no six-month error count.

### Invalid Off-Platform (Disregarded)

- `create_case` returns if `on_platform` is false. `/governance-review-case` always passes `true`.
- `src` has no Twitter string, no social-media string, and no legal-dispute string. It does not classify those posts.

### False Reports and Retaliation

- `report_false_report` inserts a row with `sanction_applied` set to `none`. It does not issue a warning or remove a maintainer. Nothing calls it.
- `report_retaliation` inserts a row with status `open`. `confirm_retaliation` sets `active` to false if the caller passes at least 4 ids. Nothing calls either function.

---

## Implementation

### Grounds for Sanctions

`CASE_TYPES` in the governance app are: `abuse`, `harassment`, `malicious_code`, `collusion`, `conflict_of_interest`, `technical_errors`, `security_violation`, `false_report`, and `retaliation`. There is no `code_of_conduct` case type and no inactivity or six-month error-count string in `src`.

`remove_maintainer` returns unless the caller passes at least 6 team approver ids and a teams count of at least 4. It does not read `case_type`, severity, participation, or a code-of-conduct flag. Its only caller is a test.

### Normal Process

`/governance-review-case` requires the commenter and the subject to be registered maintainers, validates `case_type` and `severity` against those lists, and always passes `on_platform: true` into `create_case`. `create_case` rejects `on_platform == false` and sets 30-day response and 180-day resolution deadlines; it stores caller-supplied type, severity, description, and evidence. It does not choose a sanction level or run a graduated-sanctions workflow. `issue_private_warning`, `issue_public_warning`, and `remove_maintainer` are not called from the webhook path.

---

## References

- [Team Membership Criteria](TEAM_MEMBERSHIP_CRITERIA.md)
- [Code of Conduct](../../../.github/CODE_OF_CONDUCT.md)
- [Maintainer Guide](../../guides/MAINTAINER_GUIDE.md)
- [Governance App Spec](../../../governance-app-spec.md)
