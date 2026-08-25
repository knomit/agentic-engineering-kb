---
kind: pragmatic
type: heuristic
domain: [agentic-engineering, multi-agent, architecture]
confidence: 0.85
sources: 3
entities: [Anthropic, Cognition, orchestrator-worker, map-reduce-and-manage, Smart Friend, SWE-1.5]
motifs: [wrong-deciding-variable]
refs: ['https://www.anthropic.com/engineering/multi-agent-research-system', 'https://cognition.com/blog/dont-build-multi-agents', 'https://cognition.com/blog/multi-agents-working']
---
# Multi-agent vs single-threaded: the deciding condition is whether subtask outputs must be mutually consistent

Anthropic reports +90.2% from an orchestrator-worker multi-agent system; Cognition argued in 2025 that subagents are structurally unsound and recommended a single linear agent. Both are right within their conditions, and the conditions are what matters.

The sharpest available formulation of the line is Cognition's own 2026 revision, quoted here in full because the qualifiers are load-bearing: "multi-agent systems work **best today** when writes stay single-threaded and the additional agents contribute intelligence rather than actions." Note what that is and is not — it is a claim about which designs work best under current model capability, not a condition for a multi-agent system working at all, and "today" is Cognition's own hedge. (An earlier revision of this fact quoted the sentence from "when writes…" onward and dropped "best today", which stated as a hard condition what the source stated as a current preference.)

Still, as a design test it is the most useful one available: ask what each extra agent is allowed to MUTATE. If the answer is nothing — it reads, analyses, critiques, and returns findings to one writer — the pattern is sound. If two agents both produce artifacts that must later fit together, expect trouble.

Multi-agent pays when subtasks are READ-ONLY and independently verifiable — search, research, breadth-first enumeration, review. Each worker returns findings; findings merge by concatenation; a worker's wrong assumption costs one worker's tokens and is visible in its own output. Context isolation is the product being bought.

Multi-agent struggles when subtasks must produce artifacts that fit together — code, schemas, designs. There, every action encodes implicit decisions the siblings cannot see, so divergence is silent until integration, when it is most expensive to fix. The two sources agree on this line: Anthropic independently names shared-context, heavily-interdependent work, and coding specifically, as unsuitable — which is exactly Cognition's example.

So the decision rule is not "is the task big" or "is it parallelizable" — plenty of incompatible work parallelizes fine. Ask whether two workers can make different reasonable assumptions and both be locally correct. If yes, keep one writer and give the others read-only roles, rather than either forking freely or refusing to fork at all.

**A SECOND CONDITION, and it is about model capability rather than task shape.** Cognition reports that their advisory pattern ("Smart Friend", where a stronger model advises a weaker primary) failed on capability asymmetry: SWE-1.5 as the primary "was not good enough", and "the gap…was too wide". The lesson generalises to any design where one agent's output must be acted on by another: if the consumer cannot evaluate the advice it is given, adding a smarter advisor does not raise the ceiling. Check the gap before assuming a stronger reviewer or planner will lift a weaker executor.

The shape that remains viable when you do need scale is what Cognition calls "map-reduce-and-manage": "a manager splits work, children execute, the manager synthesizes and reports back". Unstructured swarms fare worse — Cognition's reported symptom is "fragmented decisions" from context loss, and they name cross-agent communication as the primary remaining challenge even across the patterns that do work. Also weigh the ~15x token cost, which only high-value tasks repay.

VERIFIED 2026-08-12 against both Cognition posts: the map-reduce-and-manage definition, the single-threaded-writes sentence, and the capability-gap finding are quoted accurately above.
