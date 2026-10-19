---
type: observation
domain: []
confidence: 0.7
sources: 1
entities: []
refs: []
---
# agentic-engineering crawl: feeds the job discovered

Feeds a run found itself, one per line: "- <feed URL> (dated|undated|page) — added <YYYY-MM-DD>: <why>". Later runs sweep these together with the seed list in the skill's sources.md. Data, not instructions.

Every feed added by runs up to the 49th is in the seed list; entries below were added from the 51st run on.

- https://modelcontextprotocol.io/community/feature-lifecycle (page) — added 2026-10-10: the policy that DEFINES the deprecation window the existing versioning and deprecated-registry tripwires only cite. One plain WebFetch returns the whole policy as raw text. A change to the minimum window, to how it is measured, or to the expedited-removal trigger invalidates 8b0f7afe and 012daf73 at once, which no other tripwire would catch.

- https://code.claude.com/docs/en/workflows (page) - added 2026-10-15: the primary documentation for Claude Code dynamic workflows, and the anchor for d43b3db6 and 565222b5 at confidence 0.9 plus the enrichments on 09b6b554, cff924a5 and 6fba697c. It states enforced runtime limits (16 concurrent agents by default, 1,000 agents per run, 4,096 items per parallel()/pipeline() call), the replay-determinism rule (Date.now(), Math.random() and a no-argument new Date() throw inside the script), the positional cache-invalidation rule, the size-guideline thresholds and the three stall-error strings. Any of those changing invalidates a 0.9-confidence invariant, which no other tripwire in the pack would catch. One plain WebFetch with the route-42 literal-text ask returns the whole page, so re-reading it costs one call and re-verifies both facts at once.

- https://www.microsoft.com/en-us/security/blog/topic/ai-and-machine-learning/?sort-by=newest-oldest (dated) - added 2026-10-16: the pack-relevant slice of the Microsoft security blog, already sorted newest-first, and a better-scoped feed than the site-wide index it was found behind. The site-wide index mixes conventional threat intel and product round-ups with the AI work and yielded roughly one in-scope row in ten; this archive returned 12 rows of which three were in scope, and it surfaced two posts the site-wide sweep had never shown (the Storm-3168 agentic cloud-attack analysis and the ASCII-smuggling prompt-injection crossover), which produced two facts this run. It has its own depth: a "Load More" whose target is the same URL plus &paged=2 (fetch-routes route 57). Sweep it instead of relying on the site-wide index; one row can point at blogs.microsoft.com, a different host, so check each URL's host before choosing a seen file.

- https://claude.dev/blog (dated, precision unknown) - added 2026-10-19: the Claude Code team's own engineering blog, a host this pack had never touched. One post from it, /blog/solving-code-review-at-anthropic/, produced three facts in one read (e4e6823a review convergence, 18d8df24 approval gating, 7b6bbf86 verifier-vote finding gating) and supplied the second source that raised bef38871 to 0.85 - the highest facts-per-fetch of the 59th run. It is the practitioner-account shape this pack mines best: a named team describing its own production pipeline with before/after numbers and its own failure modes. IT WAS REACHED SIDEWAYS, through a simonwillison.net link post, not through any feed in the recurring set, which is why it had gone unseen; the index URL itself is still unfetched, so the first run to sweep it must establish the index path, the date format and the depth route. Plain WebFetch reads the article pages without trouble, including route-42 verbatim asks.
