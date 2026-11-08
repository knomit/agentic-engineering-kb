---
kind: pragmatic
type: heuristic
domain: [agentic-engineering, context-engineering, coding-agents, conventions, evaluation]
confidence: 0.8
sources: 1
entities: [Anthropic, Claude Code, Agent Skills, SKILL.md, product verification, Playwright, tmux, gotchas section, progressive disclosure]
motifs: [delta-from-default, failure-log-outranks-coverage]
refs: ['https://claude.dev/blog/lessons-from-building-claude-code-how-we-use-skills/', 'kb://bc6eac5f37df/kb/architecture/ai/agents/context-engineering/skills/e9b7eef3.md', 'kb://bc6eac5f37df/kb/conventions/ai/agents/coding-agents/verification/519ec939.md']
---
# A skill earns its context only where it contradicts the model's default — Anthropic's own nine-category breakdown puts the measurable quality gain on product-verification skills, and the highest-signal section of any skill on its accumulated gotchas

Claude Code's team describes its internal skill library as falling into nine categories — library and API reference, product verification, data fetching and analysis, business-process automation, code scaffolding and templates, code quality and review, CI/CD and deployment, runbooks, and infrastructure operations — and says the best skills fit cleanly into one of them, because an overly broad skill confuses the agent. Of the nine, the category they report as having had the most measurable impact on output quality is **product verification**: skills that teach the agent how to exercise and check the running product, typically driving Playwright or tmux.

The authoring advice points the same way at a finer grain. Do not state the obvious: write the information that pushes the model out of its default behaviour. And grow a gotchas section over time from the failure points you actually hit, which they call the highest-signal content in a skill. State goals and constraints rather than every step, because railroading the agent through a fixed procedure wastes the thing you are paying context for.

The unifying consequence for anyone writing one: a skill's worth is the delta between what the model does with it and what the model does without it, not its coverage of the subject. So the highest-value skill to write first is one that closes the loop the agent cannot close on its own — verification is that case, because an agent otherwise stops when the work merely looks done (see [[519ec939]]) — and the highest-value section to maintain is the one recording where it went wrong before.

WHAT THIS DOES NOT MEAN. "Product verification is the highest-impact category" is a statement about where this team measured a gain in their codebase, not a ranking that transfers unchanged: a team whose agents already have a reliable test command is buying something different from one whose product can only be checked through a browser. And it does not license writing a skill as a bare gotchas list — the description is still the entire selection surface that decides whether the skill is ever read at all ([[e9b7eef3]]), so a skill of pure gotchas with no trigger phrasing never fires.
