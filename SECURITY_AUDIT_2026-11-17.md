# Security and modernization baseline — 2026-11-17

Repository: `Kushmanmb/gem-ios` · target branch: `kushmanmb`

## Scope and verified facts

- The source tree contains **2,223 tracked blobs**, including **1,704 Swift files**, **40 Swift Package manifests**, and **32 committed `Package.resolved` lockfiles**.
- The `core` Rust blockchain engine is a Git submodule pinned to commit `e8b60d09aa9bd8fcfbc3534b56db8dbe564e8ca6`. Its own dependency inventory must be assessed from the checked-out submodule.
- Compared with archived `gemwalletcom/gem-ios:main`, this fork's `kushmanmb` branch is **10 commits ahead and 512 behind** at review time.
- The original `gemwalletcom/gem-ios` repository was archived in March 2026 and development moved to `gemwalletcom/wallet`. A direct merge is not a substitute for a migration plan.
- The prior `ci.yml` and `mobsfscan.yml` ran for `main`, but the fork's actual default branch is `kushmanmb`. This prevented normal default-branch push/PR triggers from providing the expected coverage.
- Prior Dependabot configuration used `/core` for a root-level Git submodule and `/` for Swift packages despite nested feature and package manifests; GitHub Actions dependencies were not configured.

## Changes in the security-hardening PR

- [x] Route automated macOS unit tests and MobSF PR checks to `kushmanmb`.
- [x] Set explicit read-only contents permission for unit-test workflow.
- [x] Configure Dependabot for GitHub Actions, root git submodule and nested Swift package manifests.
- [x] Add OSV-Scanner pull-request differential scan and weekly full scan, pinned to the reviewed `v2.7.1` workflow commit. Both check out the Rust submodule and recurse through lockfiles.
- [x] Correct fork links and distinguish this fork from the official Gem Wallet release.
- [x] Update the fork's vulnerability disclosure policy to avoid claiming inherited audits or compliance.

## Work remaining — not verified or fixed by this PR

- [ ] Review the new OSV SARIF results for all 32 Swift lockfiles and `core/Cargo.lock`; triage each real finding with an affected-version check and a tested remediation. No zero-vulnerability claim is made before these reports run.
- [ ] Run `just bootstrap`, `just build`, `just test-all`, and `just test-ui` on a supported Apple Silicon/macOS Xcode runner. Do not ship without successful wallet and Rust FFI integration tests.
- [ ] Run and review MobSF and GitHub Code Scanning results. Fix each actionable finding without broad rule suppression.
- [ ] Review key generation, encrypted storage, PIN/biometric boundaries, import/export/recovery, seed phrase handling, transaction signing, chain-ID and destination verification, WalletConnect approvals, deep links, RPC trust, and dependency supply chain.
- [ ] Test untrusted and oversized EVM call data, dynamic ABI argument presentation, and whether the confirmation screen clearly shows all security-relevant transaction details.
- [ ] Examine pinned `core` and its Cargo dependency health independently; never update signing or cryptographic code without regression tests.
- [ ] Plan migration/cherry-picks from the active `gemwalletcom/wallet` monorepo, preserving the fork's changes and license obligations. Do not blindly merge the 512 old upstream commits.
- [ ] Verify GitHub repository settings: branch protection on `kushmanmb`, required checks, private vulnerability reporting, secret scanning, and maintainer review.
- [ ] Review every Dependabot PR and re-run full CI before merging; automatic version bumps can break Swift and Rust ABI compatibility.

## Verification notes

This review is based on GitHub repository metadata, dependency manifests, workflows, representative Swift files, and source-tree inventory. A full source-code vulnerability audit, complete dependency advisory scan, end-to-end test run, external security assessment, and production release validation are **not yet complete**.

Automated scanner findings and successful CI are evidence, not guarantees of wallet safety. Never test against real seed phrases or assets.
