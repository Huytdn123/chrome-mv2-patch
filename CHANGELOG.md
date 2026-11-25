# Changelog

## [1.17.0] - 2026-11-25

- **Autoscan Engine (`secur32.dll`)**: Integrated dynamic structural MV2 gate recognition for Chrome, Chromium, and Microsoft Edge (versions 151–160+, x64/x86/ARM64) without requiring `signatures.json` on Windows.
- **Off-Store CRX & InstallVerifier Support**: Automatically unlocks off-store MV2 extensions (including uBlock Origin) and CRX installation checks in memory.
- **DPAPI WirePlan Cache + `rundll32.exe` Self-Helper**: Sub-second startup on cached launches; zero separate CLI executable needed.
- **Zero Renderer Crashes (`STATUS_INVALID_IMAGE_HASH`)**: Child processes only forward standard `secur32.dll` exports.
- **One-Liner Upgrade (`chrome-mv2.ps1`)**: Preserves the `irm | iex` workflow, auto-cleans legacy `version.dll` from v1.16.x, and supports Chrome, Edge, and Chromium.

## [1.16.1] - 2026-11-23

- **Intelligent Signature & Fingerprint Verification**: Pre-flight PE analysis, milestone gate resolution, and comprehensive diagnostics (`Invoke-Check`).
- **Fail-Closed Safety**: Automatic abort if gate match is incomplete or if an Authenticode hash mismatch is detected, preventing unstable browser state.
- **Smart Cache (Schema v2)**: Instantaneous repeat checks with 64-character SHA-256 validation; enforces fresh rescan on install.
- **Authenticode Signature Verification**: True signature status validation (`Valid`, `NotSigned`, `HashMismatch`, `NotTrusted`, `Unknown`) via `Get-AuthenticodeSignature`.
- **PE Parser Bounds Checking**: Robust bounds validation for DOS header, `e_lfanew`, NT headers, machine type, optional headers, and section tables.
- **Enterprise Policy Preservation**: Replaced destructive policy deletion with read-only audit (`Get-ChromePolicyStatus`, `Audit-ChromePolicies`), preserving organization registry settings.

## [1.16.0] - 2026-11-07

- Chrome 159 support.
- New instruction forms require an updated patcher.

## [1.15.0] - 2026-10-23

- Chrome 158 support.
- Fix Windows 157 x86.

## [1.14.0] - 2026-10-05

- Chrome 157 support.

## [1.13.0] - 2026-09-16

- Chrome 156 support.

## [1.12.0] - 2026-09-11

- chrome-mv2.ps1 switch from byte-patching to version.dll.

## [1.11.1] - 2026-09-11

- Fix 154.

## [1.11.0] - 2026-09-11

- Enable webRequestBlocking MV3.
- Drop Chromium support.

## [1.10.1] - 2026-09-09

- Fix macOS signatures.
- Fix Windows 154 signatures.

## [1.10.0] - 2026-09-07

- Drop 151 support, macos-x64.
- New ARM cbz based patch.

## [1.8.0] - 2026-09-05

- Enable webRequestBlocking MV3.
- Enable ExtensionSettings policy.

## [1.7.0] - 2026-09-02

- Chrome 155 support.
- Bug fixes.
- Python scripts updated.

## [1.6.1] - 2026-08-29

- New menu UI.

## [1.6.0] - 2026-08-23

- Chrome 154 support.

## [1.5.1] - 2026-08-21

- Windows script bug fixes.

## [1.5.0] - 2026-08-15

- Chromium support.

## [1.4.0] - 2026-08-14

- Linux ARM (arm64) support.

## [1.3.0] - 2026-08-13

- macOS x64, ARM support.
- Windows ARM support.

## [1.2.0] - 2026-08-12

- Linux support.
- Windows x86 support.
- Migrated from a binary to scripts.

## [1.1.0] - 2026-08-09

- Chrome 152 support.
- Windows x64 support.

## [1.0.0] - 2026-08-07

- First public release. 
- Windows x64 support.
- Chrome 151 support.
