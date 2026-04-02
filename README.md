# LoopDuck

**The Way of the Duck** — knowledgeable in a broad field, with no limitations.

LoopDuck is an AI-powered development workspace built with Tauri v2. It brings scrum boards, terminal management, Git, GitHub, Docker, AI agents, and AI chat into a single native desktop app for macOS, Windows, and Linux.

[![Latest Release](https://img.shields.io/github/v/release/bemindlabs/loopduck-releases?label=download&style=for-the-badge)](https://github.com/bemindlabs/loopduck-releases/releases/latest)
[![Mac App Store](https://img.shields.io/badge/Mac_App_Store-0D96F6?logo=apple&logoColor=white)](https://apps.apple.com/app/loopduck/id6744428938)
[![Homebrew](https://img.shields.io/badge/Homebrew-FBB040?logo=homebrew&logoColor=black)](https://github.com/bemindlabs/homebrew-loopduck)
[![Website](https://img.shields.io/badge/Website-buildonclaw.cloud-818cf8)](https://buildonclaw.cloud/products/loopduck)

## Download

### Mac App Store

[![Download on the Mac App Store](https://developer.apple.com/assets/elements/badges/download-on-the-app-store.svg)](https://apps.apple.com/app/loopduck/id6744428938)

### Homebrew (macOS)

```bash
brew install --cask bemindlabs/loopduck/loopduck
```

### Direct Download

| Platform | File | Install |
|----------|------|---------|
| **macOS** (Apple Silicon) | [`.dmg`](https://github.com/bemindlabs/loopduck-releases/releases/latest/download/LoopDuck_2026.4.2_aarch64.dmg) | Open DMG, drag to Applications |
| **macOS** (Intel) | [`.dmg`](https://github.com/bemindlabs/loopduck-releases/releases/latest/download/LoopDuck_2026.4.2_x64.dmg) | Open DMG, drag to Applications |
| **Windows** | [`.exe`](https://github.com/bemindlabs/loopduck-releases/releases/latest/download/LoopDuck_2026.4.2_x64-setup.exe) | Run installer |
| **Windows** (MSI) | [`.msi`](https://github.com/bemindlabs/loopduck-releases/releases/latest/download/LoopDuck_2026.4.2_x64_en-US.msi) | Run installer |
| **Linux** (Debian/Ubuntu) | [`.deb`](https://github.com/bemindlabs/loopduck-releases/releases/latest/download/LoopDuck_2026.4.2_amd64.deb) | `sudo dpkg -i LoopDuck_*.deb` |
| **Linux** (Fedora/RHEL) | [`.rpm`](https://github.com/bemindlabs/loopduck-releases/releases/latest/download/LoopDuck-2026.4.2-1.x86_64.rpm) | `sudo rpm -i LoopDuck_*.rpm` |
| **Linux** (AppImage) | [`.AppImage`](https://github.com/bemindlabs/loopduck-releases/releases/latest/download/LoopDuck_2026.4.2_amd64.AppImage) | `chmod +x LoopDuck_*.AppImage && ./LoopDuck_*.AppImage` |

Or browse all versions on the [Releases](https://github.com/bemindlabs/loopduck-releases/releases) page.

## Features

| Feature | Description |
|---------|-------------|
| **AI Chat** | OpenClaw gateway integration with streaming responses and multi-session support |
| **AI Agents** | Launch, manage, and communicate with AI agents via A2A protocol |
| **Agent Memory** | Persistent agent memory system with task tracking |
| **Scrum Board** | Sprints, stories, kanban board, burndown and velocity charts, sprint planning |
| **DLC Stepper** | AI-Driven Development Life Cycle phase tracking |
| **Terminal** | Tabs, split panes, PTY support, clipboard handlers, and configurable shells |
| **Git** | Branch management, staging, commits, diff viewer, and worktrees |
| **GitHub** | Browse repos, issues, pull requests, and create PRs directly |
| **Docker** | Container and image management, compose stacks, logs, and deployment |
| **File Manager** | Tree view, file preview (code, images, markdown), and editing |
| **Embedded Browser** | In-app browser via Tauri multi-webview |
| **Jira** | Bidirectional sync between local scrum board and Jira Cloud (API v3) |
| **SSH/SFTP** | Remote server connections, terminal sessions, and file transfer |
| **Team Chat** | BLE mesh routing, LAN peer-to-peer, and persistent messaging |
| **MCP** | Model Context Protocol server integration with SSE transport |
| **Auto-Update** | Automatic update checker with GitHub releases integration |
| **Focus Mode** | Distraction-free mode toggle (Cmd+Shift+F) |
| **Command Palette** | Quick actions via Cmd+K with customizable keyboard shortcuts |
| **Biometric Auth** | Touch ID / system biometric authentication for sensitive operations |
| **Telegram** | Telegram bot notifications |
| **Automations** | Templates and workflows for common development tasks |

## Tech Stack

| Layer | Technology |
|-------|-----------|
| **Frontend** | React 19, TypeScript, Tailwind CSS v4, Vite |
| **Backend** | Rust, Tauri v2 |
| **Database** | SQLite (bundled via rusqlite) |
| **AI** | OpenClaw gateway (WebSocket + REST) |
| **Auth** | System keychain (macOS Keychain, Windows Credential Manager, Linux Secret Service) |
| **Terminal** | portable-pty, xterm.js (WebGL) |
| **SSH** | russh, russh-sftp |
| **Git** | git2 (libgit2) |
| **Docker** | bollard (Docker Engine API) |
| **GitHub** | octocrab (GitHub REST API) |
| **Bluetooth** | btleplug (BLE mesh networking) |

## System Requirements

| Platform | Minimum |
|----------|---------|
| macOS | 13.0 (Ventura) or later |
| Windows | 10 (64-bit) or later |
| Linux | Ubuntu 22.04 / Fedora 38 or equivalent |

## Versioning

LoopDuck uses [Calendar Versioning](https://calver.org/) (YYYY.M.D), aligned with [OpenClaw](https://github.com/bemindlab/openclaw).

- Stable: `2026.4.2`
- Beta: `2026.4.2-beta.1`
- Same-day patch: `2026.4.2-1`

## Links

- [Build on OpenClaw](https://buildonclaw.cloud) — Project website
- [LoopDuck Product Page](https://buildonclaw.cloud/products/loopduck) — Features and downloads
- [Homebrew Tap](https://github.com/bemindlabs/homebrew-loopduck) — `brew install --cask bemindlabs/loopduck/loopduck`
- [Changelog](CHANGELOG.md) — Release history
- [Bemind Labs](https://github.com/bemindlabs) — Organization

## License

Proprietary. All rights reserved by Bemind Technology Co., Ltd. (BemindLabs)
