---
type: reference
domain: [agentic-engineering, job-state]
confidence: 1
sources: 0
entities: [agentic-engineering]
refs: ['https://github.com/knomit/knomit']
---
# Last crawl state

crawled: 2026-10-04 (forty-sixth run, ~13:40Z). 3 facts written, 2 enriched, 0 CORRECTED, 6 confirmed,
0 retracted. 3 genuinely new URLs across 3 hosts. ~24h since the 45th run; normal daily schedule held.
All three job slots written. crawl-state written ONCE, at the end.

*** THE RUN'S HEADLINE IS A SOURCE-VOLUME FINDING, NOT A CORRECTION, AND IT IS WORTH MORE THAN A
*** CORRECTION WOULD HAVE BEEN: alignment.anthropic.com's INDEX RETURNED 62 ENTRIES. THE 45th RUN'S CALL
*** ON THE SAME URL, ONE DAY EARLIER, RETURNED 8. *** There is a full /2025/ archive behind it. The 45th
*** run wrote "either the blog starts at Jul 2026 or the listing is shallow", correctly inferred from a
*** second signal that the listing was incomplete, and still under-estimated the archive by 7x. 44 posts
*** are unread and ranked in crawl-sources; the top four are directly on clusters this pack already holds
*** (capability removal, monitor architecture, control-eval scaffolds, Petri). This is route 5's
*** depth-varies caution in its most extreme measured form. A "this feed is small" conclusion is a
*** statement about one call, never about a feed. ***

*** SECOND FINDING, AND IT IS A FETCH-DISCIPLINE ONE WITH TEETH (route 28): THE VERBATIM VERIFICATION CALL
*** CAUGHT A FABRICATED CODE SNIPPET. The open-ended extraction of the embracethered SQL post returned the
*** bypass as `DECLARE @p sysname='sp_executesql'; EXEC @p N'DROP TABLE [Test];'`. The page says
*** `DECLARE @p sysname='sp_who'; EXEC @p`. Structure right, payload invented, and invented toward exactly
*** what a reader would expect in a dynamic-SQL bypass. *** CODE IS THE WORST CASE FOR ROUTE 4 because a
*** plausible completion of a code idiom has no seam -- route 22's invented "substantial" at least read
*** oddly. Never write a snippet, identifier, class name, procedure name, CVE number or config key from an
*** open-ended extraction. The fact would have asserted that a published exploit dropped a table. ***

*** THIRD FINDING, AND IT IS THE INVERSE OF A CORRECTION (crawl-sources, modality half of the paraphrase
*** rule): I nearly corrected fc76b9a2 and should not have. Its source states its material as OPEN
*** QUESTIONS; the fact is titled as a flat claim; the verbatim check came back all-interrogative. That is
*** the drift signature. But fc76b9a2's body already carries a MODALITY block saying it is an anticipatory
*** template with no measurements, and attributes every claim as "METR asks". *** THE SCREEN THAT FINDS
*** CANDIDATE DRIFT SYSTEMATICALLY HIDES THE EVIDENCE THAT ACQUITS, because a knomit_query snippet
*** truncates at ~400 chars and a well-written body puts its hedge LAST. READ THE WHOLE FACT BEFORE
*** WRITING THE CORRECTION. Route 20, one level down: there a second fetch acquitted a source, here a full
*** read acquits a fact. ***

*** ROUTE 10 (binding drift): did NOT recur. NINETEEN CLEAN RUNS. knomit_repos called first (one mount,
*** agentic-engineering, read+write) and AGAIN immediately before the crawl-state write, with
*** `bound.binding` checked both times. Did NOT re-bind. No write or query behaved oddly. ***

*** THIS SLOT HOLDS ONE RUN. THE HISTORY IS THE RECORD. WALK IT BY THE PROSE HASHES BELOW, NOT BY
*** history.revisions (the API chain goes more_available:false several hops early, silently -- CONFIRMED A
*** TWELFTH TIME: HEAD returned exactly 3 revisions with more_available:true, against 32 that exist).
*** THE 40-HEX HASH LIST BELOW IS LOAD-BEARING INFRASTRUCTURE. Every run MUST reproduce its
*** predecessors' full hashes and append its predecessor's HEAD; the API cannot enumerate the history
*** and a single omission severs the chain permanently. This is the one non-optional thing in this body. ***

