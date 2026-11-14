# Warden 1.1

**It knows what's open in your editor.** A folder open in Cursor, VS Code, Windsurf or a JetBrains IDE (IntelliJ, PyCharm, Android Studio and the rest) counts as in use, even with nothing running in it, so nothing in it is cleared or removed.

**Build output for every major language, not just node_modules.** Maven and Gradle, Rust, .NET, Python, Flutter, CMake, Unity, Unreal, Terraform and more. A folder is offered only when its tool's file is beside it and version control ignores it.

**When in doubt, it keeps everything.** If git, Mercurial or Subversion can't answer, nothing is offered. Right before anything is deleted, version control is asked again.

**Memory cards for all your work.** Main checkouts, feature branches and plain folders get a card too, not only worktrees: the sessions, commits, uncommitted files and how to continue. Warden never removes these folders.

**Also new:** Mercurial and Subversion support; a disk forecast from the last day; growth alerts that name the biggest worktree.

**Lighter:** about 8× fewer wakeups, a disk check peaks at about 30 MB instead of 100, and it uses a fraction of a percent of one core.

**Fixed:**
- A health check with an impossible port no longer stops the helper.
- Menu bar apps (OrbStack, say) starting or quitting are noticed at once.
- Siri and the terminal no longer read out an old status when the helper isn't running.
