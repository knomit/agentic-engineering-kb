---
kind: pragmatic
type: policy
domain: [agentic-engineering, mcp, security, authorization]
confidence: 0.9
sources: 1
entities: [MCP, token passthrough, OAuth, audience, RFC 9068, confused deputy]
motifs: [conflation-hides-second-defect]
refs: ['https://modelcontextprotocol.io/specification/2025-06-18/basic/security_best_practices', 'https://modelcontextprotocol.io/specification/2025-06-18', 'https://modelcontextprotocol.io/docs/2026-07-28/tutorials/security/security_best_practices', 'https://raw.githubusercontent.com/modelcontextprotocol/modelcontextprotocol/main/docs/docs/2026-07-28/tutorials/security/security_best_practices.mdx']
---
# MCP servers MUST NOT accept tokens that were not issued to them — audience-validation failure and token passthrough are two separate defects, and only the second is the one people name

The MCP spec names "token passthrough" as an explicitly forbidden anti-pattern: an MCP server accepting an access token from a client and forwarding it to a downstream API without validating that the token's audience is the MCP server itself. The rule is normative — servers MUST NOT accept any token not explicitly issued for the MCP server — and it holds even for servers that are today a thin proxy.

**THE TWO DIMENSIONS, added in the `2026-07-28` revision and worth separating** — the spec now says the vulnerability "has two critical dimensions", and a server can have the first without the second:

1. **Audience validation failures.** "When an MCP server doesn't verify that tokens were specifically intended for it (for example, via the audience claim, as mentioned in RFC9068), it may accept tokens originally issued for other services. This breaks a fundamental OAuth security boundary, allowing attackers to reuse legitimate tokens across different services than intended." This is complete on its own: the server is already exploitable at the point of *acceptance*, before anything is forwarded anywhere.
2. **Token passthrough.** "If the MCP server not only accepts tokens with incorrect audiences but also forwards these unmodified tokens to downstream services, it can potentially cause the 'confused deputy' problem, where the downstream API may incorrectly trust the token as if it came from the MCP server or assume the token was validated by the upstream API."

The practical consequence of the split: a server that terminates every token locally and never forwards one has *not* satisfied this rule. "We don't do passthrough" is an answer to dimension 2 only. The check that matters is whether you validate the audience claim on the way in.

The reasoning is not merely hygiene. Four stated consequences: (1) downstream rate limiting, request validation and traffic monitoring often key off token audience, so passthrough silently bypasses them; (2) the MCP server cannot distinguish between its own clients when they arrive bearing an upstream-issued token that is opaque to it, and the downstream resource server's logs attribute requests to the wrong identity — both wreck incident investigation; (3) a token accepted by several services without audience validation lets an attacker who compromises one service reach all the others; (4) a server that starts as a pure proxy and later needs its own security controls has no identity to hang them on.

What this does NOT mean: it is not a ban on the MCP server calling downstream APIs on the user's behalf. The server should hold its own separately-issued downstream credential, obtained through its own authorization flow — the ban is on reusing the client's inbound token as the outbound one.

**VERIFICATION.** Re-verified 2026-08-12 against both the originally cited `2025-06-18` revision (unchanged) and `2026-07-28` (which adds the two-dimension framing quoted above). Read from the specification repository while `modelcontextprotocol.io` was refusing connections; the page has moved within the repo to `docs/<rev>/tutorials/security/`.
