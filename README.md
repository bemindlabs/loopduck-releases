# LoopDuck

**AI Coding workflow desktop app** by [Bemind Labs](https://github.com/bemindlabs)

[![Latest Release](https://img.shields.io/github/v/release/bemindlabs/loopduck-releases?label=download&style=for-the-badge)](https://github.com/bemindlabs/loopduck-releases/releases/latest)

## Download

| Platform | File | Install |
|----------|------|---------|
| **macOS** (Apple Silicon) | [`.dmg`](https://github.com/bemindlabs/loopduck-releases/releases/latest/download/LoopDuck_0.2.0_aarch64.dmg) | Open DMG, drag to Applications |
| **macOS** (Intel) | [`.dmg`](https://github.com/bemindlabs/loopduck-releases/releases/latest/download/LoopDuck_0.2.0_x64.dmg) | Open DMG, drag to Applications |
| **Windows** | [`.exe`](https://github.com/bemindlabs/loopduck-releases/releases/latest/download/LoopDuck_0.2.0_x64-setup.exe) | Run installer |
| **Windows** (MSI) | [`.msi`](https://github.com/bemindlabs/loopduck-releases/releases/latest/download/LoopDuck_0.2.0_x64_en-US.msi) | Run installer |
| **Linux** (Debian/Ubuntu) | [`.deb`](https://github.com/bemindlabs/loopduck-releases/releases/latest/download/LoopDuck_0.2.0_amd64.deb) | `sudo dpkg -i LoopDuck_*.deb` |
| **Linux** (Fedora/RHEL) | [`.rpm`](https://github.com/bemindlabs/loopduck-releases/releases/latest/download/LoopDuck-0.2.0-1.x86_64.rpm) | `sudo rpm -i LoopDuck_*.rpm` |
| **Linux** (AppImage) | [`.AppImage`](https://github.com/bemindlabs/loopduck-releases/releases/latest/download/LoopDuck_0.2.0_amd64.AppImage) | `chmod +x LoopDuck_*.AppImage && ./LoopDuck_*.AppImage` |

Or browse all versions on the [Releases](https://github.com/bemindlabs/loopduck-releases/releases) page.

## Install via Homebrew (macOS)

```bash
brew install --cask bemindlabs/loopduck/loopduck
```

## What is LoopDuck?

LoopDuck is a cross-platform desktop app for AI-powered coding workflows. Built with Tauri v2 (Rust + React), it includes:

- **Integrated terminal** with PTY session management
- **Git & GitHub** integration with worktree support
- **Docker Compose** management
- **AI chat** with OpenClaw gateway integration
- **Scrum board** with markdown-driven stories, sprints, and DLC phases
- **Jira sync** — bidirectional sync between local scrum board and Jira Cloud
- **SSH** remote connections
- **Agent-to-agent** discovery and collaboration
- **Command palette** (Cmd+K) with customizable keyboard shortcuts

## System Requirements

| Platform | Minimum |
|----------|---------|
| macOS | 11.0 (Big Sur) or later |
| Windows | 10 (64-bit) or later |
| Linux | Ubuntu 22.04 / Fedora 38 or equivalent |

## Links

- [Build on OpenClaw](https://buildonclaw.cloud) — Project website
- [Bemind Labs](https://github.com/bemindlabs) — Organization

## License

Proprietary. All rights reserved by Bemind Labs.
