# Warden 1.1

Notarized by Apple. Everything since 1.0.0 (built 11 November).

## Disk: watched in the background, and finished work tidied safely
- **The disk is watched in the background.** Free space is read every hour. A full measurement runs every 6 hours, half an hour after free space drops 5 GB, and whenever the Disk view opens.
  - The forecast ("full in about 3 days") uses the last day's pace. A sudden drop whose space comes back within 3 hours (a build, a virtual machine's swap) doesn't count.
  - Growth alerts name what grew, and the biggest worktree with its build output.
- **Finished coding worktrees give back their space.** A worktree counts as finished when all of these hold:
  - its work is merged into main;
  - nothing in it changed;
  - nothing runs inside it, and it isn't open in an editor;
  - nobody touched it for an hour.

  Its packages and build output can then be cleared, and come back with `pnpm install` or a build. Settings → Coding worktrees: Clear automatically, Alert me (the default) or Off.
- **Build output for every major language:** `node_modules`, Maven and Gradle (`target`, `build`, `.gradle`, `.kotlin`), Rust `target`, .NET `bin`/`obj`, Python `.venv` and caches, Elixir, Haskell, Zig, CMake, Flutter, Ruby `vendor/bundle`, PHP `vendor`, Terraform, Unity, Unreal, iOS `Pods`, and Next, Nuxt, SvelteKit, Angular and Parcel output. A folder is offered only when two things hold: its tool's own file is beside it (`pom.xml`, `Cargo.toml`, `composer.lock`…), and version control ignores it or doesn't track it.
- **Merged worktrees that hold nothing else can be removed.** This is opt-in; Alert me is the default. It happens only after the worktree's memory card is saved, with no live session in it, and with no file in it changed today. Removal is `git worktree remove`, never forced.
- **Memory cards and Past work.**
  - **A card for every merged worktree:** the PR, commits, changed files and every conversation held there, from Claude Code, the Claude app, Codex, Gemini CLI, Cursor, Copilot CLI, Amp, OpenCode, Aider and more.
  - **Reopen** makes the worktree again and continues its conversation.
  - **Cards for work outside worktrees too:** main checkouts, feature branches and plain folders such as docs, with their sessions, commits, uncommitted files and resume commands. Warden never removes these folders.
- **It knows what's open in your editor.** A folder open in Cursor, VS Code, Windsurf, VSCodium, Kiro, Trae or a JetBrains IDE (IntelliJ, PyCharm, WebStorm, GoLand, CLion, Rider, Android Studio…) counts as in use, even with nothing running in it.
- **Mercurial and Subversion,** as well as git. Jujutsu's colocated repositories are read as git.
- **Installers you've already used** (a .dmg, .pkg, .zip or .xip in Downloads whose app is installed) can go to the Trash. Off by default.
- **`warden disk`** prints where space goes, what's safe to free and which worktrees would go and why, and changes nothing.

## Memory: when the Mac is close to freezing
- **The menu bar icon opens at once even then.** In a test with every core busy and memory at warning it opened in under 5 ms; before, a click waited 22 seconds to 2 minutes.
- **Free memory now** offers real choices once the safe steps are done: idle local AI servers, dev servers and test runs per project, idle coding sessions, and the biggest apps. Each asks first and says what could be lost. The Memory card has an Automatic switch.
- **The menu's "If the Mac is struggling" section** offers local AI servers. Force Quit asks first, and never offers Claude, Finder or Warden.

## Services
- A service that's already running outside Warden (started in Terminal, say) is adopted instead of being started twice, including when you switch a service on.
- The check on this Mac is a plain request over a socket. It follows redirects to another page on this Mac, as before.

## Lighter
- **About 8× fewer wakeups.** A health check kept an HTTP/3 connection open, and macOS pinged it every second or so.
- **About half the CPU,** a fraction of a percent of one core.
- **Less memory:** about 20–30 MB, and a disk check peaks around 30 MB instead of 100.
- **Fewer disk writes:**
  - status is saved every 2 seconds while the dashboard is open, after a reading in which something important changed, and otherwise every 2 minutes;
  - the minute-by-minute history is written in batches while the Mac is calm, and every minute while it's under strain.
- **The stuck-app check:** the app in front is asked every 10 seconds, and other apps every 30.

## Safer
- When git, Mercurial or Subversion can't answer (Xcode's licence not accepted after an update, a broken install, a stuck command), nothing is offered for clearing.
- Version control is asked again right before anything is deleted.
- A worktree git can't read counts as changed.
- A worktree that any program changed today is kept.
- An archived Claude app session's worktree may go after an hour, not a day.

## Fixed
- A health check with an impossible port no longer stops the helper.
- A crash when Free memory now refreshed its choices.
- An update could leave the helper stopped.
- Menu bar apps starting or quitting (OrbStack, say) are noticed at once.
- Siri and the terminal no longer read out an old status when the helper isn't running.
- After clearing packages, Warden says `pnpm install`, not `npm install`.
- Processes macOS refuses to describe are skipped instead of asked about on every reading.

More about Warden: https://istari-ai.dev/warden/
