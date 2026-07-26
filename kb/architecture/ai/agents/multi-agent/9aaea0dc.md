---
type: pattern
domain: [agentic-engineering, multi-agent, architecture]
confidence: 0.7
sources: 1
entities: [Cognition, Devin, single-threaded linear agent]
refs: ['https://cognition.com/blog/dont-build-multi-agents']
---
# Cognition's case against multi-agent: dispersed context produces incompatible work products

Cognition (Devin) argues against subagent architectures on two stated principles: (1) "Share context, and share full agent traces, not just individual messages" — passing a subagent only its task description, rather than the whole trace, starves it of the reasoning that constrains its choices; (2) "Actions carry implicit decisions, and conflicting decisions carry bad results" — every action a subagent takes silently commits to assumptions the other subagents never see.

Their illustration: building Flappy Bird via two subagents produced a Super Mario Bros. background from one and a visually inconsistent bird from the other. Nothing errored. The failure surfaced only at integration, where the parent agent faced work products that could not be reconciled — the expensive part was not the wrong output but that it was discovered last.

Their alternative is a single-threaded linear agent with continuous context, and when the task outgrows the window, a dedicated LLM that compresses history and action traces into key decisions and events rather than forking into parallel agents.
