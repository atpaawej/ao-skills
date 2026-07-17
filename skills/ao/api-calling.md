# Calling Partner APIs

This reference covers how to format requests to partner APIs using AgentOnboard session tokens. Before calling a partner API, you need a session token (see [token-lifecycle.md](token-lifecycle.md)) and the partner's API documentation (see [directory.md](directory.md)).

## The flow

Every partner API call follows the same pattern:

```
1. Get a fresh session token (see token-lifecycle.md)
2. Read the partner's API docs from the directory (see directory.md)
3. Call the partner API following their documentation
4. If the call fails with 401, the token may be expired — mint a new one and retry
```

## Authentication

The partner's API documentation will tell you how to present the session token. Partners choose their own authentication scheme. Common conventions include:

- **Bearer token** — `Authorization: Bearer <session-token>`
- **Custom header** — A partner-defined header like `X-Agent-Token: <session-token>`

**Always follow the partner's documented convention.** Do not assume a scheme.

## Reading partner docs

Fetch the partner's full directory listing (including API docs) via the detail endpoint:

- **With the CLI**: `aon directory get <slug>` (add `--json` for machine-readable output)
- **With curl/fetch**: `https://api.ao.aawej.in/api/directory/<slug>`

The partner's API documentation (`readme` field) will tell you:

- The **base URL** to call
- What **headers** to send (including how to present the token)
- Available **endpoints** and their HTTP methods
- **Request body** format if applicable
- **Response format** you can expect

If the documentation is unclear, do your best with what is available. Do not make up endpoints or parameters.

## Response handling

After calling the partner API:

- **2xx** — Success. Return the result to the user.
- **401** — Token expired or invalid. Mint a fresh token (see [token-lifecycle.md](token-lifecycle.md)) and retry once.
- **403** — Token is valid but the user does not have access to this resource. Explain this to the user.
- **429** — Rate limited. Wait a moment, then retry with backoff.
- **5xx** — Partner server error. Retry once after a short wait. If it persists, inform the user.

For detailed error handling, see [troubleshooting.md](troubleshooting.md).
