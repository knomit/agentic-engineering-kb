---
type: principle
domain: [agentic-engineering, security, prompt-injection, orchestration, multi-agent, cost]
confidence: 0.9
sources: 1
entities: [Anthropic, Claude Code, ultracode, dynamic workflows, Agent SDK, webhook, pull request comment, scheduled task]
motifs: [privilege-follows-provenance, trigger-word-as-instruction]
refs: ['https://code.claude.com/docs/en/workflows', 'kb://bc6eac5f37df/kb/invariants/ai/agents/security/instruction-hierarchy/99aa74e6.md']
---
# A workflow-triggering keyword is honoured only from human-typed input, and before v2.1.210 a relayed webhook payload or pull-request comment could start a run

Claude Code's `ultracode` keyword starts a dynamic workflow only when it arrives in a prompt the person typed themselves: at the interactive prompt, in an IDE extension panel, in a Remote Control client, or in an Agent SDK application that stamps the keyboard input's `origin` as `{ kind: "human" }`. It does not start a workflow when it reaches the session by another route — a prompt passed with `-p`, an Agent SDK prompt sent without the human stamp, a scheduled task prompt, or a webhook payload or pull request comment relayed into the conversation. The documentation records the earlier behaviour explicitly: before v2.1.210, the keyword started a workflow from any of these routes too, including a webhook payload or pull request comment relayed into the conversation.

The general rule this is an instance of: a trigger word is a privileged instruction, so the decision to honour it has to be gated on the PROVENANCE of the text carrying it, not on the text matching. A keyword matched anywhere in a channel that also carries third-party content hands anyone who can post into that channel the ability to spend the operator's budget — dozens to hundreds of agents in one run — while violating no tool permission at all, because the orchestration itself is the action and every individual tool call inside it is in policy.

Operational consequence: when you add a trigger phrase, a magic comment or a command word to an agent that also ingests relayed content, make the origin a required part of the match. An allowlist of routes (typed input only) is the enforceable form; a denylist of known relay shapes is not, since the next integration adds a route nobody enumerated.

WHAT THIS DOES NOT MEAN: the gate governs who may START a run, not what the run may do. The agents a workflow spawns go through the session's ordinary permission rules and sandboxing either way, so this closes an initiation-and-resource hole rather than an injection path into the agents themselves. The complementary rule for text rather than triggers is [[99aa74e6]].
