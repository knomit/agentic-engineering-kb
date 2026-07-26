---
kind: pragmatic
type: policy
domain: [agentic-engineering, mcp, security, authorization]
confidence: 0.9
sources: 1
entities: [MCP, token passthrough, OAuth, audience]
refs: ['https://modelcontextprotocol.io/specification/2025-06-18/basic/security_best_practices', 'https://modelcontextprotocol.io/specification/2025-06-18']
---
# MCP servers MUST NOT accept tokens that were not issued to them — token passthrough is spec-forbidden

The MCP spec names "token passthrough" as an explicitly forbidden anti-pattern: an MCP server accepting an access token from a client and forwarding it to a downstream API without validating that the token's audience is the MCP server itself. The rule is normative — servers MUST NOT accept any token not explicitly issued for the MCP server — and it holds even for servers that are today a thin proxy.

The reasoning is not merely hygiene. Four stated consequences: (1) downstream rate limiting, request validation and traffic monitoring often key off token audience, so passthrough silently bypasses them; (2) the MCP server cannot distinguish between its own clients when they arrive bearing an upstream-issued token that is opaque to it, and the downstream resource server's logs attribute requests to the wrong identity — both wreck incident investigation; (3) a token accepted by several services without audience validation lets an attacker who compromises one service reach all the others; (4) a server that starts as a pure proxy and later needs its own security controls has no identity to hang them on.

What this does NOT mean: it is not a ban on the MCP server calling downstream APIs on the user's behalf. The server should hold its own separately-issued downstream credential, obtained through its own authorization flow — the ban is on reusing the client's inbound token as the outbound one.
