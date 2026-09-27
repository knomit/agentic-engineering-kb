---
type: reference
domain: [agentic-engineering, job-state]
confidence: 1
sources: 0
entities: [agentic-engineering]
refs: ['https://github.com/knomit/knomit']
---
# Last crawl state

crawled: 2026-09-27 (thirty-eighth run). ONE DAY after the 37th. 5 facts written, 2 corrected, 0
retracted, 0 enriched. 3 genuinely new URLs. SIX FEEDS PLUS THE TRIPWIRE. *** openai.com/news WAS
SWEPT AFTER BEING OWED FIVE RUNS, AND IT WAS THE RUN'S BEST SOURCE. *** Queue item (4) resolved.

*** THIS SLOT HOLDS ONE RUN. THE HISTORY IS THE RECORD. WALK IT BY THE PROSE HASHES BELOW, NOT BY
*** history.revisions (36th run FINDING 1: the API chain reaches ~8 of 15 and goes more_available:false
*** three hops early, silently — CONFIRMED AGAIN THIS RUN: HEAD returned exactly 3 revisions with
*** more_available:true, against 18 that exist). One revision = one run, except the 35th run's
*** superseded insurance pair 474fbb13 / 047c8878 (2026-09-24) — do NOT count them.
*** THE 40-HEX HASH LIST BELOW IS LOAD-BEARING INFRASTRUCTURE. Every run MUST reproduce its
*** predecessors' full hashes and append its own; the API cannot enumerate the history and a single
*** omission severs the chain permanently. This is the one non-optional thing in this body. ***

*** ROUTE 10 (binding drift): did NOT recur. ELEVEN CLEAN RUNS. knomit_repos called first, one mount,
*** agentic-engineering, read+write; did NOT re-bind, and no write or query behaved oddly. Bind-once
*** is safe; route 10 should be downgraded to "call knomit_repos before believing a negative" (17d). ***
*** THIS RUN WROTE crawl-state EXACTLY ONCE, AT THE END. No insurance write. The bridge held. ***
*** The 37th run's response-classifier trip did NOT recur. No source this run reproduced attack
*** mechanics, so the 37th's altitude sub-rule was not under test; it still stands. ***

