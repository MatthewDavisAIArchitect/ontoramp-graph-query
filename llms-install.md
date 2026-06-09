# Install — OntoRamp Graph Query (for AI agents)

You are an AI agent (e.g. Cline) setting up the **OntoRamp Graph Query** MCP server for a user. This is a **hosted, remote** server (Streamable HTTP). There is **nothing to clone, build, install, or run locally** — you only add a config entry pointing at the hosted endpoint, with the user's API key.

## Step 1 — Ensure the user has a free API key

Ask the user for their OntoRamp API key (format `or_free_…`). If they don't have one, tell them to get a free key — no credit card — at **https://ontoramp.com/mcp**; it is emailed to them. Do **not** invent or guess a key.

## Step 2 — Add the server to the MCP config

Add this block to the user's MCP settings. In Cline that is `~/.cline/mcp.json` (CLI) or the Cline UI → MCP Servers → Configure → Configure MCP Servers. Merge into any existing `mcpServers` object:

```json
{
  "mcpServers": {
    "ontoramp-graph-query": {
      "url": "https://ontoramp-graph-query.fly.dev/mcp",
      "headers": { "Authorization": "Bearer <USER_API_KEY>" },
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

Replace `<USER_API_KEY>` with the user's actual key. Transport is **Streamable HTTP** (Cline's recommended remote transport); do not set a `command`/`args` — this is not a stdio server.

## Step 3 — Confirm it is reachable

Run a health check (no key required):

```bash
curl https://ontoramp-graph-query.fly.dev/health
```

Expect `{"status":"ok","version":"1.0.0","server":"ontoramp-graph-query"}`. If you get a non-200, the user's network is blocking it — there is nothing to fix in the config.

## Step 4 — Available tools

After the client reconnects, these tools are available:

- `query_architecture` — architecture-grounded answers (Free tier)
- `get_constraint_signals` — governance constraints for a proposed action (Free tier)
- `find_dependencies` — system/component dependencies (Developer tier)
- `get_evidence_for_claim` — evidence chains for a claim (Developer tier)
- `request_assessment` — request an Agentic Readiness Assessment (all tiers)

Free-tier keys can call `query_architecture` and `get_constraint_signals` (10 queries/day) and `request_assessment` anytime. The other tools return an upgrade message on the free tier — that is expected, not an error.

## Notes

- No environment variables, no dependencies, no local process.
- Auth is a Bearer API key in the `Authorization` header. The key is also accepted as a `?api_key=` query parameter if your client cannot set headers.
- Health/status: https://ontoramp-graph-query.fly.dev/health
