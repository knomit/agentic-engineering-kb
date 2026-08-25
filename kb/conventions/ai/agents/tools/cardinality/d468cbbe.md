---
type: observation
domain: [agentic-engineering, tools, coding-agents]
confidence: 0.7
sources: 1
entities: [Anthropic, Claude Code, grep, bash]
motifs: [choice-count-degrades-selection]
refs: ['https://simonwillison.net/2026/Jul/21/cat-and-thariq/']
---
# Keep tool cardinality low and let a general tool absorb specific ones — Claude Code deleted grep in favour of native bash

The Claude Code team removed grep and other dedicated search tools in favour of native bash, and hold the rule that "every tool we add has a distinct function from every other tool." The direction of travel is worth noting because it runs against the instinct to give an agent a purpose-built tool per task: when the model is strong enough to compose a shell command, a specific tool that a general tool already subsumes is not a convenience, it is another sibling competing for selection and another description the model must disambiguate against.

The rule to apply is distinctness, not count: adding a tool is justified when no existing tool can do the job, not when an existing tool could do it more awkwardly.

The genuinely surprising detail is why their dedicated file-edit tool survived. It exists primarily so the client can render a nice dedicated UI for edits — not because bash could not perform the edit. That is a legitimate reason to keep a redundant tool, and it is worth naming explicitly because it is the only one in their account: a tool can earn its place by making the agent's actions LEGIBLE to the human watching, even when it adds nothing to the model's capability. If you keep a redundant tool, know which of these two reasons you are invoking.

This complements rather than contradicts the guidance to shape tools around workflows instead of your API's CRUD surface — both reject one-tool-per-operation, and both put the burden on each tool to justify its existence against its siblings.

Source caveat: conference-talk summary of team practice, not published documentation. Also note this is calibrated to strong models in a shell-equipped coding harness; an agent without shell access, or on a weaker model, does not get bash for free.
