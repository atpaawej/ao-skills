<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://res.cloudinary.com/demo/image/upload/v1/ao-skills-dark">
    <img alt="AgentOnboard Skills" src="https://res.cloudinary.com/demo/image/upload/v1/ao-skills-light" width="369">
  </picture>
</p>

# AgentOnboard Skills

Agent skills that make your AI agent a first-class citizen of the AgentOnboard ecosystem.

[![skills.sh](https://skills.sh/b/atpaawej/ao-skills)](https://skills.sh/atpaawej/ao-skills)

## What is AgentOnboard?

AgentOnboard is an open ecosystem for AI agents to discover, authenticate with, and operate third-party services on behalf of humans — without the human juggling API keys, MCP configs, or per-platform credentials.

When your agent is equipped with this skill, it can:

- **Discover** AgentOnboard-compatible services from the directory
- **Authenticate** using short-lived session tokens instead of static API keys
- **Call partner APIs** following their documented conventions
- **Handle errors** — expired tokens, rate limits, permission issues — automatically

## Quickstart

```bash
npx skills@latest add atpaawej/ao-skills
```

Then in any Claude Code session, your agent automatically knows how to use AgentOnboard. Just ask it to use a service, and the skill handles the rest.

### First-time setup

If you haven't used AgentOnboard before, your agent will guide you through:

1. Signing up at [ao.aawej.in](https://ao.aawej.in)
2. Creating an API key from your dashboard
3. Saving it with the `aon` CLI

After that, everything is automatic.

## How it works

```
You: "Use Service X to do Y on my behalf"
        │
        ▼
Agent checks → Service X in the AgentOnboard directory?
        │                      │
       YES                     NO
        │                      └── Tells you: not in directory
        │
        ▼
Agent reads Service X's API docs from the directory
        │
        ▼
Agent runs aon token get → gets a 5-minute session token
        │
        ▼
Agent calls Service X's API with the token
        │
        ▼
Returns the result to you
```

## Security

- **Your API key never leaves your machine.** The `aon` CLI stores it locally. Your agent never reads it, never sends it, and never remembers it between sessions.
- **Session tokens expire in 5 minutes.** If a token leaks, the damage window is small.
- **Your agent is stateless.** Every session starts fresh, relying on the CLI for key management.

## Skill files

| File | What it covers |
|---|---|
| `SKILL.md` | Entry point — boot check, setup detection, branch dispatch |
| `agentonboard.md` | Full ecosystem overview — problem, actors, flow |
| `setup.md` | CLI install and API key save guide |
| `token-lifecycle.md` | Session token minting, expiry, and refresh |
| `directory.md` | Partner discovery and API documentation |
| `api-calling.md` | Calling partner APIs with session tokens |
| `troubleshooting.md` | Error codes and recovery steps |

## License

MIT
