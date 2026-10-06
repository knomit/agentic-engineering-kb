---
type: pattern
domain: [agentic-engineering, architecture, security, training, guardrails, governance]
confidence: 0.75
sources: 1
entities: [Anthropic, Alignment Science, SGTM, Selective GradienT Masking, RMU, unlearning, data filtering, gradient masking, dual-use capabilities, mixture-of-experts]
motifs: [localization-enables-deletion, suppression-not-removal]
refs: ['https://alignment.anthropic.com/2025/selective-gradient-masking/', 'kb://bc6eac5f37df/kb/architecture/ai/agents/security/capability-access-control/5a36eb3b.md', 'kb://bc6eac5f37df/kb/gotchas/ai/agents/governance/control-substitution/077ce96e.md', 'kb://bc6eac5f37df/kb/architecture/ai/agents/security/permission-systems/89df351e.md']
---
# Localizing a capability into deletable parameters during training, then ablating them: seven times more fine-tuning resistance than post-hoc unlearning, for a 5% compute penalty, measured at 254M parameters

"Beyond Data Filtering: Knowledge Localization for Capability Removal in LLMs" (Anthropic Alignment Science, December 8, 2025) describes "Selective GradienT Masking (SGTM)": designate a subset of attention heads and MLP neurons in each transformer block as forget parameters; mask gradients so that labelled dangerous data updates only those parameters; let unlabelled data update all parameters, so that the labelled capability accumulates in the designated ones; ablate those parameters after training.

The numbers that decide anything, each with the comparison it is against:

- Against post-hoc unlearning, measured as resistance to adversarial recovery by fine-tuning rather than as an end-of-training score: "RMU ... recovered baseline biology performance in just 50 fine-tuning steps" while "SGTM required 350 steps", which the post states as "7x more resistant".
- Against data filtering, in both the strengths it was run at: "SGTM achieves a better retain/forget trade-off than both approaches" — weak filtering (the target domain only) and strict filtering (the target domain plus adjacent fields).
- Cost: "SGTM incurs a 5% compute penalty to achieve the same retain loss as standard training."

The scope is narrow in four ways the post states itself, and all four have to travel with the result. The removal experiment was "a 254M parameter model on English Wikipedia" removing biology knowledge. The scaling arm used "models from 8M to 64M parameters". "We only tested SGTM on relatively small models up to 254M parameters, and scaling behavior to larger models remains uncertain." And it was tested "only on standard dense transformers - its effectiveness on mixture-of-experts (MoE) architectures ... remains unexplored". Nothing here is a frontier-scale result, and the forget/retain quantities are losses rather than capability benchmarks.

What this does NOT mean: that removing a capability from the weights removes it from the system. The post separates the two problems explicitly — "both approaches remove knowledge from model parameters but cannot prevent adversaries from supplying that knowledge at inference time". A model that cannot recall a capability can still be handed it in a prompt, a retrieved document or a tool result, so a weights-level control sets which model ships and a per-request permission layer is still what governs a given action.
