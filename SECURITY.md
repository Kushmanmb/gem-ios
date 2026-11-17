# Security Policy — Kushmanmb/gem-ios

This repository is an independently maintained fork of [Gem Wallet's archived iOS repository](https://github.com/gemwalletcom/gem-ios). Official Gem Wallet development moved to [gemwalletcom/wallet](https://github.com/gemwalletcom/wallet). Security claims, third-party audits, and support contacts for the official application must not be assumed to cover this fork.

## Reporting a vulnerability

Do **not** submit seed phrases, private keys, API secrets, wallet recovery material, or live customer data in issues, PRs, screenshots, or logs.

If GitHub private vulnerability reporting is enabled on this repository, use **Security → Advisories → Report a vulnerability** to contact this fork's maintainers confidentially. Otherwise contact the repository owner privately before disclosing reproducible exploit details; do not open a public issue containing an exploitable proof of concept.

Vulnerabilities in the official Gem Wallet product should be reported through [the upstream security policy](https://github.com/gemwalletcom/wallet/security/policy), not assumed to be handled by this fork.

Please include the affected commit, dependency or code path, impact, reproduction steps using disposable test wallets, and a suggested remediation where available. Never include real wallet secrets.

## Review scope

Priority areas include key generation and storage; seed phrase import/export and recovery; biometric access; transaction signing and chain-ID validation; WalletConnect requests; deep links; RPC and network trust boundaries; third-party dependencies; and the pinned Rust `core` submodule.

## Automated checks and limitations

- macOS CI builds and runs iOS unit tests on the default branch.
- MobSF static analysis checks Swift and Objective-C source patterns.
- OSV-Scanner checks recursive Swift dependency lockfiles and the checked-out Rust submodule on PRs and on a scheduled full scan.
- Dependabot proposes updates for GitHub Actions, the git submodule, and nested Swift packages.

These automated checks do **not** constitute an independent cryptographic audit, guarantee zero vulnerabilities, or certify production readiness. Security findings require investigation and testing before shipping any wallet build.
