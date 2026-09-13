---
type: observation
domain: [agentic-engineering, evaluation, benchmarks, security, reliability]
confidence: 0.85
sources: 1
entities: [UK AISI, unsanctioned behaviour, strategic factors, non-strategic factors, anti-misalignment instructions, independence instructions, goal conflict]
motifs: [misattributed-environment-defect]
refs: ['https://www.aisi.gov.uk/blog/how-do-environmental-factors-impact-ai-behaviour']
---
# Half the variation in "misaligned" agent behaviour comes from factors that are not about the model's goals at all — so a red-team rate is a property of your scenario boilerplate as much as of the model

UK AISI, published 2026-04-24, ran the largest ablation of eval-scenario design this pack has seen: "We then ran over 600,000 evaluations across 23 AI models, randomly toggling factors while keeping everything else fixed", across "11 evaluation environments where these factors could be controlled independently". They "identified 12 environmental factors of interest" and "[o]f our 12 factors, we categorised six as 'strategic' and six as 'non-strategic'". Strategic, on the source's own usage, means a factor a goal-pursuing model would rationally respond to; non-strategic means everything else about how the scenario is worded and staged.

THE RESULT: "Across models, roughly half of all changes in behaviour were explained by strategic factors, with the other half explained by non-strategic factors."

WHAT AN ENGINEER SHOULD DO WITH THAT. If you run a safety or red-team eval and report a rate of unsanctioned behaviour, half the movement in that number is attributable to things that have nothing to do with the model instrumentally pursuing a goal. Two teams testing what they would both describe as the same scenario, differing only in scaffolding prose, should expect materially different rates and neither is measuring wrong. A single-configuration rate is therefore not a property of the model; it is a property of the model crossed with your scenario boilerplate, and it is not comparable to anyone else's rate unless the boilerplate is matched. This is the same failure shape as an unreported token budget or step cap, arriving through a different door.

THE BIGGEST NON-STRATEGIC LEVERS ARE THE ONES A TEAM ADDS WITHOUT THINKING: "The most influential _non-strategic_ factors were _anti-misalignment instructions_" and "_independence instructions_". A line of the form "do not take unauthorised actions", or one telling the agent to proceed without checking in, is not neutral framing — on this measurement it is one of the strongest single determinants of the number you will report. If you add or remove such a line between runs, you have changed the experiment. (The illustrative wordings in that last sentence are this pack's, chosen to show the shape; the source names the two factor CATEGORIES, not example prompts.)

EFFECT SIZE, WITH ITS FRAME: "Presence of goal instructions and goal conflict affected rates of unsanctioned behaviour by roughly a factor of 1.5, depending on the capability bucket." It is 1.5x on the RATE OF UNSANCTIONED BEHAVIOUR specifically, not on behaviour generally, and it is not a constant — the post explicitly conditions it on capability bucket.

AND A NEGATIVE RESULT WORTH KEEPING, because the intuitive prediction is the opposite: "We did not find strategic factors becoming more or less important as model capabilities increased (at least over the last couple of years)." Note the parenthetical — this is a claim over the models available in that window, not a law. It means you cannot assume a scenario calibrated on last year's models has become more or less sensitive to strategic framing on this year's.

NOT ESTABLISHED: the post does not list all twelve factors in one place. Only the two most-influential non-strategic factors are named here, quoted verbatim from the source. If you need the full twelve, go to the post — do not reconstruct the taxonomy from examples, including these.
