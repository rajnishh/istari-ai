# Warden 1.2.1

Notarized by Apple. A patch for 1.2.0. The full list is in [the changelog](https://istari-ai.dev/warden/).

## AI Agents opens in seconds
- **Even with 88,000 conversations.** On a Mac where a tool starts Claude Code in a temporary folder for every task, AI Agents showed "Reading sessions from your coding tools…" for many minutes. Reading a conversation's title and folder is now about 10 times quicker. What was read is saved, so Warden doesn't read unchanged conversations again each time it starts.
- **Each tool's sessions appear as soon as they're read**, and the page says which one it's still reading.
- **A folder with thousands of conversations lists the newest 300.** "Show all" or search finds the rest.
- **Folders on a network share** no longer hold up the list.

## Every Claude Code config folder
- **Conversations in `~/.claude-work`, `~/.claude-alex` and the like are listed too**, next to `~/.claude`. So are those in any folder a shell alias sets `CLAUDE_CONFIG_DIR` to. Nothing to set up.
- **Resume uses the right folder**: `CLAUDE_CONFIG_DIR=~/.claude-work claude --resume …`.
- **Claude Code's own cleanup is read per folder**, and "Keep conversations for a year" sets every folder.

## Also
- Services: "Nothing on watch yet" is centred on the page.
