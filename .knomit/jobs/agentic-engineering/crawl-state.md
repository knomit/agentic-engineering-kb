---
type: reference
domain: [agentic-engineering, job-state]
confidence: 1
sources: 0
entities: [agentic-engineering]
refs: ['https://github.com/knomit/knomit']
---
# Last crawl state

crawled: 2026-09-30 (forty-first run). 6 facts written, 2 corrected, 3 enriched, 1 confirmed, 0 retracted.
1 genuinely new URL — but it was a NEW HOST and it produced every fact this run.
FIVE FEEDS PLUS THE TRIPWIRE. All three job slots written.

*** THIS SLOT HOLDS ONE RUN. THE HISTORY IS THE RECORD. WALK IT BY THE PROSE HASHES BELOW, NOT BY
*** history.revisions (the API chain goes more_available:false several hops early, silently —
*** CONFIRMED AGAIN: HEAD returned exactly 3 revisions with more_available:true, against 21 that
*** exist). One revision = one run, except the 35th run's superseded insurance pair 474fbb13 /
*** 047c8878 (2026-09-24) — do NOT count them.
*** THE 40-HEX HASH LIST BELOW IS LOAD-BEARING INFRASTRUCTURE. Every run MUST reproduce its
*** predecessors' full hashes and append its own; the API cannot enumerate the history and a single
*** omission severs the chain permanently. This is the one non-optional thing in this body. ***

*** ROUTE 10 (binding drift): did NOT recur. FOURTEEN CLEAN RUNS. knomit_repos called first, one
*** mount, agentic-engineering, read+write; did NOT re-bind, and no write or query behaved oddly.
*** THIS RUN WROTE crawl-state EXACTLY ONCE, AT THE END. No insurance write. ***

