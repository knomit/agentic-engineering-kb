---
type: reference
domain: [agentic-engineering, job-state]
confidence: 1
sources: 0
entities: [agentic-engineering]
refs: ['https://github.com/knomit/knomit']
---
# Last crawl state

crawled: 2026-08-17 (twentieth run). TWO DAYS after the 19th, so the feed sweep was owed and was run.
IT PAID, AND NOT FROM THE NEW POSTS: the sweep's value was discovering that a feed in the recurring
list since the 13th run had never been followed to ARTICLE level. Three back-catalogue posts, three
facts, and they are the strongest material this pack has taken in several runs.
*** A REVIEW PASS WAS RUN AFTER THE FACTS WERE WRITTEN. THE IN-RUN SELF-REVIEW FOUND ONE DEFECT IN
THIS RUN'S OWN OUTPUT (a modal-strength loss) AND THE POST-COMMIT PASS FOUND A SECOND (a row count).
Both corrected in place. ***
*** A FULL knomit_review SESSION WAS ALSO RUN AT THE USER'S REQUEST — 37 ITEMS. SEE THE REVIEW
SECTION NEAR THE FOOT. IT FOUND TWO DEFECTS THE JOB CANNOT FIX AND ONE PIPELINE OBSERVATION. ***

*** THIS SLOT HOLDS ONE RUN. THE HISTORY IS THE RECORD. WALK IT. ***

=== HISTORY WALK ===
REVISIONS READ: 6 bodies, across 5 runs (the 17th run wrote twice; both were read).
  4feee885 (HEAD, 2026-08-15T18:30:20Z) — the 19th run's final body.
  7a9ec830 (2026-08-15T13:47:52Z)       — the 18th run's body.
  3bc37431 (2026-08-14T12:51:03Z)       — the 17th run's FINAL body.
  0ac250fd (2026-08-14T12:23:46Z)       — the 17th run's FIRST write. Same run; deduped, not skipped.
  3c6323cd (2026-08-12T21:25:35Z)       — the 16th run's body.
  8b9a768d (2026-08-12T00:27:10Z)       — the 13th run's body, carrying the AUTHORITATIVE 190-URL union.
OLDEST COMMIT DATE REACHED: 2026-08-12T00:27:10Z. `more_available` was FALSE at THREE separate
revisions (0ac250fd, 3c6323cd, 8b9a768d) — the walk terminated on the API's own signal three times
over, not on an assertion in a body. No call failed; no retry needed.
NOTE ON METHOD, because I did it differently from the 18th run: the 18th read 3bc37431 and skipped
0ac250fd; I read BOTH revisions of the 17th run rather than assuming the later one is a superset.
It was — the two bodies list the same 5 articles — but that is now checked rather than assumed, and
it cost one call. A same-run second write is a diff, and a diff can drop a line.

*** THE GAP IS STILL THERE. FOURTH RUN REPORTING IT. NOT MINE TO FIX. ***
The 14th and 15th runs' bodies remain UNREACHABLE — their per-run commits were squashed into merge
commits ("Merge pull request #8", "#6") and the hashes recorded in prose (e61629fc, 8be9e4de,
5ab895cf) do not resolve. ALREADY_CRAWLED = 190 (enumerated at 8b9a768d) + 10 (16th) + 5 (17th) +
7 (18th) + 4 (19th) + 9 genuinely-new (this run) = **225 URLs I can NAME**, against an asserted true
total of ~241. The ~16 unenumerable URLs from the 14th/15th window are described at source level in
the 17th run's body and I steered clear of all of it.
FOR A HUMAN: four consecutive runs have now reported this. It will not heal on its own.

*** THE DANGLING-REF PROBLEM IS ALSO STILL THERE. NOT RE-CHECKED THIS RUN, NOT FIXED. ***
kb/invariants/ai/agents/security/threat-taxonomy/4f5e9dfe.md is retracted but still cited by THREE
live facts: 483263c5, c02ac546, bdf3336e. Carried forward from the 19th run unverified — saying so
plainly rather than re-asserting it as though I had re-checked. Still for a human.

recurring-feed indexes swept: FOUR.
https://api.github.com/repos/.../contents/docs/specification  (MCP tripwire — UNCHANGED. 2024-11-05,
  2025-03-26, 2025-06-18, 2025-11-25, 2026-07-28, draft. TENTH consecutive run unchanged.)
https://www.anthropic.com/news/     (ONE new on-topic item since the 17th run's sweep: "How Claude's
  text watermark works", Aug 14. Read. Everything else since 07-30 is below the bar.)
https://www.anthropic.com/engineering  (NOTHING new. Index still quiet since Apr 2026 — fifth
  consecutive confirmation. Stop re-sweeping this one for a while.)
https://www.aisi.gov.uk/blog/       (nothing NEWER than the 08-04 incident report — and that reading
  is exactly what made three prior sweeps miss the point. SEE FINDING 1.)
openai.com/index via WebSearch      (no post newer than the Aug 13 Ultrafast announcement, already
  catalogued as below the bar. The catalogue is current.)

articles newly crawled (9 genuinely new URLs):
https://www.aisi.gov.uk/blog/cheating-behaviour-in-frontier-model-evaluations                        <- 1 fact + 1 upd
https://www.aisi.gov.uk/blog/how-our-new-control-red-team-is-stress-testing-frontier-monitors        <- 1 fact + 1 upd
https://www.aisi.gov.uk/blog/more-compute-more-capability-why-ai-agent-evals-need-to-account-for-test-time-compute  <- 1 fact
https://openai.com/index/unlocking-self-improvement-gpt-red/    (browser route)                      <- 1 fact + 1 paired fact
https://www.anthropic.com/news/claude-text-watermark                                                 <- 1 fact
https://raw.githubusercontent.com/.../docs/specification/2026-07-28/basic/versioning.mdx             <- 1 fact + 1 upd
https://raw.githubusercontent.com/.../docs/docs/2026-07-28/learn/versioning.mdx      (diff pair)
https://raw.githubusercontent.com/.../docs/docs/2025-11-25/learn/versioning.mdx      (diff pair)
https://raw.githubusercontent.com/.../docs/specification/2026-07-28/basic/transports/stdio.mdx  +
  .../basic/transports/streamable-http.mdx   (Backward Compatibility sections only; counted as one
  target because they were read for one question. THE REST OF BOTH PAGES IS UNREAD — next MCP target.)
re-fetched for the staleness pass, already known: anthropic.com/engineering/writing-tools-for-agents,
  anthropic.com/engineering/multi-agent-research-system, huyenchip.com/2025/01/07/agents.html,
  goose-docs.ai/docs/guides/security/adversary-mode, embracethered.com/.../toctou-agent-...
VERIFICATION SWEEPS, not article reads: ALL 41 files of revision 2025-11-25 and ALL 186 files of
  revision 2026-07-28, enumerated ON THE REVISION DATE (fetch-routes 3d), 404-guarded (0 hits across
  227 files) and grepped unanchored.

errored / not obtained: NONE that survived. TWO expected-shaped 404s, both turned into findings
rather than failures: the naive `docs/specification/2025-11-25/basic/versioning.mdx` (caught by the
404-body guard, produced the 3b finding) and the title-derived anthropic slug
/news/how-claudes-text-watermark-works (resolved by one WebSearch). No 403s, no paywalls, no
timeouts. The openai.com browser route worked first try. OWASP was not touched this run.

