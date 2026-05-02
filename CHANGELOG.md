# Changelog

All notable changes to LoopDuck are documented in this file.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).
Versions follow [Calendar Versioning](https://calver.org/) (YYYY.M.D).

---

## [Unreleased]

## [2026.5.2] - 2026-05-02

### Fixed
- **GitHub integration restored** — Settings → GitHub auth check, repo list, branches, issues, PRs, and workflow runs now work end-to-end. They had been silently failing inside the app: TLS handshakes panicked on a tokio worker thread while the main UI kept running, so the breakage was invisible without log inspection. `github_clone_repo` was unaffected (it shells to the system `git` CLI).
- **All in-app HTTPS paths** — same root cause affected any rustls-using path (OpenClaw chat gateway, websocket TLS, and Docker-over-TLS in some configurations).

### Changed
- Install rustls' default crypto provider (`aws_lc_rs`) at process startup via `CryptoProvider::install_default()`. Multiple TLS deps (`reqwest`, `octocrab`, `tokio-tungstenite`, `russh`, `bollard`) all pulled rustls 0.23 with conflicting/no provider features, so no provider was auto-selected. The call is wrapped in an explicit `match` so the "already installed" branch (the only error mode in rustls 0.23, e.g. on dev hot-reload) is a documented no-op, and any future rustls error variant surfaces via `stderr` at startup instead of being silently swallowed.

## [2026.4.22] - 2026-04-22

_(no detailed entries recorded — see <https://github.com/bemindlabs/LoopDuck-Application/pull/42> for the changes shipped in this release)_

## [2026.4.16] - 2026-04-16

### Added
- **AI activity indicator** — centered activity indicator in the header showing real-time AI processing status
- **Coding automation auto-seed** — AgentsSCRUM auto-seeds coding automation and surfaces failures to the UI
- **FIFO queue with parallel lanes** — coding workflow now supports queued execution with configurable parallel lanes
- **Pipeline timeline UI** — frontend timeline visualization and runs history page for pipeline executions
- **Unified pipeline store** — dual-emit legacy pipelines into unified execution store with AiGateway migration

### Fixed
- **Coding workflow persistence** — automation runs persisted correctly; tokens scrubbed from stored data; templates hydrated properly
- **Scrum workspace hint** — workspace hint propagated correctly; JSON-escape template values to prevent parse errors
- **Story status alignment** — board column statuses aligned with story statuses; Agents Council UX improvements
- **Automations form** — coding_workflow action type wired through the automation form UI
- **Clippy lint** — resolved doc-list-item lint warning in pipeline module

### Changed
- **Pipeline execution backbone** — unified execution model replacing fragmented per-module runners; migrated to AiGateway
- **Coding workflow tests** — restored mocks for resume-from-disk and pipeline IPC scenarios

## [2026.4.14] - 2026-04-14

### Added
- **Internal MCP** — in-process service registry with 11 providers exposing 41 tools for inter-module communication; external MCP bridge on `127.0.0.1:18790` for Claude Desktop, Cursor, and other AI agents
- **Automation engine** — scheduled task execution, cross-module bus-triggered automation chains, CronBuilder and ExecutionLogModal UI
- **Shared memory bridge** — injects relevant memory notes into SCRUM orchestrator and Chat system prompts
- **Group mentions in team chat** — `@all`, `@agents`, `@buddy` with autocomplete and inline highlighting
- **AgentsSCRUM session summary** — SessionSummaryPanel with story details, vote breakdown, discussion threads, and phase progress tracking
- **Council ↔ Workflow bridge** — dev task results written to session in real-time; auto-advance DevMode to Review on completion
- **AI generators** — AI-powered Epic, Story, and Backlog generation from natural language prompts
- **Biometric gate and lock screen** — backend secret access control, idle auto-lock, full-screen lock overlay with native biometric unlock
- **Launch Agent page** — agent launcher with CLI presets, workspace buddies, and A2A remote discovery
- **Tmux window operations** — create, rename, close, and switch tmux windows from the terminal UI
- **Settings danger zone** — reset all settings and clean data actions
- **10 new settings fields** — font family, font size, sidebar position, terminal shell, scrollback, default model, streaming, temperature, max tokens, idle timeout
- **Unified notification system** — process-wide notifications for AgentsSCRUM, Coding Workflow, SSH, GitHub, and Run All Stories
- **Session-lifetime secret cache** — OS keychain secrets cached for entire app session; single password prompt at startup

### Changed
- **Scrum board** — renamed Backlog to Plan, Deploy to Done
- **Gateway URL default** — changed from `localhost:3000` to `127.0.0.1:18789`
- **Settings** — sidebar grouped by scope (Project vs Global); reads/writes via config.json instead of only SQLite
- **AgentsSCRUM** — default model changed to `openclaw`; sessions persisted immediately; credential recovery from keychain on restart
- **Modernized UI** — agent cards with hover lift, StoryCard visual effects, dialog animations, landing page polish, Markdown rendering improvements

### Fixed
- **AgentsSCRUM** — consensus transitions, session persistence on restart, council epic loading, profile search paths
- **Chat** — workspace scoping, message persistence, stream delivery, stale response cancellation, group mention fan-out limiting
- **Generate Backlog** — prompt restructuring, retry logic, gateway error surfacing
- **Terminal** — agent window width, tmux session management
- **Config.json** — serialized writes to prevent corruption from concurrent saves
- **Wizard** — workspace context updated immediately on finish

## [2026.4.12] - 2026-04-12

### Changed
- **Remove bundled resource templates** — workspace init now only creates .LoopDuck directory structure
- **Rename DevCanvas Templates → Workspace Structure** in Settings
- **Wizard pre-populates existing settings** — all steps load saved values on mount
- **Gitignore templates** — added "None (minimal)" option, .LoopDuck included in all templates
- **Standardize .LoopDuck casing** — added migration on case-sensitive filesystems

### Fixed
- **PR #38 review comments** — 12 findings addressed: security (redact raw AI response), stale closures, z-index consistency, React key stability, scrum path mismatch, secret cache TTL
- **Release workflow** — tag-vs-config version validation; upgraded action-gh-release v2 → v3

## [2026.4.11] - 2026-04-12

### Added
- **Agents SCRUM** — AI council of 3–9 specialist agents with 8-phase deliberation pipeline: Intake → Decomposition → Refinement → Estimation → Consensus → Dev Mode → Review → Retrospective
- **Orchestrator** — async phase chaining via OpenClaw AI gateway with prompt builders, response parsers, and real-time Tauri events
- **Dev Mode engine** — wave-based parallel story execution with git branch creation, test running, and bounded concurrency
- **Coding workflow** — AI-powered multi-step plan generation, step editor, workflow persistence
- **~/.LoopDuck Application Home Directory** — global config.json, profile.md, cross-workspace memory graph, global agent profiles, template resolution, MCP server registry
- **Workspace-scoped data isolation** — `.LoopDuck/` directory per workspace for scrum, agents, chat, automations, MCP
- **Settings page redesign** — 17 modular section components, `useConfig()` reactive hook, auto-save
- **Setup Wizard** expanded to 6 steps — workspace directory, scrum process configuration
- **Splash screen** — branded splash with dark/light theme awareness
- **16 new test files** for previously untested modules

### Changed
- **HTTP connection pooling** — single static `reqwest::Client` via `OnceLock` (~3s saved per workflow)
- **SQLite connection pooling** — single shared connection via `OnceLock<Mutex<Connection>>`
- **Config cache** — 5-minute TTL with invalidation on write
- **settings.db deprecated** — config.json first, SQLite fallback for unmigrated keys
- **Dependency upgrades** — Vite 8, React 19.2, React Router 7.14, rusqlite 0.39, russh 0.60, git2 0.20

### Fixed
- Scrum board showing all projects across workspaces instead of filtering
- Settings invoke timeout — added HTTP timeouts and increased IPC tolerance
- Windows icon — converted icon.ico to proper ICO format
- CI disk space — resolved exhaustion during `cargo test`

## [2026.4.10] - 2026-04-10

### Added
- **Coding Workflow recovery** — `workflow_recovery.rs` detects interrupted workflows and offers resume/discard
- **Workspace rules** — `.LoopDuck/rules.md` read at startup for workspace-specific AI behavior

### Changed
- **Coding workflow persistence** — workflow state saved to disk after each step for crash recovery
- **Terminal shell detection** — reads user's default shell from system instead of hardcoding bash

### Fixed
- **Coding workflow** — step execution order preserved; file conflicts resolved before applying edits
- **Chat DB** — messages persisted to correct workspace-scoped database path

## [2026.4.8] - 2026-04-08

### Added
- **iOS Tauri app** — full Tauri v2 iOS support with edge-to-edge WebView, safe area handling
- **Mobile responsive layout** — CSS `min()` fallbacks, `sm:` breakpoints, responsive Kanban
- **Mobile sidebar UX** — slide animation, swipe gestures, haptic feedback, 44px touch targets
- **AskAI mobile overlay** — full-screen slide-up panel on phones; desktop side panel unchanged
- **Shared Xcode workspace** for iOS + watchOS projects
- **Dynamic app version** — `getAppVersion()` falls back to Tauri API on iOS

### Changed
- **App icons** regenerated from `loopduck-mascot.svg` for all platforms
- **ChatPage** sidebar becomes full-screen overlay on mobile
- **SettingsPage** — SSH and GitHub sections hidden on iOS
- **Viewport meta** — removed `user-scalable=no` for accessibility

### Fixed
- **Bottom space on iOS** — disabled WKWebView automatic safe area inset via Rust `objc2` FFI
- **Release build** — guarded `open_devtools()` behind `#[cfg(debug_assertions)]`
- **CI disk space** — resolved exhaustion during `cargo test`

### Removed
- **Native iOS app** (`mobile/ios/`) — replaced by Tauri iOS app

## [2026.4.6] - 2026-04-06

### Fixed
- **Release workflow** — macOS builds failing with keychain errors; moved secret checks into shell guards
- **Code signing gate** — env vars only exported when `APPLE_CERTIFICATE` is configured
- **Notarization verification** — same condition fix applied

## [2026.4.4] - 2026-04-03

### Changed
- **ESLint** — stricter TypeScript rules, `eslint-plugin-unused-imports`, refactors
- **CI / Release** — pinned actions, macOS signing fix, publish step improvements

### Fixed
- **Scrum** backlog generation session key; **Landing** GitHub repo load cancellation
- **Rust** Clippy warnings in `device_identity` and `openclaw` tests

## [2026.4.3] - 2026-04-03

### Added
- **Skills Browser** — browse and install OpenClaw skills
- **Plugin management** UI — enable/disable gateway plugins
- **Doctor** — OpenClaw gateway diagnostics and auto-fix
- **Model switcher** — list and select AI models in the Ask AI panel
- **Agents** — multi-select, bulk quick actions, drag-to-reorder cards
- **Git worktrees** — backend commands and Git page list/status
- **Workspace quick switcher** in header with context provider
- **Tmux** session mode, session picker, kill/destroy tmux session
- **Ask AI** — multi-turn context, workspace-aware system prompt, persisted chat history
- **Scrum board** — Local vs Jira data source toggle, workspace-scoped project isolation
- **Landing** — GitHub clone dialog with repo dropdown + URL parsing
- **Release / quality** infrastructure — production build pipeline, Vitest coverage expansion

### Changed
- **DLC** product surface removed — page, module, Tauri commands, and shortcut references
- **App menu** — Terminal first under Development; GitHub entry added

### Fixed
- Gateway integration regressions
- macOS Edit menu — native clipboard support (Cmd+C/V)
- Gateway URL normalization and clearer HTTP error messages

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

## [0.1.3] - 2026-03-31

### Added
- Quality gates: pre-commit (`cargo check`) and pre-push (`tsc` + `vite build` + `cargo test`)
- CI: `cargo clippy`, `cargo fmt --check`, ESLint, and Prettier checks
- Homebrew Cask distribution (`brew install --cask bemindlabs/loopduck/loopduck`)

## [0.1.2] - 2026-03-31

### Changed
- **Rebrand:** Renamed from DevCanvas / AI-DLC to LoopDuck across all surfaces (Tauri config, Cargo.toml, package.json, UI text, agent card, workflows)

## [0.1.1] - 2026-03-31

### Changed
- Version bump across package.json, Cargo.toml, Cargo.lock, and tauri.conf.json

## [0.1.0] - 2026-03-28

Initial public release of LoopDuck — AI Coding workflow desktop app built with Tauri v2 + React 19.

---

[2026.4.14]: https://github.com/bemindlabs/loopduck-releases/releases/tag/v2026.4.14
[2026.4.12]: https://github.com/bemindlabs/loopduck-releases/releases/tag/v2026.4.12
[2026.4.11]: https://github.com/bemindlabs/loopduck-releases/releases/tag/v2026.4.11
[2026.4.10]: https://github.com/bemindlabs/loopduck-releases/releases/tag/v2026.4.10
[2026.4.8]: https://github.com/bemindlabs/loopduck-releases/releases/tag/v2026.4.8
[2026.4.6]: https://github.com/bemindlabs/loopduck-releases/releases/tag/v2026.4.6
[2026.4.4]: https://github.com/bemindlabs/loopduck-releases/releases/tag/v2026.4.4
[2026.4.3]: https://github.com/bemindlabs/loopduck-releases/releases/tag/v2026.4.3
[2026.4.2]: https://github.com/bemindlabs/loopduck-releases/releases/tag/v2026.4.2
[0.1.4]: https://github.com/bemindlabs/loopduck-releases/releases/tag/v0.1.4
[0.1.3]: https://github.com/bemindlabs/loopduck-releases/releases/tag/v0.1.3
[0.1.2]: https://github.com/bemindlabs/loopduck-releases/releases/tag/v0.1.2
[0.1.1]: https://github.com/bemindlabs/loopduck-releases/releases/tag/v0.1.1
[0.1.0]: https://github.com/bemindlabs/loopduck-releases/releases/tag/v0.1.0
