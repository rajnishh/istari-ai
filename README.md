# Istari

**The memory and supervision layer for AI coding agents.**

Istari (`ist`) sits on top of the coding agents you already use - Claude Code, Codex CLI, Cursor and Ollama - and gives them what a single session lacks: memory that carries across sessions, a supervised pipeline that takes a ticket to a pull request, safety limits, and background automation such as PR review.

> **Free early access.** Istari is free to use. This repository hosts the releases, the issue tracker and security reports; the source code will be published here under the Apache 2.0 licence once it is ready. Expect rough edges and breaking changes between minor versions.

---

## What it does

| You want to... | Istari gives you |
|---|---|
| Stop re-explaining your project every session | Memory that persists across sessions and engines, injected automatically at session start |
| Find what you or your agents decided weeks ago | `ist recall` - search over past sessions, decisions, PR reviews and meeting notes, with citations and a refusal when nothing relevant exists |
| Hand a ticket to an agent without babysitting it | `ist pick` - a supervised pipeline: enrich, plan, implement, verify (Istari runs your build and tests itself), self-review, open a PR |
| Keep control of what it does | Plan and push approval gates, trust levels, budgets, loop detection, scope rules and secret scanning before anything is pushed |
| Run several agents at once | Isolated git worktrees with their own ports and environment |
| Get PRs reviewed in the background | A watcher that reviews PRs where your review is requested, with code, security and architecture passes |
| Automate the rest | YAML "when this, then that" workflows, a personal engineering inbox, standups, Discord control from your phone |

---

## Install

```bash
curl -fsSL https://istari-ai.dev/install.sh | bash
```

The installer downloads the binary for your platform from this repository's [Releases](https://github.com/rajnishh/istari-ai/releases), verifies its SHA-256 checksum against `SHA256SUMS.txt`, and installs `ist`. No account or token is needed.

It does not enable anything: no hooks and no daemon until you run `ist setup`. The only change outside `~/.istari` is a `PATH` line in `~/.zshrc` or `~/.bashrc`, and only when the install directory is not already on your `PATH`.

To update later: `ist upgrade`, or run the installer again.

### Platform support

| Platform | Status |
|---|---|
| macOS, Apple Silicon | Supported |
| macOS Intel, Linux x64/arm64 | Not offered by the installer yet |
| Windows | Not supported |

---

## Quick start

```bash
# 1. Configure: three questions - your role, your engines, and whether to install hooks
ist setup

# 2. Review the work on your current branch - locally, posts nothing
ist review

# 3. Ask your memory a question
ist recall "what did we decide about the auth migration?"

# 4. Hand a ticket to an agent and follow along
ist pick PROJ-123 --follow

# 5. See what is running
ist status
```

`ist guide` lists what Istari can do, task by task. `ist examples` shows command recipes for common situations.

### What you need

- **An AI coding engine**: [Claude Code](https://docs.claude.com/en/docs/claude-code) (the most complete integration), Codex CLI, Cursor's `cursor-agent`, or [Ollama](https://ollama.com) for local models.
- **Git**, and the **GitHub CLI** (`gh`) for anything that touches pull requests.
- **Optional**: JIRA (tickets), Discord (remote control and notifications), an OpenAI key or Ollama (embeddings for recall).

Ticket integration currently targets **JIRA**. GitHub Issues and Linear are on the list.

---

## What Istari changes on your machine

Istari hooks into your AI tools, so here is exactly what it touches:

- **`~/.istari/`** - all of its own state: a SQLite database, config, logs, worktrees.
- **Only after `ist setup`, and only for the tools you keep enabled**: hook entries in `~/.claude/settings.json`, Codex and Cursor hook files, `/ist-*` slash commands and skills, and a marked block in shared instruction files such as `AGENTS.md`. Every change outside `~/.istari` is recorded in an install manifest.
- **`ist hooks off`** pauses every hook without uninstalling. **`ist uninstall`** shows a dry run first, then reverses exactly what the manifest recorded. Your data is kept unless you pass `--purge`, which offers an export first.

Istari sends nothing to its authors: there is no telemetry. It only talks to the services you connect (GitHub, JIRA, Discord, model providers).

---

## Feedback and support

- **Bugs and ideas:** open an [issue](https://github.com/rajnishh/istari-ai/issues/new/choose). `ist support-bundle` packages redacted diagnostics you can attach.
- **Security problems:** report them privately - see [SECURITY.md](SECURITY.md).

## Licence

The Istari binaries are free to use under the terms in [LICENSE.md](LICENSE.md). Each release includes `THIRD_PARTY_NOTICES.txt` for the open-source components it contains.

The name comes from the wizards of J.R.R. Tolkien's legendarium. Istari is an independent project and is not affiliated with or endorsed by the Tolkien Estate or Middle-earth Enterprises.
