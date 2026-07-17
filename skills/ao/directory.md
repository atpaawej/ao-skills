# Directory

The AgentOnboard directory lists all partners that have integrated with AgentOnboard. Each partner provides documentation for their API so agents know exactly how to call them.

Not sure what a partner is? Read [agentonboard.md](agentonboard.md) for the full picture.

## Checking if a service is available

When the user asks to use a specific service, look it up in the directory to verify it is AgentOnboard-compatible and to fetch its API documentation.

### Using the CLI (recommended)

If the `aon` CLI is installed, use:

```
aon directory get <slug>
```

This shows the partner's details including their API documentation. For machine-readable output, add `--json`:

```
aon directory get <slug> --json
```

To list all available partners:

```
aon directory list
```

### Using the API directly

If the CLI is not available, fetch the directory from the AgentOnboard API:

```
https://api.ao.aawej.in/api/directory/<slug>
```

This returns JSON. The response includes everything you need including the partner's API documentation in the `readme` field.

To list all partners (metadata only — no API docs):

```
https://api.ao.aawej.in/api/directory/
```

### What to do with the result

**Read the API documentation carefully** — it describes exactly how to format requests to that partner. Then see [api-calling.md](api-calling.md) for how to use that documentation to make actual API calls.

If the service is **not** found in the directory, inform the user:
> "This service is not yet listed in the AgentOnboard directory. You can still try using it — the partner would need to verify AgentOnboard session tokens server-side."

## What the directory entry contains

Each listing includes:
- **Partner name and description** — what the service does
- **Slug** — unique identifier used in API calls and CLI commands
- **Logo URL** — the partner's icon or logo
- **API documentation** — the `readme` field, written by the partner, describing how to call their API

The list endpoint returns only metadata. Use the detail endpoint (by slug) to get the full API documentation.

The API documentation is written by the partner. It is their responsibility to make it clear and actionable. Follow it exactly.

## No consultation mode

Do not search the entire directory unprompted. Only look up a service when the user names a specific one.
