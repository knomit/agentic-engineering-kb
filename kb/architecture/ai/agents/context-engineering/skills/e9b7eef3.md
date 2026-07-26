---
type: pattern
domain: [agentic-engineering, context-engineering, architecture, security, tools]
confidence: 0.75
sources: 0
entities: [Anthropic, Agent Skills, SKILL.md, progressive disclosure, MCP, supply chain]
refs: ['https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills']
---
# Agent Skills invert context economics — but the description is the entire selection surface, and the bundle is executable supply chain

Structurally a Skill is just a directory with a SKILL.md whose YAML frontmatter carries `name` and `description`, plus arbitrary bundled files. Loading is three-level progressive disclosure:

1. At startup, ONLY name and description enter the system prompt.
2. When the agent judges the skill relevant, it reads the whole SKILL.md.
3. Bundled files (reference.md, scripts, data) are read only when the agent decides it needs them.

The economic consequence Anthropic emphasises is that bundled context is effectively unbounded, because an agent with a filesystem and code execution can pull files on demand rather than holding them resident. This is the same manoeuvre as deferring MCP tool definitions behind a search tool: pay for a pointer, not the payload.

Two consequences that matter more than the structure and are easy to miss:

THE DESCRIPTION IS THE WHOLE SELECTION SURFACE. Level 1 is all the model ever sees when deciding whether the skill applies, so a skill with excellent content and a vague description is dead weight — it costs resident tokens and never fires. This puts skill descriptions under exactly the same rule as tool descriptions: they compete with their siblings, so lead with the distinguishing trigger condition rather than restating the skill's name. A skill that never loads and a skill that loads on the wrong task are both description bugs, not content bugs.

A SKILL IS AN EXECUTABLE SUPPLY-CHAIN BOUNDARY. Anthropic states plainly that a malicious skill can cause Claude to exfiltrate data and take unintended actions. Unlike a prompt snippet, a skill bundles code and instructions that enter the agent's context and execution environment on the agent's own initiative. Installing a third-party skill is therefore closer to adding a dependency than to pasting a prompt: audit skills from untrusted sources, inspect the code dependencies they carry, and monitor outbound network connections made by bundled code.

Anthropic positions skills as complementary to MCP rather than a replacement — MCP supplies the tool connections, skills teach the workflow that uses them — and as an alternative to fine-tuning for procedural knowledge, since they are composable and loadable at runtime with no retraining.

What the article does NOT give: any token budget, file-size cap, or numeric threshold for skill or bundle size. If you need a limit, measure it; there is no published one to cite.