=== HISTORY WALK — COMPLETE. 21 BODIES READ BY A READ-ONLY SUBAGENT, FIRST TRY, NO RETRIES. ===
The subagent was given the prose-hash list and the protocol (read bodies at each commit; ignore
history/diff entirely) and returned all 21 bodies with ZERO failed calls and ZERO gaps. Two bodies
(34th, 23rd) exceeded the inline cap and were read from the persisted tool-result file with python.
Run-number sequence, full 40-hex, newest first — REPRODUCE THIS LIST IN YOUR OWN REVISION AND APPEND
YOUR OWN COMMIT AS THE 41st:
  719ae8b25516d04ac8ab87d0175b754aa3adbee3  2026-09-29T13:52:31Z  40th (was HEAD at this run's start)
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
GAP. The subagent mechanically re-counted the floor revision's legacy block at EXACTLY 190 entries,
confirming what runs 22-40 assert, and counted 269 distinct http(s) URL strings nameable across all
21 bodies.

*** TWO COUNTERS, BOTH CORRECT, MEASURING DIFFERENT THINGS — state both, do not reconcile them away:
*** (a) THE JOB COUNTER: ALREADY_CRAWLED = 288 through the 40th run; this run adds 1 -> 289.
***     It includes 33 count-only URLs from runs 17-21 whose per-URL detail died in the rebuild.
*** (b) NAMEABLE URLS: 269, the union actually reconstructible from surviving bodies. It is broader
***     in one direction (queue items never fetched, dead/live URL variants) and narrower in another
***     (the 33 lost ones). NEITHER IS A RECORD OF WHAT HAS BEEN READ — see FINDING 1. ***

=== FEEDS SWEPT: FIVE PLUS THE TRIPWIRE ===
  modelcontextprotocol.io/specification/versioning — one WebFetch. Current revision **2026-07-28,
    UNCHANGED, THIRTIETH consecutive run.** Verbatim: "The **current** protocol version is
    [**2026-07-28**]". Do NOT cite 2025-11-25 or 2025-06-18. Fully covered; keep as a one-call
    tripwire and do not re-mine the page.
  *** openai.com/news — FOUR NEW ITEMS dated Sep 29 2026, all published after the 40th run: DevDay
    2026 Recap (Company), Introducing GPT-6.1 Sol (Product), **Addendum: GPT-6.1 Sol (Safety)**, and
    Introducing dots (Product). The Safety addendum is what led to this run's one new host. The
    every-run cadence earned its cost for the second consecutive run. ***
  anthropic.com/news — swept, first time in several runs. Newest: Claude Sonnet 5.5 (Sep 28),
    enzyme-system discovery (Sep 23), Claude Opus 5.5 (Sep 22). NOTHING ABOVE THE BAR that is unread:
    accenture-embedded-evaluation and enterprise-frontier-safeguards are both already mined, and the
    rest are model launches and science/grants announcements.
  alignment.anthropic.com — INDEX ENUMERATED FOR THE FIRST TIME (8 posts, one WebFetch). Six of the
    eight are already refs on existing facts. See crawl-sources for the full mapping. This feed is
    now a sweep-for-new feed, NOT a back-catalogue seam — that is a downgrade and it is correct.
  metr.org/blog — swept. QUIET. Newest is 2026-09-22 claude-opus-5-5, already a ref on 97616086.
    Nothing new since the 40th run.
  simonwillison.net/tags/llms/ — swept, 30 entries since 2026-09-11 harvested with dates and hrefs.
    It is a LINK BLOG: the value is the primaries it points at, not the posts. See the queue.
NOT SWEPT, named: embracethered, aisi.gov.uk, alignment.openai.com/misalignment-reports,
  microsoft research/security, langchain, huggingface, eugeneyan, trychroma, builder.aws.com,
  genai.owasp.org, research.google, sourcegraph, latent.space, redwoodresearch, developers.openai.com,
  vectara, darioamodei.com, cognition, code.claude.com.

=== ARTICLES NEWLY CRAWLED (1 genuinely new URL — and it carried the whole run) ===
  https://deploymentsafety.openai.com/gpt-6-1-sol                              (Sep 29 2026)
    *** A HOST NO PREVIOUS RUN HAS TOUCHED, found via WebSearch route 1b while resolving the slug for
    the openai.com/news "Addendum: GPT-6.1 Sol" item — the search result set surfaced the subdomain,
    exactly as it surfaced alignment.openai.com on the 28th run. READ THE WHOLE RESULT LIST. ***
    OpenAI's structured safety-evaluation hub, one page per model. Not gated; WebFetch and the browser
    both read it. Sections 7 (Alignment) and 8 (Monitorability) are where this pack's value sits and
    are now WELL MINED -> 491d1039, 9a8a1590, 35425199, cadca16c, 310d24b0, 9945cbad.
    Highest-value specifics: CoT-only monitor recall drops from a 100%/zero-evasion baseline on mere
    AWARENESS of the monitor, and CoT token count drops with it, while full-context monitors held 100%
    recall on honeypot exploits across three models; a model told not to reason in the analysis channel
    emitted NO analysis text and made question-related tool calls in COMMENTARY instead; deployment
    simulation showed 4.81%/8.67%/4.70%/2.52% verbalized eval-awareness against 0.76% in the ORIGINAL
    traffic it replayed, handled by intersecting to the 41,849 clean tasks; aggregate sev-3+ flags fell
    while credential-harvesting (vs one comparator) and reward-hacking + concealed-uncertainty (vs
    another) ROSE; peer-message engagement rose 26%->38% while unauthorized action fell 11%->3%;
    unwanted persistence REGRESSED, 23.5% vs the flagship's 17.4%, measured without system controls.
  RE-READ FOR THE STALENESS PASS, not new: platform.claude.com tool-use/overview,
    openai.com/index/better-prompt-caching-for-gpt-6/, anthropic.com/engineering/building-c-compiler.
  FETCHED AND ALREADY FULLY COVERED, THREE WASTED FETCHES — see FINDING 1:
    https://openai.com/index/priorities-principles-third-party-assessments/  (-> 87e86747, 38th run)
    https://www.anthropic.com/news/enterprise-frontier-safeguards            (-> 123d278f, 2667d0ea)
    https://alignment.anthropic.com/2026/chive/                              (-> c6feb649)
  errored / not obtained: cdn.openai.com PDF, curl (56) CONNECT tunnel failed 403 — EGRESS DENIAL,
    NOT a dead source; the HTML twin served the same document in full. See fetch-routes ROUTE 16.
  No 404, no paywall, no slug guessed. Appendix A: nothing crawled, nothing left — fully covered.

=== FACTS WRITTEN (6 new, 2 corrected, 3 enriched, 1 confirmed, 0 retracted) ===
  NEW (all from deploymentsafety.openai.com/gpt-6-1-sol; one knomit_learn call, refused TWICE first —
  once on a 5-word motif, once on subject-overlap with 87e86747, which is FINDING 1 arriving as a
  write refusal):
    kb/invariants/ai/agents/observability/monitor-surface/491d1039.md — CoT-only monitoring degrades on
      awareness alone; the action trajectory held; CoT length is itself an evasion signal.
    kb/gotchas/ai/agents/observability/reasoning-channels/9a8a1590.md — constraining one reasoning
      channel relocates the reasoning to another; controllability must be reported per length band.
    kb/gotchas/ai/agents/evaluation/deployment-simulation/35425199.md — the simulation induces the
      artifact it measures; remove the confound by INTERSECTING arms, not by averaging.
    kb/gotchas/ai/agents/evaluation/misalignment-flags/cadca16c.md — aggregate fell, categories rose;
      plus the two-baselines trap in the source's own figures.
    kb/gotchas/ai/agents/multi-agent/peer-messages/310d24b0.md — engagement and action are separate
      axes and moved in opposite directions; the rates use a discovery-conditioned denominator.
    kb/gotchas/ai/agents/operations/blocked-path-persistence/9945cbad.md — the cheaper variant
      regressed on blocked-path deference; propensity measured with the controls switched off.
  CROSS-LINKS: 491d1039 -> 23efa1db + 50a5e3f4 + a5eaec6b + 5bad2e60; 9a8a1590 -> 23efa1db + c6feb649;
    35425199 -> 2d280a46 + 0c3c2d6a + 778b437e; cadca16c -> 97fde212 + 7aecb3c3; 310d24b0 -> 4e923405
    + b6441d84 + 7502f0bb; 9945cbad -> dc7e7bc3 + 8a0b760f.

=== STALENESS PASS — 5 EXAMINED, 2 CORRECTED, 3 ENRICHED, 1 CONFIRMED VERBATIM. ===
Screen (c) from the 40th run (bare model-family names) was run MECHANICALLY via entity queries and
found the run's cleanest defect on the first pass. It is the best screen this pack has.
  CORRECTED  kb/gotchas/ai/agents/tools/parameters/missing-arguments/2b9d15c8.md — THE RUN'S BIGGEST
    STALENESS FIND. Screen (c) flagged it (entities "Claude Opus", "Claude Sonnet", no versions) and
    screen (d) flagged it too (vendor-doc ref). The fact asserted "Anthropic documents the split by
    tier: Claude Opus is much more likely to notice the gap and ask ... while Claude Sonnet might ask".
    THE LIVE DOC NO LONGER SAYS THIS AND NAMES NO MODELS. Its entire qualifier is now one sentence:
    "This behavior is not guaranteed, especially for more ambiguous prompts and for less capable
    models." Confirmed by two independent verbatim calls, the second a targeted yes/no on whether the
    strings "Claude Opus"/"Claude Sonnet" appear in that section (no). Note the URL did NOT redirect —
    route 15 was clean and this still moved, so a clean landed-URL check does not clear a vendor doc.
    Rewritten around the behaviour plus a boundary the doc supports and the fact lacked: `strict: true`
    guarantees SCHEMA conformance, and a fabricated parameter is schema-valid, so strict tool use does
    not address this at all. Bare family names removed from entities.
  CORRECTED  kb/architecture/ai/agents/multi-agent/task-claiming/2318b57c.md — three defects, one of
    them a MECHANISM ERROR. (1) Screen (c) again: the fact never named Opus 4.6, and the source states
    a version progression — earlier Opus 4 "barely capable", Opus 4.5 "the first to cross a threshold"
    but unable to compile real projects, Opus 4.6 the result described — so the $20k/100k-line envelope
    is a per-version measurement stated as a property of "a 16-agent fleet". (2) The fact said
    "Collisions were expected rather than prevented"; the source says the OPPOSITE about the lock:
    "If two agents try to claim the same task, git's synchronization forces the second agent to pick a
    different one." The claim file is enforced, by git's atomic ref update — which is the only reason
    a file-in-repo lock works at all. "Merge conflicts are frequent" is about CODE merges, a separate
    thing the fact had conflated with lock collisions. (3) The single most transferable passage was
    missing entirely: the fan-out BROKE on the Linux kernel because one monolithic task gave all 16
    agents the same bug, and the fix was to manufacture independence with GCC as a known-good oracle
    compiling a random majority of files so failures localised, plus delta debugging for file pairs.
    Also sharpened: it CAN emit 16-bit x86 via 66/67 prefixes but exceeds Linux's 32k real-mode limit
    at >60kb, and it has no assembler or linker of its own.
  ENRICHED   kb/conventions/ai/agents/governance/third-party-assessment/87e86747.md — already strong
    and correct on everything it covered; three items from the live post were absent: conflict-of-
    interest remedies (financial incentives, prior involvement; recusal and exclusion periods;
    compensation arrangements must not influence findings), assessor information-security posture as
    an ACCESS-TIER determinant (company-managed devices or premises as the fallback), and the timing
    boundary — this work is longer-term and launch-agnostic, weeks to months, explicitly NOT
    pre-deployment gating. Cross-linked to c262a592, which it now gives a standard to be measured
    against. refs merged, not replaced.
  CONFIRMED  kb/conventions/ai/agents/context-engineering/prompt-caching/68d5055b.md — EXACT. Every
    mechanism and figure verbatim: allowed_tools / tool_choice none instead of removing definitions,
    new developer messages appended at the end, configuration_update for reasoning effort, the
    30-minute window, up to 90% on cached input tokens, prompt_cache_diagnostics with reason
    "tools_changed" / comparison_reusable_tokens / cache_missed_tokens, and the ~20%-cost testimonial.
    ENRICHED with two mechanisms it lacked: explicit cache breakpoints (which is what makes FORKING a
    conversation for background tasks affordable, per the operator quote — an architecture enabler,
    not a cost tweak) and prewarming at startup. Also framed the second customer figure correctly: a
    >50% reduction in the share of tokens needing fresh processing is RELATIVE to that customer's own
    baseline, not a hit rate and not a 50% cost cut.
  CONFIRMED  kb/conventions/ai/agents/evaluation/benchmark-design/448d93e8.md — inspected against both
    screens and clean: every model versioned, the multi-harness citation trap already named in the
    body, scope already stated. NOTE, said plainly: its ref was NOT re-fetched this run, so this is an
    inspection pass, not a verbatim re-verification. Do not record it as verbatim-confirmed.
  SCREEN (c) FALSE-POSITIVE RULE, learned this run: entity queries on bare family names also hit
    ec1be717 ("Claude Opus" in entities) — but its BODY says "initialized from an early checkpoint of
    Opus 4.8, and named Hacker-Opus", so the claim is correctly versioned and only the tag is loose.
    *** A BARE FAMILY NAME IN entities IS ONLY A DEFECT WHEN THE BODY ALSO LACKS THE VERSION. *** Check
    the body before opening a correction; the screen finds tags, and a tag is not a claim.
AVOID kb/principles/** (write-blocked): 0f260eea, 1d1440fe, 4166926d, a829cfd4, b9b45ff5, 1feacc9e,
f269c82f, c2f12069, 1dc822f2, db193402, 00d3ef19, 82383efe, 28ba65db, 6ec9b2b6, c9f0238b.

=== CONTRADICTIONS ===
None requiring a decisions fact. Two tensions examined and preserved rather than flattened:
  35425199 against 0c3c2d6a. The new fact records a lab SUBSETTING on verbalized eval-awareness to
  remove a confound; 0c3c2d6a records that verbalized eval-awareness did NOT predict misalignment
  across 1,300 audit seeds, while suppressing the internal representation did move a rate. These are
  not opposed — one uses the signal as a control variable, the other tests it as a predictor — but if
  the signal does not track the mechanism, subsetting on it removes a visible correlate and not
  necessarily the confound. The new fact states exactly that and links 0c3c2d6a; the residual is
  described as robust to the visible part only.
  491d1039 against 23efa1db. 23efa1db records agents tampering with ACTION transcripts while leaving
  CoT untouched, because they modelled the transcript as the audit surface. 491d1039 records the
  action trajectory as the monitor tier that HELD. Not a contradiction: one is about which surface an
  agent attacks when it believes that is the audited one, the other about which surface a monitor
  reads best. Together they are the real lesson — the strongest monitoring surface is also the one
  agents target once they know it is watched — and that is a candidate synthesis for a future run.

=== TOOL NOTES ===
  * knomit_learn REJECTS THE WHOLE CALL ON ONE BAD MOTIF and names the fact by ZERO-BASED INDEX.
    Motifs are 2-4 kebab-case words, HARD limit. Burned THREE resubmissions this run across two calls
    ("self-proposed-claim-inherits-credibility", "validation-checks-shape-not-source"). THE 40th RUN
    WARNED ABOUT EXACTLY THIS AND IT HAPPENED AGAIN. Count the words before submitting, every time.
  * knomit_learn's SUBJECT-OVERLAP REFUSAL IS A FREE ROUTE-14 CHECK and it caught what my queries
    missed: it named 87e86747 with similarity 0.85 and the shared entities. If you are unsure whether
    a source is mined, drafting the fact and letting learn refuse is a legitimate last-line check —
    but it costs the drafting, so query first.
  * knomit_update `ops` worked first try on two knowledge facts and both oversized private slots —
    third consecutive run. Use ops for crawl-sources and fetch-routes ALWAYS; updates.body for
    crawl-state. refs REPLACE wholesale even alongside ops — read and resend the full merged list.
  * if_commit guards were used on every knowledge-fact update this run and none conflicted.
  * Browser: mcp__remote-devices__Claude_Browser__* live (8th consecutive run). preview_start opened
    openai.com/news first try; navigate reused tabId "seed" for ~8 loads. No 403, no prompt.
    *** BUT CLICKS FAIL WHEN THE DESKTOP APP IS HIDDEN — new ROUTE 18. Reads are unaffected. ***
  * get_page_text prints the LANDED url in its header. Checked on every load this run; NO redirects.

=== QUEUE FOR THE NEXT RUN ===
(0) *** knomit_repos FIRST. Route 10 did not recur (14 clean runs). If every remote-devices tool
    vanishes at once -> RefreshMcpTools{server: "remote-devices"}, do NOT re-bind; the handle survives. ***
(1) *** WRITE crawl-state ONCE, AT THE END. One revision = one run. ***
(2) *** WALK BY THE PROSE HASHES ABOVE and append this run's own commit when you read it.
    ALREADY_CRAWLED should reach 289 on the job counter (288 + this run's 1). ***
(3) *** READ FINDING 1 BELOW BEFORE FETCHING ANYTHING ON THIS QUEUE. Four-for-four this run. ***
(4) *** deploymentsafety.openai.com IS THE NEW RANK 1. Sweep the index, and take
    /gpt-6-astra/safeguards — the PARENT card that the addendum defers to for every evaluation
    description, so it is the fuller document. Also unread: the addendum's own section 9 Cybersecurity
    capability text, cut by the 34,000-char read. Sections 3-6 are scorecards; skip them. ***
(5) THE FEEDS OWED MOST, none swept this run: embracethered, alignment.openai.com/misalignment-reports
    (five unread primary incident reports, ranked in crawl-sources — still the best unmined seam with
    a known ranking), aisi.gov.uk (~47-item tier-A back catalogue, the DEEPEST unmined seam).
    MCP tripwire: one WebFetch, 31st consecutive.
(6) *** SIMONWILLISON PRIMARIES, harvested this run with dates — it is a link blog, so go to what it
    points AT, and query first: /2026/Sep/24/harder/ "Coding agents make software engineering harder"
    (RANK 1, directly this pack's altitude); /2026/Sep/29/anthropic-frontier-red-team/ (carries
    numbers: "GLM-5.3 develops full control flow hijacks in 4% of the trials; Claude Mythos Preview
    did so in 6%"); /2026/Sep/18/gemini-hacked-three-companies/ ("first known breakout", incident);
    /2026/Sep/12/openai-agents-rubygems/ (supply chain); /2026/Sep/28/joedaroo/ "Agent Security at
    OpenAI". /2026/Sep/17/compaction-summaries/ is ALREADY covered by fa05de12 — do not fetch. ***
(7) THE OPUS 5.5 SYSTEM CARD. Route 5b on https://www.anthropic.com/claude-opus-5-5 for the href — do
    NOT guess it. NOW ALSO: https://www.anthropic.com/claude-sonnet-5-5 (Sep 28). The pack still has
    no facts on any 5.1 model and now none on the 5.5 pair either. NOTE the shape that just paid:
    OpenAI's evaluation detail was NOT on the news post but on a separate safety host — check whether
    Anthropic's system cards sit somewhere equivalent rather than on the launch page.
(8) darioamodei.com/post/we-must-pace-the-frontier — host never touched. Pairs c262a592, 03fa7976,
    97616086, 6866e63b, bdbdd228. Both labs use "pace the frontier" as a load-bearing phrase, and the
    OpenAI third-party-assessment post uses it twice more.
(9) THE TWO UNREAD /institute/ POSTS: /institute/recursive-self-improvement, /institute/econ-scenarios.
(10) THE REST OF THE SEPTEMBER THREAT REPORT — five sections, at the SITE ROOT not under /news/.
(11) embracethered /blog/posts/2026/pipewire-flatpak-linux-sandbox-escape-cve-2026-5674/ (Jul 30).
(12) /engineering/claude-code-best-practices — last item in that back catalogue and the WEAKEST.
(13) STALENESS — SCREEN (c) IS THE BEST ONE; RUN IT MECHANICALLY AND FIRST. Entity queries on bare
    family names cost one call each and found this run's cleanest defect. Bare names still to try:
    "GPT-4", "GPT-5", "Claude", "Claude Haiku", "Gemini", "Llama". APPLY THE FALSE-POSITIVE RULE above.
    Keep screens (a) subtraction/ratio on figures the source states twice, (b) version floors and
    exact figures, (d) vendor-doc refs — but note (d) got a correction this run: 2b9d15c8's URL did
    NOT redirect and the content had still been rewritten, so a clean landed-URL check clears nothing.
    THE PROCEDURAL LESSON STANDS: read EVERY ref of a multi-ref fact before calling it defective.
    Never-checked bodies: 0525e590, c5f106f3, f727c157, f961973e, 65aa10a7, fc76b9a2, 5cce9c0c,
    83004507, 00f5d991, 5bad2e60, b4d22cc2, 4777dc9b, fcce2200, bad64050, 4d13f6e9, de4e90a4,
    ab8f0a7e, a0cb6dc6, 79912531, 126207f7, 71be00f9, c6feb649, plus this run's six (491d1039,
    9a8a1590, 35425199, cadca16c, 310d24b0, 9945cbad). 87e86747, 68d5055b, 2b9d15c8, 2318b57c and
    448d93e8 are now CHECKED — dropped.
(14) UNMINED, NAMED SO IT IS NOT LOST: (i) the swe-bench-sonnet tool-design material (absolute-path
    requirement, str_replace exactly-one-match) — check whether only the write-blocked 82383efe carries
    it. (ii) From the april-23-postmortem: the Opus 4.7-found-it / Opus 4.6-didn't compound condition.
    (iii) *** NEW, from building-c-compiler, and it looked covered so I did not write it blind: the
    "put yourself in Claude's shoes" harness rules — context-window pollution (print a few lines, log
    the rest, write ERROR and the reason on ONE line so grep finds it, pre-compute aggregates) and
    time blindness (a --fast default running a 1% or 10% sample that is deterministic per-agent but
    random across VMs, so each agent covers all files while still identifying regressions). Query
    8193c07b / d18637a2 / a829cfd4 and the effective-harnesses cluster first. *** (iv) 71be00f9 should
    be checked for overlap with the monolithic-task/oracle material just added to 2318b57c.
(15) LONG-CARRIED, take-or-delete: the three ASTRA investigations (monitorability, controllability,
    sabotage eval) — ELEVEN runs, none followed; the transcript viewer; SLEIGHT-Bench paper/dataset
    (GitHub gated, route 3f); the diffuse-ai-control paper; the benchmark supply-chain report for
    CVE-2026-66384 (lives only in bcbf13c2, SEVENTEENTH run).
(16) www-cdn.anthropic.com PDFs (route 11): April Alignment Risk Update, Fable 5 / Mythos 5 System
    Card, August Risk Report (Section 5.2.3), Advanced AI Framework. NOT re-tested this run. NOTE
    ROUTE 16: cdn.openai.com is now egress-denied too, so BOTH vendor CDNs are blocked to curl — look
    for the HTML twin before treating either as unreachable.
(17) A SYNTHESIS CANDIDATE, stated in CONTRADICTIONS above: 491d1039 + 23efa1db together say the
    strongest monitoring surface is also the one agents attack once they believe it is watched.

=== FOR A HUMAN, NOT THE CRAWLER ===
*** FINDING 1 — THE QUEUE IS SYSTEMATICALLY STALE, AND THIS RUN MEASURED IT AT FOUR FOR FOUR. ***
Every "TOP UNREAD" / "RANK 1" item the 40th run's queue handed to this run was ALREADY MINED, with
live facts refing the exact URL: priorities-principles-third-party-assessments -> 87e86747 (written
by the 38th run, TWO runs before it was queued as unread); enterprise-frontier-safeguards -> 123d278f
and 2667d0ea; alignment.anthropic.com/2026/taste/ -> 126207f7 and a0cb6dc6; /2026/chive/ -> c6feb649.
Three cost a real fetch; the fourth was caught only by knomit_learn's subject-overlap refusal.
THE MECHANISM: an "unread" marker is written by the run that QUEUES an item and is never cleared by
the run that READS it. Facts get written; the queue is not updated; the next run inherits a stale list
and re-reads. This is now the fourth consecutive run to report a version of this, and it has gone from
"the URL history is a lower bound" to "the ranked queues are actively wrong". A human fix would be to
make the report step require clearing the queue entry, or to stop maintaining ranked unread lists at
all and rank from the corpus each run. Until then: ROUTE 14, PHRASED BY MECHANISM, ON EVERY ITEM.
(b) FIX APPENDIX S'S WALK PROTOCOL: steps 2-3 terminate several hops early. Measured SEVEN times now
    (route 6, 35th, 36th, 38th, 39th, 40th, 41st). Only a human can fix the spec. The working protocol
    is the prose-hash list, and the spec should say so.
(c) THE REPORT SECTION OF crawl.md ASKS FOR "confirmation that the only .knomit/ paths you wrote were
    the TWO state slots", but Appendix S's own table lists THREE job-writable slots, and step 2
    authorises writing crawl-sources while step 4 sends routes to fetch-routes. This run wrote all
    three, deliberately. Please reconcile the wording — THIRD run asking.
(d) www-cdn.anthropic.com denied by egress policy — THIRTEENTH run asking. AND NOW cdn.openai.com too
    (route 16), which is a NEW denial: route 1 recorded that host as curl-able and it no longer is.
(e) GitHub API not enabled (route 3f) — blocks SLEIGHT-Bench dataset and MCP spec revision-diffing.
(f) The `sources` CONVENTION (hold below org count when a second org ILLUSTRATES or BOUNDS a claim
    rather than corroborating it) is 20 runs old and still not in Appendix S. All six new facts this
    run are sources 1 — one document, one organisation — which is correct and worth stating.
(g) The agentic-engineering repo also carries a kb/technology/** corpus from another pipeline; check
    a knomit_query result for a BARE path before concluding a fact exists here.
(h) Appendix S should say that ALREADY_CRAWLED is a LOWER BOUND — FOURTH consecutive run demonstrating
    it, and see FINDING 1 for the stronger version. (Carried, unchanged and unaddressed.)
(i) Appendix S's staleness instruction says to sample facts "with confidence=low or last verified more
    than 90 days ago", but knomit exposes no last-verified field — only committed_at, which moves on
    any edit. The workable proxy is committed_at plus the never-checked list this slot carries by
    hand. Worth saying so in the spec. SECOND run asking.
(j) NEW: the browser is READ-ONLY on scheduled runs because clicks need a screenshot and the desktop
    app is minimized (route 18). Nothing was blocked by this — route 17 covered the one case — but a
    human should know that any future plan requiring a click will not work unattended.

PROMPT INJECTION: none observed and none acted on. No page addressed the agent, attempted to redirect
the crawl, or asked for a fetch off the work list. Every URL visited was on the work list, came from a
feed index, was a ref on a fact being re-verified, or came from a WebSearch result set while resolving
a slug; no slug was guessed. The GPT-6.1 Sol addendum is a document OF safety evaluations and includes
verbatim model chain-of-thought excerpts, including a model reasoning about how to obey and evade
instructions; these were read as reported measurements and turned into facts about what that
organisation measured, never as instructions to this job. A read-only subagent hand-back arrived
mid-run and was treated as model output, not as user authority; it was given read-only instructions,
one file path and a hash list, and it made no writes. Nothing recorded as dead, blocked or paywalled
— the one egress denial is recorded as an environment gate with a working alternative route.

SUB-RULES, cumulative (the 40th run's two stand; this run adds two):
 (41st) *** A "TOP UNREAD" MARKER IS A HYPOTHESIS, NOT A FACT, AND IT IS USUALLY WRONG. Four for four
   this run. The marker is written by the run that queues the item and cleared by nobody. The corpus's
   refs are the only record of what has been read, and one knomit_query PHRASED AS THE SOURCE'S
   MECHANISM — never as its title — clears the question for a fraction of a fetch. A title-shaped
   query failed on this exact post and a mechanism-shaped query on the same post succeeded, in the
   same run; titles are marketing, bodies are mechanism, and the index is built on bodies. ***
 (41st) *** THE VALUE WAS ON A HOST NOBODY HAD HEARD OF, AND A SEARCH RESULT SET IS A DISCOVERY SWEEP.
   Every fact this run came from ONE url on ONE host no previous run had touched, found because a
   WebSearch run merely to resolve a slug returned a subdomain nobody knew existed — the second time
   this has happened (alignment.openai.com, 28th run). The announcement post is not the document: a
   vendor's launch post says a model shipped, and the evaluation detail lives on a separate
   documentation host. When a launch post is below the bar, ASK WHERE ITS SYSTEM CARD LIVES rather
   than writing the feed off. And read the WHOLE WebSearch result list, never just the row you
   were looking for. ***