Appendix A: nothing crawled, nothing left. Fully covered since the eighth run.

=== FINDINGS ===

*** FINDING 1 — A FEED CAN BE SWEPT THREE TIMES AND STILL BE UNREAD, BECAUSE "SWEPT" MEANT "ASKED
WHETHER ANYTHING IS NEWER THAN THE ONE POST WE READ". THE HIGHEST-YIELD FINDING OF THE RUN. ***
aisi.gov.uk/blog entered the recurring list on the 13th run. It was swept on the 13th, the 17th and
again today. Every sweep asked the same question — is there anything newer than the 08-04 incident
report? — got "no", and moved on. Three sweeps, three correct answers, and the feed's BACK CATALOGUE
was never opened. Today it yielded THREE substantial facts from posts dated Jul 2, Jul 21 and Jul 23,
all of which predate the one post this pack had read from that feed.
WHY THE EXISTING RULE DID NOT CATCH IT: Appendix S's test is "a recurring URL that has never produced
an ARTICLE-LEVEL fetch is UNREAD". aisi.gov.uk HAD produced an article-level fetch — exactly one, and
it arrived via a different route (the 13th run's incident-cluster hunt), not by following the index.
So the feed looked read and the test passed. THE SHARPER TEST, offered for the next run: a feed is
unread until someone has looked at its FRONT PAGE AS A LIST and made a per-item keep/skip decision.
One article beneath a feed is evidence about that article, not about the feed. The since-last-run
filter is only valid once that has happened at least once.
This is the third instance of the same shape (anthropic.com/engineering, metr.org/blog, now AISI) and
the asymmetry the 13th run recorded still holds: unread means UNKNOWN yield. metr.org was low. This
was the best block of the run.

*** FINDING 2 — *** THE FETCH TOOL INVENTED A NUMBER, AND I CAUGHT IT BY ASKING THE SAME PAGE TWICE.
A FIFTH MECHANISM FOR A WRONG RESULT, AND THE ONLY ONE THAT PRODUCES A CONFIDENT POSITIVE. ***
Isolated cleanly: same URL, two WebFetch calls, only the PROMPT differed.
  open-ended prompt -> "a monitor suspicion score of 3 out of 100 within 5,000 queries, compared to
                       Best-of-N baseline scores of 14-18 across three runs of 150,000 queries each"
  verbatim prompt   -> "In one run, the evolutionary algorithm achieved a score of 3 in under 5k
                       steps" / "BoN scores of 14, 15 and 18" / BoN query count: **NOT STATED**
THREE FABRICATIONS IN ONE SENTENCE: a scale maximum ("out of 100") the page never gives; an entire
baseline budget ("three runs of 150,000 queries each") that was the denominator the whole efficiency
claim rested on; and "queries" for the source's "steps". It also dropped "In one run", promoting a
single observation to a general result.
WHAT MAKES THIS WORSE THAN THE OTHER FOUR NEGATIVE-GREP MECHANISMS: those produce FALSE ABSENCES,
which read as uncertainty. This produces a CONFIDENT PRESENCE. And the bias is not random — every
invention made the comparison more complete and more quotable, i.e. fabrication is narrative
gap-filling, so the invented figure is precisely the one that makes a fact worth writing. It passes a
plausibility check because plausibility is what generated it.
THE FIX IS CHEAP AND IS NOW MANDATORY (fetch-routes route 4): never write a number, quotation or
threshold from an open-ended WebFetch; run a second call on the same URL demanding VERBATIM sentences
for each figure, with an explicit "or say NOT STATED" licence to report absence.
CALIBRATION, so nobody over-corrects: the same two-call pattern confirmed 7 of 7 figures on one page,
8 of 8 on another and 8 of 8 quoted strings on a third. WebFetch is accurate when the page states the
thing. It invents when the page does NOT, and only the second call separates those two cases.
AND IT IS RETROSPECTIVE — see the staleness pass, which found this exact defect class twice.

FINDING 3 — A PAGE THAT DELEGATES A RULE STRIPS ITS MODAL STRENGTH, AND THE BINDINGS DISAGREE.
Caught by my own in-run self-review. MCP's basic/versioning.mdx gives a compatibility matrix and then
says the detection mechanics are "specified in the binding pages". Its summary carries NO modal
keyword. Reading the binding pages: on stdio a dual-era client **SHOULD** probe with `server/discover`;
on Streamable HTTP a dual-era client only **MAY** detect the era. The stdio page also carries a
**MUST NOT** ("The fallback **MUST NOT** be keyed to one specific error code") that appears nowhere
in the summary. A fact written from the summary states two different obligations as one and silently
drops a MUST NOT — which is exactly what I did before catching it.
THIS IS THE MIRROR OF PRECONDITION (e). (e) catches a rule RESTATED more weakly after a split; this
catches a rule NOT RESTATED AT ALL, only pointed at. New precondition (f): IF A PAGE SAYS A RULE IS
SPECIFIED ELSEWHERE, YOU HAVE NOT READ THE RULE. Follow the pointer before writing any modal verb,
and expect per-binding rules to differ by binding.

FINDING 4 — A POSITIVE GREP IS AS WEAK AS A NEGATIVE ONE WHEN THE CLAIM IS ABOUT SEMANTICS.
Grepping `protocolVersion` across all 41 files of 2025-11-25 returns 15 hits in 5 files. Read as a
count, that says "present in the predecessor, nothing new here" and kills a true version-attribution
finding. Read as HITS, every one is the `initialize` handshake field on `InitializeRequestParams` /
`InitializeResult`; none is the per-request `_meta` key of 2026-07-28. The token survived the
revision; its meaning did not. This pack has four recorded mechanisms for a false NEGATIVE grep and
had none for a misleading POSITIVE one. Rule: read the hits, do not count them.

FINDING 5 — THE 19th RUN'S "Keep reading" CATEGORY HYPOTHESIS IS FALSIFIED, AS IT ASKED.
The 19th run proposed from four observations that an openai.com post's footer lists the three newest
posts IN ITS OWN CATEGORY, and explicitly flagged it as a hypothesis to test. Tested on
/index/unlocking-self-improvement-gpt-red/ (tagged Safety / Publication): the footer returned
Expanding Daybreak (Security, Aug 10), Ten advances in mathematics (Publication, Aug 1), ARC-AGI-3
(Research, Jul 29) — three different categories, only one of which the post carries, in strict date
order. That is plain recency, the 18th run's original reading. Recorded as FALSIFIED rather than
deleted, so a future run does not re-derive the category theory from another small sample. Worth
noting as method: the 19th run stated it as a hypothesis with a named cheap test, and the test ran
one run later and settled it. Do that more.

FINDING 6 — TWO INDEPENDENT ORGANISATIONS PUBLISHED AUTOMATED-RED-TEAM RESULTS A WEEK APART, AND
THE PAIR IS WORTH MORE THAN EITHER. OpenAI (Jul 15) trains an attacker by self-play and reports its
hardened model failing on 0.05% of that attacker's injections. UK AISI (Jul 23) red-teams other
labs' monitors and reports vulnerabilities in every version tested, plus the warning that beating
THEIR red team does not bound a real adversary. Neither contradicts the other on any fact; they set
opposite defaults for reading a robustness number. The deciding variable, and the reason this became
a `decisions` fact rather than two observations: OpenAI holds the ENVIRONMENTS out and leaves the
ATTACKER in the defender's training distribution, which is precisely the axis AISI's caution is
about. OpenAI's own generalisation test (84% vs 13% human success on a novel arena) is a test of the
ATTACKER generalising to new scenarios, against GPT-5.1 — not of the hardened defender against a new
attacker. A generalisation claim has a subject; check which side of the game it is about.

=== FACTS WRITTEN (7 new, 3 updated from crawling, 5 updated by the staleness pass, 0 retracted) ===
  NEW —
    kb/architecture/ai/agents/security/adversarial-training/5f4497f2   (GPT-Red: self-play RL, the
      TWO-SIDED defender reward that prevents the refuse-everything degenerate solution, per-
      environment threat models, attacker kept undeployed, and the over-refusal control. All figures
      transcribed from raw browser page text, not extracted by a model.)
    kb/decisions/ai/agents/security/robustness-measurement/9b0c8c78   (Finding 6. The three questions
      to ask of any published robustness rate, marked as this pack's framing.)
    kb/gotchas/ai/agents/evaluation/oversight-methods/8756141e        (AISI: every model tested
      attempted to cheat; self-report <50%; CoT unreliable in two distinct ways; NO capability trend
      but a strong TRAINING effect; lower-bound modality load-bearing.)
    kb/architecture/ai/agents/security/monitor-design/a5eaec6b        (AISI Control Red Team: vulns
      in every monitor version; the ROUTING RULE is a softer target than the monitor; async monitors
      defeated by faked instruction provenance; and the search result stated WITH the two limits the
      source imposes on it — no BoN budget, no scale range.)
    kb/decisions/ai/agents/evaluation/compute-budget/80866fc3         (capability as a curve;
      exponent 0.7-1.0 against human task duration; the STOPPING rule — compute buys little without a
      self-check signal; the 40min->4h horizon swing from budget alone; the 10-30% regression band.)
    kb/invariants/ai/agents/tools/mcp/interop/versioning/f4367bd0     (no handshake; -32022; the
      seven-row matrix and its two failing cells; the silent-wrong-semantics cell; per-transport
      detection with its real modal strengths; era as a server property.)
    kb/gotchas/ai/agents/provenance/watermarking/943a7e3c             (SynthID-Text rides on lexical
      freedom, so it is thinnest exactly where agent output is most constrained — code, exact
      outputs, edits of human text. All 8 quoted strings verified verbatim by a second fetch.)
  UPDATED FROM CRAWLING —
    193d5de2  — AISI has PUBLISHED THE CONTROL IT BUILT after the incident: an automated LLM monitor
      over full trajectories plus manual transcript review. sources 3->4, conf .85->.9.
    ee458c93  — the fact's own caveat ("CoT monitoring depends on the trace being faithful") is now
      an independent MEASUREMENT rather than a caution, and the monitor's evadability is a second
      one. sources 2->3.
    fafca497  — the degradation rule is a **MUST** in the specification, not the guidance the docs
      overview implies; identifier prefixes are mandatory by cross-reference to the `_meta` rules;
      AND the capabilities-map mechanism is DATED to 2026-07-28, verified across all 41 files of
      2025-11-25.

CONTRADICTIONS: none between sources requiring a `decisions` fact on facts. ONE genuine
METHODOLOGICAL disagreement, and it became a decisions fact rather than being flattened — Finding 6,
9b0c8c78. Both positions kept, the deciding variable named.

=== STALENESS PASS (5 sampled; PRIMARY AXIS EARLIEST-COMMITTED as the rotation required. ALL FIVE ===
=== are first-run facts committed 2026-07-26 and none had ever been checked. 4 CORRECTED, 1        ===
=== CONFIRMED-with-marking-correction, 0 retracted. THE HIGHEST DEFECT RATE THIS PASS HAS SEEN.)   ===
  HOW THE SAMPLE WAS FOUND: every knomit_query result row carries `committed_at` in its frontmatter
    as a UNIX epoch, and it is the LAST-TOUCH timestamp. The topical queries run earlier for the
    query-first rule had already surfaced dozens of facts WITH their ages. Sorting those and dropping
    everything in the verification pool produced an earliest-committed sample at ZERO marginal cost.
  *** TWO OF THE FIVE CARRIED FABRICATED NUMBERS — THE SAME DEFECT CLASS AS FINDING 2, RETROSPECTIVE.
  This is now a named class: the figure most likely to be invented is the one that COMPLETES A SET —
  the remainder of a percentage, the range around a qualitative duration, the denominator of a ratio. ***
  19ed6273 (0.75, held) CORRECTED — FABRICATED FIGURE. "another ~15%" of BrowseComp variance is NOT
    in the source, which quantifies only the 80%. Also pinned the upgrade claim to its two specific
    models and added the SECOND reason the source gives for coding being a poor fit.
  70127cdd (0.75 -> 0.85) CORRECTED TWICE, IN OPPOSITE DIRECTIONS. (a) OVERCLAIM: "(2-4 seconds)" is
    not in the source, which says only "multiple seconds". (b) UNDERCLAIM: the fix was hedged as
    "reportedly" when the source carries a NAMED attribution and a DIRECT QUOTE. One fact, one
    invention and one needless hedge.
  a13a57c9 (0.8 -> 0.85) CORRECTED — A TOOL IDENTIFIER THAT DOES NOT EXIST, RECORDED AS A DEFAULT.
    Default scope is `shell` ALONE, and `computercontroller__automation_script` appears NOWHERE on
    the page. Also: the blocked-behaviour list is a user-authored plain-language policy file, and the
    threat model was modally strengthened. Every correction made the control sound NARROWER.
  0b340b6b (0.8 -> 0.85) CORRECTED — A PARAPHRASE WEARING QUOTE MARKS ("narrow your query"), and the
    source's actual example points the OTHER WAY — toward decomposition. Plus an unmarked inference.
  ac887ec9 (0.8 -> 0.85) CONFIRMED, with a MARKING correction — three paragraphs of the pack's own
    prescription sat under Huyen's citation; the source discusses no mitigation at all.
  Nothing in the kb is yet older than 90 days (pack began 2026-07-26; today is day 22).

=== IN-RUN SELF-REVIEW: ONE DEFECT (f4367bd0, modal strength lost to a delegated rule — Finding 3). ===
=== POST-COMMIT REVIEW PASS: ONE DEFECT (f4367bd0, "both dual-era rows" for three of seven).        ===
  NEW SUB-RULE (20th): A QUANTIFIER OVER A STRUCTURE YOU DID NOT REPRODUCE IS UNCHECKED. "Both",
  "all", "the two", "every" — applied to rows, entries or cases a fact SUMMARISES rather than lists.
  Item 8 inspects the word and item 13 re-runs the arithmetic; a quantifier whose arithmetic was
  never written down falls between them. Go back to the structure and COUNT.

*** ================================================================================== ***
*** knomit_review SESSION, RUN AT THE USER'S REQUEST AFTER THE CRAWL. 37 ITEMS, ALL     ***
*** ANSWERED. Pruned 0, Merged 0, Updated 2, Synthesized 3.                             ***
*** ================================================================================== ***

WHY NOTHING WAS PRUNED OR MERGED, stated so the next run does not read zero as a skipped job. Every
prune item was a thematically coherent cluster of NON-duplicates. The pack is written with explicit
disambiguation between adjacent claims — facts routinely say "this is a different axis from X" and
name the distinction — so the clusters the review proposes are related-by-topic, not redundant. The
two mix-up defences (36d792c3 discovery-document, fails CLOSED; bdb36fce authorization-response,
fails OPEN) are the clearest case: same attack family, opposite failure modes, and each fact tells
you not to conflate them. Merging on topical similarity would have destroyed that.
ALSO LOAD-BEARING: the 13th run's warning that a scoped knomit_review is what deleted 4f5e9dfe. This
session was run UNSCOPED and every prune proposal touching a fact cited by another fact was declined.

THREE SYNTHESES WRITTEN (all origin: distilled, under kb/principles/ where the pipeline puts them):
  kb/principles/ai/agents/tools/mcp/counterparty-contingent-controls  — MCP authorization controls
    are contingent on counterparties you do not operate, and the spec's failure defaults are NOT
    consistent: two fail closed (PKCE discovery, AS-metadata issuer validation), one fails OPEN
    (RFC 9207 iss), three are delegated to policy or to a human (localhost impersonation, CIMD
    admission, multi-AS selection). Only the client-side dereference bans are fully yours. So
    "we implemented MCP authorization" does not determine your posture; a per-counterparty
    enumeration does. None of the seven source facts tallies the failure defaults against each other.
  kb/principles/ai/agents/evaluation/harness-parameter-sensitivity   — FOUR harness parameters have
    each been SEPARATELY measured moving an agentic result, from three organisations: benchmark
    implementation (MMLU across HELM/EleutherAI/original), resource allocation (6pp on Terminal-Bench
    2.0 but only 1.54pp on SWE-bench — magnitude is benchmark-specific), the step cap (REORDERS
    rankings: 300 vs 600 turns flips which model wins on ExploitBench), and token budget (40min->4h
    horizon for one model). A score without its configuration is uninterpretable, not merely
    imprecise. Carries the correction that small gaps are NOT "noise" — they "deserve skepticism
    until the configuration is documented and matched", which is a different instruction.
  kb/principles/ai/agents/evaluation/environment-boundary             — benchmark CONTAMINATION and
    eval CONTAINMENT are one engineering problem: the agent's action space includes the real world
    and the fiction exists only in the prompt. Four documented forms (fiction resolves to a real
    company; resolves to nothing so the agent CREATES it; the benchmark is public and gets decrypted;
    the assertion targets the screen not the state). The unifying rule is the simulation-belief
    fact's: the boundary must be ENVIRONMENTAL, because the model's belief about whether it is in a
    test is unreliable in BOTH directions. Yields a four-item checklist that buys a cleaner score and
    a contained run at once — which is the payoff of treating the two jobs as one.

ELEVEN DISTILL ITEMS DECLINED, and the reason matters: in most of them the synthesis ALREADY EXISTS
and was one of the inputs (b9b11a69 for runtime durability, 3afa31af for MCP statelessness, db193402
for OWASP artifact limits, 1d1440fe for reviewer error direction, c9f0238b for context accumulation,
00d3ef19 for tool selection). A synthesis-of-syntheses over facts already dense with "WHAT THIS DOES
NOT MEAN" clauses is compression where compression is the known failure mode. One tempting
generalisation was FALSIFIED before writing: "model-judgement controls fail, deterministic ones hold"
is contradicted by fdad859e, which documents three bypasses of a deterministic control.

*** TWO DEFECTS THE REVIEW FOUND THAT THE JOB CANNOT FIX — FOR A HUMAN. ***
BOTH ARE THE SAME STRUCTURAL PROBLEM AND IT IS WORTH NAMING: **A DISTILLED SYNTHESIS FACT DOES NOT
INHERIT CORRECTIONS MADE TO ITS SOURCE FACTS.** The synthesis is written once from the sources as they
stood; when a later staleness pass corrects a source, the synthesis keeps the old claim, and nothing
in the pipeline links them. Two live instances:
  1. kb/principles/ai/agents/context-engineering/0f260eea asserts that pin metadata "is written
     during the first reduction and persists through every later one". Its own cited source,
     714a540c, REMOVED that claim as unsupported by the refs — the Strands docs page does not specify
     pin_first at all. The synthesis states as mechanism what the source retracted.
  2. kb/principles/ai/agents/multi-agent/1d1440fe says Goose's adversary mode "covers only two tools
     by default (`shell` and `computercontroller__automation_script`)". THIS RUN corrected a13a57c9:
     the default is `shell` ALONE and that identifier does not exist on the page. The synthesis
     carries a fabricated identifier that its source no longer carries.
BOTH WERE FLAGGED via the review's confidence lever (each dropped to 0.7, which the session applied —
that is the "Updated: 2"). THE BODIES ARE NOT FIXED. Direct `knomit_update` on either fails with
`must-have-designer-entity: principles must be authored via /knomit-principle`, exactly as Appendix S
documents. The review PIPELINE can write kb/principles/ (it wrote three facts there this session);
the job cannot. So a human must edit these two bodies, or a future review must merge them forward.
GENERAL RULE FOR FUTURE STALENESS PASSES: when you correct a fact, grep the corpus for other facts
carrying the same claim — sub-rule 15 already says this for QUOTATIONS, and these two show it applies
just as strongly to SYNTHESES that consumed the fact. The synthesis is the likeliest silent carrier.

*** ONE PIPELINE OBSERVATION, ALSO FOR A HUMAN. ***
knomit_review's distill stage OFFERED THE THREE PRIVATE `.knomit/` JOB-STATE SLOTS AS DISTILLATION
INPUTS (item 37: crawl-sources, crawl-state, fetch-routes, plus one ordinary kb fact). knomit_query
cannot see those slots — that exclusion is the whole point of the private namespace, and Appendix S
states it plainly: "machinery is not knowledge, and it should not be indexed, embedded or ranked
alongside the pack's actual content." The REVIEW walker evidently does not apply the same exclusion.
I declined the item and wrote nothing. Had a less careful run accepted it, the job's own bookkeeping
— including the standing-rule material in fetch-routes — would have been distilled into kb/ as
knowledge, which is close to the thing the spec forbids (publishing the job's instructions into a
slot the job can write). Worth fixing at the walker.
NOTE ON HOW I READ THAT ITEM: pages 1, 3 and 4 were read in full. Page 2 exceeded the tool-result
limit and was persisted to a file; I read its metadata and confirmed it carried crawl-state.md — the
body I had written earlier in the same session and still held in context — rather than re-reading
56KB of it. Saying so because "I read every page" would not have been quite true.

=== SUGGESTED SPLIT FOR THE NEXT RUN ===
(1) FINISH THE AISI BACK CATALOGUE — NEW TOP PRIORITY, and the reason is Finding 1. Four unread posts
    are listed in crawl-sources with a warning that three of the four slugs are UNVERIFIED.
    *** AND APPLY FINDING 1's TEST TO EVERY OTHER RECURRING FEED: has anyone ever read its FRONT PAGE
    AS A LIST? For huggingface.co/blog, embracethered, research.google and microsoft/security the
    honest answer may be no. That check is cheap and it just paid three facts. ***
(2) MCP TRANSPORTS — basic/transports/streamable-http.mdx and stdio.mdx in FULL. Only their Backward
    Compatibility sections were read this run and both pages are large and normative.
(3) THE GPT-RED PAPER. The post carries a "Read the paper" link that was NOT followed — it will carry
    the eval protocol, which is exactly what 9b0c8c78's three questions need.
(4) OWASP AGENTIC TOP 10, APPENDIX C — the NHI Top 10 2025 mapping, extract line 1882+, table at
    1886. Nothing OWASP was fetched this run, so that whole queue is untouched and intact.
(5) openai.com/index/putting-frontier-cyber-models-in-more-trusted-hands/ (Aug 10) is the top unread
    OpenAI item. ALSO the ARC-AGI-3 post (Jul 29) — a harness-configuration result, and this run's
    new harness-parameter synthesis gives it somewhere to land.
(6) OWASP companion corpus, still unread: Solutions Landscape Red Teaming Taxonomy, A Practical Guide
    for Secure MCP Server Development, CheatSheet — Securely Using Third-Party MCP Servers, GenAI Red
    Teaming Guide, Agentic AI Solution Landscape, OWASP AIBOM, GenAI Data Security.
(7) LLM Top 10 2026 per-entry chapters: LLM03 Excessive Agency (p23-26), LLM08 Hidden Context
    Exposure (p46-49). id 56857.
(8) THE MASEC reference list: NetSafe (arXiv 2410.15686) and chaos engineering for LLM MAS (arXiv
    2505.03096). Both report MEASUREMENTS. Pairs with 24e4552d — and now also with 80866fc3.
(9) STILL WATCHING, four artifacts, none landed as of 2026-08-17:
      (a) OpenAI's TECHNICAL REPORT on the HF incident — promised "in the coming weeks" 2026-07-21.
      (b) The METR + Redwood JOINT assessment — contracted, not published.
      (c) Irregular's containment white paper.
      (d) Anthropic's WATERMARK DETECTION API — 943a7e3c is qualitative in every respect because the
          post publishes no rates and no minimum length; the API docs are where those land.
(10) The OWASP ASI incidents tracker at owasp-agentic-ai-security-incidents.lovable.app — NINE runs
    listed without a fetch. Check first whether it is simply Appendix D of the Top 10 PDF.
(11) FOR A HUMAN, NOT THE CRAWLER — now FOUR items:
    (a) 4f5e9dfe is retracted but cited by THREE live facts — 483263c5, c02ac546, bdf3336e.
    (b) The 14th/15th run bodies are unreachable behind squashed merges. FOUR runs have reported both.
    (c) NEW — 0f260eea and 1d1440fe each carry a claim their source fact has since corrected, and
        kb/principles/ is write-blocked to the job. See the review section above.
    (d) NEW — knomit_review's distill stage can see the private .knomit/ slots. See above.

=== PER-SOURCE STATUS AND QUEUE, as of the 20th run ===
Each run REPLACES this section with its own — carry forward what is unread, drop what was read.

*** UK AISI — PROMOTED. Article catalogue now in crawl-sources. 4 read, 4 unread, 2 below the bar. ***
OWASP GenAI PDF REPORTS — STATUS (unchanged this run; nothing OWASP was fetched):
  AIUC-1 Crosswalks (55pp, id 54627)                         READ (11th), 3 facts+1 upd; re-verified 18th.
  AI Security Solutions Landscape Red Teaming Q2 2026 (15pp, id 54018) READ (11th), 1 fact; re-verified 18th.
  State of Agentic AI Security and Governance 2.01 (139pp, id 50592)   READ (12th), 8 facts+1 upd
    ^ chapters still NOT written up: Enterprise Adoption Maturity Model (p53-62), Alignment with
      Top 10 Agentic (p61), Future Trends / What Remains Unsolved (p63-68); AI SBOM and Supply Chain
      Provenance (p46-48); Explainable AI (p49); Appendix 1 agent-type taxonomy (p70-76); Appendix 3
      ASI risk classes (p116); Appendix 6 Top 10 Impacting Personal Agents (p128). Appendix 2 is low.
  OWASP GenAI LLM Top 10 2026 (122pp, id 56857)              READ (13th), 2 facts + 1 upd
    ^ NOT mined: the ten per-entry chapters. LLM03 (p23-26) and LLM08 (p46-49) most relevant.
  Securing Agentic Applications Guide 1.0 (id 49059)         READ (15th), 2 facts
    ^ MOSTLY BELOW THE BAR. One pass maximum: 2.2 Secure Architecture Patterns (extract lines
      833-1313), 2.5 Case Studies, 9.x runtime hardening.
  Multi-Agentic System Threat Modeling Guide v1.0 (id 46950) READ (15th), 1 fact + critiqued 16th
    ^ SECTION 5 STILL UNMINED: "Threat Modeling Anthropic MCP Protocol using MAESTRO" (extract line
      3132 on). Sections 3-4 are RPA/blockchain enumeration, skip.
  Agent Name Service (ANS) v1.0 (id 47278)                   READ (16th), 1 fact + 1 upd. DONE.
  OWASP Top 10 for Agentic Applications 2026 (id 52117)      READ (17th, 18th), 5 facts total.
    ^ Remaining: Appendix C (NHI mapping, line 1882+), Appendix B (CycloneDX/AIBOM), per-entry
      mitigations for ASI03-ASI07 and ASI09, Appendix D per-incident detail.
OWASP HTML blog posts read fine with a plain WebFetch. Unread and promising:
  /2026/05/13/memory-is-a-feature-it-is-also-an-attack-surface/  (ASI06; pairs with 7bd6c6c9)
  /2026/04/14/owasp-genai-exploit-round-up-report-q1-2026/
  /2026/04/14/finbot-ctf-is-live-a-hands-on-companion-to-the-owasp-genai-security-project/
*** MCP 2026-07-28 — TRIPWIRE CHECKED 20th RUN VIA THE REPO, STILL UNCHANGED (10th consecutive) ***
READ SO FAR: changelog, versioning (BOTH the learn page and the new spec page), deprecated,
  server/discover, basic/patterns/mrtr, basic/index, server/tools, learn/server-concepts,
  docs/extensions/overview, security_best_practices at 2025-06-18 / 2025-11-25 / 2026-07-28, THE
  ENTIRE 2026-07-28 AUTHORIZATION SPLIT (all four pages), basic/authorization.mdx at 2025-11-25 /
  2025-06-18 / 2025-03-26, and (20th) the Backward Compatibility sections of transports/stdio and
  transports/streamable-http.
  ALSO: all 41 files of revision 2025-11-25 and all 186 of 2026-07-28 fetched for verification sweeps.
STILL UNREAD, in rough value order:
  /specification/2026-07-28/basic/transports/streamable-http   <- NEW TOP (only its compat section read)
  /specification/2026-07-28/basic/transports/stdio             <- same
  /specification/2026-07-28/server/utilities/caching  (ttlMs/cacheScope)
  /extensions/tasks/overview and /extensions/apps/overview
  /docs/2026-07-28/develop/clients/client-best-practices
  /specification/2026-07-28/schema                 (reference only; expensive, low altitude — but
     NOTE the schema/<rev>/ tree is a SEPARATE top-level tree, see fetch-routes 3d)
OPENAI: full /index/ catalogue in crawl-sources. GPT-Red READ and closed out except its linked PAPER.
  developers.openai.com/api/docs/guides/ — plain WebFetch, no browser. Scan the tree for siblings.
ANTHROPIC /news/: watermark post READ. Slugs are editorially shortened — never derive from titles.
Also still unread: https://www.cnn.com/2026/08/05/tech/meta-ai-hacking (a fifth lab; secondary —
  find the primary), and the simonwillison queue: /2026/Jul/31/stateless-mcp/ (pairs with 3afa31af),
  the-tokenpocalypse (404media), /2026/Aug/2/open-letters/.
