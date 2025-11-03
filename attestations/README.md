# Release Attestations (Phase 1)

Store N-of-M maintainer signatures and verification artifacts per release.

Recommended layout:

- releases/
  - <release-set-id>/
    - VERIFY_BUNDLE_SHA256.txt
    - SOURCE_TAG.txt
    - SOURCE_TAG.txt.asc (PGP signatures, N-of-M)
    - BIN_HASHES.txt
    - BIN_HASHES.txt.asc (PGP signatures, N-of-M)
    - verify-artifacts.tar.gz
    - verify-artifacts.tar.gz.ots (OpenTimestamps receipt)

Process:
1. Create verification bundle from `consensus-proof/verify-artifacts/`.
2. Hash bundle and binaries; record in TXT files.
3. Collect N-of-M signatures.
4. Commit to this directory or attach to the GitHub Release.
