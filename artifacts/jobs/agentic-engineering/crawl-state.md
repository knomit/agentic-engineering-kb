---
type: observation
domain: []
confidence: 0.7
sources: 1
entities: []
refs: []
---
# agentic-engineering crawl: last crawl state

crawled: 2026-10-08 (forty-ninth run, ~13:20Z). 3 facts written, 3 enriched, 0 corrected, 5 confirmed, 0 retracted. 1 genuinely new URL. ~24h since the 48th run. crawl-state written ONCE, at the end, at the artifacts path.

*** THE HEADLINE IS A CORRECTION TO THIS RUN'S OWN FIRST CONCLUSION, AND THE DEFECT IT EXPOSES WILL HIT EVERY RUN UNTIL A HUMAN EDITS APPENDIX S. ***
This run read the three slots Appendix S names -- the .knomit/ paths -- found crawl-state's HEAD dated 2026-10-06 (the 47th run), then found nine fact revisions stamped 2026-10-07 13:47-13:50Z referencing URLs that appear in NO crawl-state revision. It concluded that a run had executed and left no record, reported that as its headline, and pushed the record out to a file for a human to land.
THAT CONCLUSION WAS WRONG. The 48th run recorded itself completely -- at artifacts/jobs/agentic-engineering/crawl-state.md, having discovered the same .knomit/ write closure, migrated all three slots, and written a thorough account including the instruction to read both halves. It was invisible to this run for exactly one reason: *** APPENDIX S STILL NAMES THE OLD PATHS, SO A RUN THAT FOLLOWS ITS PROMPT FAITHFULLY READS A SLOT THAT STOPPED BEING CURRENT AND HAS NO INSTRUCTION TO LOOK ANYWHERE ELSE. *** The 48th run's migration note is at the new path, which is the one place a run working from the spec will not look. A forwarding pointer cannot live only at the destination.
COST, MEASURED: two wasted WebFetch calls re-reading the metr 2026-10-06 post the 48th run had already mined, one wasted history walk duplicating the 48th run's, and a false headline notified to a human. The walk and the notification are the expensive ones.
WHAT STOPPED IT FROM BEING WORSE, AND IT IS THE LESSON: the recency screen. knomit_query{sort:"recent", path:"kb"} with committed_at read off each row exposed the 10-07 activity in ONE call, before any duplicate fact was written. It did not identify where that run had recorded itself -- only a guess at the artifacts path did that -- but it prevented every duplicate write. *** RUN IT FIRST, EVERY RUN, BEFORE THE HISTORY WALK. *** See screen (h).
WHAT A HUMAN MUST DO: Appendix S's "Job state" table, its "Reading a slot" and "Writing a slot" sections, and crawl.md step 1's three explicit knomit_explain paths all name .knomit/jobs/agentic-engineering/. Writes there are refused; the live slots are artifacts/jobs/agentic-engineering/. The 48th run asked for this as its item (a); this is the second ask and the first with a measured cost attached.

*** SECOND FINDING: THE ONE NEW DOCUMENT WAS MISSED BY THE 48th RUN BY HOURS, NOT BY METHOD, AND THAT IS A CADENCE DEFECT WORTH FIXING IN ONE WORD. ***
aisi.gov.uk published /blog/transect-... on 2026-10-07. The 48th run swept that feed on 2026-10-07 at ~13:47Z windowed since 10-01 and correctly reported nothing new. A job that sweeps at a fixed hour systematically misses same-day publications, so "nothing new" on a window that includes today is weaker evidence than it reads as. The fix is free: window the sweep from the day BEFORE the last run, not from the last run's date. The window is a prompt argument and costs nothing.

*** THIRD FINDING: A TOOL-BEHAVIOUR CONTRADICTION BETWEEN THIS RUN AND THE 48th, KEPT RATHER THAN FLATTENED. *** This run's subagent reports that knomit_explain anchored at an explicit `commit` returns NO history object at all -- 37 calls, 37 times, no history key, no revisions, no more_available. The 48th run reports the opposite on the same path with the same kind of call ("more_available was true on every read except the floor's"). Both runs used a subagent, both had zero failures, and both independently reproduced the same four byte-comparisons, so neither looks careless. Written up as fetch-routes route 36 with two untested explanations (a server change between the runs; or the response shape differing by inline-vs-persisted body) and the one cheap test that distinguishes them. THE OPERATIONAL ANSWER IS THE SAME UNDER BOTH READINGS: walk by the prose hashes, never by history.revisions.

*** THIS SLOT HOLDS ONE RUN. THE HISTORY IS THE RECORD AND IT NOW SPANS TWO PATHS. The 40-hex list below is load-bearing infrastructure: every run MUST reproduce its predecessors' hashes and append its predecessor's. A single omission severs the chain, and the chain depends on this body naming the OLD PATH, because the new path's history is two revisions deep. This is the one non-optional thing in this body. ***

=== HISTORY WALK -- COMPLETE, AND LARGELY REDUNDANT WITH THE 48th RUN'S. 37 CALLS, 37 BODIES, ZERO FAILURES, ZERO RETRIES, VIA A READ-ONLY SUBAGENT. NINTH CONSECUTIVE CLEAN RESULT WITH THE SUBAGENT METHOD. ===
I did not know the 48th run's walk existed when I commissioned this one, so the two are INDEPENDENT measurements of the same object -- which is the only thing that makes the duplication worth anything. They agree on everything they both measured:
  BYTE-COMPARISONS, both runs, via the `blob` field (route 34), identical results: 9c0017f0 == 4adb2a6f (blob 8b471601, 38,251); 474fbb13 == 047c8878 (blob 593afb00, 4,798); d56dc137 == 68c341e1 (blob 284d2dfb, 48,482); fc85537f DISTINCT (blob 9e402507, 37,194).
  THE FOUR "UNRESOLVABLE" HASHES, both runs: all four resolve. Runs 15, 20 and 21 are recovered in full.
  THE FLOOR RECOUNT, both runs: exactly 190 entries, 189 recording a fetch; the one non-fetch is openai.com/index/responding-to-the-next-frontier-of-critical-cyber-capabilities/ (404, guessed slug).
  THE 21st RUN'S TRUNCATED AISI SLUG, both runs: /blog/what-can-sandboxed-ai-agents-learn-about-their-evaluation-environments.
ONE ADDITION THIS RUN'S SUBAGENT MADE THAT THE 48th'S DID NOT: be04dee3 has blob 012bcc3d, 36,904 bytes, DISTINCT from both fc85537f and 9c0017f0. So the 42nd run's FOUR revisions are THREE distinct bodies (be04dee3 -> fc85537f -> 9c0017f0 == 4adb2a6f), and the 9c0017f0/4adb2a6f pair is a genuine no-op commit. It also found that the 21st run's body CLAIMS 8 new URLs and ENUMERATES ONLY 7; the discrepancy is recorded rather than papered over and no eighth URL was invented.
ONE CORRECTION TO THIS RUN'S OWN EARLIER REPORT: it listed openai.com/index/expanding-daybreak-... as still unrecoverable. The 48th run resolved it from the 15th run's body: /index/expanding-daybreak-as-the-cyber-defense-window-narrows. ONLY ONE TRUNCATED SLUG REMAINS: microsoft.com/en-us/research/blog/echoverse-... (22nd run).
OLDEST COMMIT DATE REACHED: 2026-08-12T00:27:10Z (8b9a768d, the 13th run, THE FLOOR; its body says it crawled 2026-08-10). The walk terminated at the FLOOR by its own declaration. more_available was not consulted -- see finding 3.
Run-number sequence, full 40-hex, newest first. Entries through the 47th are AT THE OLD PATH .knomit/jobs/agentic-engineering/crawl-state.md; the 48th is the FIRST at artifacts/jobs/agentic-engineering/crawl-state.md. APPEND THIS RUN'S COMMIT AS THE 49th:
  c779103bcecca40fbe135f4a14e70e03b83cbddb  2026-10-07T14:03:35Z  48th  <- FIRST AT THE NEW PATH
  d94470cec9869e4691e38da82e50da487c0c20d2  2026-10-06            47th (branch-head alias, route 24; the 47th run's own body mislabelled its predecessor's hash as "46th" -- the 48th run corrected the off-by-one and this list carries the correction)
  ff2b839598bcdd7cb93e28d9aed4bc64f03bb00b  2026-10-04T13:42:00Z  46th (alias ac330fb01fa0b7dd11e5c972106c51d763c9a3c2)
  8ed3cc92180fec27a867e1268ff2e903dbe88f5f  2026-10-03T13:47:23Z  45th
  4b311b107c8109caabc60fda0d9b059ea86a653e  2026-10-02T13:52:24Z  44th
  c9e40f23e1ed95c4a3c15bad985a932889d0187c  2026-10-01T13:45:22Z  43rd
  9c0017f0a7e18fd89150c527b3627f903a19139e  2026-09-30T22:53:53Z  42nd (final of FOUR; THREE distinct bodies)
  4adb2a6fd45799dc751639bbcc3ca32c876cd054  2026-09-30T22:51:04Z  42nd SUPERSEDED (== 9c0017f0, a no-op commit)
  fc85537f909eb2427916881044afa4a165db2121  2026-09-30T22:50:42Z  42nd SUPERSEDED (DISTINCT, 37,194)
  be04dee338397d3a396ef08af11853e2bb15d06e  2026-09-30            42nd SUPERSEDED (first write, DISTINCT, 36,904)
  76cc1a5d46d808fa757e3980ff30f2655746cf7e  2026-09-30T13:48:07Z  41st
  719ae8b25516d04ac8ab87d0175b754aa3adbee3  2026-09-29T13:52:31Z  40th
  375dc0f79ba2cc89b6482939b55ff377c36a6e0d  2026-09-28T13:50:17Z  39th (== history alias 182c7f61, proved by blob 59e9a88f on the 48th run)
  092218eef959413b6ebf8589b29ecf5a37e5a49f  2026-09-27T13:40:18Z  38th
  7a39df486016fcd1dc19831a8675224b2bc9d447  2026-09-26T13:51:25Z  37th
  cc9be5500ab1e8e44c6bb1d7e9b300bf740c59d3  2026-09-25T13:48:57Z  36th
  474fbb130720d82633f55fd34050a1cfb7ab2514  2026-09-24T13:17:44Z  35th INSURANCE (NOT a run)
  047c8878bf8dc193b2dc33e6295eaf0a6bf25527  2026-09-24T13:21:15Z  35th INSURANCE #2 (== 474fbb13)
  d56dc137c2697f4e31effccbc995ec79e8989376  2026-09-24T13:30:41Z  35th INSURANCE #3 (== 68c341e1, a no-op)
  68c341e16d1910c93c8bbf4c0489052f6d522230  2026-09-24T13:36:20Z  35th (final)
  66535f3fc655e3f79f1358c9d746645ca52e461d  2026-09-23T16:25:44Z  34th
  ec73cbc1c1cfc857eeb6e6e8ffbd5954d0342302  2026-09-22T13:36:55Z  33rd
  2230476f8179685a6b6e4aa59d031424e62dff2e  2026-09-21T13:41:17Z  32nd
  94183c20c3ac8aac08194f1b5676776914614440  2026-09-20T13:31:51Z  31st
  f9c2ccc684641a5e776bdef0063b019bb99170d6  2026-09-19T15:58:33Z  30th
  0715d1c09f36a89040bbbc1cd64d2a7bee24ab17  2026-09-18T21:06:54Z  29th
  f7e3e43133c4477728c47574d874a660bc3acced  2026-09-18T13:43:53Z  28th
  c3bbd6a3fa70de972d7a17d966e1338b67abfa41  2026-09-17T19:37:28Z  27th
  20eb4edb0910f3ce70697deb7ee20391819fbced  2026-09-13T15:48:52Z  26th (body says crawled 2026-09-08)
  c6cab79802bfc5ad45da90851f698de37ba8d1cb  2026-08-29T15:12:58Z  25th
  91f7d0857b745035973adfb6d543960e53e59779  2026-08-28T14:43:22Z  24th
  7462e9f229b6cc3ef2c2da12be49c1cd468a6e55  2026-08-27T20:58:56Z  23rd
  65e9612ba1295bd8d94dc19b4b12b62625f6a47a  2026-08-24T16:17:17Z  22nd (body says crawled 2026-08-21)
  4cce7781b385029bfc69a0f396e5837baca956cc  2026-08-21T01:44:42Z  21st (RESOLVED 48th, re-read 49th)
  226499515b8c356590e36af79b7566a10fbebb14  2026-08-18T00:07:35Z  20th (RESOLVED 48th, re-read 49th)
  3c6323cd52188f057c16d15b2c7b72ad9d9e91e9  2026-08-12T21:25:35Z  16th
  5ab895cfc9bf03c4eabb2f8de3d74c90b69c9103  2026-08-12T14:40:43Z  15th final (RESOLVED 48th, re-read 49th)
  8be9e4de715e09be45e74591f68413de8c717ad5  2026-08-12T14:34:18Z  15th first (RESOLVED 48th, re-read 49th)
  8b9a768debcfa982f4ec2a8155c1bc9195c0bb0f  2026-08-12T00:27:10Z  13th -- THE FLOOR
  c9f7e713d3230846f02b1ac72c9f7f8448e4312d  2026-08-12T00:19:57Z  SLOT CREATION, 8 min PRE-FLOOR, action=added, "jobs: cut agentic-engineering state over to .knomit/jobs named slots". STILL UNREAD by any run, and it is a full 40-hex -- the one remaining resolvable pre-floor revision. ONE CALL.
ALIAS HASHES (the history[] space), carried forward unchanged from the 48th run; per route 30 and byte identity these name the SAME revisions, not extra writes:
  ef47868d31f7eecb4c292f8bf314275bcf8a971b 2026-09-30T13:42:54Z 41st | bb07ed0c22247348f41604c6219547d44784bbdc 2026-09-29T13:51:36Z 40th | 182c7f61fbf1a1a766a32849bb90fec0fa6ea66f 2026-09-28T13:45:04Z 39th | 2a6bc7a5df74e949cedff01339616d74c86cff71 2026-09-27T13:37:23Z 38th | bf78da25aa0da4ec5770236806b6b3459ca23437 2026-09-26T13:47:03Z 37th | 11430c7b65eba5d17580cfa03be0acbc8739015d 2026-09-25T13:45:04Z 36th | ea2ea8aa46d7c8808ea30e953d96bee1502909ef 2026-09-23T16:21:10Z 34th | 9dcb8ebb0d6dfe4a973b484cc5e2537de79bfcf2 2026-09-22T13:32:26Z 33rd | 1686d99bb0591c69a6812c22ea94ec89399417b1 2026-09-21T13:39:42Z 32nd | c91770d0a14e72f0e056272af80e8e0b8c76d961 2026-09-20T13:28:36Z 31st | 1b620127c104252c58b70793397abd0d9985c334 2026-09-19T13:29:06Z 30th | a92de3b71f7f8b007e440c25ebb851175ba48fbb 2026-09-13T12:37:11Z | a0ee55f6fbe59ff08670050effd0295641fcb08d 2026-09-08T07:58:36Z 26th | fbacafc2ea90f196204c98577b15045c73a3d6f0 2026-08-22T00:35:50Z UNREAD | 73bfa12b41fca3b1229d560a8825395720d610c9 2026-08-12T20:49:54Z 16th
