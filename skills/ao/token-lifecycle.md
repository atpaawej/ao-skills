# Token Lifecycle

This reference covers everything about session tokens: how to mint them, how long they last, and how to handle expiry.

Make sure setup is complete (see [setup.md](setup.md)) before using tokens. For how to present tokens to partner APIs, see [api-calling.md](api-calling.md).

## Minting a session token

To get a fresh session token, run:

```bash
aon token get
```

The CLI reads the saved API key from disk, exchanges it, and returns a session token. The token is opaque — treat it as an opaque string.

**Important:** The agent should capture the token from the stdout and use it for partner API calls. Do not log or display the token unnecessarily.

## Token expiry

Session tokens are valid for **5 minutes** from the moment they are minted.

After 5 minutes, the token is no longer accepted by partners. The agent must mint a new one.

## Reuse strategy

Mint a token once at the start of the task, then reuse it for all partner API calls during the conversation. The token is valid for the full 5 minutes — no need to mint more than once for a single coherent task.

If a partner API returns a 401 response, the token may have expired. Mint a fresh token and retry the request (see [troubleshooting.md](troubleshooting.md) for more error scenarios).

## Pattern

```
1. Call aon token get → capture token
2. Call partner API with token
3. If 401 → go to step 1 and retry
4. Continue until task is complete
```
