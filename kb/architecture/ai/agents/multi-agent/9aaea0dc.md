---
type: pattern
domain: [agentic-engineering, multi-agent, architecture]
confidence: 0.8
sources: 2
entities: [Cognition, Devin, single-threaded linear agent]
refs: ['https://cognition.com/blog/dont-build-multi-agents', 'https://cognition.com/blog/multi-agents-working']
---
# Cognition's case against multi-agent: dispersed context produces incompatible work products

Cognition (Devin) argued in June 2025 against subagent architectures on two stated principles: (1) "Share context, and share full agent traces, not just individual messages" — passing a subagent only its task description, rather than the whole trace, starves it of the reasoning that constrains its choices; (2) "Actions carry implicit decisions, and conflicting decisions carry bad results" — every action a subagent takes silently commits to assumptions the other subagents never see.

Their illustration: building Flappy Bird via two subagents produced a Super Mario Bros. background from one and a visually inconsistent bird from the other. Nothing errored. The failure surfaced only at integration, where the parent agent faced work products that could not be reconciled — the expensive part was not the wrong output but that it was discovered last.

RESOLVED 2026-07-26 — Cognition has since narrowed this themselves. Their April 2026 follow-up ("Multi-Agents: What's Actually Working") keeps the mechanism but restricts its blast radius: the failure is specific to CONCURRENT WRITES, not to multi-agent per se. Their revised rule is that multi-agent systems work "when writes stay single-threaded and the additional agents contribute intelligence rather than actions." Under that constraint they now run several multi-agent patterns in production. So the 2025 post should no longer be read as a general case against subagents — read it as the case against parallel agents that each mutate shared artifacts, which is the part that survived.

What did NOT get walked back: the claim that cross-agent communication does not happen by default. The 2026 post still reports agents assuming they share state with their children when they do not, and attributes it to models not having been trained in environments where such communication was required.

Also worth holding alongside it: the frameworks the 2025 post argues against by name (OpenAI Swarm, Microsoft AutoGen) are not the shape the question takes now, since current models spawn subagents natively without any framework being chosen.
