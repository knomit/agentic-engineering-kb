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

=== SWEEPS, 49th RUN (2026-10-08). SEVEN FEEDS PLUS THE TRIPWIRE, ALL PLAIN WebFetch, ALL BEFORE ANY WRITE. ===
ONE GENUINELY NEW POST ACROSS SEVEN FEEDS. It was read and produced five facts.

www.aisi.gov.uk/blog -- windowed since 2026-10-01. *** ONE NEW, AND THE 48th RUN'S SWEEP MISSED IT BY
*** HOURS RATHER THAN BY METHOD: ***
  /blog/transect-making-large-scale-agentic-evaluations-easier-to-understand (Oct 7 2026) -> 81dcb24c,
  263da769, ad69c6c7, plus the 94858345 and 0cc69d27 enrichments. AISI's open-source transcript-analysis
  Python package built on Inspect Scout, released "with the support of Meridian Labs". ONE open-ended call
  plus ONE verbatim call covering nine passages. *** ITS VALUE IS NOT THE TOOL. It is three caveats the
  authors state about their own output, plus the non-reproducibility of a model-judged analysis -- all of
  it stated by the team shipping the thing, which is the strongest modality this kind of claim gets. ***
  TIMING NOTE, AND IT IS A CADENCE FINDING NOT A FAULT: the 48th run swept this feed on 2026-10-07 at
  ~13:47Z with a window since 10-01 and correctly reported nothing new. This post is dated 10-07. A feed
  swept at a fixed hour will systematically miss same-day publications, so "nothing new" on a sweep
  windowed to include today is weaker evidence than it looks. Re-sweeping yesterday as well as today costs
  nothing (the window is a prompt argument) and would have caught this a day earlier.
  Newest before the window still /blog/building-a-more-secure-environment-... (Oct 1, read 45th).

