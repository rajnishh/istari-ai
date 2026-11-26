# Warden 1.2.2

Notarized by Apple. A safety patch for 1.2.1. The full list is in [the changelog](https://istari-ai.dev/warden/changelog/).

## Worktree clean-up never loses your data
- **Merged code is removed as before.** It's safe in git, so it's deleted outright, along with build output like `node_modules`. The log keeps the branch, the last commit and a command that brings it back.
- **Files git ignores are never deleted.** Things like `.env`, `output/`, uploads and databases aren't in git, so nothing else holds a copy. Warden won't remove a worktree with these on its own. When you press Remove, only those files go to the Trash (Finder → Put Back restores them), each listed with its size.
- **Warden only empties what it put in the Trash**, after 30 days, or 7 when the disk is nearly full, with a notice first.
- **A worktree in use is never removed.** That means a program has files open in it, runs from it, or one of Warden's services is set to run there.
