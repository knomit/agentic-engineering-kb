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

- https://www.anthropic.com/engineering | dated | newest crawled: 2026-04-23 https://www.anthropic.com/engineering/april-23-postmortem | last swept: 2026-10-10 (nothing newer than the mark; the index serves its whole back catalogue on one page with no pagination control at all, fetch-routes route 44)
- https://www.anthropic.com/news/ | dated | newest crawled: 2026-10-07 https://www.anthropic.com/claude-haiku-5-5 | last swept: 2026-10-09
- https://www.anthropic.com/research | dated | newest crawled: 2026-10-09 https://www.anthropic.com/research/investigating-unintended-model-actions | last swept: 2026-10-12 (swept with the route-39 ask: 12 unique entries on that date, the "See more" href still `#`, so no depth route; two entries at or above the mark left unread, see queue)
- https://alignment.anthropic.com/ | dated | newest crawled: 2026-08-28 https://alignment.anthropic.com/2026/taste/ | last swept: 2026-10-15 (84 entries enumerated on that date with the route-33 ask, no pagination control at all — one WebFetch is the whole archive. The index is MONTH-DATED only, so no entry can be ordered against a day-precision mark; all six August 2026 rows are now read. Of the 84, roughly 20 are off-host links to www.anthropic.com/research or arxiv.org. The 2026 and 2025 on-host research posts are overwhelmingly unread — see queue item 6 for the ranked list)
- https://alignment.openai.com/misalignment-reports/ | undated | newest crawled: undated | last swept: 2026-10-08
- https://deploymentsafety.openai.com/ | dated | newest crawled: 2026-09-29 https://deploymentsafety.openai.com/gpt-6-1-sol | last swept: 2026-10-01
- https://developers.openai.com/cookbook | undated | newest crawled: undated | last swept: unknown
- https://developers.openai.com/api/docs/guides/ | undated | newest crawled: undated | last swept: unknown
- https://simonwillison.net/tags/llms/ | dated | newest crawled: 2026-09-24 https://simonwillison.net/2026/Sep/24/harder/ | last swept: 2026-10-13 (first sweep; 30 entries at or above the old mark on that date, of which 1 read, 19 skip-marked and the rest queued. REAL pagination, ?page=N, 67 pages as of that date, fetch-routes route 50. It is a link blog: most rows are quoted comments, model launches and tool release notes, so the triage ratio here is unlike a method-post feed)
- https://www.langchain.com/blog/ | dated | newest crawled: 2026-10-08 https://www.langchain.com/blog/agents-that-can-pay-with-stripe-link | last swept: 2026-10-12 (20 cards, 18 unique on that date; the index repeats featured entries, so deduplicate by URL, and it has REAL pagination, fetch-routes route 45; nothing dated after 2026-10-09, and both entries at or above the mark are now resolved — one read, one skip-marked)
- https://www.latent.space/archive | dated | newest crawled: 2026-10-12 https://www.latent.space/p/claude-dynamic-workflows | last swept: 2026-10-15 (first swept 2026-10-14; 12 entries that date, no pagination control. ROUTE 54 APPLIES AND IT CORRECTS ROUTE 43: /archive?sort=new ERRORS on this Substack, plain /archive serves the list. The two newest rows carry RELATIVE dates ("5 hrs ago"), uncomparable with the mark. Roughly half the feed is the AINews daily digest, which is a pointer feed, so the triage ratio here is unlike a method-post feed)
- https://eugeneyan.com/writing/ | dated | newest crawled: 2026-07-30 https://eugeneyan.com/writing/cybersecurity-evals/ | last swept: unknown
- https://www.microsoft.com/en-us/research/blog/ | dated | newest crawled: 2026-07-30 https://www.microsoft.com/en-us/research/blog/echoverse-deep-evolving-environments-for-computer-use-agents/ | last swept: unknown
- https://www.microsoft.com/en-us/security/blog/ | dated | newest crawled: 2026-10-07 https://www.microsoft.com/en-us/security/blog/2026/10/07/3-lessons-from-frontier-ai-vulnerability-research/ | last swept: 2026-10-15 (first sweep; 10 unique posts across 14 index entries on that date — the featured block repeats rows, so deduplicate by URL. NO site-wide pagination, but the per-topic "View all" links DO resolve and are the depth route, route 55. Most of the index is conventional threat intel and product round-ups; one row in ten was in scope)
- https://aws.amazon.com/blogs/machine-learning/ | dated | newest crawled: unknown | last swept: unknown
- https://research.google/blog/ | dated | newest crawled: 2026-10-05 https://research.google/blog/open-and-emergent-problems-in-agentic-privacy-and-security-a-contextual-angle/ | last swept: 2026-10-14 (first sweep; 12 entries on that date, all Sep-Oct 2026. NO DEPTH ROUTE, route 52: the numbered pagination says "of 135" pages but every page link's href is `javascript(0):void`, so the back catalogue is unreachable, as on anthropic.com. Most of the front page is non-agent AI research, so expect roughly one in-scope row per sweep)
- https://embracethered.com/blog/ | dated | newest crawled: 2026-09-30 https://embracethered.com/blog/posts/2026/from-select-to-sysadmin-sql-copilot-bluehat-asia/ | last swept: 2026-10-08
- https://metr.org/blog/ | dated | newest crawled: 2026-10-06 https://metr.org/blog/2026-10-06-ai-systems-could-cover-up-misbehavior/ | last swept: 2026-10-08
- https://sourcegraph.com/blog | dated | newest crawled: 2026-08-28 https://sourcegraph.com/blog/a-smarter-way-to-run-code-migrations-with-less-llm-context | last swept: 2026-10-14 (first sweep; 19 entries on that date back to 2026-05-04. REAL pagination, "Older →" -> ?page=2, route 53. The three rows above the mark are skip-marked in seen as product and pricing notes, so the mark sits below them deliberately)
- https://cognition.com/blog | dated | newest crawled: 2026-05-29 https://cognition.com/blog/testing-development | last swept: unknown
- https://www.trychroma.com/research | dated | newest crawled: 2026-03-01 https://www.trychroma.com/research/context-1 | last swept: 2026-10-09 (all 5 index entries now read or skip-marked)
- https://builder.aws.com/learn/topics/builders-library | undated | newest crawled: undated | last swept: unknown
- https://code.claude.com/docs/en/best-practices | page | newest crawled: page | last swept: unknown
- https://genai.owasp.org/ | undated | newest crawled: undated | last swept: unknown
- https://owasp-agentic-ai-security-incidents.lovable.app/ | undated | newest crawled: undated | last swept: unknown
- https://www.aisi.gov.uk/blog/ | dated | newest crawled: 2026-10-07 https://www.aisi.gov.uk/blog/transect-making-large-scale-agentic-evaluations-easier-to-understand | last swept: 2026-10-08
- https://openai.com/news/ | dated | newest crawled: 2026-09-28 https://openai.com/index/towards-safety-cases-for-frontier-ai-training/ | last swept: 2026-09-30
- https://blog.redwoodresearch.org/ | dated | newest crawled: 2026-09-25 https://blog.redwoodresearch.org/p/continual-learning-might-make-your | last swept: 2026-10-10 (first sweep; the root is a JS shell that serves no entries, read /archive?sort=new instead, fetch-routes route 43)
- https://github.com/vectara/hallucination-leaderboard | page | newest crawled: page | last swept: unknown
- https://huggingface.co/blog | dated | newest crawled: 2026-10-03 https://huggingface.co/blog/microsoft/thinkingbox | last swept: 2026-10-15 (first sweep; 34 unique posts on that date. TWO BLOCKS WITH DIFFERENT DATE PRECISION, route 56: the "Community Articles" block carries RELATIVE dates ("6 days ago") that cannot be compared with the mark, the main listing carries absolute ones. REAL pagination at ?p=N, 63 pages, zero-indexed. It is a community blog, so provenance varies by author and most rows are model launches)
- https://modelcontextprotocol.io/specification/versioning | page | newest crawled: page | last swept: 2026-10-13
- https://modelcontextprotocol.io/specification/2026-07-28/deprecated | page | newest crawled: page | last swept: 2026-10-11
- https://api.github.com/repos/modelcontextprotocol/modelcontextprotocol/contents/docs/specification | page | newest crawled: page | last swept: unknown

- https://modelcontextprotocol.io/community/feature-lifecycle | page | newest crawled: page | last swept: 2026-10-11
