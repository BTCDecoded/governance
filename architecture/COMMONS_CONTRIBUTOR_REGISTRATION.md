# Commons Contributor Registration

## Current model

**Commons contributor metrics are not a substitute for maintainer merge policy.** Repository governance is **maintainer multisig + tiers + review periods** only.

Optional **contribution metrics** (merge mining, fee forwarding, zaps, marketplace, etc.) may still be tracked for **reporting, grants, or community visibility**. Those metrics are **orthogonal** to whether a PR may merge.

## Configuration reference

Human-readable thresholds for contribution types (in BTC) may be recorded in:

- `governance/config/commons-contributor-thresholds.yml`

That file is a **reference** for maintainers and tooling; it does **not** add an extra merge gate unless you implement and ship new enforcement explicitly.

## Operational checklist

1. **Merges**: Use governance signing and tier rules only.
2. **Contributions**: If you record them, keep accounting separate from merge authorization unless product requirements change.
3. **Docs**: Point contributors to [GOVERNANCE.md](../GOVERNANCE.md) and the maintainer guide for process.
