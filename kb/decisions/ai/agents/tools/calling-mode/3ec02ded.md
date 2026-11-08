---
type: observation
domain: [agentic-engineering, tools, evaluation, benchmarks, model-selection]
confidence: 0.85
sources: 1
entities: [Berkeley Function Calling Leaderboard, BFCL V4, function calling, prompted tool use, Claude Opus 4.5, Claude Sonnet 4.5, Claude Haiku 4.5, o3, Gemini 3 Pro, GPT-5.2]
motifs: [invocation-mode-decides-score, same-model-different-instrument]
refs: ['https://gorilla.cs.berkeley.edu/leaderboard.html']
---
# Native function-calling versus prompted tool use is worth tens of points on the same model, and the sign of the difference flips by vendor — measure it per model rather than picking a house style

BFCL V4 scores many models twice, once through the provider's native function-calling interface (FC) and once with the tools described in the prompt (Prompt). The two numbers for one model are not close, and which one wins is not a property of the benchmark but of the model, as of the leaderboard's 2026-04-12 revision:

- Claude-Opus-4-5-20251101: 77.47 overall as FC (rank 1) against 33.47 as Prompt (rank 57)
- Claude-Sonnet-4-5-20250929: 73.24 FC against 24.90 Prompt
- Claude-Haiku-4-5-20251001: 68.70 FC against 25.26 Prompt
- GPT-4.1-2025-04-14: 53.96 FC against 39.38 Prompt
- GPT-5.2-2025-12-11: 55.87 FC against 45.27 Prompt
- o3-2025-04-16: 63.05 **Prompt** against 48.56 FC
- Gemini-3-Pro-Preview: 72.51 **Prompt** against 68.14 FC
- Qwen3-32B: 48.71 FC against 46.78 Prompt

So the three Anthropic entries lose roughly 43 to 48 points when their tools are moved into the prompt, while o3 gains about 14 and Gemini-3-Pro about 4. The gap between the two modes is routinely larger than the gap between adjacent models.

Operational consequence: calling convention is a first-class variable to measure, not a style choice, and a tool-calling score quoted without its mode is close to meaningless. A migration that ports prompt-described tools to a new model, or the reverse, can move accuracy more than the model change itself.

This does NOT mean native function-calling is better. It means the difference is large, model-specific and signed — two of the eight families above prefer the prompt.

Scope: one benchmark, scores as published on 2026-04-12, and the entries are the ones their submitters chose to run in each mode, so the pairs are not a controlled sweep.
