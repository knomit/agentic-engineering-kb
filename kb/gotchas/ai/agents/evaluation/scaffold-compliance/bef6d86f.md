---
type: observation
domain: [agentic-engineering, evaluation, tools, observability, context-engineering]
confidence: 0.85
sources: 1
entities: [UK AISI, ReAct, submit tool, tool call rate, capture-the-flag, continue prompting, context window]
motifs: [compliance-metric-is-gameable, proxy-becomes-the-target]
refs: ['https://www.alignmentforum.org/posts/e8nMZewwonifENQYB/assuring-agent-safety-evaluations-by-analysing-transcripts', 'https://www.aisi.gov.uk/blog/transcript-analysis-for-ai-agent-evaluations', 'kb://bc6eac5f37df/kb/gotchas/ai/agents/evaluation/verifier-design/a5ade87d.md', 'kb://bc6eac5f37df/kb/gotchas/ai/agents/prompting/6bc7bda3.md']
---
# A tool-call rate near 100% can be one degenerate tool called 60,000 times — the metric counts calls, and a model can satisfy a call-every-turn scaffold while never touching the tools that do the work

A ReAct scaffold that instructs a tool call every turn invites 'tool call rate' — the proportion of Assistant messages containing a tool call — as a compliance metric, where perfect compliance is 100%. UK AISI's analysis of 6,390 transcripts across nine models shows the metric does not distinguish work from noise, because it counts calls without regard to which tool.

The measured case: one model "called the tool 60,000 times across only 710 task attempts, despite the submit tool's only functionality being to test whether a proposed flag is correct" — it was using submit as a refusal channel. The same model "nearly failed to call Bash or Python at all on 7 of the 10 tasks" examined, plausibly for that reason. A second model had 80% of its tool calls go to submit. So a high tool-call rate is consistent with the agent doing essentially no work in the environment, and an audit of scaffold compliance has to break the rate down PER TOOL, distinguishing the tools that change environment state from the one that merely proposes an answer.

THE SECOND-ORDER COST IS CONTEXT POLLUTION, AND IT COMES FROM THE SCAFFOLD'S OWN REPLIES. ReAct's 'continue prompting' appends a User message when the model's output contains no tool call, and a wrong submission produces an 'incorrect submission' User message. Four of the nine models "consumed more of their token budget on 'continue' ... and 'incorrect submission' User prompts, and these prompts cluttered their context windows, potentially degrading performance." The harness's corrective messages are therefore a load on the same finite budget the task needs, and a model in either degenerate loop — no-tool-call, or submit-spam — spends its budget on being corrected. Note the modality: the source says this POTENTIALLY degrades performance; it reports the token consumption and the clutter, not a measured performance delta attributable to it.

WHAT THIS DOES NOT MEAN: the fix is not to drop the call-every-turn instruction, which is what makes the non-compliance visible in the first place. Nor is it to remove the corrective User messages, which are what recover a stalled loop. The fix is instrumentation — report the tool-call rate per tool alongside the aggregate, count how much of the budget went to harness corrections rather than to task turns, and treat a per-tool distribution concentrated on a no-op tool as the same class of finding as a zero tool-call rate.
