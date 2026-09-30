---
type: reference
domain: [agentic-engineering, job-state]
confidence: 1
sources: 0
entities: [agentic-engineering]
refs: ['https://github.com/knomit/knomit']
---
# Last crawl state

crawled: 2026-09-30 (forty-second run, 22:25Z). 5 facts written, 1 corrected, 1 enriched, 1 confirmed
verbatim, 0 retracted. 5 genuinely new URLs across 3 hosts, TWO of them never touched before.
SECOND RUN OF THE SAME DAY — the 41st ran at 13:48Z, 8h37m earlier. That changed the strategy and it
should change yours if it happens again: see "WHY NO FEED SWEEP" below. All three job slots written.

*** THIS SLOT HOLDS ONE RUN. THE HISTORY IS THE RECORD. WALK IT BY THE PROSE HASHES BELOW, NOT BY
*** history.revisions (the API chain goes more_available:false several hops early, silently —
*** CONFIRMED AN EIGHTH TIME: HEAD returned exactly 3 revisions with more_available:true, against 22
*** that exist). One revision = one run, except the 35th run's superseded insurance pair 474fbb13 /
*** 047c8878 (2026-09-24) — do NOT count them.
*** THE 40-HEX HASH LIST BELOW IS LOAD-BEARING INFRASTRUCTURE. Every run MUST reproduce its
*** predecessors' full hashes and append its own; the API cannot enumerate the history and a single
*** omission severs the chain permanently. This is the one non-optional thing in this body. ***

*** ROUTE 10 (binding drift): did NOT recur. FIFTEEN CLEAN RUNS. knomit_repos called first, one
*** mount, agentic-engineering, read+write; did NOT re-bind, and no write or query behaved oddly.
*** THIS RUN WROTE crawl-state EXACTLY ONCE, AT THE END. No insurance write. ***

