---
type: synthesis
domain: [agentic-engineering, architecture, context-engineering, cost, multi-agent, tools]
confidence: 0.8
sources: 1
evidence_weight: 0.7101449275362319
entities: [orchestrator-worker, programmatic tool calling, BrowseComp, allowed_callers, context window]
refs: [kb/architecture/ai/agents/multi-agent/19ed6273.md, kb/architecture/ai/agents/tools/code-execution/fc911d9c.md]
---
# Two shipped answers to 'this does not fit in one context window' — spend 15x on parallel windows, or spend 37% less by never letting intermediates in — and knowable control flow decides which

When a task's data exceeds one context window, two architectures are shipped by major vendors and they move cost in OPPOSITE directions. Choosing between them by intuition tends to pick the expensive one, so the deciding condition is worth stating.

OPTION A — MULTI-AGENT: BUY MORE CONTEXT WINDOWS, PAY ~15x. An orchestrator-worker research system (Opus 4 lead spawning Sonnet 4 subagents) beat single-agent Opus 4 by 90.2% on an internal research eval. The price is token volume: agents run roughly 4x a chat interaction, multi-agent roughly 15x. The causal finding is the important part — on BrowseComp, TOKEN VOLUME ALONE explained about 80% of performance variance, with tool-call count and model choice another ~15%. So the architecture wins by buying a way to SPEND MORE TOKENS IN PARALLEL across separate context windows, not by reasoning better.

OPTION B — PROGRAMMATIC TOOL CALLING: KEEP THE INTERMEDIATES OUT, PAY LESS. The model writes code that orchestrates many tool calls — real loops, conditionals, intermediate processing — and that program runs in a sandbox. Only the program's FINAL output enters the conversation; intermediate tool results never reach the model's context at all. Measured on Anthropic's implementation: a complex research task fell from 43,588 to 27,297 tokens (~37% fewer), knowledge retrieval accuracy rose 25.6% -> 28.5%, GAIA 46.5% -> 51.2%. Note the accuracy gains are MODEST — the dominant benefit is token and context economy, not capability. The canonical case is fetching 500 rows to compute one aggregate: direct calling pays for all 500 rows in context and again every subsequent turn; the program pays for the aggregate.

THE DECIDING VARIABLE IS WHETHER THE CONTROL FLOW IS KNOWABLE IN ADVANCE.
- If you can write down the sequence — three or more DEPENDENT tool calls, large-dataset aggregation, wide parallel operations (checking 50+ endpoints), filtering or transforming before the model sees anything — write it as code. Option B.
- If the agent genuinely must re-evaluate after each result (adaptive search), a program just guesses. Both vendors say DIRECT calling remains the recommended baseline, and single-tool invocations need neither option.
- If the INFORMATION ITSELF exceeds one window and subtasks genuinely parallelize, that is Option A's stated boundary — worth it when task value justifies ~15x.

A SECOND DISCRIMINATOR THAT CUTS THE OTHER WAY, and is easy to miss: Option B is precisely WRONG when the model SHOULD see and reason about all intermediate results. Hiding them is the whole mechanism, so if the reasoning depends on them you have removed the thing that makes the run work.

OPTION A'S EXPLICIT ANTI-CONDITIONS: unsuitable when subtasks need shared context or have heavy interdependencies — most coding tasks are named as falling on that side of the line. And the corollary the numbers force: upgrading the model beat doubling the token budget on the older model, so reach for multi-agent only AFTER model choice is maxed.

OPTION B'S SHARP CONSTRAINTS, worth knowing before designing around it: OpenAI's runtime (hosted V8) is fresh and isolated per program — no Node.js, no package installation, no network, no filesystem, no console, no persistence between programs. Client-owned functions still execute in YOUR application, so results must be fed back explicitly. MCP tools carrying a `require_approval` policy PAUSE the program mid-execution, so a safety gate becomes a latency cliff inside a loop. Deferred tools are invisible to a program unless loaded first. With `store: false` you must replay every output item including program and reasoning items. Anthropic's Python runtime has tools opt in via `allowed_callers: ["code_execution_20250825"]`. A second, less obvious benefit: because filtering happens in the execution environment, PII can be tokenized so real values flow between systems without passing through the model — a privacy control as much as a cost one. The trade is that you now need a sandbox with real isolation, and a model writing code is more expressive and correspondingly harder to constrain.

WHAT THIS DOES NOT MEAN. Not a claim that these are mutually exclusive — nothing stops a subagent from using programmatic tool calling. Not a claim Option B always saves tokens: both vendors state the saving DEPENDS ON THE TASK and is not guaranteed. And the +90.2% figure is anchored to Claude Opus 4 leading Claude Sonnet 4, both several generations superseded; the single-agent baseline has moved the most, so treat the margin as a point-in-time result and expect it to have narrowed. What does NOT depend on model generation is the token-volume-explains-the-variance finding and both sets of boundary conditions. One material change since publication: current models orchestrate subagents NATIVELY and over-delegate without being asked, so Option A is no longer a purely deliberate architectural choice — the first tuning problem is now damping delegation rather than enabling it.
