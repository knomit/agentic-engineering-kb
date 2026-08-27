---
type: observation
domain: [agentic-engineering, cost, reliability, prompting, evaluation]
confidence: 0.6
sources: 1
entities: [Anthropic, Claude Mythos, CryptanalysisBench, HAWK, AES-128, Simon Willison, long-horizon agents]
motifs: [effort-ends-before-exhaustion]
refs: ['https://simonwillison.net/2026/Jul/28/discovering-cryptographic-weaknesses-with-claude/']
---
# On genuinely hard open-ended problems the binding constraint was the model concluding it was impossible, not capability — 60 hours and ~$100k of prompting to two findings

Anthropic researchers ran Claude Mythos Preview on cryptanalysis of HAWK and a reduced-round AES-128 variant, producing two mathematical weaknesses (neither with practical implications for deployed systems) plus a benchmark, CryptanalysisBench, built with ETH Zurich, Tel Aviv University and the University of Haifa. Reported cost: roughly 60 hours of runtime and approximately $100,000 in API spend.

The engineering content is what the human time was spent on. Human involvement was minimal and was not technical direction — it was persistence management. The researchers' own framing: "the models tend to think it is impossible to solve so they don't try; they need a good amount of prompting." The other recurring intervention was redirecting the model toward findings worth publishing rather than superficial ones.

Two things to take from this. First, a cost anchor for open-ended long-horizon research agents: at this frontier, the unit of work is tens of hours and five figures for a small number of genuine findings, so the economics only close when the finding is worth that much — this is not a regime where you iterate cheaply. Second, a failure mode to design the harness against: on problems where the honest prior is that the task is intractable, premature abandonment is the dominant loss, and it presents as a confident, well-reasoned decision to stop rather than as an error. A harness for this class of work needs an explicit mechanism to keep the agent going past its own negative assessment, and a bar for what counts as a result, or the run terminates early with a plausible explanation of why the problem could not be solved.

Confidence is limited: this is a single reported research effort relayed second-hand via Simon Willison's write-up, with no token accounting published and no controlled comparison against a differently-prompted run.