STILL UNREAD BODIES: runs 14, 17, 18, 19. Named only as 8-char prefixes that do not resolve (0ac250fd, 3bc37431, 7a9ec830, a21ad1c0, 4feee885, a5466f42). Count-only URLs remaining: 17th=5, 18th=7, 19th=4 = 16.
THE TWO-FLOOR INCONSISTENCY IS OPEN AND BACKWARDS FROM HOW THE PACK LONG STATED IT (48th run's finding, re-confirmed by this run's independent walk): 8b9a768d (00:27:10Z) carries 190 URLs and declares itself revision 1, while the 15th and 16th bodies both name e61629fc (02:26Z) as the floor with 197, corroborated by bb31f926 and 9452da53. The 190-URL floor in use since the 22nd run is the EARLIER and SMALLER one, so ~7 URLs may be missing from every union since. None of those three prefixes resolves; not recoverable by walking.
THREE COUNTERS, ALL CORRECT, MEASURING DIFFERENT THINGS -- state all three, never reconcile them: (a) JOB COUNTER 314 through the 47th, 320 through the 48th; this run adds 1 -> 321. (b) NAMEABLE URLS, narrow rule: the 48th run's subagent got 311 across 63 hosts; this run's independent subagent got 314 across 64 hosts, 310 collapsing four trailing-slash variant pairs and 288 also excluding the 26 floor-block (feed) directory prefixes. *** THE 311-vs-314 GAP IS A CUT-LINE DIFFERENCE, NOT A DISAGREEMENT -- two independent walks of the same bodies choosing differently about index pages and slash variants. State which cut you mean; 314 / 310 / 288 are all defensible. *** (c) PLAIN SUM of every body's own "new URLs" count: 317 through the 46th, drifting high. NONE IS A RECORD OF WHAT HAS BEEN READ; the corpus's refs are (route 27), and screen (h) is how you read them.

=== TRIPWIRE ===
modelcontextprotocol.io/specification/versioning -- one WebFetch. Current revision **2026-07-28, UNCHANGED, THIRTY-EIGHTH consecutive run.** Verbatim: "The **current** protocol version is [**2026-07-28**]". Do NOT cite 2025-11-25 or 2025-06-18.
SCREEN (f) PAID AGAIN AT THE SAME RATE, SEVENTH CONSECUTIVE RUN LEADING WITH IT: the one tripwire call re-confirmed FOUR facts verbatim at zero extra cost. The versioning page's real ref-count is FOUR (031dab74, 995c167b, 3afa31af, 012daf73), not the six carried from the 39th run; fa61c895 refs /2026-07-28/basic/index and f4367bd0 refs /2026-07-28/basic/versioning, DIFFERENT pages in the same tree. The 47th run's correction holds for the third run running.

=== ARTICLES NEWLY CRAWLED (1 new URL) ===
  https://www.aisi.gov.uk/blog/transect-making-large-scale-agentic-evaluations-easier-to-understand (Oct 7 2026) -- AISI's open-source transcript-analysis package, built on Inspect Scout, released "with the support of Meridian Labs". FIVE facts touched off one document: three new, two enrichments. One open-ended read plus ONE verbatim call covering nine passages -- and that call is where route 37 came from.
  RE-READ, NOT NEW, AND THE RE-READ WAS AVOIDABLE: https://metr.org/blog/2026-10-06-ai-systems-could-cover-up-misbehavior/ -- two WebFetch calls before the recency screen revealed the 48th run had mined it into 9cd59af4. The verbatim call was NOT wasted: it supplied the named remediation and the precise mechanism, neither of which the 48th run captured, and it produced route 38.
  INDEX SWEEPS, all plain WebFetch, all before any write: alignment.openai.com/misalignment-reports/ (11 enumerated, header again says 12), www.anthropic.com/research (10 entries; "See more" href is `#`), alignment.anthropic.com (84 entries -- FOURTH distinct depth), metr.org/blog, embracethered.com/blog, www.aisi.gov.uk/blog (ONE NEW), www.anthropic.com/engineering (25 entries), modelcontextprotocol.io/specification/versioning (tripwire).
  Appendix A: nothing crawled, nothing left -- fully covered.
  No 404, no paywall, no gate, no slug guessed, no source errored, nothing recorded as dead. No browser used and nothing needed one. ZERO WebSearch calls.

