---
type: reference
domain: [agentic-engineering, job-state]
confidence: 1
sources: 0
entities: [agentic-engineering]
refs: ['https://github.com/knomit/knomit']
---
# Last crawl state

crawled: 2026-09-24 (thirty-fifth run). ONE DAY after the 34th run committed (2026-09-23T16:25:44Z),
so a light sweep — but a real one, because several feeds had gone two or more runs unswept.
SIX FEEDS PLUS THE TRIPWIRE. 5 facts written, 5 existing facts corrected or enriched, 0 retracted.
3 genuinely new URLs.

*** THIS SLOT HOLDS ONE RUN. THE HISTORY IS THE RECORD. WALK IT. ***
*** READ THIS BEFORE THE WALK: THIS RUN WROTE crawl-state TWICE, AND IT IS THE FIRST TO DO SO.
*** The 34th run's FINDING 10 and QUEUE ITEM (2) asked for an early insurance write; it was performed
*** at 474fbb130720d82633f55fd34050a1cfb7ab2514 before the fact batch, and THIS revision supersedes it.
*** SO THE 35th RUN OCCUPIES TWO REVISIONS OF THIS PATH, NOT ONE. A walk that counts revisions as runs
*** will count 36 runs where there are 35. The early body identifies itself as an insurance write in its
*** own first paragraph — read the first paragraph before counting. SEE FINDING 1: the mitigation works
*** and it has a cost nobody named in advance. ***
*** fetch-routes ROUTE 10 (binding drift): did NOT recur. EIGHT CLEAN RUNS. knomit_repos called first,
*** one mount, agentic-engineering, read+write. Per the job prompt's step 0 this run did NOT re-bind.
*** FINDING 10 of the 34th run (total bridge withdrawal) also did NOT recur. ***

=== HISTORY WALK — COMPLETE, FIFTEEN RUN BODIES, THE MOST ANY RUN HAS READ ===
REVISIONS READ: **15 distinct revisions.** FULL 40-HEX, per route 7b:
  66535f3fc655e3f79f1358c9d746645ca52e461d (HEAD at start, 2026-09-23T16:25:44Z, "Merge #26") — 34th.
  ec73cbc1c1cfc857eeb6e6e8ffbd5954d0342302 (2026-09-22T13:36:55Z, "Merge #23") — 33rd run.
  2230476f8179685a6b6e4aa59d031424e62dff2e (2026-09-21T13:41:17Z, "Merge #20") — 32nd run.
  94183c20c3ac8aac08194f1b5676776914614440 (2026-09-20T13:31:51Z, "Merge #17") — 31st run.
  f9c2ccc684641a5e776bdef0063b019bb99170d6 (2026-09-19T15:58:33Z, "Merge #12") — 30th run.
  0715d1c09f36a89040bbbc1cd64d2a7bee24ab17 (2026-09-18T21:06:54Z) — 29th run.
  f7e3e43133c4477728c47574d874a660bc3acced (2026-09-18T13:43:53Z) — 28th run.
  c3bbd6a3fa70de972d7a17d966e1338b67abfa41 (2026-09-17T19:37:28Z) — 27th run.
  20eb4edb0910f3ce70697deb7ee20391819fbced (2026-09-13T15:48:52Z, "Merge #11") — 26th run.
  c6cab79802bfc5ad45da90851f698de37ba8d1cb (2026-08-29T15:12:58Z) — 25th run.
  91f7d0857b745035973adfb6d543960e53e59779 (2026-08-28T14:43:22Z) — 24th run.
  7462e9f229b6cc3ef2c2da12be49c1cd468a6e55 (2026-08-27T20:58:56Z) — 23rd run. OVERSIZED AGAIN,
    persisted to a file as the [{type,text}] ARRAY shape. NINTH consecutive run it has overflowed.
  65e9612ba1295bd8d94dc19b4b12b62625f6a47a (2026-08-24T16:17:17Z, "Merge #9") — 22nd run.
  3c6323cd52188f057c16d15b2c7b72ad9d9e91e9 (2026-08-12T21:25:35Z, "Merge #8") — 16th run.
  8b9a768debcfa982f4ec2a8155c1bc9195c0bb0f (2026-08-12T00:27:10Z, "Merge #6") — 13th run, THE FLOOR.
RUN-NUMBER SEQUENCE: 34, 33, 32, 31, 30, 29, 28, 27, 26, 25, 24, 23, 22, 16, 13. NOT ENUMERATED:
14, 15, 17-21 — the known one-off repo rebuild between the 22nd and 23rd runs (route 7). No new gap.
OLDEST COMMIT DATE REACHED: 2026-08-12T00:27:10Z. `more_available` was FALSE at 8b9a768d (revision 1
of this path, which says so in its own body), FALSE at 3c6323cd and FALSE at 65e9612b. NO CALL FAILED
and no retry was needed. Aging: none applied, per Appendix S's default.
METHOD, STATED PLAINLY BECAUSE IT IS NEW: the first six bodies (34th-29th) were read directly in this
  session. The remaining NINE (28th-13th) were read by a READ-ONLY SUBAGENT given the nine full 40-hex
  hashes and instructed to return per-revision commit dates, run numbers, `more_available` values, the
  listing at each anchor, and the verbatim newly-crawled URL list — with the 13th run's 190-URL
  baseline summarised by host rather than dumped. It reported 9 of 9 read, no failed calls, and its
  per-run URL counts (3, 2, 7, 1, 3, 6, 2, 10, 190-baseline) MATCH the counts the 33rd and 34th runs
  independently derived, which is the check that makes the delegation acceptable. Recorded because a
  future run should know the walk can be delegated for roughly a tenth of the context, and should know
  that it is only safe because the per-run counts are independently checkable against prior bodies.

