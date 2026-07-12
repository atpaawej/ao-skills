# Setup

This reference covers the first-time setup: installing the `aon` CLI and saving the user's API key.

Don't know what AgentOnboard is yet? Read [agentonboard.md](agentonboard.md) first.

## Prerequisite

The user needs an AgentOnboard account. If they don't have one, tell them:

> Go to ao.aawej.in, sign in with Google or GitHub, and create an API key from your dashboard. Come back here and give me the key — I'll save it for you.

## Install `aon`

If `which aon` returns nothing, install the CLI:

```bash
npm install -g @agentonboard/cli
```

Once installed, verify it works:

```bash
aon doctor
```

This runs a suite of checks and reports the result. If everything is green, setup is complete. If it reports anything missing, follow the next steps.

## Save an API key

Ask the user for their API key. When they provide it:

```bash
aon save <api-key>
```

The CLI stores it in `~/.agentonboard/tokens.json`. The agent never sees the key — it is written directly by the CLI to the user's filesystem.

Once saved, run `aon doctor` to confirm everything is green.

## Setup complete

When `aon doctor` passes, setup is done. The agent can now mint session tokens (see [token-lifecycle.md](token-lifecycle.md)) and call partner APIs (see [api-calling.md](api-calling.md)). No further configuration is needed.