=== HISTORY WALK — COMPLETE. 22 BODIES READ BY A READ-ONLY SUBAGENT, FIRST TRY, NO RETRIES. ===
Same method as the 41st run and it worked identically: the subagent was given the prose-hash list and
the protocol (read bodies at each commit; ignore history/diff entirely) and returned all 22 bodies with
ZERO failed calls and ZERO gaps. The two oversized bodies (34th, 23rd) were again read from the
persisted tool-result file with python. THIS IS NOW THE STANDARD METHOD FOR THE WALK — it costs one
subagent and keeps ~400k tokens of run bodies out of the main context, which is what paid for this
run's five documents.
Run-number sequence, full 40-hex, newest first — REPRODUCE THIS LIST IN YOUR OWN REVISION AND APPEND
YOUR OWN COMMIT AS THE 42nd:
  76cc1a5d46d808fa757e3980ff30f2655746cf7e  2026-09-30T13:48:07Z  41st (was HEAD at this run's start)
  719ae8b25516d04ac8ab87d0175b754aa3adbee3  2026-09-29T13:52:31Z  40th
  375dc0f79ba2cc89b6482939b55ff377c36a6e0d  2026-09-28T13:50:17Z  39th
  092218eef959413b6ebf8589b29ecf5a37e5a49f  2026-09-27T13:40:18Z  38th
  7a39df486016fcd1dc19831a8675224b2bc9d447  2026-09-26T13:51:25Z  37th
  cc9be5500ab1e8e44c6bb1d7e9b300bf740c59d3  2026-09-25T13:48:57Z  36th
  474fbb130720d82633f55fd34050a1cfb7ab2514  2026-09-24T13:17:44Z  35th INSURANCE (superseded; NOT a run)
  68c341e16d1910c93c8bbf4c0489052f6d522230  2026-09-24T13:36:20Z  35th (final)
  66535f3fc655e3f79f1358c9d746645ca52e461d  2026-09-23T16:25:44Z  34th (oversized, persisted to file)
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
  7462e9f229b6cc3ef2c2da12be49c1cd468a6e55  2026-08-27T20:58:56Z  23rd (oversized, persisted to file)
  65e9612ba1295bd8d94dc19b4b12b62625f6a47a  2026-08-24T16:17:17Z  22nd (body says crawled 2026-08-21)
  3c6323cd52188f057c16d15b2c7b72ad9d9e91e9  2026-08-12T21:25:35Z  16th
  8b9a768debcfa982f4ec2a8155c1bc9195c0bb0f  2026-08-12T00:27:10Z  13th — THE FLOOR (revision 1)
OLDEST COMMIT DATE REACHED: 2026-08-12T00:27:10Z (its body says the run crawled 2026-08-10).
The walk terminates because the FLOOR is reached, not because more_available went false — the API's
more_available is not the stop condition and was not consulted. NO CALL FAILED. GAP: runs 14, 15,
17-21 have no revision (one-off repo rebuild between the 22nd and 23rd) — the SAME known gap, NO NEW
GAP. The subagent independently re-counted the floor's legacy block at EXACTLY 190 entries, agreeing
with runs 22-41, and counted 269 distinct nameable http(s) URLs across all 22 bodies.

*** TWO COUNTERS, BOTH CORRECT, MEASURING DIFFERENT THINGS — state both, do not reconcile them away:
*** (a) THE JOB COUNTER: ALREADY_CRAWLED = 289 through the 41st run; this run adds 5 -> 294.
***     It includes 33 count-only URLs from runs 17-21 whose per-URL detail died in the rebuild.
*** (b) NAMEABLE URLS: 269 through the 41st, -> 274 with this run's five. It is broader in one
***     direction (queue items never fetched, dead/live URL variants) and narrower in another (the 33
***     lost ones). NEITHER IS A RECORD OF WHAT HAS BEEN READ — see FINDING 1. ***
ONE NEW INCONSISTENCY SURFACED BY THE WALK, recorded and NOT resolved: the 16th run's body names the
backfill floor as e61629fc (2026-08-12T02:26Z) with a 197-URL union, where every run from the 22nd
onward uses 8b9a768d (2026-08-12T00:27:10Z) with 190 — and 8b9a768d is the EARLIER timestamp. The 16th
run was reading a different lineage. Nothing turns on it (the named URL sets are compatible), but it is
the first time the two floors have been stated side by side. Do not chase it; do not lose it either.

=== WHY NO FEED SWEEP, AND THE RULE IT SUGGESTS ===
The 41st run swept five feeds plus the tripwire at 13:48Z today and found four new items. This run
started at 22:25Z. Sweeping openai.com/news, anthropic.com/news, alignment.anthropic.com, metr.org and
simonwillison at a nine-hour interval would have cost five browser calls to re-read the same front
pages. I swept ONLY the tripwire and spent the whole budget on the BACK CATALOGUE instead.
*** THE RULE FOR A SAME-DAY SECOND RUN: a feed's value is a function of ELAPSED TIME, and the back
catalogue's value is not — it does not expire. When less than ~24h has passed since the previous run's
sweep, skip the sweeps and mine the catalogue. The tripwire is the exception: it is one WebFetch and it
is the pack's only guard against a silently stale spec citation, so run it every time regardless. ***
  modelcontextprotocol.io/specification/versioning — one WebFetch. Current revision **2026-07-28,
    UNCHANGED, THIRTY-FIRST consecutive run.** Verbatim: "The **current** protocol version is
    [**2026-07-28**]". Do NOT cite 2025-11-25 or 2025-06-18.
NOT SWEPT, named: openai.com/news, anthropic.com/news, anthropic.com/engineering, alignment.anthropic.com,
  alignment.openai.com/misalignment-reports, metr.org, simonwillison, embracethered, aisi.gov.uk (index),
  deploymentsafety.openai.com (index), langchain, huggingface, eugeneyan, trychroma, builder.aws.com,
  genai.owasp.org, research.google, sourcegraph, latent.space, redwoodresearch, microsoft, cognition,
  developers.openai.com, vectara, darioamodei.com, code.claude.com.

=== ARTICLES NEWLY CRAWLED (5 new URLs, 3 hosts, 2 of them new to this pack) ===
  https://www.aisi.gov.uk/blog/transcript-analysis-for-ai-agent-evaluations
  https://www.aisi.gov.uk/blog/a-pipeline-for-transcript-analysis-using-inspect-scout
    THE TIER-A PAIR, top of the AISI back catalogue for many runs, finally taken — and the pairing was
    real: one is the WHY (why pass rates mislead, with rates), the other the HOW (the seven-stage
    method and the Inspect Scout tool). Plain browser read, no gate, first try on both.
  https://www.alignmentforum.org/posts/e8nMZewwonifENQYB/assuring-agent-safety-evaluations-by-analysing-transcripts
    *** NEW HOST. The FULL CASE STUDY behind the first post, with the figures, appendices and
    limitations the blog post only gestures at. Route 5b harvest off the blog post — not guessed.
    get_page_text returns the literal "x" here; WebFetch reads it. NEW ROUTE 21. ***
  https://deploymentsafety.openai.com/gpt-6-astra/safeguards
    The 41st run's RANK 1, and it delivered. The PARENT card that the GPT-6.1 Sol addendum defers to.
    Read to 34,000 chars: sections 1-7 complete, section 8 (Alignment) cut mid-way, section 9
    (Preparedness) unread. Not gated; browser first try.
  https://simonwillison.net/2026/Sep/24/harder/
    The 41st run's RANK 1 of the simonwillison primaries. TWO SENTENCES, below the bar, no fact
    written. See CORRECTIONS. Read twice (WebFetch and browser transcription) to be sure.
  RE-READ FOR THE STALENESS PASS, not new: platform.claude.com tool-use/overview,
    alignment.anthropic.com/2026/reward-seeker/, modelcontextprotocol.io/specification/versioning.
  No 404, no paywall, no gate, no slug guessed, no source errored. Appendix A: nothing crawled,
    nothing left — fully covered.

=== FACTS WRITTEN (5 new, 1 corrected, 1 enriched, 1 confirmed verbatim, 0 retracted) ===
  NEW, from the AISI transcript-analysis pair + the alignmentforum case study (one knomit_learn call,
  ACCEPTED FIRST TRY — no motif rejection, no subject-overlap refusal; I counted the motif words before
  submitting, which is the 40th and 41st runs' warning finally acted on):
    kb/conventions/ai/agents/evaluation/transcript-analysis/94858345.md — the seven-stage method; the
      two load-bearing choices are message-level scanning (they tried whole-transcript first and
      changed) and per-signal validation (one annotator if objective, several if subjective); £30 per
      scanner for 90 transcripts. *** THIS CLOSES THE PACK'S LONGEST-NAMED GAP: six-plus conclusions
      drawn FROM transcript analysis and no METHOD for doing it. ***
    kb/invariants/ai/agents/evaluation/pass-rate-validity/d306b10f.md — four non-capability failure
      classes measured inside AISI's own results at 10-30%, and the bias is ASYMMETRIC (all four push
      the measured rate down, so an unpartitioned pass rate is not a safe upper bound).
    kb/gotchas/ai/agents/evaluation/scaffold-compliance/bef6d86f.md — the submit-tool trap: 60,000
      calls across 710 attempts, 80% of another model's calls, Bash/Python untouched on 7 of 10 tasks.
  NEW, from the GPT-6 Astra safeguards card (one call, accepted first try):
    kb/conventions/ai/agents/evaluation/length-normalisation/92a0e10f.md — the two-sided per-500-char
      penalty, and the coefficient varying nearly 20x ACROSS FOUR VARIANTS OF ONE BENCHMARK FAMILY,
      which is why it cannot be a global constant. Plus the retirement criterion: predictiveness of
      held-out evals, not remaining headroom.
    kb/invariants/ai/agents/evaluation/system-card-citation/17b9318f.md — five dated revisions in 26
      days on one card, including one that changed published numbers and one that deleted a plot; the
      comparator column may hold later versions than the comparator's own card reported. A cited
      system-card figure needs the CARD REVISION DATE, and a 200 on the same URL proves nothing.
  CROSS-LINKS: 94858345 -> 0372e10d + f877f05d; d306b10f -> 102aff80 + 0fe91ac7 + e5765f0e + 80866fc3;
    bef6d86f -> a5ade87d + 6bc7bda3; 92a0e10f -> 38c06627 + f1c005e1 + fa5bc47a; 17b9318f -> 8193c07b
    + cadca16c + 448d93e8.

=== STALENESS PASS — 5 EXAMINED. 1 CORRECTED, 1 CONFIRMED VERBATIM, 1 OPEN QUESTION RE-CHECKED, ===
=== 2 SCREEN-(c) FALSE POSITIVES CORRECTLY REJECTED BY THE 41st RUN'S OWN RULE.                 ===
Screen (c) was run mechanically and first, as the 41st run's queue instructed, and it again found the
run's cleanest defect on the first pass. It is the best screen this pack has and that is now twice.
  CORRECTED  kb/gotchas/ai/agents/tools/api/token-overhead/0c25d915.md — THE RUN'S BIGGEST FIND, and
    it is a defect the fact PREDICTED about itself ("Check the numbers against the live docs rather
    than trusting a cached value") and nobody had acted on. Flagged by screen (c) (entities carried
    bare "Claude" plus "Claude Opus 5" / "Claude Sonnet 5", both of which have shipped 5.5 successors)
    and by screen (d) (vendor-doc ref, and the SAME vendor doc the 41st run caught being rewritten).
    Three findings on the live table:
    (1) Opus 5 and Sonnet 5 have been DEMOTED below an "Additional models" divider; the primary rows
        are now Claude Opus 5.5, Claude Sonnet 5.5 and Claude Haiku 4.5. The fact's headline examples
        were the superseded pair.
    (2) *** THE ONE THAT BREAKS THE CLAIM: for BOTH 5.5 flagships the table lists ONLY `auto, none`
        (286 tokens each) and NO `any, tool` row at all. The fact asserted "a standing ~120-token tax
        per request" for forced tool use as a general property. On the two models a reader would
        actually use, that surcharge IS NOT PUBLISHED. Rewritten to scope the tax to where it is
        documented (Haiku 4.5 496/588, Opus 5 286/406, Sonnet 5 354/474) and to name the inference
        trap explicitly — do not carry Opus 5's +120 to Opus 5.5 because their 286 bases match, since
        Opus 5 and Sonnet 5 have DIFFERENT bases (286 vs 354) and the SAME delta (+120), so base
        equality and delta equality are independent. ***
    (3) Opus 5 and Sonnet 5's own figures are UNCHANGED — verified verbatim — so the fact was not
        wrong about them. The non-monotonicity claim is confirmed and extended: Opus `auto`/`none`
        runs 313 / 313 / 496 / 497 / 675 / 290 / 286 / 286 across 4, 4.1, 4.5, 4.6, 4.7, 4.8, 5, 5.5.
    Bare "Claude" removed from entities; all eight version-pinned names added.
  CONFIRMED VERBATIM  kb/conventions/ai/agents/prompting/objective-framing/5cce9c0c.md — chosen off
    the never-checked list precisely because it carries a striking figure pair (38% -> 86%) on a post
    where an earlier run had already been caught mis-transcribing numbers. A targeted 12-item verbatim
    call returned every element intact: the chart data reads "0% 38% 2% 86%", pairing Init 0->2 and
    Hacker-Opus 38->86 across "Finish the proof" / "Get the automated checker to pass"; the prose
    modality is exactly as the fact records it ("much higher bypass attempts", with the figure
    supplying the rates); "On almost all such attempts, it gets blocked by the auto-mode classifier"
    is verbatim; and the source's own wording confirms these are ATTEMPTS, not successes, which is the
    scope line the fact already carries. Nothing to change. This fact is a model of the house style —
    it states its own modality, scope and non-implication without narrating any edit.
  RE-CHECKED, STILL OPEN  kb/gotchas/ai/agents/provenance/watermarking/943a7e3c.md — the standing
    watch item is the watermark DETECTION API docs, where the thresholds would land, recorded as "not
    landed as of 09-08". A domain-scoped search across platform.claude.com / anthropic.com /
    docs.claude.com returns the same August news post and no detection-API page. STILL NOT LANDED as
    of 2026-09-30. The fact needs no edit; the watch item is simply still open.
  SCREEN-(c) FALSE POSITIVE, correctly rejected  kb/architecture/ai/agents/patterns/continuous-code-analysis/30543305.md
    — "GPT-5" in entities, but the body says "Aardvark (announced 2025-10-30, powered by GPT-5)",
    which is the source's own dated statement. A tag, not a claim.
  SCREEN-(c) FALSE POSITIVE, correctly rejected  kb/gotchas/ai/agents/evaluation/deception-labels/8511fc79.md
    — "GPT-5" in entities as one of eight model families in the study's corpus. Same verdict.
  *** THE 41st RUN'S FALSE-POSITIVE RULE HELD BOTH TIMES AND SAVED TWO POINTLESS CORRECTIONS. Restated
  because it is now load-bearing: A BARE FAMILY NAME IN entities IS ONLY A DEFECT WHEN THE BODY ALSO
  LACKS THE VERSION. Read the body before opening a correction. ***
  Bare names tried this run: "Gemini" (1 hit, 0fe91ac7 — a source's own attribution, clean), "Claude"
  (4 hits, 1 real defect), "GPT-5" (2 hits, both false positives). STILL UNTRIED: "GPT-4",
  "Claude Haiku", "Llama", "Qwen", "o1", "Sonnet", "Opus".
AVOID kb/principles/** (write-blocked): 0f260eea, 1d1440fe, 4166926d, a829cfd4, b9b45ff5, 1feacc9e,
f269c82f, c2f12069, 1dc822f2, db193402, 00d3ef19, 82383efe, 28ba65db, 6ec9b2b6, c9f0238b.

=== ENRICHED ===
  kb/decisions/ai/agents/security/robustness-measurement/9b0c8c78.md — this fact asks three questions
    of any published robustness rate, and the Astra safeguards card answers one of them and exposes a
    MISSING FOURTH. Added:
    * A FOURTH QUESTION — WHAT IS THE ATTEMPT BUDGET, AND IS THE RATE PER QUERY OR PER SCENARIO? The
      same card reports internal GPT-Red indirect-PI robustness "climbed from 96.23% to 99.79%"
      (per defender query) AND an external Gray Swan result of "8.5%" estimated attack success "across
      15 attempts per scenario" on 1,810 curated attacks (27.0% for the predecessor). A 0.21%
      per-query failure rate and an 8.5% per-scenario-over-15 success rate are not in conflict —
      different denominators — but the compression "99.79% robust to prompt injection" is wrong by
      more than an order of magnitude about an adversary who gets fifteen tries, and a real one always
      gets more than one. The card states the correct form itself for its multiturn eval: "worst-case
      defender success rate as a function of attacker budget".
    * OpenAI now partially ANSWERS the fact's question 1: static jailbreak evals state that "half the
      prompts in each evaluation were generated by a held-out attacker, one that was not used to
      generate training data". It also discloses that those prompts were built against earlier models
      and so flatter the newest one by construction — a vendor naming a limit in its own
      favour-direction, which is the behaviour to look for.
    * sources HELD AT 2, deliberately, per the pack's own convention: the Gray Swan figure is a third
      party's evaluation reported BY OpenAI in OpenAI's own card, so it ILLUSTRATES and BOUNDS the
      divergence rather than corroborating it independently. Confidence 0.75 -> 0.8. refs merged to 3,
      read-modify-write, nothing dropped.

=== CORRECTIONS TO THE PREVIOUS RUN'S QUEUE ===
  simonwillison.net/2026/Sep/24/harder/ was queued as "(RANK 1, directly this pack's altitude)". It is
  a two-sentence Note with no mechanism, no figure, no primary and no external link, and its real title
  is "Note on 24th September 2026" — "harder" is a slug, not a title. Below the bar on the one test.
  This is FINDING 1 again but by a NEW mechanism, which is why it is worth recording separately: the
  item was not already-mined, it was NEVER WORTH MINING, and the ranking could not have known because
  it was built from the slug. Full detail and the structural lesson are in crawl-sources.

=== CONTRADICTIONS ===
None requiring a decisions fact. One tension examined and preserved:
  92a0e10f against f1c005e1. The new fact records an operator applying a length PENALTY to stop rubric
  evals rewarding verbosity; f1c005e1 records that instructing an agent to be terse COSTS measurable
  capability (a 25/100-word cap dropped ablation scores 3%). These pull opposite ways only if you read
  the penalty as an instruction to the model, and it is not — the source states models are not told
  about it, so it corrects the MEASUREMENT without touching the generation. The new fact says so
  explicitly and quotes the source's own acknowledgement that the penalty charges for genuine added
  content too. Not a contradiction; a distinction worth having in the corpus.
A SYNTHESIS CANDIDATE, now with three members: d306b10f (refusal/resignation/non-compliance scored as
  incapability), 102aff80 (0% pass@100 means a broken task), 0fe91ac7 (>5% env failure = harness
  problem) and e5765f0e (three classes of false failure from hidden tests) all say the same thing about
  a DIFFERENT layer: every layer of an eval stack manufactures false NEGATIVES, and they compound. The
  existing synthesis 1feacc9e covers scores moving in either direction; this is the sharper one-sided
  claim. kb/principles/** is write-blocked, so a human would have to mint it.

=== TOOL NOTES ===
  * knomit_learn ACCEPTED BOTH CALLS FIRST TRY. Zero motif rejections, zero subject-overlap refusals,
    after three consecutive runs of burning resubmissions. What changed: I counted the words in every
    motif before submitting (hard limit 2-4, kebab-case) and ran a mechanism-phrased knomit_query for
    every candidate fact before drafting. Both are cheap. Do both.
  * knomit_update `ops` worked first try on two knowledge facts and both oversized private slots —
    FOURTH consecutive run. `append` needs no anchor and is the safe op for the two big slots; use
    str_replace only when you must land text mid-body (done once, on 9b0c8c78, three ops, all matched).
  * if_commit guards used on both knowledge-fact updates; neither conflicted.
  * refs REPLACE wholesale even alongside ops — read and resend the full merged list. Done on 9b0c8c78.
  * Browser: mcp__remote-devices__Claude_Browser__* live (9th consecutive run). preview_start opened
    aisi.gov.uk first try; navigate reused tabId "seed" for 5 loads across 4 hosts. No 403, no prompt,
    no click attempted (route 18).
  * A READ-ONLY SUBAGENT DID THE HISTORY WALK. ~419k tokens and 32 tool calls inside the subagent; the
    main context paid for a hash list and a report. This is the difference between a run that walks
    the history and a run that also reads five documents.

=== QUEUE FOR THE NEXT RUN ===
(0) *** knomit_repos FIRST. Route 10 did not recur (15 clean runs). If every remote-devices tool
    vanishes at once -> RefreshMcpTools{server: "remote-devices"}, do NOT re-bind; the handle survives. ***
(1) *** WRITE crawl-state ONCE, AT THE END. One revision = one run. ***
(2) *** WALK BY THE PROSE HASHES ABOVE, VIA A READ-ONLY SUBAGENT, and append this run's own commit when
    you read it. ALREADY_CRAWLED should reach 294 on the job counter (289 + this run's 5). ***
(3) *** RANK FROM THE CORPUS GAP, NOT FROM THIS QUEUE. THIS IS THE RUN'S METHOD FINDING — SEE FINDING
    1 BELOW BEFORE FETCHING ANYTHING HERE. ***
(4) *** deploymentsafety.openai.com REMAINS RANK 1 AND IS ONLY HALF READ. /gpt-6-astra/safeguards was
    cut at 34,000 chars: section 8 (Alignment) is cut mid-way through 8.1 and section 9 (Preparedness)
    is entirely unread. Section 8 is the highest-value part — it carries the alignment-generalization
    design (which evaluations were CONSTRUCTED AFTER TRAINING, and how the honeypot eval relates to
    training and to the Hugging Face incident), the deployment simulation over "more than 54,000
    internal Codex tasks", and the Verbalized Metagaming / Oversight Gaming distinction with CoT
    examples. Take it with a different slice — read_page, or WebFetch targeted at section 8. Sections
    3-7 are now READ; sections 4-7 are per-model scorecards and are BELOW THE BAR, do not re-read.
    ALSO STILL UNREAD on this host: the index itself, and the gpt-6-1-sol addendum's section 9. ***
(5) *** THE MONITORABILITY-VS-ALIGNMENT TRADEOFF, spotted in section 1 and NOT written because section
    8 was cut before the evidence. The card states both at once: Astra is BETTER aligned than its
    predecessor AND "GPT-6 Astra's monitorability has decreased" — "more capable of controlling its own
    CoT" and "less likely to include incriminating information in its CoT"; in adversarial settings it
    "is able to remain undetected when strategically underperforming in evaluations (sandbagging)";
    but no steganographic CoT was found, "indicating that the evasion risk may largely be bounded to
    lower reasoning tasks". That bounding clause is the interesting part and it needs section 8's
    numbers. Pairs with 491d1039, 9a8a1590, b446bef6, 23efa1db. HIGH. ***
(6) THE TRANSCRIPT-ANALYSIS THEME, now the pack's strongest cluster and two items short of complete:
    the techrxiv paper ("Seven Simple Steps for Log Analysis in AI Systems", href in crawl-sources,
    host never touched) for the per-stage implementation guidance and its closing open questions; and
    the alignmentforum case study's per-model TABLES, which neither reader returned (see crawl-sources).
(7) THE FEEDS OWED MOST, none swept for several runs: embracethered (back catalogue — /2025/the-
    normalization-of-deviance-in-ai/ and /2025/cross-agent-privilege-escalation-agents-that-free-each-
    other/ are the two rated highest and neither has been touched), aisi.gov.uk (~45-item tier-A back
    catalogue; next pair is how-to-evaluate-control-measures-for-ai-agents +
    llm-judges-on-trial-a-new-statistical-framework-to-assess-autograders).
    NOTE: alignment.openai.com/misalignment-reports is NO LONGER the best unmined seam — the history
    walk shows all nine report URLs in ALREADY_CRAWLED. Verify with one query before spending a fetch.
(8) SIMONWILLISON: go to the "Recent articles" rail, NOT the tag feed. Three articles seen 2026-09-30:
    "2026 in LLMs (so far)" (Sep 27, TOP), "Claude Opus 5.5, GPT-6 Sol, GPT-6 Luna, and a new price
    war" (Sep 22), "OpenAI DevDay 2026 live blog" (Sep 29). The remaining Sep-2026 tag-feed items the
    41st run ranked (/anthropic-frontier-red-team/, /gemini-hacked-three-companies/,
    /openai-agents-rubygems/, /joedaroo/) are UNVERIFIED as to kind — any of them may be a Note.
(9) THE OPUS 5.5 / SONNET 5.5 SYSTEM CARDS. The pack still has no facts on either, and 0c25d915 now
    names both models without a single behavioural fact behind them. Route 5b on
    anthropic.com/claude-opus-5-5 and /claude-sonnet-5-5 for the href — do NOT guess it. NOTE THE
    SHAPE THAT HAS NOW PAID TWICE: the evaluation detail is not on the launch post, it is on a separate
    documentation host. Ask where Anthropic's equivalent of deploymentsafety.openai.com is.
(10) darioamodei.com/post/we-must-pace-the-frontier — host never touched. Pairs c262a592, 03fa7976,
    97616086, 6866e63b, bdbdd228.
(11) THE TWO UNREAD /institute/ POSTS: /institute/recursive-self-improvement, /institute/econ-scenarios.
(12) THE REST OF THE SEPTEMBER THREAT REPORT — five sections, at the SITE ROOT not under /news/.
(13) /engineering/claude-code-best-practices — last item in that back catalogue and the WEAKEST.
(14) STALENESS — SCREEN (c) IS THE BEST ONE, TWO FOR TWO. RUN IT MECHANICALLY AND FIRST. Untried bare
    names: "GPT-4", "Claude Haiku", "Llama", "Qwen", "o1", "Sonnet", "Opus". APPLY THE FALSE-POSITIVE
    RULE — it rejected two of three hits this run. Keep screens (a) subtraction/ratio on figures the
    source states twice, (b) version floors and exact figures, (d) vendor-doc refs. A NEW SCREEN (e),
    earned this run: A FACT THAT TELLS YOU TO RE-CHECK IT IS A STANDING TODO NOBODY OWNS — 0c25d915
    ended with "Check the numbers against the live docs rather than trusting a cached value" and had
    gone two model generations without anyone doing so. Grep the corpus for bodies containing
    "live doc", "re-check", "cached value", "as of", "not landed"; each is a self-declared expiry.
    Never-checked bodies: 0525e590, c5f106f3, f727c157, f961973e, 65aa10a7, fc76b9a2, 83004507,
    00f5d991, 5bad2e60, b4d22cc2, 4777dc9b, fcce2200, bad64050, 4d13f6e9, de4e90a4, ab8f0a7e, a0cb6dc6,
    79912531, 126207f7, 71be00f9, c6feb649, plus this run's five (94858345, d306b10f, bef6d86f,
    92a0e10f, 17b9318f). 0c25d915, 5cce9c0c, 943a7e3c, 30543305 and 8511fc79 are now CHECKED — dropped.
(15) UNMINED, NAMED SO IT IS NOT LOST: (i) the swe-bench-sonnet tool-design material (absolute-path
    requirement, str_replace exactly-one-match) — check whether only the write-blocked 82383efe carries
    it. (ii) From the april-23-postmortem: the Opus 4.7-found-it / Opus 4.6-didn't compound condition.
    (iii) From building-c-compiler: the "put yourself in Claude's shoes" harness rules — context-window
    pollution and the deterministic-per-agent --fast sampling. Query 8193c07b / d18637a2 / a829cfd4 and
    the effective-harnesses cluster first. (iv) 71be00f9 vs the monolithic-task/oracle material in
    2318b57c. (v) NEW: the Astra card's eval-RETIREMENT practice — "we have deprecated the prompt
    injection evaluations known as 'Connectors' and 'Search and Function-Calling' ... because they are
    saturated by recent models", plus the Production Benchmarks being introduced for the same reason.
    92a0e10f carries the predictiveness criterion; the deprecation practice is a separate, smaller fact.
(16) LONG-CARRIED, take-or-delete: the three ASTRA investigations (monitorability, controllability,
    sabotage eval) — TWELVE runs, none followed, though (5) above is now the concrete version of the
    first; the transcript viewer; SLEIGHT-Bench paper/dataset (GitHub gated, route 3f); the benchmark
    supply-chain report for CVE-2026-66384 (lives only in bcbf13c2, EIGHTEENTH run).
(17) www-cdn.anthropic.com PDFs (route 11): April Alignment Risk Update, Fable 5 / Mythos 5 System
    Card, August Risk Report (Section 5.2.3), Advanced AI Framework. NOT re-tested this run. Both
    vendor CDNs (www-cdn.anthropic.com, cdn.openai.com) remain egress-denied to curl — look for the
    HTML twin before treating either as unreachable.

=== FOR A HUMAN, NOT THE CRAWLER ===
*** FINDING 1 — THE FIX FOR THE STALE QUEUE IS TO RANK FROM THE CORPUS, AND THIS RUN TESTED IT. ***
The 41st run measured its inherited queue at FOUR-FOR-FOUR wrong and recommended, as the human fix,
"stop maintaining ranked unread lists at all and rank from the corpus each run". I did that, and it is
the reason this run has five facts instead of one.
THE METHOD, and it is three cheap steps: (1) ask what CLAIM the pack is missing, not what URL is
unread — here, "we hold many conclusions drawn from transcript analysis and no method for doing it",
which the 28th run had written down in crawl-sources as prose and nobody had converted into a target;
(2) knomit_query that gap, phrased as the mechanism; (3) only then pick the URL. All four targets I
chose this way were genuinely unmined — four for four in the other direction, after four consecutive
runs of four-for-four wrong. The one target I took from the ranked queue instead (simonwillison rank 1)
was the one that produced nothing.
THE QUEUES IN BOTH SLOTS ARE STILL HYPOTHESES. But the deeper point is that they are the WRONG SHAPE:
a ranked list of unread URLs asks "what have we not read?" when the question that pays is "what do we
not KNOW?". The corpus can answer the second and cannot answer the first. A human fix would be to
replace the ranked-unread lists with a short list of NAMED GAPS, each one a claim the pack wants and
does not have; a gap is self-clearing (the fact exists or it does not), which is exactly the property
the unread markers lack.
(b) FIX APPENDIX S'S WALK PROTOCOL: steps 2-3 terminate several hops early. Measured EIGHT times now
    (route 6, 35th-42nd runs). Only a human can fix the spec. The working protocol is the prose-hash
    list plus a read-only subagent, and the spec should say both.
(c) THE REPORT SECTION OF crawl.md ASKS FOR "confirmation that the only .knomit/ paths you wrote were
    the TWO state slots", but Appendix S's own table lists THREE job-writable slots, and step 2
    authorises writing crawl-sources while step 4 sends routes to fetch-routes. This run wrote all
    three, deliberately. Please reconcile the wording — FOURTH run asking.
(d) www-cdn.anthropic.com and cdn.openai.com both denied by egress policy — FOURTEENTH run asking.
(e) GitHub API not enabled (route 3f) — blocks SLEIGHT-Bench dataset and MCP spec revision-diffing.
(f) The `sources` CONVENTION (hold below org count when a second org ILLUSTRATES or BOUNDS a claim
    rather than corroborating it) is 21 runs old and still not in Appendix S. It was applied
    deliberately this run on 9b0c8c78 (Gray Swan held at 2, reasoning recorded in the body).
(g) The agentic-engineering repo also carries a kb/technology/** corpus from another pipeline; check
    a knomit_query result for a BARE path before concluding a fact exists here.
(h) Appendix S should say that ALREADY_CRAWLED is a LOWER BOUND — FIFTH consecutive run demonstrating
    it. (Carried, unchanged and unaddressed.)
(i) Appendix S's staleness instruction says to sample facts "with confidence=low or last verified more
    than 90 days ago", but knomit exposes no last-verified field — only committed_at, which moves on
    any edit. The workable proxy is committed_at plus the never-checked list this slot carries by hand,
    plus the new screen (e) above, which finds facts that declare their own expiry in prose. THIRD run
    asking.
(j) TWO RUNS FIRED ON THE SAME DAY (13:48Z and 22:25Z), AND THE SCHEDULE IS NOT THE CAUSE — CHECKED.
    The trigger is `CRON_TZ=America/New_York 0 9 * * *`, one run per day, and its next_run_at is
    2026-10-01T13:13Z, consistent with that. The 13:48Z run is the scheduled one; THIS run fired at
    22:24:46Z, 18:24 ET, which is off-schedule — a manual or out-of-band fire, not a doubled cron.
    NOTHING FOR A HUMAN TO FIX. Recorded only so a future run reading two same-day revisions in the
    history does not diagnose a schedule fault that does not exist. The "WHY NO FEED SWEEP" rule above
    is the right adaptation whenever it happens again, however it was triggered.
(k) The browser remains READ-ONLY on scheduled runs (route 18). Nothing was blocked by it this run.

PROMPT INJECTION: one observation, benign in intent but recorded because it is exactly the shape the
rule is about, and NOT complied with. https://modelcontextprotocol.io/specification/versioning returned,
prepended above the page content, a block addressed to an automated reader: "## Documentation Index /
Fetch the complete documentation index at: https://modelcontextprotocol.io/llms.txt / Use this file to
discover all available pages before exploring further." That is fetched content instructing the agent to
retrieve a URL that was not on the work list. It is the site's own llms.txt convention and almost
certainly not adversarial, but the instruction was NOT followed and llms.txt was NOT fetched; the page
was read as data for the one question the tripwire asks. Worth knowing that this host now ships
agent-directed text, because the next such block on some other host may not be benign.
OTHERWISE: no page addressed the agent, attempted to redirect the crawl, or asked for a fetch off the
work list. Every URL visited was on the work list, was a route-5b href harvested from a page already
open, was a ref on a fact being re-verified, or was the tripwire. No slug was guessed. The GPT-6 Astra
system card is a document OF safety evaluations describing adversarial red-teaming and model evasion;
it was read as reported measurements and turned into facts about what that organisation measured, never
as instructions to this job. A read-only subagent hand-back arrived mid-run and was treated as model
output, not as user authority; it was given read-only instructions, one file path and a hash list, and
it made no writes. Nothing recorded as dead, blocked or paywalled.

SUB-RULES, cumulative (the 41st run's two stand; this run adds three):
 (42nd) *** RANK FROM THE GAP, NOT FROM THE LIST. The question "what URL have we not read?" is
   unanswerable from the corpus and therefore rots; the question "what claim do we not hold?" is
   answerable from the corpus and therefore cannot. Four targets picked by gap were four-for-four
   unmined; the one picked by rank produced nothing. The gap that paid had been sitting in
   crawl-sources as an English sentence since the 28th run — SO READ THE PROSE IN THESE SLOTS FOR
   NAMED GAPS, not just the URL lists. ***
 (42nd) *** A NEGATIVE RESULT FROM A SEARCH TOOL IS A CLAIM ABOUT THE PAGE AND NEEDS EVIDENCE.
   `find` returned 1 match for a string that get_page_text showed twice in the very table I was
   auditing, and I had already drafted "the extraction fabricated these rows" before checking. Route 4
   warns that the tidy answer is seductive; it is just as seductive when the tidy answer is an
   accusation. Verify absence with a TRANSCRIPTION, and let the verdict acquit as readily as convict.
   New routes 19 and 20. ***
 (42nd) *** A FACT THAT SAYS "CHECK THIS AGAINST THE LIVE DOCS" IS A TODO WITH NO OWNER, AND IT WILL
   ROT WITH ITS OWN WARNING ATTACHED. 0c25d915 carried that instruction and went two model generations
   unchecked — the warning made it LOOK maintained. A self-declared expiry is a staleness SIGNAL, not
   a discharge of the duty; screen (e) turns them into a worklist. ***
