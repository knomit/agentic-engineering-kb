---
kind: pragmatic
type: heuristic
domain: [agentic-engineering, multi-agent, architecture]
confidence: 0.85
sources: 3
entities: [Anthropic, Cognition, orchestrator-worker, map-reduce-and-manage]
refs: ['https://www.anthropic.com/engineering/multi-agent-research-system', 'https://cognition.com/blog/dont-build-multi-agents', 'https://cognition.com/blog/multi-agents-working']
---
# Multi-agent vs single-threaded: the deciding condition is whether subtask outputs must be mutually consistent

Anthropic reports +90.2% from an orchestrator-worker multi-agent system; Cognition argued in 2025 that subagents are structurally unsound and recommended a single linear agent. Both are right within their conditions, and the conditions are what matters.

The sharpest available formulation of the line is Cognition's own 2026 revision: multi-agent works "when writes stay single-threaded and the additional agents contribute intelligence rather than actions." Test a proposed design by asking what each extra agent is allowed to MUTATE. If the answer is nothing — it reads, analyses, critiques, and returns findings to one writer — the pattern is sound. If two agents both produce artifacts that must later fit together, it is not.

This subsumes the earlier framing and is easier to apply. Multi-agent pays when subtasks are READ-ONLY and independently verifiable — search, research, breadth-first enumeration, review. Each worker returns findings; findings merge by concatenation; a worker's wrong assumption costs one worker's tokens and is visible in its own output. Context isolation is the product being bought.

Multi-agent fails when subtasks must produce artifacts that fit together — code, schemas, designs. There, every action encodes implicit decisions the siblings cannot see, so divergence is silent until integration, when it is most expensive to fix. The two sources agree on this line: Anthropic independently names shared-context, heavily-interdependent work, and coding specifically as unsuitable, which is exactly Cognition's example.

So the decision rule is not "is the task big" or "is it parallelizable" — plenty of incompatible work parallelizes fine. Ask whether two workers can make different reasonable assumptions and both be locally correct. If yes, keep one writer and give the others read-only roles, rather than either forking freely or refusing to fork at all.

The shape that remains viable when you do need scale is what Cognition calls "map-reduce-and-manage": a manager splits work, children execute, the manager synthesizes. Unstructured swarms with peer-to-peer negotiation remain impractical. Also weigh the ~15x token cost, which only high-value tasks repay.
