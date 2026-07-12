# AgentOnboard

AgentOnboard is an open ecosystem for AI agents to discover, authenticate with, and operate third-party services on behalf of humans — without the human juggling API keys, MCP configs, or per-platform credentials.

## The problem

Today, if a human wants their AI agent to use a service on their behalf, they face a mess:

- **Per-platform credentials** — Every service requires its own API key, OAuth flow, or token. Managing them across sessions is painful.
- **Key leakage risk** — Giving a static API key to an agent means that key lives in conversation context, logs, and transcripts. If it leaks, the damage is permanent until manually revoked.
- **No discovery** — There is no way for an agent to know which services a human can access, or how to integrate with them.
- **No verification for partners** — Every service that wants to allow AI agent access has to build its own auth system, manage its own tokens, and solve the same problems independently.

AgentOnboard solves all of this with one unified layer.

## How AgentOnboard helps each actor

### For humans

You sign up once, create a single API key, and save it with the `aon` CLI. From that point on, your agent can discover and use AgentOnboard-compatible services on your behalf — without ever touching your API key again.

- **One key, infinite services** — No more managing per-platform credentials.
- **Your key never leaves your machine** — The agent works with short-lived session tokens that expire in minutes. Your static key stays safely on disk.
- **Full control** — Revoke your key from the dashboard at any time. All agents instantly lose access.

### For agents

When you are equipped with the AgentOnboard skill, you gain the ability to:

- **Check if a service is available** by looking up the AgentOnboard directory
- **Read the service's own documentation** to learn exactly how to call it
- **Get a session token** that proves you are acting on behalf of a specific human
- **Call the service's API** following their documented conventions
- **Handle errors gracefully** — expired tokens, rate limits, permission issues

You never need to know the human's API key. You never store secrets. You never persist credentials between sessions. The `aon` CLI handles all of that.

### For partners (service providers)

You integrate with AgentOnboard once, and instantly every AgentOnboard-equipped agent becomes a potential user of your service.

- **No auth system to build** — AgentOnboard handles verification. You receive a session token and validate it server-side to know exactly which human is making the request.
- **Better user experience** — Your users don't need to generate API keys, copy tokens, or configure MCP servers. They just tell their agent to use your service.
- **Discovery** — Your service appears in the AgentOnboard directory, making it discoverable by agents everywhere.
- **You own the documentation** — You write the API docs that agents read. Clear docs mean seamless integrations.

## The flow

```
Human signs up → gets API key → saves it with aon CLI
                                              │
Agent starts a session                        │
  ├── aon doctor ✓ ─── setup good, proceed
  └── aon doctor ✗ ─── guide human through setup
              │
              ▼
Agent receives a task: "use Service X on my behalf"
              │
              ▼
Agent checks the directory → is Service X listed?
              │                    │
             YES                   NO
              │                    └── Tell human: not in directory yet
              │
              ▼
Agent reads Service X's API docs from the directory
              │
              ▼
Agent runs aon token get → gets a 5-minute session token
              │
              ▼
Agent calls Service X's API using the token
              │
              ▼
If 401 → token expired → aon token get → retry
If 200 → done → return result to human
```

## Key properties

- **The API key never leaves the human's machine.** It is stored by the `aon` CLI in the home directory. The agent never reads it, never stores it, never sends it.
- **Session tokens expire in 5 minutes.** If a token leaks, the damage window is small. The agent mints a new one as needed.
- **The agent is stateless.** Every session starts fresh. The agent always relies on `aon` for key management.
- **Partners verify server-side.** They never touch the human's API key — they only see session tokens, which they validate on every request.
- **Open ecosystem.** Any service can integrate with AgentOnboard and become available to every AgentOnboard-equipped agent.
