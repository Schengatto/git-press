<div align="center">

<img src="assets/icon.png" alt="GitPress" width="96" />

# GitPress

**A fast, free Git GUI for Windows, macOS and Linux, with AI built in.**

[![CI](https://github.com/Schengatto/git-press/actions/workflows/ci.yml/badge.svg)](https://github.com/Schengatto/git-press/actions/workflows/ci.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

[Website](https://schengatto.github.io/git-press/) &nbsp;·&nbsp; [Download](https://github.com/Schengatto/git-press/releases/latest) &nbsp;·&nbsp; [User manual](USER_MANUAL.md) &nbsp;·&nbsp; [Changelog](CHANGELOG.md)

</div>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="website/images/screenshots/dark.png">
  <img src="website/images/screenshots/light.png" alt="GitPress main window: commit graph, staging panel and diff viewer">
</picture>

GitPress is a desktop Git client inspired by [GitExtensions](https://gitextensions.github.io/), rebuilt for every
platform with Electron, React and TypeScript. It shows your whole history as a virtualized commit graph that stays
smooth on large repositories, lets you stage single hunks, and turns interactive rebase into drag and drop.
Every Git command it runs is visible in the command log, so nothing happens behind your back.

## Why GitPress

- **The graph is the interface.** Branches, merges, cherry-picks, resets and tags start from the commit graph.
- **Precise staging.** Stage files, hunks or single lines, then review them in a unified or side-by-side diff.
- **Interactive rebase without the editor.** Reorder, squash and drop commits with drag and drop.
- **AI where it saves time.** Commit messages, conflict resolution, pull request descriptions and code review, with your own provider.
- **Scriptable by agents.** A built-in MCP server exposes 50+ Git operations to Claude, ChatGPT, Copilot or any MCP client.

## AI features

Configure a provider in **Settings → AI / MCP** (Anthropic Claude, OpenAI GPT or Google Gemini) with your own API key.

| Feature | What it does |
|---|---|
| **Commit messages** | Reads the staged diff and proposes a Conventional Commits message you can edit before committing. |
| **Conflict resolution** | In the 3-way merge editor, analyzes base, ours and theirs and previews a resolution you accept, edit or reject. |
| **Pull request descriptions** | Writes title and description from the branch commits, following the repository PR template when one exists. |
| **Code review** | Right-click a commit or a range to get a review of bugs, security, performance and style in a dedicated panel. |
| **MCP server** | Exposes 50+ read and write Git operations (status, log, diff, blame, branches, commit, merge, rebase, push, stash) to external AI assistants. |

## Features

### Core
- **Commit graph** with colored lane lines, virtualized scrolling, branch/tag decorations
- **Staging panel** with file-level and line-level (hunk) staging
- **Diff viewer** with unified and side-by-side modes (powered by diff2html)
- **Commit dialog** with amend support and discard changes
- **Command log** showing every git command executed

### Branch Management
- Create, rename, delete branches
- Merge and rebase (standard + interactive rebase with drag-and-drop)
- Cherry-pick from commit graph context menu
- Reset branch to any commit (soft, mixed, hard)
- Create tags (lightweight or annotated) with optional push to remote

### Remote Operations
- Push, pull (merge/rebase), fetch (all/prune)
- Clone repositories
- Manage remotes (add, remove)
- Ahead/behind indicators on tracked branches

### Advanced
- **Blame view** with per-line annotations
- **File history** (git log --follow) with per-commit diff
- **Stash** create, pop, apply, drop
- **Submodule** list and update
- **Search/filter** commits by message, author, hash, or ref
- **Auto-fetch** with configurable interval and prune option

### UI
- Dark theme (Catppuccin Mocha) and light theme (Catppuccin Latte)
- Dockable panel layout (sidebar, graph, details, command log)
- Welcome screen with recent repositories
- Settings panel (git config, fetch, commit, diff, graph, advanced)
- Keyboard shortcuts: `Ctrl+O` open, `Ctrl+K` commit, `Ctrl+F` search

## Installation

Download the latest release from the [GitHub Releases](https://github.com/Schengatto/git-press/releases) page:

- **Windows:** MSI installer or Portable ZIP
- **macOS:** ZIP archive (Apple Silicon)
- **Linux:** `.deb` (Debian/Ubuntu) or `.rpm` (Fedora/RHEL)

> **Note:** GitPress is not yet code-signed. Your OS may show a security warning on first launch:
>
> - **Windows:** SmartScreen will warn you — click "More info" → "Run anyway"
> - **macOS:** Right-click the app → "Open" → "Open" again, or run `xattr -cr /Applications/GitPress.app`
>
> See the [User Manual](USER_MANUAL.md#security-warnings-on-first-launch) for detailed instructions.

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) 20+
- [Git](https://git-scm.com/) 2.30+

### Install & Run

```bash
git clone https://github.com/Schengatto/git-press.git
cd git-press
npm install
npm start
```

### Scripts

| Command | Description |
|---|---|
| `npm start` | Start in development mode |
| `npm test` | Run unit tests |
| `npm run test:e2e` | Run E2E tests (Playwright) |
| `npm run lint` | Lint with ESLint |
| `npm run format` | Format with Prettier |
| `npm run package` | Package the app |
| `npm run make` | Create distributables |

## Tech Stack

| Package | Role |
|---|---|
| Electron + Electron Forge (Vite) | Desktop shell + packaging |
| React 18 + TypeScript | UI + type safety |
| simple-git | Git CLI wrapper |
| dockview | Dockable panel layout |
| diff2html | Diff rendering |
| Tailwind CSS | Styling |
| zustand | State management |
| react-virtuoso | Virtualized commit list |
| electron-updater | Auto-update via GitHub Releases |
| vitest + Playwright | Unit + E2E testing |

## Project Structure

```
src/
├── main/              # Electron main process
│   ├── git/           # GitService, graph-builder
│   └── ipc/           # IPC handlers (repo, status, commit, log, branch, remote, diff, stash, blame)
├── preload/           # Typed contextBridge API
├── renderer/          # React UI
│   ├── components/    # Layout, graph, sidebar, commit, details, diff, dialogs, command-log
│   └── store/         # Zustand stores (repo, graph, ui, command-log)
└── shared/            # Types and IPC channel constants shared between processes
```

## Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

Before contributing, please review our [Code of Conduct](CODE_OF_CONDUCT.md).

## Security

To report a vulnerability, please see [SECURITY.md](SECURITY.md).

All release binaries are scanned with [VirusTotal](https://www.virustotal.com) (~70 antivirus engines). Scan reports are linked in each [GitHub release](https://github.com/Schengatto/git-press/releases).

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for a list of changes.

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
