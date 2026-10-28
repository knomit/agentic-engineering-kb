---
type: observation
domain: [agentic-engineering, operations, cost, observability, model-selection]
confidence: 0.75
sources: 1
entities: [OpenAI, cookbook, model routing, Batch API, output cap, reasoning tokens, prompt caching]
motifs: [proxy-diverges-from-target, hidden-tokens-in-budget]
refs: ['https://developers.openai.com/cookbook/examples/agent_optimization/optimizing_agents_for_cost_and_quality', 'kb://bc6eac5f37df/kb/decisions/ai/agents/model-selection/total-cost/26e77a95.md']
---
# Two of four optimization rounds cut cost while raising total tokens, so a token-count dashboard is not a cost dashboard

In OpenAI's cost-and-quality cookbook, two of the four optimization rounds moved cost and token count in OPPOSITE directions. Routing raised mean total tokens by 106 and still cut cost, because the extra tokens were spent on cheaper models. Splitting real-time from follow-up work lowered synchronous tokens but raised total tokens by 290, because work moved to the background path rather than disappearing — the page is explicit that moving work off the synchronous path still counts its tokens and its Batch cost.

The consequence for instrumentation: a dashboard that tracks tokens per request cannot tell you whether an optimization worked, and can report a regression for a change that halved the bill. Price out the configuration, per model and per token class, rather than counting tokens; the same divergence shows up across models in [[26e77a95]], where cache-read pricing made the cheaper-listed model nearly twice as expensive over 417 tasks.

A second counting trap on the same page: an output cap includes both visible and reasoning tokens, so a cap set from the length of the answer you want will truncate responses whose reasoning is long. The page's own instruction is to check for incomplete responses after setting one.

WHAT THIS DOES NOT MEAN: token counts are not useless — they are how you find what to change, and the same page's controls round cut mean tokens from 11,935 to 1,379 while cutting cost 87%. The claim is narrower: token count is a diagnostic, and only the priced configuration is the cost. These figures come from a dry-run simulation the page says is not a production benchmark.