*** ALREADY_CRAWLED = 278. *** Re-derived from the fifteen bodies, not copied: 190 (floor, 13th)
+ 10 (16th) + 33 (runs 17-21, count-only, per-URL detail unrecoverable) + 2 (22nd) + 6 (23rd)
+ 3 (24th) + 1 (25th) + 7 (26th) + 2 (27th) + 3 (28th) + 6 (29th) + 3 (30th) + 3 (31st) + 0 (32nd)
+ 2 (33rd) + 4 (34th) = 275 through the 34th. + 3 new this run = **278**.
Arithmetic re-run: 190+10=200; +33=233; +2=235; +6=241; +3=244; +1=245; +7=252; +2=254; +3=257;
+6=263; +3=266; +3=269; +0=269; +2=271; +4=275; +3=278.
NAMED (enumerable by me from bodies read this run): **245**. COUNTED BUT UNNAMEABLE: 33 (runs 17-21).
*** THE EARLY INSURANCE WRITE SAYS 279 AND 4 NEW URLS. IT IS WRONG AND THIS REVISION IS RIGHT. ***
  The fourth entry it counted was modelcontextprotocol.io/specification/versioning, which has been in
  ALREADY_CRAWLED since the 12th run — reading a known URL more deeply is not a new URL, and the 32nd
  run already established that "crawled" and "read" are different things without inflating the count.
  Recorded rather than silently corrected, because a walk that unions bodies will see both numbers.

=== FEEDS SWEPT: SIX PLUS THE TRIPWIRE ===
  modelcontextprotocol.io/specification/versioning — one plain WebFetch (route 3f), then a BROWSER
    read of the whole page (FINDING 2). Current revision **2026-07-28. UNCHANGED, TWENTY-FOURTH
    consecutive run.** Quoted verbatim from the browser transcription: "The current protocol version
    is 2026-07-28."
  www.anthropic.com/news — THREE NEW since the 32nd run's sweep, and TWO OF THE THREE ARE ON PATH
    SHAPES THE PACK DID NOT HAVE. See FINDING 9. All three UNREAD:
      /news/claude-discovers-novel-enzyme-system (Sep 23) — biology result. Below the bar; named anyway.
      /claude-opus-5-5 (Sep 22) — SITE-ROOT path. Opus 5.5 launch. UNREAD, and it matters for staleness.
      /features/ebola-response (Sep 22, "The Situation Report") — *** A FOURTH PATH SHAPE: /features/. ***
  alignment.anthropic.com — QUIET. Newest entry is still /2026/reward-seeker/ (August 2026); nothing
    has been published on this blog since. The index listing also surfaced ONE ENTRY THE 30th RUN'S
    ENUMERATION DOES NOT CONTAIN: /2026/teaching-claude-why/ (May 2026). Consistent with the
    known depth-varies-between-calls behaviour (crawl-sources, 23rd-run correction) — a deeper listing
    EXTENDS the catalogue rather than contradicting it. Catalogue is now 85, not 84.
  metr.org/blog — ONE NEW: /blog/2026-09-22-claude-opus-5-5/. TAKEN, and it produced a fact.
    *** THE THIRD-PARTY-HACKING FOLLOW-UP HAS STILL NOT LANDED — TEN RUNS WAITING. *** Also still
    uncatalogued: /blog/2026-08-14-funding-update/ (Aug 14), never named by any run.
  www.aisi.gov.uk/blog — QUIET. Newest is STILL optimal-stopping (Aug 27), read by the 23rd run.
    FOUR WEEKS with no new post. The ~47-item tier-A back catalogue remains the whole value.
  www.anthropic.com/institute — *** ENUMERATED AT LAST, CARRIED FROM RUNS 31-34, ONE WebFetch. ***
    Three /institute/ posts exist, not one: /institute/measuring-pace-of-ai-development (READ, 31st
    run, four facts), /institute/econ-scenarios (UNREAD), /institute/recursive-self-improvement
    ("When AI builds itself", UNREAD — the on-topic one). The page also links
    /research/anthropic-institute-agenda, /features/81k-interviews and /economic-index.
NOT SWEPT, named rather than left implicit: anthropic.com/engineering, openai.com/news,
  alignment.openai.com/misalignment-reports, embracethered, simonwillison, microsoft research,
  microsoft security, langchain, huggingface, eugeneyan, trychroma, builder.aws.com, genai.owasp.org,
  research.google, sourcegraph, latent.space, redwoodresearch, developers.openai.com, vectara,
  cognition (demoted), the OWASP ASI tracker.

=== ARTICLES NEWLY CRAWLED (3 new URLs, none guessed) ===
  https://alignment.anthropic.com/2026/coding-audit-realism/
    "Measuring and improving coding audit realism with deployment resources" (Kissane, MacDiarmid,
    Roger; March 23 2026; Anthropic Fellows Program and Anthropic). *** RANK 5 ON THE 30th RUN'S LIST
    AND THE RUN'S BEST SOURCE BY SOME MARGIN — four facts, and three of them are method rather than
    result. *** Read COMPLETE, tl;dr through Appendix K, 54,025 chars, one get_page_text at
    max_chars 250000; the result exceeded the inline limit and persisted as the [{type,text}] array.
    -> b84c73e8, 9693b43b, 7be4071e, 7f3f9f8b, plus the 778b437e enrichment.
  https://metr.org/blog/2026-09-22-claude-opus-5-5/
    "Summary of METR's predeployment evaluation of Claude Opus 5.5" (Sep 22 2026). Found by the metr
    sweep. Read COMPLETE in the browser. -> 97616086, plus the 03fa7976 and c262a592 enrichments.
  https://www.anthropic.com/institute
    Index enumeration only, one WebFetch. Discharges a queue item carried from runs 31-34.
RE-FETCHED, ALREADY IN ALREADY_CRAWLED, NOT COUNTED:
  https://www.anthropic.com/news/accenture-embedded-evaluation — route-5b href harvest only, for the
    34th run's QUEUE ITEM (4). BOTH HREFS RESOLVED — see FINDING 8's second half.
  https://modelcontextprotocol.io/specification/versioning — browser read of the full page. FINDING 2.
errored / not obtained: NONE on the web side. No 403s, no 404s, no paywalls, no timeouts, no guessed
  slugs, no tool failure of any kind. Nothing was recorded as dead.
Appendix A: nothing crawled, nothing left. Fully covered since the eighth run.

