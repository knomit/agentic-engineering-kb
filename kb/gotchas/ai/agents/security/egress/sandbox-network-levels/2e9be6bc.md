---
type: observation
domain: [agentic-engineering, security, sandboxing, exfiltration, coding-agents, operations]
confidence: 0.85
sources: 1
entities: [Anthropic, Claude Code, cloud sessions, network access level, egress proxy, Anthropic API, prompt injection, working branch]
motifs: [strictest-setting-still-open, guarantee-narrower-than-assumed]
refs: ['https://claude.dev/blog/claude-code-in-the-cloud/', 'kb://bc6eac5f37df/kb/invariants/ai/agents/evaluation/containment/egress/2dfac716.md', 'kb://bc6eac5f37df/kb/gotchas/ai/agents/security/egress/fdad859e.md']
---
# The strictest network setting on a hosted coding agent is documented as not closed — two channels stay open by design: requests to the model API, and the session's push to its own branch

Claude Code's cloud sessions offer a network level of None as the strictest setting, and the documentation states plainly that None is not an air gap: even at None, Claude Code still sends requests to the Anthropic API, so data can leave the VM that way, and the session can still push to its own branch. All outbound traffic passes through a proxy that logs hostnames; the default level, Trusted, additionally allows package registries, GitHub, and major cloud SDK hosts.

Consequence for anyone designing or reviewing a containment story: the network level bounds which third parties the agent can reach, not whether data can leave. Treat the inference channel and the version-control push as two permanently open conduits and defend them on their own terms — by what you are willing to place in the agent's context, and by how narrowly the push credential is scoped — rather than by tightening the allowlist.

What this does NOT mean: it is not a claim that the None setting is useless or misdescribed. It genuinely removes general internet reach, which is what blocks the bulk of indirect-prompt-injection payloads from calling home to an arbitrary host. It is the stronger reading — that no data can leave a None-level session — that is false, and it is the reading a reviewer will reach for when the setting is named after an absence.
