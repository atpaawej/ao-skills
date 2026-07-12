# Directory

The AgentOnboard directory lists all partners that have integrated with AgentOnboard. Each partner provides documentation for their API so agents know exactly how to call them.

Not sure what a partner is? Read [agentonboard.md](agentonboard.md) for the full picture.

## Checking if a service is available

When the user asks to use a specific service, look it up in the directory to verify it is AgentOnboard-compatible and to fetch its API documentation.

The directory is publicly readable at the AgentOnboard website. Fetch the listing for the service the user wants to use.

If the service is found, you will receive the partner's API documentation. **Read it carefully** — it describes exactly how to format requests to that partner. Then see [api-calling.md](api-calling.md) for how to use that documentation to make actual API calls.

If the service is **not** found in the directory, inform the user:
> "This service is not yet listed in the AgentOnboard directory. You can still try using it — the partner would need to verify AgentOnboard session tokens server-side."

## What the directory entry contains

Each listing includes:
- **Partner name and description** — what the service does
- **API documentation** — how to call the partner's API, what endpoints are available, what authentication header to use, and what responses look like

The API documentation is written by the partner. It is their responsibility to make it clear and actionable. Follow it exactly.

## No consultation mode

Do not search the entire directory unprompted. Only look up a service when the user names a specific one.