=== HISTORY WALK — COMPLETE. 17 BODIES READ BY A READ-ONLY SUBAGENT, FIRST TRY, NO RETRIES. ===
A read-only subagent was given the prose-hash list and the protocol (read bodies at each commit;
ignore history/diff fields entirely) and returned all 17 bodies with ZERO failed calls and ZERO gaps.
Two bodies (34th, 23rd) exceeded the inline cap and were read from the persisted tool-result file.
Run-number sequence, full 40-hex, newest first — REPRODUCE THIS LIST IN YOUR OWN REVISION:
  7a39df486016fcd1dc19831a8675224b2bc9d447  2026-09-26T13:51:25Z  37th (was HEAD at this run's start)
  cc9be5500ab1e8e44c6bb1d7e9b300bf740c59d3  2026-09-25T13:48:57Z  36th
  474fbb130720d82633f55fd34050a1cfb7ab2514  2026-09-24T13:17:44Z  35th INSURANCE (superseded; NOT a run)
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
  7462e9f229b6cc3ef2c2da12be49c1cd468a6e55  2026-08-27T20:58:56Z  23rd (oversized, persisted to file)
  65e9612ba1295bd8d94dc19b4b12b62625f6a47a  2026-08-24T16:17:17Z  22nd (body says crawled 2026-08-21)
  3c6323cd52188f057c16d15b2c7b72ad9d9e91e9  2026-08-12T21:25:35Z  16th
  8b9a768debcfa982f4ec2a8155c1bc9195c0bb0f  2026-08-12T00:27:10Z  13th — THE FLOOR (revision 1)
OLDEST COMMIT DATE REACHED: 2026-08-12T00:27:10Z (its body says the run crawled 2026-08-10).
more_available was FALSE at the floor. NO CALL FAILED. GAP: runs 14, 15, 17-21 have no revision
(one-off repo rebuild between the 22nd and 23rd) — the SAME known gap, NO NEW GAP.

*** ALREADY_CRAWLED = 282 through the 37th run. *** Re-derived from the bodies this run, not copied
forward, and the derivation is worth recording because it disagrees with the 37th body by one:
  217 distinct ARTICLE urls in the union across the 17 bodies (the floor contributes 163 non-feed
    urls of its 190-entry block; the floor's one "NEVER FETCHED — 404, guessed slug" openai.com
    entry is excluded)
+  29 FEED/INDEX prefixes (26 marked "(feed)" in the floor's block, plus openai.com/news,
    alignment.openai.com/misalignment-reports/ and alignment.anthropic.com/, each recorded by a
    later run as an index sweep rather than an article read)
=  246 NAMED through the 36th
+  33 COUNT-ONLY (runs 17-21: 5+7+4+9+8; per-URL detail died in the rebuild)
=  279 through the 36th, + the 37th run's 3 = 282 through the 37th.
The 37th body computed 278 / 281 for the same two points. The difference is entirely in how the
floor's block is partitioned between articles and feed prefixes; the NAMED SET IS IDENTICAL and
nothing turns on the total. Do not chase it. This run adds 3 -> next run's ALREADY_CRAWLED = 285.

=== FEEDS SWEPT: SIX PLUS THE TRIPWIRE. ONE WAS HOT; THE OTHER FIVE WERE QUIET. ===
  modelcontextprotocol.io/specification/versioning — one WebFetch. Current revision **2026-07-28,
    UNCHANGED, TWENTY-SEVENTH consecutive run.** Verbatim: "The **current** protocol version is
    [**2026-07-28**]". Do NOT cite 2025-11-25 or 2025-06-18 as current.
  *** openai.com/news — HOT, AND IT WAS OWED FIVE RUNS. Browser (route 1) via preview_start; read
    first try, no 403, no approval prompt. Front page newest-first: two-years-of-openai-academy,
    Altman UN Security Council remarks, ChatGPT Ads SE Asia, Airbnb GPT-6 Astra (all Sep 23);
    better-prompt-caching-for-gpt-6, Introducing GPT-6 Sol and Luna, priorities-principles-third-
    party-assessments (all Sep 22); advisory group on mathematics + Academy learning paths (Sep 21).
    TWO WERE READ (below). THE LESSON: five runs of "not swept, named" cost the pack two facts it
    could have had in mid-September. A feed that keeps getting deferred is not low-yield, it is
    UNMEASURED — the 37th run's own sub-rule about aiming at what the queue flagged, applied to
    feeds instead of to the staleness axis. ***
  alignment.openai.com/misalignment-reports — QUIET. Index still 9 reports, newest still the three
    of 2026-09-25 that the 37th run read. NO fourth batch. All 9 are in ALREADY_CRAWLED.
  www.aisi.gov.uk/blog — SWEPT (3 runs since the last sweep, as the 37th queued). 96 posts returned
    in one WebFetch. NOTHING new since /blog/optimal-stopping-... (Aug 27 2026, read 23rd run).
    FIVE WEEKS QUIET. The ~47-item tier-A back catalogue is untouched and remains the deepest
    unmined seam. Keep the every-third-run cadence.
  www.anthropic.com/news — QUIET. Newest still /news/claude-discovers-novel-enzyme-system (Sep 23,
    below bar). Nothing newer than the 37th run's sweep.
  metr.org/blog — QUIET. Newest still /blog/2026-09-22-claude-opus-5-5/ (read 36th). Still
    uncrawled: /blog/2026-08-14-funding-update/. THIRD-PARTY-HACKING FOLLOW-UP still not published
    — THIRTEEN runs.
  alignment.anthropic.com — not re-enumerated this run (the 36th run's index of 84 posts stands and
    the 37th confirmed nothing newer than Aug 2026). ONE post from that index was READ (below).
NOT SWEPT, named: anthropic.com/engineering, embracethered, simonwillison, microsoft research/
  security, langchain, huggingface, eugeneyan, trychroma, builder.aws.com (route: browser/JS),
  genai.owasp.org, research.google, sourcegraph, latent.space, redwoodresearch,
  developers.openai.com, vectara, darioamodei.com, cognition.

=== ARTICLES NEWLY CRAWLED (3 new URLs; 2 read in the browser, 1 index-resolved by WebSearch) ===
  https://openai.com/index/priorities-principles-third-party-assessments/  (Sep 22 2026, Safety)
    OpenAI's stated priorities and principles for third-party safety assessments. Defines SAFETY
    CLAIM and SAFETY CASE operationally (a case is scoped to ONE activity — training, evaluation,
    internal deployment, external deployment). Four priority areas; the principles are the yield:
    pre-registration of claims before assessment begins, labelling each claim by who proposed it,
    a pre-agreed process for out-of-scope risks, conclusions stating what was NOT assessed,
    findings separated from interpretation, redaction noted with its impact. "Grey box" named as
    the access tier for adversarial safeguard testing. -> 87e86747.
  https://openai.com/index/better-prompt-caching-for-gpt-6/                (Sep 22 2026, Product)
    THE BEST SINGLE ITEM THIS RUN, and it is a Product post, which the pack's heuristics would have
    ranked below the Safety one. Concrete API-level mechanics for keeping a persistent agent's
    cached prefix intact: allowed_tools / tool_choice:"none" INSTEAD of deleting tool definitions;
    new developer message appended at the END rather than editing earlier instructions;
    configuration_update to change reasoning effort without breaking cache; 30-minute reuse window;
    up to 90% discount on cached input; prompt_cache_diagnostics with reason / 
    comparison_reusable_tokens / cache_missed_tokens; prewarming; explicit cache breakpoints.
    -> 68d5055b, and it BOUNDED f5bf2d02 (see corrections).
  https://alignment.anthropic.com/2026/taste/                              (Aug 28 2026)
    Queue item (3) rank 1, and it paid. TASTE: 92 pairwise preferences over AI-safety research
    proposals, 77% estimated human agreement. Pair-discussion + strong-confidence filtering moved
    estimated agreement 53% -> 68%; a >=2-point score-gap filter reached 77%. Fable 5 best at 60%;
    almost all models within 2 SD of chance; Opus 5 and GPT-5.6-Sol near chance. Fable 5 scores 69%
    on the 74 CROSS-prompt pairs vs 60% overall. Two agreement estimators give 77% (92 pairs) vs
    83% (50 pairs). -> a0cb6dc6, 79912531, 126207f7. Paper NOT fetched (linked, unread).
errored / not obtained: NONE. No 403, 404, paywall, timeout or gate. No slug guessed — the two
  openai.com slugs came from WebSearch+allowed_domains (route 1b), not from the titles.
Appendix A: nothing crawled, nothing left — fully covered since the 8th run.

=== FACTS WRITTEN (5 new, 2 corrected, 0 enriched, 0 retracted) ===
  NEW (two knomit_learn calls, BOTH CLEAN — no dedup refusal, no serialize refusal; every motif was
  hyphen-counted before sending, per the 37th run's tool note, and all five came in at 3-4 tokens):
    kb/conventions/ai/agents/context-engineering/prompt-caching/68d5055b.md — deleting tool
      definitions to narrow an agent's tool set destroys the cached prefix; mask callability with
      allowed_tools / tool_choice instead, append instructions rather than editing them, and the
      GPT-6 specifics (configuration_update, 30-min window, diagnostics fields).
    kb/conventions/ai/agents/governance/third-party-assessment/87e86747.md — pre-register claims,
      label who proposed each, pre-agree the out-of-scope process, state what was not assessed.
    kb/gotchas/ai/agents/evaluation/llm-judge/same-prompt-pairs/a0cb6dc6.md — a judge comparing two
      completions of the SAME prompt drifts toward scoring prompt-adherence; 60% vs 69% cross-prompt.
    kb/conventions/ai/agents/evaluation/human-labels/79912531.md — the label-quality recipe with its
      numbers, its coverage cost, and the two-estimator trap (77%/92 vs 83%/50).
    kb/gotchas/ai/agents/evaluation/judge-model-selection/126207f7.md — frontier agentic rank did not
      transfer to research judgment; most models within 2 SD of chance.

=== STALENESS PASS — MODEL-VERSION AND REF-FIDELITY AXIS. 5 EXAMINED, 2 CORRECTED, 3 CONFIRMED. ===
Axis chosen: claims tied to a model version with a shipped successor, plus ref-fidelity on the
cluster this run was already reading (which is where a correction is cheapest to verify). Nothing
in the kb is yet older than 90 days (day 63), so age was not a usable selector.
  CORRECTED  kb/decisions/ai/agents/architecture/f5bf2d02.md (conf 0.65 -> 0.70, sources held at 1).
    THE DEFECT: the fact derived that fan-out pays full input rates because "each new context window
    starts a cold prefix", and stated only ONE platform precondition (that cache reads are
    discounted). The GPT-6 caching post falsifies the unstated second one: with explicit cache
    breakpoints and a reuse window spanning the fork, a worker spun off a shared prefix re-reads it
    at the cached rate, and a named customer reports forking conversations for background tasks
    became economically viable on exactly that basis. The derivation is now scoped to workers whose
    context is genuinely distinct, and weakens toward nothing inside the reuse window. sources held
    at 1 deliberately per the convention in (f) below — OpenAI BOUNDS the derivation, it does not
    corroborate it.
  CORRECTED  kb/decisions/ai/agents/tools/discovery/0915b0a2.md (conf held 0.85).
    THE DEFECT: the fact asserted "Sonnet 4.5 minimum" for the Tool Search Tool. A verbatim re-read
    of its only ref shows the docs state NO minimum and NO supported-model list — they merely use
    claude-sonnet-4-5-20250929 in the example. An example model had been promoted to a floor. Also
    added: the 49->74% / 79.5->88.1% figures are anchored to the Opus 4 and Opus 4.5 generations and
    the ~10K-token / 10-tool thresholds are Anthropic's guidance rather than a measurement. Beta
    header advanced-tool-use-2025-11-20 and the ~500-token search-tool overhead RE-VERIFIED verbatim
    and unchanged; still published as beta. DEFECT CLASS WORTH A SWEEP: an example value in a doc
    restated as a constraint. That is the same shape as the misfiled-ref and the two-number `sources`
    defects — a claim stronger than the ref that carries it.
  CONFIRMED  kb/conventions/ai/agents/tools/mcp/caching/6b072def.md — body re-read; its ref (the MCP
    2026-07-28 changelog) is live and the revision is still current per this run's tripwire.
  CONFIRMED  kb/decisions/ai/agents/model-selection/total-cost/26e77a95.md — ref re-fetched; "$79
    total ($0.19/task)" vs "$155 ($0.37/task)" over "417 tasks on the AppWorld Test Challenge"
    verbatim, and the post does attribute the gap to "Sonnet's lower cache-read pricing". Exact.
  CONFIRMED  kb/gotchas/ai/agents/evaluation/reasoning-budget/f435e753.md — one of the queue's
    never-checked bodies. Read in full: ref live, figures internally consistent, and the body is
    CLEAN of the edit-history/job-state defect. No change.
AVOID kb/principles/** (write-blocked): 0f260eea, 1d1440fe, 4166926d, a829cfd4, b9b45ff5, 1feacc9e,
f269c82f, c2f12069, 1dc822f2, db193402, 00d3ef19, 82383efe, 28ba65db.

=== CONTRADICTIONS — ONE TENSION EXAMINED AND CORRECTLY NOT WRITTEN AS A DECISION. ===
OpenAI's "never remove a tool definition mid-session" appears to contradict the pack's deferral
guidance (0915b0a2, 62c9a78b: keep definitions OUT of context). It does not, and the distinction is
now written into both facts: DEFERRING a definition so it never enters the prefix leaves the prefix
stable; DELETING one already in it rewrites the prefix. Same goal, different mechanism, no live
disagreement — so no `decisions` fact. Recorded here because the next run will meet the same
apparent clash and should not re-adjudicate it.
The TASTE facts sit alongside 0cc69d27 (inter-rater agreement is the calibration target) and
38c06627 (judge biases) without tension: 79912531 supplies the CONSTRUCTION recipe that raises the
ceiling 0cc69d27 describes, and a0cb6dc6 adds a FOURTH judge bias to 38c06627's three. Cross-linked.

=== TOOL NOTES ===
  * Browser: mcp__remote-devices__Claude_Browser__* was again the live server (5th consecutive run).
    preview_start opened openai.com/news first try; consecutive navigate calls reused tabId "seed"
    with no tab management. No 403 anywhere, no approval prompt.
  * knomit_explain on BOTH crawl-sources (68,384 chars) and fetch-routes (65,173 chars) EXCEEDED THE
    INLINE CAP and persisted to a tool-result file. This is now the normal case for those two slots,
    not an exception: budget for reading them by character-range slice, and grep them for the
    sections you need rather than reading either end to end.
  * WebSearch + allowed_domains resolved both openai.com slugs from their index titles in one call
    each. Route 1b remains the correct way to turn a browser-only index listing into a URL.
  * The read-only history-walk subagent is now the right default for the walk: 17 bodies, ~380K of
    its own tokens, none of it spent in the main run's context. Give it the hash list AND the
    "ignore history/diff, read bodies" protocol.

=== QUEUE FOR THE NEXT RUN ===
(0) *** knomit_repos FIRST. Route 10 did not recur (11 clean runs). If every remote-devices tool
    vanishes at once -> RefreshMcpTools{server: "remote-devices"}, do NOT re-bind; the handle survives. ***
(1) *** WRITE crawl-state ONCE, AT THE END. One revision = one run. ***
(2) *** WALK BY THE PROSE HASHES ABOVE and append this run's own commit when you read it.
    ALREADY_CRAWLED should reach 285 (282 + this run's 3). ***
(3) *** openai.com/news IS NOW A LIVE, PRODUCTIVE FEED — SWEEP IT EVERY RUN, NOT WHEN CONVENIENT.
    Unread and ranked from this run's sweep and the WebSearch surplus:
      /index/safety-overview-gpt-6-astra/  (Sep 3) <- still TOP of the unread openai.com backlog;
        the system-card companion to path-to-astra. Named unread since the 28th run.
      /index/trusted-access-for-cyber/     <- NEW, spotted this run. Access-tier design for cyber
        capabilities; pairs with the third-party-assessment fact 87e86747 and with 0547d73f.
      /index/safety-bug-bounty/ and /index/introducing-openai-safety-fellowship/ <- NEW, spotted
        this run. Probably programme announcements; skim for the disclosure mechanics only.
      "Introducing GPT-6 Sol and Luna" (Sep 22) <- slug NOT resolved. Framework/launch post, so
        expect capability scores; skim for the one design decision per the standing rule.
      /index/pacing-model-development-cyber-capabilities/ <- carried from the 28th run, still unread. ***
(4) alignment.anthropic.com: /2026/chive/ (counterfactual explanation testing; pairs 0372e10d) then
    /2026/conceptual-reasoning-index/ (skim, expect scores). /2026/taste/ is DONE this run — but its
    PAPER is linked and unfetched, and the paper carries the rubric, the scaffold and the fuller
    disagreement breakdown. Ranked below /chive/ because the blog post was already dense.
(5) THE OPUS 5.5 SYSTEM CARD. Route 5b on https://www.anthropic.com/claude-opus-5-5 for the href —
    do NOT guess it. Launch-post tail past 30,000 chars (watermarking, data retention) also unread.
(6) darioamodei.com/post/we-must-pace-the-frontier — the Opus 5.5 post frames the release around it
    and cites it by name. Pairs c262a592, 03fa7976, 97616086, 6866e63b, bdbdd228. Host never touched.
    NOTE: OpenAI's third-party-assessment post also opens with "As part of our efforts to pace the
    frontier", so the phrase is now load-bearing at BOTH labs — this is a cross-lab pairing.
(7) THE TWO UNREAD /institute/ POSTS: /institute/recursive-self-improvement, /institute/econ-scenarios.
    Cheap and high — the one /institute/ post read produced four facts.
(8) THE REST OF THE SEPTEMBER THREAT REPORT — five sections (surveillance, influence ops,
    conventional weapons, biological misuse, scams/fraud), at the SITE ROOT not under /news/.
(9) FEEDS: openai.com/news EVERY run now (item 3). Then embracethered (not swept for several runs),
    anthropic.com/engineering, alignment.openai.com (re-check for a 4th batch), metr.org,
    anthropic.com/news. aisi.gov.uk swept this run — next sweep in ~3 runs. MCP tripwire: one
    WebFetch, 28th consecutive.
(10) STALENESS — THE AXIS THIS RUN OPENED AND DID NOT FINISH: **a claim stronger than the ref that
    carries it.** 0915b0a2 had promoted a doc's EXAMPLE model into a stated minimum. That defect
    class is mechanical to screen for: take any fact asserting a version floor, a threshold, a
    "minimum", a "required", or an exact figure, re-read its ref verbatim, and check the ref says it.
    Aim this at the model-version-tied facts first (anything naming Opus 4, Opus 4.5, Sonnet 4.5,
    GPT-4.1, Claude 4 — all now have shipped successors). This outranks the `sources` two-number
    sweep (36th FINDING 8, ~1 real defect per 8 candidates), which remains unrun.
    Never-checked bodies: 0525e590, c5f106f3, f727c157, 5eeb059b, f1e54f16, f961973e, 65aa10a7,
    fc76b9a2, 5cce9c0c, 83004507, 00f5d991, 5bad2e60, 0c3c2d6a, b4d22cc2, 4777dc9b, fcce2200,
    fe1fd6b2, plus the 37th run's four (bad64050, 4d13f6e9, de4e90a4, ab8f0a7e) and this run's five
    (68d5055b, 87e86747, a0cb6dc6, 79912531, 126207f7). f435e753 is now CHECKED — drop it.
(11) LONG-CARRIED, take-or-delete: the three ASTRA safety-overview investigations (monitorability,
    controllability, sabotage eval) — EIGHT runs, none followed; the transcript viewer; SLEIGHT-Bench
    paper/dataset (GitHub gated, route 3f); the diffuse-ai-control paper (href unresolved); the
    benchmark supply-chain report for CVE-2026-66384 (lives only in bcbf13c2, FOURTEENTH run).
(12) www-cdn.anthropic.com PDFs (route 11, egress-denied to curl; WebFetch truncates): April
    Alignment Risk Update, Fable 5 / Mythos 5 System Card, August Risk Report (Section 5.2.3 unread),
    Advanced AI Framework. NOT re-tested this run.
(13) UNMINED FROM THIS RUN'S OWN SOURCES, if a later run wants cheap yield without a fetch: the
    third-party-assessment post's SAFEGUARDS priority area lists four assessment questions this pack
    did not turn into facts — grey-box adversarial robustness, agents-vs-cyber-defences under
    authorized realistic conditions, whether CoT monitoring stays reliable as capabilities improve
    (OpenAI states this as OPEN), and whether monitoring is implemented "in a way that cannot easily
    be disabled". The last pairs directly with de4e90a4 and 406e5a50 and is the strongest of the four.

=== FOR A HUMAN, NOT THE CRAWLER ===
(a) *** GIVE PRIVATE SLOTS AN APPEND/PATCH OP. ELEVENTH run asking, and it is now the binding
    constraint on this job's quality, not a convenience. knomit_update takes the whole body as a
    string, so editing the 68KB crawl-sources slot means re-emitting 68KB reconstructed from
    character-range slices of a persisted tool-result file — precisely the re-type-from-tool-output
    hazard the pack forbids everywhere else. So the owed edits below have now gone UNDONE FOR ELEVEN
    RUNS and the list only grows: ***
      fetch-routes ROUTE 6: the walk under-walks by half; prose hashes are the record (re-confirmed
        this run: HEAD offered 3 revisions of 18).
      fetch-routes ROUTE 9c: replace the "cannot be paged through" sentence (EIGHTH run).
      fetch-routes NEW: both state slots now exceed the inline explain cap and persist to file — this
        is the normal case, and the recipe is character-range slicing plus grep.
      fetch-routes NEW: the 37th run's response-classifier caveat (read the page, write at altitude).
      fetch-routes NEW ROUTE 12 (34th run bridge-disconnect); ROUTE 11 (www-cdn egress denial).
      fetch-routes 5c: DELETE the evaluate/querySelectorAll form (Appendix S forbids page scripts).
      crawl-sources: PROMOTE openai.com/news to every-run and record why (five runs deferred, then
        two facts on first sweep); add darioamodei.com (watch) and metr funding-update; mark this
        run's three URLs READ with their fact paths; record the 36th run's alignment.anthropic index.
(b) FIX APPENDIX S'S WALK PROTOCOL: steps 2-3 terminate several hops early. The job has now measured
    this FOUR times (route 6, 35th, 36th, 38th). Only a human can fix the spec.
(c) www-cdn.anthropic.com denied by egress policy — TENTH run asking.
(d) Route 10 (binding drift): ELEVEN clean runs. Downgrade it in fetch-routes.
(e) GitHub API not enabled (route 3f) — blocks SLEIGHT-Bench dataset and MCP spec revision-diffing.
(f) The `sources` CONVENTION (hold below org count when a second org ILLUSTRATES or BOUNDS a claim
    rather than corroborating it) is 17 runs old, was applied again this run on f5bf2d02, and is
    still not written into Appendix S. It should be.
(g) The agentic-engineering repo also carries a kb/technology/** corpus from another pipeline; check
    a knomit_query result for a BARE path before concluding a fact exists here.

PROMPT INJECTION: none observed and none acted on. No page addressed the agent, attempted to
redirect the crawl, or asked for a fetch off the work list. Every URL visited was on the work list
or came from an index/WebSearch resolution of a title on it; no slug was guessed. None of this run's
three sources reproduces attack mechanics, so nothing required the 37th run's altitude handling.
The read-only history-walk subagent was given read-only instructions, one file path and a hash list;
it reported that every past body's own injection section recorded "none acted on", and that the only
instruction-shaped strings in the history are third-party attack payloads quoted as evidence by past
runs (already flagged in their own bodies). Nothing recorded as dead, blocked or paywalled.

SUB-RULES, cumulative (the 37th run's two stand; this run adds two):
 (38th) *** A FEED DEFERRED IS A FEED UNMEASURED, NOT A FEED KNOWN TO BE LOW-YIELD. openai.com/news
   was carried as "NOT SWEPT, named" for five consecutive runs while cheaper feeds were swept every
   run and returned nothing. Swept once, it produced two of this run's five facts. The queue's
   "owed N runs" counter is the strongest yield signal this job has, and it was being read as a
   backlog item rather than as evidence. SWEEP THE MOST-OWED FEED FIRST, BEFORE THE CHEAP ONES. ***
 (38th) *** THE POST'S CATEGORY DOES NOT PREDICT ITS VALUE TO THIS PACK. The run's best source was
   filed under Product — a prompt-caching release note — and the Safety post next to it yielded one
   fact to its two. The standing "prefer method posts to framework posts" rule is about research-lab
   framework announcements; do not over-extend it into skipping vendor API release notes, which are
   where the operational specifics (exact parameter names, windows, diagnostic fields) actually live
   and which no model produces from its priors. ***
