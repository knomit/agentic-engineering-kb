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
