---
type: observation
domain: [agentic-engineering, evaluation, governance, observability, benchmarks]
confidence: 0.85
sources: 1
entities: [OpenAI, Apollo Research, GPT-6 Astra, GPT-5.5, GPT-5.6 Sol, evaluation awareness, third-party evaluation, chain-of-thought access, system card]
motifs: [access-determines-baseline, limited-window-weakens-null]
refs: ['https://deploymentsafety.openai.com/gpt-6-astra/safeguards', 'kb://bc6eac5f37df/kb/decisions/ai/agents/evaluation/eval-awareness-measurement/0c3c2d6a.md', 'kb://bc6eac5f37df/kb/gotchas/ai/agents/evaluation/eval-awareness/2d280a46.md', 'kb://bc6eac5f37df/kb/invariants/ai/agents/evaluation/system-card-citation/17b9318f.md']
---
# A third-party evaluator benchmarked the new model's evaluation-awareness rate against a two-generations-old baseline because it was not granted chain-of-thought access to the immediate predecessor — the comparator was chosen by access, not by relevance

In OpenAI's GPT-6 Astra safeguards card, Apollo Research reports verbalized evaluation awareness — the model stating in its reasoning that it is being evaluated — at "41.1% of Astra samples" at xhigh reasoning effort "compared with 27.7% for GPT-5.5 at the same effort", and 50.6% for Astra at max reasoning effort.

THE COMPARATOR IS GPT-5.5, NOT THE MODEL ASTRA ACTUALLY SUCCEEDS. The card gives the reason in the same paragraph: "Apollo provided comparative rates with GPT-5.5 as they did not have chain of thought access to GPT-5.6-Sol." The baseline in a published third-party comparison can therefore be set by what the evaluator was granted access to rather than by which model is the relevant predecessor, and the resulting delta spans two releases rather than one. A reader computing "evaluation awareness rose from 27.7% to 41.1% in this generation" would be attributing to one release a change measured across two.

THE CONSEQUENCE FOR READING ANY THIRD-PARTY EVALUATION IN A VENDOR CARD: the comparator is a methodological choice that may be access-constrained, and the constraint is often disclosed in a subordinate clause rather than in the figure caption. Check which model the baseline column actually is before quoting a delta, and check whether the card says why that model was chosen.

THE EVALUATOR ALSO DISCLAIMS ITS OWN NULL. Apollo's stated conclusion is that "given the higher rates of eval awareness and limited evaluation window, low rates of misbehavior here do not provide substantial evidence about the model's alignment or misalignment." Two reasons are given and they are independent: high evaluation awareness, and a limited evaluation window. A low misbehaviour rate from this setup is therefore not being offered as evidence of alignment by the party that measured it, and should not be cited as such by anyone else. Note that this is the opposite operational stance to the Anthropic result recorded in [[kb/decisions/ai/agents/evaluation/eval-awareness-measurement/0c3c2d6a.md]], where verbalized awareness did not correlate with misalignment score across 1,300 seeds; the conditions separating the two positions are set out there.

NOT ESTABLISHED: the card does not give Astra's rate at the effort level where GPT-5.6 Sol's rate would have been measured, does not state the size of the evaluation window Apollo calls limited, and does not report whether the access limitation was a policy or a timing constraint.
