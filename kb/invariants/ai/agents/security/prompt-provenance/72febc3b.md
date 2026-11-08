---
type: principle
domain: [agentic-engineering, security, guardrails, orchestration, multi-agent, prompt-injection]
confidence: 0.9
sources: 1
entities: [Anthropic, Claude Code, dynamic workflows, auto permission mode, permission classifier, agent(), subagent, script-computed prompt]
motifs: [privilege-follows-provenance, authority-lost-on-rewrite]
refs: ['https://code.claude.com/docs/en/workflows', 'kb://bc6eac5f37df/kb/invariants/ai/agents/security/trigger-provenance/3bf8bbab.md', 'kb://bc6eac5f37df/kb/architecture/ai/agents/security/permission-systems/89df351e.md']
---
# A prompt an orchestration script computed does not carry the user's authority into the subagent it spawns — the permission classifier is told it is script-computed text, not a request from the person

When an orchestrator builds a subagent's prompt in code and the subagent's tool calls are then reviewed by a permission classifier, the provenance of that prompt decides how much it can authorise. Claude Code's dynamic workflows make this explicit: "In auto mode, the prompt your script passes to `agent()` doesn't count as a request from you when the classifier reviews that subagent's actions, because Claude Code marks it as text the script computed."

The consequence for anyone designing an orchestrator is that you cannot launder authority through a script. A string the script assembled — even one built from something the user typed earlier, even one the user would have approved verbatim — is not a user instruction at the point where the subagent's actions are judged. So a fan-out cannot pre-authorise its workers' risky tool calls by writing "the user asked for this" into their prompts, and a worker that needs a privileged action still faces whatever gate an unattended agent faces.

The general shape, which is the part that transfers beyond this one product: a permission system that weighs who asked must track provenance through every hop that rewrites the request, and must default a rewritten request to the lower authority. The attractive-but-wrong design is to attach the authority to the request's content; the correct one attaches it to the channel the content arrived on.

WHAT THIS DOES NOT MEAN: it is not that script-spawned subagents are unprivileged or sandboxed more tightly. They run under the session's own permission rules, and the keyword that starts a workflow "only chooses how Claude structures the work: the agents' tool calls receive the same permission checks and sandboxing as any other tool call in the session." What changes is only whether the prompt itself counts as a human request during classifier review.
