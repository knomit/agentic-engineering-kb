---
type: observation
domain: [agentic-engineering, evaluation, llm-judge, benchmarks, reliability]
confidence: 0.7
sources: 1
entities: [Anthropic, Alignment Science, Anthropic Fellows Program, TASTE, Fable 5, LLM-as-judge, pairwise preference]
motifs: [shared-input-confounds-comparison]
refs: ['https://alignment.anthropic.com/2026/taste/', 'kb://bc6eac5f37df/kb/gotchas/ai/agents/evaluation/llm-judge/38c06627.md', 'kb://bc6eac5f37df/kb/gotchas/ai/agents/evaluation/judge-calibration/human-baseline/0cc69d27.md']
---
# An LLM judge comparing two completions of the SAME prompt drifts toward scoring prompt-adherence; the same judge scores higher on cross-prompt pairs

On TASTE, a 92-pair benchmark of expert preferences over AI-safety research proposals, the best model (Fable 5) reached 60% agreement with human labels overall but 69% on the 74 pairs drawn from *different* motivating-question prompts. The authors' stated reading of the gap: models over-focus on how well a proposal answers the motivating question when both candidates were generated from the same prompt.

**Why this matters more than the benchmark does.** The configuration where the confound is strongest — two candidate outputs generated from one prompt, judge picks the better — is the default LLM-judge setup in production A/B evaluation and in preference-data collection. When both candidates address the same question, relevance to that question is nearly constant between them and carries no signal, yet it is the dimension the judge weights. The judge then reports a quality preference that is substantially a prompt-adherence preference, and it will look consistent and confident while doing so.

**Operational consequence.** Treat same-prompt pairwise scores as a weaker measurement than cross-prompt ones, and do not read a judge's same-prompt win rate as a quality estimate without a check. Where the task allows it, validating a judge on pairs drawn from different prompts separates the two dimensions. The source does not establish a remedy: its alternative setup — scoring each candidate individually and deriving the preference from the scores — is described as *tougher* for models, not as a correction for this confound.

**What is not established.** This is one within-model contrast on a 92-pair benchmark, and the paper reports per-model confidence intervals of roughly ±10 percentage points; 60 versus 69 is suggestive rather than resolved. The mechanism is the authors' interpretation of the gap, offered as "some evidence", not a controlled ablation.
