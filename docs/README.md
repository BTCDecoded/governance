# Governance documentation

| Document | Purpose |
|----------|---------|
| [ACTION_TIERS.md](./ACTION_TIERS.md) | PR action tiers 1–5 (`config/action-tiers.yml`) |
| [../LAYER_TIER_MODEL.md](../LAYER_TIER_MODEL.md) | Layer + tier combination (source narrative) |
| [../GOVERNANCE.md](../GOVERNANCE.md) | Full governance model (Tier 5 special process, emergency keyholders) |
| [../config/README.md](../config/README.md) | YAML config index |

**Machine-readable policy** lives under `config/*.yml`. The [blvm-docs](https://github.com/BTCDecoded/blvm-docs) site expands `[[gov:KEY]]` from those files at build time; edit YAML here, not duplicated numbers in the book.

**Emergency classes** are only in `config/emergency-tiers.yml` (not in `action-tiers.yml`).
