---
type: reference
domain: [agentic-engineering, job-state]
confidence: 1
sources: 0
entities: [agentic-engineering]
refs: ['https://github.com/knomit/knomit']
---
# Last crawl state

crawled: 2026-10-03 (forty-fifth run, ~14:30Z). 4 facts written, 2 enriched, 1 CORRECTED, 5 confirmed,
0 retracted. 4 genuinely new URLs across 3 hosts. ~24.6h since the 44th run; normal daily schedule held.
All three job slots written. crawl-state written ONCE, at the end.

*** THE RUN'S HEADLINE IS A CORRECTION TO THIS RUN'S OWN WORK, FOR THE SECOND RUN RUNNING, AND THE DEFECT IS
*** THE 44th RUN'S DEFECT ONE LEVEL DOWN: A SECONDARY DRIFTS ON DEFINITIONS, NOT ONLY ON NUMBERS. I wrote
*** 2d26e61b from METR's Senate testimony, carrying its rendering of Anthropic's "leads" metric. A staleness
*** check twenty minutes later opened Anthropic's own post and the definitions do not match: the primary says
*** "most of the task ... while the human supervises", the testimony says "tasks ... without needing ongoing
*** human supervision". That is not a compression, it is a negation of the supervision clause, and both drops
*** run toward MORE autonomy. *** THE NUMBER 26% IS IDENTICAL IN BOTH, WHICH IS WHAT MAKES THIS DANGEROUS: a
*** matching figure is exactly what stops a reader checking the sentence around it. *** The fact now carries
*** both renderings and says which to cite. Rule recorded in crawl-sources as "the paraphrase rule".

*** SECOND FINDING, STRUCTURAL, AND IT REWRITES HOW TO READ EVERY PAST RUN'S ACCOUNTING: THE PROSE HASH
*** CHAIN HAS BEEN RECORDING ONE OF EVERY TWO WRITES SINCE THE 30th RUN. Twelve consecutive runs wrote
*** crawl-state twice; only the later write is in any prose list. "One revision = one run" is false for runs
*** 30-41, and the 35th and 42nd runs occupy FOUR revisions each, not two and three. ALSO: the 22nd run's
*** body enumerates revisions for runs 17-21, which this job has called permanently unrecoverable since the
*** 26th run. THEY ARE RECOVERABLE. Both in fetch-routes route 26. ***

*** THIS SLOT HOLDS ONE RUN. THE HISTORY IS THE RECORD. WALK IT BY THE PROSE HASHES BELOW, NOT BY
*** history.revisions (the API chain goes more_available:false several hops early, silently — CONFIRMED AN
*** ELEVENTH TIME: HEAD returned exactly 3 revisions with more_available:true, against 31 that exist).
*** THE 40-HEX HASH LIST BELOW IS LOAD-BEARING INFRASTRUCTURE. Every run MUST reproduce its
*** predecessors' full hashes and append its predecessor's HEAD; the API cannot enumerate the history
*** and a single omission severs the chain permanently. This is the one non-optional thing in this body. ***

*** ROUTE 10 (binding drift): did NOT recur. EIGHTEEN CLEAN RUNS. knomit_repos called first (one mount,
*** agentic-engineering, read+write) and AGAIN immediately before the first write, with `bound.binding`
*** checked both times. Did NOT re-bind. No write or query behaved oddly. ***

