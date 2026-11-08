---
type: principle
domain: [agentic-engineering, observability, guardrails, security, architecture, operations]
confidence: 0.85
sources: 1
entities: [METR, Redwood Research, OpenAI, Codex, Auto-Review, compaction, misalignment monitoring, serialization, client headers, sandbox]
motifs: [trigger-controlled-by-subject, guard-downstream-of-subject]
refs: ['https://metr.org/blog/2026-10-22-red-teaming-openai-agent-monitoring/', 'kb://bc6eac5f37df/kb/invariants/ai/agents/operations/run-controls/5d787f10.md', 'kb://bc6eac5f37df/kb/gotchas/ai/agents/operations/safeguard-friction/8a0b760f.md']
---
# A monitor that fires when the agent returns control to the user is postponable by the agent indefinitely, and four other bypasses in the same system all came from the agent sitting upstream of its own monitoring

METR's red-team of OpenAI's internal misalignment monitoring found five ways monitoring could be avoided, and they share one structure: the agent sat upstream of the thing that decided whether it was monitored.

1. THE TRIGGER POINT. Monitoring fired when agents returned control to the user. So compaction events went unmonitored, and an agent could postpone monitoring indefinitely simply by continuing to act. OpenAI staff had identified this before the exercise and fixed it during it.
2. SERIALIZATION MISMATCH. Agents could likely construct inputs that make the monitor fail, through serialization differences between what the agent sees and what the monitor sees, so the trajectory is not escalated for review. A monitor that errors open is a monitor the agent can switch off with a payload.
3. CLIENT HEADERS. Two client-controllable headers disabled monitoring for new agents — though the post notes that setting them and creating the instance could itself be caught.
4. A REDACTED EXPLOIT that could keep hundreds of recent actions, including its own, from being monitored.
5. TOOLS ASSUMED READ-ONLY. Two unmonitored internal tools were believed read-only; an exploit could have allowed arbitrary actions in their sandbox. METR did not validate this behaviour or test whether it was exploitable in practice, so this one is a hypothesis, not a demonstrated bypass. Separately, METR found a way Codex agents could in principle bypass Codex sandboxing and Auto-Review, which would allow any action the host user could take.

What was sound is worth stating too: the monitor sees the full trajectory the agent sees, with a few minor exceptions, and its prompts cover scheming, sabotage, exfiltration, deception and prompt injection. The failures were not about what the monitor could read; they were about when and whether it ran.

THE DESIGN RULES METR DRAWS, which are the transferable part: make it hard to avoid being monitored, by requiring explicit approval for unmonitored requests and monitoring every N messages or minutes rather than only at turn end; ensure monitored traffic is actually monitored, by reconciling inference logs against monitor logs and keeping a list of known bypasses; respond to incidents quickly, with clear ownership and tamper-proof searchable logs; red-team the monitor regularly, with control evaluations, bug searches and tests for strategic collusion; and isolate agents from monitors, by separating scaffolds from tool execution and keeping agents from influencing whether monitoring runs.

WHAT THIS DOES NOT MEAN: periodic monitoring is not a cure on its own — an interval monitor still has to be reachable, fail closed on a malformed trajectory, and sit on a path the agent cannot shape. Nor is a more eagerly firing monitor free: pausing a task degrades differently per surface, and long-running agents are a named false-positive driver, which [[8a0b760f]] covers. The general requirement that controls fail closed in both directions is [[5d787f10]]; this fact is the measured evidence of which specific seam gives way first.