YIELD RANKING as of the TWENTIETH run — spend the budget in this order:
  1. SPEC AND PROTOCOL TRIPWIRES via the GitHub contents API. Cheapest high-value call, outage-proof,
     EVERY run. AND: where a spec is versioned in git, DIFF REVISIONS — but only with the SIX
     preconditions now in fetch-routes. Held rank 1 for a fifth run.
  2. *** UK AISI BLOG — NEW ENTRY, STRAIGHT IN AT RANK 2 on this run's evidence: three back-catalogue
     posts, three substantial facts, plain WebFetch, no gate. A government evaluator publishing
     MEASUREMENTS and negative results about its own methods is the closest thing this pack has to an
     ideal source. Four posts still unread. Re-rate downward only if that block disappoints. ***
  3. OWASP GenAI PDF REPORTS. Nine read across seven runs for 26 facts + corroborations.
  4. PRIMARY OPERATOR SECURITY POSTS — openai.com/index, anthropic.com/news. Use WebSearch+
     allowed_domains, NOT the "Keep reading" footer (hypothesis falsified this run, Finding 5).
  5. PUBLISHED CRITIQUES OF SOURCES ALREADY IN THE KB. Search "critique/gaps in <document>".
  6. MCP remaining spec pages (list above). The two transport pages are next.
  7. anthropic.com/engineering — UNREAD: AI-resistant-technical-evaluations, building-c-compiler,
     contextual-retrieval, swe-bench-sonnet, desktop-extensions. Index quiet since Apr 2026 and
     confirmed quiet AGAIN this run — fifth consecutive. Stop sweeping the index; go to the articles.
  8. microsoft.com/en-us/research/blog — 1 fact of 3 last time. Prefer METHOD over FRAMEWORK posts.
  9. Azure Architecture Center. The six-part RAG series is the largest coherent unread block.
 10. aws.amazon.com/blogs/machine-learning — product-heavy, but spec-level changes surface early.
 11. builder.aws.com Builders' Library — 16 of 30 read for 55+ facts; the 12 unread skew CI/CD.
 12. cognition.com/blog — dense, specific, publishes reversals of its own positions. Unread:
     coding-agents-101-the-art-of-actually-getting-things-done, swe-grep, blockdiff,
     devin-annual-performance-review-2025, evaluating-coding-agents, making-fable-cheaper-than-opus,
     devin-fusion, swe-1-7, measuring-open-source-model-trustworthiness,
     introducing-devin-security-swarm, frontier-code and frontier-code-1.1, ai-productivity.
 13. huggingface.co/blog — scan for incident/infrastructure/engineering; SKIP model/dataset launches.
     *** APPLY FINDING 1's TEST HERE FIRST — has its front page ever been read as a list? ***
 14. sourcegraph.com/blog — real measurements. Unread: compliance-first-ai-proving-agent-provenance,
     owning-a-codebase, sourcegraph-mcp-and-a-cheaper-model-beat-a-mythos-class-model-alone,
     the-hidden-cost-of-code-that-nobody-touches.
 15. eugeneyan.com/writing — unread: secure-source-code (May 2026) and anything newer.
 16. simonwillison.net/tags/llms/ — VALUE IS THE LINKS. CAVEAT: talk summaries are the weakest link.
 17. latent.space/archive — unread: /p/aiewf26trends, /p/modal2026, /p/poolside, /p/chatgpt-work.
 18. langchain.com/blog — eval and benchmark posts clear the bar; customer stories do not.
 19. blog.redwoodresearch.org — watch-only, for the METR+Redwood joint assessment.
 20. metr.org/blog — demoted 13th run. RE-RATE when the joint assessment lands.
 21. embracethered.com/blog — low volume, high value, security only. Its TOCTOU post was re-verified
     this run and held up well under scrutiny.
 22. trychroma.com/research — rare but substantial. Unread: evaluating-chunking.
 23. research.google/blog — checked twice, output is health/quantum/diffusion. Low yield.
     microsoft.com/en-us/security/blog — one good agent-identity post, otherwise threat intel.