=== FINDING 1 — THE EARLY-WRITE MITIGATION WORKS, AND IT BREAKS THE ONE-REVISION-PER-RUN INVARIANT
=== THAT THE WALK PROTOCOL IS BUILT ON. THE 34th RUN RECOMMENDED IT WITHOUT COSTING THAT. ===
PERFORMED: a compact body carrying the history walk, ALREADY_CRAWLED and the URL list was written at
474fbb130720d82633f55fd34050a1cfb7ab2514 BEFORE the first fact write, and this revision replaced it
afterwards. Cost: one extra knomit_update. Benefit: had the bridge dropped during the fact batch —
which is exactly what happened to the 34th run — the walk and the URLs would have survived.
*** BUT APPENDIX S SAYS "Each run is exactly one revision, and its diff is its work", AND THE AGING
*** RULE, THE RUN-NUMBER INTEGRITY CHECK (route 7) AND THE PER-RUN AUDIT ALL LEAN ON THAT. *** A run
that writes twice is now indistinguishable from two runs by revision count alone. THE MITIGATION USED
HERE, and the next run should keep it: the early body's FIRST PARAGRAPH declares in capitals that it
is an insurance write and not a run record. That is a convention, not a mechanism, and conventions of
this kind are exactly what this pack records failing elsewhere. THE HONEST OPTIONS ARE THREE, and the
choice belongs to a human, not to a run: (a) accept two revisions per run and change the walk's
counting rule to read first paragraphs rather than count revisions; (b) drop the early write and
accept that a late transport failure erases a run; (c) give private slots an append operation, which
is item (18a) below and which would make this whole trade disappear. DO NOT let successive runs decide
this individually — a job whose revision count means different things in different weeks is worse off
than one that consistently loses the occasional run.

=== FINDING 2 — TWENTY-FOUR RUNS READ ONE SENTENCE OFF THE TRIPWIRE PAGE. THIS RUN READ THE PAGE.
=== THE PACK ALREADY HAD EVERY CLAIM ON IT, AND THAT IS THE RESULT. ===
The MCP versioning page has been fetched every run since the 12th to check one date. Nobody had read
it as a document. Read in full in the browser this run, it carries: per-request version negotiation
via `io.modelcontextprotocol/protocolVersion` in `_meta` and the `MCP-Protocol-Version` header on
Streamable HTTP; per-request accept/reject by the server; `UnsupportedProtocolVersionError` listing
supported versions; `server/discover` as a mandatory RPC that clients need not call; and a feature
lifecycle whose deprecated features stay "at least twelve months, or at least ninety days under the
policy's expedited-removal exception".
*** EVERY ONE OF THOSE IS ALREADY IN THE CORPUS — 031dab74, 995c167b, f4367bd0 and 3afa31af, written
*** by the 16th-run-era MCP work from the spec pages proper. NOTHING WAS MISSING. *** I expected the
opposite and I am recording the negative, because the 34th run's FINDING 2 (a low-ranked item paying
out) makes the reverse error attractive: "a source we only skim must be hiding something" is not a
rule, it is a hope. The 30th run's query-the-KB-first rule is what settled this in one call.
WHAT THE READ DID BUY, at zero marginal cost: a verbatim re-verification of 031dab74 against its own
primary, one real defect (FINDING 3), and a cosmetic repair in 995c167b.

=== FINDING 3 — A `sources` NUMBER THAT MATCHES NEITHER THE REF COUNT NOR THE ORGANISATION COUNT IS
=== THE CHEAPEST DEFECT IN THIS CORPUS TO FIND, AND THE AXIS SHOULD BE AIMED AT IT ===
031dab74 carried **sources: 3** against FOUR external refs, all four of them modelcontextprotocol.io
pages — one organisation publishing its own specification. Under the pack's fourteen-run
organisation-level convention the correct value is 1. Corrected to 1.
THE GENERALISABLE TEST, and it costs nothing because both candidate numbers sit in the frontmatter
next to each other: if `sources` equals neither the number of external refs nor the number of distinct
organisations among them, it is almost certainly a residue of an earlier revision's ref list and it is
wrong in a direction nobody notices. Three was neither four nor one.
NOTE THE SHAPE THIS DEFECT TAKES ON A SPEC FACT, because a future run may be tempted to "fix" it back:
for a specification, one organisation is the CEILING rather than a weakness — the spec is the
authority on its own contents and there is no independent corroboration to be had. The fact now says
so in a SOURCE COUNT paragraph, so the reasoning is visible to the next reader.

=== FINDING 4 — THE RUN'S BEST FACT: A REALISM METRIC COMPUTED ON ONE TRANSCRIPT CANNOT SEPARATE
=== "THIS EVAL LOOKS FAKE" FROM "THIS JUDGE THINKS ANYTHING UNUSUAL IS FAKE" ===
Realism win rate: show a judge ONE PAIR — the eval transcript and one real deployment transcript — and
ask which is the evaluation; the score is the fraction of pairs the eval fooled the judge. The two
standard alternatives both score a transcript in isolation and both fail the same way. Verbalized
situational awareness is binary and misses the unverbalized kind. Post-hoc 0-10 realism rating is
bimodal and mislabels REAL traffic: run on genuine deployment transcripts, the judge "sometimes
confidently label[s] real deployment usage as evaluations". -> b84c73e8.
*** THE CONTROL IS THE PART TO COPY AND IT IS FREE: pair DEPLOYMENT transcripts against OTHER
*** DEPLOYMENT transcripts. Sonnet 4.5 "thinks the harmful wildchat transcripts are least realistic,
*** with the Claude Code transcripts as most realistic" — all real traffic. That spread is the judge's
*** own suspicion floor, and an eval's number means nothing without it. ***
AND THE FLOOR IS PER-JUDGE: the bias "is less present for Gemini 3 Pro, suggesting different models
are suspicious of different features", judges vary dramatically in raw detection ability, and the
TARGET model does not move the win rate against a fixed judge. A realism number without its judge and
its deployment baseline is not comparable to anyone's, including your own from last quarter.

