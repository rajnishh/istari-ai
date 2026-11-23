# Warden 1.2

Notarized by Apple. Everything since 1.1.0 (14 November). There was no separate 1.1.1; its fixes are here too. The full list is in [the changelog](https://istari-ai.dev/warden/).

## Disk Insight: what filled the disk, for any app
- **Warden notices which folders change**, from macOS's own record, at no measurable cost. When free space drops 3 GB within an hour, or falls under the warning level, a short-lived separate process measures only those folders and names what was written: "Google Chrome: 6 copies of code_sign_clone (14 GB; can go once Chrome quits)".
- **Each find gets a verdict**: caches, copies of the same thing, older versions next to a newer one, build output, or something that may be yours. Places macOS protects are named, never read. Nothing new is deleted on its own.
- **Known cases are rules**: iPhone and Watch symbols, browsers' code-sign copies, Cursor snapshots, Android system images, Xcode build files, Adobe and Spotify caches and more. Rules update with the update check, signed with Warden's update key.
- **Low-space alerts say what grew** ("iPhone support files +11 GB") and offer unused iPhone support files.
- **Warnings go by what's really free**, not Finder's figure, which counts space macOS may purge later. Under 3 GB really free, the alert comes at once with a sound.

## Disk: more that can go, safely
- **App checkpoints**: Cursor's copies for undoing AI edits (18 GB in 15 minutes on one Mac) are cleared once Cursor quits. Off, Alert me (the default) or Automatic.
- **Flutter**: build output in idle worktrees, and old `.dart_tool/flutter_build` caches.
- **Spare Next.js builds** next to a running server, and **Xcode builds of projects that are gone**, even while Xcode is open.
- **Simulators one by one**, with their size and when they were last used, and a Delete button.
- **Sizes say what deleting really frees** (pnpm's shared packages used to be counted 5 times over).

## Sessions and worktrees: tidied the way production tools do it
- **Only days you use the Mac count.** A weekend or a week off doesn't make work look abandoned.
- **Standard defaults**: sessions archived after 30 days unused, merged worktrees removed after 14.
- **Never silent**: anything due is listed as **Tidying soon** for at least a day, with Keep for a week, a month or always.
- **Parent sessions** keep their worktree while the side sessions they started are in use. **Away mode** holds all tidying until you're back.
- **Claude Code's own 30-day cleanup** is announced 5 days ahead, and Settings can set it to a year.
- **AI Agents** has tabs and a tree: project → worktree → conversations.

## Services: run a whole stack
- **Docker containers, "Starts after", on-demand services and services that take turns**, plus `warden services` and `warden start|stop|restart` in Terminal.
- **Updating or restarting Warden never stops a service.**
- **One list, grouped by stack**, with memory per service. **Spotted on this Mac** shows containers and servers Warden doesn't run, and **Put on watch** adopts one.
- **Who turned a service off** is logged: the app, the menu bar or a terminal command, and which coding agent ran it.

## Warns before it stops, and urgent alerts
- **A warning first**, with **Keep It Running** and **Do It Now**, 2 minutes before Warden stops something you might be using.
- **Urgent alerts** (close to freezing, the disk nearly full, a service down) come as time-sensitive notifications plus a small window that stays on top.
- **Simulators** wait the usual 20 minutes unless the Mac is close to freezing.

## Menu bar and screens
- **A calmer icon** with a small dot when something needs a look, and **the problem itself** as the first row.
- **Pause Automatic Actions** for an hour, three hours or until morning.
- **Settings** in six tabs; from the menu it opens on its own.
- **Activity** opens in one go, and Programs, Disk and AI Agents are calmer.

## Privacy
- **Settings → Privacy** says what Warden connects to and lets you turn each off. **Offline mode** turns them all off.
- **Every connection Warden made** is listed on the Mac (`warden connections`).

## Memory and fixes
- **One big local AI model at a time**: an idle Ollama model is unloaded when a second big one runs.
- **A container engine going down is said**, with a button to start it and its containers again.
- **Only one helper runs at a time**, and `warden version` says which Warden this is.
