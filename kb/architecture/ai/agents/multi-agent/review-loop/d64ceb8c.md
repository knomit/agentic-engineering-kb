---
type: pattern
domain: [agentic-engineering, multi-agent, coding-agents, context-engineering]
confidence: 0.8
sources: 2
entities: [Cognition, Devin, generator-verifier, context rot, Anthropic, Playwright MCP, Claude Opus 4.6]
motifs: [shared-context-defeats-independence]
refs: ['https://cognition.com/blog/multi-agents-working', 'https://www.anthropic.com/engineering/harness-design-long-running-apps']
---
# The reviewer agent must have clean context, not a shared briefing with the coder

A generator agent paired with a separate evaluator agent is the most consistently reported working multi-agent pattern, and two independent vendors describe it in the same terms. Cognition reports a coding agent plus review agent catching "an average of 2 bugs per PR, of which roughly 58% are severe." Anthropic reports that a single agent reliably overpraises its own work, on subjective judgments (design taste) and objective ones (bugs) alike, and that without external evaluation pressure the output is "bland" and features get stubbed rather than finished.

The non-obvious design constraint is that the evaluator must start from COMPLETELY CLEAN context — no shared briefing, no handoff of the generator's trace. This is the opposite of the instinct to "give the reviewer everything so it understands the intent," and it is also the opposite of Cognition's own general advice to share full traces between agents. The stated reason is context rot: the generator's context is long by the time the artifact exists, and inherited length degrades the reviewer's attention. A reviewer that sees only the diff can re-discover whatever context it actually needs, and pays attention cost only for that.

This is the specific case where context isolation beats context sharing, and it works because review is read-only — the evaluator contributes intelligence, never writes.

Give the evaluator real tools rather than only the artifact. Anthropic's evaluator drove the running application through Playwright MCP before grading and caught defects a diff read would not surface. An evaluator restricted to reading the diff can only find what is visible in the diff.

The cost is on the return path: the generator must filter evaluator feedback against the original user intent before acting on it. Without that filter the loop degrades into looping, scope creep, and the generator following the evaluator into work the user never asked for. An unfiltered evaluator-to-generator channel is where this pattern fails, not the review itself.

Two things that bound when to use it. Price: Anthropic measured a solo 20-minute run at $9 against $200 for the full three-agent harness — roughly a 20x multiplier. And the value DECAYS as models improve: with Opus 4.6 the evaluator became "unnecessary overhead" for tasks inside the model's native capability, and stayed cost-justified only at the boundary of it. So re-benchmark whether the evaluator still earns its place on each model upgrade rather than treating the harness as permanent — this is a pattern whose ROI is model-version-dependent.
