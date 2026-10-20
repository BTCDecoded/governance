# Team Membership Approval and Revocation Criteria

## Overview

Team membership is not a 7-by-7 roster. `get_tier_requirements` returns `(4, 5)` for tier 1, `(5, 6)` for tier 2, `(6, 6)` for tier 3, `(5, 5)` for tier 4, and `(7, 6)` for tier 5. Those numbers are teams required and signatures required per team. `maintainers/teams.yml` is not in this repository, so `load_teams_for_nested_multisig` returns an empty list.

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

**Duration**: The source has no probation period. `/governance-sign` verifies a signature for a registered maintainer. It does not check a 90-day probation flag.

**Requirements During Probation:**
- `src` has no probation field, so there is no demonstration list, team review, or early termination.
- The 4-count is `PRIVATE_WARNING_THRESHOLD`. `issue_private_warning` compares it with a caller-supplied list. That is not probation feedback.
- `IMPROVEMENT_EXTENSION_DAYS` is 30 and has no caller.

### 1.3 Approval Process

There is no team-approval step for a new maintainer. `maintainers/teams.yml` is not in this repository. `sign-pr` prints an `INSERT INTO maintainers` statement. The 6 and 4 counts are `REMOVAL_TEAM_THRESHOLD` and `REMOVAL_TEAMS_THRESHOLD`. `ConfigCache::reload` has no caller.

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

The source has no voluntary-exit path. `src` has no notice period and no 3-of-7 count. `maintainers/teams.yml` is not in this repository. `handle_pr_merged` does not deactivate a key. `src` has no emeritus string.

### 2.2 Performance-Based Removal

**Grounds for Removal:**
1. **Inactivity**: The source has no inactivity check. `remove_maintainer` does not read participation. The 0.20 figure is `mining_pool_weight_cap` in the Growth phase. `RESOLUTION_DEADLINE_DAYS` is 180 for a review case, not a participation window.
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
- The 4-count is `issue_private_warning`, which inserts a SQLite row and is called from tests. It does not write `governance/warnings/`.
- `issue_public_warning` requires 5 caller-supplied ids and sets `IMPROVEMENT_PERIOD_DAYS` (90). Nothing calls it.
- `create_warning_file` returns a filename and does not write a file. Nothing calls it. `warnings/` contains `.gitkeep` only.

**Step 4: Removal Vote**
- `maintainers/teams.yml` is not in this repository.
- `remove_maintainer` counts a caller-supplied list against `REMOVAL_TEAM_THRESHOLD` (6) and a caller-supplied team count against `REMOVAL_TEAMS_THRESHOLD` (4). It does not exclude the subject.
- The tests are the only caller.

**Step 5: Appeal Period**
- `submit_appeal` and `review_appeal` have no caller. The expired-check binary only calls `check_expired_appeals`.
- The unused `submit_appeal` sets the deadline to the earlier of 60 days from submission and the case resolution deadline. It does not start 60 days after removal.
- The unused `review_appeal` compares a caller-supplied integer with `APPEAL_OVERTURN_THRESHOLD` (5). It does not count teams.

**Step 6: Final Removal**
- `handle_pr_merged` does not set `active` to false.
- `remove_maintainer` sets `active` to false and is called from tests.
- `deactivate_maintainer` is called only from `emergency_remove` in the same file.

### 2.3 Emergency Removal

**Grounds:**
- Key compromise (immediate security risk)
- Gross violations **on-platform** (immediate security threat, active attack, ongoing fraud)
- Network-threatening actions