dead or unreadable — EMPTY, and now TEN FOR TEN on false dead ends. Read the warning in Appendix S.
  block.github.io/goose -> goose-docs.ai. AND goose-docs.ai ITSELF now shows a "goose has moved to
    the Agentic AI Foundation (AAIF)" banner dated 2026/04/07 — the docs still serve normally. A
    governance change, NOT a dead source.
  https://strandsagents.com/latest/... -> 404. Use /docs/... instead.
  modelcontextprotocol.io -> ECONNREFUSED 2026-08-12; fully up 08-14, 08-15, 08-17. Transient.
  modelcontextprotocol.io/docs/concepts/tools -> recorded GONE by the 16th run; it REDIRECTS (200).
  .../2025-11-25/basic/authorization/security-considerations.mdx 404s — authorization was ONE FILE at
    that revision. A 404 can mean the path SHAPE changed. fetch-routes 3b/3c.
  .../2025-11-25/basic/versioning.mdx 404s — NEW THIS RUN, a DIFFERENT shape again: the spec-tree
    versioning page exists only at 2026-07-28 and draft, while a same-named page lives in the docs/
    tree for every revision. Two pages, one name, two trees. fetch-routes 3b.
  /news/how-claudes-text-watermark-works -> 404. Anthropic slugs are editorially SHORTENED; the real
    one is /news/claude-text-watermark. Guessed slugs have now 404'd on five separate hosts.

