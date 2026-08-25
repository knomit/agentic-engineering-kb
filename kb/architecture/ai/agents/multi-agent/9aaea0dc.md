---
type: pattern
domain: [agentic-engineering, multi-agent, architecture]
confidence: 0.85
sources: 2
entities: [Cognition, Devin, single-threaded linear agent]
motifs: [context-assumed-not-transferred]
refs: ['https://cognition.com/blog/dont-build-multi-agents', 'https://cognition.com/blog/multi-agents-working']
---
# Cognition's case against multi-agent: dispersed context produces incompatible work products

Cognition (Devin) argued in June 2025 against subagent architectures on two stated principles, both quoted verbatim: (1) "Share context, and share full agent traces, not just individual messages" — passing a subagent only its task description, rather than the whole trace, starves it of the reasoning that constrains its choices; (2) "Actions carry implicit decisions, and conflicting decisions carry bad results" — every action a subagent takes silently commits to assumptions the other subagents never see.

Their illustration: building Flappy Bird via two subagents. One produced "a background that looks like Super Mario Bros"; the other produced "a bird, but it doesn't look like a game asset and it moves nothing like the one in Flappy Bird". Nothing errored. The failure surfaced only at integration, where the parent agent faced work products that could not be reconciled — the expensive part was not the wrong output but that it was discovered last.

NARROWED BY COGNITION THEMSELVES. Their April 2026 follow-up ("Multi-Agents: What's Actually Working") keeps the mechanism but restricts its blast radius to CONCURRENT WRITES rather than to multi-agent per se. The revised sentence, quoted in full because the qualifiers matter: "multi-agent systems work **best today** when writes stay single-threaded and the additional agents contribute intelligence rather than actions." That is a statement about which designs work best under current model capability — not a hard condition for working at all, and "today" is Cognition's own hedge. (A previous revision of this fact quoted the sentence from "when writes…" onward, dropping "best today" and thereby stating a preference as a rule. Corrected 2026-08-12.) Under that constraint Cognition now runs several multi-agent patterns in production, so the 2025 post should no longer be read as a general case against subagents — read it as the case against parallel agents that each mutate shared artifacts, which is the part that survived.

What did NOT get walked back: the claim that cross-agent communication does not happen by default. The 2026 post still reports that "Agents assume they share state with their children when they don't", and that such communication "doesn't happen by default, because models haven't been trained in environments where it needed to". Cognition names communication as the primary remaining challenge across even their successful patterns — so this is the open problem, not a solved one.

Also worth holding alongside it: the 2025 post argues by name against OpenAI's Swarm and Microsoft's AutoGen, which are not the shape the question takes now, since current models spawn subagents natively without any framework being chosen.

VERIFIED 2026-08-12: both 2025 principles, the Flappy Bird descriptions, the state-sharing sentence and the revised rule were re-checked against the two posts and are quoted accurately. Quotation boundaries clean.
