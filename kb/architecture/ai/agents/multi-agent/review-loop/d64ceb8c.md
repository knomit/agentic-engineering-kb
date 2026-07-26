---
type: pattern
domain: [agentic-engineering, multi-agent, coding-agents, context-engineering]
confidence: 0.75
sources: 1
entities: [Cognition, Devin, generator-verifier, context rot]
refs: ['https://cognition.com/blog/multi-agents-working']
---
# The reviewer agent must have clean context, not a shared briefing with the coder

A coding agent paired with a review agent is the generator-verifier pattern, and Cognition reports it working in production: the reviewer catches "an average of 2 bugs per PR, of which roughly 58% are severe."

The non-obvious design constraint is that the reviewer must start from COMPLETELY CLEAN context — no shared briefing, no handoff of the coder's trace. This is the opposite of the instinct to "give the reviewer everything so it understands the intent," and it is also the opposite of Cognition's own general advice to share full traces between agents. The stated reason is context rot: the coder's context is long by the time the diff exists, and inherited length degrades the reviewer's attention. A reviewer that sees only the diff can re-discover whatever context it actually needs, and pays attention cost only for that.

This is the specific case where context isolation beats context sharing, and it works because review is read-only — the reviewer contributes intelligence, never writes.

The cost is on the return path: the coding agent must filter review feedback against the original user intent before acting on it. Without that filter the loop degrades into looping, scope creep, and the coder following the reviewer into work the user never asked for. Budget for that filtering step — an unfiltered review-to-coder channel is where this pattern fails, not the review itself.