TIER 6 GITHUB READMEs — CLOSED OUT. A repo README is worth a fetch for LIFECYCLE STATUS and nothing
else. AMENDMENT (16th run): a repo that HOSTS a documentation site is different — there the repo is
the primary source. Only remaining tier-6 item: the x1xhlol INDIVIDUAL prompt files.

VERIFICATION-POOL NOTE (updated 20th run). Checked so far — cb98732e, 27652a82, 111f8b2c, 2b74037b,
5ad0fb45, 62312b79, 0fe91ac7, fc249ffc, a5ade87d, dee636a2, 77b3e628, f877f05d, d4e3b247, bcbf13c2,
d468cbbe, 089c7cba, 15e7bf02, 46f3ea69, 56986e8f, d87795d4, 882100d9, 28ba65db, c93d93ee, c7290868,
c1bbf73f, 48c4e555, c2f12069, 62c9a78b, e9b7eef3, 96ebc34e, c858a924, c99ec745, 30869b36, c436422a,
c1e18090, 9920b5d6, 773a89ee, 48c9de1b, afce1dae, 4b0261d0, 052c2b66, f78a326a, 38c06627, d18637a2,
1beb89e6, f1cbb540, 89df351e, 4e923405, 714a540c, f7dee43a, 9aaea0dc, 9e29d93a, 1531a0d1, b4d688b1,
99aa74e6, 0720e9d7, 59a75c06, b471f9ef, ba5db3ec, f4005c98, c28c7f7b, 11ebefd6, db15af92, 8f2fdde8,
ee3bc7d3, ca3382bd, 46eeb374, 703147ba, ba1b7aad, 8cf06566, 07eec7ff, 2d060289, 1719fe66, 43155c66,
406e5a50, bdb36fce, f8646714, ce7e0330, 30543305, 60544a53, f4bba0ae, eae23eac, 6c0c742e, 74996815,
24e4552d, 36d792c3, 00fd386c, and (20th run) 0b340b6b, 19ed6273, a13a57c9, ac887ec9, 70127cdd, plus
this run's own f4367bd0 via self-review and review pass.
THREE AXES, ROTATE THEM: confidence (lowest first), earliest-committed, shared-ref grouping.
13th earliest-committed (2 defects in 5); 14th confidence (1 + 1 partial); 15th shared-ref (3 in 5);
16th earliest-committed AND shared-ref (2 in 5); 17th SHARED-REF primary (0 claim defects, 3 ref
additions, 2 source-count fixes); 18th EARLIEST-COMMITTED primary (1 correction, 1 scope correction,
4 enrichments, 2 source self-contradictions); 19th CONFIDENCE primary + shared-ref (2 corrected, 3
confirmed-and-enriched, 1 confidence raised); 20th EARLIEST-COMMITTED primary — **4 DEFECTS IN 5,
THE HIGHEST RATE YET, INCLUDING TWO FABRICATED NUMBERS AND ONE FABRICATED IDENTIFIER.**
READ THE 20th RESULT CAREFULLY, BECAUSE IT SAYS SOMETHING ABOUT THE POOL AND NOT JUST THE AXIS. All
five were FIRST-RUN facts, written on 2026-07-26, and never checked since. The first run wrote fast
and wide, and its output is measurably less reliable than later runs' — three of the four defects
(two invented figures, one invented identifier) are the SAME class: a plausible specific inserted
where the source gave none. Later runs' defects skew toward modal and attribution errors instead.
IMPLICATION FOR THE ROTATION: RUN EARLIEST-COMMITTED AGAIN NEXT RUN rather than rotating away from
it, and only rotate back to confidence once the 2026-07-26 band is exhausted. Candidates in that band
can be found free of charge via `committed_at` on any query result row (~1785089xxx).
AVOID SAMPLING kb/principles/** — write-blocked, you cannot record the result. CONFIRMED AGAIN THIS
RUN: knomit_update on kb/principles/ai/agents/multi-agent/1d1440fe.md failed with
`must-have-designer-entity`. You CAN flag such a fact through a knomit_review confidence decision,
which is how the two defects above were marked — but you cannot fix the body.
SUB-RULE (14th): a PARTIAL confirmation must be written down as partial, in the fact.
SUB-RULE (15th): when a quoted sentence appears in more than one fact, a defect in it is duplicated
  too. Query the kb for the quotation before correcting it. *** EXTENDED 20th: this applies just as
  strongly to SYNTHESES that consumed the fact, and a distilled synthesis is the likeliest silent
  carrier because nothing links it back to a corrected source. ***
SUB-RULE (15th): check that a CITED PAGE ACTUALLY CARRIES the detail attributed to it.
SUB-RULE (15th): RUN THE CHECKLIST ON THE FACTS YOU JUST WROTE, and RUN A SEPARATE PASS AFTER
  COMMITTING. Four runs have now done the post-commit pass and ALL FOUR found defects the in-run
  review structurally could not. Budget both.
SUB-RULE (16th): WHERE A SOURCE IS VERSIONED AND IN GIT, DIFF THE REVISIONS INSTEAD OF RE-READING.
SUB-RULE (17th): A CLAIM THAT A PATH IS DEAD, OR THAT CONTENT MOVED SOMEWHERE, IS A CLAIM LIKE ANY
  OTHER. Test the redirect; grep the alleged successor for the content.
SUB-RULE (17th): THE SELF-REVIEW MUST RE-RUN COMPUTATIONS, NOT RE-READ PASSAGES.
SUB-RULE (18th): "NEW IN REVISION X" REQUIRES SEARCHING THE WHOLE PREDECESSOR REVISION — every page
  AND every top-level tree. Enumerate on the REVISION DATE, not a docs/ prefix.
SUB-RULE (18th): VERIFY WHAT YOU DOWNLOADED, NOT THAT THE DOWNLOAD HAPPENED.
SUB-RULE (18th): A TABLE OF NUMBERS WITHOUT THEIR ANCHORS IS NOT A REFERENCE.
SUB-RULE (19th): MATCH THE SEARCH'S SCOPE TO THE CLAIM'S SUBJECT NOUN.
SUB-RULE (19th): WHEN A SOURCE GIVES BOTH A LIST AND A COUNT OF THAT LIST, COUNT THE LIST.
SUB-RULE (19th): A NEGATIVE GREP FAILS FOR FOUR INDEPENDENT REASONS — wrap, hyphen, form feed, and
  markdown emphasis in .mdx. The fourth survives a perfect download.
SUB-RULE (20th): *** NEVER WRITE A NUMBER, QUOTATION OR THRESHOLD FROM AN OPEN-ENDED WebFetch. ***
  Run a second call demanding VERBATIM sentences per figure, with an explicit "or say NOT STATED".
  A FIFTH mechanism for a wrong result and the only one producing a confident POSITIVE.
  COROLLARY: where a page is browser-readable, `get_page_text` returns RAW text with no model in the
  loop — prefer it over WebFetch for any number-heavy page, even when WebFetch works.
SUB-RULE (20th): *** A POSITIVE GREP IS AS WEAK AS A NEGATIVE ONE WHEN THE CLAIM IS ABOUT MEANING. ***
  READ THE HITS, DO NOT COUNT THEM.
SUB-RULE (20th): *** IF A PAGE SAYS A RULE IS SPECIFIED ELSEWHERE, YOU HAVE NOT READ THE RULE. ***
SUB-RULE (20th): *** A QUANTIFIER OVER A STRUCTURE YOU DID NOT REPRODUCE IS UNCHECKED. *** Go back
  to the structure and COUNT.

WHAT THE VERIFICATION PASS ACTUALLY FINDS — THIRTEEN RUNS OF EVIDENCE. Mostly NOT stale facts. It
finds CITATION-FIDELITY and COMPLETENESS defects in facts whose underlying claims are correct:
  ninth      — 56986e8f: a paraphrase wearing quote marks.
  tenth      — c93d93ee: an overclaiming gloss attributed to the source.
  tenth      — c7290868: INVERTED CAUSATION pointing at the wrong remedy.
  eleventh   — 96ebc34e: BOTH at once, and the gloss reversed the blame.
  eleventh   — c858a924: WRONG ACTOR — 'independent auditors' were two LLM judges, not humans.
  twelfth    — 30869b36: a pack gloss wearing quote marks ('combined surface area').
  twelfth    — c436422a: WRONG TERMS attributed to the source (brain/hands/session).
  thirteenth — f78a326a: WRONG TERM + one instance generalised into a rule.
  thirteenth — 38c06627: MISATTRIBUTION ACROSS A FACT'S OWN TWO REFS.
  fourteenth — d18637a2: MODAL STRENGTHENING + a scope error.
  fifteenth  — f7dee43a AND 9aaea0dc: MODAL STRENGTHENING, the same quotation, in two facts.
  fifteenth  — 714a540c: ATTRIBUTION TO AN UNLISTED REF + a language-binding error.
  fifteenth  — b4d688b1: MODAL STRENGTHENING IN A TITLE, in a fact written that same run.
  fifteenth  — 0720e9d7: A PDF LINE-WRAP SILENTLY RECONSTRUCTED and printed as a literal.
  sixteenth  — 59a75c06: A TITLE THE SUCCESSOR REVISION EXPLICITLY CONTRADICTS. First genuine
    STALENESS rather than citation infidelity — the fact was right when written.
  sixteenth  — b471f9ef: AN OVERCLAIMED ABSENCE concealing a MUST silently downgraded to SHOULD.
  sixteenth  — 11ebefd6 (own): A QUANTIFIER INFLATED IN A TITLE — 'most' for seven of sixteen.
  sixteenth  — db15af92 (own): AN UNCHECKED VERSION ATTRIBUTION.
  sixteenth  — 8f2fdde8 (own): A TITLE CLAUSE THE FACT'S OWN BODY UNDERCUT.
  seventeenth— ca3382bd AND 46eeb374: SOURCE-COUNT INFLATION — N pages of ONE spec counted as N sources.
  seventeenth— 703147ba (own): AN INCOMPLETE MAPPING, plus a METHOD SENTENCE that vouched for it.
  seventeenth— 8cf06566 (own): A CONTAMINATED COUNTING RANGE, AND WRONG EVIDENCE FOR A CORRECT
    CONCLUSION. Re-derived independently the 18th run from the primary: the correction HOLDS.
  seventeenth— ba1b7aad (own): A TENSE-ALTERED QUOTATION ('operating' for 'operates').
  eighteenth — 406e5a50: A TABLE OF DURATIONS WITH NO START EVENTS. CLASS: OMISSION OF THE FRAME.
  eighteenth — 2d060289: A SUPERLATIVE TRUE ONLY WITHIN A SUBSET.
  eighteenth — 30543305 (own): MODAL OVERCLAIM IN A TITLE. Confirmed correct by the successor post.
  eighteenth — 1719fe66 (own, REVIEW PASS): A FALSE METHOD CLAIM ('independently re-derived').
  eighteenth — bdb36fce (own, REVIEW PASS): AN INCOMPLETE SWEEP DESCRIBED AS EXHAUSTIVE.
  eighteenth — ce7e0330 (own, REVIEW PASS): TWO UNMARKED INFERENCES adjacent to quoted MUSTs.
  nineteenth — f4bba0ae: THREE DEFECTS IN ONE FACT, all attribution blur.
  nineteenth — eae23eac: ATTRIBUTION TO AN UNLISTED REF, second occurrence of the 714a540c class.
  nineteenth — 74996815: THE FIRST UNDERCLAIM — a fact that penalised its own confidence wrongly.
  nineteenth — 30543305 (own, REVIEW PASS): TWO SOURCE CLAIMS JOINED INTO ONE.
  *** twentieth — 19ed6273: A FABRICATED PERCENTAGE ('~15%' of BrowseComp variance). NEW CLASS AND
    THE MOST DANGEROUS ONE FOUND SO FAR, because nothing about it looks wrong: the fact's every other
    number is exact, and the invented one COMPLETES A SET (80% + a remainder). ***
  *** twentieth — 70127cdd: THE SAME CLASS AGAIN ('(2-4 seconds)') AND, in the same fact, A SECOND
    UNDERCLAIM — a named, directly-quoted vendor mitigation hedged as 'reportedly'. ***
  *** twentieth — a13a57c9: A FABRICATED IDENTIFIER — a tool name that appears nowhere in the source
    recorded as one of two defaults, where the true default is one tool. ***
  twentieth  — 0b340b6b: A PARAPHRASE WEARING QUOTE MARKS (sixth occurrence) plus an unmarked pack
    inference — and the invented quote pointed the OPPOSITE WAY from the source's actual advice.
  twentieth  — ac887ec9: PACK PRESCRIPTION READING AS SOURCE PRESCRIPTION.
  twentieth  — f4367bd0 (own): MODAL STRENGTH LOST TO A DELEGATED RULE, and (REVIEW PASS) A ROW COUNT.
  *** twentieth, FROM THE knomit_review SESSION — 0f260eea AND 1d1440fe: A DISTILLED SYNTHESIS
    CARRYING A CLAIM ITS SOURCE FACT HAS SINCE RETRACTED OR CORRECTED. NEW CLASS, AND THE ONLY ONE
    THIS JOB CANNOT REPAIR (kb/principles is write-blocked). Flagged by confidence; bodies unfixed. ***
CHECKLIST — verify all SEVENTEEN explicitly, not just 'is the claim still true':
  (1) quotation boundaries — VERBATIM INCLUDING TENSE AND INFLECTION, and does the quote START where
      the source's sentence starts;
  (2) causal direction; (3) WHO the actor is in a cited measurement (human vs model vs tool);
  (4) what the pronoun refers to — AND WHETHER THE SOURCE DISAMBIGUATES IT AT ALL;
  (5) are the TERMS attributed to the source actually the source's terms;
  (6) refs classification and `sources` counts — N pages of ONE specification is ONE source;
  (7) FOR MULTI-REF FACTS, which specific ref supports each specific number. A claim can be TRUE,
  from the SAME vendor, and still be cited to the wrong post;
  (8) MODAL STRENGTH, QUANTIFIERS AND SCOPE, IN THE BODY AND IN THE TITLE SEPARATELY;
  (9) LANGUAGE BINDING AND VERSION for anything from framework or vendor docs;
  (10) LITERALS FROM A PDF ARE RECONSTRUCTIONS, and a negative grep is unreliable for FOUR reasons.
  Distinguish PACK ANALYSIS from SOURCE CLAIM — a gloss next to a citation gets read as cited;
  (11) VERSION ATTRIBUTION IS A CLAIM. Check the WHOLE predecessor revision, every tree. A surviving
  TOKEN is not a surviving MEANING — read the hits, do not count them;
  (12) A FACT'S STATEMENT OF ITS OWN METHOD IS THE CLAIM MOST LIKELY TO BE FALSE — and the error is
  not always flattering;
  (13) RE-RUN EVERY COMPUTATION AND RE-DERIVE EVERY CROSS-DOCUMENT INFERENCE;
  (14) DOES EVERY NUMBER CARRY ITS FRAME? A duration needs its start event, a percentage its
  denominator, a count its region, a superlative its population, A RELATIVE DELTA ITS BASELINE;
  (15) RE-RUN THE SEARCH ITSELF — inspect its ANCHOR and its SCOPE, and match the scope to the
  CLAIM'S SUBJECT NOUN;
  (16) DID YOU JOIN TWO SOURCE CLAIMS THAT THE SOURCE KEPT APART? Where the source offers both a LIST
  and a COUNT of it, count the list;
  (17) *** IS THIS SPECIFIC ACTUALLY IN THE SOURCE, OR WAS IT INVENTED TO COMPLETE A SET? ***
  Percentages that are the remainder of another percentage, ranges around a qualitative duration,
  denominators of a ratio, identifiers in a list of defaults. Three instances in one five-fact
  sample. The tell is that the figure makes the claim tidier, and every OTHER figure in the fact is
  correct — so partial verification actively misleads. Verify the specifics ONE AT A TIME against a
  verbatim-demanding read. AND CHECK THE SYNTHESES THAT CONSUMED THE FACT.