alignment.anthropic.com -- *** INDEX RETURNED 84 ENTRIES. FOURTH MEASUREMENT, FOURTH DIFFERENT DEPTH:
*** 8 (45th) -> 62 (46th) -> 62 (47th) -> 79 (48th) -> 84 (49th), same URL, date window asked every time.
*** Route 33's depth-varies finding is now measured across five calls and four distinct values, and the
*** sequence is monotonically non-decreasing, which is consistent with a listing that deepens rather than
*** with a feed that grows -- the newest entry has been August 2026 for four runs. NEITHER 79 NOR 84 IS
*** THE ARCHIVE'S SIZE. Page still says it spans "April 2022 through August 2026". ***
*** AND IT CLOSES THE YEAR-PREFIX QUESTION OUTRIGHT -- 48th-run queue item (19), carried since the 46th.
*** The 84-entry listing names all three disputed slugs WITH their prefixes: /2026/sleight-bench/ (May
*** 2026), /2026/coding-audit-realism/ (Mar 2026), /2026/ai-organizations/ (Apr 2026). ALL THREE ARE
*** /2026/, matching what the corpus already holds, so no fact's refs need changing. Combined with /2025/
*** being confirmed twice (selective-gradient-masking, summarization-for-monitoring), BOTH prefixes are
*** real and the corpus's addressing is correct throughout. DELETE THIS ITEM; it is settled by an
*** enumeration, which is the stronger instrument than the fact-refs check the queue asked for. ***
THE 84-ENTRY ENUMERATION, slugs not yet read by any run. This is a superset of the 48th run's 79 and I
cannot say which five are the delta, so the whole list is given rather than a diff:
  /2026/backdooring-classifiers/ (Apr 2026) -- *** RANK 1. Poisoning the fine-tuning datasets of
    constitutional classifiers: an attack on a defence the pack already holds facts about. ***
  /2026/hot-mess-of-ai/ (Feb 2026) -- RANK 2. Misalignment scaling with model intelligence AND task
    complexity, which is a two-variable claim and the pack has no fact on the interaction.
  /2026/conceptual-reasoning-index/ (Aug 2026) -- still unread, still unrefed; FOUR runs have now named it
    without spending the call.
  /2026/teaching-claude-why/ (May), /2026/msm/ (May, Model Spec Midtraining),
  /2026/introspection-adapters/ (Apr), /2026/automated-w2s-researcher/ (Apr),
  /2026/abstractive-red-teaming/ (Mar), /2026/automated-alignment-agent/ (Mar), /2026/auditbench/ (Mar),
  /2026/challenges-hopes/ (Mar), /2026/psm/ (Feb), /2026/auditing-overt-saboteur/ (Jan),
  /2025/bloom-auto-evals/ (Dec), /2025/activation-oracles/ (Dec),
  /2025/alignment-faking-mitigations/ (Dec), /2025/auditing-mo-replication/ (Dec),
  /2025/anthropic-fellows-program-2026/ (Dec, off-topic), /2025/honesty-elicitation/ (Nov),
  /2025/sabotage-risk-report/ (Oct), /2025/stress-testing-model-specs/ (Oct),
  /2025/believe-it-or-not/ (Oct), /2025/subtle-reasoning/ (Oct), /2025/openai-findings/ (Aug),
  /2025/subliminal-learning/ (Jul), /2025/inverse-scaling/ (Jul), /2025/cheap-monitors/ (Jun),
  /2025/unsupervised-elicitation/ (Jun), /2025/modifying-beliefs-via-sdf/ (Apr), /2025/bumpers/ (Apr),
  /2025/alignment-faking-revisited/ (Apr), /2025/distill-paraphrases/ (Mar),
  /2025/automated-researchers-sandbag/ (Mar),
  /2025/introducing-safeguards-research-team/index.html (Feb), /2025/wont-vs-cant/ (Feb),
  /2025/reward-hacking-ooc/index.html (Jan), /2025/recommended-directions/index.html (Jan),
  /2024/how-to-alignment-faking/index.html (Dec), /2024/rogue-eval/index.html (Dec),
  /2024/safety-cases/index.html (Nov).
  *** NOTE THE /index.html SUFFIX ON SEVERAL OLDER SLUGS. The 48th run read
  *** /2025/summarization-for-monitoring/ successfully WITHOUT it, though this listing gives it WITH --
  *** so both forms resolve and the suffix is not load-bearing. Do not treat a listing's /index.html as a
  *** different page, and do not add it when it is absent. ***
  THE INDEX ALSO LINKS OFF-SITE, and this is the reachable route to anthropic.com/research depth (see the
  /research entry below): /research/alignment-faking, /research/sabotage-evaluations,
  /research/reward-tampering, /research/many-shot-jailbreaking, /research/probes-catch-sleeper-agents,
  /research/sleeper-agents-training-deceptive-llms-that-persist-through-safety-training,
  /research/specific-versus-general-principles-for-constitutional-ai,
  /research/towards-understanding-sycophancy-in-language-models,
  /research/studying-large-language-model-generalization-with-influence-functions,
  /research/influence-functions, /research/measuring-faithfulness-in-chain-of-thought-reasoning,
  /research/question-decomposition-improves-the-faithfulness-of-model-generated-reasoning,
  /research/discovering-language-model-behaviors-with-model-written-evaluations,
  /research/constitutional-ai-harmlessness-from-ai-feedback,
  /research/measuring-progress-on-scalable-oversight-for-large-language-models,
  /research/language-models-mostly-know-what-they-know,
  /research/training-a-helpful-and-harmless-assistant-with-reinforcement-learning-from-human-feedback,
  plus arxiv.org/abs/2506.18032 and arxiv.org/abs/2411.07494, and a Google Drive folder for the CoT
  faithfulness evaluations (Apr 2025) which is an asset host this job has never touched.

www.anthropic.com/research -- 10 entries, identical to the 47th and 48th runs' listings, newest
  /research/claude-shaped-science (Oct 1). *** AND THE "See more" MYSTERY IS SOLVED: ITS href IS `#`, A
  PLACEHOLDER. The depth behind the 10-entry window is NOT reachable from this page at all, which is why
  two runs have left it "unexplored". The reachable route is the alignment.anthropic.com index above,
  which links 17 older /research/ slugs directly. STOP QUEUEING "the See more depth" AS A TARGET ON THIS
  PAGE; take the slugs from the alignment index instead. See fetch-routes route 38. ***
  RANK 1 remains /research/project-swap (Sep 24, agents transacting on a human's behalf -- nothing in the
  corpus covers agent-to-counterparty commerce). Then /research/claude-shaped-science (Oct 1),
  /research/yes-claude-can-do-nine-loops (Sep 25),
  /research/intelligence-targeting-conventional-weapons-capabilities (Sep 10).
  TWO FEATURED ITEMS, both outside /research/ and both off-topic, named so they are not re-ranked:
  /news/claude-discovers-novel-enzyme-system (Sep 23, already named by the 48th run) and
  /institute/econ-scenarios (undated).