**Process:**
- `emergency_remove` returns unless the caller passes at least 4 ids. It does not check that those ids are emergency keyholders, and it does not check a set of 5.
- Nothing in `src/webhooks`, `src/main.rs`, or the tests calls `emergency_remove`.
- `src` has no 7-day follow-up. `submit_appeal` has no caller.

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
- `src` has no transfer path. `Maintainer` stores `layer` and `active`. It does not store a team.
- `maintainers/teams.yml` is not in this repository.

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
- `KeyType::Maintainer` expires after 180 days, not 2 years. `KeyType::Emergency` expires after 90 days.
- `rotate_key` takes a key id and an optional owner. It does not take a team-approval count. `src` has no 3-of-7 count.
- `maintainers/teams.yml` is not in this repository. `rotate_key` runs only from the `key_manager` binary. A maintainer key update writes the new public key into `maintainers`.

**Emergency Rotation:**
- `rotate_key` does not check emergency keyholders. `emergency_remove` counts caller-supplied ids and has no caller. It does not rotate a key.

### 4.3 Key Loss

**Process:**
- `src` has no key-loss path and no social-recovery path.
- `key_manager` can `Generate`, `Rotate`, or `Revoke` a key. Those commands do not take a team-approval count.
- The 5-counts in source are `PUBLIC_WARNING_THRESHOLD` and `APPEAL_OVERTURN_THRESHOLD`. `emergency_remove` has no caller.

---

## Part 5: Team Composition Requirements

### 5.1 Diversity Requirements

**Geographic Distribution:**
- `Maintainer` has no jurisdiction field. `src` has no 30% team cap and no key-ceremony path.
- `operator.jurisdiction` is a non-empty string on a server record. The check rejects an empty string. It does not count jurisdictions on a team.

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

**Minimum Team Size**: `Maintainer` has no team field. `src` has no team-size, expansion, or merger path.
**Maximum Team Size**: There is no maximum of 7. `maintainers/teams.yml` is not in this repository.
**Team Expansion**: `src` has no expansion approval. The 5-counts are `PUBLIC_WARNING_THRESHOLD` and `APPEAL_OVERTURN_THRESHOLD`.
**Team Reduction**: `src` has no 90-day recruiting rule and no merger vote. `IMPROVEMENT_PERIOD_DAYS` is 90 on `issue_public_warning`, which has no caller.

---

## Part 6: Approval Thresholds Summary

These rows are not separate votes in the source.

- Adding a maintainer: `sign-pr` prints an `INSERT INTO maintainers` statement. `src` has no 6-of-7 team vote and no 49% consensus check.
- Removing a maintainer: `remove_maintainer` counts a caller-supplied list against `REMOVAL_TEAM_THRESHOLD` (6) and a caller-supplied team count against `REMOVAL_TEAMS_THRESHOLD` (4). It does not exclude the subject. The tests are the only caller. `src` has no 3-of-7 count.
- Emergency removal: `emergency_remove` returns unless the caller passes at least 4 ids. Nothing in `src/webhooks`, `src/main.rs`, or the tests calls it.
- Team transfer: `src` has no transfer path.
- Key rotation: `rotate_key` runs from the `key_manager` binary and does not take a team-approval count. `src` has no 3-of-7 count.

---

## Part 7: Transparency and Accountability

### 7.1 Public Documentation

**All Actions Publicly Documented:**
- `src` has no nomination string and no discussion string.
- A verified `/governance-sign` stores a row in `governance_events`. The HTTP routes do not publish that row.
- `remove_maintainer` sets `active` to false and is called from tests. It does not open a pull request.
- `warnings/` contains `.gitkeep` only. `create_warning_file` returns a filename and has no caller.
- `submit_appeal` inserts a SQLite row and has no caller.

### 7.2 Audit Trail

**Cryptographic Proof:**
- A `pull_request_review` is stored by `handle_review_event` with the GitHub review state. That handler does not verify a signature.
- The webhook verifies a signature with the public key stored for that maintainer. The HTTP routes do not publish that key or a verification result. `sign-pr verify` checks a signature only when the caller passes a local public-key file.
- The audit logger appends a local JSONL file and links each entry to the previous hash. `rotate` renames that file. The module comment says the log is tamper-evident.
- `stamp()` writes a `MOCK_OTS_PROOF` string. `OtsConfig::default` sets `enabled: false`.

