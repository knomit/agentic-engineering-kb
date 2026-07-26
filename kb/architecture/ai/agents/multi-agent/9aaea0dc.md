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

STALENESS (re-checked 2026-07-26, source live and unedited): the post is dated June 2025 and its argument is explicitly time-indexed — the author frames multi-agent unreliability as a property of what models could do in 2025 and expects improved agent-to-agent communication to make collaboration viable later. So read this as a strong claim about a mechanism (dispersed context produces incompatible commitments) and a dated claim about severity. The mechanism has not been refuted; whether it still dominates on current models is not something this post can tell you.

Also worth holding alongside it: the frameworks it argues against by name (OpenAI Swarm, Microsoft AutoGen) are not the shape the question takes now, since current models spawn subagents natively without any framework being chosen.
