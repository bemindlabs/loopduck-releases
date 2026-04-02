# Changelog

All notable changes to LoopDuck are documented in this file.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).
Versions follow [Calendar Versioning](https://calver.org/) (YYYY.M.D).

---

## [2026.4.2] - 2026-04-02 — Developer Preview

### Added
- **Team Chat** — BLE mesh routing, persistence, and transport manager
- **Agent memory system** with OpenClaw mascot component and QA-tester agent
- **Dev task system** with agents working view and workspace rules
- **Session management** — kill session command and backlog session reuse
- **Auto-update checker** with GitHub releases integration
- **Focus mode** toggle (Cmd+Shift+F) via command palette
- **Native Edit menu** and improved Help menu with clipboard key handlers
- **Embedded browser** in main window using Tauri multi-webview
- **Jira bidirectional sync** — migrated to Jira API v3 search/jql
- **FilePreview** expanded format support and improved UX
- **File logger** and improved OpenClaw error messages
- **Playwright e2e** test setup
- Homebrew cask auto-update step in release workflow
- Mirror release assets to public `bemindlabs/loopduck-releases` repo

### Changed
- **Versioning switched from SemVer to CalVer** (YYYY.M.D) — aligned with OpenClaw release strategy
- Extracted reusable Select UI component, replaced all native `<select>` elements
- Merged READ mode into DOCS mode (distraction-free reading)
- Renamed `.devcanvas` to `.loopduck` across backend and frontend
- Updated icons, configs, app pages, and project tooling
- Coverage thresholds updated to match current coverage levels

### Fixed
- PTY session now stays alive after command completes
- AskAI panel resize stale closure and widened grab target
- Browser page navigation, XSS protection, and backend cleanup
- Clippy warnings: added Default impl and used `clamp()`
- Ref updates moved to `useEffect` to satisfy react-hooks/refs lint
- Gated `chrono::Utc` import behind BLE platform cfg for CI
- ESLint warnings and Prettier formatting across codebase

## [0.1.4] - 2026-04-01

### Added
- CLAUDE.md for Claude Code context
- Mac App Store distribution with signed .pkg and entitlements
- App Store upload script (`scripts/appstore-upload.sh`)
- App Store button on website product page and get-started page
- macOS Xcode project with full icon set (iOS + macOS)
- Claude Code hooks for type-checking, pre-commit, pre-push, and version sync
- Cross-platform builds: macOS aarch64 + x64 DMGs, Windows, Linux via CI

### Changed
- Comprehensive README with feature tables, architecture map, and install options
- Switched direct distribution from .pkg back to .dmg (standard macOS UX)
- Homebrew cask includes `postflight` xattr fix for Gatekeeper

### Fixed
- TypeScript strict mode fixes
- Keychain error handling for Linux CI
- SSH agent gated behind `#[cfg(unix)]` for Windows build compatibility
- Release workflow permissions and Linux CI dependencies

## [0.1.0] - 2026-03-28

Initial public release of LoopDuck — AI Coding workflow desktop app built with Tauri v2 + React 19.

---

[2026.4.2]: https://github.com/bemindlabs/loopduck-releases/releases/tag/v2026.4.2
[0.1.4]: https://github.com/bemindlabs/loopduck-releases/releases/tag/v0.1.4
[0.1.0]: https://github.com/bemindlabs/loopduck-releases/releases/tag/v0.1.0