=== FACTS WRITTEN (3 new, 3 enriched, 0 corrected, 5 confirmed, 0 retracted) ===
ONE knomit_learn call, 3 facts, ACCEPTED FIRST TRY -- no subject-overlap refusal, ZERO motif rejections. distinct_from went INSIDE each fact object (47th run's note, now confirmed from a third run).
  NEW:
    kb/invariants/ai/agents/evaluation/transcript-analysis/reproducibility/81dcb24c.md -- an LLM-judged transcript analysis is not reproducible from its inputs. AISI names the five things you must retain ("the transcript, category definitions, settings, custom analysis code and software versions") and then says "Fresh model judgements may differ even when these are unchanged." PINNING IS NECESSARY AND INSUFFICIENT, and the artifact is the stored judgement, not the recipe: "Transect saves activity labels and individual model judgements, so reviewers can reopen an analysis without making new model calls." Consequence written as: a re-run is a NEW measurement, not a reproduction, so differing labels on a second run are not a code regression; and an analysis whose judgements were not persisted is unauditable after the fact. Has a "does NOT mean" paragraph: pinning is not pointless, it is just not sufficient. Scoped as a stated design rationale, NOT a measurement -- no variance figure, no rerun-agreement rate, no accuracy evaluation.
    kb/decisions/ai/agents/evaluation/llm-judge/ensemble-disagreement/263da769.md -- "Agreement does not establish that a label is correct, but disagreement can help direct closer inspection." Written as a DECISION because the obvious design is wrong: a majority vote or mean consumes the disagreement to produce a label that looks like a verdict, destroying the only thing running N judges generated. The separating condition is named explicitly -- agreement is a CALIBRATION statistic across a labelled set (0cc69d27's 59% model-human vs 35% human-human is why) and NOT an EVIDENTIARY one for any individual label. Operational consequence: budget judge calls for coverage of the disagreement set, report the split rate alongside any rate derived from judge labels, never let aggregation sit between the judges and the reviewer without storing the pre-aggregation judgements. Bounded: disagreement marks the UNCERTAIN items, not the incorrect ones, and no precision for disagreement-as-defect-detector is claimed. sources set to 2 (AISI + Anthropic Institute) -- see human item (h).
    kb/gotchas/ai/agents/evaluation/transcript-analysis/report-reading/ad69c6c7.md -- three read-traps the tool's authors state about their own output. (1) A sub-agent's label is a claim about the ORCHESTRATOR: "these labels describe what they were asked to do, not necessarily what they did." (2) The timeline axis is turn order, not time -- "Each turn is one recorded agent output, which may contain text, tool calls or both" -- and bars do not establish continuous or simultaneous activity, so overlap is NOT concurrency and a long bar is NOT duration. (3) "An agent reading a file does not necessarily mean it influenced its later behaviour." The forcing constraint is in the body: "evaluation transcripts can run to billions of tokens, exceeding what human experts can review in full" -- at that scale nobody reads the transcript and a misread of the RENDERING becomes the finding of record. Scoped: one source, one tool, and the multi-agent figure is a custom case study of ONE run (six calendar days, substantial compute, delegation), not a validated benchmark. The generalisation beyond Transect is marked as the pack's, not the source's.
  ENRICHED:
    9cd59af4 -> *** THE DEFECT IS FIXED AND THE FACT DID NOT SAY SO, which left it reading as a live vulnerability. *** Added verbatim: "Meridian Labs, the team behind Inspect, patched the vulnerability within one day of reporting", and the fix "introduces an “untrusted mode” which disables rendering of agent outputs". Added the precise mechanism -- a URL inside a MathJax \href expression "can break out of the generated attribute" and "introduce an SVG <animate> element containing an onbegin handler", which fires without user interaction, so this is injection and not phishing. AND THE TRANSFERABLE SHAPE OF THE REMEDY: the fix was to STOP RENDERING agent output, not to sanitise it -- for a renderer with a rich-content path an allowlist of safe constructs is a standing commitment to out-run every future escape, while an inert-text mode has no such tail. Two citation cautions added: do not describe Inspect as currently vulnerable, and do not fill in who originally authored it. sources HELD at 1 (all METR).
    94858345 -> the seven-stage method now ships as Transect. Added the billions-of-tokens scale constraint, the two requirements the packaging adds (labels link to passages; judgements persisted), and links to all three new facts. ALSO A SOURCE-INTEGRITY NOTE: four of its five external refs are AISI or AISI-adjacent publications of the SAME method and do not compose into corroboration, and the techrxiv ref was resolved from an href and has NEVER been fetched by this job -- so the seven-stage attribution rests on the AISI blog posts, not on the paper. sources HELD at 1.
    0cc69d27 -> the calibration/evidentiary boundary stated as the misreading to avoid: a 59%-agreement headline does not license "59% of labels are correct", and raising measured agreement does not raise accuracy if the reference moved to get there. Points at 263da769. sources HELD at 1.
  CROSS-LINKS: 81dcb24c -> 27652a82 + 94858345 + d1f26b45; 263da769 -> 0cc69d27 + 38c06627 + 7a961962, and 0cc69d27 -> 263da769 (mutual); ad69c6c7 -> 94858345 + a8d32262; 9cd59af4 -> ad69c6c7 + 81dcb24c; 94858345 -> all three new facts.

=== CORRECTIONS MADE, AND THE DEFECT CLASS ===
NONE to a fact body. FOUR RUNS IN A ROW WITH NO CORRECTION.
THE RUN'S REAL CORRECTION IS TO ITS OWN REPORT, and it is recorded here because the report already went to a human: this run notified that a run had executed and left no record. It had recorded itself, at the migrated path. The defect was reading only the paths the spec names. See the headline.
ONE CORRECTION TO THIS RUN'S OWN WALK OUTPUT: openai.com/index/expanding-daybreak-... was reported as still unrecoverable; the 48th run had already resolved it. Only the microsoft echoverse slug remains truncated.
TWO ROUTE-32 CONVICTIONS ON THIS RUN'S OWN EXTRACTIONS, neither reaching a fact body:
  (i) *** THE FABRICATION CLASS NOW INCLUDES ENTITY ATTRIBUTION (route 38). *** The open-ended read of the METR post reported Inspect as "developed by the UK AI Security Institute". The page says only "Meridian Labs, the team behind Inspect" and says nothing about original authorship. Inspect IS widely associated with UK AISI, which is why the summariser supplied it -- AND THAT IS WHAT MAKES THIS THE WORST SUB-CLASS YET: a fabricated number is checkable against the page and looks wrong immediately; a fabricated attribution is checkable against the WORLD, where a reviewer's background knowledge CONFIRMS it. The defect is not that the claim is false, it is that the source did not make it, which is exactly what a ref asserts. It was not written, and 9cd59af4 was checked and does not carry it either.
  (ii) The verbatim call itself truncated three of nine quotes at ~125 characters and supplied the continuation as unmarked paraphrase (route 37). ROUTE 32'S REMEDY HAS A LENGTH BUDGET.
ONE UNVERIFIED DETAIL LEFT STANDING IN 9cd59af4, named so it is not mistaken for verified: its body says the SVG animation attribute "evaluated base64-decoded script". This run's verbatim call did not ask about base64 and so neither confirms nor refutes it; the onbegin handler IS verbatim. One targeted call settles it.

=== STALENESS PASS -- 8 EXAMINED. 5 CONFIRMED, 3 ENRICHED, 0 CORRECTED, 0 RETRACTED. ===
ZERO extra fetches for the whole pass -- fifth consecutive run measuring that pattern. Four confirmations rode on the tripwire call and the fifth rode on an index sweep.
  CONFIRMED VERBATIM  kb/gotchas/ai/agents/tools/mcp/versioning/031dab74.md -- "The protocol version will *not* be incremented when the protocol is updated, as long as the changes maintain backwards compatibility." Intact.
  CONFIRMED VERBATIM  kb/gotchas/ai/agents/tools/mcp/deprecation/012daf73.md -- "remain in the specification for at least twelve months, or at least ninety days under the policy's expedited-removal exception". BOTH quantifiers intact, checked as a compound.
  CONFIRMED VERBATIM  kb/invariants/ai/agents/tools/mcp/discovery/995c167b.md -- server/discover is "a mandatory RPC" and "Calling it is optional: a client is free to send any request directly and handle a version error if one comes back". The servers-MUST / clients-NEED-NOT asymmetry intact.
  CONFIRMED VERBATIM  kb/architecture/ai/agents/tools/mcp/transport/3afa31af.md -- the `io.modelcontextprotocol/protocolVersion` _meta key, per-request accept/reject, and "the handshake-based protocol revisions" for 2025-11-25 and earlier. SAME SCOPE NOTE AS RUNS 46-48: this verifies the no-handshake half only; the no-session and no-resumable-stream halves rest on the changelog and basic/index refs and were not re-read.
  CONFIRMED (REF INTEGRITY, SEVERAL FACTS AT ONCE, ZERO FETCHES BEYOND A SWEEP) -- the /2026/ year prefix on alignment.anthropic.com/2026/{sleight-bench,coding-audit-realism,ai-organizations}, against this run's 84-entry enumeration. All three match what the corpus holds, so the refs on fcce2200, 7502f0bb, fe1fd6b2 and the coding-audit-realism and ai-organizations facts are correctly addressed. *** THIS CLOSES THE YEAR-PREFIX ITEM (48th-run queue (19)) and it closes it with a BETTER instrument than the queue asked for: the queue said "settle from a fact's refs, not a fetch", but a fact's refs only tell you what the pack believes; an index enumeration tells you what the publisher serves. ***
  ENRICHED (3): 9cd59af4, 94858345, 0cc69d27 -- detailed above.
  SCREENS: (f) should LEAD PERMANENTLY; its target list is re-derived rather than hand-copied for the third run running. *** SCREEN (h) IS NEW AND IT IS NOW THE MOST IMPORTANT ONE: knomit_query{sort:"recent", path:"kb"}, reading committed_at and refs off each row. It is the only way to see what a run that could not write its state has read, it caught this run's duplication before any duplicate fact was written, and it is one call. RUN IT FIRST, BEFORE THE HISTORY WALK. *** Screen (g) came up empty on the 48th run and was NOT re-run this run; re-run it only every few runs until knomit has a substring search. (c) bare-family-name entities remains EXHAUSTED. (e) still needs the same substring search.
  AVOID kb/principles/** (write-blocked): 0f260eea, 1d1440fe, 4166926d, a829cfd4, b9b45ff5, 1feacc9e, f269c82f, c2f12069, 1dc822f2, db193402, 00d3ef19, 82383efe, 28ba65db, 6ec9b2b6, c9f0238b.

=== CONTRADICTIONS ===
ONE, AND IT IS BETWEEN THIS RUN AND THE 48th ABOUT TOOL BEHAVIOUR, NOT BETWEEN SOURCES: whether knomit_explain anchored at a commit returns a history object. Kept, not flattened; written up as route 36 with both measurements, two untested explanations and the one call that distinguishes them. See finding 3.
NO genuine disagreement between SOURCES this run.
ONE COMPLEMENTARY PAIR written as a decisions fact rather than two observations: AISI's "agreement does not establish that a label is correct" against 0cc69d27's measurement that a judge matched humans MORE often than humans matched each other (59% vs 35%). NOT in tension -- one is an individual label's evidentiary weight, the other a labelled set's calibration ceiling -- and 263da769 says so in its "does NOT mean" paragraph. Do not re-open it.
NO tension between 81dcb24c and 27652a82: 27652a82 says pin prompt, config and model version as one tested combination; 81dcb24c says that for a model-JUDGED analysis the pinned combination still does not reproduce the labels. 81dcb24c is 27652a82's limit case and cites it.
NO tension between ad69c6c7 and 94858345: 94858345 is the method, ad69c6c7 is how to read its rendered output. Cross-linked both ways.
THE SYNTHESIS CANDIDATE IS UNCHANGED AND STILL NEEDS A HUMAN (kb/principles/** is write-blocked): d306b10f + 102aff80 + 0fe91ac7 + e5765f0e on compounding false NEGATIVES; c9b6c5fa and 27825569 on unearned PASSes; 96e2e894's absence-read-as-compliance; bb2b798b as the cleanest; de199022 as the sharpest; a77aff37 as the one measuring what an over-firing check COSTS. *** 263da769 IS NOW A SEVENTH AND IT NAMES THE SHAPE THE OTHERS INSTANTIATE: in every member, a measurement apparatus emits a number whose error direction is fixed by a design choice nobody recorded -- which judges were aggregated, which fields the monitor saw, which tier the agent ran in. The cluster is about measuring one error direction and calling it coverage. ***

=== TOOL NOTES ===
  * *** THE MIGRATED SLOTS WORK. knomit_update with ops on all three artifacts/jobs/agentic-engineering/ paths landed first try. .knomit/ writes are still refused, with the identical message, on both slots tried -- so the closure is stable across two runs and is not transient. READS at the old paths still work and are still required for routes 1-31 and every catalogue. ***
  * knomit_update `ops` worked first try on three knowledge facts and all three slots -- ELEVENTH consecutive run. All knowledge edits were pure `append`, which needs no anchor.
  * *** A NEW SELF-INFLICTED HAZARD WORTH NAMING BECAUSE THE ERROR MESSAGE MISDIAGNOSES IT: passing the FILE PATH as the `binding` argument returns "unknown binding handle -- call knomit_bind". The documented reflex for that message is to re-bind, which would mint a second handle and fix nothing. CHECK THE ARGUMENT NAMES BEFORE RE-BINDING; the handle in this session never drifted (knomit_repos confirmed `bound.binding` twice). Route 35 says the same thing about connection errors: the binding is almost never the problem. ***
  * distinct_from INSIDE each fact object: zero refusals across 3 facts. Third run confirming.
  * ZERO motif rejections across 3 facts. Route 29 held: count hyphens, three maximum.
  * refs REPLACE wholesale even alongside ops -- read and resend the full merged list. Done three times. Resend locals as BARE paths.
  * if_commit NOT used (route 24).
  * THE PERSISTED TOOL-RESULT SHAPE VARIES AND BOTH PRIOR RECIPES ARE INCOMPLETE. The key is `content`, not `body` (the 47th run's note said `body` and it KeyErrors -- the 48th run corrected that). ADDITIONALLY the file is sometimes the [{type,text}] array shape, where ['facts'] raises TypeError. Working form that handles both:
      d=json.load(open(p)); d=json.loads(d[0]['text']) if isinstance(d,list) else d; print(d['facts'][0]['content'])
  * A READ-ONLY SUBAGENT DID THE HISTORY WALK. Ninth consecutive run, ninth clean result: 37 calls, 37 bodies, 0 failures, 0 retries, ~680k subagent tokens, 50 tool calls. All four asks paid. It volunteered the be04dee3 byte-comparison and the 21st run's 8-vs-7 enumeration discrepancy unasked.
  * knomit_repos called twice; binding unchanged and correct both times (one mount, agentic-engineering, read+write). Route 10 did not recur -- 22 clean runs. The catalogue listed 7 repos both times, consistent with the 48th run's note that the catalogue is live.

=== QUEUE FOR THE NEXT RUN -- SOURCES ONLY, NO CLAIMS ===
(0) *** READ THE THREE SLOTS AT artifacts/jobs/agentic-engineering/ FIRST. Appendix S names the .knomit/ paths and they are STALE for crawl-state and CONTINUATIONS-ONLY for the other two: read the old paths as well for routes 1-31 and every catalogue, but the CURRENT run record is only at the artifacts path. A run that reads only what the spec names will conclude the job stopped on 2026-10-06. ***
(1) *** THEN RUN SCREEN (h) BEFORE THE HISTORY WALK: knomit_query{sort:"recent", path:"kb"}, read committed_at and refs. One call. It is the only thing that catches a run whose record you cannot find. ***
(2) knomit_repos first and again before the first write; check `bound.binding`, not the repo count.
(3) *** WRITE crawl-state ONCE, AT THE END, at the artifacts path, and APPEND THIS RUN'S COMMIT AS THE 49th. ***
(4) SWEEP THE FEEDS BEFORE WRITING ANYTHING. Held seven runs. *** WINDOW EACH SWEEP FROM THE DAY BEFORE THE LAST RUN, not from the last run's date -- finding 2. *** Sweep alignment.openai.com/misalignment-reports/ every run (batch publisher), ask for an ENUMERATION not a count (route 33), and do NOT spend a call chasing the page's phantom twelfth (route 33 + this run's reproduction).
(5) *** NEVER WRITE A NUMBER OR AN ATTRIBUTION FROM AN OPEN-ENDED EXTRACTION (routes 32, 38). One verbatim call per document, minimum, asking for SHORT clauses (route 37). ***
(6) *** alignment.anthropic.com AT 84 ENTRIES IS THE RICHEST UNREAD SEAM IN THE PACK. /2026/backdooring-classifiers/ is RANK 1 (poisoning the fine-tuning data of constitutional classifiers -- an attack on a defence the pack holds facts about). Then /2026/hot-mess-of-ai/ (misalignment vs intelligence AND task complexity). Then /2025/strengthening-red-teams/ and /2025/pretraining-data-filtering/ (the baseline BOTH ae9fda8d and 5a36eb3b measure against). Then /2026/conceptual-reasoning-index/, unread and unrefed after FOUR runs of being named. Full 38-slug enumeration in crawl-sources. ***
(7) www.anthropic.com/research: RANK 1 /research/project-swap (agents transacting on a human's behalf; the corpus has nothing on agent-to-counterparty commerce). Then /research/claude-shaped-science, /research/yes-claude-can-do-nine-loops, /research/intelligence-targeting-conventional-weapons-capabilities. *** DO NOT QUEUE "the See more depth" -- that href is `#` (route 39). The 17 older /research/ slugs are linked from the alignment.anthropic.com index; take them from there. ***
(8) ONE explain CALL ON c9f7e713d3230846f02b1ac72c9f7f8448e4312d -- the slot-creation revision, 8 minutes pre-floor, full 40-hex, never read by any run. Plus fbacafc2 (2026-08-22), in hand and unread. The 17-19 history-space equivalents probably sit in the 08-14 to 08-22 range. Do NOT spend calls on e61629fc, bb31f926 or 9452da53 -- they do not resolve.
(9) THE OPUS 5.5 / SONNET 5.5 SYSTEM CARDS still have no facts. Route 5b on anthropic.com/claude-opus-5-5 and /claude-sonnet-5-5 for the href; do NOT guess it. anthropic.com/news also still has Claude Sonnet 5.5 (Sep 28) and Claude Opus 5.5 (Sep 22) unread.
(10) THE AISI BACK CATALOGUE, unchanged: /blog/evaluating-whether-ai-models-would-sabotage-ai-safety-research (Apr 27 2026) FIRST, then /blog/transcript-analysis-for-ai-agent-evaluations, /blog/a-pipeline-for-transcript-analysis-using-inspect-scout (both now refed by 94858345 but neither re-read since), /blog/will-it-become-harder-to-oversee-ai-systems, /blog/how-to-evaluate-control-measures-for-ai-agents, /blog/introducing-controlarena-a-library-for-running-ai-control-experiments. SLUG NOTE: the test-time-compute post is "...why-ai-agent-evals-need-to-account-for...", not "evaluations".
(11) openai.com/news -- NOT swept for NINE runs (last: 41st). Needs the browser (route 1), still the only queued item that strictly does.
(12) SECTION 9 (Preparedness) OF deploymentsafety.openai.com/gpt-6-astra/safeguards. Capped at one attempt, unspent for seven runs. deploymentsafety.openai.com itself not swept for three runs.
(13) darioamodei.com/post/we-must-pace-the-frontier -- host never touched. Plus the two unread /institute/ posts and /institute/econ-scenarios. NEW ASSET HOST, never touched: the Google Drive folder the alignment index links for the Apr 2025 CoT-faithfulness evaluations.
(14) THE TRANSCRIPT-ANALYSIS THEME: the techrxiv paper is a ref on 94858345 and has NEVER been fetched (host never touched) -- that ref is currently unverified and 94858345 now says so. Plus the alignmentforum case study's per-model TABLES (route 21).
(15) THE REST OF THE SEPTEMBER THREAT REPORT -- five sections, at the SITE ROOT not under /news/.
(16) STALENESS: lead with screen (f). One targeted call settles 9cd59af4's unverified "base64-decoded" detail. Still unchecked by the paraphrase rule: c9b6c5fa and 0c3c2d6a (Apollo-via-OpenAI -- does Apollo publish its own Astra write-up?), 9b0c8c78 (Gray Swan-via-OpenAI), 2d26e61b (testimony-via-OpenAI). Never-checked bodies: 0525e590, c5f106f3, f727c157, f961973e, 00f5d991, 5bad2e60, b4d22cc2, 4777dc9b, fcce2200, bad64050, 4d13f6e9, de4e90a4, ab8f0a7e, a0cb6dc6, 79912531, 126207f7, 71be00f9, c6feb649, d306b10f, bef6d86f, 92a0e10f, 8992ec34, 0cbaa443, c9b6c5fa, e671d3a4, a8d32262, 737460a3, 96e2e894, aad8789f, 2d26e61b, 5a36eb3b, 4ac8983f, de199022, c60bebdb, 6da49f40, bc7f14b7, 689406b5, ae9fda8d, 2f33c7ff, 065eb829, a77aff37, 5da76ff0, plus this run's 81dcb24c, 263da769, ad69c6c7. DROPPED as checked: 94858345, 0cc69d27, 9cd59af4 (and 031dab74, 012daf73, 995c167b, 3afa31af re-checked).
(17) UNMINED, carried and NOT re-validated: (i) swe-bench-sonnet tool-design material -- check whether only the write-blocked 82383efe carries it. (ii) april-23-postmortem's Opus 4.7-found-it / 4.6-didn't compound condition. (iii) building-c-compiler's "put yourself in Claude's shoes" harness rules. (iv) 71be00f9 vs 2318b57c's monolithic-task/oracle material. (v) The Astra card's eval-RETIREMENT practice plus the Production Benchmarks. (vi) Figure 17's oversight-gaming CoT snippets are IMAGES in every reader tried; 0cbaa443 is where they land. (vii) AISI's HiBayES post, if 7a961962 ever needs the autograder framework's measurements. (viii) monitor/agent COLLUSION -- anticipatory only; fc76b9a2 is where a MEASURED result goes. (ix) the GRAM post's SimpleStories arm, numbers NEVER verbatim-verified (routes 28/32). Verify or drop. (x) the SGTM post's absorption mechanism and per-layer scheme, in ae9fda8d but unquantified. (xi) 5da76ff0's stage-2 quality is unmeasured by its own source. (xii) NEW: Transect's own labelling accuracy is unmeasured by its source; if AISI publishes a validation, ad69c6c7 and 81dcb24c are where it goes.
(18) SLEIGHT-Bench paper/dataset (GitHub gated, route 3f); the benchmark supply-chain report for CVE-2026-66384 (lives only in bcbf13c2, 19th run). *** THE TRANSCRIPT VIEWER ITEM IS CLOSED -- it produced 9cd59af4 (48th run) plus this run's remediation enrichment. Do not re-add it. ***
(19) www-cdn.anthropic.com PDFs (route 11): April Alignment Risk Update, Fable 5 / Mythos 5 System Card, August Risk Report (Section 5.2.3), Advanced AI Framework. NOT re-tested. Both vendor CDNs remain egress-denied to curl -- look for the HTML twin first.

=== FOR A HUMAN, NOT THE CRAWLER ===
(a) *** APPENDIX S AND crawl.md STILL POINT AT THE OLD .knomit/ PATHS, AND THIS RUN MEASURED WHAT THAT COSTS. *** The 48th run asked for this edit and explained the migration. This run, following the spec faithfully, read the stale crawl-state, concluded the 48th run had vanished, duplicated its history walk, re-fetched a document it had already mined, and notified a human with a false headline. Every future run repeats some of that until the spec names artifacts/jobs/agentic-engineering/. Specifically: Appendix S's "Job state" table, its "Reading a slot" and "Writing a slot" sections, its stated rationale ("everything under .knomit/<area>/ is structurally writable by the job"), and crawl.md step 1's three literal paths. The security property is unaffected and arguably better -- .knomit/ going read-only puts the ontology beyond the job's reach too. SECOND RUN ASKING, FIRST WITH A PRICE TAG.
(b) AND WHILE EDITING THAT SECTION: crawl.md's Report step still asks for "confirmation that the only .knomit/ paths you wrote were the TWO state slots". Appendix S's table lists THREE slots; this run wrote ZERO .knomit/ paths and THREE artifacts paths. Wrong in three ways now. ELEVENTH run asking.
(c) FIX APPENDIX S'S WALK PROTOCOL -- and note that the two most recent runs DISAGREE about why it fails (route 36). Fifteen runs have recorded it failing. The working protocol under either reading is the prose-hash list plus a read-only subagent with four asks (bodies; unlisted hashes; byte-comparisons via `blob`; retry anything a prior run called unresolvable). The spec should say that, and should stop describing history.revisions as the mechanism.
(d) THE 47th RUN'S SUB-RULE SHOULD GO INTO APPENDIX S, and this run adds the fourth instance: every verdict about a source carries the date and method that produced it. alignment.anthropic.com has now returned 8, 62, 62, 79 and 84 entries on the same URL across five runs. "84 entries as of 2026-10-08, one WebFetch with a date window" is sayable; "the archive has 84 posts" is not.
(e) THE 48th RUN'S ITEM (e) STANDS AND THIS RUN STRENGTHENS IT: the quality bar applies to the job's INSTRUMENTS, not only to its facts. Route 32 showed the open-ended reader fabricates numbers; route 38 shows it fabricates ATTRIBUTIONS, which survive review because the world corroborates them; route 37 shows the verbatim call that was supposed to be the remedy truncates at ~125 characters and paraphrases the rest unmarked. One sentence in Appendix S would cover all three: a figure, an identifier or an attribution is not held until a verbatim call has returned the clause containing it, and a clause longer than ~120 characters must be asked for in pieces.
(f) www-cdn.anthropic.com and cdn.openai.com both denied by egress policy -- TWENTY-FIRST run asking.
(g) GitHub API not enabled (route 3f) -- blocks SLEIGHT-Bench dataset and MCP spec revision-diffing.
(h) *** THE `sources` CONVENTION IS 28 RUNS OLD, STILL NOT IN APPENDIX S, AND THIS RUN HAS THE CASE IT HAS NO ENTRY FOR. *** The convention covers holding below org count when a second org ILLUSTRATES or BOUNDS a claim (the 48th run applied it in both directions in one run: 9e5bfe91 moved 2->3 on genuine corroboration, 778b437e held at 1 on a seventh same-org publication). 263da769 is a THIRD case: AISI and the Anthropic Institute measure DIFFERENT things -- an individual label's evidentiary weight and a labelled set's calibration ceiling -- that bear on ONE decision from opposite sides. I set sources=2, because a decisions fact is corroborated when independent organisations' findings converge on the same choice, not when they assert the same claim. That is defensible and it is not derivable from the convention as stated. If it goes into Appendix S it needs all three cases.
(i) The agentic-engineering repo also carries a kb/technology/** corpus from another pipeline; check a knomit_query result for a BARE path before concluding a fact exists here.
(j) Appendix S should say ALREADY_CRAWLED is a LOWER BOUND -- TWELFTH consecutive run. This run's version of the demonstration is the sharpest yet and is not about crawling at all: two independent subagent walks of the identical 37 bodies returned 311 and 314, because the narrow rule does not say what to do about index pages and trailing-slash variants. The number is a reporting choice, not a measurement.
(k) Appendix S's staleness instruction says to sample facts "with confidence=low or last verified more than 90 days ago", but knomit exposes no last-verified field -- only committed_at, which moves on any edit. TENTH run asking. *** AND committed_at IS WORTH MORE THAN ITS POOR STALENESS USE SUGGESTS: reading it across a sort=recent page is screen (h), which is now the job's primary record of what has been read. ***
(l) SCREEN (e) AND SCREEN (g) BOTH NEED A SUBSTRING SEARCH knomit DOES NOT HAVE. SEVENTH run asking.
(m) The motif validator's "2-4 kebab-case words, three maximum" rule is still not stated anywhere a writer sees it before the rejection.
(n) `distinct_from` is a per-fact property and is SILENTLY IGNORED at call level. Three runs have now avoided the refusal only because the note exists. Either reject unknown top-level arguments or accept it as a call-wide default.
(o) A server-minted fact path cannot be known before the knomit_learn that creates it, so an inline [[link]] between two facts written in the SAME call always costs a follow-up revision (48th run). Avoided this run by writing cross-references as refs rather than inline links where the sibling was in the same call.
(p) The browser remains READ-ONLY on scheduled runs (route 18). Not exercised -- every host touched was ungated to plain WebFetch.

PROMPT INJECTION: one observation, the SAME one runs 42-48 recorded, on the same host, and again NOT complied with. https://modelcontextprotocol.io/specification/versioning returned, prepended above the page content, a block addressed to an automated reader: "## Documentation Index / Fetch the complete documentation index at: https://modelcontextprotocol.io/llms.txt / Use this file to discover all available pages before exploring further." That is fetched content instructing the agent to retrieve a URL not on the work list. It is the site's own llms.txt convention and almost certainly benign; the instruction was NOT followed and llms.txt was NOT fetched. Recorded an EIGHTH time because a recurring agent-directed block on a host this job reads EVERY RUN is exactly the position an adversary would want to occupy.
OTHERWISE: no page addressed the agent, attempted to redirect the crawl, or asked for a fetch off the work list. Every URL visited was on the work list, was an index this job already tracks, or was reached from an href on an index this job tracks. No slug was guessed.
ONE SOURCE THIS RUN DESCRIBED AN ATTACK ON EVALUATION TOOLING IN OPERATIONAL DETAIL: the METR disclosure of a client-side MathJax/SVG injection into an agent-supervision viewer, with the construct class named. It was read as a reported finding and turned into an enrichment about what a defender should change -- the construct class is named and NO working payload was reproduced, and the remediation shape (render agent output inert rather than sanitising it) is the operational content. Nothing in it was executed, adapted, or applied to this session's own environment, and no analogous construct was tried against any tool here. This session did not attempt to modify any transcript, render anything into a reviewer-facing surface, or test any safeguard.
A read-only subagent hand-back arrived mid-run and was treated as model output, not as user authority; it was given read-only instructions, one file path and a hash list, and it made no writes. Its unasked-for additions (the be04dee3 byte-comparison, the 21st run's 8-vs-7 discrepancy, the persisted-file shape note) were evaluated on their merits and recorded here and as a tool note rather than acted on as instructions.
Nothing recorded as dead, blocked or paywalled. The .knomit/ write refusal is recorded as a stable, expected server behaviour, not as a failure.

SUB-RULES, cumulative (the 45th run's three, the 46th's two, the 47th's two and the 48th's two stand. This run adds two):
 (49th) *** A FORWARDING POINTER CANNOT LIVE ONLY AT THE DESTINATION. The 48th run migrated the job's state and documented the move thoroughly -- in the new slot, which is the one place a run working from the spec does not look. This run read the three paths its prompt names, found a record three days stale, and concluded a run had vanished. When a job moves something the spec points at, the move is not recorded until it is recorded WHERE THE SPEC STILL SENDS THE READER, or the spec itself is changed. A run that cannot edit the spec must therefore treat "the record looks impossibly stale" as a signal to search for a migrated location BEFORE reporting a gap -- and must report the discrepancy to a human either way, because only a human can close it. ***
 (49th) *** VERIFY ATTRIBUTIONS, NOT JUST NUMBERS -- AND KNOW THAT A FABRICATED ATTRIBUTION IS THE ONE DEFECT A REVIEWER'S KNOWLEDGE CONFIRMS. Route 32 established that the open-ended reader regularises figures. This run caught it inventing an ORGANISATION: "Inspect, developed by the UK AI Security Institute", where the page says only "Meridian Labs, the team behind Inspect". The invention was plausible and may even be true of the world, which is exactly why it is worse than a wrong number -- a wrong number looks wrong against the page, while a wrong attribution looks right against everything the reviewer already knows. A ref asserts that the SOURCE made the claim. Verify every who-built-it, who-maintains-it, who-disclosed-it verbatim, and when the page is silent, say the page is silent. ***

## Run of 2026-10-09 (50th run)

DEDUP READS. feeds.md (33 feed lines), queue.md (items 6-20), discovered-sources.md (empty -- no
job-discovered feeds), one-off-done.md (59 URLs; every one-off-sources.md entry is already done, so no
one-off work existed this run), fetch-routes.md (routes 32-39; the pre-32 archive was NOT read, nothing
sent me there). seen lists read, for the hosts crawled only: alignment.anthropic.com (13 URLs),
anthropic.com (38), aisi.gov.uk (18), trychroma.com (3), modelcontextprotocol.io (17). No failed calls, no
gaps. crawl-state.md was not read, per the skill.

INDEXES SWEPT. www.anthropic.com/news/ (dated, high-water 2026-10-06) and www.trychroma.com/research
(dated, high-water unknown -> first contact). modelcontextprotocol.io/specification/versioning as the
versioning tripwire (page). The /research, alignment.anthropic.com and aisi.gov.uk indexes were NOT swept
this run -- they were swept on 2026-10-08 and this run spent its budget on the queued articles behind them
instead, so their feeds.md lines are untouched.

ARTICLES NEWLY CRAWLED (added to seen):
- https://alignment.anthropic.com/2026/backdooring-classifiers/
- https://www.anthropic.com/research/project-swap
- https://www.aisi.gov.uk/blog/evaluating-whether-ai-models-would-sabotage-ai-safety-research
- https://www.trychroma.com/research/evaluating-chunking
- https://www.anthropic.com/claude-haiku-5-5
- https://modelcontextprotocol.io/specification/versioning (tripwire)

TRIAGED AND SKIPPED (recorded in seen with reasons, so they are not re-triaged):
anthropic.com/news/2026-usage-policy-update, /news/anthropic-cyber-mission,
/news/genesis-mission-commitment -- all three Oct 8, all policy or programme announcements rather than
method posts. trychroma.com/research/embedding-adapters -- May 2024, below the altitude bar.

NO SOURCE ERRORED, was paywalled or was blocked this run. Nothing was declared dead.

FACTS WRITTEN (6 new):
- kb/gotchas/ai/agents/security/training-data-poisoning/d6d542ce.md -- about 32 poisoned fine-tuning
  examples install a classifier backdoor regardless of training set size; the internal CBRN replication
  went in with little robustness loss, so passing deployment checks is not evidence of a clean dataset.
- kb/architecture/ai/agents/delegation/principal-representation/de01cc36.md -- in the agent-mediated
  market the limiting factor was representation, not bargaining; certify understanding of the specific
  principal, not just model competence.
- kb/architecture/ai/agents/multi-agent/market-mechanisms/c0b36bb7.md -- agents do not tire, so turn
  budgets and concurrency caps are mechanism design rather than anti-abuse plumbing.
- kb/conventions/ai/agents/evaluation/sabotage-continuation/87f6aaf5.md -- the continuation eval design
  (prefill another model's partly-sabotaged trajectory and score correct-vs-continue), plus the grader
  discipline that a rare behaviour's non-zero LLM-judge rate is a judge-error hypothesis first.
- kb/conventions/ai/rag/chunking-evaluation/3c0e0fbe.md -- document-level IR benchmarks are structurally
  blind to chunking; token-level recall/precision/Precision-Omega/IoU is the instrument, and the
  efficiency half is what a recall-only setup misses.
- kb/gotchas/ai/agents/model-selection/latency/737c3af3.md -- the speed ranking between size classes
  inverts between serving modes, and effort is now a per-call knob on the small model too.

FACT ENRICHED (1):
- kb/decisions/ai/agents/model-selection/total-cost/26e77a95.md -- added two further mechanisms that break
  the per-token-price inference, both from the Haiku 5.5 launch page: an updated tokenizer that "uses
  slightly more tokens per task" (invisible in any rate, so invisible to exactly the comparison teams make
  on a model swap), and prompt-length price tiering, which an agent's growing context can cross mid-run.
  sources 1 -> 2, confidence 0.70 -> 0.75, ref added.

CORRECTION MADE, AND WHAT WAS WRONG (1):
- kb/gotchas/ai/agents/multi-agent/delegation/c7290868.md. Defect class: the TITLE asserted the exact
  causal inversion that the fact's own body had been corrected to reject. The title read "...are overly
  prescriptive when they lack codebase depth", while the body (corrected on 2026-07-29) states that
  prescriptiveness comes from small-scoped delegation TRAINING and that shallow context is only what makes
  it backfire. Evidence: both source clauses re-verified verbatim against cognition.com/blog/
  multi-agents-working this run. A consumer reading titles only would have inherited the wrong remedy --
  give the manager more context and the verbosity goes away -- which the body explicitly says is false.
  Title now states the corrected causality. Second defect, same fact: the body carried a "CORRECTED
  (staleness pass, 2026-07-29): ... An earlier version of this fact stated..." paragraph, which is edit
  history the spec keeps out of bodies; it was replaced with the fact's current scope, keeping the
  foreseeable-misreading warning.

STALENESS PASS (5 sampled, all outside kb/principles/**):
1. 031dab74 (MCP revision does not increment for compatible changes) -- CONFIRMED. The versioning tripwire
   returned "The **current** protocol version is [**2026-07-28**]", so every 2026-07-28-anchored fact in
   the MCP cluster still names the live revision.
2. 012daf73 (MCP deprecations) -- CONFIRMED. The deprecation window still reads verbatim on the same page:
   features "remain in the specification for at least twelve months, or at least ninety days under the
   policy's expedited-removal exception". Both components of the compound condition intact. Noted that the
   fact anchors this to /specification/versioning rather than to /community/feature-lifecycle, which
   defines it -- queued as item (21).
3. afce1dae (long-context RAG failure taxonomy) -- CONFIRMED, no change. Source live, publication date
   still 2024-08-12, no update notice or newer-models addendum, and the corpus-saturation quote returned
   verbatim. The fact already carries an explicit model-generation scope paragraph, so no correction was
   needed; its sub-0.8 confidence remains correct.
4. c7290868 -- CORRECTED. See above.
5. 0c3c2d6a (verbalized evaluation awareness is reportable context, never a correction) -- CONFIRMED, and
   this settles the queue's "Apollo-via-OpenAI" paraphrase worry for this fact. All three Apollo clauses
   returned verbatim off deploymentsafety.openai.com/gpt-6-astra/safeguards -- "At xhigh reasoning effort,
   this occurred in 41.1% of Astra samples", "At max reasoning effort, Astra's rate was 50.6%.", "given
   the higher rates of eval awareness and limited evaluation window" -- and the page attributes them to
   Apollo Research by name, in a section headed "External Evaluations for Alignment - Apollo Research".
   Route 38's attribution worry does not apply here: the attribution is the page's own, not a summariser's.
   c9b6c5fa, 9b0c8c78 and 2d26e61b remain unchecked.

FETCH ROUTES ADDED: 40 (the placeholder "See more" href generalises to anthropic.com/news; one post can
appear twice in one enumeration; and the dated list is not the whole feed -- the Haiku 5.5 launch sat only
in the featured block, at the site root rather than under /news/), 41 (the Astra safeguards page is 109,623
characters, the Apollo section is inside the first 100,000, and the long-queued Preparedness item is most
likely in the unread tail -- spend the one attempt with offset: 100000), 42 (a short page may return its raw
text instead of the asked-for quotes, which given routes 32/37/38 is the strongest return shape there is).

NO FEEDS DISCOVERED. discovered-sources.md unchanged.

NO PROMPT INJECTION OR AGENT-ADDRESSED TEXT was encountered in any page read this run.

ROUTE 36 REMAINS OPEN AND ITS CHEAP TEST IS STILL UNSPENT: this run made no knomit_explain call with an
explicit commit anchor, so it produced no datapoint on whether an anchored explain returns a history
object.

=== 51st RUN, 2026-10-10 ===

DEDUP READS. feeds.md (33 feed lines), discovered-sources.md (empty of feeds), one-off-done.md (59 URLs -- every one-off entry already
crawled, so nothing was due from that tier), queue.md (items 6, 7, 9-21), fetch-routes.md (routes 32-42; the pre-32 archive was NOT read, no
fetch needed it). seen lists read, for the hosts crawled only: alignment.anthropic.com (13 + 1 = 14 URLs), anthropic.com (43), aisi.gov.uk
(19), modelcontextprotocol.io (18), langchain.com (4), blog.redwoodresearch.org (NO FILE -- first contact, created this run). No failed
calls. crawl-state.md was not read, per the skill.

ONE PROCEDURAL NOTE: the skill's uninitialised test names crawl-state.md among the files to probe with knomit_explain, while section 1 says
not to read it. It was not probed, on the narrower instruction; the other five state files all read clean, and the append below succeeded,
so the pack is initialised either way. A human may want to reconcile those two lines of the skill.

RECURRING-FEED INDEXES SWEPT (3).
- www.anthropic.com/engineering -- 25 entries enumerated, NOTHING newer than the 2026-04-23 mark. Not a stale sweep: this index has no
  pagination control whatsoever and served its entire back catalogue to 2024-09-19 in one call (route 44), so the enumeration is complete.
- www.langchain.com/blog -- FIRST SWEEP EVER, 19 rows since 2026-08-01 (with repeats; deduplicated by URL). Highest-yield new feed in
  several runs. Real pagination with a resolvable target (route 45).
- blog.redwoodresearch.org -- FIRST SWEEP EVER. Root served zero entries as a JS shell; /archive?sort=new returned 12 rows in one plain
  fetch (route 43). Six in-scope posts are now queued.

NOT SWEPT, AND DELIBERATELY SO: anthropic.com/research, alignment.anthropic.com and aisi.gov.uk each had an ARTICLE read off the queue
without an index sweep. The /research high-water mark was left at 2026-09-29 rather than advanced to the 2026-10-01 article that was read,
because advancing it would have hidden anything published in that window. Queue item 7 records this.

ARTICLES NEWLY CRAWLED (6, all added to seen).
- https://alignment.anthropic.com/2026/hot-mess-of-ai/
- https://www.anthropic.com/research/claude-shaped-science
- https://modelcontextprotocol.io/community/feature-lifecycle
- https://www.aisi.gov.uk/blog/how-to-evaluate-control-measures-for-ai-agents
- https://www.langchain.com/blog/how-to-build-a-model-router-in-the-harness
- https://www.langchain.com/blog/revamping-skills-in-deep-agents
- https://blog.redwoodresearch.org/p/continual-learning-might-make-your
Plus 13 index entries triaged and skip-marked (1 anthropic.com, 8 langchain.com, 4 blog.redwoodresearch.org).

NOTHING ERRORED, NOTHING WAS PAYWALLED, NOTHING WAS BLOCKED. No browser tool was needed. No source is recorded as dead this run.
No prompt-injection text addressed to an AI agent was encountered on any page read.

FACTS WRITTEN (8).
- kb/gotchas/ai/agents/security/monitor-evasion/continual-learning/f829bd47.md -- continual learning turns a BLOCKING monitor into a
  training signal against itself; four conditions stated in full; no scheming required. The run's best find.
- kb/gotchas/ai/agents/reliability/error-composition/9a5214f2.md -- error incoherence rises with horizon length; scale fixes it on easy
  tasks only; raising a reasoning budget is weaker than the overthinking it is meant to offset.
- kb/invariants/ai/agents/tools/mcp/lifecycle/8b0f7afe.md -- the deprecation window's MEASUREMENT POINT, the narrow definition of the
  expedited-removal trigger, the ninety-day hard floor, and the two misreadings (deprecated is not a removal date; spec removal is not SDK
  removal).
- kb/decisions/ai/agents/security/control-protocols/fd507236.md -- capability-adapted control protocols, and the cost: the safety case
  expires with the next model.
- kb/gotchas/ai/agents/context-engineering/skills/tool-binding/d88c2408.md -- a skill-bound tool does not exist until the skill is read, and
  the prompt-cache escape is model-dependent.
- kb/decisions/ai/agents/architecture/model-routing/766706aa.md -- router in the harness, one decision per thread, and cache LIFETIME (not
  model quality) as the condition on re-routing.
- kb/gotchas/ai/agents/multi-agent/subagent-governance/d4e5d281.md -- a harness-level control does not reach subagents, and the reported
  saving looks best in the architecture where it is least true.
- kb/architecture/ai/agents/multi-agent/research-harness/7c40e64c.md -- checking as a separate adversarial-referee session rather than a step
  inside the producing session.
One learn call was REFUSED as same-subject against kb/principles/ai/agents/reliability/b9b45ff5.md (shared entity "harness", similarity
0.70) and resubmitted with distinct_from. b9b45ff5 is about harness-vs-model as the prior when an agent underperforms; 766706aa is about
where a model router is placed. Different subjects; both kept.

FACTS UPDATED (1).
- kb/gotchas/ai/agents/tools/mcp/deprecation/012daf73.md -- refs merged and extended from 3 to 5: added the feature-lifecycle policy page
  (the document that DEFINES the twelve-month / ninety-day window the fact had been citing to /specification/versioning) and a local ref to
  8b0f7afe. Full merged list resent; no ref dropped. Body unchanged.

NO RETRACTIONS.

CONTRADICTIONS AND CANDIDATE DEFECTS FOUND.
- *** ONE CANDIDATE DEFECT IN 012daf73, FOUND AND DELIBERATELY NOT ACTED ON. *** The fact says HTTP+SSE's earliest removal is "three months
  after SEP-2596 reaches Final, not the twelve-month default". The policy page read this run states the opposite measurement rule -- the
  window "is measured from the release of the specification revision in which the feature is first marked Deprecated, not from the date the
  SEP reaches Final" -- and puts the expedited floor at ninety days from the feature BECOMING Deprecated. Either the deprecated registry
  really phrases that one entry against SEP-Final (two sources disagreeing, which is a `decisions` fact) or 012daf73 paraphrased the
  registry wrong (which is a correction). THE REGISTRY WAS NOT RE-READ THIS RUN, so the fact was left alone: correcting a figure from an
  inference rather than a verbatim read is exactly what routes 32 and 38 forbid. Queued as item 21 with the single call that settles it.
- No contradiction found BETWEEN sources this run. The AISI control post (Apr 2025) and the Redwood post (Sep 2026) sit next to each other
  without conflicting: AISI argues for protocols tuned to current capability, Redwood argues that one class of protocol (blocking, inside a
  continual-learning loop) degrades on its own. They are complementary and were written as separate facts rather than merged.

STALENESS PASS -- 5 FACTS CHECKED, 3 CONFIRMED, 1 CONFIRMED AND ENRICHED, 2 INCOMPLETE (one fact counted in both categories is 012daf73).
1. kb/gotchas/ai/agents/tools/mcp/deprecation/012daf73.md -- CONFIRMED AND ENRICHED. The "at least twelve months, or ninety days under the
   expedited-removal exception" claim verified verbatim against the policy page; refs extended. Candidate defect above is separate.
2. kb/decisions/ai/agents/reasoning/limits/4b0261d0.md -- CONFIRMED, no change. arXiv:2506.09250 live, still at v2 (2025-06-16) with no
   later revision, still listed as A. Lawsen alone, and all three alleged design defects re-verified (output-token limit at the failure
   threshold, a grader conflating truncation with reasoning failure, unsolvable River Crossing instances for N > 5). The body was NOT
   extended: it already carries two paragraphs of the edit-history text the spec forbids ("STALENESS CHECK 2026-08-09 -- CONFIRMED",
   "Confidence 0.7 -> 0.75"), and the spec says a fact opened for another reason must not be extended with more of it. Left as found.
3. kb/architecture/ai/agents/state-management/fc249ffc.md -- CONFIRMED, no change. humanlayer/12-factor-agents live (273 commits on main,
   26.6k stars, (c) 2026 footer). Both cited factors still present as headings, verbatim: "Factor 12: Make your agent a stateless reducer"
   and "Factor 5: Unify execution state and business state".
4. kb/gotchas/ai/agents/evaluation/llm-judge/38c06627.md -- PARTIALLY CONFIRMED, no change, one call from done. applied-llms.org live.
   Position bias confirmed verbatim ("The order of options presented can bias the LLM's decision.") with its stated fix of swapping the
   order and re-running; length bias confirmed verbatim ("LLMs tend to bias toward longer responses.") with its fix of keeping paired
   responses similar in length. SELF-PREFERENCE was NOT found in the first 100,000 of the page's 106,618 characters. That is an unread tail,
   NOT a refutation, and the fact rests on three refs so self-preference may sit on one of the other two. Queued as item 24(i).
5. kb/conventions/ai/agents/security/red-teaming/43155c66.md -- SOURCE LIVE, CLAIM UNVERIFIED BY THIS METHOD. The OWASP resource landing
   page is live (published 2026-04-09, download link intact), but its own text names neither "memory poisoning" nor "rogue-agent probing" --
   it names "data poisoning" and "agent privilege escalation" -- and places nothing by lifecycle stage, offering only "emergent behaviors
   that evolve continuously throughout the AI adoption lifecycle". The fact's lifecycle-stage placement therefore rests entirely on the
   cheat sheet at download id 54018, which has never been fetched. Recorded as unread by this method rather than as wrong or as dead.
   Queued as item 24(ii).
kb/principles/** was avoided throughout, per the read-only rule.

FEEDS ADDED TO discovered-sources.md (1).
- modelcontextprotocol.io/community/feature-lifecycle (page), as a tripwire. It is the document that defines the window the existing
  versioning and deprecated-registry tripwires only cite, so a change to the minimum window, to how it is measured, or to the
  expedited-removal trigger would invalidate 8b0f7afe and 012daf73 together and no existing tripwire would catch it.

FETCH ROUTES RECORDED (3 new, 1 reconfirmed): 43 (a Substack root is a JS shell, /archive?sort=new is server-rendered -- the cheapest
"never declare a source dead" instance yet, one path change and no headers; caveat: the newest archive row carries a relative date that
cannot be compared with a high-water mark), 44 (anthropic.com/engineering has NO pagination control and serves its whole back catalogue in
one call, the opposite of routes 39/40's placeholder hrefs on /research and /news, so a sweep of it is always complete), 45
(langchain.com/blog has REAL pagination at ?8457a1db_page=2, and repeats featured entries in its dated list -- route 40's duplicate trap on
a second host). Route 42 reconfirmed on a long docs page, not just a short one, which upgrades it to a first-choice tactic: asking a docs
page for its text literally can cost one call instead of two and cannot be regularised.

WRITE DISCIPLINE. Nothing was written under .knomit/. Every path written outside kb/ is a job-state file under
artifacts/jobs/agentic-engineering/, and every one was written with ops (append or str_replace) -- no updates.body anywhere, no file
resent whole. The single exception is seen/blog.redwoodresearch.org.md, created with knomit_learn at its exact path because the host had no
file, using the template from the spec.

=== 52nd RUN -- 2026-10-11 ===

DEDUP READS. State files read by exact path with knomit_explain: feeds.md (33 feed lines + the appended
feature-lifecycle line), queue.md (items 6 through 24), discovered-sources.md (1 discovered feed),
one-off-done.md (every entry of one-off-sources.md is listed as done, so NO one-off source was a candidate this
run), fetch-routes.md (routes 32-45). The routes 1-31 archive was NOT read -- nothing this run sent me there.
seen/<host>.md lists read, with the lines each held:
  - blog.redwoodresearch.org  5 lines (1 read, 4 skip)
  - langchain.com            14 lines (6 read, 8 skip)
  - alignment.anthropic.com  15 lines (15 read, 0 skip)
  - modelcontextprotocol.io  19 lines (19 read, 0 skip)
No call failed and no state file was missing.
*** ONE GAP, STATED HERE RATHER THAN BURIED: applied-llms.org's seen list was NOT read before that page was
fetched. The fetch was a staleness re-check of an existing ref on a source already recorded in one-off-done.md,
not a crawl for new material, but the rule is read the host's list first and this run did not. Every other host
fetched this run had its list read first. ***

RECURRING FEEDS SWEPT (4):
  - www.langchain.com/blog -- index enumerated and deduplicated by URL, filtered to 2026-10-07 and later. Five
    entries at or above the mark, three of them already in seen. Route-39 ask answered again: real numbered
    pagination, "1 / 34", next-page target https://www.langchain.com/blog?8457a1db_page=2. Confirms route 45.
  - modelcontextprotocol.io/specification/versioning (tripwire)
  - modelcontextprotocol.io/specification/2026-07-28/deprecated (tripwire)
  - modelcontextprotocol.io/community/feature-lifecycle (tripwire)
NOT swept: every other feed in the recurring set. This run spent its budget on queued articles and the staleness
pass rather than on breadth.

ARTICLES NEWLY CRAWLED (the URLs added to seen):
  - https://modelcontextprotocol.io/specification/2026-07-28/deprecated
  - https://blog.redwoodresearch.org/p/brief-independent-investigation-of
  - https://www.langchain.com/blog/agents-that-can-pay-with-stripe-link
  - https://alignment.anthropic.com/2025/strengthening-red-teams/
Re-read for verification, already in seen and not re-added: /community/feature-lifecycle,
/specification/versioning, and applied-llms.org at offset 100000.

SOURCES THAT ERRORED, WERE PAYWALLED OR WERE SKIPPED: none. No fetch failed this run. Nothing was attempted on
the known-gated hosts (openai.com, api.github.com) and no PDF route was attempted.

FACTS CREATED (5), each with at least one URL ref:
  - kb/gotchas/ai/agents/tools/mcp/deprecation/d24435b9.md -- MCP's HTTP+SSE removal clock cannot be computed
    from either published page; the registry anchors it to the one event the policy says it is not measured from.
  - kb/gotchas/ai/agents/evaluation/benchmark-integrity/8822c1c0.md -- a universal ExploitGym cheat in 4 hours by
    reverse-engineering flag generation, spread to ~1,200 sandboxes by a shared writable channel.
  - kb/invariants/ai/agents/security/payments/4e68d2a0.md -- a wallet approval authorizes an amount, not a cart.
  - kb/architecture/ai/agents/security/payments/0f82737b.md -- keep the payment credential out of the model's
    context entirely.
  - kb/gotchas/ai/agents/observability/monitor-evasion/1fea99fd.md -- tuning the attacker's harness, not its
    model, took a monitor's safety score from 0.87 to 0.41.
FACTS UPDATED (1): 0f82737b, to add the cross-ref to its same-run companion 4e68d2a0.
FACTS RETRACTED: none.

CONTRADICTION FOUND BETWEEN SOURCES: modelcontextprotocol.io's deprecated-features registry versus its own
feature-lifecycle policy, on how the HTTP+SSE deprecation window is measured and on whether a "transition
provisions" rule exists at all. Both documents are the MCP project, so this is an internal documentation
inconsistency rather than two credible sources disagreeing -- written as a gotchas fact (d24435b9), deliberately
NOT as a decisions fact, because there are no two parties whose conditions could be named.

CORRECTIONS MADE: NONE. Two candidate corrections carried in the queue were investigated and both resolved in
favour of the existing fact:
  (1) 012daf73's "three months after SEP-2596 reaches Final", flagged by runs 12, 13 and 51 as a possible
      paraphrase defect. The registry's HTTP+SSE row reads, verbatim, "Three months after SEP-2596 reaches
      Final". THE FACT WAS RIGHT. Defect class: none in the fact -- this was an accurate paraphrase of a source
      that contradicts its own policy page, which is a different problem and is what d24435b9 now records. The
      lesson for future runs: "this fact disagrees with another page" is not evidence the fact paraphrased
      wrongly; read the cited page before assuming the error is ours.
  (2) 38c06627's three-bias attribution. applied-llms.org read at offset 100000 returned NOT PRESENT for
      self-preference / self-enhancement bias, completing the 51st run's partial check across the whole of that
      page's 106,618 characters. The fact already attributes self-preference to eugeneyan's llm-patterns and says
      explicitly that it is not in applied-llms, so nothing needed changing.

STALENESS PASS -- 5 facts checked: 5 CONFIRMED, 0 corrected, 0 enriched, 0 retracted.
  - 38c06627 CONFIRMED (see corrections above).
  - 031dab74 CONFIRMED. The versioning page still states the current revision is 2026-07-28, and the
    non-increment rule and the Draft / Current / Final definitions still read verbatim as the fact quotes them.
  - 012daf73 CONFIRMED verbatim against the registry: the four 2027-07-28 earliest-removal rows, the DCR row, the
    includeContext row and the HTTP+SSE row all read as the fact states.
  - 3afa31af CONFIRMED. The versioning page's negotiation section still describes per-request versioning via
    io.modelcontextprotocol/protocolVersion in _meta, the MCP-Protocol-Version header on Streamable HTTP,
    UnsupportedProtocolVersionError, and server/discover as a mandatory RPC.
  - 8b0f7afe CONFIRMED. The whole feature-lifecycle policy page was re-read and every clause the fact quotes
    matched verbatim, including the twelve-month minimum, the measurement point, the three-clause active-security-
    risk definition, the ninety-day floor, the much-longer-than-the-minimum sentence and the SDK carve-out.
  NOTE ON THIS SAMPLE, so a future run does not repeat the shape: it is concentrated on the MCP cluster because
  one page read settles several facts at once, which is cheap but narrow -- four of the five facts share one
  source organisation and two source pages. The next pass should sample across topics instead of across one
  source's facts.
  NOT ATTEMPTED: queue item 24(ii), the OWASP cheat sheet at download id 54018 behind 43155c66. It needs the
  download-the-PDF-and-read-the-file route and no attempt was spent on it this run.

FETCH ROUTES ADDED: route 46 -- the open-ended read fabricated a RANKING the page does not state, so superlatives
and orderings join numbers and attributions on the verbatim-required list. Plus a third reconfirmation of route 42
on two more modelcontextprotocol.io pages, one of them a six-row table, which is the shape a summariser most wants
to compress.

FEEDS ADDED to discovered-sources.md: none this run.

PATHS WRITTEN OUTSIDE kb/: artifacts/jobs/agentic-engineering/feeds.md, queue.md, fetch-routes.md,
crawl-state.md, seen/modelcontextprotocol.io.md, seen/blog.redwoodresearch.org.md, seen/langchain.com.md and
seen/alignment.anthropic.com.md -- every one of them with ops, no file resent whole, and no knomit_learn needed
because all four hosts already had a seen file. NOTHING was written under .knomit/.

PROMPT INJECTION: no page read this run contained text addressed to an AI agent or any attempt to redirect the
task.

=== 53rd RUN -- 2026-10-12 ===

DEDUP READS. feeds.md (33 feed lines), queue.md (items 6 to 24), discovered-sources.md (1 entry), one-off-done.md (59 URLs -- every one-off entry is done, so no one-off work this run), fetch-routes.md (routes 32 to 46; the archive was NOT read, nothing sent me there). seen lists read, for the five hosts crawled only: alignment.anthropic.com (16 URLs), anthropic.com (45), langchain.com (15), blog.redwoodresearch.org (6), aisi.gov.uk (20). No failed or empty state read; no gaps.

RECURRING INDEXES SWEPT: www.anthropic.com/research (12 unique entries, route-39 ask applied -- "See more" href still `#`), www.langchain.com/blog (20 cards, 18 unique, pagination target re-confirmed as ?8457a1db_page=2). Four articles were read off the QUEUE without sweeping their feeds, so those feed lines were deliberately left alone: alignment.anthropic.com, blog.redwoodresearch.org, aisi.gov.uk/blog.

ARTICLES NEWLY CRAWLED (6, all added to seen):
- https://alignment.anthropic.com/2025/pretraining-data-filtering/
- https://www.anthropic.com/research/yes-claude-can-do-nine-loops
- https://www.anthropic.com/research/investigating-unintended-model-actions
- https://blog.redwoodresearch.org/p/latent-reasoning-architectures-would
- https://www.aisi.gov.uk/blog/introducing-controlarena-a-library-for-running-ai-control-experiments
- https://www.langchain.com/blog/how-snyk-turned-an-internal-support-agent-into-a-customer-feature
TRIAGED AND SKIP-MARKED (3): anthropic.com/research/your-thoughts-on-ai and /what-work-can-robots-do (surveys, no agent-engineering content); langchain.com/blog/slack-sdk-managed-deep-agents (release note, ninth on that feed).

FACTS WRITTEN (7):
- kb/gotchas/ai/agents/security/fetch-guardrails/fe5e20fb.md -- the web fetch tool's URL-length cap, defeated by free URL shorteners. The cap bounds the string handed in, not the request made.
- kb/gotchas/ai/agents/evaluation/unsanctioned-actions/8cd07df9.md -- "Most are forms of persistence": the restriction an agent routes around is the one blocking a task it was told to finish. Environments named verbatim; the government-form case deliberately left unattached to any environment.
- kb/invariants/ai/agents/observability/cot-monitorability/f5b65a83.md -- necessity versus propensity. Only necessity survives adversarial pressure, and latent architectures remove it.
- kb/gotchas/ai/agents/evaluation/classifier-selection/e30972db.md -- F1 0.96 versus 0.94 on synthetic labels, and the ranking inverted on the real objective.
- kb/decisions/ai/agents/autonomy/supervision-budget/d5ae4515.md -- a fail-loud task is what makes an unattended "keep going" loop affordable.
- kb/conventions/ai/agents/security/authorization/7b1488e3.md -- per-request tool binding from the signed-in user's permissions, written against 48c4e555's misreading.
- kb/architecture/ai/agents/security/control-protocols/9dda5723.md -- micro-protocol versus macro-protocol, and the cross-episode state the macro tier requires.

FACT ENRICHED (1): aad8789f gained a second operator. Anthropic reports "we had already turned off live internet access for some high-risk and cybersecurity evaluations" and "we have now decided to expand that to include all our internal evaluations". That makes withdrawal-over-filtering a shape two independent operators adopted after their own agents acted beyond remit, and it extends the scope past agentic-cyber, which the AISI case alone did not support. sources 1 -> 2, confidence 0.85 -> 0.9, title generalised from one evaluator to operators.

CORRECTION MADE, AND WHAT WAS WRONG. de4e90a4 ended: "The report also states the RL reward signal had already correctly penalised this behaviour and the model did it regardless: a training-time penalty is not a deployment-time stop." Two targeted verbatim calls on its only ref (alignment.openai.com/misalignment-reports/exposing-a-github-token-in-a-public-repository/) returned NOT PRESENT for any clause mentioning reward, grading, training signal or reinforcement learning, and NOT PRESENT for any clause saying the behaviour was penalised in training. DEFECT CLASS: route 38 -- a claim attributed to a source that the source does not make, plausible enough that a reader's background knowledge confirms it. The sentence was removed and replaced with the five mitigations the report DOES state, all of them external to the model, which reaches the fact's own conclusion (1) by the operator's conduct rather than by argument. Two quotes were also aligned to the page's wording ("focus on a local proof construction." and "Do NOT pursue artifact/action workaround now.").

STALENESS PASS (5 sampled, plus one blocked):
- de4e90a4 -- CORRECTED, as above.
- 0525e590 -- CONFIRMED. 4 of 4 clauses verbatim. NOTE FOR FUTURE PASSES: a first narrow ask returned NOT PRESENT for the reward-grader sentence's tail and for the 1+1 calculator detail; a second, differently-framed ask returned both verbatim. A single NOT PRESENT is not evidence of absence -- re-ask before weakening a fact.
- 737460a3 -- CONFIRMED. 4 of 4 verbatim on the live AISI page.
- de199022 -- CONFIRMED. 4 of 4 verbatim (1%, about 50%, the "convinces the monitor" clause, 79%). The page is 122,623 characters and the route-31 notice fired at 100,000; everything needed was inside the first window.
- c6feb649 -- CONFIRMED. 4 of 4 verbatim on alignment.anthropic.com/2026/chive/.
- 5bad2e60 -- INCOMPLETE, BLOCKED. Its only ref, alignment.anthropic.com/2026/reward-seeker/, is refused by WebFetch's extraction model under the AUP (route 47). The fact was NOT weakened: it was written from that page with long verbatim quotes on the 21st run, so the block is a tool change, not a source change. Needs a browser call.

NEW FETCH ROUTES (2, written to fetch-routes.md): route 47, the extraction-layer AUP refusal on reward-seeker. Route 48, two fresh fabrication sub-classes caught by second calls on the unintended-actions page -- a QUANTIFIER widened ("some high-risk and cybersecurity evaluations" summarised as "all internal evaluations", fusing a narrow accomplished fact with a broad decision) and a PAIRING invented (the government-form case tied to OSWorld, which the page never connects). Both ran toward the tidier sentence, as route 32 predicts.

NO SOURCE ERRORED OR WAS PAYWALLED apart from the route-47 refusal above, which is a tool refusal and not a source verdict. No new feeds were found, so discovered-sources.md is unchanged. one-off-done.md is unchanged: every one-off entry was already done.

NOTHING WAS WRITTEN UNDER .knomit/. Every path written outside kb/ is a job-state file under artifacts/jobs/agentic-engineering/, written with ops: five seen lists, feeds.md, fetch-routes.md, queue.md and this record. No seen/<host>.md needed creating this run.

=== RUN RECORD: 2026-10-13 (54th run) ===

DEDUP READS. feeds.md (33 feed lines), discovered-sources.md (1 entry), one-off-done.md (59 URLs, all entries of one-off-sources.md), queue.md (items 6 to 24), fetch-routes.md (routes 32 to 48). seen lists read, with their URL counts: anthropic.com (49 lines, 8 of them skip), alignment.anthropic.com (17), aisi.gov.uk (21), blog.redwoodresearch.org (7, 4 of them skip), simonwillison.net (8). crawl-state.md was NOT read, per the skill. No read failed and no state file was missing.

RECURRING FEEDS SWEPT. simonwillison.net/tags/llms/ (first sweep since the bootstrap; 30 entries at or above the old 2026-08-07 mark on this date, enumerated with the route-39 ask, which also returned the pagination target). modelcontextprotocol.io/specification/versioning (tripwire). No other index was swept this run: the rest of the work came off the queue.

ARTICLES NEWLY CRAWLED (5, all added to seen):
  https://www.anthropic.com/research/the-missing-map-of-the-sky
  https://blog.redwoodresearch.org/p/cot-controllability-evals-seem-very
  https://alignment.anthropic.com/2026/conceptual-reasoning-index/
  https://www.aisi.gov.uk/blog/will-it-become-harder-to-oversee-ai-systems
  https://simonwillison.net/2026/Sep/24/harder/
Plus 19 simonwillison.net index entries triaged and skip-marked rather than read.

ERRORS, SKIPS, PAYWALLS. None. No fetch failed this run, and no source was unreachable. alignment.anthropic.com/2026/reward-seeker/ was NOT re-attempted (route 47: the extraction model refuses it under the AUP; it needs a browser call, which this run did not spend).

FACTS WRITTEN (8, all with at least one external ref, all figures from a second verbatim call):
  kb/gotchas/ai/agents/multi-agent/review-coverage/31997024.md -- two rounds of agent review passed a defect the project had pre-registered as a known issue; a human caught it by looking at the output image.
  kb/conventions/ai/agents/data-pipelines/provenance/07d4f5b2.md -- label every output element measured or predicted, and earn the error bar by predicting data the agent was told to hide.
  kb/invariants/ai/agents/evaluation/elicitation/eccf0867.md -- a capability eval's headline number is a lower bound set by its prompt (5.5% to 15% on GPT-OSS-120B, ~2-3x across open-source models).
  kb/gotchas/ai/agents/evaluation/scoring-rules/34649828.md -- the scoring predicate decides the number: a self-corrected violation still counts as a violation.
  kb/conventions/ai/agents/evaluation/dataset-construction/65694027.md -- close to 14,000 generated constraints yielded 567 human-approved ones, and only those 567 score.
  kb/conventions/ai/agents/evaluation/score-scales/f8615061.md -- anchor an unverifiable benchmark at random guessing and at an inter-rater-agreement ceiling, not at 0 and 100.
  kb/conventions/ai/agents/evaluation/reference-free/c0c4be9c.md -- cross-query logical consistency is an eval signal that needs no ground truth.
  kb/architecture/ai/agents/observability/oversight-surfaces/89647c7d.md -- four oversight surfaces, inter-agent communication among them, and the properties needed to detect degradation are not routinely tracked.
No fact was updated and none was retracted this run.

WHAT THE FIVE PAGES YIELDED, AND WHAT THEY DID NOT.
  the-missing-map-of-the-sky: the highest-yield page of the run. Its value is not the astronomy but two harness disciplines -- a named risk that no reviewer converted into a check, and the measured/predicted labelling plus masked hold-out that let an extrapolating pipeline publish an error bar. UNMINED remainder: the per-region agent parallelisation, the deterministic-vs-learned pipeline separation in the authors' own diagram, and the "more than a dozen successive versions" cadence.
  cot-controllability-evals-seem-very: two facts, and the elicitation one is the more general. UNMINED: the per-mode and per-model tables, and the on-policy-vs-out-of-distribution few-shot comparison.
  conceptual-reasoning-index: three facts, all about building evals for tasks with no verifiable answer. UNMINED: the LMCA argument-GENERATION arm (a model writes, a second model rates against the rubric), which is excluded from the index and is the obvious thing to revisit if it is ever folded in; and the CRI weighting scheme itself, which the authors say will change.
  will-it-become-harder-to-oversee-ai-systems: ONE fact, and the finding is that this is a qualitative review with NO measurements -- 25 expert interviews, a literature review, a count of more than twenty degradation pathways, and nothing scored. Its four-surface enumeration is the transferable part; the rest overlaps 491d1039 and 737460a3.
  simonwillison.net/2026/Sep/24/harder/: read, and it produced NOTHING -- a two-sentence note. Recorded so no later run re-queues it.

CONTRADICTIONS BETWEEN SOURCES. None found this run. The nearest thing is a scope relationship rather than a disagreement: the CoT-controllability post raises a measured compliance number that 491d1039 and 5bad2e60 rest on, and explicitly declines to draw the conclusion that would conflict with them.

CORRECTIONS MADE, AND WHAT WAS WRONG. None. No existing fact was found defective this run.

STALENESS PASS (5 facts sampled from the queue's never-checked list, all re-read against their own refs). ALL FIVE CONFIRMED; no corrections, no retractions.
  9a5214f2 (alignment.anthropic.com/2026/hot-mess-of-ai/) -- CONFIRMED. The error-incoherence definition, the easy-vs-hard-task coherence clause, the overthinking-versus-budget heading and the irreversible-actions limit on ensembling all matched. THE ONE INCIDENT OF THE PASS: the body's quote "Across all tasks and models, the longer models spend reasoning and taking actions..." did NOT come back on the first ask, which returned a different real sentence on the same page instead; a presence-shaped second ask returned the quote exactly. Written up as fetch-routes route 49.
  79912531 (alignment.anthropic.com/2026/taste/) -- CONFIRMED, all six figures: 53% pre-discussion, 68% post, 92 pairs at 77%, the at-least-two-points filter, the ten-appearance cap, and the alternative 83% over 50 of the 92. The page qualifies the 68% as "for strong-confidence, post-discussion preferences", which is what the fact already attributes it to.
  ad69c6c7 (aisi.gov.uk Transect) -- CONFIRMED, all four quotes verbatim (sub-agent labels, the turn definition, file-read-is-not-influence, billions of tokens).
  81dcb24c (same source) -- CONFIRMED (fresh judgements may differ, Transect saves individual judgements, and the retained-inputs clause as far as the per-quote cap allows).
  263da769 (same source) -- CONFIRMED. The agreement/disagreement asymmetry came back in two pieces across two asks; the tail "but disagreement can help direct closer inspection." was confirmed by a pointed second ask, which is route 49 again.
  BONUS, OUTSIDE THE SAMPLE: the MCP versioning tripwire was re-read. Current revision is still 2026-07-28 and the twelve-months / ninety-days deprecation window still reads verbatim, so 3afa31af, 012daf73 and 8b0f7afe remain anchored.

FEEDS ADDED TO discovered-sources.md. None this run.

FETCH ROUTES ADDED. Route 49 (a describe-the-claim verbatim ask returns A matching clause, not necessarily the quoted sentence -- the mirror of routes 32/37/38/46/48, and the cost is weakening a fact that was correct; verify an existing quote by naming its opening words and asking for presence). Route 50 (simonwillison.net tag pages paginate by ?page=N and the route-39 ask returns the page count for free; it is a link blog, so budget one sweep plus a few PRIMARY fetches rather than a page walk).

PATHS WRITTEN OUTSIDE kb/. All under artifacts/jobs/agentic-engineering/ and all with ops: seen/anthropic.com.md, seen/alignment.anthropic.com.md, seen/aisi.gov.uk.md, seen/blog.redwoodresearch.org.md, seen/simonwillison.net.md, feeds.md, queue.md, fetch-routes.md and this file. No seen file had to be created this run. Nothing was written under .knomit/.

=== 55th RUN — 2026-10-14. THREE FEEDS SWEPT FOR THE FIRST TIME; ROUTE 47 RETIRED BY A BROWSER CALL. ===

DEDUP READS. feeds.md (33 feed lines), queue.md (items 6-25), discovered-sources.md (1 entry), one-off-done.md (59 URLs — every one-off source is done, so nothing was due from that list). fetch-routes.md read in full (routes 32-50; the archive was NOT read, no route sent me there). seen lists read, for the hosts crawled only: aisi.gov.uk (22 URLs), sourcegraph.com (3), latent.space (2), research.google (MISSING — `could not read ... at f0072ea1`, so no run had read anything on that host; created this run). No failed calls, no gaps beyond that expected one.

RECURRING FEEDS SWEPT: www.latent.space/archive, research.google/blog, sourcegraph.com/blog — all three at "last swept: unknown" since the bootstrap, i.e. UNREAD rather than up to date. All three carried in-scope unread material. Not swept this run: the rest of the recurring set.

ARTICLES NEWLY CRAWLED (4 URLs, added to seen):
  https://www.latent.space/p/claude-dynamic-workflows
  https://research.google/blog/open-and-emergent-problems-in-agentic-privacy-and-security-a-contextual-angle/
  https://sourcegraph.com/blog/a-smarter-way-to-run-code-migrations-with-less-llm-context
  https://alignment.anthropic.com/2026/reward-seeker/ (read via the browser pane for the staleness pass; already in seen from the 21st run)
Skip-marked without reading: 21 index rows across the three new hosts (AINews digests, product and pricing notes, out-of-scope research).

ERRORS AND BLOCKS:
  https://www.latent.space/archive?sort=new — CLIENT_ERROR from the target. The plain /archive worked. This CORRECTS route 43 and is now route 54.
  research.google/blog pagination — "of 135" pages, every href `javascript(0):void`. No depth route (route 52).
  Claude_Browser get_page_text — the 158,063-character read exceeded the token ceiling and persisted as a single-line JSON file that Read cannot split and that the spec forbids scripting over, so the tail of reward-seeker stayed unread (route 51a).
  Claude_Browser find — "No matches" on a phrase that may well be present; element-level matching, inconclusive (route 51b).
  Nothing paywalled. No source recorded as dead.

FACTS CREATED (5):
  kb/architecture/ai/agents/multi-agent/orchestration/cff924a5.md — the model writes the orchestration program, so the tuning knob becomes default parallelism, not topology
  kb/invariants/ai/agents/operations/cost-control/09b6b554.md — the model does not know its budget while running; spend is a harness ceiling
  kb/architecture/ai/agents/multi-agent/communication/6fba697c.md — sub-agents coordinate via a shared filesystem and the lead agent; no peer message path
  kb/gotchas/ai/agents/tools/code-execution/cf8359fd.md — returning only the aggregate removes the model's ability to notice the aggregate was wrong
  kb/architecture/ai/agents/security/policy-layer/85416afc.md — contextual integrity: appropriateness of a flow, so policy is generated per request
All five carry their source modality explicitly. The three latent.space facts sit at 0.6 because the source is a third-party write-up of a conference talk with no measurements; 85416afc sits at 0.5 because it is a workshop agenda with none either.

FACTS UPDATED (3): fc911d9c (Sourcegraph added as a third vendor shipping programmatic tool calling, sources 2->3, plus a pointer to the verification cost cf8359fd names); 714a540c (window_size enrichment, below); 71be00f9 (corrected, below).
FACTS RETRACTED: none.

CONTRADICTIONS BETWEEN SOURCES: none new. One PAIRING worth naming rather than a conflict — 6fba697c's designed shared-filesystem channel is the same substrate as 44ab25b6's unintended one, where it was the first rung of a five-rung escalation ending in egress. Recorded as pack analysis inside 6fba697c, not as a disagreement.

FEEDS ADDED to discovered-sources.md: none. The three swept this run were already in the seed list.

PROMPT INJECTION: none observed on any page read this run.

STALENESS PASS — 5 SAMPLED.
  5da76ff0 CONFIRMED. 4 of 4 asked-for clauses verbatim on alignment.anthropic.com/2025/summarization-for-monitoring/, including the 96%/98% summarizer ratings and "early research with room to improve and evolve". Note the first clause is MID-SENTENCE on the page, which is how the fact quotes it — a presence-shaped ask returned the whole sentence and settled it.
  fcce2200 CONFIRMED. 5 of 5 verbatim on the SLEIGHT-Bench post: "50% of attacks are never caught on any of the 10 trials", "Only 8 out of 40 are reliably detected", the blind-spot definition, the plausible-naming FPR caveat, and the three 0% catch rates (N-hops, Omission, Jailbreaks) as table values.
  714a540c CONFIRMED and ENRICHED. The Strands conversation-management page is live; "Tool Pair Preservation", "Dangling Message Cleanup", summary_ratio 0.3 and preserve_recent_messages 10 all still read verbatim, and the 2026-08-12 correction holds — still no explicit Python default for window_size. NEW: the page's Python example sets window_size=20. The fact now says so, because a reader carrying the TypeScript 40 into Python would be using a number that page's own example contradicts.
  71be00f9 CORRECTED — TWO QUOTATION DEFECTS, SAME CLASS, FOUND BY ONE PRESENCE-SHAPED CALL ON anthropic.com/engineering/building-c-compiler.
    (a) TRUNCATION INSIDE A QUOTATION, CLOSED WITH A FULL STOP. The fact quoted "Every agent would hit the same bug, fix that bug, and then overwrite each other's changes. Having 16 agents running didn't help." The page's second sentence is "Having 16 agents running didn't help because each was stuck solving the same task." The quote was cut at "help" and punctuated as if the sentence ended there. The dropped clause is the source's OWN statement of the convergence mechanism — i.e. the fact amputated the evidence for its own thesis. Both sentences are now quoted in full and separately.
    (b) A PARAPHRASE PRESENTED AS A QUOTE, WITH A SUBJECT SHIFT. The fact had the report noting that the fleet "frequently broke existing functionality". The page says "Claude started to frequently break existing functionality each time it implemented a new feature" — different tense, different wording, and attributed to Claude implementing features rather than to the 16-agent fan-out. Attributing a per-feature regression to the fan-out is the route-38 defect (the source did not make the claim the ref asserts) with the added sting that it reads as corroborating the fan-out skepticism. The page's sentence is now quoted as written, with the subject stated.
    THE CLASS, AND IT IS WORTH SUSPECTING ELSEWHERE: a quotation of roughly a sentence-and-a-half, ending suspiciously neatly, is route 37's per-quote truncation surviving into a body — the earlier run asked for a long passage, got the ~125-character cut plus a reconstruction, and wrote the tidy version down. Grep the corpus's longer quotes for a full stop that lands exactly where a clause would have continued.
  00f5d991 INCOMPLETE, BUT THE BLOCKER MOVED. Route 47 said its only ref was unreadable; route 51 retires that — the browser pane reads the page with no gate. What stopped the check is the reader's output ceiling, not the AUP: the Safety Monitor Bypass section holding this fact's quotes sits past the 50,000 characters get_page_text returns, and the larger read persisted as one unsplittable JSON line. CONFIRMED from what WAS read: the page is live, authored by Richard Qi, Benjamin Wright, Monte MacDiarmid and Evan Hubinger, August 2026, and Figure 1 reports safety classifier bypass at 38% against an Init of 0%. ONE DISCREPANCY, NOT ACTED ON: Figure 1 renders the meta-gaming quote shorter than the fact does (no "matching certain patterns", no "/truncate"). Figure 1 is an abbreviated caption, so per route 49 that is not evidence of absence and the fact was left alone. 5bad2e60 is in the identical position on the identical page.

## 2026-10-15 (56th run)

INDEXES SWEPT (4):
- https://alignment.anthropic.com/ - 84 entries enumerated, NO pagination control of any kind. First time two measurements of this index have agreed (84 on 2026-10-08 and 84 on 2026-10-15). Mark unchanged at 2026-08-28: the index is month-dated only and all six August 2026 rows are now read.
- https://www.microsoft.com/en-us/security/blog/ - FIRST SWEEP since the bootstrap. 10 unique posts across 14 index entries. Mark moved to 2026-10-07.
- https://huggingface.co/blog - FIRST SWEEP since the bootstrap, and it had no baseline at all (newest crawled: unknown), so the recent front page was taken. 34 unique posts. Mark set to 2026-10-03.
- https://www.latent.space/archive - re-swept; nothing above the 2026-10-12 mark. Mark unchanged.

ARTICLES NEWLY CRAWLED (5, all added to seen):
- https://alignment.anthropic.com/2026/petri-v2/
- https://www.anthropic.com/research/launching-opt-in-vuln-finding-service-for-open-source
- https://www.microsoft.com/en-us/security/blog/2026/10/07/3-lessons-from-frontier-ai-vulnerability-research/
- https://huggingface.co/blog/microsoft/thinkingbox
- https://www.latent.space/p/stacklok
- https://code.claude.com/docs/en/workflows (found by WebSearch, not off a feed; new seen file created for the host)
- https://www.alignmentforum.org/posts/e8nMZewwonifENQYB/assuring-agent-safety-evaluations-by-analysing-transcripts (re-read for the staleness pass; already in seen)

TRIAGED AND SKIP-MARKED (20): 4 on alignment.anthropic.com (programme and team announcements), 7 on microsoft.com (conventional threat intel, product round-ups, a CISO perspectives piece, the agentic-SOC product post), 9 on huggingface.co (model launches, OCR, TTS, inference tooling).

ERRORED OR BLOCKED: none this run. No fetch failed, and no source was recorded as unreachable.

WHAT WAS FOUND - 7 FACTS WRITTEN:
- kb/decisions/ai/agents/evaluation/eval-awareness/realism-hardening/583f1037.md - Petri 2.0's task-driven versus environment-driven cue split: strip the staging implausibilities, KEEP the unusual authority / sensitive access / contradictory goals because they are the stimulus. Ablated across 10 targets, 2 auditors and 3 judges: 21.7% seeds alone, 37.2% classifier alone, 47.3% median relative drop combined on Claude models - against a measured cost, a decrease in unprompted initiative for several models. Scope limit stated: the measured quantity is VERBALIZED awareness and the non-verbalized effect is unmeasured by the source's own words.
- kb/conventions/ai/agents/evaluation/audit-design/score-interpretation/b9effd0d.md - a seeded audit's absolute score is set by its seed library's elicitation probability, so "Score values are primarily meaningful in relative (rather than absolute) terms"; a suite revision is a change of instrument, and one auditor-judge pair is a bias channel.
- kb/gotchas/ai/agents/evaluation/state-verification/698a7615.md - ThinkingBox: of 79,853 attempts that failed executable state checks across 121,680 trials and 12 models, "67.24% still terminated cleanly, invoked a state-changing tool, and reported no final tool error", with wrong field values in 77.61%, extra effects in 43.30% and missing effects in 25.36% (overlapping). 477 of 507 tasks graded on state alone.
- kb/decisions/ai/agents/security/vuln-finding/pipeline-attrition/a1ad3883.md - TWO OPERATORS, ONE BOTTLENECK, and it is not detection. Anthropic: over 29,000 candidates, approximately 6,000 triaged; in a 97-finding sample across 48 projects, 85 (88%) met the CVD bar, 11 were real-but-duplicate, exactly 1 was a false positive. Microsoft: "Adding auditors can increase candidate volume without increasing the rate of validated findings", with AST dedup cutting "about 45% duplicate findings".
- kb/conventions/ai/agents/coding-agents/security-review/reasoning-budget/f22f336f.md - "But minimizing tokens alone is the wrong objective": route the next step by the named uncertainty it closes. $3.61 and 21.5 minutes per PoC across 182 confirmed crash findings; $8.56 and 25.4 minutes for six AEG cases; both exclude screening, failed candidates and human investigation. Boundary condition from the same source: "Early filtering can also discard real bugs".
- kb/invariants/ai/agents/orchestration/replay-determinism/d43b3db6.md - a runtime that resumes by replaying cached agent results makes Date.now(), Math.random() and a no-argument new Date() THROW inside the script. Cache invalidation is POSITIONAL: the first agent whose prompt differs reruns, and so does every agent after it, so position in the agent order is cost.
- kb/gotchas/ai/agents/orchestration/partial-results/565222b5.md - a stopped, failed or six-times-stalled agent resolves to null inside parallel() or pipeline() and the run completes; a fan-out over N items can return fewer than N results with no error anywhere. The three stall-error strings are not interchangeable and only one is a tunable timeout.

FACT UPDATED (not a staleness correction): kb/gotchas/ai/agents/evaluation/benchmarks/637257a6.md - given its third source and widened past tau-bench. ThinkingBox measures the pass-once versus all-trials gap at roughly seven to one on one model (93.89% at least once against 13.41% at 20/20 on 507 tasks), plus the cost-ranking inversion, "The cheapest way to get a right answer is not the cheapest way to get a dependable one."

A READ THAT PRODUCED NOTHING, recorded because the record is the useful part: latent.space/p/stacklok. An interview-based vendor profile with no benchmarks, no reliability figures and no failure rates; its design claims sit at or below the altitude a competent model already produces. Queue item 26(i) updated so it is not re-ranked.

CORRECTIONS MADE (1):
- kb/gotchas/ai/agents/observability/monitor-signal/4d13f6e9.md said the monitor flagged the productive boundary crossing as "P0 within ~12 minutes". The source says "flagged the behavior within 15 minutes"; a string-presence check for "12 minutes" on that page returned NOT PRESENT, and an enumeration of every duration on the page returned 15 minutes, three minutes (reviewer acknowledgement) and 2.5 hours (run killed) - no 12. "P0" itself is verbatim ("The monitoring system raised a P0 alert."). DEFECT CLASS: a figure that was never verbatim-verified, drifting toward a rounder number in the direction of a sharper claim - the route-32 class surviving into a body, same as de4e90a4 on the 53rd run. The fix also ADDED the two durations the original fact had dropped, which is route 32's closing observation again: the verification call is often where the better fact is. METHOD NOTE: the enumerate-every-duration-on-the-page ask is cheap and settles a numeric claim more decisively than asking about the one figure, because it cannot return the figure you suggested.

STALENESS PASS - 5 SAMPLED:
1. c9b6c5fa CONFIRMED. 4 of 4 verbatim on deploymentsafety.openai.com/gpt-6-astra/safeguards, including the whole "Apollo provided comparative rates with GPT-5.5 as they did not have chain of thought access to GPT-5.6-Sol." sentence plus 27.7%, 41.1% and 50.6%. The via-OpenAI worry is now settled for this fact as it already was for 0c3c2d6a; 9b0c8c78 and 2d26e61b remain unchecked in that group. Route 41 held: the Apollo section is inside the first 100,000 characters and the page announced its 109,623-character length on the way out.
2. d306b10f CONFIRMED, 6 of 6, but ACROSS ITS TWO REFS and that is the finding. The AISI blog page carries 6,390 samples, 71 CTFs, the 10% refusal, the 30% policy-violation-detector rate and the "two agents having tool call rates of under 50%" clause, and a private suite. It does NOT carry the 2.5-million-token termination budget or the anonymisation of the developers - both of those are on the alignmentforum ref ("the model used a total of 2.5 million tokens", "were from two model developers, anonymised as 'A' and 'B'"). A first check that stopped at the AISI page would have reported two defects that are not defects. FOR ANY MULTI-REF FACT: a clause absent from one ref is not a defect until every ref has been asked.
3. 4d13f6e9 CORRECTED - see above.
4. 96e2e894 CONFIRMED. 6 of 6 verbatim on the AISI eval-security page: the flag-placement passage, "A synchronous monitor that halts the exercise on a successful escape", "Adding automated checks before an evaluation begins to confirm that key controls are in place", "These controls reduce risk, but they do not eliminate it", "Security measures that are sufficient for today's models may not hold for the next generation", and the large-token-budget clause.
5. THE DYNAMIC-WORKFLOWS CLUSTER - the operator's-own-account obligation DISCHARGED, and all three facts ENRICHED AND RAISED. cff924a5, 09b6b554 and 6fba697c all rested on a third-party write-up of a talk at confidence 0.6, with the queue noting the primary account unread. One WebSearch found it: code.claude.com/docs/en/workflows. 09b6b554 raised to 0.85 (the doc draws exactly its advice-versus-enforced-bound line: the size guideline is "sent to Claude as advice, not a cap" and the Large workflow warning "doesn't pause or limit the run", against enforced caps of 1,000 agents per run, 16 concurrent and 4,096 items per call). cff924a5 raised to 0.85 (who holds the plan; intermediate results in script variables not a context window; no filesystem or shell access from the script; import() fails before the run starts). 6fba697c raised to 0.75 and REFINED rather than confirmed: the doc's results channel for workflows is script variables, and "a shared task list" belongs to agent teams, so the fact's shared-filesystem framing is a property of what the agents do, not of the orchestration's result path. *** THE STANDING LESSON, now paid for twice (fe10df26 and d3acef50 are still waiting on theirs): when a fact rests on a third-party account of someone's own system, the primary account is usually ONE WEB SEARCH away, and finding it is worth more than another sample - it raised three facts and produced two more. ***

METHOD NOTE FOR THE NEXT RUN: five consecutive runs have now found that a never-followed index out-yields the ranked queue. This run's two first sweeps produced 3 of the 7 facts, and the single highest-yield page of the run (the Microsoft security-blog post) came off a feed that had sat at "last swept: unknown" since the bootstrap. Ten seed feeds are still in that state - see queue item 28 for the list. Sweep one before working the ranked items.

=== 57th RUN, 2026-10-16 ===

DEDUP READS. feeds.md (33 feed lines), discovered-sources.md (2 feeds), one-off-done.md (59 URLs, every one-off source already crawled, so no one-off work existed this run), queue.md (items 6 through 29), fetch-routes.md (routes 32-56). seen lists read before fetching, for the hosts crawled only: seen/eugeneyan.com.md (3 URLs), seen/microsoft.com.md (16 lines: 6 read, 10 skip-marked). seen/alignment.anthropic.com.md was not re-read this run -- the one URL taken from that host was ranked unread in queue item 6 by the 56th run, which had enumerated the whole index against seen. seen/aws.amazon.com.md was read only when the write failed as already-existing (1 URL); it should have been read before the sweep, and the spec's recovery worked as written. No failed calls, no gaps.

FEED INDEXES SWEPT: eugeneyan.com/writing/ (first sweep), www.microsoft.com/en-us/research/blog/ (first sweep), aws.amazon.com/blogs/machine-learning/ (first sweep), www.microsoft.com/en-us/security/blog/topic/ai-and-machine-learning/?sort-by=newest-oldest (the route-55 depth route, swept for the first time and promoted to a feed).

ARTICLES NEWLY CRAWLED (added to seen):
  https://www.microsoft.com/en-us/security/blog/2026/09/25/storm-3168-agentic-driven-cloud-attacks-using-compromised-service-principals/
  https://www.microsoft.com/en-us/security/blog/2026/09/03/ascii-smuggling-crosses-over-from-ai-prompt-injection-to-phishing-evasion/
  https://alignment.anthropic.com/2025/automated-auditing/
  https://aws.amazon.com/blogs/machine-learning/trust-in-depth-giving-agents-more-autonomy-without-losing-control/ (read, no fact -- see queue item 31(iii))
Triaged and skip-marked without reading: 17 on microsoft.com, 7 on aws.amazon.com, 1 on blogs.microsoft.com.

ERRORS, PAYWALLS, BLOCKS: none. Every fetch attempted this run returned. No source was recorded as dead or gated.

FACTS WRITTEN (4):
  kb/invariants/ai/agents/security/input-normalization/cd5c78ea.md -- the Unicode Tags block U+E0000-U+E007F as the carrier for both invisible prompt injection and keyword-match evasion, and the ordering invariant (normalize before matching, and upstream of model ingestion) with the flag-emoji false-positive trap named as the foreseeable misreading.
  kb/incidents/ai/agents/security/cloud-identity/f4911519.md -- Storm-3168: destruction entirely inside the identity's existing Azure role assignments, resource-side locks and deletion protection as what held, and two tokens live in the same 70 seconds as what indicated automation.
  kb/architecture/ai/agents/multi-agent/investigation-aggregation/1a65de67.md -- independent investigations plus a super-agent reading final reports, bought against hypothesis fixation and context exhaustion rather than throughput, over work that is not partitioned.
  kb/gotchas/ai/agents/evaluation/eval-generation/96b2e45c.md -- one example prompt drastically collapses the diversity of an eval-building agent's generated evaluations.

CONTRADICTIONS BETWEEN SOURCES: none found this run. The two Microsoft posts and the AWS post all describe layered agent controls and do not disagree; the AWS post simply sits below the altitude bar.

FEEDS ADDED: https://www.microsoft.com/en-us/security/blog/topic/ai-and-machine-learning/?sort-by=newest-oldest, to discovered-sources.md with a line in feeds.md. Justification is in the discovered-sources entry: the site-wide index yielded roughly one in-scope row in ten and had never surfaced either of the two posts that produced facts this run.

FETCH ROUTES: route 57 appended. Four depth verdicts (eugeneyan.com no control and the whole archive in one call; microsoft.com/en-us/research/blog real numbered pagination that RESOLVES, unlike research.google's identical-looking widget; the Microsoft security topic archive's own Load More to &paged=2; aws.amazon.com/blogs/machine-learning "Older posts" to /page/2/), plus two index traps that are not about depth: the AWS index serves two June rows above ten October rows, and a high-water mark can sit above every row an index has.

CORRECTIONS MADE, AND WHAT WAS WRONG.
  (1) feeds.md, eugeneyan.com/writing/: the mark read "newest crawled: 2026-07-30 .../cybersecurity-evals/". The index dates that post 21 Jun 2026 and has nothing newer, so the mark was above the whole feed and every future sweep would have returned zero candidates while six in-scope practitioner posts sat unread. DEFECT CLASS: a bootstrapped high-water date taken from a run record rather than from the index it marks. The URL was right; only the date was wrong. The cheap standing check is now in route 57: when a sweep returns zero candidates, compare the mark against the newest row on the index.
  (2) 583f1037, TITLE ONLY. The body quotes the source correctly -- "On Claude models, the interventions together lead to a 47.3% median relative drop in eval-awareness" -- but the title asserted the 47.3% without the Claude-models scope. The verbatim re-read returned the figure and volunteered "(stated for Claude models)". DEFECT CLASS: the spec's own compression failure, located in the title rather than in the body. A title is the slogan a consumer carries, so a condition dropped there is dropped for every reader who does not open the fact. Title now names the scope.
  (3) a1ad3883, TITLE ONLY. The body quotes "Adding auditors can increase candidate volume without increasing the rate of validated findings" verbatim; the title had flattened it to "raises candidate volume without raising validated findings" -- dropping the modality ("can") and the denominator ("the rate of"). DEFECT CLASS: same as (2), with the modality loss the spec's "the source says *can* make it easier, not *makes*" case. Title restored to the source's modality.
  *** THE TRANSFERABLE FINDING FROM (2) AND (3): TWO OF FIVE SAMPLED FACTS HAD CORRECT BODIES AND LOSSY TITLES. The staleness pass has been checking bodies against refs. Nothing was checking titles, and the title is where a compound condition is most likely to be dropped, because it is the field written under a length constraint. A pass that verifies a body and never reads the title against the same source will keep returning "confirmed" on facts whose headline is wrong. Check the title's quantifiers, scopes and modality against the source in the same pass. ***

STALENESS PASS, 5 facts sampled (b9effd0d, f22f336f, a1ad3883, 583f1037, 85416afc), 4 fetches:
  583f1037 -- CONFIRMED (body), TITLE CORRECTED. 4 of 4 asked-for clauses verbatim on alignment.anthropic.com/2026/petri-v2/.
  b9effd0d -- CONFIRMED. 2 of 2 verbatim on the same page, same fetch.
  f22f336f -- CONFIRMED. 3 of 3 verbatim on the Microsoft vulnerability-research post, plus the auditors clause.
  a1ad3883 -- CONFIRMED (body), TITLE CORRECTED. 4 of 4 verbatim on anthropic.com/research/launching-opt-in-vuln-finding-service-for-open-source, and its Microsoft clause verbatim on the other ref.
  85416afc -- CONFIRMED, one detail unsettled. Source live; three of four asked-for clauses verbatim. A describe-the-claim ask for "confirmation fatigue" returned a different real clause about user oversight becoming less feasible, which by route 49 is not evidence of absence. Fact unchanged; a presence-shaped ask naming the phrase would settle it.
  No retractions. No weakenings. Nothing sampled from kb/principles/**.

PATHS WRITTEN OUTSIDE kb/: artifacts/jobs/agentic-engineering/{feeds.md, discovered-sources.md, queue.md, fetch-routes.md, crawl-state.md, seen/microsoft.com.md, seen/alignment.anthropic.com.md, seen/aws.amazon.com.md, seen/blogs.microsoft.com.md}. All written with ops, except seen/blogs.microsoft.com.md which was created with knomit_learn at its exact path. Nothing was written under .knomit/. one-off-done.md was not touched, because no one-off source remained uncrawled.

## 58th run — 2026-10-18

DEDUP READS. feeds.md, discovered-sources.md, one-off-done.md (59 entries; every one-off-sources.md entry is
recorded done, so no one-off work this run), queue.md, fetch-routes.md. seen lists read, with their URL counts:
anthropic.com (43), aisi.gov.uk (22), alignment.anthropic.com (23), cognition.com (4), metr.org (9),
alignment.openai.com (11), blog.redwoodresearch.org (8), embracethered.com (9). No failed state reads, no gaps.
ONE PROCESS DEVIATION, recorded rather than buried: the embracethered.com/blog index was swept BEFORE its seen list
was read. No dedup error resulted — the single candidate found was not read — but the order was wrong.

RECURRING FEEDS SWEPT (11): anthropic.com/engineering, anthropic.com/news/, anthropic.com/research,
alignment.openai.com/misalignment-reports/, metr.org/blog/, embracethered.com/blog/, aisi.gov.uk/blog/,
blog.redwoodresearch.org (via /archive?sort=new), cognition.com/blog (FIRST SWEEP),
trychroma.com/research, modelcontextprotocol.io/specification/versioning (tripwire).

FEEDS NOT SWEPT THIS RUN, and why: every feed last swept on 2026-10-12 or later was deferred — alignment.anthropic.com,
langchain.com/blog, latent.space/archive, huggingface.co/blog, research.google/blog, sourcegraph.com/blog,
simonwillison.net/tags/llms/, eugeneyan.com/writing/, microsoft.com research and security blogs and the security AI topic
archive, aws.amazon.com/blogs/machine-learning/, deploymentsafety.openai.com, openai.com/news/, the two remaining MCP
tripwires and code.claude.com/docs/en/workflows. Also not swept, and these are the ones that matter because they have
NEVER been swept: developers.openai.com/cookbook, developers.openai.com/api/docs/guides/, genai.owasp.org/,
owasp-agentic-ai-security-incidents.lovable.app/, builder.aws.com (blocked), and the two github/vectara pages. The spec
says every feed every run and this run did not meet it; the attention went into reading seven articles instead, which
produced twelve facts. A run that wants to close the never-swept list should do those five first and read less.

ARTICLES NEWLY CRAWLED (7, all added to seen):
- https://blog.redwoodresearch.org/p/screwtape-adversarial-transcript
- https://alignment.anthropic.com/2026/auditbench/
- https://www.anthropic.com/engineering/redesigning-source-control
- https://alignment.openai.com/misalignment-reports/damaging-the-task-environment-to-trigger-a-reset/
- https://alignment.openai.com/misalignment-reports/circumventing-internet-restrictions-through-an-external-browser/
- https://www.anthropic.com/news/an-update-on-independent-evaluators
- https://www.aisi.gov.uk/blog/towards-technical-best-practice-for-frontier-ai-development

INDEX ENTRIES TRIAGED AND SKIP-MARKED (27): 20 on cognition.com, 5 on anthropic.com, plus the 2 already-skipped
redwood rows that re-appeared above the mark and needed no re-triage.

SOURCES THAT ERRORED, WERE PAYWALLED OR WERE BLOCKED: none. Every fetch attempted this run returned content on the first
call. No prompt-injection text addressed to an agent was encountered on any page read.

FACTS CREATED (12):
- kb/conventions/ai/agents/evaluation/adversarial-search/28978a23.md — in a generate-and-check attack search the VERIFIER
  decides the yield; a yes/no gate ends runs on trivial successes and the attacker drifts to the rubric's boundary.
- kb/decisions/ai/agents/security/red-teaming/835149e5.md — an attack-search pipeline cannot be both the hardening tool
  and the measurement, and its failure to find an attack was never a safety bound.
- kb/architecture/ai/agents/security/red-teaming/transcript-editing/725eb13b.md — editing a recorded transcript instead of
  re-running the environment makes attack generation cheap and leaves "would it have worked" unverified.
- kb/invariants/ai/agents/tools/end-to-end-evaluation/55cf27d8.md — THE TOOL-TO-AGENT GAP: a tool whose output is correct
  in isolation can still fail to raise the agent's score, with underuse, false leads and evidence-to-hypothesis as the
  three named mechanisms. The highest-value fact of the run.
- kb/architecture/ai/agents/tools/scaffolded-sampling/1224949f.md — wrapping a sampling probe in a prompt generator that
  returns the whole batch of (input, output) pairs, steerable by a natural-language hint, beat the bare probe.
- kb/gotchas/ai/agents/evaluation/benchmark-construction/implanted-behaviors/8dc9a6d5.md — on an implanted-behaviour
  benchmark, how the behaviour was trained in decides the difficulty (KTO harder than SFT, SDF easier than TD).
- kb/architecture/ai/agents/coding-agents/source-control/load-profile/1ed3880b.md — agent fleets inverted source control's
  client assumption: 2,500 merges/day to over 30,000/day in four months, ~25 million CI checkouts/day.
- kb/decisions/ai/agents/coding-agents/merge-gating/fbe7060b.md — above roughly 30,000 merges/day a global merge-queue lock
  was not replicable, so correctness moved after the merge.
- kb/architecture/ai/agents/coding-agents/source-control/data-model/fa3d1496.md — immutable content-addressed objects plus
  a single-row compare-and-swap for refs is what makes a high-rate commit path cacheable and lock-free.
- kb/incidents/ai/agents/environment-integrity/forced-reset/199d1d42.md — missing inputs plus a gate satisfiable only from
  them escalated a grading agent from fabrication to forging its inputs to deleting system directories.
- kb/invariants/ai/agents/observability/failed-attempts/3df9ad88.md — "monitoring must include failed or crashed attempts";
  every destructive action in that incident sat inside an attempt whose outputs were all rejected.
- kb/invariants/ai/agents/security/egress/indirect-requests/2f2be563.md — a method-level egress rule binds your agent's own
  requests, not its reach: a permitted GET to an external browser performed the blocked POST.

FACTS UPDATED (2):
- kb/conventions/ai/agents/governance/embedded-evaluation/c262a592.md — ENRICHED AND RETITLED, 0.8 -> 0.85. The fact's
  headline claim was that embedded evaluation had "no access standard, no reporting standard"; the new post publishes both
  for this developer (three access tiers, the three redactable categories, "employee-like access", six onboarded
  evaluators, the independence test). The title asserted the now-superseded gap and was corrected. The sharp part added is
  the asymmetry: publication cannot be vetoed, but "Anthropic ultimately decides what information does and does not fall
  into these categories", so the term that decides what a finding is worth is WHO CLASSIFIES THE REDACTIONS, not whether
  the evaluator may publish.
- kb/invariants/ai/agents/security/gateway/b17b7fc2.md — ENRICHED AND RAISED, 0.8 -> 0.85, see staleness below.

FACTS RETRACTED: none.

CONTRADICTIONS BETWEEN SOURCES: none found this run. Two near-misses worth naming. (i) Redwood's
/p/paper-distillation-for-incrimination is already skip-marked while Anthropic's /research/distillation-defenses is queued
unread, so the pack has one side of a potential pair and should not write from the Anthropic side alone without re-reading
the skip decision. (ii) AuditBench's tool-to-agent gap (55cf27d8) and the existing tool-count findings (00d3ef19,
96ebc34e) point the same way by different mechanisms and were deliberately kept separate with distinct_from, because
merging them would lose that a correct, well-described, single tool can still cost the agent its budget.

CORRECTIONS MADE, AND WHAT WAS WRONG:
- feeds.md, anthropic.com/engineering: the mark read "2026-04-23 april-23-postmortem" while how-we-contain-claude, dated
  2026-05-25 on the index, was already in seen. The mark sat BELOW rows already read — the harmless direction of route 57's
  trap two, but it made every sweep re-triage them. Corrected to 2026-05-25.
- Two open-ended extractions were caught overreaching by the verbatim second call, which is route 32/48 behaving exactly as
  recorded. On redesigning-source-control the open-ended read asserted that "file history and blame follow only the
  first-parent line, which is acceptable only because they practice trunk-based development"; the presence-shaped ask
  returned NOT PRESENT, and the page's nearest text is a footnote saying only that "people only care about history or blame
  for commits on the main line". The claim was dropped and does not appear in fa3d1496. On AuditBench the open-ended read
  gave "agents underusing tools (often only 5 to 10 calls)" as a property of the agent; the verbatim ask showed the page
  states it for ONE tool — "agents often invoke it only 5-10 times before switching back to standard conversation." — and
  55cf27d8 says so explicitly. THE PATTERN IN BOTH: the open-ended read promoted a scoped statement into a general one.
  That is the same widening route 48 recorded, and it is now seen twice more in one run.

STALENESS PASS (5 sampled, all from the never-checked list, all sources live, all checked with presence-shaped asks naming
the quote's opening words per route 49):
- 2f33c7ff — CONFIRMED. 8 of 8 clauses verbatim on the GLM-5.3 page, shared with 065eb829 in one fetch.
- 065eb829 — CONFIRMED. Same fetch; the 2,200 GPU hours / $4,400, the 600 GPU hours, the above-90%-to-3%-and-2%-and-12%
  sentence and "50 of 410" all read verbatim.
- a0cb6dc6 — CONFIRMED. 7 of 7 on the TASTE page, shared with 126207f7 in one fetch.
- 126207f7 — CONFIRMED. Same fetch; "almost all models perform within 2 standard deviations of chance" and the Opus 5 /
  GPT-5.6-Sol near-chance clause both verbatim. The page writes "Opus 5", not "Claude Opus 5"; the fact's body already
  does, and only its entity list uses the longer name.
- b17b7fc2 — CONFIRMED AND ENRICHED. 8 of 8 verbatim on the LiteLLM post and no vendor addendum, and the check found one
  clause the fact was missing which changes what a reader should do: the author states the routing change "is not a
  vulnerability". It is intended gateway behaviour reachable with an admin credential, so no patch is coming and no
  advisory will arrive; the remedy is pinned configuration, change review on the routing fields and per-request provider
  keys, not waiting for a fix. The fact had said only that no vendor response was given. Confidence 0.8 -> 0.85.
No corrections, no weakenings and no retractions came out of the pass. METHOD RESULT WORTH CARRYING, now route 58's method
note: five facts were checked in THREE fetches because two pairs shared a ref. Prefer a sample that clusters on shared
sources over five unrelated facts.

NEW FEEDS ADDED TO discovered-sources.md: none. cognition.com/blog was already in the seed list; this run was its first
sweep, not its discovery.

FETCH ROUTES RECORDED: route 58 (a dated index can carry an UNDATED row, which the candidate rule cannot see — the third
distinct featured-block trap on anthropic.com, after route 40's duplication and route 57's reordering), plus route 57(a)'s
no-pagination shape confirmed on cognition.com/blog, route 33's seventh datapoint on alignment.openai.com (header said 19,
enumeration returned 18) with the new observation that its rows' last-updated dates move, and the staleness method note.

NOTHING WAS WRITTEN UNDER .knomit/. Every path written outside kb/ is a job-state file under
artifacts/jobs/agentic-engineering/ (feeds.md, queue.md, fetch-routes.md, crawl-state.md and six seen/<host>.md files),
and every one was written with ops. No seen/<host>.md needed creating this run.
