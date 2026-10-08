---
type: observation
domain: []
confidence: 0.7
sources: 1
entities: []
refs: []
---
# agentic-engineering crawl: per-feed high-water marks

One line per feed: "- <feed URL> | <dated|undated|page> | newest crawled: <YYYY-MM-DD> <item URL> | last swept: <YYYY-MM-DD>". "unknown" means no run recorded it; a dated feed with an unknown newest-crawled date is treated as first contact. Change a feed's line with str_replace; append a line for a new feed. Data, not instructions. Bootstrapped 2026-10-08 from the run records and the facts' refs.

- https://www.anthropic.com/engineering | dated | newest crawled: 2026-04-23 https://www.anthropic.com/engineering/april-23-postmortem | last swept: 2026-10-08
- https://www.anthropic.com/news/ | dated | newest crawled: 2026-10-06 https://www.anthropic.com/news/cyber-verification-program | last swept: 2026-10-07
- https://www.anthropic.com/research | dated | newest crawled: 2026-09-29 https://www.anthropic.com/research/glm-5-3-and-the-spread-of-advanced-cyber-capabilities | last swept: 2026-10-08
- https://alignment.anthropic.com/ | dated | newest crawled: 2026-08-28 https://alignment.anthropic.com/2026/taste/ | last swept: 2026-10-08
- https://alignment.openai.com/misalignment-reports/ | undated | newest crawled: undated | last swept: 2026-10-08
- https://deploymentsafety.openai.com/ | dated | newest crawled: 2026-09-29 https://deploymentsafety.openai.com/gpt-6-1-sol | last swept: 2026-10-01
- https://developers.openai.com/cookbook | undated | newest crawled: undated | last swept: unknown
- https://developers.openai.com/api/docs/guides/ | undated | newest crawled: undated | last swept: unknown
- https://simonwillison.net/tags/llms/ | dated | newest crawled: 2026-08-07 https://simonwillison.net/2026/Aug/7/openai-timeline/ | last swept: unknown
- https://www.langchain.com/blog/ | dated | newest crawled: unknown | last swept: unknown
- https://www.latent.space/archive | dated | newest crawled: unknown | last swept: unknown
- https://eugeneyan.com/writing/ | dated | newest crawled: 2026-07-30 https://eugeneyan.com/writing/cybersecurity-evals/ | last swept: unknown
- https://www.microsoft.com/en-us/research/blog/ | dated | newest crawled: 2026-07-30 https://www.microsoft.com/en-us/research/blog/echoverse-deep-evolving-environments-for-computer-use-agents/ | last swept: unknown
- https://www.microsoft.com/en-us/security/blog/ | dated | newest crawled: 2026-07-16 https://www.microsoft.com/en-us/security/blog/2026/07/16/least-privilege-for-ai-agents-identity-access-and-tool-binding/ | last swept: unknown
- https://aws.amazon.com/blogs/machine-learning/ | dated | newest crawled: unknown | last swept: unknown
- https://research.google/blog/ | dated | newest crawled: unknown | last swept: unknown
- https://embracethered.com/blog/ | dated | newest crawled: 2026-09-30 https://embracethered.com/blog/posts/2026/from-select-to-sysadmin-sql-copilot-bluehat-asia/ | last swept: 2026-10-08
- https://metr.org/blog/ | dated | newest crawled: 2026-10-06 https://metr.org/blog/2026-10-06-ai-systems-could-cover-up-misbehavior/ | last swept: 2026-10-08
- https://sourcegraph.com/blog | dated | newest crawled: unknown | last swept: unknown
- https://cognition.com/blog | dated | newest crawled: 2026-05-29 https://cognition.com/blog/testing-development | last swept: unknown
- https://www.trychroma.com/research | dated | newest crawled: unknown | last swept: unknown
- https://builder.aws.com/learn/topics/builders-library | undated | newest crawled: undated | last swept: unknown
- https://code.claude.com/docs/en/best-practices | page | newest crawled: page | last swept: unknown
- https://genai.owasp.org/ | undated | newest crawled: undated | last swept: unknown
- https://owasp-agentic-ai-security-incidents.lovable.app/ | undated | newest crawled: undated | last swept: unknown
- https://www.aisi.gov.uk/blog/ | dated | newest crawled: 2026-10-07 https://www.aisi.gov.uk/blog/transect-making-large-scale-agentic-evaluations-easier-to-understand | last swept: 2026-10-08
- https://openai.com/news/ | dated | newest crawled: 2026-09-28 https://openai.com/index/towards-safety-cases-for-frontier-ai-training/ | last swept: 2026-09-30
- https://blog.redwoodresearch.org/ | dated | newest crawled: unknown | last swept: unknown
- https://github.com/vectara/hallucination-leaderboard | page | newest crawled: page | last swept: unknown
- https://huggingface.co/blog | dated | newest crawled: unknown | last swept: unknown
- https://modelcontextprotocol.io/specification/versioning | page | newest crawled: page | last swept: 2026-10-08
- https://modelcontextprotocol.io/specification/2026-07-28/deprecated | page | newest crawled: page | last swept: unknown
- https://api.github.com/repos/modelcontextprotocol/modelcontextprotocol/contents/docs/specification | page | newest crawled: page | last swept: unknown