alignment.openai.com/misalignment-reports/ -- windowed since 2026-09-26. NOTHING NEW; both 2026-10-02
  reports were read by the 47th run. *** ROUTE 33 INDEPENDENTLY REPRODUCED ONE RUN LATER, WHICH PROMOTES
  IT FROM AN OBSERVATION TO A STABLE PROPERTY OF THIS PAGE: the header and footer again say TWELVE and the
  table again lists ELEVEN. The 48th run established by a second enumerating call that there is no twelfth.
  So the 12 is a STATIC MISCOUNT IN THE PAGE ITSELF, not a summariser artifact and not a stale header
  about to resolve -- the 48th run's framing ("a count invents rows") was right about the remedy and the
  defect is upstream of the extraction. DO NOT SPEND A CALL CHECKING WHETHER THE TWELFTH HAS APPEARED;
  only a change in the ENUMERATED count matters on this feed. ***
  Sweep it every run regardless: it has gone 6 -> 9 -> 11 in batches and looks exhausted between them.

metr.org/blog -- windowed since 2026-09-28. NOTHING NEW beyond the 48th run's find; newest still
  /blog/2026-10-06-ai-systems-could-cover-up-misbehavior/ (Oct 6), already mined to 9cd59af4. RE-READ this
  run (two calls, one open-ended and one verbatim) before the recency screen revealed it was already
  mined -- see crawl-state for the cost and the screen that prevents it. The verbatim call was NOT wasted:
  it supplied the named remediation and the precise mechanism for the 9cd59af4 enrichment, neither of
  which the 48th run captured.

embracethered.com/blog -- windowed since 2026-09-30. NOTHING NEW; newest still the SQL Copilot post
  (Sep 30, read 46th). TWO SLUGS NOT PREVIOUSLY RECORDED ANYWHERE IN EITHER SLOT, both listed under a
  "0001" heading with Jan 01 dates that are plainly wrong:
  /blog/posts/2026/device-bound-session-credentials-dbsc-great-news/ and
  /blog/posts/2026/chrome-device-bound-session-credentials/. Browser-credential topics, judged off-topic
  for this pack; recorded so a later run does not mistake them for new publications or chase the dates.

www.anthropic.com/engineering -- windowed since 2026-04-23. NOTHING NEW; newest still april-23-postmortem
  (Apr 23 2026). NINE RUNS QUIET at the newest-date level, which per the 47th run's sub-rule is a
  statement about the newest date and not about coverage. Index returned 25 entries, reproducing the 39th
  run's count exactly. The featured card (how-we-contain-claude) carries no date on the index.

modelcontextprotocol.io/specification/versioning -- the tripwire, one call. 2026-07-28 UNCHANGED,
  THIRTY-EIGHTH consecutive run. Four facts re-confirmed verbatim off that one call.

NOT SWEPT THIS RUN, NAMED: openai.com/news (needs the browser, route 1; last swept the 41st -- NINE RUNS,
  and still the only queued item that strictly needs the browser), anthropic.com/news (swept by the 48th
  run, which found /news/cyber-verification-program), deploymentsafety.openai.com, simonwillison,
  langchain, huggingface, eugeneyan, trychroma, builder.aws.com, genai.owasp.org, research.google,
  sourcegraph, latent.space, redwoodresearch, microsoft research, microsoft security, cognition,
  developers.openai.com, vectara, darioamodei.com, code.claude.com, owasp-agentic incidents tracker,
  aws machine-learning.
NO new feed was added this run. No source errored, 404'd, was paywalled or was gated. No slug was guessed.
No browser was used and nothing needed one. ZERO WebSearch calls.
