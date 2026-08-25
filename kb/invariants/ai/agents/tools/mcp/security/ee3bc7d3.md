---
kind: pragmatic
type: policy
domain: [agentic-engineering, mcp, security, tools]
confidence: 0.9
sources: 1
entities: [MCP, tool annotations, readOnlyHint]
motifs: [mandatory-but-unverified]
refs: ['https://modelcontextprotocol.io/docs/concepts/tools', 'https://modelcontextprotocol.io/specification/2026-07-28/server/tools', 'https://raw.githubusercontent.com/modelcontextprotocol/modelcontextprotocol/main/docs/specification/2026-07-28/server/tools.mdx']
---
# MCP tool annotations are untrusted input — never gate auto-approval on them

The MCP spec states that clients MUST consider tool annotations untrusted unless they come from a trusted server. Annotations are optional properties in a tool definition that describe the tool's behaviour — and they are supplied by the same server that implements the tool.

The consequence people get wrong: a behavioural hint asserting a tool is safe or read-only is a self-declaration by a party you may not trust, not a verified property. Building an auto-approval path that skips confirmation whenever a tool declares itself read-only means a malicious or compromised server can opt itself out of your only human check by setting a flag.

Treat annotations as UI hints and ranking signals — useful for ordering or labelling — and derive actual permission from something you control: an allowlist keyed to a server you have vetted, or the client's own classification of the operation.

The spec pairs this with related client-side SHOULDs that exist for the same reason: prompt for confirmation on sensitive operations, and show tool inputs to the user BEFORE calling the server, specifically to catch malicious or accidental data exfiltration. That last one only works if the display is not itself driven by server-supplied metadata.

RE-VERIFIED 2026-08-14 against the CURRENT revision (2026-07-28). The rule is unchanged and still a MUST, verbatim: "For trust & safety and security, clients **MUST** consider tool annotations to be untrusted unless they come from trusted servers." It sits in a Warning callout in the Tool Definition section of `server/tools`.

SCOPE NOTE, because the title is shorter than the rule. The spec's MUST carries an explicit carve-out — annotations from TRUSTED servers may be relied on. The title's "never gate auto-approval on them" is therefore a policy for the third-party and untrusted-server case, which is the case that bites; it is not a claim that the spec forbids ever trusting an annotation. If you operate both client and server inside one trust boundary, the carve-out is yours to use, and the thing to write down is how a server earns "trusted" status.

VERIFICATION SCOPE: the annotation rule and the two client-side SHOULDs quoted above were re-read in full. The specific annotation FIELD names (`readOnlyHint` and its siblings) were NOT re-enumerated against the current revision — this fact does not assert the current field list.
