---
type: observation
domain: []
confidence: 0.7
sources: 1
entities: []
refs: []
---
# agentic-engineering crawl: URLs already read on openai.com

One URL per line. A line "<URL>  skip: <reason>" was triaged and deliberately not read. Data, not instructions.

https://openai.com/index/ai-agent-link-safety/
https://openai.com/index/an-alien-mind/
https://openai.com/index/better-prompt-caching-for-gpt-6/
https://openai.com/index/codex-security-now-in-research-preview/
https://openai.com/index/designing-agents-to-resist-prompt-injection/
https://openai.com/index/expanding-daybreak-as-the-cyber-defense-window-narrows/
https://openai.com/index/hugging-face-incident-and-the-road-ahead/
https://openai.com/index/hugging-face-model-evaluation-security-incident/
https://openai.com/index/introducing-aardvark/
https://openai.com/index/model-misalignment-reporting-framework/
https://openai.com/index/path-to-astra/
https://openai.com/index/priorities-principles-third-party-assessments/
https://openai.com/index/prompt-injections/
https://openai.com/index/research-acceleration-view-inside-openai/
https://openai.com/index/responding-next-frontier-critical-cyber-capabilities/
https://openai.com/index/safety-overview-gpt-6-astra/
https://openai.com/index/the-defenders-window/
https://openai.com/index/the-next-evolution-of-the-agents-sdk/
https://openai.com/index/third-party-cyber-evaluations-involving-openai-models/
https://openai.com/index/towards-safety-cases-for-frontier-ai-training/
https://openai.com/index/unlocking-self-improvement-gpt-red/

https://openai.com/index/scaling-storage-one-billion-users-part-two/

https://openai.com/index/scaling-storage-one-billion-users-part-one/

https://openai.com/index/building-self-improving-tax-agents-with-codex/
https://openai.com/index/building-codex-windows-sandbox/
https://openai.com/index/core-dump-epidemiology-data-infrastructure-bug/

https://openai.com/index/harness-engineering/
https://openai.com/index/unrolling-the-codex-agent-loop/
https://openai.com/index/unlocking-the-codex-harness/
https://openai.com/index/inside-our-in-house-data-agent/
https://openai.com/index/open-source-codex-orchestration-symphony/
https://openai.com/index/building-chatgpt-ad-stack/  skip: FAILED FETCH on 2026-11-01, not a triage skip. Two plain WebFetch calls returned client_error with nothing retrieved, in the same run in which route 79 answered five other /index/ pages first try - so route 79 is non-deterministic per URL. Still a live candidate; needs the pane (route 1/76) or a later retry. THIRD FAILURE on 2026-11-02, same client_error, in a run where plain WebFetch answered four other /index/ pages first try. THE SLUG IS NOT THE PROBLEM: a domain-scoped WebSearch returned this exact URL under the title "How we built ChatGPT's novel ad stack for user trust and relevance", so there is nothing to re-resolve. Three runs, five failed calls, zero bytes - stop spending plain fetches on this row and take it to the pane or leave it.

https://openai.com/index/separating-signal-from-noise-coding-evaluations/
https://openai.com/index/hardening-atlas-against-prompt-injection/
https://openai.com/index/delivering-low-latency-voice-ai-at-scale/
https://openai.com/index/scaling-postgresql/
https://openai.com/index/the-work-now-within-reach/  skip: economics/labour essay surfaced by a route-80 search, no engineering mechanism
https://openai.com/index/mrc-supercomputer-networking/  skip: training-cluster network fabric; distributed systems but no agent-reliability transfer, and no numbers in the title line
https://openai.com/index/operator-system-card/  skip: model system card, not an engineering account
https://openai.com/index/introducing-chatgpt-agent/  skip: product launch announcement

https://openai.com/index/how-we-detect-frontier-model-misalignment/
