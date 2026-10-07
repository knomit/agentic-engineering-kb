---
type: observation
domain: []
confidence: 0.7
sources: 1
entities: []
refs: []
---
# agentic-engineering crawl: recurring sources and URL catalogues

type: reference / job-state. The recurring source list and the URL catalogues earlier runs paid fetches to enumerate.

*** READ THIS FIRST. THIS SLOT IS A CONTINUATION, NOT THE WHOLE SOURCE LIST. ***
THE RECURRING FEED LIST AND EVERY CATALOGUE LIVE AT THE OLD PATH AND ARE STILL FULLY READABLE:
    knomit_explain(file=".knomit/jobs/agentic-engineering/crawl-sources.md")
120,273 characters, 1,404 lines. READS WORK NORMALLY THERE; WRITES ARE REFUSED (see fetch-routes route 32
section header / the migration note in artifacts/jobs/agentic-engineering/fetch-routes.md).
EVERY RUN MUST READ BOTH. The old path holds: the recurring-feed list (the ~35 URLs swept each run), the
Anthropic /engineering, /news/ and /research back catalogues, the alignment.anthropic.com and
alignment.openai.com inventories, the AISI 98-post archive, the OWASP resource/download-id map, the AWS
Builders' Library 30-item enumeration, the Cognition archive, the MCP spec page map, the
deploymentsafety.openai.com index, the third-party-evaluation rule and the paraphrase rule. This slot holds
additions from the 48th run onward. Nothing was copied in the move, so nothing was truncated.

=== SWEEPS, 48th RUN (2026-10-07). EIGHT FEEDS PLUS THE TRIPWIRE, ALL PLAIN WebFetch, ALL BEFORE ANY WRITE. ===
TWO GENUINELY NEW POSTS ACROSS EIGHT FEEDS. Both were read and both produced facts.

metr.org/blog — windowed since 2026-09-30. *** ONE NEW, AND IT WAS THE RUN'S BEST DOCUMENT: ***
  /blog/2026-10-06-ai-systems-could-cover-up-misbehavior/ (Oct 6 2026) -> 9cd59af4, plus the 9e5bfe91
  enrichment. METR's own disclosure of a client-side injection in Inspect's transcript viewer. ONE CALL
  PLUS ONE VERBATIM CALL. *** THIS CLOSES THE LONG-CARRIED "transcript viewer" QUEUE ITEM (16)(i), which
  had been take-or-delete for many runs — the operator published its own account, which is Appendix S's
  "check for the operator's own account" rule paying out for the second run running. ***
www.anthropic.com/news/ — windowed since 2026-09-20; last swept the 43rd run. ONE NEW ON-TOPIC:
  /news/cyber-verification-program (Oct 6 2026) -> a77aff37, plus the 8a0b760f enrichment. Carries measured
  per-tier block and completion rates on CyScenarioBench, which is the rarest thing in this area: the COST
  side of a guardrail decision as a number. Also new and OFF-TOPIC, named so a later run does not re-rank
  them: /news/claude-frontier-academy (Oct 2), /news/barclays-scales-claude (Oct 1),
  /news/claude-discovers-novel-enzyme-system (Sep 23). Still UNREAD and still worth a call:
  Claude Sonnet 5.5 (Sep 28) and Claude Opus 5.5 (Sep 22) — the SYSTEM CARDS remain factless. Route 5b on
  anthropic.com/claude-opus-5-5 and /claude-sonnet-5-5 for the href; do NOT guess it.
alignment.openai.com/misalignment-reports/ — windowed since 2026-10-05, then ENUMERATED in full.
  NOTHING NEW. ELEVEN reports, every slug already in ALREADY_CRAWLED. *** THE FIRST CALL CLAIMED "12 total
  reports" AND THERE IS NO TWELFTH — see fetch-routes route 33. *** Sweep it every run regardless: it has
  gone 6 -> 9 -> 11 in batches and looks exhausted between them. The 6866e63b enrichment date-stamps the
  count at 11 as of 2026-10-07 rather than calling the series complete.
