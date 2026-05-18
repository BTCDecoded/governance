# Action tiers (PR classification)

**Machine-readable policy:** [`config/action-tiers.yml`](../config/action-tiers.yml) — review periods and maintainer signature thresholds for **governance tiers 1–5** on pull requests.

**Emergency response classes** are **not** defined here; use [`config/emergency-tiers.yml`](../config/emergency-tiers.yml) only.

**Tier 5 special process** (wider maintainer pool and emergency keyholders for governance-rule changes) is described in [`GOVERNANCE.md`](../GOVERNANCE.md), not in `action-tiers.yml`. The YAML tier_5_governance row covers routine numeric fields (e.g. 180-day review) used where the standard 5-of-5 maintainer pool applies.

**Published book:** [blvm-docs](https://github.com/BTCDecoded/blvm-docs) resolves `[[gov:…]]` placeholders from these YAML files at `mdbook build` time.

**Layer + tier combination:** see [`LAYER_TIER_MODEL.md`](../LAYER_TIER_MODEL.md) and [`config/repository-layers.yml`](../config/repository-layers.yml).
