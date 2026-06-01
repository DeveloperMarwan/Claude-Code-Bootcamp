# Before you start — installing Claude Code

This book is hands-on: every chapter asks you to run **Claude Code** in your own
terminal. If you have not installed it yet, this takes about five minutes. (In
the live workshop this is pre-work; reading on your own, do it now.)

## Install

The native installer is the recommended path on every platform:

```bash
# macOS, Linux, or Windows (WSL)
curl -fsSL https://claude.ai/install.sh | bash
```

```powershell
# Windows (PowerShell)
irm https://claude.ai/install.ps1 | iex
```

Prefer npm? Claude Code also ships as a global package (requires Node.js 18+):

```bash
npm install -g @anthropic-ai/claude-code
```

Native installs update themselves in the background, so you stay current without
any extra steps.

## Verify

Confirm the binary is on your `PATH`:

```bash
claude --version
claude doctor   # deeper check of your install and configuration
```

## Sign in

Claude Code needs a **Pro, Max, Team, Enterprise, or Console** account — the free
Claude.ai plan does not include access. Start it in any project folder and follow
the browser prompt the first time:

```bash
claude
```

Once `claude --version` prints a version and you have signed in, you are ready
for Module 1. Everything else in this book builds on that one command.