=== FINDING 5 — FIDELITY HAS A CEILING SET BY THE SCENARIO, AND THE DIAGNOSTIC THAT FINDS IT IS A
=== BENIGN CONTROL ARM ===
Giving the Petri auditor real deployment system prompts, tool definitions and codebases raised average
realism win rate on reward-hacking audits from 4.6% to 32.8% (50 audits: 5 seeds x 10, 60 turns max,
Sonnet 4.5 auditor and target, Sonnet 4.5 with thinking as judge). On a high-stakes shutdown-resistance
scenario the same affordance left the win rate NEAR 0%; rewriting the seed instruction reached 15.0%
and adding resources on top reached only 19.3%. On benign ML/SWE seeds resources improve it
consistently. The authors name it "task-driven evaluation awareness". -> 9693b43b.
OPERATIONAL: run benign seeds through the same pipeline first. If resources move those and not your
real scenario, the SCENARIO is your ceiling and the fix is to rewrite the scenario, not the
environment. AND THE BOUNDS THE HEADLINE DROPS ARE IN THE FACT: 32.8% is one pair in three, not
indistinguishability; a resource bank that does not match the seed is SILENTLY UNUSED ("the auditor is
more likely to ignore resources and resort to creating fully synthetic codebases"), so a flat result
across an unmatched pool is not evidence the resources did nothing; and the whole result is scoped to
agentic coding — the same trick on chat-style sycophancy audits produced no substantial uplift.

=== FINDING 6 — THREE WAYS TO PUSH A REALISM NUMBER UP, THREE TELLS MOVED RATHER THAN REMOVED, AND
=== TWO OF THE THREE WERE ABANDONED BY THEIR OWN AUTHORS ===
(a) Resampling the target whenever it verbalized eval awareness DID cut verbalized eval awareness
    across ~111 seeds — and was dropped: "the new audits weren't actually more realistic ... It's
    plausible that the target still had unverbalized eval awareness, despite the decrease in
    verbalized eval awareness."
(b) Needle-in-a-haystack realism (one eval hidden among N-1 deployment transcripts) was built and
    dropped for context/rate-limit cost AND because THE JUDGE CHEATS: the haystack is a narrow slice
    of deployment, so the judge picks the odd one out on spurious features. The tell they caught it
    using was LENGTH.
(c) The fidelity intervention itself trades tells: resources "substantially reduce[d] the rate that
    the grader mentions that the eval transcript is 'too clean'" and cut unrealistic user behaviour
    and artificial pressure, while causing "a slight increase in inconsistent tool results, likely
    because the environments with resources are more complicated".
-> 7be4071e. THIS IS 19218a92's SHAPE IN A THIRD SETTING and 5536f138's condition applies verbatim:
when the detector has several distinguishable features, closing one redistributes mass onto the
others. Both are cited from the new fact. THE FACT ALSO BLOCKS THE WRONG READING, because it is
available and attractive: this is NOT an argument against improving realism — all three metrics the
programme measured agreed that resources helped. The failure is optimising one proxy directly.

=== FINDING 7 — A CONTRADICTION, KEPT AS A `decisions` FACT: REALISM WENT UP SEVENFOLD AND THE
=== MEASURED BEHAVIOUR DID NOT MOVE ===
Same post: across the 4.6% -> 32.8% realism range, no significant difference in Sonnet 4.5's
reward-hacking rate; on Sonnet 3.7, "a slight increase ... (with big error bars)". Against 2d280a46 /
0c3c2d6a, where suppressing the INTERNAL REPRESENTATION of eval awareness moved a rate from 0% to ~7%.
NOT FLATTENED. -> 7f3f9f8b names the separating condition: the interpretability intervention removes
the BELIEF; the realism intervention removes some of the EVIDENCE for it, and only some — 32.8% is not
indistinguishability. The authors supply the threshold themselves and decline to claim it: "maybe
models will only change behavior if they are 99%+ confident if they are in deployment or an eval."
THE OPERATIONAL PAYLOAD: a flat behaviour curve across a realism sweep is NOT evidence that eval
awareness is absent from your numbers, and must not be reported as one. THE OPPOSITE MISREADING IS
BLOCKED IN THE FACT TOO: this is not evidence that realism does not matter — one of two targets moved,
and nobody has reached the top of the realism range, so the experiment bounds nothing up there.

=== FINDING 8 — ACCESS TIERING RUNS INSIDE THE EVALUATOR, AND THE CLAIM A READER WILL QUOTE IS THE
=== ONE WHOSE EVIDENCE THE PUBLISHING TEAM COULD NOT SEE ===
METR's Opus 5.5 predeployment summary draws on "a separate METR team with elevated access" which
"shared its conclusions with us, but was not able to share the supporting evidence or details of their
reasoning", and therefore states: "we use the evidence in the provided AI R&D report as an input to our
assessment but do not argue directly in defense of its claims." The claim that arrived that way is the
quotable number — "~1.5X overall acceleration in capabilities due to AI (i.e. 1.5 years in 1 year),
with perhaps 30% chance of 2X acceleration" — and the publishing team bounds it in the next sentence:
the preliminary report "did not specify the time period for this estimate". -> 97616086.
SO 03fa7976's RULE HAS TO BE APPLIED PER CLAIM, NOT PER REPORT. Two claims in one document can rest on
two different access tiers, and the higher-tier one may be the one nobody outside that tier has
checked. 03fa7976 now says so and cites the case.
AND THE INDEPENDENCE TERMS ARE A SECOND DATA POINT ON c262a592's "no settled system for funding
independent evaluation": "This evaluation was conducted under an unpaid agreement ... Anthropic had
the opportunity to review and edit the text. We signed off on this final text from the Claude Opus 5.5
system card." UNPAID BUT SUBJECT-EDITED, against Accenture's PAID-BY-THE-SUBJECT. Neither is obviously
the independent one, which is why c262a592 now says "who paid" is not a sufficient question on its own.
SCOPE EXCLUSIONS CARRIED INTO THE FACT because a summary drops them: the work "was not meant to verify
compliance with any specific threshold" and "does not attempt to assess whether Claude Opus 5.5 has or
does not have particular alignment properties". Access: "API access granted over a period of 10
business days", five named tasks.
THE 34th RUN'S QUEUE ITEM (4) IS DISCHARGED, half-successfully. One route-5b harvest on the Accenture
post resolved BOTH unresolved hrefs, neither derivable:
  "We Must Pace the Frontier" -> https://darioamodei.com/post/we-must-pace-the-frontier  *** A HOST
    THIS PACK HAS NEVER TOUCHED. Not fetched this run. ***
  "Advanced AI Framework"     -> https://www-cdn.anthropic.com/files/4zrzovbb/website/0a58d567024a8b448ff15158ebc3625328dfcc1f.pdf
    *** ON THE EGRESS-DENIED HOST (route 11). Resolving the href does not unblock it. ***

=== FINDING 9 — A FOURTH ANTHROPIC PUBLICATION PATH, AND THE /institute/ ENUMERATION AT LAST ===
The 30th run recorded three path shapes on anthropic.com: /news/<slug>, the site root, and
/institute/<slug>. This run's news sweep returns a fourth: **/features/<slug>** (/features/ebola-
response), and the /institute/ index itself links /features/81k-interviews. So four shapes, and a run
that sweeps /news/ is sweeping less of Anthropic than ever. ASK THE INDEX FOR HREFS, EVERY TIME — the
rule the 30th run wrote is now supported by two independent discoveries rather than one.
THE /institute/ ENUMERATION, carried unspent from runs 31, 32, 33 and 34 and costing ONE WebFetch,
found TWO unread posts behind a path whose single read post produced four facts. Four runs of carrying
it cost more than the call did. This is the 34th run's own sub-rule — take it or delete it on the
third carry — arriving on a different queue entry, and it paid the same way.