### 7.3 Community Oversight

**Public Comment Periods:**
- There is no nomination comment period in the source. `/governance-review-case` sets a 30-day response deadline on a case about an existing maintainer.
- 30-day response period for removal concerns
- Community can raise issues
- Journalists can report on patterns

---

## Part 8: Special Cases

### 8.1 Emeritus Status

The source has no emeritus status. `Maintainer` stores `active`. There is no `maintainers/emeritus.yml`. `/governance-sign` does not check an emeritus role.

### 8.2 Temporary Leave

The source has no temporary-leave status. `load_teams_for_nested_multisig` returns an empty list when `maintainers/teams.yml` is missing, and the loaded maintainer record keeps `github` and `public_key`. It does not read `on_leave` or a 180-day limit.

---

## Part 9: Implementation Notes

### 9.1 Governance App Integration

**Automated Checks:**
- Does not verify team approval thresholds. The pull-request webhook counts stored signatures with `check_signatures` against `get_combined_requirements`. `verify_nested_multisig` is reached only from `verify_multisig_threshold`, which the tests call.
- Does not track probation. `src` has no probation field. `Maintainer` stores `github_username`, `public_key`, `layer`, and `active`.
- Does not measure participation. `update_participation_weights` stores `0.0` for the contribution and both weights. The pull-request webhook does not read them.
- Does not enforce a key-rotation schedule. `auto_rotation` is never read, `key_manager` starts with an empty `rotation_policies` list, and `rotate_key` runs only from that binary. The timer in `src/main.rs` rotates the audit log file.

**Manual Override:**
- The pull-request path passes `emergency_mode: false`. It does not ask an emergency keyholder.
- `emergency_remove` returns unless the caller passes at least 4 ids. Nothing in `src/webhooks`, `src/main.rs`, or the tests calls it.
- That function would insert a SQLite row. It does not publish the row. `NostrConfig::default` and `config/app.toml` both set Nostr `enabled` to false.

### 9.2 Configuration Files

**Team Membership:**
- `maintainers/teams.yml` is not in this repository. `load_teams_for_nested_multisig` returns an empty list when that file is missing.
- `warnings/` contains `.gitkeep` only. `create_warning_file` returns a filename and does not write a file. Nothing calls it.
- There is no `maintainers/emeritus.yml`. `src` has no emeritus string.

**Changes Require:**
- PR to governance repository
- Appropriate approval thresholds
- The app does not reload after merge. `handle_pr_merged` calls `publish_merge_action`. `ConfigCache::reload` has no caller, and `ConfigCache` is never constructed outside `src/config/loader.rs`.

---

## Conclusion

Team membership follows a rigorous but fair process:

**Approval**: There is no team-approval threshold. `sign-pr` prints an `INSERT INTO maintainers` statement. The 6 and 4 counts are `REMOVAL_TEAM_THRESHOLD` and `REMOVAL_TEAMS_THRESHOLD`, and `remove_maintainer` is called from tests.
**Revocation**: `remove_maintainer` counts a caller-supplied list against `REMOVAL_TEAM_THRESHOLD` (6) and a caller-supplied team count against `REMOVAL_TEAMS_THRESHOLD` (4). It does not exclude the subject. The tests are the only caller.
**Transparency**: A verified `/governance-sign` stores a row in `governance_events`. The HTTP routes do not publish that row. The audit log default path is `/var/lib/governance/audit-log.jsonl`. `NostrConfig::default` and `config/app.toml` set Nostr `enabled` to false.
**Accountability**: Clear criteria and processes for all decisions

The nested multisig verifier does not decide team membership. `verify_nested_multisig` is reached only from `verify_multisig_threshold`, which the tests call. `maintainers/teams.yml` is absent, so `load_teams_for_nested_multisig` returns an empty list.

