---
kind: pragmatic
type: policy
domain: [agentic-engineering, mcp, security, tools]
confidence: 0.9
sources: 1
entities: [MCP, tool annotations, readOnlyHint]
refs: ['https://modelcontextprotocol.io/docs/concepts/tools']
---
# MCP tool annotations are untrusted input — never gate auto-approval on them

The MCP spec states that clients MUST consider tool annotations untrusted unless they come from a trusted server. Annotations are optional properties in a tool definition that describe the tool's behaviour — and they are supplied by the same server that implements the tool.

The consequence people get wrong: a behavioural hint asserting a tool is safe or read-only is a self-declaration by a party you may not trust, not a verified property. Building an auto-approval path that skips confirmation whenever a tool declares itself read-only means a malicious or compromised server can opt itself out of your only human check by setting a flag.

Treat annotations as UI hints and ranking signals — useful for ordering or labelling — and derive actual permission from something you control: an allowlist keyed to a server you have vetted, or the client's own classification of the operation.

The spec pairs this with related client-side SHOULDs that exist for the same reason: prompt for confirmation on sensitive operations, and show tool inputs to the user BEFORE calling the server, specifically to catch malicious or accidental data exfiltration. That last one only works if the display is not itself driven by server-supplied metadata.