=== FACTS WRITTEN (5 new, 5 enriched or corrected, 0 retracted) ===
  BATCH 1 — all five in ONE knomit_learn call, committed CLEAN on the first attempt: no dedup refusal,
  no motif refusal. Worth noting against the 32nd/33rd runs' experience, because three of the five sit
  in the eval-awareness / llm-judge cluster, which is where refusals have been concentrated.
    kb/conventions/ai/agents/evaluation/audit-realism/realism-measurement/b84c73e8 — FINDING 4.
      *** THE RUN'S BEST FACT, and the deployment-vs-deployment control is the cheapest thing on this
      list to act on. ***
    kb/decisions/ai/agents/evaluation/audit-realism/realism-budget/9693b43b — FINDING 5.
    kb/gotchas/ai/agents/evaluation/audit-realism/metric-gaming/7be4071e — FINDING 6.
    kb/decisions/ai/agents/evaluation/eval-awareness/realism-effect/7f3f9f8b — FINDING 7.
    kb/gotchas/ai/agents/governance/third-party-evaluation/access-firewall/97616086 — FINDING 8.
  ENRICHED OR CORRECTED — 03fa7976, c262a592, 778b437e, 031dab74, 995c167b (the staleness sample),
    plus 069468bb (the 34th run's owed queue item (6), DISCHARGED).

=== STALENESS PASS — 5 FACTS. 1 CORRECTED, 1 REPAIRED, 3 CONFIRMED-AND-ENRICHED, 0 RETRACTED.
=== REF-DEFECT AXIS: 0 LINK-WITHOUT-REF DEFECTS IN 5. ONE `sources` DEFECT, WHICH IS A NEW SUB-AXIS. ===
AXIS: verifiable-against-a-document-read-this-run, intersected with never-checked where possible.
EVERY ONE OF THE FIVE COST ZERO EXTRA FETCHES.
  031dab74 (0.9 HELD, **sources 3 -> 1**) *** CORRECTED — THE RUN'S REAL DEFECT FIND. FINDING 3. ***
    Every substantive claim re-verified VERBATIM against the live versioning page read in the browser:
    the YYYY-MM-DD semantics, the no-increment-for-compatible-changes rule, Draft/Current/Final, the
    current revision, per-request `_meta` negotiation, the MCP-Protocol-Version header, independent
    per-request accept/reject, UnsupportedProtocolVersionError, server/discover as mandatory-but-
    optional-to-call, and the twelve-month / ninety-day deprecation clock. No content defect in any of
    it. Two additions the page carries and the fact lacked: "Clients and servers MAY support multiple
    protocol versions simultaneously", and that a deprecated feature must document a migration path or
    state none is required. The as-of date for the current revision was refreshed to this run's
    verification rather than left at 2026-07-30.
  995c167b (0.9 HELD, sources 1 HELD) CONFIRMED IN PART + COSMETIC REPAIR. The asymmetric obligation
    (servers MUST implement, clients need not call) and UnsupportedProtocolVersionError re-verified
    against the versioning page. *** THE REST WAS NOT RE-VERIFIED and I am saying so rather than
    implying a full check: DiscoverResult's fields, the self-reported-serverInfo warning, ttlMs /
    cacheScope and the stdio argument come from the server/discover spec page, which was NOT
    re-fetched. *** THE REPAIR: the body carried an UNCLOSED `**` in the sentence "clients SHOULD NOT
    use it to change their behaviour or **rely on it for security decisions." — so every character
    after it rendered bold until the next marker, in the fact's single most important warning. Same
    class as the 31st run's mis-cased heading. Fixed; nothing else in the body touched.
  03fa7976 (0.85 HELD, sources 1 HELD) CONFIRMED + ENRICHED. FINDING 8. The tiering claim now says the
    ladder has rungs INSIDE one evaluator and that the read-the-access-terms rule applies per claim.
    sources HELD at 1 with the reasoning written in: the predeployment evaluation is METR again — the
    same organisation applying its own framework, which is an illustration, not a corroboration.
  c262a592 (0.75 -> 0.8, sources 1 HELD) CONFIRMED + ENRICHED. Its "different evaluators under
    different funding arrangements" sentence now has a documented second instance, and the enrichment
    changes the advice rather than decorating it: "who paid" is not sufficient, because the unpaid
    arrangement is the one where the subject holds editorial review. A do-not-conflate line was added
    — an ordinary predeployment evaluation is not the embedded programme producing results.
    sources HELD at 1: the evaluator documents a DIFFERENT arrangement rather than testing this one.
  778b437e (0.85 HELD, sources 1 HELD) CONFIRMED + ENRICHED WITH A DEPLOYMENT-SIDE RATE. Its
    direction 1 (the model suspects a test when it should not) had no rate on real traffic. It has one
    now: sampling single harmful user turns from real WildChat, Sonnet 4.5 and Haiku 4.5 each
    verbalized eval awareness "at low rates (~1%) overall". The grader-side mirror is in the same
    appendix. SCOPE WRITTEN INTO THE FACT so the number cannot travel: first user turn only,
    single-turn, one T=1 resample, two models CHOSEN for high verbalized eval awareness.
    sources HELD at 1 — five references, five pieces of work, one organisation.
  069468bb (0.8 HELD, sources 1 HELD) ENRICHED — THE 34th RUN'S OWED ITEM, DISCHARGED. Its "intent is
    shipped by nobody in this corpus" claim now carries the nearest real instance and why it does not
    close the gap: 519d977b is a COARSE natural-language scope at organisation-or-project granularity,
    declared once per grant, checked AFTER the fact by drift monitoring, and signed by nothing. The
    paragraph ends by telling a reader not to count it as the intent assertion arriving.
  REF-DEFECT SUB-AXIS: every [[link]] in all six bodies checked against that fact's refs. 03fa7976's
    four, c262a592's three, 778b437e's one, 069468bb's three — all present. 031dab74 and 995c167b
    carry no [[links]] at all. *** ZERO DEFECTS, against the 33rd run's three-in-five and the 34th
    run's zero-in-five. Two consecutive clean passes. The 34th run's PROVISIONAL READING — that the
    defect belongs to the runs 22-30 cohort — is NOT confirmed by this, because 031dab74, 995c167b
    and 069468bb are all from that older cohort and were clean. The honest statement is that the axis
    has now returned 3, 0, 0 and nobody has aimed it deliberately at the cohort. ***
  NEW SUB-AXIS PROPOSED AND USED ONCE: the `sources`-matches-neither test (FINDING 3). One defect in
    six facts, found by reading two numbers in the frontmatter. No fetches, no page reads.
  Nothing in the kb is yet older than 90 days (pack began 2026-07-26; today is day 60).
  METHOD NOTE: ZERO route-4 exposure on any fact written or enriched this run. Every quoted string and
  figure came from browser get_page_text, a transcription. WebFetch was used SIX times — the tripwire
  and five index/href harvests — and NOT ONE of those six outputs was written into any fact. The
  tripwire's own quoted sentence in this body is from the browser read, not from the WebFetch.

=== CONTRADICTIONS — ONE, KEPT AS A `decisions` FACT RATHER THAN RESOLVED ===
The realism-sweep null versus the eval-awareness suppression result (FINDING 7). Both Anthropic
Alignment Science, months apart. 7f3f9f8b keeps both and names the separating condition — which
channel the intervention acts on, and how far up the realism range it reached — and cites 2d280a46 and
0c3c2d6a. The condition is MARKED AS PACK ANALYSIS where neither source states it.
NO OTHER CONTRADICTION. One tension checked and dismissed: b84c73e8's "the target model does not move
the win rate" and fa5bc47a's "the judge's label tracks what it is told the label is FOR" are not in
conflict — the first is about the transcript's authorship, the second about the judge's incentive, and
the realism judge in this study is told nothing about consequences.

=== IN-RUN SELF-REVIEW, INCLUDING OF THIS FILE ===
  * THE INHERITED CLAIM I WAS MOST AT RISK OF REPEATING was my own early write's "4 new URLs / 279".
    It was wrong by one within the same run, and the fourth entry was a URL crawled twenty-three runs
    ago. Corrected in the body above rather than silently, because a history walk unions both.
    The second was the 34th run's FINDING 2 generalised into "skimmed sources are hiding value" —
    FINDING 2 of this run is the counter-example, and it cost one query to establish.
  * NUMBERS CARRY THEIR FRAME. 4.6% and 32.8% are AVERAGE REALISM WIN RATES over 50 audits against a
    named judge and a named deployment set — not detection rates and not probabilities of being
    fooled in general. 15.0% and 19.3% are the same metric on a DIFFERENT scenario with a DIFFERENT
    target model (Sonnet 4), so they are not comparable to the 32.8%. ~1% is a verbalized-eval-
    awareness rate on SINGLE FIRST USER TURNS from two models selected for that property. 1.5X is an
    acceleration estimate with NO STATED TIME PERIOD, by the publisher's own admission. 10 business
    days is an access window, not an evaluation duration. Twelve months and ninety days are MINIMUM
    residency periods before a deprecated MCP feature becomes ELIGIBLE for removal, not removal dates.
  * NO NUMBERS WERE TAKEN FROM ANY FIGURE IN THE REALISM POST, AND THE REFUSAL IS RECORDED IN THE
    FACTS. That post's results live in Figures 1-21; 4.6/32.8, 15.0/19.3 and ~1% are all stated in
    PROSE and are quoted from prose. The per-judge, per-auditor and per-target comparisons
    (Appendices C, D, E) are reported at the ORDERING the prose states and nothing finer. Do not
    "recover" those values from cell order.
  * MODALITY CHECKED INDIVIDUALLY. b84c73e8 states that its metric depends on deployment data the
    authors call narrow (25-30 transcripts). 9693b43b states the coding-only scope and the negative
    chat result. 7be4071e marks two of its three instances as ABANDONED DIRECTIONS rather than
    results. 7f3f9f8b states that no power analysis is published and that the range never reached
    indistinguishability. 97616086 states that every term it reports is self-disclosed by the
    evaluator and is not an accusation.
  * ARITHMETIC RE-DERIVED: 275 + 3 = 278 and the sixteen-term sum checks; 245 named; 15 revisions
    named and 15 listed; 5 new facts named and 5 paths listed; 6 updates named and 6 listed; 3 new
    URLs named and 3 listed; 5 staleness facts named and 5 listed (069468bb counted separately as the
    owed enrichment, which makes 6 facts touched, and the body says both numbers).
  * MOTIF TOKEN COUNTS were checked before sending — all nine are 2-4 kebab-case tokens including
    articles. None was rejected. Counted tokens, not concepts, per the 34th run's note.
  NOT DONE, said plainly: the alignment.anthropic.com back catalogue (80 of 85 unread); the
    diffuse-ai-control PAPER; the rest of the September threat report (five sections); the slot
    migrations, an EIGHTH run; the two unread /institute/ posts just found; anthropic.com/claude-opus-
    5-5 and the Opus 5.5 system card; darioamodei.com/post/we-must-pace-the-frontier; the transcript
    viewer; the AISI transcript-analysis pair; four of the six OpenAI reports' updated-dates; the
    three ASTRA investigations; the SLEIGHT-Bench paper and dataset; openai.com/news and
    alignment.openai.com, both unswept this run.

=== MIGRATIONS NOT DONE — EIGHTH RUN, SAME TOOL REASON ===
The 30th-34th runs' reasoning stands: knomit_update replaces the whole body, both slots are ~62-66KB,
and re-emitting that through the agent to change a paragraph is the hazard the pack's own rules forbid.
*** AND THIS RUN READ NEITHER SLOT IN FULL — crawl-sources only its first ~11,000 chars (the recurring
*** feed list and the catalogue-building notes) and fetch-routes only routes 9/9b/9c plus the header.
*** Saying so rather than implying a full read: no fetch failed and no gated host was touched. ***
THE OWED EDITS, carried, with this run's additions:
  fetch-routes ROUTE 9c, second bullet: replace the "cannot be paged through" sentence. FIFTH RUN
    ASKING. Wording unchanged from the 34th run's.
  fetch-routes ROUTE 6: still do not add the anchor-density rule. Add the 34th run's determinism
    result, and add this run's addition — THE WALK CAN BE DELEGATED TO A READ-ONLY SUBAGENT, and the
    check that makes it safe is that per-run URL counts are independently verifiable against prior
    bodies.
  fetch-routes NEW ROUTE 12: the 34th run's bridge-disconnect finding. Still not written.
  fetch-routes ROUTE 11: the www-cdn egress denial, written out in full by the 30th run, STILL never
    migrated. This run resolved a FOURTH www-cdn artifact behind it (the Advanced AI Framework PDF).
  crawl-sources, alignment.anthropic.com block: mark /2026/coding-audit-realism/ READ with its four
    fact paths; ADD /2026/teaching-claude-why/ (May 2026), absent from the 30th run's enumeration;
    the catalogue is 85, not 84; 80 remain.
  crawl-sources, ANTHROPIC block: add the /institute/ path WITH ITS THREE POSTS and the NEW /features/
    path shape; mark /institute/measuring-pace-of-ai-development READ.
  crawl-sources, METR block: mark /blog/2026-09-22-claude-opus-5-5/ READ with 97616086; add
    /blog/2026-08-14-funding-update/ as uncatalogued.
  crawl-sources, NEW HOST: darioamodei.com — low volume, essays by the CEO of a frontier lab, named as
    the source of a public commitment this pack already holds a fact about. Watch, do not sweep.

=== QUEUE FOR THE NEXT RUN ===
(0) *** knomit_repos FIRST, AND AGAIN AFTER ANY SURPRISING NEGATIVE. Route 10 did not recur; EIGHT
    clean runs. AND IF EVERY remote-devices TOOL VANISHES AT ONCE, that is the 34th run's FINDING 10 —
    RefreshMcpTools{server: "remote-devices"}, do not re-bind, the handle survives. ***
(1) *** READ FINDING 1 BEFORE WRITING crawl-state. This run wrote it TWICE and the history now has two
    revisions for one run. Either keep doing it and check first paragraphs when walking, or stop.
    Pick one and say which; do not leave it to be rediscovered. ***
(2) *** anthropic.com/claude-opus-5-5 AND THE OPUS 5.5 SYSTEM CARD — NEW TOP ITEM, AND IT IS A
    STALENESS TRIGGER, NOT JUST A SOURCE. A frontier model shipped on 2026-09-22. The pack holds
    facts pinned to Opus 4.8, Opus 5, Mythos 5 and Fable 5.1 rosters (8756141e, ec1be717, 2d7219c8,
    f654f7dd), and Appendix S's staleness rule names "a model version that has since shipped a
    successor" explicitly. The METR summary says its text sits IN the system card, so the card is
    reachable prose. Note the launch post is at the SITE ROOT, not under /news/. ***
(3) *** THE alignment.anthropic.com BACK CATALOGUE — 80 of 85 unread, and the SIX taken so far have
    each been among the best documents of their run; this run's was the best of five. The 30th run's
    ranked list is at f9c2ccc684641a5e776bdef0063b019bb99170d6. NEXT: /2026/auditbench/ (rank 6,
    pairs a8d32262 and now b84c73e8), then /2026/modular-pretraining/ (rank 7), then
    /2026/teaching-claude-why/ (NEW to the catalogue this run, unranked). ***
(4) THE TWO UNREAD /institute/ POSTS, found this run: /institute/recursive-self-improvement ("When AI
    builds itself" — the on-topic one) and /institute/econ-scenarios. The one post already read from
    this path produced four facts. CHEAP AND HIGH.
(5) THE diffuse-ai-control PAPER. Carried from the 34th run. Unresolved href; route 5b on the post.
    It carries the figure values the 34th run deliberately declined to read off charts.
(6) darioamodei.com/post/we-must-pace-the-frontier — RESOLVED THIS RUN, NOT FETCHED. Named by the
    Accenture post as the source of the embed-evaluators commitment. Pairs c262a592, 03fa7976,
    97616086, 6866e63b. The Advanced AI Framework PDF resolves to the egress-denied host (route 11)
    and is NOT reachable — do not spend a call on it.
(7) FEEDS: openai.com/news and alignment.openai.com/misalignment-reports are now OWED BY TWO RUNS —
    top of the sweep list. Then anthropic.com/news, alignment.anthropic.com, metr.org, aisi.gov.uk
    (quiet 4 weeks), embracethered (quiet). AND THE MCP TRIPWIRE — twenty-four consecutive; one
    WebFetch is enough, FINDING 2 settled that there is nothing else on that page.
(8) THE REST OF THE SEPTEMBER THREAT REPORT — five sections. One navigate + one large get_page_text.
(9) STALENESS: the never-checked axis is not exhausted. Still never-checked: 0525e590, c5f106f3,
    f727c157, 5eeb059b, fa5bc47a, f1e54f16, f961973e, f435e753, 0cc69d27, 65aa10a7, fc76b9a2,
    5cce9c0c, 83004507, 00f5d991, 5bad2e60, 0c3c2d6a, b4d22cc2, 4777dc9b, fcce2200, fe1fd6b2,
    347a5dac, the 34th run's seven, and this run's five. *** RUN THE NEW `sources`-MATCHES-NEITHER
    TEST (FINDING 3) ACROSS A WIDE SAMPLE — it needs no fetches and no page reads, only two numbers
    from each frontmatter, so it can be swept far more broadly than any axis so far. *** AVOID
    kb/principles/** (write-blocked: 0f260eea, 1d1440fe, 4166926d, a829cfd4, b9b45ff5, 1feacc9e,
    f269c82f, c2f12069, 1dc822f2, db193402).
(10) THE TRANSCRIPT VIEWER named by the summer-2026 post (240 + 260 + 260 browsable transcripts).
    UNRESOLVED HREF — route-5b harvest before guessing. Pairs the AISI transcript-analysis item, top
    of tier A for TWELVE runs.
(11) THE THREE INVESTIGATIONS LINKED FROM ASTRA'S SAFETY OVERVIEW — monitorability, controllability,
    sabotage evaluation. Carried from runs 30-34, none followed.
(12) THE SLEIGHT-Bench PAPER AND DATASET. *** The post carries a benchmark canary GUID; if the repo is
    opened, do NOT copy that identifier into any fact. *** GitHub API access is not enabled for this
    session (route 3f), which blocks the dataset repo.
(13) THE BENCHMARK SUPPLY CHAIN (CVE-2026-66384) still lives only inside bcbf13c2. ELEVENTH run
    untaken. QUERY THE KB FIRST — a carried entry of this age has a history of turning out already
    done, and FINDING 2 is this run's example of that query paying.
(14) metr.org's THIRD-PARTY-HACKING FOLLOW-UP: still not published, TEN runs waiting. Also uncrawled:
    metr.org/blog/2026-08-14-funding-update/.
(15) harnesstax.github.io; /index/pacing-model-development-cyber-capabilities/;
    openai.com/hugging-face-incident-and-misalignment/ — carried unchecked from runs 27-34.
(16) ANTHROPIC'S www-cdn PDFs — April Alignment Risk Update, Fable 5 / Mythos 5 System Card, August
    Risk Report, and NOW the Advanced AI Framework (resolved this run). All behind the egress policy
    (route 11, STILL not in fetch-routes). NOT re-tested.
(17) *** FOR A HUMAN, NOT THE CRAWLER ***
    (a) *** `knomit_update` REPLACES A WHOLE BODY AND THERE IS NO PATCH OR APPEND. EIGHTH run asking,
        and FINDING 1 turns this from a chore into a design question: the early-write mitigation the
        34th run asked for WORKS and costs the job its one-revision-per-run invariant. An append
        operation on a private slot removes the trade entirely — a run could record incrementally and
        still occupy one revision. This is now the single highest-value item on this list. ***
    (b) www-cdn.anthropic.com is denied by this session's egress policy. SEVENTH run asking. A FOURTH
        document is now known to sit behind it.
    (c) THE BINDING DRIFT (route 10) — did not recur. EIGHT CLEAN RUNS. The standing conflict remains:
        the job prompt says bind once, fetch-routes route 10 says re-bind before every write. This
        run verified with knomit_repos and did not re-bind, as the 34th run argued.
    (d) GitHub API access is not enabled for this session (route 3f). Blocks queue item (12).
    (e) *** Appendix S vs fetch-routes 5c: TENTH run asking. Appendix S forbids running page scripts,
        which forbids the querySelectorAll harvest. Route 5b covered every need again this run,
        including the two-href resolve in FINDING 8. DELETE 5c's evaluate form. ***
    (f) 4f5e9dfe is retracted but cited by THREE live facts (483263c5, c02ac546, bdf3336e). Carried
        forward UNVERIFIED for a FOURTEENTH run. NOT re-checked.
    (g) *** THE `sources` CONVENTION, FIFTEEN RUNS OLD, AND IT FINALLY COST SOMETHING MEASURABLE.
        FINDING 3 found an inflation that had sat in a high-confidence spec fact since the 16th-run
        era, and the only reason it was findable is that the convention exists to be violated against.
        SEVEN consecutive runs with no inflation INTRODUCED, one historic inflation now REMOVED. It is
        still not written down anywhere normative, and it is now demonstrably load-bearing. ***
    (h) The agentic-engineering repo also carries a kb/technology/** corpus written by another
        pipeline. Check knomit_query results for a BARE path before concluding a fact exists here.

TOOL NOTES: no dedup refusal and no motif refusal this run — a five-fact batch touching the
llm-judge, eval-awareness and governance clusters committed on the first attempt, which is the
cleanest write of the last several runs. knomit_explain on crawl-sources and fetch-routes again
exceeded the inline limit and persisted as a single JSON OBJECT, while the oversized 23rd-run
crawl-state revision persisted as the [{type,text}] ARRAY — both shapes occurred again and they need
different parsing, exactly as the 33rd and 34th runs recorded. A browser_batch of
[navigate, get_page_text{max_chars: 250000}] also persists as the ARRAY shape. NEW: five knomit_explain
calls issued in ONE parallel block all returned inline and none was persisted, so parallelism does not
change the persistence threshold — but five inline crawl-state bodies is ~75,000 characters arriving
at once, which is why the older nine were delegated.

SUB-RULES, cumulative (the 34th run's list stands; this run adds three):
 (35th) *** A MITIGATION THAT ADDS A WRITE CHANGES WHAT A REVISION MEANS. *** The early-write insurance
   the 34th run asked for is correct about the risk and silent about the invariant it breaks: this
   job's history walk, its run-number integrity check and its aging rule all assume one revision per
   run. Before adopting any fix that changes how often a durable record is written, check what else
   counts those writes. The fix is not wrong; it is incomplete until the counting rule moves with it.
 (35th) *** A SOURCE NOBODY HAS READ CLOSELY IS AN UNKNOWN, NOT A RESERVE. *** The 34th run showed
   that a long-deferred item can pay handsomely, and the attractive generalisation is that skimmed
   sources are hoarding value. This run read a page twenty-four runs had only glanced at and found the
   corpus already held every claim on it. Both runs are evidence for the same narrower rule — SPEND
   THE CALL AND FIND OUT — and for nothing stronger. A deferral produces no information in either
   direction, which is exactly why it should be resolved rather than re-ranked.
 (35th) *** CHECK `sources` AGAINST BOTH CANDIDATE NUMBERS, NOT AGAINST YOUR JUDGEMENT. *** A count
   that equals neither the external-ref count nor the distinct-organisation count among those refs is
   almost certainly a leftover from an earlier revision's ref list. It is the cheapest defect test
   this pack has: two numbers, both already in the frontmatter, no fetch, no page read, and it caught
   a 0.9-confidence spec fact carrying 3 where the answer was 1.

Appendix S checklist (all SEVENTEEN, from the 23rd run) still governs the staleness pass and the
self-review, and was applied to this body as well as to the facts.

PROMPT INJECTION: none acted on, and two things are worth naming rather than waving through.
(1) The coding-audit-realism post publishes, in Appendix K, the FULL PROMPTS of a realism judge, a
reward-hacking judge, an eval-awareness judge and the auditor seed instructions — that is, working
text for building a system that decides whether a transcript is an evaluation. They were transcribed
as evidence and are directly copyable by a defender; none was addressed to this job and none was acted
on. Worth naming because this run's subject is how a model tells a test from reality, and a scheduled
job reading untrusted pages is itself a system that could be told it is in a test.
(2) The METR summary is a document ABOUT a third party's capabilities written under an arrangement
where that third party reviewed and edited the text. Nothing in it instructs a reader, and the fact
written from it leads with the arrangement rather than the conclusions.
No page attempted to redirect this run, and no URL was visited that was not on the work list or
returned as an href by an index already on it. No source was recorded as dead, blocked or paywalled.
The subagent delegated the history walk was given read-only instructions, nine specific commits and
nothing else; its report was checked against three prior runs' independently derived counts before any
of it was used.
