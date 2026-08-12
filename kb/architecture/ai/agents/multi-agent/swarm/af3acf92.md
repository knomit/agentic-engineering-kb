---
type: pattern
domain: [agentic-engineering, multi-agent, architecture, security, guardrails]
confidence: 0.75
sources: 1
entities: [OWASP, swarm architecture, central orchestrator, decentralized identity, verifiable credentials, agent reputation]
refs: ['https://genai.owasp.org/resource/securing-agentic-applications-guide-1-0/', 'https://genai.owasp.org/download/49059/?tmstv=1753666640', 'kb://bc6eac5f37df/kb/decisions/ai/agents/multi-agent/f7dee43a.md', 'kb://bc6eac5f37df/kb/decisions/ai/agents/multi-agent/delegation-style/c1bbf73f.md']
---
# A swarm has no in-band guidepost for "correct action" or "trusted collaborator" — both must be assigned from outside the agentic flow, and self-expansion gated on a human

OWASP's securing-agentic-applications guide treats swarm architectures separately from orchestrator-based multi-agent systems, and names the property that forces the separation: **a swarm does not necessarily have an easy guidepost for what the correct action is, or for which collaborators are trustworthy.** In an orchestrator design both questions have a natural home — the orchestrator holds the plan and the roster. Remove it and nothing in the system is positioned to answer them, because every participant is a peer with the same standing to assert an answer.

The guide's consequence is a placement rule rather than a mechanism: **assign trust and action authority outside the agentic flow.** Whatever decides that an action is correct, or that a peer may be collaborated with, must not itself be a participant in the peer conversation — otherwise it is subject to the same manipulation as everything else in that channel, and a compromised or injected peer can vote itself trustworthy.

**THE SECOND RULE IS THE ONE PEOPLE SKIP: limit or prevent the swarm from adding new agents without human guidance.** Self-expansion is usually presented as a swarm's strength — spawn a specialist when the work needs one. It is also the step that lets a compromised participant introduce a collaborator, and there is no orchestrator to refuse. If the roster can grow from inside the flow, every other trust control in the system is downstream of an unauthenticated decision.

**WHAT THE GUIDE PROPOSES TO FILL THE GAP**, and its status matters: decentralised identifiers (W3C DIDs) giving each agent a persistent verifiable identity, verifiable credentials proving specific capabilities or authorisations, and decentralised reputation scores accumulated from behaviour and used for collaboration decisions. These are the right shape — identity and capability assertions that are verifiable without a central authority, which is what a swarm needs by definition — but they are standards and proposals, not shipped infrastructure. Treat them as the target architecture, and in the meantime accept that the practical way to get a trustworthy answer to "is this action correct" in a swarm is a component that is not in the swarm.

**HOW THIS SHOULD AFFECT THE ARCHITECTURE CHOICE.** This pack already records that the deciding condition between multi-agent and single-threaded is whether subtask outputs must be mutually consistent, and between manager and handoff styles whether control returns to the caller. Add this: a swarm additionally requires you to build out-of-band trust and action arbitration that an orchestrator design gets for free. That cost is rarely counted when swarm is chosen for its autonomy, and it is the reason a swarm is a poor default for anything with a security boundary in it.
