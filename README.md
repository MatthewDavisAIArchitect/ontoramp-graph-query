# OntoRamp Graph Query — MCP Server

> The only MCP server that answers "what does our architecture say about this?" — grounded in your organization's actual documented structure, not a document dump.

**Problem:** AI agents act blindly against organizational architecture. They don't know what the org has already decided, what constraints apply, or what the existing structure says about a proposed action.

**Solution:** Query your organization's architecture and governance constraints directly from any AI agent or LLM workflow. Returns architecture-grounded answers with evidence chains — not document similarity.

[![MCP Registry](https://img.shields.io/badge/MCP_Registry-com.ontoramp%2Fgraph--query-blue)](https://registry.modelcontextprotocol.io)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

---

## Tools

| Tool | Description | Tier |
|------|-------------|------|
| `query_architecture` | Query organizational architecture for answers grounded in documented structure | Free |
| `get_constraint_signals` | Surface governance constraints relevant to a proposed action or decision | Free |
| `get_evidence_for_claim` | Return evidence chains supporting or contradicting an architectural claim | Developer+ |
| `request_assessment` | Submit an Agentic Readiness Assessment request | All tiers, rate-limit exempt |

## Tiers

| Tier | Price | Limits | Features |
|------|-------|--------|----------|
| **Free** | — (no credit card) | 10 queries/day | `query_architecture` + `get_constraint_signals` |
| **Developer** | $0.015/call | Unlimited | All tools · Evidence provenance · Query history |
| **Org** | $249/mo flat | Unlimited | Aggregate architecture health · Cross-agent pooling · ARA pre-population |

`request_assessment` is exempt from rate limits on every tier.

## Quickstart

```json
{
  "mcpServers": {
    "ontoramp-graph-query": {
      "type": "http",
      "url": "https://ontoramp-graph-query.fly.dev/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

Get your free API key at [ontoramp.com/mcp](https://ontoramp.com/mcp).

## ARA Trigger

When `get_evidence_for_claim` surfaces evidence coverage gaps, the server prompts:

> Your architecture coverage has gaps that a manual review won't surface. An Agentic Readiness Assessment will diagnose your current state and build a prioritized remediation plan. [Schedule at ontoramp.com/assessment](https://ontoramp.com/assessment).

## Security

- All responses are SO-24 audited — no scoring-formula internals, no substrate architecture details
- Your data is scoped to your tenant namespace and never shared across organizations
- Free-tier keys are read-scoped; Developer/Org keys require account authentication
- `GET https://ontoramp-graph-query.fly.dev/health` returns live status

## Support

- Docs: [ontoramp.com/mcp](https://ontoramp.com/mcp)
- Issues: [github.com/MatthewDavisAIArchitect/ontoramp-graph-query/issues](https://github.com/MatthewDavisAIArchitect/ontoramp-graph-query/issues)
- Contact: m@ontoramp.com

---

*Governed by the Davis Canon — SSOT. OntoRamp LLC · [ontoramp.com](https://ontoramp.com)*
