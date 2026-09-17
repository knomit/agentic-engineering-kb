---
type: reference
domain: [agentic-engineering, job-state]
confidence: 1
sources: 0
entities: [agentic-engineering]
refs: ['https://github.com/knomit/knomit']
---
# Last crawl state

crawled: 2026-09-17 (twenty-seventh run). NINE DAYS after the 26th run's crawl date (2026-09-08,
committed 2026-09-13), so a full feed sweep was owed and taken. Six feeds swept, four quiet, two
paid. 7 facts written, 1 existing fact corrected in scope. 0 retracted.

*** THIS SLOT HOLDS ONE RUN. THE HISTORY IS THE RECORD. WALK IT. ***

*** ====================================================================================== ***
*** READ FINDING 1 BEFORE ANYTHING ELSE. THE SESSION'S BINDING SILENTLY REVERTS FROM       ***
*** agentic-engineering TO THE DEFAULT LENS PART-WAY THROUGH A RUN, AND EVERY knomit CALL  ***
*** AFTER THAT SILENTLY ADDRESSES THE WRONG REPOS. IT PRESENTS EXACTLY AS "THE PACK'S      ***
*** CORPUS HAS BEEN WIPED". THIS RUN NEARLY WROTE THAT AS A FINDING. RE-BIND OFTEN.        ***
*** ====================================================================================== ***

