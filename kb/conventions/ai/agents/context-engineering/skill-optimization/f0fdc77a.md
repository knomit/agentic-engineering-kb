---
type: process
domain: [agentic-engineering, context-engineering, prompting, evaluation, coding-agents]
confidence: 0.75
sources: 1
entities: [Microsoft Research, SkillOpt, SKILL.md, SpreadsheetBench, OfficeQA, GPT-5.5, Claude Code, Codex, textual learning rate]
motifs: [conditioning-substitutes-for-capacity]
refs: ['https://www.microsoft.com/en-us/research/blog/skillopt-agent-skills-as-trainable-parameters/']
---
# Agent skill files can be optimized like parameters instead of hand-edited — and a trained skill on a smaller model beat an untrained larger one

Microsoft Research's SkillOpt treats an agent's skill file (the instruction artifact, not the weights) as a **learnable parameter optimized against held-out validation data**, with the target model frozen throughout. The loop borrows its structure from gradient descent without touching weights:

1. **Forward pass** — the frozen target model runs tasks using the current skill file.
2. **Backward pass** — a *separate optimizer model* reads the execution trajectories and extracts patterns from what succeeded and what failed.
3. **Update** — the optimizer proposes small add/delete/replace text edits, bounded by a **"textual learning rate"** budget.
4. **Validation gating** — a candidate skill is adopted only if it beats the incumbent on held-out data.
5. **Rejected-edit feedback** — edits that failed the gate inform later proposals.
6. **Slow/meta updates** — epoch-wise consolidation of longer-horizon lessons.

**The measured results, across six benchmarks, seven models (GPT-5.5 down to Qwen3.5-4B), and three harnesses (direct chat, Codex, Claude Code):**

- Best-or-tied in **all 52 evaluation cells** against human-written, one-shot-LLM, Trace2Skill, TextGrad, GEPA and EvoSkill baselines.
- GPT-5.5: **+23.5 points absolute** across the six benchmarks (58.8 → 82.3).
- Procedural tasks gain most: SpreadsheetBench **41.8 → 80.7**, OfficeQA **33.1 → 72.1**.
- **A trained skill substituted for model scale:** GPT-5.4-mini with an optimized skill scored **64.3**, above GPT-5.4 with no skill at **59.7**.
- **Cross-harness transfer worked:** a spreadsheet skill trained under Codex, moved to Claude Code, lifted that baseline from **22.1 to 81.8**.

**Why the mechanism matters more than the headline number.** The two components doing the work are *step-size control* and *validation gating* — precisely what hand-editing an instruction file lacks. Manual prompt maintenance has no bound on edit size and no held-out check, so it accumulates drift, and revisions that read as obviously reasonable silently degrade task performance. If you are not going to run SkillOpt itself, those two properties are the transferable lesson: bound the size of each edit, and gate every change on held-out tasks rather than on whether it sounds right.

**Conditions where this does not apply — stated by the authors, and load-bearing:**

- It **requires an automatic evaluator or reliable verifier**. With no programmatic success signal there is no backward pass, and the method simply does not run. This is the same precondition that gates every other optimization loop in this pack.
- Final skill files stay **compact — ~920 tokens median**. Tasks whose procedural knowledge will not compress to roughly that size are outside what was demonstrated.
- Transfer was shown across model scales, harnesses, and **related** tasks. Unrelated-domain transfer is not evidenced.
- It optimizes **instructions, not reasoning capability**. It cannot buy a competence the model lacks; the SpreadsheetBench and OfficeQA gains are procedural tasks, where knowing the procedure is most of the job.

Treat the specific figures as one lab's published measurement rather than settled: they are single-source, and the comparison baselines are chosen by the authors.
