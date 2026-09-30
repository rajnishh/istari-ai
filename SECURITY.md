# Security Policy

Istari runs AI coding agents on your machine, hooks into the AI tools you already use, and can act on GitHub and JIRA on your behalf. We take reports about it seriously.

## Reporting a vulnerability

Please report privately. **Do not open a public issue, discussion or pull request** for a security problem.

- **Preferred:** use GitHub's private reporting - open the repository's **Security** tab and choose **Report a vulnerability**.
- **Or email:** security@istari-ai.dev

Please include what you found, how to reproduce it, the Istari version (`ist --version`), your platform, and the impact you expect. A proof of concept helps but is not required.

What to expect:

- an acknowledgement within 5 working days;
- an assessment and, where needed, a fix plan, shared with you before anything is published;
- credit in the release notes if you would like it.

Istari is maintained by a small team, so a fix may take longer than we would like; we will keep you informed.

## Supported versions

Only the **latest release** receives security fixes. Please upgrade (`ist upgrade`, or re-run the installer) before reporting.

## Security model

Knowing what Istari is allowed to do makes it easier to see what counts as a vulnerability.

**What Istari has access to**

- Everything under `~/.istari/`: its SQLite database (session memory, decisions, PR review history), config, logs and worktrees.
- After `ist setup`, and only for the tools you keep enabled: hook entries in `~/.claude/settings.json`, Codex and Cursor hook files, slash commands and skills, and marked blocks in shared instruction files such as `AGENTS.md`. Changes outside `~/.istari` are recorded in an install manifest so `ist uninstall` can reverse them.
- The credentials you give it: a GitHub token (or your `gh` login), a JIRA token, a Discord bot token, and model API keys. Secrets can be referenced from the environment, a file or a command instead of being stored in config.
- The agents it starts run with the permissions of their role and trust level. At higher trust levels they can commit, push and open pull requests.

**Protections that exist by design**

- Hooks can be switched off without uninstalling (`ist hooks off`) and the whole system can be halted (`ist down`).
- A pre-push secret scan (gitleaks when installed, otherwise a built-in pattern set) runs before the pipeline delivers code, and outbound messages are scrubbed for secrets before they are posted to Discord, Slack or JIRA.
- Automated writes to external systems pass through a mutation gate with de-duplication and a circuit breaker.
- Commands arriving from remote channels such as Discord are allowlisted and blocked from exfiltrating local data.
- The web dashboard binds to `127.0.0.1` only.
- The installer verifies a SHA-256 checksum for every download and refuses to install when the checksum file is missing.

**In scope** - for example:

- a way for a remote party (a Discord message, a PR comment, a ticket description, a webhook) to make Istari run commands, read files or leak secrets;
- secrets written to logs, memory, Discord or GitHub in clear text;
- bypassing trust levels, approval gates, the mutation gate or the halt switch;
- the dashboard, companion server or MCP server being reachable or exploitable beyond their intended scope;
- installer or upgrade integrity problems.

**Out of scope**

- Actions an agent takes within the permissions you explicitly granted it, such as pushing code when you set it to autonomous.
- Prompt-injection behaviour of the underlying models themselves, unless Istari makes it worse or fails to apply a protection it claims.
- Vulnerabilities in third-party tools (Claude Code, Codex, Cursor, Ollama, `gh`) - please report those to their maintainers.
- Issues that require an attacker who already controls your user account.