www.anthropic.com/research — 10 entries returned, identical to the 47th run's listing, newest Oct 1. No
  new material. The "See more" depth is STILL UNEXPLORED; see the ranked unread list in the old slot's
  47th-run section. RANK 1 now /research/project-swap (agents transacting on a human's behalf — nothing
  else in the corpus covers agent-to-counterparty commerce), then /research/claude-shaped-science, then
  /research/yes-claude-can-do-nine-loops, then
  /research/intelligence-targeting-conventional-weapons-capabilities. DONE THIS RUN:
  /research/glm-5-3-and-the-spread-of-advanced-cyber-capabilities (Sep 29) -> 2f33c7ff + 065eb829.
  DONE THIS RUN: the unread tail of /research/alignment-assessment-cybersecurity-incidents via
  offset=100000 (route 31) -> the 778b437e enrichment. *** THAT DOCUMENT IS NOW FULLY READ, both halves. ***
alignment.anthropic.com — index returned 79 ENTRIES, against 62 on the 46th and 47th runs and 8 on the
  45th, same URL, date window asked for every time. THIRD MEASUREMENT, THIRD DIFFERENT DEPTH — see
  fetch-routes route 33. Newest entry still August 2026; the page still says it spans April 2022 to August
  2026. READ THIS RUN: /2025/summarization-for-monitoring/ (the 47th run's RANK 1) -> 5da76ff0, THE MONITOR
  CLUSTER'S FIRST BUILD FACT. *** AND IT SETTLES THE YEAR-PREFIX QUESTION A SECOND TIME: the post fetched
  at /2025/ and its own Bibtex gives 2025-02-27. The /2025/ prefix is real. sleight-bench,
  coding-audit-realism and ai-organizations are still held under /2026/ and still need settling from a
  fact's refs, not a fetch. ***
  REMAINING RANKED UNREAD: /2025/strengthening-red-teams/ is now RANK 1; then
  /2025/pretraining-data-filtering/ (the baseline BOTH ae9fda8d and 5a36eb3b measure against);
  then /2026/conceptual-reasoning-index/ (CONFIRMED present on this run's listing, still unread, still
  unrefed by any fact — three runs have now named it without spending the call); then /2025/petri-v2/ and
  /2025/petri/; /2025/automated-auditing/; /2025/reward-hacking-ooc/; /2025/inoculation-prompting/.
embracethered.com/blog — windowed since 2026-09-30. NOTHING NEW; newest still the SQL Copilot post
  (Sep 30, read 46th). The 2025/2018 back catalogue remains the standing optional backlog.
www.aisi.gov.uk/blog — windowed since 2026-10-01. NOTHING NEW; newest still
  /blog/building-a-more-secure-environment-for-evaluating-dangerous-capabilities (Oct 1, read 45th). Every
  slug returned was already in the old slot. The AISI BACK CATALOGUE is untouched and unchanged as a
  backlog — ranked list in the old slot and in this run's crawl-state queue.
www.anthropic.com/engineering — windowed since 2026-09-20. NOTHING NEW; newest still april-23-postmortem
  (Apr 23 2026). EIGHT RUNS QUIET at the newest-date level. Per the 47th run's sub-rule, that is a
  statement about the newest date and NOT about coverage — the back catalogue is separately tracked.
modelcontextprotocol.io/specification/versioning — the tripwire, one call. 2026-07-28 UNCHANGED,
  THIRTY-SEVENTH consecutive run. Four facts re-confirmed verbatim off that one call.
NOT SWEPT THIS RUN, NAMED: openai.com/news (needs the browser, route 1; last swept the 41st — EIGHT RUNS,
  and it is the only queued item that strictly needs the browser), deploymentsafety.openai.com,
  simonwillison, langchain, huggingface, eugeneyan, trychroma, builder.aws.com, genai.owasp.org,
  research.google, sourcegraph, latent.space, redwoodresearch, microsoft research, microsoft security,
  cognition, developers.openai.com, vectara, darioamodei.com, code.claude.com, owasp-agentic incidents
  tracker, aws machine-learning.
NO new feed was added this run. No source errored, 404'd, was paywalled or was gated. No slug was guessed.
No browser was used and nothing needed one. ZERO WebSearch calls.
