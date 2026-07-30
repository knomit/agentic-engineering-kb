---
type: pattern
domain: [agentic-engineering, mcp, architecture, state-management, distributed-systems]
confidence: 0.9
sources: 1
entities: [MCP, "2026-07-28", SEP-2575, SEP-2567, initialize, Mcp-Session-Id, server/discover, subscriptions/listen]
refs: ['https://modelcontextprotocol.io/specification/2026-07-28/changelog', 'https://modelcontextprotocol.io/specification/versioning', 'https://aws.amazon.com/blogs/machine-learning/how-agentcore-gateway-supports-the-mcp-2026-07-28-spec/']
---
# MCP 2026-07-28 deleted the connection as a unit of state — no handshake, no session, no resumable stream

Revision `2026-07-28` is a single coherent bet, not a list of unrelated breaks: **every piece of per-connection state was removed from MCP, so a tool call is fully self-contained.** Read the individual changes as one decision and they stop looking arbitrary.

What was deleted:

- The `initialize` / `notifications/initialized` handshake. Protocol version and client capabilities now ride on every request in `_meta` (`io.modelcontextprotocol/protocolVersion`, `io.modelcontextprotocol/clientCapabilities`) (SEP-2575).
- Protocol-level sessions and the `Mcp-Session-Id` header on Streamable HTTP (SEP-2567). A consequence stated outright: `tools/list`, `resources/list` and `prompts/list` **no longer vary per-connection**.
- SSE stream resumability — the `Last-Event-ID` header and SSE event IDs. A broken response stream loses the in-flight request; the client MUST re-issue it as a new request with a new request ID.
- `ping`, `logging/setLevel`, and `notifications/roots/list_changed`. Log level is now per-request via `io.modelcontextprotocol/logLevel` in `_meta`, and servers MUST NOT emit `notifications/message` for a request that did not carry that field.
- The HTTP GET endpoint and `resources/subscribe`/`unsubscribe`, replaced by `subscriptions/listen`: one long-lived POST-response stream carrying only opted-in change notifications. Request-scoped notifications (`notifications/progress`, `notifications/message`) still flow on the response stream of the request they belong to, **not** on the `subscriptions/listen` stream — mixing those two up is the easy implementation error here.

What was added to make that survivable: `server/discover`, a **mandatory** server RPC returning supported versions, capabilities and identity in one round trip; and required `Mcp-Method` / `Mcp-Name` HTTP headers on Streamable HTTP POSTs so intermediaries can route without parsing the JSON body.

**What it buys.** An MCP deployment now load-balances like any stateless HTTP service — no sticky sessions, no shared session store, no session-affinity failure mode. Header-level routing means a gateway can dispatch and version-negotiate without deserialising payloads. AWS reports gateways supporting several protocol versions concurrently via a `supportedVersions` configuration, which the per-request negotiation model makes cheap.

**What it costs, and this is the part to plan for.** State did not disappear; it was pushed up the stack. Servers needing cross-call state must mint explicit handles and pass them as ordinary tool arguments, which puts state identifiers in the model's context where injection can reach them. Losing resumability means an interrupted long request is genuinely lost and must be retried under a new ID, so at-least-once delivery is now your problem at the application layer. Both were previously absorbed, badly, by the transport.
