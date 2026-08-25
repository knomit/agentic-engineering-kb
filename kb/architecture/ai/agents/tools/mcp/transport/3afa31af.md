---
type: pattern
domain: [agentic-engineering, mcp, architecture, state-management, distributed-systems]
confidence: 0.9
sources: 2
entities: [MCP, "2026-07-28", SEP-2575, SEP-2567, initialize, Mcp-Session-Id, server/discover, subscriptions/listen]
motifs: [guarantee-narrower-than-assumed]
refs: ['https://modelcontextprotocol.io/specification/2026-07-28/changelog', 'https://modelcontextprotocol.io/specification/versioning', 'https://modelcontextprotocol.io/specification/2026-07-28/basic/index', 'https://raw.githubusercontent.com/modelcontextprotocol/modelcontextprotocol/main/docs/specification/2026-07-28/basic/index.mdx', 'https://aws.amazon.com/blogs/machine-learning/how-agentcore-gateway-supports-the-mcp-2026-07-28-spec/', 'kb://bc6eac5f37df/kb/invariants/ai/agents/tools/mcp/metadata/fa61c895.md']
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

**THE NORMATIVE TEXT, and the stdio trap it closes.** The above was originally assembled from the changelog; the spec body states the rule directly — "The Model Context Protocol (MCP) is a **stateless protocol**: all the information needed to process a request is contained in the request itself" — and then constrains servers in a way an implementer will otherwise violate by accident:

- "Servers **MUST NOT** rely on prior requests over the same connection to establish context (e.g., capabilities, protocol version, client identity)."
- "State that needs to span multiple requests (e.g., long-running tasks, application-level handles) **MUST** be referenced by an explicit identifier the client passes on each request."
- Servers SHOULD be prepared to handle requests "associated with multiple tasks, threads, or conversations", and SHOULD NOT require a client to reuse the same connection or process for related operations. Clients SHOULD NOT use "an individual task, thread, or conversation as the lifetime boundary for the stdio process".

The spec spells out the consequence for stdio specifically, and this is the one to internalise because stdio *looks* like a session: "an open connection, such as a STDIO process, is not a conversation or session: clients may interleave unrelated requests on the same transport, and a server must not treat connection or process identity as a proxy for conversation or session continuity." **A stdio server that caches per-user state, tenant scope or auth context in process memory keyed to "the current conversation" is non-conformant, and the failure mode is cross-conversation leakage rather than an error.** Note the scope: this forbids inferring *identity or context* from the connection; a process may still hold caches keyed to an explicit identifier the client sends.

Long-lived requests like `subscriptions/listen` are not an exception — they "remain request/response; the response is just an open stream of notifications", with state "scoped to the request itself, not to the connection underneath".

**What it buys.** An MCP deployment now load-balances like any stateless HTTP service — no sticky sessions, no shared session store, no session-affinity failure mode. Header-level routing means a gateway can dispatch and version-negotiate without deserialising payloads. AWS reports gateways supporting several protocol versions concurrently via a `supportedVersions` configuration, which the per-request negotiation model makes cheap.

**What it costs, and this is the part to plan for.** State did not disappear; it was pushed up the stack. Servers needing cross-call state must mint explicit handles and pass them as ordinary tool arguments, which puts state identifiers in the model's context where injection can reach them. Losing resumability means an interrupted long request is genuinely lost and must be retried under a new ID, so at-least-once delivery is now your problem at the application layer. Both were previously absorbed, badly, by the transport.

**Refs note:** `sources` corrected 1→2 — the AWS gateway post is an independent operator report and was already cited but not counted. The `basic/index` addition is the same source as the changelog (the MCP spec) and adds no independent corroboration. The spec text here was read from the spec repository's `.mdx` on branch `main` while `modelcontextprotocol.io` was refusing connections.