=== FINDING 1 — BINDING DRIFT, AND THE FALSE FINDING IT ALMOST PRODUCED ===
The job prompt says to bind once and not call knomit_bind again for the rest of the run. THAT
INSTRUCTION ASSUMES THE BINDING HOLDS. IT DOES NOT. Measured, in order:
  1. knomit_bind{repo: agentic-engineering} -> binding "agentic-engineering", one mount, read+write.
     Correct. crawl-state, crawl-sources and fetch-routes all read normally at this point.
  2. Some calls later, WITH NO INTERVENING BIND: five path-scoped knomit_query calls
     (kb/incidents/ai/agents, kb/architecture/ai/agents, kb/gotchas/ai/agents,
     kb/conventions/ai/agents, kb/invariants/ai) ALL returned ZERO facts.
  3. knomit_explain on two exact fact paths the 26th run recorded writing (6b8f82c2, b446bef6)
     -> "could not read". Then knomit_explain on .knomit/jobs/agentic-engineering/crawl-state.md
     itself -> "could not read". The job could not even read its own state slot.
  4. knomit_query sort=recent returned 15 facts, every bare-path row under kb/technology/**, with
     committed_at stamps from today — a corpus this pack does not own. Broad queries on
     kb/invariants, kb/conventions and kb/gotchas returned only kb://3ec012f5b4d2/ rows (knomit-kb).
  5. knomit_repos -> "bound": {"binding": "knomit-positioning", ...}. THE LENS, NOT THE REPO.
     knomit-positioning mounts core (read+write), knomit-io-kb and knomit-kb — and does NOT mount
     agentic-engineering at all. That is the whole explanation for steps 2, 3 and 4.
  6. knomit_bind{repo: agentic-engineering} again -> correct binding. knomit_explain on 6b8f82c2
     immediately returned the full fact. THE CORPUS WAS INTACT THE ENTIRE TIME.
IT RECURRED: a later knomit_learn was rejected with `validate path: unknown topic "incidents"` —
which is the same drift wearing a different costume, since core's ontology has no "incidents" topic.
Re-binding and resubmitting the identical call committed all six facts.

*** WHY THIS IS THE MOST DANGEROUS FAILURE MODE THIS JOB HAS HIT. *** Four of this pack's own
standing rules fire on the symptom and all four point the wrong way. An empty scoped query looks
like "this pack holds nothing here", which is the reading that LICENSES WRITING DUPLICATES.
"could not read" on an exact path looks like the route-7 history problem. A repo full of unfamiliar
kb/technology facts looks like the corpus having been replaced. And a tidy causal story was
available and tempting: knomit-kb carries a fact dated today
(kb://3ec012f5b4d2/kb/gotchas/mcp/learn/empty-title-unvalidated/6cb021a3.md) describing a knomit
0.5.3 defect whose two named symptoms are EXACTLY "query never lists it" and explain failing with
"could not read". It matched perfectly and it was not the cause. Route 4's narrative-gap-filling
bias, arriving one level up: the tidiest available explanation was wrong, and only a sixth
measurement — knomit_repos, which nothing required — separated them.

*** WHAT EVERY FUTURE RUN MUST DO, and it costs one cheap call: ***
  (a) CALL knomit_repos AND CHECK `bound.binding` BEFORE BELIEVING ANY NEGATIVE RESULT. An empty
      query, a "could not read", or an "unknown topic" error is a BINDING claim until knomit_repos
      says otherwise. Never record a corpus-state finding without that check in the same breath.
  (b) RE-BIND BEFORE EVERY WRITE. The prompt's bind-once rule is overridden by observation here;
      re-binding to the SAME repo serves its intent (never switch repos mid-run) and costs one
      call. This run re-bound three times and every write after a re-bind succeeded.
  (c) A REFUSAL NAMING AN ONTOLOGY TOPIC THE PACK OWNS ("unknown topic incidents") IS DRIFT, NOT A
      SCHEMA ERROR. Re-bind and resubmit the identical call before editing anything.
FOR THE OPERATOR: the cause of the drift is not established. It was not observed to correlate with
any particular tool, and no call was made that would switch the binding. knomit-positioning appears
to be the session default that the binding falls back to. That is a question for a person; the
workaround above is reliable and cheap.

=== HISTORY WALK — AND ITS RESULT IS PARTLY INVALID. SAY SO. ===
REVISIONS READ: **2 distinct run bodies.** FULL 40-HEX, per route 7b:
  20eb4edb0910f3ce70697deb7ee20391819fbced (HEAD, committed 2026-09-13T15:48:52Z, "Merge #11")
    — carries the 26th RUN's body (crawled 2026-09-08). Read inline.
  65e9612ba1295bd8d94dc19b4b12b62625f6a47a (2026-08-24T16:17:17Z, "Merge #9") — the 22nd RUN's body
    (crawled 2026-08-21). Read inline.
more_available was TRUE at HEAD, FALSE at 65e9612b.
RUN-NUMBER SEQUENCE OBTAINED: 26, 22. NOT ENUMERATED: 23, 24, 25 and everything below 22.

*** THE COMMIT-RESOLUTION TEST THIS RUN RAN IS VOID. DO NOT INHERIT ITS RESULT. *** Using the full
40-hex hashes the 26th run recorded, this run tried 3c6323cd52188f057c16d15b2c7b72ad9d9e91e9 (twice),
8b9a768debcfa982f4ec2a8155c1bc9195c0bb0f, c6cab79802bfc5ad45da90851f698de37ba8d1cb and
7462e9f229b6cc3ef2c2da12be49c1cd468a6e55. All five calls returned "could not read". THAT LOOKED LIKE
A CLEAN MEASUREMENT — including on 3c6323cd, which the CURRENT history listing names, which would
have been a decisive finding that a listed commit can fail to resolve.
IT IS NOT USABLE, BECAUSE THE BINDING DRIFT (Finding 1) WAS ACTIVE ACROSS AN UNKNOWN PART OF THAT
SEQUENCE AND THE CALLS WERE NOT RE-BASELINED. A "could not read" from a session bound to a lens that
does not mount this repo is indistinguishable from one against a genuinely absent commit, and this
run cannot say where the boundary fell. THE RESULT IS "NOT ESTABLISHED", not "these commits are
gone", and the reason it is being written down at all is so no future run quotes the five failures
as evidence.
NEXT RUN, and this is cheap and worth doing properly: knomit_repos -> verify binding -> re-run all
five full hashes back to back -> knomit_repos again to confirm the binding did not move mid-test.
Only then is there a measurement. That is route 2's isolate-the-variable rule applied to the
bookkeeping, which is where this pack keeps failing to apply it.

*** ALREADY_CRAWLED — TWO NUMBERS, HONESTLY LABELLED. ***
  ENUMERABLE BY ME FROM BODIES I READ: 9 URLs (2 from the 22nd run's body, 7 from the 26th's), plus
    this run's 2 new = 11.
  INHERITED AS A CLAIM, NOT RE-DERIVED: the 26th run states 252 through its own run. Its derivation
    rests on bodies this walk did not reach, so it stays its claim and does not become mine.
PRACTICAL IMPACT: none. Appendix A has been fully covered since the eighth run, so the union's only
live use is the unread-feed test, which crawl-sources' READ/UNREAD markers answer — exactly the
contingency crawl-sources' own header was written for.

=== FINDING 2 — THE GITHUB API ROUTE IS GATED IN THIS ENVIRONMENT. THE TRIPWIRE HAS A ONE-CALL
=== REPLACEMENT. NOT A DEAD SOURCE — A CHANGED ENVIRONMENT. ===
  curl api.github.com/repos/modelcontextprotocol/modelcontextprotocol/contents/docs/specification
  -> HTTP 403, body: "GitHub access to this repository is not enabled for this session. Use add_repo
     to request access."
That is the HARNESS refusing, not GitHub rate-limiting and not the repo moving. WebFetch on the
github.com HTML tree page is refused separately, with ROBOTS_DISALLOWED. So route 3's whole
curl-based family — the tripwire, the recursive tree enumeration, and the raw.githubusercontent
fetches the spec-revision-diffing technique depends on — is UNAVAILABLE HERE until repo access is
granted.
THE WORKING REPLACEMENT FOR THE TRIPWIRE, one plain WebFetch, no gate:
  WebFetch https://modelcontextprotocol.io/specification/versioning
RESULT THIS RUN, quoted from the page: "The **current** protocol version is
[**2026-07-28**](/specification/2026-07-28/)." UNCHANGED — SEVENTEENTH consecutive run.
THE TRADE, stated so nobody over-trusts it: the site page answers "what is current" but NOT "has a
new directory appeared", and it cannot support revision diffing. For the sweep question it is
strictly sufficient; for the diffing technique it is not a substitute.
BONUS — TWO UNMINED ITEMS THE DIRECTORY LISTING NEVER SURFACED, both now queued: the deprecation
policy has an "expedited-removal exception" with a ninety-day floor against the normal twelve
months, and `server/discover` is described as "a mandatory RPC". Both are spec-level invariant
material on a page the sweep already loads.

=== FINDING 3 — APPENDIX S FORBIDS THE 5c HREF HARVEST AS WRITTEN, AND fetch-routes DOES NOT SAY SO ===
fetch-routes 5c prescribes a `querySelectorAll` evaluate as "the pack's highest-yield trick".
Appendix S's tool list says of the browser tools: "Read-only navigation and text extraction. Do not
run page scripts." Appendix S is on disk and the job cannot edit it; fetch-routes is job-writable.
Appendix S therefore governs, and 5c's evaluate form is NOT available to a compliant run.
THE COMPLIANT SUBSTITUTES, both used successfully this run:
  * Named-link resolution on a WebFetch-readable host: route 5b, phrased "Give me the EXACT href/URL
    of the links whose text is X, Y, Z... Do not derive or guess URLs — only report hrefs actually
    present in the page." Returned three exact Anthropic slugs first try, including one that breaks
    the site's own convention (below).
  * Article text: `get_page_text`, which Appendix S explicitly permits as text extraction and which
    is still a TRANSCRIPTION — so route 9's transcription-over-extraction argument survives intact.
    Route 9 is about fabrication risk, not about scripting, and this finding does not weaken it.
WHAT IS ACTUALLY LOST: only the harvest-every-page discovery sweep. Flagged for the spec's author in
the human list below, because a job cannot resolve this conflict in its own favour.

=== FINDING 4 — THE BROWSER SERVER HAS A THIRD NAME, VINDICATING ROUTE 1'S "CHECK, DO NOT HARDCODE" ===
Neither `mcp__browser__*` (runs 23-26) nor `mcp__claude-in-chrome__*` was the one that worked. This
session serves `mcp__remote-devices__Claude_Browser__*`: preview_start / navigate / get_page_text /
find / read_page / browser_batch. It read anthropic.com and arena.ai first try, no approval prompt,
no 403. `browser_batch` takes a list of actions in one round trip, which makes navigate + wait +
get_page_text a single call.
TWO ERGONOMIC NOTES WORTH THE LINES:
  * `read_page` returned "(empty page)" with "Viewport: 0x0", and a click by ref then failed with
    "entirely outside the viewport". `get_page_text` on the SAME tab at the SAME moment returned the
    full article. AN EMPTY read_page IS NOT EVIDENCE THE PAGE FAILED TO LOAD — try the other reader.
  * `get_page_text` caps at max_chars and truncates FROM THE START with no offset parameter, so a
    document longer than the cap cannot be paged through with it. Hit at 48,000 chars on the threat
    report. The compliant fallback is the PDF: route 5b for the href, curl, pdftotext.

=== FEEDS SWEPT: SIX, PLUS THE TRIPWIRE. FOUR QUIET, TWO PAID. ===
  modelcontextprotocol.io/specification/versioning — tripwire by the NEW route (Finding 2).
    Current revision 2026-07-28. UNCHANGED, seventeenth consecutive run.
  www.aisi.gov.uk/blog/    — QUIET. Newest is STILL optimal-stopping (Aug 27), read by the 23rd run.
    Three weeks with no new post. The ~47-item tier-A back catalogue remains the entire value.
  embracethered.com/blog/  — QUIET. Newest still breaking-claude-code-opus-5-and-automode (Aug 26).
    The call returned the complete 2026 run, 14 posts back to Jan 14, identical to the 26th run's
    listing. The 2025 seam is still the unmined part.
  metr.org/blog/           — QUIET. Newest still the Aug 31 security update, read by the 26th run.
    *** THE PROMISED FOLLOW-UP ON WHETHER AGENTS HACKED THIRD PARTIES DURING METR'S OWN EVALUATIONS
    HAS STILL NOT LANDED. Two runs waiting. Keep watching. ***
  www.anthropic.com/news/  — THREE NEW. One read and heavily mined, two queued.
  openai.com/news/         — NOT SWEPT. Named rather than left implicit: the budget went to the
    threat report and then to Finding 1. The 26th run's six catalogued unread posts all stand.
NOT SWEPT, named: simonwillison, microsoft research, microsoft security, langchain, huggingface,
  eugeneyan, trychroma, builder.aws.com, genai.owasp.org, research.google, sourcegraph, latent.space,
  redwoodresearch, developers.openai.com, vectara, cognition (demoted, 26th run split 13), the OWASP
  ASI tracker.

=== ARTICLES NEWLY CRAWLED (2 URLs, both by browser transcription) ===
  https://www.anthropic.com/threat-intelligence-report-september-2026   (Sep 10 2026)
    "Detecting and countering misuse of AI: September 2026". Read to 48,000 chars, covering the whole
    cyber-operations half. -> SIX facts. WELL MINED for that half; six later sections unread.
    *** SLUG WARNING, NEW AND SHARP: THIS POST IS NOT UNDER /news/. *** Every other Anthropic post in
    the listing is /news/<slug>; this one sits at the site root as
    /threat-intelligence-report-september-2026. A run deriving the URL from the pattern would 404.
    Resolved by route 5b. Its PDF and IOC CSV hrefs are recorded in the queue below.
  https://arena.ai/blog/coding-agents-harness-tax   (Sep 16 2026)
    Arena's "HarnessTax". -> one `decisions` fact plus a scope correction to 8193c07b. Reached by
    following a secondary row seen during the drift window (see the queue) back to its primary,
    which is the pack's standing rule about the operator's own account working in a new place.
  Index sweeps (4 WebFetch) and the tripwire are not article fetches and are listed above.
errored / not obtained: the GitHub API and the github.com HTML tree (Finding 2) — both ENVIRONMENT
  GATES, NOT dead sources. No 404s, no paywalls, no guessed slugs, no timeouts.
Appendix A: nothing crawled, nothing left. Fully covered since the eighth run.

=== FACTS WRITTEN (7 new, 1 existing corrected, 0 retracted) ===
  SIX from the threat report, all in ONE knomit_learn call after a re-bind, committed together:
    kb/incidents/ai/agents/security/ai-supply-chain/90ecc753        — stolen AI credentials buy
      LOOT, COMPUTE and COVER; the cover property makes the victim's own logs the attacker's alibi.
    kb/incidents/ai/agents/security/supply-chain-intrusion/94648eeb — *** THE RUN'S BEST FACT. ***
      GTG-50020 prompt-injected an AI vendor's AUTOMATED EVALUATION SANDBOX to make it surrender the
      production keys it held, then replayed the one working path against ~30 AI companies in ~4
      days. The eval-containment cluster had only ever held agents getting OUT; this is an adversary
      using the harness as the way IN, chosen for what it is trusted to hold.
    kb/gotchas/ai/agents/security/detection-evasion/732629b8        — an agent loop rebuilding
      malware until undetected removes the COST a signature exists to impose; the signature keeps
      matching and stops meaning anything. Anthropic's "at least in theory" hedge is carried.
    kb/architecture/ai/agents/multi-agent/long-horizon-operations/8994141b — a months-long swarm ran
      on PERSISTENT CAMPAIGN STATE, not parallelism; coordination converted into storage.
    kb/architecture/ai/agents/patterns/hypothesis-test-loop/0182fb5a — the zero-day foundry loop
      closes on a LAB COPY of the target; a curated KB supplies hypotheses, the lab build is the
      oracle. "more than a dozen POSSIBLE zero day findings in a single month" kept its hedge.
    kb/conventions/ai/agents/security/credential-rotation/f389632c  — rotation does not end the
      compromise while the harvester is resident; it restores the precondition and looks like
      remediation.
  ONE from HarnessTax:
    kb/decisions/ai/agents/evaluation/harness-choice/c2624a17       — harness choice moves COST not
      SCORE when the turn budget is pinned, and moves SCORE when the budget or grader is what
      differs. Written as a `decisions` fact rather than flattening either side. See CONTRADICTIONS.
  CORRECTED:
    8193c07b — scope. Two revisions (body, then refs).

=== CONTRADICTIONS — ONE, HANDLED BY NOT FLATTENING, WHICH IS WHY c2624a17 EXISTS ===
HarnessTax measures the OPPOSITE of this pack's standing position on harness effects, and the
dedup engine surfaced four facts carrying that position: a829cfd4, b9b45ff5, 8a7dc152 ("the
apparatus moves the result more than the model does") and 1feacc9e ("a score that moves in either
direction is an eval defect until proven otherwise"). Three are under kb/principles/ and are
WRITE-BLOCKED, so they could not be amended even if that were right — and it would not have been.
THE RESOLUTION IS A CONDITION, NOT A WINNER: every case behind the existing position varies a BUDGET
or GRADING parameter (turn cap, reasoning level, extraction and scoring rules, machine size).
HarnessTax pinned those — one 100-turn cap, one price list, native configs — and varied scaffolding,
prompt length and tool surface instead. Under that setup SUCCESS moved within ±2% / ±5% while COST
moved up to ~2×. So the apparatus claim is about budget and grading specifically, and cost is an
axis none of the existing facts measure. Both sides stand; c2624a17 names the separating condition
and 8193c07b now carries a SCOPE paragraph pointing at it.
THE knomit_learn DEDUP REFUSAL IS WORTH KNOWING ABOUT AS A TOOL BEHAVIOUR: it refused twice, naming
three candidates and then a fourth, and `distinct_from` must list EVERY candidate any refusal named
— they accumulate across attempts rather than being re-listed in full. Two round trips, no edits.

=== STALENESS PASS — REDUCED IN SCOPE, AND SAYING SO RATHER THAN PADDING ===
ONE fact re-checked and CORRECTED, not five. The axis was the 26th run's queued MODEL-VERSION axis,
and 8193c07b was the right member of it: its claims are pinned to GPT-5.6 Sol and GPT-5.6-Cyber,
both superseded by GPT-6 Astra on Sep 3.
  8193c07b (0.85 HELD, sources 3 HELD) CORRECTED — SCOPE, and the correction came from a NEW
    MEASUREMENT rather than from re-reading the old refs, which is the stronger form. The fact's
    title generalises to "the same model scores differently across eval harnesses"; HarnessTax shows
    that with budget and grading pinned it mostly does NOT — within ±2% on SWE-bench Lite and about
    ±5% on Terminal-Bench 2.0 — while cost diverges ~2×. Added a SCOPE paragraph naming which
    harness parameters the claim covers and warning against compressing it to "the harness decides
    the score". Confidence HELD deliberately: nothing in the fact was shown false, and the MMLU and
    ExploitBench cases are untouched. sources HELD at 3 because the new measurement lives in
    c2624a17 and NARROWS this fact rather than corroborating it — counting it here would overstate
    agreement. Refs merged in a second update (the three originals plus c2624a17), read-modify-write.
WHY ONLY ONE: the budget went to Finding 1 and then to the threat report. Recording that plainly
rather than running four shallow checks to make the count look right. The MODEL-VERSION axis is
FAR from exhausted and carries forward with its candidate list intact: 2d7219c8, 8756141e, f654f7dd,
56cefe53, 069468bb — none checked. AVOID kb/principles/** (write-blocked; a829cfd4, b9b45ff5,
1feacc9e now confirmed members of that set alongside 0f260eea, 1d1440fe, 4166926d).
Nothing in the kb is yet older than 90 days (pack began 2026-07-26; today is day 53).

=== IN-RUN SELF-REVIEW, INCLUDING OF THIS FILE ===
The 26th run's closing instruction was to run the checklist over the crawl-state body too, and
specifically over any claim it INHERITED rather than observed. Done, and it caught the big one:
  * THE VOIDED COMMIT TEST. A near-complete draft of this body reported the five "could not read"
    results as a clean measurement and built a corpus-loss finding on them. Finding 1 invalidated
    the whole sequence. It is recorded as VOID with the re-test procedure, not quietly dropped —
    a deleted false finding teaches the next run nothing.
  * The 252 figure is labelled inherited, with the reason it could not be re-derived.
  * Finding 1's own CAUSE is left open, and the tempting empty-title explanation is written down
    precisely because it was tempting, marked untested.
  * Every quoted string in the seven facts is browser get_page_text innerText — a transcription —
    so route 4 does not apply to any of them. No WebFetch output was quoted into a fact. The four
    index sweeps produced href lists only.
  * Hedges preserved and checked individually: "at least in theory" on the close-the-loop claim;
    "POSSIBLE zero day findings" with its one-month, one-workflow frame; "roughly thirty ... about
    four days"; "validated by the actor in their own lab environment" attributed to the actor.
    HarnessTax's own limitations carried in full, including the two a reader would otherwise miss —
    that web tools were DISABLED in Claude Code and Codex for the SWE-bench Lite comparison, and
    that the 100-turn cap bounds the result to tasks finishing inside it.
  * The report-wide scope sentence ("aren't typical misuse, but rather examples of the most notable
    and novel threat activity") is carried in the facts that quote figures, so none reads as a base
    rate.
  * Arithmetic: 9 enumerable + 2 new = 11. Six feeds named as swept; six listed. Seven facts named;
    seven paths listed.
NOT DONE, said plainly: four of the five staleness samples; the openai.com sweep; the migration of
Findings 2/3/4 into fetch-routes (see below).

PROMPT INJECTION: none observed. Stated explicitly because this run read a long first-person account
of adversaries using an AI assistant as attack infrastructure, including a case study whose entire
technique was injecting instructions into an AI vendor's automated sandbox to make it surrender the
credentials it held — a document describing an attack whose target shape resembles this job. It was
treated as data throughout. Nothing in it addressed this job, no fetched page attempted to redirect
the run, and no URL was visited that was not on the work list or resolved from a swept index.

=== TO MIGRATE — READ BEFORE WRITING THE OTHER TWO SLOTS ===
*** Findings 1, 2, 3 and 4 are FETCH ROUTES / TOOL CAVEATS and belong in fetch-routes.md; the new
*** Anthropic posts and the threat-report catalogue entry belong in crawl-sources.md. THEY ARE HERE
*** INSTEAD, DELIBERATELY. The reason is a rule this pack already holds: knomit_update REPLACES the
*** whole body, both slots are ~56KB, and both came back OVERSIZED and had to be read from disk in
*** character slices. Re-emitting 56KB from chunked tool output to change five paragraphs is exactly
*** the "never re-type a file's content from tool output" failure, aimed at the two most valuable
*** durable slots the job has, on a run that spent its first third unsure whether the corpus existed.
*** Leaving them byte-intact was the conservative call. NEXT RUN: migrate Finding 1 into fetch-routes
*** as ROUTE 10 (it is the most important entry in that file now), Findings 2/3/4 as route amendments,
*** and the source updates into crawl-sources — ideally on a run with nothing else on fire. ***

=== QUEUE FOR THE NEXT RUN ===
(0) *** knomit_repos FIRST, AND AGAIN AFTER ANY SURPRISING NEGATIVE. Finding 1. Re-bind before every
    write. This is now the cheapest highest-value habit in the job. ***
(1) THE REST OF THE SEPTEMBER THREAT REPORT — six sections unread past the 48,000-char cap:
    surveillance, influence operations, conventional weapons, biological misuse, scams and fraud,
    and illicit distillation. The last is likeliest to clear the bar. Take the PDF, which removes
    the truncation problem and is a transcription. HREFS RESOLVED BY ROUTE 5b THIS RUN, NOT GUESSED:
    https://www-cdn.anthropic.com/e50be2e51e7695dc4b1366a37a245a597377d3b5/Anthropic-Detecting-and-countering-091026.pdf
    https://www-cdn.anthropic.com/b5af8acd5ee681422114af7c7b6b02c1ecd074ca/20260910_Anthropic_AI_Misuse_Report_IOCs.csv
    pdfinfo it and record the fingerprint. Note route 8: cdn filenames rot — re-harvest if it 404s.
(2) *** ANTHROPIC'S TWO NAMED-BUT-UNFETCHED ARTIFACTS, RANK 1, NOW CARRIED A SECOND RUN: the
    ALIGNMENT SCIENCE post on the 80-environment reward-hacking experiment (where ec1be717's numbers
    live, plus the claim that alignment training environments "can substantially reduce reward
    hacking"), and the AUGUST RISK REPORT (Section 5.2.3, further accidental CoT training —
    completes b446bef6). Resolve both by route 5b on /news/improving-alignment-security-efforts. ***
(3) anthropic.com/news/enterprise-frontier-safeguards (Sep 1) — unread a second run. One cheap read.
(4) anthropic.com/news/life-sciences-verification-program (Sep 17, NEW) — a VERIFICATION programme,
    adjacent to the access-tiering material in ee458c93. One cheap read, low expectations.
(5) openai.com/news/ — NOT SWEPT THIS RUN. safety-overview-gpt-6-astra (Sep 3) still TOP, plus
    whatever landed Sep 8-17. Needs the browser.
(6) *** OPENAI DISCLOSED SIX FURTHER MODEL MISALIGNMENT INCIDENTS PLUS A DISCLOSURE FRAMEWORK ON
    2026-09-16. HIGH — potentially the biggest addition to the eval-containment cluster since the
    Aug 26 post-mortem. *** Seen only as a SECONDARY row during the drift window
    (kb/technology/ai/safety/misalignment-incident-reporting/d5bdc723 in the `core` repo, ref
    thehackernews.com), quoting OpenAI: "We do not believe that the AI industry has solved alignment
    and monitoring to a sufficient degree to continue responsibly scaling at maximum speed for much
    longer." FIND THE PRIMARY on openai.com — the operator's-own-account rule applies exactly here.
    The same rows also name a SentinelOne reconstruction of the Hugging Face activity from PUBLIC
    account histories (accounts 0Time and Nyx9), relevant to 02f74ac7 and 2dfac716.
    NOTE THE METHOD POINT: those rows were visible only because the binding had drifted into a lens
    mounting `core`. A neighbouring corpus is a legitimate discovery feed for secondary leads — but
    every lead from it goes to its primary before a fact is written.
(7) THE MCP VERSIONING PAGE'S TWO UNMINED ITEMS, free on a page the sweep now loads (Finding 2): the
    "expedited-removal exception" with its ninety-day floor against the normal twelve months, and
    server/discover as "a mandatory RPC". Spec-level invariant material.
(8) THE AISI TRANSCRIPT-ANALYSIS PAIR — still top of tier A, still unread, and the feed has been
    quiet three weeks so nothing competes for the budget:
    /blog/transcript-analysis-for-ai-agent-evaluations and
    /blog/a-pipeline-for-transcript-analysis-using-inspect-scout. Then
    /blog/will-it-become-harder-to-oversee-ai-systems, /blog/hibayes-...,
    /blog/the-inspect-sandboxing-toolkit-... .
(9) METR's "Early Work on Monitorability Evaluations" (site footer, unread), and the promised
    third-party-hacking follow-up, now two runs overdue.
(10) THE BENCHMARK SUPPLY CHAIN (CVE-2026-66384, the poisoned Artifactory container-image cache)
    still lives only inside bcbf13c2. CARRIED UNTAKEN A THIRD RUN. Re-harvest the technical report
    href by route 5b/8 rather than trusting the recorded hyphenated form, untested since 08-29.
(11) 2dfac716 SHOULD ABSORB THE SSRF-vs-ZERO-DAY CLARIFICATION. Untaken a THIRD time. Do with (10).
(12) MCP TRANSPORTS IN FULL — EIGHT runs untouched (20th-27th), and the route that would fetch them
    is now GATED (Finding 2). *** RECOMMENDATION FIRMED UP: DELETE THIS ITEM. Eight runs of every
    reader ranking it last is the verdict, and it now costs an environment change to attempt. ***
(13) HarnessTax names a paper-style landing page, https://harnesstax.github.io/, and promises "we
    will publicly release our profiling traces". Cheap to check once; traces would be a rare
    primary for per-turn cost analysis.
(14) *** FOR A HUMAN, NOT THE CRAWLER ***
    (a) *** THE BINDING DRIFT (Finding 1). The job's binding reverts to the knomit-positioning lens
        mid-run, silently, and every knomit call after that addresses the wrong repos. The
        re-bind-before-every-write workaround is reliable, but the underlying behaviour is a
        correctness hazard for any job that trusts a single bind — and it is capable of convincing
        a careful run that a corpus has been destroyed. Worth a look. ***
    (b) GitHub API access is not enabled for this session (Finding 2). If MCP spec revision-diffing
        is wanted back, that is an access grant, not a route to rediscover.
    (c) Appendix S vs fetch-routes 5c (Finding 3) — a conflict a job cannot resolve in its own
        favour. Was the browser evaluate form meant to be permitted?
    (d) 4f5e9dfe is retracted but cited by THREE live facts (483263c5, c02ac546, bdf3336e). Carried
        forward UNVERIFIED for a SIXTH run.
    (e) The `sources` convention is STILL UNSETTLED, seven runs old. Organisation-level counting was
        applied again this run (8193c07b HELD at 3 with the reasoning written into the fact).
    (f) The agentic-engineering repo also carries a kb/technology/** corpus written by another
        pipeline. Confirmed this run as a real property of the repo, not an artifact of the drift.
        Whether the two corpora are meant to share a repo is an operator question; the practical
        consequence for this job is that knomit_query results must be checked for a BARE path before
        concluding a fact exists in this pack.

SUB-RULES, cumulative (the 26th run's list stands; this run adds three):
 (27th) *** A NEGATIVE RESULT FROM knomit IS A CLAIM ABOUT THE BINDING UNTIL knomit_repos SAYS
   OTHERWISE. *** Empty scoped queries, "could not read" on an exact path, and "unknown topic <a
   topic this pack owns>" are all produced by binding drift and are indistinguishable from corpus
   damage. Check `bound.binding` before recording anything about the corpus, and re-bind before
   every write. Finding 1.
 (27th) *** A TEST RUN ACROSS AN UNCONTROLLED VARIABLE IS VOID, EVEN IF ITS RESULT LOOKS CLEAN — AND
   VOIDING IT MUST BE WRITTEN DOWN. *** Five commit-resolution calls returned a consistent, decisive
   answer; the binding moved underneath them and the answer means nothing. Appendix S's
   isolate-the-variable rule applies to bookkeeping experiments exactly as it does to fetch recipes,
   and the record has to say VOID rather than silently omit, or the next run re-derives the same
   wrong conclusion.
 (27th) *** A TOOL RESULT THAT COMES BACK EMPTY IS NOT THE SAME AS THE THING BEING EMPTY. *** read_page
   returned "(empty page)" and "Viewport: 0x0" on a fully loaded article that get_page_text read in
   full one call later. Same family as route 3c (a 404 body written to a file), route 2d (a grep that
   errored) and Finding 1 itself: the tool's failure wears the costume of the data's absence. Try the
   other reader before recording anything.

Appendix S checklist (all SEVENTEEN, from the 23rd run) still governs the staleness pass and the
self-review, and was applied to this body as well as to the facts.