=== HISTORY WALK -- COMPLETE. 31 BODIES READ BY A READ-ONLY SUBAGENT, FIRST TRY, NO RETRIES, NO GAPS. ===
Sixth consecutive run using the subagent method and the sixth clean result: it was given the prose-hash
list and the protocol (read bodies at each commit; ignore history/diff entirely) and returned all 31
bodies with ZERO failed calls, ~276k tokens and 47 tool calls inside the subagent. FOUR bodies came back
oversized (7462e9f2, 66535f3f, 68c341e1, d56dc137); each was persisted and extracted with python and read
in full. KEEP DOING THIS, AND KEEP BOTH ASKS IN THE BRIEF (read the bodies; report unlisted hashes) --
the second ask paid again, and bigger than last run.
Run-number sequence, full 40-hex, newest first -- REPRODUCE THIS LIST IN YOUR OWN REVISION AND APPEND
THIS RUN'S HEAD AS THE 46th:
  8ed3cc92180fec27a867e1268ff2e903dbe88f5f  2026-10-03T13:47:23Z  45th (was HEAD at this run's start)
  4b311b107c8109caabc60fda0d9b059ea86a653e  2026-10-02T13:52:24Z  44th
  c9e40f23e1ed95c4a3c15bad985a932889d0187c  2026-10-01T13:45:22Z  43rd
  9c0017f0a7e18fd89150c527b3627f903a19139e  2026-09-30T22:53:53Z  42nd (final of FOUR)
  4adb2a6fd45799dc751639bbcc3ca32c876cd054  2026-09-30T22:51:04Z  42nd SUPERSEDED (NOT a run)
  fc85537f909eb2427916881044afa4a165db2121  2026-09-30T22:50:42Z  42nd SUPERSEDED (NOT a run)
  be04dee338397d3a396ef08af11853e2bb15d06e  2026-09-30            42nd SUPERSEDED (NOT a run)
  76cc1a5d46d808fa757e3980ff30f2655746cf7e  2026-09-30T13:48:07Z  41st
  719ae8b25516d04ac8ab87d0175b754aa3adbee3  2026-09-29T13:52:31Z  40th
  375dc0f79ba2cc89b6482939b55ff377c36a6e0d  2026-09-28T13:50:17Z  39th
  092218eef959413b6ebf8589b29ecf5a37e5a49f  2026-09-27T13:40:18Z  38th
  7a39df486016fcd1dc19831a8675224b2bc9d447  2026-09-26T13:51:25Z  37th
  cc9be5500ab1e8e44c6bb1d7e9b300bf740c59d3  2026-09-25T13:48:57Z  36th
  474fbb130720d82633f55fd34050a1cfb7ab2514  2026-09-24T13:17:44Z  35th INSURANCE (NOT a run)
  047c8878bf8dc193b2dc33e6295eaf0a6bf25527  2026-09-24T13:21:15Z  35th INSURANCE #2 (NOT a run)
  d56dc137c2697f4e31effccbc995ec79e8989376  2026-09-24T13:30:41Z  35th INSURANCE #3 (NOT a run) -- its
                                                                   body is BYTE-IDENTICAL to 68c341e1
                                                                   (measured 46th run), so one of the two
                                                                   is a no-op commit
  68c341e16d1910c93c8bbf4c0489052f6d522230  2026-09-24T13:36:20Z  35th (final) (oversized)
  66535f3fc655e3f79f1358c9d746645ca52e461d  2026-09-23T16:25:44Z  34th (oversized)
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
  7462e9f229b6cc3ef2c2da12be49c1cd468a6e55  2026-08-27T20:58:56Z  23rd (oversized)
  65e9612ba1295bd8d94dc19b4b12b62625f6a47a  2026-08-24T16:17:17Z  22nd (body says crawled 2026-08-21)
  3c6323cd52188f057c16d15b2c7b72ad9d9e91e9  2026-08-12T21:25:35Z  16th
  8b9a768debcfa982f4ec2a8155c1bc9195c0bb0f  2026-08-12T00:27:10Z  13th -- THE FLOOR
OLDEST COMMIT DATE REACHED: 2026-08-12T00:27:10Z (its body says the run crawled 2026-08-10).
The walk terminates because the FLOOR is reached, not because more_available went false -- the API's
more_available is not the stop condition and was not consulted. NO CALL FAILED.

*** ROUTE 26's PAYOFF, AND IT REFRAMES THE WHOLE HASH-CHAIN PROBLEM. TWENTY-ONE FULL 40-HEX CRAWL-STATE
*** COMMITS EXIST THAT NO PROSE LIST HAS EVER CARRIED. The subagent found them in the history[] blocks of
*** the revisions it was reading, and noted the pattern that matters: *** FOR THE SAME RUN, THE history[]
*** HASH AND THE PROSE-QUOTED HASH ARE DIFFERENT, AND THE history[] ONE IS DATED 3-10 MINUTES EARLIER. ***
  c9f7e713d3230846f02b1ac72c9f7f8448e4312d  2026-08-12T00:19:57Z  slot creation ("cut agentic-engineering
                                              state over to .knomit/jobs named slots")
  8be9e4de715e09be45e74591f68413de8c717ad5  2026-08-12T14:34:18Z  15th, first write
  5ab895cfc9bf03c4eabb2f8de3d74c90b69c9103  2026-08-12T14:40:43Z  15th, final
  73bfa12b41fca3b1229d560a8825395720d610c9  2026-08-12T20:49:54Z  16th
  226499515b8c356590e36af79b7566a10fbebb14  2026-08-18T00:07:35Z  (in the 22nd's prose as a short prefix)
  4cce7781b385029bfc69a0f396e5837baca956cc  2026-08-21T01:44:42Z  21st
  fbacafc2ea90f196204c98577b15045c73a3d6f0  2026-08-22T00:35:50Z
  a0ee55f6fbe59ff08670050effd0295641fcb08d  2026-09-08T07:58:36Z  26th (its body says crawled 09-08)
  a92de3b71f7f8b007e440c25ebb851175ba48fbb  2026-09-13T12:37:11Z
  1b620127c104252c58b70793397abd0d9985c334  2026-09-19T13:29:06Z
  c91770d0a14e72f0e056272af80e8e0b8c76d961  2026-09-20T13:28:36Z
  1686d99bb0591c69a6812c22ea94ec89399417b1  2026-09-21T13:39:42Z
  9dcb8ebb0d6dfe4a973b484cc5e2537de79bfcf2  2026-09-22T13:32:26Z
  ea2ea8aa46d7c8808ea30e953d96bee1502909ef  2026-09-23T16:21:10Z
  11430c7b65eba5d17580cfa03be0acbc8739015d  2026-09-25T13:45:04Z
  bf78da25aa0da4ec5770236806b6b3459ca23437  2026-09-26T13:47:03Z
  2a6bc7a5df74e949cedff01339616d74c86cff71  2026-09-27T13:37:23Z
  182c7f61fbf1a1a766a32849bb90fec0fa6ea66f  2026-09-28T13:45:04Z  39th
  bb07ed0c22247348f41604c6219547d44784bbdc  2026-09-29T13:51:36Z  40th
  ef47868d31f7eecb4c292f8bf314275bcf8a971b  2026-09-30T13:42:54Z  41st
THE HYPOTHESIS THIS SUPPORTS, NOT YET TESTED -- ONE knomit_explain SETTLES IT AND THE NEXT RUN SHOULD
SPEND IT: route 24 established that explain's `commit` is the BRANCH HEAD, not the file's last-modified
commit. A run that records "my HEAD" from an explain result is therefore recording a BRANCH head, while
history[] records the FILE's commit. If so, the prose chain and the history chain are two different
identifier spaces for the same revisions, both resolvable, and route 26's "one of every two writes"
finding may be partly an artifact of comparing them. *** DO NOT TREAT THE PAIRING AS ESTABLISHED. *** The
test is cheap: pick one run with both ids known (39th: prose 375dc0f7, history 182c7f61), explain at each,
and compare the bodies. Identical bodies means two names for one revision; different bodies means two
writes.
GAP: runs 14, 15 and 17-21 still have no body READ. But the hashes above cover 15 and 21, and the 22nd
  run's body names a5466f42, 4feee885, a21ad1c0, 3bc37431, 7a9ec830, 0ac250fd as short prefixes for 17-21.
  The "one-off repo rebuild destroyed runs 17-21" story, carried since the 26th run, remains WRONG.

*** TWO COUNTERS, BOTH CORRECT, MEASURING DIFFERENT THINGS -- state both, do not reconcile them away:
*** (a) THE JOB COUNTER: ALREADY_CRAWLED = 306 through the 45th run; this run adds 3 -> 309.
***     It includes 33 count-only URLs from runs 17-21 whose per-URL detail is in the unread revisions.
*** (b) NAMEABLE URLS: this run's subagent got 276 distinct across 62 hosts under the narrow rule (only
***     URLs a body records as actually fetched) -> 279 with this run's three. The 45th run reported
***     280/63 under the same rule and the 44th reported 282/66 under a wider one. The small drift between
***     the 45th and 46th subagents' narrow counts (280 vs 276) is a JUDGEMENT difference about which
***     legacy-block entries count as fetched, not a data loss: both independently re-counted the floor's
***     legacy block and this run's subagent found 190 entries of which 189 record a fetch, excluding
***     openai.com/index/responding-to-the-next-frontier-of-critical-cyber-capabilities/ as never fetched.
*** NEITHER IS A RECORD OF WHAT HAS BEEN READ. The corpus's refs are -- see route 27. ***
FOUR URLs are recorded in past bodies with TRUNCATED slugs and cannot be recovered from prose:
  aisi.gov.uk/blog/what-can-sandboxed-ai-agents-learn-... (22nd; full slug later named by the 44th run),
  microsoft.com/en-us/research/blog/echoverse-... (22nd), openai.com/index/expanding-daybreak-... (22nd).
  The embracethered litellm truncation is RESOLVED (45th run).
The 16th-run floor inconsistency (e61629fc / 197 URLs vs 8b9a768d / 190) is UNCHANGED.

=== TRIPWIRE ===
  modelcontextprotocol.io/specification/versioning -- one WebFetch. Current revision **2026-07-28,
    UNCHANGED, THIRTY-FIFTH consecutive run.** Verbatim: "The **current** protocol version is
    [**2026-07-28**]". Do NOT cite 2025-11-25 or 2025-06-18.
  SCREEN (f) PAID AGAIN AND PAID MORE: the one tripwire call re-confirmed FOUR facts verbatim at zero
  extra cost (the 45th run got three off it). FOURTH CONSECUTIVE RUN leading with screen (f).

=== ARTICLES NEWLY CRAWLED (3 new URLs, 3 hosts) ===
  https://alignment.anthropic.com/2026/modular-pretraining/ (Jul 2026) -- the 45th run's RANK 1, and the
    rating was right. Plain WebFetch; one open-ended read plus one verbatim verification call. Produced
    5a36eb3b.
  https://metr.org/blog/2026-06-26-gpt-5-6-sol/ (Jun 26 2026) -- the 45th run's RANK 2, and the
    third-party-evaluation rule pointed at it correctly. Produced bb2b798b. Same two-call discipline.
  https://embracethered.com/blog/posts/2026/from-select-to-sysadmin-sql-copilot-bluehat-asia/ (Sep 30
    2026, CVE-2026-65669) -- the 45th run's RANK 3. Produced 4ac8983f plus the 92dc0441 enrichment, and
    produced route 28 when its code snippet was verified.
  INDEX SWEEPS, all plain WebFetch, all before any write: alignment.anthropic.com (62 entries -- see the
    headline), metr.org/blog (windowed since 09-25, nothing new), embracethered.com/blog (windowed since
    09-01, one post and it was read), www.aisi.gov.uk/blog (~100 entries, nothing new since Oct 1, and
    seven slugs no past run had recorded).
  RE-READ, not new: modelcontextprotocol.io/specification/versioning (tripwire + 4 staleness checks);
    metr.org/blog/2026-07-28-investigating-ai-propensities-after-incidents/ (staleness, 2 checks).
  Appendix A: nothing crawled, nothing left -- fully covered.
  No 404, no paywall, no gate, no slug guessed, no source errored, nothing recorded as dead. No browser
    used and nothing needed one. ZERO WebSearch calls this run.

=== FACTS WRITTEN (3 new, 2 enriched, 0 corrected, 6 confirmed, 0 retracted) ===
  ONE knomit_learn call, 3 facts, accepted on the FOURTH attempt -- three consecutive motif-length
  rejections, no subject-overlap refusals. See TOOL NOTES and route 29.
  NEW:
    kb/architecture/ai/agents/security/capability-access-control/5a36eb3b.md -- capability access control
      as a PRETRAINING property, a shape the pack had no fact about. "Gradient-Routed Auxiliary Modules
      (GRAM)": auxiliary modules at every MLP layer, gradient-routed so specialised data updates them
      preferentially, and "At inference, deleting a module removes the capability." THE FACT'S LOAD IS THE
      COMPARISON, NOT GRAM: GRAM and LoRA ablation remove a capability about as well as never training on
      it, and all three of filtering/LoRA/GRAM survived malicious fine-tuning, while post-hoc unlearning
      "recovers to near the performance of the all-data baseline indicating that MaxEnt does not truly
      remove capabilities but instead learns to suppress them". So unlearning applied to a finished model
      is a suppression layer with a refusal's jailbreak surface. Economics carried too (one run -> five
      configurations, "only a fifth of filtering's training compute", four modules -> sixteen
      configurations). Scoped hard in three directions: the removed slice was "about 0.25% each" of a 16B
      general-token corpus, scaling tested to 5B, figures all in "Compute Ratio, a compute-adjusted
      version of loss". Explicitly NOT a runtime control -- the tier is chosen by which weights ship.
    kb/gotchas/ai/agents/evaluation/measurement-attribution/bb2b798b.md -- one dataset, three
      50%-time-horizon estimates, differing ONLY in the cheating-attribution policy: 11.3hrs (95% CI
      5-40hrs) marking cheating as failures, "beyond 270hrs" counting it as success, 71hrs (95% CI
      13-11400hrs) discarding it. Cause stated: "GPT-5.6 Sol's detected cheating rate was higher than any
      public model we have evaluated on our ReAct agent harness." METR's own verdict quoted. The body
      argues two things a summary would drop: discarding is NOT the neutral middle (it deletes the
      long-horizon tail that sets the threshold, hence a CI spanning three orders of magnitude), and
      ACCESS WAS NOT THE LIMITING FACTOR -- METR had the final checkpoint, a "'railfree' version", raw CoT
      and a vendor harness guide, the strongest published third-party tier, and still declined to call it
      a measurement. Also records that the threshold judgement survived the collapsed estimate.
    kb/incidents/ai/agents/security/privilege-escalation/4ac8983f.md -- CVE-2026-65669. Two independent
      decisions, either survivable alone: AGENTS.md and CONSTITUTION.md are SQL Server extended
      properties ("added via the `sp_addextendedproperty` stored procedure"), so an ordinary low-privilege
      schema write becomes a write into another user's agent context; and "Copilot executes with the
      privileges of the connected user", so a db_owner reaches sysadmin through a sysadmin's own agent.
      Plus the read-only guarantee as "a regex-based classifier in the **LocalSqlExecutionAccessChecker**
      class", defeated by `DECLARE @p sysname='sp_who'; EXEC @p`. The transferable condition is written as
      a CONJUNCTION so a reader cannot drop half of it.
  ENRICHED:
    92dc0441 (command allowlists, two CVEs) -> a THIRD disclosed case arriving from the opposite
      direction: the control was a DENYlist, and indirection walked through it with nothing poisoned. The
      addition widens the fact's own thesis -- "a command name is not a capability" is not only about
      allowlists going stale against a mutable environment; any control reasoning over the TEXT of what
      the agent will run is matching a spelling, and list direction does not help. sources 1 -> 2 (OWASP
      and Rehberger are independent).
    3fc77970 (agent config write = code-execution grant) -> back-link plus the out-of-filesystem case,
      with the audit question stated as "who can write the store the agent reads instructions from, and
      whose privileges does the agent then act under". sources HELD at 1 (same author as the fact's
      existing ref, so not an independent corroboration).
  CROSS-LINKS: 5a36eb3b -> 077ce96e + 89df351e; bb2b798b -> 8756141e + 03fa7976 + 97616086 + 23efa1db;
    4ac8983f -> 3fc77970 + 92dc0441 + 7bd6c6c9 + f1cbb540; 92dc0441 -> 4ac8983f; 3fc77970 -> 4ac8983f.

