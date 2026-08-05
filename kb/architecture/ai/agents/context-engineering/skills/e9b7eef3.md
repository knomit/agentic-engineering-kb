---
type: pattern
domain: [agentic-engineering, context-engineering, architecture, security, tools]
confidence: 0.85
sources: 1
entities: [Anthropic, Agent Skills, SKILL.md, progressive disclosure, MCP, supply chain, open standard]
refs: ['https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills']
---
# Agent Skills invert context economics — but the description is the entire selection surface, and the bundle is executable supply chain

Structurally a Skill is just a directory with a SKILL.md whose YAML frontmatter carries `name` and `description`, plus arbitrary bundled files. Loading is three-level progressive disclosure, verbatim from the source:

1. "At startup, the agent pre-loads the `name` and `description` of every installed skill."
2. "If Claude thinks the skill is relevant to the current task, it will load the skill by reading its full `SKILL.md` into context."
3. Skills can "bundle additional files within the skill directory and reference them by name from `SKILL.md`... Claude can choose to navigate and discover only as needed."

The economic consequence Anthropic emphasises is that bundled context is effectively unbounded, because an agent with a filesystem and code execution can pull files on demand rather than holding them resident. This is the same manoeuvre as deferring MCP tool definitions behind a search tool: pay for a pointer, not the payload.

**IT IS NO LONGER AN ANTHROPIC-ONLY FORMAT.** The page carries an update notice dated **18 December 2025**: Agent Skills were published as an **open standard for cross-platform portability**. This changes the build-vs-wait calculus — a skill authored today is a portable artifact rather than a bet on one vendor's harness, and it makes third-party skill distribution (and therefore the supply-chain risk below) a cross-ecosystem concern rather than a Claude-specific one. Original article published 16 October 2025.

Two consequences that matter more than the structure and are easy to miss:

**THE DESCRIPTION IS THE WHOLE SELECTION SURFACE.** Level 1 is all the model ever sees when deciding whether the skill applies, so a skill with excellent content and a vague description is dead weight — it costs resident tokens and never fires. This puts skill descriptions under exactly the same rule as tool descriptions: they compete with their siblings, so lead with the distinguishing trigger condition rather than restating the skill's name. A skill that never loads and a skill that loads on the wrong task are both description bugs, not content bugs.

**A SKILL IS AN EXECUTABLE SUPPLY-CHAIN BOUNDARY.** Anthropic states that "malicious skills may introduce vulnerabilities in the environment where they're used or direct Claude to exfiltrate data and take unintended actions." Unlike a prompt snippet, a skill bundles code and instructions that enter the agent's context and execution environment on the agent's own initiative. Installing a third-party skill is therefore closer to adding a dependency than to pasting a prompt: audit skills from untrusted sources, inspect the code dependencies they carry, and monitor outbound network connections made by bundled code. Open-standard portability widens the blast radius here — the same bundle now runs across harnesses with different sandboxing guarantees.

Anthropic positions skills as complementary to MCP rather than a replacement — skills "complement Model Context Protocol (MCP) servers by teaching agents more complex workflows that involve external tools and software" — and as an alternative to fine-tuning for procedural knowledge, since they are composable and loadable at runtime with no retraining.

What the article still does NOT give, re-confirmed 2026-07-30: **any token budget, file-size cap, or numeric threshold for skill or bundle size.** If you need a limit, measure it; there is no published one to cite. For an empirical anchor, one independent optimization study converged on skill files of ~920 tokens median — evidence about what works, not a specification.
