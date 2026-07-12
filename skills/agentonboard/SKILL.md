---
name: agentonboard
description: Use when the user needs to set up or use AgentOnboard — an open ecosystem for AI agents to discover, authenticate with, and operate third-party services on behalf of humans. Guides CLI installation, API key saving, session token management, partner discovery, and calling partner APIs. Also triggers when the user mentions "aon", "session token", "exchange key", or asks how to authenticate with or connect to a service.
---

# AgentOnboard

You are now an AgentOnboard-equipped agent. AgentOnboard lets agents discover, authenticate with, and operate third-party services on behalf of humans — without the human juggling API keys, MCP configs, or per-platform credentials.

This skill is your reference for everything AgentOnboard. Start with the boot check below, then follow the branch that matches what you find.

## Boot check

Run this at the start of every session (before any task):

```bash
which aon 2>/dev/null && aon doctor 2>/dev/null
```

**All checks pass and at least one key is saved** → Setup is complete. Read the reference that matches the user's task and proceed.

**`aon` not found or doctor reports failures** → Follow the [setup.md](setup.md) reference to install and configure.

**Doctor passes but reports "no keys to test"** → The user has the CLI but hasn't saved an API key yet. Follow the saving section of [setup.md](setup.md).

## Reference files

Load only what you need:

- [agentonboard.md](agentonboard.md) — What AgentOnboard is, how it works, the three actors, and the full ecosystem
- [setup.md](setup.md) — Installing `aon`, saving an API key, first-time guide
- [token-lifecycle.md](token-lifecycle.md) — Minting, reusing, and refreshing session tokens
- [directory.md](directory.md) — Discovering AgentOnboard-compatible partners and reading their API docs
- [api-calling.md](api-calling.md) — How to format requests to partner APIs using session tokens
- [troubleshooting.md](troubleshooting.md) — Error codes, recovery steps, diagnosis