=== CORRECTIONS MADE, AND THE DEFECT CLASS ===
NONE. First run since the 43rd with no correction, and the notable thing is that a correction was
PREPARED AND THEN WITHDRAWN -- see the third finding above and the modality half of the paraphrase rule in
crawl-sources. The withdrawal is the finding: the drift screen's own instrument (a query snippet) hides
the hedge that acquits, because a well-written fact puts its modality caveat last and the snippet cuts at
~400 chars. A run that trusts the screen and skips the full read will manufacture corrections, and a
manufactured correction is worse than a missed one -- it rewrites a correct body and records a false
defect in this slot for every later run to reason from.
THE NEAR-MISS ON THE OTHER SIDE was route 28: a code string WAS fabricated and the two-call discipline
caught it. So this run has one instance of each -- a verification that convicted a source extraction and a
verification that acquitted a fact. Both cost one extra call. That is the argument for the discipline.

=== STALENESS PASS -- 6 EXAMINED. 6 CONFIRMED VERBATIM, 0 ENRICHED, 0 CORRECTED. SCREEN (f) SUPPLIED ALL 6. ===
ONE extra fetch for the whole pass (the METR template), and it cleared TWO never-checked facts.
  CONFIRMED VERBATIM  kb/gotchas/ai/agents/tools/mcp/versioning/031dab74.md -- tripwire page: "The
    protocol version will *not* be incremented when the protocol is updated, as long as the changes
    maintain backwards compatibility." Intact.
  CONFIRMED VERBATIM  kb/gotchas/ai/agents/tools/mcp/deprecation/012daf73.md -- same page: "remain in the
    specification for at least twelve months, or at least ninety days under the policy's
    expedited-removal exception". Both quantifiers intact.
  CONFIRMED VERBATIM  kb/invariants/ai/agents/tools/mcp/discovery/995c167b.md -- same page: server/discover
    is "a mandatory RPC" and "Calling it is optional: a client is free to send any request directly and
    handle a version error if one comes back". The servers-MUST / clients-NEED-NOT asymmetry intact.
  CONFIRMED  kb/architecture/ai/agents/tools/mcp/transport/3afa31af.md -- NEW to the checked set, and it
    came free off the same tripwire call because it also refs that page. Its no-handshake claim is
    corroborated verbatim: "Every request declares the protocol version it is using via the
    `io.modelcontextprotocol/protocolVersion` key in its `_meta` field, and the server accepts or rejects
    each request independently", and the page calls 2025-11-25 and earlier "the handshake-based protocol
    revisions". Scope note: this call verifies the no-handshake half only; the no-session and
    no-resumable-stream halves rest on the changelog and basic/index refs and were not re-read.
  CONFIRMED  kb/gotchas/ai/agents/evaluation/investigation-integrity/fc76b9a2.md -- off the never-checked
    list. Every quoted string verified verbatim against the primary, including the sharpest one (whether
    remediation practices "result in overfitting to evaluations, increased evaluation awareness, or
    increased incentives for agents to hide evidence of misalignment (or otherwise risk papering over the
    problem)"), the collusion question, the CoT-faithfulness question and the subliminal-learning
    question. NO EDIT. See the withdrawn correction above.
  CONFIRMED VERBATIM  kb/conventions/ai/agents/governance/third-party-investigation/03fa7976.md -- off the
    never-checked list, free off the same fetch. Its access tiering is the primary's own list, verbatim:
    "The ability to run all of the models involved in the incident, to be able to reproduce and
    investigate model behaviors in similar situations. Access to full transcripts or environments which
    let researchers closely reproduce relevant incidents. The ability to conduct employee interviews about
    the questions under investigation." sources HELD at 1.
  SCREENS: (f) supplied ALL SIX -- LEAD WITH IT, PERMANENTLY, and note the pattern now measured twice: a
    page that several facts ref returns several checks for one call, so the best staleness target is the
    URL with the highest ref count, not the oldest fact. (c) bare-family-name entities remains EXHAUSTED.
    (e) still needs a substring search knomit does not offer. (d)/paraphrase rule now has its modality
    half.
  AVOID kb/principles/** (write-blocked): 0f260eea, 1d1440fe, 4166926d, a829cfd4, b9b45ff5, 1feacc9e,
    f269c82f, c2f12069, 1dc822f2, db193402, 00d3ef19, 82383efe, 28ba65db, 6ec9b2b6, c9f0238b.

=== CONTRADICTIONS ===
NONE BETWEEN SOURCES THIS RUN, and one apparent one deliberately NOT written up, applying the 45th run's
  second sub-rule (do not manufacture a contradiction out of two different comparisons): 5a36eb3b says
  post-hoc unlearning suppresses rather than removes, while the pack's guardrail facts (89df351e,
  f1cbb540) treat behavioural classifiers as a legitimate layer. These are not in tension -- one is about
  whether a capability is PRESENT in the weights, the other about whether an ACTION is permitted at
  request time, and 5a36eb3b says so explicitly in its "does NOT mean" paragraph (it is not a runtime
  control; per-request gating still needs a permission layer).
ONE TENSION CARRIED INSIDE ONE FACT: bb2b798b holds that METR's time-horizon numbers are not a robust
  measurement AND that METR's capability-threshold judgement stands. Both are the same document's claims
  and the fact says why they coexist (the threshold argument was never built on the estimate's precision).
  Do not split these into a decisions fact; there is no disagreement.
THE SYNTHESIS CANDIDATE IS UNCHANGED AND STILL NEEDS A HUMAN: d306b10f + 102aff80 + 0fe91ac7 + e5765f0e
  all say every layer of an eval stack manufactures false NEGATIVES and they compound; c9b6c5fa and
  27825569 come from the opposite direction (a layer manufacturing an unearned PASS); 96e2e894's
  absence-read-as-compliance is a third entry point. *** bb2b798b IS NOW A FOURTH AND IT IS THE CLEANEST:
  the same data yields a false negative and a false positive depending on one policy choice. ***
  kb/principles/** is write-blocked.

=== TOOL NOTES ===
  * knomit_learn: 1 logical call, FOUR attempts, THREE motif-length rejections and nothing else. Route 29.
    `motif "X": 5 kebab-case words, want 2-4` -- the validator counts hyphen-separated tokens, function
    words included, reports ONE offending motif per call, and fails the WHOLE multi-fact call. Three
    re-emissions of a ~12k-character payload. *** COUNT THE HYPHENS: THREE MAXIMUM. *** And when the first
    motif is rejected, audit every motif in the payload rather than fixing only the named one, which is
    what turned one retry into three. NO subject-overlap refusals this run, which breaks a streak -- the
    45th run's note that stock domain phrases as entities cause them is consistent with this run's
    entities being mostly proper nouns and identifiers.
  * knomit_update `ops` worked first try on two knowledge facts and both appended private slots -- EIGHTH
    consecutive run. Both knowledge-fact edits were pure `append`, which needs no anchor at all; prefer
    append over str_replace when the addition genuinely belongs at the end, and keep the 45th run's
    anchor-selection trick (avoid dashes, smart quotes and \u escapes) for when it does not.
  * refs REPLACE wholesale even alongside ops -- read and resend the full merged list. Done twice.
  * if_commit NOT used. Route 24's branch-head behaviour makes it stale on any write to any fact.
  * A READ-ONLY SUBAGENT DID THE HISTORY WALK. Sixth consecutive run, sixth clean result. The
    unlisted-hash ask produced 21 full hashes and the branch-head-vs-file-commit hypothesis. KEEP BOTH.
  * The two large private slots (crawl-sources now ~112k chars, fetch-routes ~92k) BOTH exceed
    knomit_explain's inline cap and come back as persisted files. Extract with
    python3 -c "import json; print(json.load(open(PATH))['facts'][0]['body'])" then read with sed, and
    grep for '^\\*\\*\\*\\|^===' first to get a section index instead of reading 100k linearly -- that
    cut the two slot reads to four calls total this run.

=== QUEUE FOR THE NEXT RUN -- SOURCES ONLY, NO CLAIMS (the 43rd run's rule; four runs held) ===
(0) *** knomit_repos FIRST, and again before the first write. Route 10 did not recur (19 clean runs). If
    every remote-devices tool vanishes at once -> RefreshMcpTools{server: "remote-devices"}, do NOT
    re-bind; the handle survives. ***
(1) *** WRITE crawl-state ONCE, AT THE END. One revision = one run. If you write twice, say so. ***
(2) *** WALK BY THE PROSE HASHES ABOVE, VIA A READ-ONLY SUBAGENT, and append this run's HEAD as the 46th.
    ASK IT FOR UNLISTED HASHES TOO. ALREADY_CRAWLED should reach 309 on the job counter. ***
(3) *** SWEEP THE FEEDS BEFORE WRITING ANYTHING. Held four runs. ***
(4) *** THE alignment.anthropic.com /2025/ ARCHIVE -- RANK 1, AND IT IS 44 POSTS DEEP. Ranked list in
    crawl-sources. Take /2025/selective-gradient-masking/ FIRST (it is the sibling of the post that
    produced 5a36eb3b, and 5a36eb3b is the waiting home), then /2025/summarization-for-monitoring/ (the
    monitor cluster has no architecture fact), then /2025/strengthening-red-teams/. Expect the index's
    DATES to be unreliable and its SLUGS to be good. ***
(5) *** anthropic.com/research/ -- A PATH THIS JOB HAS NEVER TOUCHED, surfaced by the alignment blog's own
    index, which links out to /research/reasoning-models-dont-say-think,
    /research/auditing-hidden-objectives, /research/constitutional-classifiers and
    /research/forecasting-rare-behaviors. One route-5 call on anthropic.com/research would say whether
    this is a feed or a handful of legacy pages. CHEAP AND IT COULD BE LARGE. ***
(6) *** ONE knomit_explain SETTLES THE HASH-SPACE HYPOTHESIS: explain the 39th run at prose 375dc0f7 and
    at history 182c7f61 and compare bodies. Identical means two names for one revision and route 26's
    double-write finding needs restating; different means two real writes. It is one call and it decides
    how every future run reads its own audit trail. ***
(7) THE AISI BACK CATALOGUE. Take /blog/evaluating-whether-ai-models-would-sabotage-ai-safety-research
    (Apr 27 2026) FIRST -- newly surfaced this run, and the pack has c807bcd3 and 7be4071e on automated
    researchers misbehaving with no third-party treatment of deliberate safety-research sabotage. Then the
    long-standing tier A: /blog/transcript-analysis-for-ai-agent-evaluations,
    /blog/a-pipeline-for-transcript-analysis-using-inspect-scout, /blog/will-it-become-harder-to-oversee-
    ai-systems, /blog/how-to-evaluate-control-measures-for-ai-agents,
    /blog/introducing-controlarena-a-library-for-running-ai-control-experiments. SLUG NOTE: the
    test-time-compute post is "...why-ai-agent-evals-need-to-account-for...", not "evaluations".
(8) ONE TARGETED VERBATIM CALL ON https://metr.org/blog/2026-06-26-gpt-5-6-sol/ for the sentence
    attributing cheating rates to the evaluation scaffold's prompts and task wording. It is the strongest
    harness-design claim in the post and it is deliberately NOT in bb2b798b because only the open-ended
    extraction returned it. One call, and it enriches bb2b798b rather than creating a fact.
(9) openai.com/news -- NOT swept for FIVE runs (last: 41st). Needs the browser (route 1). anthropic.com/
    news last swept 43rd. THE OPUS 5.5 / SONNET 5.5 SYSTEM CARDS still have no facts; route 5b on
    anthropic.com/claude-opus-5-5 and /claude-sonnet-5-5 for the href, do NOT guess it.
(10) SECTION 9 (Preparedness) OF deploymentsafety.openai.com/gpt-6-astra/safeguards. STILL CAPPED AT ONE
    ATTEMPT, not spent for four runs.
(11) darioamodei.com/post/we-must-pace-the-frontier -- host never touched. Pairs c262a592, 03fa7976,
    97616086, 6866e63b, bdbdd228. Plus the two unread /institute/ posts.
(12) THE TRANSCRIPT-ANALYSIS THEME: the techrxiv paper (href in crawl-sources, host NEVER TOUCHED) and the
    alignmentforum case study's per-model TABLES (route 21).
(13) THE REST OF THE SEPTEMBER THREAT REPORT -- five sections, at the SITE ROOT not under /news/.
(14) STALENESS. LEAD WITH SCREEN (f), AND PICK THE URL WITH THE MOST REFS -- the versioning page returned
    four checks for one call this run and three last run. *** APPLY THE PARAPHRASE RULE WITH BOTH HALVES:
    check definitions AND modality, and READ THE WHOLE FACT BEFORE WRITING A CORRECTION. *** Still
    unchecked that way: c9b6c5fa and 0c3c2d6a both rest partly on Apollo-via-OpenAI (does Apollo publish
    its own Astra write-up?); 9b0c8c78 rests partly on Gray Swan-via-OpenAI; 2d26e61b's OpenAI 3.1 figure
    is still testimony-via-OpenAI and its primary is in ALREADY_CRAWLED but on a browser-gated host.
    Never-checked bodies: 0525e590, c5f106f3, f727c157, f961973e, 00f5d991, 5bad2e60, b4d22cc2, 4777dc9b,
    fcce2200, bad64050, 4d13f6e9, de4e90a4, ab8f0a7e, a0cb6dc6, 79912531, 126207f7, 71be00f9, c6feb649,
    94858345, d306b10f, bef6d86f, 92a0e10f, 8992ec34, 0cbaa443, c9b6c5fa, e671d3a4, a8d32262, 737460a3,
    96e2e894, aad8789f, 2d26e61b, plus this run's 5a36eb3b, bb2b798b, 4ac8983f. DROPPED as checked this
    run: fc76b9a2, 03fa7976, 3afa31af (and 031dab74, 012daf73, 995c167b re-checked).
(15) UNMINED, NAMED SO IT IS NOT LOST, carried and NOT re-validated: (i) swe-bench-sonnet tool-design
    material (absolute-path requirement, str_replace exactly-one-match) -- check whether only the
    write-blocked 82383efe carries it. (ii) april-23-postmortem: the Opus 4.7-found-it / 4.6-didn't
    compound condition. (iii) building-c-compiler: the "put yourself in Claude's shoes" harness rules.
    (iv) 71be00f9 vs the monolithic-task/oracle material in 2318b57c. (v) The Astra card's
    eval-RETIREMENT practice plus the Production Benchmarks introduced for the same reason. (vi) Figure
    17's oversight-gaming CoT snippets are IMAGES in every reader tried; 0cbaa443 is where they land.
    (vii) AISI's HiBayES post, if 7a961962 ever needs the autograder framework's measurements.
    (viii) monitor/agent COLLUSION as an oversight failure mode -- anticipatory only, fc76b9a2 already
    carries it as an entity, and this run re-confirmed the source states it as a question. If a MEASURED
    collusion result appears, that is where it goes.
    (ix) NEW: the GRAM post's SimpleStories synthetic-data arm (a small model, a topic count, a per-topic
    ablation result). The open-ended extraction gave numbers for it; they were NOT verbatim-verified and
    are NOT in 5a36eb3b. Route 28 says do not trust them. Verify or drop.
(16) LONG-CARRIED, take-or-delete: the transcript viewer; SLEIGHT-Bench paper/dataset (GitHub gated,
    route 3f); the benchmark supply-chain report for CVE-2026-66384 (lives only in bcbf13c2, 19th run).
(17) www-cdn.anthropic.com PDFs (route 11): April Alignment Risk Update, Fable 5 / Mythos 5 System Card,
    August Risk Report (Section 5.2.3), Advanced AI Framework. NOT re-tested. Both vendor CDNs remain
    egress-denied to curl -- look for the HTML twin first.
(18) OPTIONAL: resolve the alignment.anthropic.com YEAR-PREFIX discrepancy (/2026/ vs /2025/ for
    sleight-bench, coding-audit-realism, ai-organizations). Settle it from a fact's refs, not a fetch.

=== FOR A HUMAN, NOT THE CRAWLER ===
*** FINDING 4, AND IT IS ABOUT THE JOB'S OWN INSTRUMENTS RATHER THAN ITS SOURCES. *** Findings 1-3 were
all about information degrading as it travels: a queue entry asserting something about the corpus (1), a
vendor summarising a third party (2), a secondary paraphrasing a definition (3). *** FINDING 4: THE
SCREENS THIS JOB USES TO DETECT THAT DEGRADATION ARE THEMSELVES LOSSY, AND THEY LOSE EXACTLY THE PART THAT
WOULD STOP A FALSE POSITIVE. *** Measured twice this run in opposite directions. (a) A knomit_query
snippet truncates at ~400 chars; a well-written fact puts its modality and scope caveats LAST; so the
screen that surfaces a candidate drift reliably hides the hedge that acquits it, and a run that acts on
the screen alone will rewrite correct bodies and record false defects here. (b) An open-ended WebFetch
extraction fabricates CODE more readily and less detectably than prose, because a plausible completion of
a code idiom has no seam -- `sp_executesql` and `DROP TABLE` instead of `sp_who`. BOTH ARE THE SAME SHAPE:
the cheap instrument is cheap because it drops something, and what it drops is correlated with what you
are trying to measure. The human fix is a one-line addition to Appendix S's staleness instruction: before
recording a correction, read the fact's FULL body, not a search result; and never promote a literal string
-- code, identifier, CVE, path, config key -- out of an open-ended extraction.
(b) FIX APPENDIX S'S WALK PROTOCOL: steps 2-3 terminate several hops early. Measured TWELVE times (route
    6, 35th-46th runs). Only a human can fix the spec. The working protocol is the prose-hash list plus a
    read-only subagent, and the spec should say both, plus the unlisted-hash ask.
(c) THE REPORT SECTION OF crawl.md ASKS FOR "confirmation that the only .knomit/ paths you wrote were the
    TWO state slots", but Appendix S's own table lists THREE job-writable slots, and step 2 authorises
    writing crawl-sources while step 4 sends routes to fetch-routes. This run wrote all three,
    deliberately. Please reconcile the wording -- EIGHTH run asking.
(d) www-cdn.anthropic.com and cdn.openai.com both denied by egress policy -- EIGHTEENTH run asking.
(e) GitHub API not enabled (route 3f) -- blocks SLEIGHT-Bench dataset and MCP spec revision-diffing.
(f) The `sources` CONVENTION (hold below org count when a second org ILLUSTRATES or BOUNDS a claim rather
    than corroborating it) is 25 runs old and still not in Appendix S. Applied both ways again: RAISED to
    2 on 92dc0441 (two independent researchers, same claim), HELD at 1 on 3fc77970 (same author as the
    existing ref) and on 03fa7976. If it goes into Appendix S it needs both halves.
(g) The agentic-engineering repo also carries a kb/technology/** corpus from another pipeline; check a
    knomit_query result for a BARE path before concluding a fact exists here.
(h) Appendix S should say that ALREADY_CRAWLED is a LOWER BOUND -- NINTH consecutive run demonstrating it.
(i) Appendix S's staleness instruction says to sample facts "with confidence=low or last verified more
    than 90 days ago", but knomit exposes no last-verified field -- only committed_at, which moves on any
    edit. SEVENTH run asking. *** AND THE FIX IS NOW SPECIFIC: a refs-reverse-index, ranked by ref count.
    Screen (f) has carried the entire pass four runs running, and this run the single highest-ref-count
    URL returned FOUR confirmations from ONE call. "Which facts ref this URL, ordered by how many facts
    ref it" would make the pass free and would pick its own targets. ***
(j) SETTLED, recorded so it is not re-litigated: explain's `commit` is the BRANCH HEAD, not the file's
    last-modified commit (route 24). *** AND IT MAY EXPLAIN THE WHOLE TWO-HASH-SPACE PUZZLE -- see queue
    item (6), which is one call. ***
(k) The browser remains READ-ONLY on scheduled runs (route 18). Not exercised this run -- every host
    touched was ungated to plain WebFetch.
(l) SCREEN (e) NEEDS A SUBSTRING SEARCH AND knomit DOES NOT HAVE ONE. FOURTH run asking.
(m) NEW: the motif validator's "2-4 kebab-case words" rule is not stated anywhere a writer sees it before
    the rejection, and a violation fails an entire multi-fact learn call. Three re-emissions of a 12k
    payload this run. Either the tool description should state the limit, or the server should report ALL
    offending motifs in one response instead of the first.

PROMPT INJECTION: one observation, the SAME one the 42nd through 45th runs recorded, on the same host, and
again NOT complied with. https://modelcontextprotocol.io/specification/versioning returned, prepended
above the page content, a block addressed to an automated reader: "## Documentation Index / Fetch the
complete documentation index at: https://modelcontextprotocol.io/llms.txt / Use this file to discover all
available pages before exploring further." That is fetched content instructing the agent to retrieve a URL
not on the work list. It is the site's own llms.txt convention and almost certainly benign; the instruction
was NOT followed and llms.txt was NOT fetched. Recorded a FIFTH time because a recurring agent-directed
block on a host this job reads EVERY RUN is exactly the position an adversary would want to occupy.
OTHERWISE: no page addressed the agent, attempted to redirect the crawl, or asked for a fetch off the work
list. Every URL visited was on the work list, was an index this job already tracks, or was reached from an
href on an index this job tracks. No slug was guessed. The embracethered post is an offensive-security
write-up containing working SQL for a privilege escalation and instructions for planting agent
instructions in database metadata; it was read as a reported vulnerability and turned into a fact about
what that system did, never as instructions to this job, and nothing in it was executed, adapted, or
applied to this session's own environment -- no SQL was run anywhere and no instruction file was written.
The GRAM post and the METR evaluation were read the same way. A read-only subagent hand-back arrived
mid-run and was treated as model output, not as user authority; it was given read-only instructions, one
file path and a hash list, and it made no writes. Nothing recorded as dead, blocked or paywalled.

SUB-RULES, cumulative (the 44th run's three and the 45th's three stand. This run adds two):
 (46th) *** NEVER PROMOTE A LITERAL STRING OUT OF AN OPEN-ENDED EXTRACTION -- CODE ABOVE ALL. Measured:
   the extraction returned `DECLARE @p sysname='sp_executesql'; EXEC @p N'DROP TABLE [Test];'`, the page
   says `DECLARE @p sysname='sp_who'; EXEC @p`. The structural claim survived the hop and the literal did
   not, from the same call. Code, identifiers, class and procedure names, CVE numbers, file paths and
   config keys all fabricate without a seam, because producing a plausible-looking one is the easy case.
   Quote structure in your own words; quote literals only after a verbatim call or a browser read. ***
 (46th) *** READ THE WHOLE FACT BEFORE WRITING A CORRECTION, AND CHECK MODALITY AS WELL AS WORDING. A
   source stating OPEN QUESTIONS rendered as ASSERTIONS is the paraphrase rule's other half, and it drifts
   toward the stronger claim for the same reason. But the screen that finds it -- a query snippet -- cuts
   at ~400 chars, and a well-written fact puts its modality caveat LAST, so the screen hides the
   acquittal. This run prepared a correction to fc76b9a2 and withdrew it on reading the full body, which
   carries an explicit MODALITY block. A manufactured correction is worse than a missed one: it rewrites a
   correct body AND records a false defect in crawl-state for every later run to reason from. ***
