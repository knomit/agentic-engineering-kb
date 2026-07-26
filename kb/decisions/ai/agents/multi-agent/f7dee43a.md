---
kind: pragmatic
type: heuristic
domain: [agentic-engineering, multi-agent, architecture]
confidence: 0.75
sources: 2
entities: [Anthropic, Cognition, orchestrator-worker]
refs: ['https://www.anthropic.com/engineering/multi-agent-research-system', 'https://cognition.com/blog/dont-build-multi-agents']
---
# Multi-agent vs single-threaded: the deciding condition is whether subtask outputs must be mutually consistent

Anthropic reports +90.2% from an orchestrator-worker multi-agent system; Cognition argues subagents are structurally unsound and recommends a single linear agent. Both are right within their conditions, and the conditions are what matters.

Multi-agent pays when subtasks are READ-ONLY and independently verifiable — search, research, breadth-first enumeration. Each worker returns findings; findings merge by concatenation; a worker's wrong assumption costs one worker's tokens and is visible in its own output. Context isolation is the product being bought.

Multi-agent fails when subtasks must produce artifacts that fit together — code, schemas, designs. There, every action encodes implicit decisions the siblings cannot see, so divergence is silent until integration, when it is most expensive to fix. Note the two sources agree on this line: Anthropic independently names shared-context and heavily-interdependent work, and coding specifically, as unsuitable, which is exactly Cognition's example.

So the decision rule is not "is the task big" or "is it parallelizable" — plenty of incompatible work parallelizes fine. Ask whether two workers can make different reasonable assumptions and both be locally correct. If yes, stay single-threaded and compress context instead of forking. Also weigh the ~15x token cost, which only high-value tasks repay.