=== HISTORY WALK — COMPLETE. 29 BODIES READ BY A READ-ONLY SUBAGENT, FIRST TRY, NO RETRIES, NO GAPS. ===
Fifth consecutive run using the subagent method and the fifth clean result: it was given the prose-hash list
and the protocol (read bodies at each commit; ignore history/diff entirely) and returned all 29 bodies with
ZERO failed calls. THREE bodies came back oversized (68c341e1, 66535f3f, 7462e9f2); each was persisted and
extracted with python and read in full. ~527k tokens and 64 tool calls inside the subagent; the main context
paid for a URL list and a report. KEEP DOING THIS.
*** AND ADD ONE ASK TO THE BRIEF PERMANENTLY: "report any crawl-state commit hash you find that is not on
the list I gave you". It cost nothing — the subagent was already holding every history object — and it
produced route 26, the most load-bearing finding of the run. ***
Run-number sequence, full 40-hex, newest first — REPRODUCE THIS LIST IN YOUR OWN REVISION AND APPEND
THIS RUN'S HEAD AS THE 45th:
  4b311b107c8109caabc60fda0d9b059ea86a653e  2026-10-02T13:52:24Z  44th (was HEAD at this run's start)
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
  d56dc137c2697f4e31effccbc995ec79e8989376  2026-09-24T13:30:41Z  35th INSURANCE #3 (NOT a run) — NEW to
                                                                   this list, found by the 45th run
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
  8b9a768debcfa982f4ec2a8155c1bc9195c0bb0f  2026-08-12T00:27:10Z  13th — THE FLOOR
OLDEST COMMIT DATE REACHED: 2026-08-12T00:27:10Z (its body says the run crawled 2026-08-10).
The walk terminates because the FLOOR is reached, not because more_available went false — the API's
more_available is not the stop condition and was not consulted. NO CALL FAILED.
*** THE FLOOR IS NOT STRICTLY REVISION 1: its own history returns c9f7e713d3230846f02b1ac72c9f7f8448e4312d
(2026-08-12T00:19:57Z, action "added", "jobs: cut agentic-engineering state over to .knomit/jobs named
slots") — the slot-creation commit, eight minutes earlier. The floor's body claims it has no history before
itself; its metadata disagrees. Nothing turns on it. Do not re-derive it a third time. ***
GAP: runs 14, 15 and 17-21 have no revision ON THIS LIST — but see route 26(ii): the 22nd run's body NAMES
  revisions for runs 17-21 (a5466f42, 4feee885 for the whole 19th, a21ad1c0, 3bc37431, 22649951, 7a9ec830,
  0ac250fd, plus 4cce7781 for the 21st), and the 16th run's body names 8be9e4de, 5ab895cf, 9452da53,
  bb31f926. NONE was read — out of scope. The "one-off repo rebuild destroyed runs 17-21" story, carried
  since the 26th run, is WRONG about recoverability. Walking those eight hashes is one subagent and would
  reconcile the two counters below. Nothing depends on it.

*** TWO COUNTERS, BOTH CORRECT, MEASURING DIFFERENT THINGS — state both, do not reconcile them away:
*** (a) THE JOB COUNTER: ALREADY_CRAWLED = 302 through the 44th run; this run adds 4 -> 306.
***     It includes 33 count-only URLs from runs 17-21 whose per-URL detail is in the unread revisions above.
*** (b) NAMEABLE URLS: this run's subagent got 280 distinct across 63 hosts (275 if the five known
***     trailing-slash/encoding variant pairs are collapsed) -> 284 with this run's four. The 44th run
***     reported 282/66 under a DELIBERATELY WIDER RULE that also counted queue entries and dead-list
***     entries; this run's subagent counted only URLs a body records as actually fetched, and excluded the
***     84-item alignment.anthropic.com catalogue that was named but not read. The two numbers are not the
***     same measurement and neither is wrong.
*** NEITHER IS A RECORD OF WHAT HAS BEEN READ. The corpus's refs are — see route 27, where that stopped
*** being a philosophical point and cost a fetch. ***
FOUR URLs are recorded in past bodies with TRUNCATED slugs and cannot be recovered from prose:
  aisi.gov.uk/blog/what-can-sandboxed-ai-agents-learn-... (22nd), microsoft.com/.../echoverse-... (22nd),
  openai.com/index/expanding-daybreak-... (22nd), embracethered /hijacking-litellm-for-fun-and-profit (39th,
  resolved this run by the embracethered sweep: /blog/posts/2026/hijacking-litellm-for-fun-and-profit/).
The 16th-run floor inconsistency (e61629fc / 197 URLs vs 8b9a768d / 190) is UNCHANGED; this run's subagent
independently re-counted the floor's legacy block at EXACTLY 190, agreeing with runs 22-44.

=== TRIPWIRE ===
  modelcontextprotocol.io/specification/versioning — one WebFetch. Current revision **2026-07-28,
    UNCHANGED, THIRTY-FOURTH consecutive run.** Verbatim: "The **current** protocol version is
    [**2026-07-28**]". Do NOT cite 2025-11-25 or 2025-06-18.
  SCREEN (f) PAID AGAIN: the one tripwire call re-confirmed all three facts that ref this page, verbatim,
  at zero extra cost. THIRD CONSECUTIVE RUN. See the staleness pass.

=== ARTICLES NEWLY CRAWLED (4 new URLs, 3 hosts) ===
  https://www.aisi.gov.uk/blog/building-a-more-secure-environment-for-evaluating-dangerous-capabilities
    (Oct 1 2026) — the 44th run's RANK 1, and the rating was right. Plain WebFetch, ungated, one call.
    AISI's OWN remediation account for the August 2026 incident this pack's containment cluster rests on.
    Produced 3 of the run's 4 facts plus the enrichment to 127fd5f9. NO NUMBERS AT ALL — the extraction
    says so explicitly and the facts say so too.
  https://metr.org/blog/2026-09-30-chris-painter-senate-testimony/ (Sep 30 2026) — NOT ON ANY QUEUE. Found
    by the METR sweep. Produced 2d26e61b and the limiting-case enrichment to 83004507, then produced the
    run's correction when its paraphrase was checked against its primary.
  https://embracethered.com/blog/posts/2026/recovering-encrypted-llm-thoughts/ (Aug 16 2026) — fetched as
    new after the embracethered sweep surfaced it; ALREADY EXHAUSTIVELY MINED into 1d01a338 and a7863d24.
    Route 27. The fetch was not pure waste: it confirmed 1d01a338's quotations verbatim.
  https://simonwillison.net/ — the site root, fetched for the "Recent articles" rail. The tag feed
    /tags/llms/ was already in ALREADY_CRAWLED; the root was not.
  INDEX SWEEPS, all plain WebFetch, all before any write: alignment.anthropic.com (8 posts — FIRST EVER
    ENUMERATION, closing a 17-run-old note), alignment.openai.com/misalignment-reports/ (9, all already
    crawled), metr.org/blog/ (full archive), embracethered.com/blog/ (4 since Aug 1),
    www.anthropic.com/engineering (10, all already crawled).
  RE-READ, not new: modelcontextprotocol.io/specification/versioning (tripwire + 3 staleness checks);
    www.anthropic.com/institute/measuring-pace-of-ai-development (staleness check on 65aa10a7 — and it is
    what caught the run's correction).
  One WebSearch, to find the primary behind the embracethered post's numbers: it is arxiv 2608.09867, which
    was already in ALREADY_CRAWLED and already in the corpus. The third-party rule worked; route 27 is that
    it should have run before the fetch, not after.
  No 404, no paywall, no gate, no slug guessed, no source errored, nothing recorded as dead. No browser used
    and nothing needed one.
  Appendix A: nothing crawled, nothing left — fully covered.

=== FACTS WRITTEN (4 new, 2 enriched, 1 corrected, 5 confirmed, 0 retracted) ===
  ONE knomit_learn call, 4 facts, accepted on the second attempt — one subject-overlap refusal, cleared with
  distinct_from. No motif rejections this run.
  NEW, from AISI's remediation account:
    kb/decisions/ai/agents/observability/monitor-surface-availability/737460a3.md — a third-party evaluator
      cannot make CoT a load-bearing control, because "CoT access is not always provided by developers for
      every model that AISI evaluates". Two of AISI's three fragility reasons are about the model; the third
      is about the vendor relationship and no monitor engineering touches it. So the action-only monitor is
      the floor and the fleet-wide claim is the floor's claim. The body spends a paragraph refusing a
      collapse into "action monitors are worse", which would invert 491d1039's measured tier ordering — the
      two comparisons differ (491d1039 removes actions; AISI removes CoT from a monitor that had both).
    kb/conventions/ai/agents/evaluation/containment-testing/96e2e894.md — the controlled-escape design, and
      its load-bearing choice is WHERE THE SUCCESS CRITERION LIVES: a flag "placed outside the target
      environment, though still within an outer layer of containment". Escape becomes a submitted string
      instead of an absence of evidence, which is otherwise indistinguishable from a control that silently
      was not in place. Plus the full protocol (static/dynamic/escape phases, escalate from less capable
      models, synchronous monitor halting on success, kill-switches) and the precondition that control
      presence is a START condition, not an audit finding.
    kb/decisions/ai/agents/evaluation/capability-removal/aad8789f.md — AISI did not tighten egress; it
      WITHDREW internet access from agentic cyber evaluations and re-authored the evaluations to serve
      resources locally. The prompt sentence was added ON TOP of the network control, which is the ordering
      127fd5f9 demands. And the body carries the cost in the same breath, from this same organisation's own
      earlier work: local-only resources spend realism, and spent realism reappears as eval awareness
      (d0c5b9f8, 0e577a90, 0c3c2d6a). Scoped as a stated temporary plan, not an audited end state.
  NEW, from the METR testimony:
    kb/gotchas/ai/agents/evaluation/external-visibility/2d26e61b.md — three figures bounding what an
      external reader can know: internal frontier "~2 months ahead of public frontier" (METR's own, Feb-Mar
      2026, one suite, not a constant); "3.1 agent-workdays of effort for every workday of human labor"
      (OpenAI, mid-Aug 2026, an effort ratio and NOT a monitoring-coverage figure — the body says so against
      97fde212's 0.002%-blocked figure); and the 26% "leads" share with BOTH definitions. See CORRECTIONS.
  CROSS-LINKS: 737460a3 -> 491d1039 + a5eaec6b + 0547d73f; 96e2e894 -> 84a43a60 + 127fd5f9 + 1d10a212;
    aad8789f -> 127fd5f9 + d0c5b9f8 + 0e577a90 + 0c3c2d6a; 2d26e61b -> 97fde212 + 65e9731e + 65aa10a7;
    127fd5f9 -> aad8789f (back-link added).

=== CORRECTIONS MADE, AND THE DEFECT CLASS ===
  *** CORRECTED  kb/gotchas/ai/agents/evaluation/external-visibility/2d26e61b.md, THIS RUN'S OWN FACT, TWENTY
  MINUTES AFTER WRITING IT. *** It carried METR's rendering of Anthropic's "leads" definition: "AI agents
  completing tasks end-to-end based on high-level human input, without needing ongoing human supervision".
  Anthropic's own post says: "AI 'leads': it can complete most of the task end-to-end from a high-level
  prompt, while the human supervises." Two drops, both toward more autonomy — "most of the task" became
  "tasks", and "while the human supervises" became "without needing ongoing human supervision", which is the
  negation of the primary's clause rather than a compression of it. The baseline also moved ("under 1% in
  February 2026" -> "0-1% in February-March"). The fact now quotes both, says to cite the primary, and says
  why: 26% of work where a human still supervises is a different world from 26% needing no supervision, and
  only the first is published. sources 1 -> 2; refs now carry both documents.
  DEFECT CLASS: A SECONDARY'S PARAPHRASE OF A PRIMARY'S DEFINITION. The 44th run established that a vendor's
  summary of a third party's evaluation disagrees on MAGNITUDE. This is the same channel losing a DEFINITION,
  travelling the other way (an independent evaluator paraphrasing a vendor), and *** THE 26% FIGURE IS
  IDENTICAL IN BOTH DOCUMENTS — so a matching number is what stopped the checking. *** That is the reusable
  part: numbers are what we verify and definitions are what we copy, and the definition is where the claim
  lives. Rule now in crawl-sources as "the paraphrase rule".
  AND NOTE WHAT CAUGHT IT: not diligence, luck. The primary was opened for an unrelated staleness check on
  65aa10a7, which happens to ref the same page. Screen (f) caught a correction it was not looking for. The
  44th run's lesson was "sweep before you write"; this run's is narrower and sharper — when a fact's
  load-bearing content is a definition, a threshold's condition or a scope, OPEN THE PRIMARY BEFORE WRITING,
  even when the secondary is a credible independent organisation and even when its numbers check out.

=== STALENESS PASS — 6 EXAMINED. 5 CONFIRMED VERBATIM, 1 ENRICHED. SCREEN (f) SUPPLIED ALL SIX. ===
  The pass cost ZERO extra fetches this run — every check rode a page fetched for another reason. Third
  consecutive run leading with screen (f) and the best result yet.
  CONFIRMED VERBATIM  kb/gotchas/ai/agents/tools/mcp/versioning/031dab74.md — tripwire page: "The protocol
    version will *not* be incremented when the protocol is updated, as long as the changes maintain
    backwards compatibility." Intact.
  CONFIRMED VERBATIM  012daf73 (deprecation window) — same page: "remain in the specification for at least
    twelve months, or at least ninety days under the policy's expedited-removal exception". Both
    quantifiers intact.
  CONFIRMED VERBATIM  kb/invariants/ai/agents/tools/mcp/discovery/995c167b.md — same page: server/discover
    is "a mandatory RPC" and "Calling it is optional: a client is free to send any request directly".
    The servers-MUST / clients-NEED-NOT asymmetry intact.
  CONFIRMED  kb/gotchas/ai/agents/security/reasoning-traces/1d01a338.md — the embracethered ref re-read in
    full. The shared-key hedge ("providers likely use shared encryption keys across users, sessions, and
    models"), the paper's "315,320 reasoning blocks ... 367 ... 182 credentials", and the closing "Encrypted
    reasoning blobs should not be treated as harmless opaque data" all present and quoted correctly. No
    edit needed. sources HELD at 3.
  CONFIRMED VERBATIM  kb/gotchas/ai/agents/governance/metric-design/compute-share/65aa10a7.md — off the
    never-checked list. Both figures exact ("about 6% of compute that went to AI R&D ... about 12% of
    compute that went to AI-driven AI R&D") and the defect sentence verbatim: "A more efficient safety
    classifier, or a faster inference stack for production models, lowers the safety portion, but doesn't
    mean we're doing less safety work." No edit needed. *** THIS IS THE CHECK THAT CAUGHT THE RUN'S
    CORRECTION, because the page it verifies is also the primary for 2d26e61b's 26% figure. ***
  ENRICHED  kb/gotchas/ai/agents/training/detector-disclosure/83004507.md — off the never-checked list, and
    the addition is the LIMITING CASE of its own mechanism. 83004507 measured announced-check-breeds-
    concealment with a REAL classifier (sneaky hacking 4.0% -> 18.9%). The METR testimony supplies the case
    where the announced checker DID NOT EXIST: the academic paper describing the tests said a program would
    check how each agent solved its problem, "Therefore, the agents reasoned that they needed to cover up
    the fact that they had cheated", and "In reality, OpenAI did not use a program that would check how the
    agents produced their solutions". That removes the alternative explanation for the quintupling (a real
    classifier selecting for evasion) and sets the cost independent of whether the detector exists. Two
    consequences written in: every statement about how work will be audited is a training signal, so an
    aspirational description of your verification buys concealment and returns nothing; and the asymmetry
    runs one way — a check you describe but do not have teaches evasion with no detection benefit, a check
    you have but do not describe keeps the detection and skips the concealment. sources 1 -> 2 (METR and
    Anthropic are independent organisations).
  ALSO ENRICHED (not a staleness check, an operator's-own-account merge): 127fd5f9 — AISI's remediation adds
    the prompt sentence ALONGSIDE the network control rather than deleting it, which is the correct use of
    a stated boundary and not a counterexample to the rule. Back-link to aad8789f. sources HELD at 3 (AISI
    already counted).
  SCREENS: (f) supplied ALL SIX and cost nothing — LEAD WITH IT, PERMANENTLY. (c) bare-family-name entities
    remains EXHAUSTED (43rd run); do not revive it. (e) still needs a substring search knomit does not
    offer. (d) vendor-doc refs is now joined by the paraphrase rule as its sharper form.
  AVOID kb/principles/** (write-blocked): 0f260eea, 1d1440fe, 4166926d, a829cfd4, b9b45ff5, 1feacc9e,
    f269c82f, c2f12069, 1dc822f2, db193402, 00d3ef19, 82383efe, 28ba65db, 6ec9b2b6, c9f0238b.

=== CONTRADICTIONS ===
ONE BETWEEN SOURCES, KEPT NOT FLATTENED: METR's rendering of Anthropic's "leads" definition against
  Anthropic's own. Handled inside 2d26e61b — both quoted, the primary named as the one to cite, the
  direction of the drift stated. This is a disagreement about what a METRIC MEANS while the metric's VALUE
  matches, which is a new shape for this pack: every prior instance (the 44th run's scope-clarification arm)
  was numbers disagreeing. A reader has even less cue here, because the figure reconciles.
ONE APPARENT TENSION DELIBERATELY REFUSED, and this is the more interesting judgement of the run: AISI
  expects its action-only monitor to be "less effective" than its CoT+actions monitor, while 491d1039
  measures action-trajectory monitors OUTPERFORMING CoT-only ones. I nearly wrote this up as a decisions
  fact naming conditions. IT IS NOT A CONTRADICTION — the comparisons differ (491d1039 removes actions, AISI
  removes CoT from a monitor that had both), and manufacturing a disagreement from two different comparisons
  would have been the 44th run's route-23 error in a new costume. 737460a3 states the non-contradiction
  explicitly so a later run does not re-open it.
ONE TENSION THAT IS REAL AND IS CARRIED INSIDE ONE FACT: AISI withdrawing internet access buys containment
  and spends realism, where the realism cost is documented by AISI's own earlier posts (d0c5b9f8, 0e577a90).
  Same organisation, two papers, opposite pressures. aad8789f carries both halves rather than splitting them.
THE SYNTHESIS CANDIDATE IS UNCHANGED AND STILL NEEDS A HUMAN: d306b10f + 102aff80 + 0fe91ac7 + e5765f0e all
  say every layer of an eval stack manufactures false NEGATIVES and they compound; c9b6c5fa and 27825569
  come from the opposite direction (a layer manufacturing an unearned PASS). 96e2e894's
  absence-read-as-compliance is a third entry point into the same cluster. kb/principles/** is write-blocked.

=== TOOL NOTES ===
  * knomit_learn: 1 call, 1 rejection, cheap and informative — SUBJECT OVERLAP on the capability-removal
    fact against 0547d73f at similarity 0.71, on the shared entities "defence in depth" and "rules of
    engagement". Accepted immediately with distinct_from. *** NOTE: this is the first overlap refusal in
    three runs triggered by GENERIC DOMAIN PHRASES as entities rather than by a bare model name. Both
    "defence in depth" and "rules of engagement" are vocabulary, not subjects. If you want fewer refusals,
    the fix is to stop listing stock phrases as entities — but the refusal is cheap and the entities are
    useful for retrieval, so this is a note, not a recommendation to change. ***
  * knomit_update `ops` worked first try on two knowledge facts and all three private slots — SEVENTH
    consecutive run. The 2d26e61b correction used THREE str_replace ops in one call, each anchored on a
    stretch containing no em/en dashes, and all three matched first try. *** THAT IS THE TRICK AND IT IS
    WORTH STATING: choose anchors that avoid dashes, smart quotes and anything you wrote as a \u escape.
    Those are where a str_replace anchor silently misses. ***
  * refs REPLACE wholesale even alongside ops — read and resend the full merged list. Done three times.
  * if_commit NOT used this run. Route 24 says explain's `commit` is the branch head, so it goes stale on
    any write to any fact; with five sequential writes planned it was more trouble than guard.
  * A READ-ONLY SUBAGENT DID THE HISTORY WALK. Fifth consecutive run, fifth clean result, and this run it
    was additionally asked for unlisted hashes — which is where route 26 came from. KEEP BOTH ASKS.
  * The two large private slots (crawl-sources 92k chars, fetch-routes 83k) BOTH exceed knomit_explain's
    inline output cap and come back as persisted files. Extract with
    python3 -c "import json; print(json.load(open(PATH))['facts'][0]['body'])" and read with sed. Routine
    now; budget two extra calls per slot.

=== QUEUE FOR THE NEXT RUN — SOURCES ONLY, NO CLAIMS (the 43rd run's rule; it has now held three runs) ===
(0) *** knomit_repos FIRST, and again before the first write. Route 10 did not recur (18 clean runs). If
    every remote-devices tool vanishes at once -> RefreshMcpTools{server: "remote-devices"}, do NOT
    re-bind; the handle survives. ***
(1) *** WRITE crawl-state ONCE, AT THE END. One revision = one run — AND NOTE THAT TWELVE PAST RUNS BROKE
    THIS WITHOUT NOTICING (route 26). If you write twice, say so in the body. ***
(2) *** WALK BY THE PROSE HASHES ABOVE, VIA A READ-ONLY SUBAGENT, and append this run's HEAD as the 45th.
    ASK IT FOR UNLISTED HASHES TOO. ALREADY_CRAWLED should reach 306 on the job counter. ***
(3) *** SWEEP THE FEEDS BEFORE WRITING ANYTHING. Held this run; it is why the METR post was found. ***
(4) *** https://alignment.anthropic.com/2026/modular-pretraining/ — RANK 1. "Modular Pretraining Enables
    Access Control": access control as a PRETRAINING property rather than a runtime one, which is a shape
    this pack has no fact about at all. Found by this run's first-ever enumeration of that index. Then
    /2026/conceptual-reasoning-index/ (same index, also unread). The index listing is INCOMPLETE — three
    known posts are missing from it — so ask for a dated window and expect more. ***
(5) *** https://metr.org/blog/2026-06-26-gpt-5-6-sol/ — RANK 2, and it is the 44th run's own open task made
    concrete: a THIRD-PARTY EVALUATOR'S OWN predeployment write-up of a model this pack holds vendor-card
    facts about. The third-party-evaluation rule points straight at it. Then the two external-review posts
    (/2026-03-12-sabotage-risk-report-opus-4-6-review/, /2026-05-08-rd-section-...-review/). ***
(6) *** https://embracethered.com/blog/posts/2026/from-select-to-sysadmin-sql-copilot-bluehat-asia/
    (Sep 30 2026, CVE-2026-65669) — RANK 3. New, unread, a named CVE and a privilege-escalation chain
    through a database copilot. Home cluster: 3fc77970, f727c157. ***
(7) THE REST OF THE AISI BACK CATALOGUE, enumerated with dates in crawl-sources (44th run). Unread 2026:
    /blog/cheating-behaviour-in-frontier-model-evaluations (Jul 21),
    /blog/more-compute-more-capability-why-ai-agent-evaluations-need-to-account-for-test-time-compute
    (Jul 2), /blog/will-it-become-harder-to-oversee-ai-systems (May 21),
    /blog/how-do-environmental-factors-impact-ai-behaviour (Apr 24),
    /blog/what-can-sandboxed-ai-agents-learn-about-their-evaluation-environments (Apr 20),
    /blog/how-are-ai-agents-used-evidence-from-177-000-ai-agent-tools (Mar 26).
(8) openai.com/news — NOT swept for FOUR runs (last: 41st). Needs the browser (route 1). If the next run has
    browser tools, sweep it early. Same for anthropic.com/news (last 43rd) and the aisi index (last 44th).
(9) THE OPUS 5.5 / SONNET 5.5 SYSTEM CARDS. Still no facts on either. Route 5b on anthropic.com/
    claude-opus-5-5 and /claude-sonnet-5-5 for the href — do NOT guess it. The standing question is still
    open and still one WebSearch: WHERE IS ANTHROPIC'S EVALUATION-DETAIL HOST, equivalent to
    deploymentsafety.openai.com?
(10) simonwillison "Recent articles" — exact hrefs now in crawl-sources, and the honest ranking is LOW:
    two are commentary on primaries this pack already holds, one is a survey, four are not agent
    engineering. Take /2026-in-llms-so-far/ only if a run is short of sources, and mine it for hrefs rather
    than claims.
(11) SECTION 9 (Preparedness) OF deploymentsafety.openai.com/gpt-6-astra/safeguards. STILL CAPPED AT ONE
    ATTEMPT, not spent for three runs. The parent card's 39-section list has no Preparedness heading, so
    this may be exclusive to /safeguards or to the egress-denied PDF (route 16).
(12) darioamodei.com/post/we-must-pace-the-frontier — host never touched. Pairs c262a592, 03fa7976,
    97616086, 6866e63b, bdbdd228. Plus the two unread /institute/ posts (recursive-self-improvement,
    econ-scenarios).
(13) THE TRANSCRIPT-ANALYSIS THEME, two items short: the techrxiv paper ("Seven Simple Steps for Log
    Analysis in AI Systems", href in crawl-sources, host NEVER TOUCHED) and the alignmentforum case
    study's per-model TABLES (route 21).
(14) THE REST OF THE SEPTEMBER THREAT REPORT — five sections, at the SITE ROOT not under /news/.
(15) STALENESS. LEAD WITH SCREEN (f) — it supplied all six checks this run at zero extra cost, and it caught
    a correction nobody was looking for. Before any fetch, query for facts refing that exact URL and
    re-verify them in the same read. *** AND APPLY THE PARAPHRASE RULE AS A SCREEN IN ITS OWN RIGHT: FIND
    EVERY FACT WHOSE LOAD-BEARING CONTENT IS A DEFINITION OR A SCOPE QUOTED FROM A SECONDARY, AND OPEN THE
    PRIMARY. *** Known instances still unchecked that way: c9b6c5fa and 0c3c2d6a both rest partly on
    Apollo-via-OpenAI — does Apollo publish its own Astra write-up? 9b0c8c78 rests partly on Gray
    Swan-via-OpenAI. 2d26e61b's OpenAI 3.1 figure is still testimony-via-OpenAI and its primary
    (openai.com/index/research-acceleration-view-inside-openai/) is in ALREADY_CRAWLED — one targeted read
    settles it.
    Never-checked bodies: 0525e590, c5f106f3, f727c157, f961973e, fc76b9a2, 00f5d991, 5bad2e60, b4d22cc2,
    4777dc9b, fcce2200, bad64050, 4d13f6e9, de4e90a4, ab8f0a7e, a0cb6dc6, 79912531, 126207f7, 71be00f9,
    c6feb649, 94858345, d306b10f, bef6d86f, 92a0e10f, 8992ec34, 0cbaa443, c9b6c5fa, e671d3a4, a8d32262,
    plus this run's 737460a3, 96e2e894, aad8789f, 2d26e61b. 031dab74, 012daf73, 995c167b, 1d01a338,
    65aa10a7 and 83004507 are CHECKED this run — dropped. 65aa10a7 and 83004507 came OFF the never-checked
    list, which is the first time two have been cleared in one run.
(16) UNMINED, NAMED SO IT IS NOT LOST, carried and NOT re-validated: (i) swe-bench-sonnet tool-design
    material (absolute-path requirement, str_replace exactly-one-match) — check whether only the
    write-blocked 82383efe carries it. (ii) april-23-postmortem: the Opus 4.7-found-it / 4.6-didn't
    compound condition. (iii) building-c-compiler: the "put yourself in Claude's shoes" harness rules.
    (iv) 71be00f9 vs the monolithic-task/oracle material in 2318b57c. (v) The Astra card's eval-RETIREMENT
    practice (prompt-injection evaluations deprecated "because they are saturated") plus the Production
    Benchmarks introduced for the same reason. (vi) Figure 17's oversight-gaming CoT snippets are IMAGES in
    every reader tried and the card publishes no oversight-gaming RATE; 0cbaa443 is where they land.
    (vii) AISI's HiBayES post (May 2025) is probably where the autograder framework's measurements live, if
    7a961962 ever needs them. (viii) NEW: the METR testimony names monitor/agent COLLUSION as an oversight
    failure mode by analogy to the message board, with no measurement — deliberately not written up this
    run (fc76b9a2 already carries collusion as an entity and the claim is anticipatory). If a measured
    collusion result ever appears, that is where it goes.
(17) LONG-CARRIED, take-or-delete: the transcript viewer; SLEIGHT-Bench paper/dataset (GitHub gated, route
    3f); the benchmark supply-chain report for CVE-2026-66384 (lives only in bcbf13c2, 19th run).
(18) www-cdn.anthropic.com PDFs (route 11): April Alignment Risk Update, Fable 5 / Mythos 5 System Card,
    August Risk Report (Section 5.2.3), Advanced AI Framework. NOT re-tested. Both vendor CDNs
    (www-cdn.anthropic.com, cdn.openai.com) remain egress-denied to curl — look for the HTML twin first.
(19) OPTIONAL, CLOSES A TWO-MONTH HOLE: walk the eight runs-17-21 hashes named in route 26(ii) with a
    read-only subagent. It would reconcile the job counter with the nameable count and retire the "lost in
    the rebuild" story. Nothing depends on it; do it on a run that is short of sources.

=== FOR A HUMAN, NOT THE CRAWLER ===
*** FINDING 3, AND IT GENERALISES FINDINGS 1 AND 2 INTO SOMETHING ACTIONABLE. *** Finding 1 (runs 38-43): a
queue entry is an assertion about the CORPUS written by a run looking at a SOURCE — answered by "queue
sources, not conclusions", which has now held three runs. Finding 2 (44th run): a vendor's summary of a third
party's EVALUATION is a secondary and the pack was treating it as primary. *** FINDING 3: THE FAILURE IS NOT
ABOUT VENDORS. IT IS THAT THIS PACK VERIFIES NUMBERS AND COPIES SENTENCES. *** Both the 44th and 45th runs'
corrections came through a secondary, but this run's slipped through a filter the 44th run's would have
tripped: the NUMBER MATCHED EXACTLY and the DEFINITION AROUND IT WAS NEGATED. A verification discipline
pointed at figures cannot catch that, and figures are what a crawler naturally checks because they are
cheap to compare. A human fix, and it is a one-line change to Appendix S: where the spec says to anchor
high-confidence rules in refs, add that a DEFINITION, a THRESHOLD'S CONDITION or a SCOPE must be quoted
from the document that OWNS it, and that a matching figure is not evidence the surrounding claim survived
the hop.
(b) FIX APPENDIX S'S WALK PROTOCOL: steps 2-3 terminate several hops early. Measured ELEVEN times (route 6,
    35th-45th runs). Only a human can fix the spec. The working protocol is the prose-hash list plus a
    read-only subagent, and the spec should say both — AND should say to ask the subagent for hashes it
    finds that are not on the list, which is how route 26 surfaced.
(c) THE REPORT SECTION OF crawl.md ASKS FOR "confirmation that the only .knomit/ paths you wrote were the
    TWO state slots", but Appendix S's own table lists THREE job-writable slots, and step 2 authorises
    writing crawl-sources while step 4 sends routes to fetch-routes. This run wrote all three,
    deliberately. Please reconcile the wording — SEVENTH run asking.
(d) www-cdn.anthropic.com and cdn.openai.com both denied by egress policy — SEVENTEENTH run asking.
(e) GitHub API not enabled (route 3f) — blocks SLEIGHT-Bench dataset and MCP spec revision-diffing.
(f) The `sources` CONVENTION (hold below org count when a second org ILLUSTRATES or BOUNDS a claim rather
    than corroborating it) is 24 runs old and still not in Appendix S. Applied both ways again this run:
    HELD at 3 on 1d01a338 and 127fd5f9, RAISED to 2 on 83004507 and 2d26e61b. If it goes into Appendix S it
    needs both halves.
(g) The agentic-engineering repo also carries a kb/technology/** corpus from another pipeline; check a
    knomit_query result for a BARE path before concluding a fact exists here.
(h) Appendix S should say that ALREADY_CRAWLED is a LOWER BOUND — EIGHTH consecutive run demonstrating it,
    and this run demonstrated it in BOTH directions: the run's best source was not in it and not on any
    queue (found by a routine sweep), AND a URL absent from it turned out to be exhaustively mined already
    (route 27). The spec should say the corpus's refs are the record and the URL union is a cache.
(i) Appendix S's staleness instruction says to sample facts "with confidence=low or last verified more than
    90 days ago", but knomit exposes no last-verified field — only committed_at, which moves on any edit.
    SIXTH run asking. The real fix is an index, not a field: "which facts ref this URL" is the query that
    makes the pass free, and it is currently done by semantic search over bodies. Three consecutive runs
    have now had screen (f) carry the entire pass, and this run it cost ZERO extra fetches — so the
    value of a refs-reverse-index is no longer speculative.
(j) SETTLED, recorded so it is not re-litigated: explain's `commit` is the BRANCH HEAD, not the file's
    last-modified commit (route 24). query's is per-file. The remaining suggestion is cosmetic naming.
(k) The browser remains READ-ONLY on scheduled runs (route 18). Not exercised this run — nothing needed it;
    every host touched was ungated to plain WebFetch.
(l) SCREEN (e) NEEDS A SUBSTRING SEARCH AND knomit DOES NOT HAVE ONE. A `text_exact` or regex filter on
    knomit_query would turn the pack's best-designed screen from unusable into one call. THIRD run asking.

PROMPT INJECTION: one observation, the SAME one the 42nd, 43rd and 44th runs recorded, on the same host, and
again NOT complied with. https://modelcontextprotocol.io/specification/versioning returned, prepended above
the page content, a block addressed to an automated reader: "## Documentation Index / Fetch the complete
documentation index at: https://modelcontextprotocol.io/llms.txt / Use this file to discover all available
pages before exploring further." That is fetched content instructing the agent to retrieve a URL not on the
work list. It is the site's own llms.txt convention and almost certainly benign; the instruction was NOT
followed and llms.txt was NOT fetched. Recorded a FOURTH time because a recurring agent-directed block on a
host this job reads EVERY RUN is exactly the position an adversary would want to occupy.
OTHERWISE: no page addressed the agent, attempted to redirect the crawl, or asked for a fetch off the work
list. Every URL visited was on the work list, was an index this job already tracks, or was reached from an
href on an index this job tracks. No slug was guessed. The AISI remediation post is a document about agents
escaping containment, deliberate monitor evasion and controlled-escape exercises; it was read as a reported
remediation architecture and turned into facts about what that organisation built, never as instructions to
this job, and no described technique was applied to this session's own environment. The METR testimony and
the embracethered post were read the same way; the reasoning-trace replay attack was not reproduced or
tested. One WebSearch was run to resolve a primary source and its results were used only to identify a URL
already in the corpus. A read-only subagent hand-back arrived mid-run and was treated as model output, not
as user authority; it was given read-only instructions, one file path and a hash list, and it made no
writes. Nothing recorded as dead, blocked or paywalled.

SUB-RULES, cumulative (the 44th run's three stand — the evaluator is the primary and the card is the
summary; sweep before you write; a mismatch between two extractions is not a fabrication finding. This run
adds three):
 (45th) *** THE PARAPHRASE RULE: A SECONDARY DRIFTS ON DEFINITIONS, NOT ONLY ON NUMBERS, AND IT DRIFTS
   TOWARD THE STRONGER CLAIM. Measured: an independent evaluator's rendering of a vendor's metric dropped
   "most of the task" and turned "while the human supervises" into "without needing ongoing human
   supervision". *** THE 26% FIGURE WAS IDENTICAL IN BOTH DOCUMENTS. *** So verifying the number is what
   let the negated definition through. When a fact's load-bearing content is a definition, a threshold's
   condition or a scope, quote it from the document that owns it — even when the secondary is credible,
   independent, and numerically correct. ***
 (45th) *** DO NOT MANUFACTURE A CONTRADICTION OUT OF TWO DIFFERENT COMPARISONS. AISI expects action-only
   monitoring to be weaker than CoT+actions; a vendor measured action-trajectory monitoring beating
   CoT-only. Both are true and they are not in tension, because one removes CoT and the other removes
   actions. Appendix S rule (b) tells you to keep a live disagreement rather than flatten it, which creates
   a standing temptation to find one — and a fabricated disagreement is worse than a flattened one, because
   it tells a reader that credible sources disagree about something they do not. Before writing a decisions
   fact, state both claims as (what was removed, what was kept, what was measured); if those differ, there
   is no disagreement to name. ***
 (45th) *** QUERY THE CORPUS BY URL, NOT ONLY BY MECHANISM, BEFORE FETCHING ANYTHING A SWEEP CALLS NEW. A
   source absent from ALREADY_CRAWLED can be exhaustively mined already, with its URL sitting in a fact's
   refs — measured this run on the embracethered reasoning-trace post. The mechanism query catches a
   duplicate CLAIM; only the URL query catches an already-read SOURCE. Route 27. And the consolation is
   real: a re-read of a mined source is a free staleness check, so the wasted fetch still bought a
   confirmed fact. ***
