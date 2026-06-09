# Usage examples — OntoRamp Graph Query

Once the server is connected (see [`../llms-install.md`](../llms-install.md)), an agent can call these tools. The inputs below are realistic; outputs are described conceptually (your organization's real data determines the actual response).

## `query_architecture`

Ask what the organization's documented architecture says about a topic — grounded in structure, not document similarity.

```jsonc
// tool call
{ "name": "query_architecture", "arguments": {
  "query": "What are our data-residency constraints for EU customer data?"
}}
```

Returns an architecture-grounded answer plus the structural elements it drew on. If coverage is thin, the response flags the gap (and may surface an Agentic Readiness Assessment prompt).

## `get_constraint_signals`

Before an agent takes a consequential action, check which governance constraints apply.

```jsonc
{ "name": "get_constraint_signals", "arguments": {
  "action": "Deploy a new microservice that stores PII in us-east-1"
}}
```

Returns the constraint signals relevant to that action (e.g. data-handling, residency, approval-authority categories) so the agent can decide whether to proceed, adjust, or escalate.

## `find_dependencies` *(Developer tier)*

Trace what a system or component depends on — and what depends on it.

```jsonc
{ "name": "find_dependencies", "arguments": {
  "component": "billing-service"
}}
```

Returns upstream/downstream dependency edges from your architecture so an agent can reason about blast radius before changing something.

## `get_evidence_for_claim` *(Developer tier)*

Ask the graph to support or contradict a claim, with provenance.

```jsonc
{ "name": "get_evidence_for_claim", "arguments": {
  "claim": "All customer-facing services enforce SSO."
}}
```

Returns an evidence chain — the documented elements that support or contradict the claim — rather than an unsourced assertion.

## `request_assessment`

Kick off an Agentic Readiness Assessment (free on every tier, rate-limit exempt).

```jsonc
{ "name": "request_assessment", "arguments": {
  "context": "Evaluating agent readiness for our payments platform"
}}
```

Returns a confirmation and next steps; the OntoRamp team follows up.

---

**Tiers at a glance:** Free → `query_architecture`, `get_constraint_signals`, `request_assessment` (10 queries/day). Developer → all tools + evidence provenance. Get a free key at [ontoramp.com/mcp](https://ontoramp.com/mcp).
