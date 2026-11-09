---
type: observation
domain: [agentic-engineering, evaluation, benchmarks, llm-judge, conventions]
confidence: 0.8
sources: 1
entities: [OpenAI, ROUGE-L, G-Eval, context recall, context precision, pass/fail threshold, held-out set]
motifs: [illustrative-value-becomes-standard, copyability-outruns-provenance]
refs: ['https://developers.openai.com/api/docs/guides/evaluation-best-practices', 'kb://bc6eac5f37df/kb/conventions/ai/agents/evaluation/datasets/41a5dc4e.md']
---
# The worked eval thresholds in vendor documentation carry no stated source, validation or sample-size rationale — ROUGE-L 0.40, 80% coherence, 0.85 recall and a 1,000-example set are illustrations, and reading them as calibrated gates is the error

OpenAI's evaluation guidance contains concrete-looking acceptance criteria inside its worked examples. For a transcript-summarisation task: "On a held-out set of 1000 reference transcripts → summaries, the implementation should achieve a ROUGE-L score of at least 0.40 and coherence score of at least 80% using G-Eval." For retrieval-augmented question answering: "Context recall of at least 0.85, context precision of over 0.7, and 70+% positively rated answers."

THE PROBLEM IS NOT THE NUMBERS, IT IS THEIR PROVENANCE. The page gives no source, no derivation and no validation for any of them, and no general sample-size guidance anywhere — the 1,000 figure appears only inside that one example. They are the shape of a specification, filled in with plausible values, and they are the most copyable thing on the page.

CONSEQUENCE. A borrowed threshold imports a decision someone else did not make. The number that matters for your system is the one at which the metric separates outputs your reviewers accept from ones they reject, which has to be found on your own labelled data; until then a threshold is a placeholder and should be written down as one. Quoting a vendor page as the authority for a gate is how an arbitrary number acquires the appearance of a standard.

WHAT THE SAME PAGE DOES GET RIGHT, and it is the part worth copying instead: the guidance to "Include a pass/fail threshold in addition to the numerical score" for human review, and the judge-calibration order — "validate agreement against your human labels before optimizing for cost or latency", scaling up only once the judge "consistently agrees with human annotations". That ordering is a procedure you can follow; note that the page names no agreement metric for it.

SCOPE. This is an observation about one vendor documentation page's epistemic status, not a claim that these metrics are bad or that the values are wrong. Several of its other recommendations — using the most capable available judge, controlling for response length, preferring pairwise comparison or classification over open-ended generation — are stated without data on that page too, but are independently corroborated elsewhere; the thresholds are not.
