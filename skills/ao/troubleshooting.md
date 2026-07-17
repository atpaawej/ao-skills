# Troubleshooting

This reference covers common errors and how to recover from them. If you are unsure about the overall flow, read [agentonboard.md](agentonboard.md) for context.

## Error: `aon: command not found`

The `aon` CLI is not installed.

**Fix:** Install it:
```bash
npm install -g @agentonboard/cli
```
Then run `aon doctor` to verify. See [setup.md](setup.md) for full setup instructions.

## Error: `aon doctor` fails

Run `aon doctor` to see what is wrong. It will tell you exactly what is missing or misconfigured.

Common causes:
- **No API key saved** — Guide the user to get their key from the AgentOnboard dashboard and save it with `aon save <key>`.
- **CLI not installed** — Install it (see above).
- **Corrupt config** — The CLI's config file may be damaged. The user can re-run `aon save` to overwrite it.

Tell the user what `aon doctor` reports and guide them through the fix.

## Error: Partner API returns 401

The session token may have expired (they are valid for 5 minutes — see [token-lifecycle.md](token-lifecycle.md)).

**Fix:** Mint a fresh token:
```bash
aon token get
```
Then retry the partner API call with the new token (see [api-calling.md](api-calling.md)).

If a fresh token also returns 401, the token may have been revoked or the user may not have access to this partner. Inform the user.

## Error: Partner API returns 429 (rate limited)

The partner is rate-limiting requests.

**Fix:** Wait briefly, then retry. If the partner's docs specify a rate limit, respect it. If rate limiting persists, inform the user.

## Error: Partner API returns 403

The token is valid but the user does not have permission to access this resource.

**Fix:** Inform the user. They may need to contact the partner directly to gain access.

## Error: Partner API returns 5xx

The partner's server is experiencing an issue.

**Fix:** Retry once after a short wait. If it fails again, inform the user — the partner's service may be down.

## Error: Service not found in directory

The user asked to use a service that is not in the AgentOnboard directory (see [directory.md](directory.md)).

**Fix:** Inform the user that the service is not yet AgentOnboard-integrated. If the user still wants to try calling it, they can — the partner just needs to verify AgentOnboard session tokens server-side. The skill cannot help further without directory docs.
