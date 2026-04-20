# Auto-Registration Integration Guide

## What this document is for

Optional **Commons contribution metrics** (merge mining, zaps, etc.) can be tracked for transparency or analytics. **Merge authorization** is **maintainer multisig, tier classification, and review periods** only (see `blvm-commons/src/validation/threshold.rs`, `tier_classification.rs`, and merge gating).

## If you track contributions

You may still record merge-mining, fee forwarding, zaps, or marketplace flows for **analytics, transparency, or grants**. That data:

- Does **not** replace maintainer signatures.
- Should not be wired to a second “automatic merge block” unless you add **new** explicitly reviewed code and policy.

## Configuration

`commons-contributor-thresholds.yml` in this repo describes **BTC-denominated contribution thresholds** for **documentation and optional reporting**. It does not override maintainer merge rules. Changes follow your normal governance process for config.

## Related docs

- [Maintainer Guide](../guides/MAINTAINER_GUIDE.md)
- [Commons contributor thresholds](../config/commons-contributor-thresholds.yml) (numeric reference only)
