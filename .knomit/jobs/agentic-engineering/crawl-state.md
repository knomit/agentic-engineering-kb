---
type: reference
domain: [agentic-engineering, job-state]
confidence: 1
sources: 0
entities: [agentic-engineering]
refs: ['https://github.com/knomit/knomit']
---
# Last crawl state

crawled: 2026-09-28 (thirty-ninth run). ONE DAY after the 38th. 4 facts written, 1 corrected,
1 enriched, 0 retracted, 3 confirmed. 3 genuinely new URLs. SIX FEEDS PLUS THE TRIPWIRE.
*** THE ELEVEN-RUN BLOCKER ON EDITING crawl-sources AND fetch-routes IS RETIRED: knomit_update
*** accepts an `ops` array (append / str_replace) that patches a slot without re-emitting its body.
*** BOTH SLOTS WERE EDITED THIS RUN, FOR THE FIRST TIME IN TWELVE RUNS. See fetch-routes ROUTE 13. ***

*** THIS SLOT HOLDS ONE RUN. THE HISTORY IS THE RECORD. WALK IT BY THE PROSE HASHES BELOW, NOT BY
*** history.revisions (the API chain goes more_available:false several hops early, silently —
*** CONFIRMED AGAIN THIS RUN: HEAD returned exactly 3 revisions with more_available:true, against 19
*** that exist). One revision = one run, except the 35th run's superseded insurance pair
*** 474fbb13 / 047c8878 (2026-09-24) — do NOT count them.
*** THE 40-HEX HASH LIST BELOW IS LOAD-BEARING INFRASTRUCTURE. Every run MUST reproduce its
*** predecessors' full hashes and append its own; the API cannot enumerate the history and a single
*** omission severs the chain permanently. This is the one non-optional thing in this body. ***

*** ROUTE 10 (binding drift): did NOT recur. TWELVE CLEAN RUNS. knomit_repos called first, one mount,
*** agentic-engineering, read+write; did NOT re-bind, and no write or query behaved oddly. ***
*** THIS RUN WROTE crawl-state EXACTLY ONCE, AT THE END. No insurance write. The bridge held. ***
*** No response-classifier trip. One source this run (embracethered/LiteLLM) touches attack
*** mechanics and was NOT turned into a fact — it was already in the corpus; see FINDING 1. ***

=== HISTORY WALK — COMPLETE. 19 BODIES READ BY A READ-ONLY SUBAGENT, FIRST TRY, NO RETRIES. ===
A read-only subagent was given the prose-hash list and the protocol (read bodies at each commit;
ignore history/diff fields entirely) and returned all 19 bodies with ZERO failed calls and ZERO gaps.
Two bodies (34th, 23rd) exceeded the inline cap and were read from the persisted tool-result file.
Run-number sequence, full 40-hex, newest first — REPRODUCE THIS LIST IN YOUR OWN REVISION:
  092218eef959413b6ebf8589b29ecf5a37e5a49f  2026-09-27T13:40:18Z  38th (was HEAD at this run's start)
  7a39df486016fcd1dc19831a8675224b2bc9d447  2026-09-26T13:51:25Z  37th
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
The walk terminates because the FLOOR is reached, not because more_available went false — the API's
more_available is not the stop condition and was not consulted. NO CALL FAILED. GAP: runs 14, 15,
17-21 have no revision (one-off repo rebuild between the 22nd and 23rd) — the SAME known gap, NO NEW GAP.

*** ALREADY_CRAWLED = 285 through the 38th run. *** = the 38th body's 282 + that run's 3. The 38th
re-derived the partition of the floor's block and found it disagrees with the 37th by one; the NAMED
SET IS IDENTICAL and nothing turns on the total, so this run did not re-derive it. Do not chase it.
This run adds 3 -> next run's ALREADY_CRAWLED = 288.
*** BUT SEE FINDING 1: the per-run URL lists in this history are NOT a complete record of what has
*** been read. Several URLs absent from every body's URL list are carried as refs by existing facts.
*** ALREADY_CRAWLED is a LOWER BOUND on what has been read, and the corpus's refs are the upper one. ***

=== FEEDS SWEPT: SIX PLUS THE TRIPWIRE. TWO HAD UNREAD MATERIAL; NEITHER WAS "NEW". ===
  modelcontextprotocol.io/specification/versioning — one WebFetch. Current revision **2026-07-28,
    UNCHANGED, TWENTY-EIGHTH consecutive run.** Verbatim: "The **current** protocol version is
    [**2026-07-28**]". Do NOT cite 2025-11-25 or 2025-06-18 as current. The page's substantive
    content (per-request negotiation via io.modelcontextprotocol/protocolVersion, server/discover as
    a mandatory RPC, UnsupportedProtocolVersionError, the >=12-month / >=90-day expedited deprecation
    window) is ALREADY fully covered by 031dab74, 995c167b, fa61c895, 3afa31af, f4367bd0, 012daf73.
    Nothing to write. Keep it as a one-call tripwire and do not re-mine the page.
  *** www.anthropic.com/engineering — THE RUN'S BEST SOURCE, AND IT WAS NOT NEW. Full index of 25
    posts enumerated in one WebFetch. Newest is still how-we-contain-claude / april-23-postmortem, so
    the "quiet since Apr 2026" label carried for many runs was TRUE about the newest date and FALSE
    about coverage: two posts from early 2026 had never been read and produced three of this run's
    four facts. Full read/unread inventory now recorded in crawl-sources. ***
  openai.com/news — QUIET. Swept in the browser (route 1) at the 38th run's new every-run cadence.
    Front page identical to the 38th run's sweep: newest still the four Sep 23 items
    (two-years-of-openai-academy, Altman UN Security Council, ChatGPT Ads SE Asia, Airbnb GPT-6
    Astra). Nothing newer. One call, correct price for the cadence.
  embracethered.com/blog — SWEPT (owed several runs). 15 most recent listed. THREE posts looked
    unread against the history's URL lists; TWO of them are already refs on existing facts (see
    FINDING 1). Only /blog/posts/2026/pipewire-flatpak-linux-sandbox-escape-cve-2026-5674/
    (Jul 30 2026) is genuinely unread. Nothing newer than Aug 26 2026 — FIVE WEEKS QUIET.
  metr.org/blog — QUIET. Full 24-post index returned. Newest still /blog/2026-09-22-claude-opus-5-5/
    (read 36th). Still uncrawled: /blog/2026-08-14-funding-update/ (low value, funding),
    /blog/2026-06-26-gpt-5-6-sol/, /blog/2026-05-08-rd-section-anthropic-risk-report-feb-2026-review/,
    /blog/2026-03-12-sabotage-risk-report-opus-4-6-review/,
    /blog/2026-02-17-how-we-protect-confidential-information/,
    /blog/2025-12-09-common-elements-of-frontier-ai-safety-policies/. THIRD-PARTY-HACKING FOLLOW-UP
    still not published — FOURTEEN runs.
  alignment.openai.com/misalignment-reports — QUIET. Index still 9 reports, newest still the three of
    2026-09-25. NO fourth batch. All 9 are in ALREADY_CRAWLED.
  alignment.anthropic.com — not re-enumerated (the 36th run's index of 84 posts stands). ONE post
    from that index was READ (below).
NOT SWEPT, named: anthropic.com/news, simonwillison, microsoft research/security, langchain,
  huggingface, eugeneyan, trychroma, builder.aws.com (route: browser/JS), genai.owasp.org,
  research.google, sourcegraph, latent.space, redwoodresearch, developers.openai.com, vectara,
  darioamodei.com, cognition, aisi.gov.uk (swept 38th; next sweep ~2 runs).

=== ARTICLES NEWLY CRAWLED (3 new URLs) ===
  https://www.anthropic.com/engineering/building-c-compiler                 (Feb 05 2026)
    THE RUN'S BEST SOURCE. 16 agents, ~2,000 Claude Code sessions, two weeks, 2B input / 140M output
    tokens, just under $20,000, a 100,000-line compiler at 99% pass rate on most compiler test suites,
    compiling Linux 6.9 on x86/ARM/RISC-V. Coordination was a claim FILE in the repo
    (current_tasks/parse_if_statement.txt), per-agent containers cloning to /workspace, merge
    conflicts expected and left to the model. Standing roles for dedup / perf / codegen / docs.
    THE FAILURE: aimed at the Linux kernel as ONE target, "Every agent would hit the same bug, fix
    that bug, and then overwrite each other's changes. Having 16 agents running didn't help" — fixed
    by using GCC as an online known-good oracle to partition the kernel. Also: lacks efficient
    codegen and 16-bit x86, and "frequently broke existing functionality". -> 71be00f9, 2318b57c,
    and it BOUNDED f7dee43a.
  https://www.anthropic.com/engineering/AI-resistant-technical-evaluations  (Jan 21 2026)
    A hiring take-home maintained since Nov 2023 (4h limit, later 2h). Shortening the clock FAILED
    (Opus 4.5 in a casual Claude Code session hit 1790 cycles, matching the best human at 2h); adding
    depth FAILED; picking a harder well-known problem FAILED (data transposition, bank conflicts
    saturate). Only "sufficiently out of distribution" worked — a constrained puzzle-game instruction
    set. "over 50% of candidates would have been better off delegating to Claude Code entirely."
    Six cycle counts for the same task across model/harness/time configurations: 2164 (Opus 4, many
    hours, harness, May 2025), 1790 (Opus 4.5, casual session), 1579 (Opus 4.5, 2h harness), 1548
    (Sonnet 4.5, many more than 2h), 1487 (Opus 4.5, 11.5h), 1363 (Opus 4.5, improved harness).
    Fewer is better. -> 448d93e8.
  https://alignment.anthropic.com/2026/chive/                               (queue item (4) rank 1)
    CHIVE: sample 30 responses per prompt, screen with an investigator model, run 5-15 counterfactual
    prompt edits per behaviour, verify with an independent judge. Predictor Claude Opus 4.8; targets
    Gemma, Qwen3-8B, Qwen3.5-397B-A17B. Activation oracles, natural-language autoencoders and sparse
    autoencoders each given "5 read-only calls on the target model's activations". "No tool beats the
    transcript-only baseline" — mechanism: tool outputs name the features and the behaviours but
    "almost never explicitly state the causal relationship between them". Training on counterfactual
    prediction DID beat base models and generalised. Limits: ground truth needs sampling access;
    discovered behaviours "fairly simple"; most system-card studies lack a transcript-reading
    reference. -> c6feb649. Paper NOT fetched.
RE-READ FOR THE STALENESS PASS, not new: infrastructure-noise, claude-think-tool, sleight-bench,
  reward-seeker, agentic-misalignment-summer-2026, advanced-tool-use.
FETCHED AND ALREADY COVERED, zero yield — see FINDING 1: openai.com/index/safety-overview-gpt-6-astra/
  (browser), embracethered/hijacking-litellm-for-fun-and-profit.
errored / not obtained: NONE. No 403, 404, paywall, timeout or gate. No slug guessed.
Appendix A: nothing crawled, nothing left — fully covered since the 8th run.

=== FACTS WRITTEN (4 new, 1 corrected, 1 enriched, 3 confirmed, 0 retracted) ===
  NEW (one knomit_learn call; refused once on fact 0 against 984a2491 and resubmitted with
  distinct_from, which was the correct resolution — 984a2491 is about how much CONTEXT to give a
  second agent, this is about whether the decomposition is viable at all):
    kb/decisions/ai/agents/multi-agent/parallel-writes/71be00f9.md — the same organisation's two
      reports pull opposite ways on parallel agents writing code; the separating conditions are a
      per-unit mechanical verifier that needs no sibling's work PLUS an exclusive claim, and the
      failure of an unpartitioned target is CONVERGENCE (duplicate work, then clobbering) rather than
      the divergence the earlier sources describe.
    kb/architecture/ai/agents/multi-agent/task-claiming/2318b57c.md — claim files in the repo as the
      mutual-exclusion mechanism, the standing janitorial roles, and the full cost envelope. Notes the
      ~14:1 input:output ratio: a write fleet's bill is re-reading context, so cache economics decide
      affordability.
    kb/conventions/ai/agents/evaluation/benchmark-design/448d93e8.md — three documented failed fixes
      for a saturating evaluation and the one that worked; plus the trap that the source gives six
      cycle counts for one task and the within-version spread exceeds the between-version gap.
    kb/decisions/ai/agents/observability/interpretability-tooling/c6feb649.md — establish the
      transcript-reading baseline before adopting activation-level tooling, and make the tooling beat
      it on a prediction task rather than on how interpretable its output looks.
  CROSS-LINKS WRITTEN: f7dee43a <-> 71be00f9 (mutual), 71be00f9 <-> 2318b57c (mutual),
    448d93e8 -> 8193c07b, c6feb649 -> 0372e10d, 71be00f9 -> 984a2491 + 9aaea0dc.

=== STALENESS PASS — AXIS: A CLAIM STRONGER THAN THE REF THAT CARRIES IT (queue item (10)). ===
5 EXAMINED, 1 CORRECTED, 1 ENRICHED, 3 CONFIRMED. Every candidate was chosen for asserting a version
floor, a threshold, a "minimum", or an exact figure, and every ref was re-fetched verbatim.
  CORRECTED  kb/decisions/ai/agents/reasoning/think-tool/d4e3b247.md (title changed; conf held 0.80;
    sources held 1). TWO defects, one of them a NEW SUB-CLASS of this axis.
    DEFECT A — the title asserted "Anthropic now recommends extended thinking INSTEAD of a dedicated
    'think' tool". The live page gives a CONDITIONAL SPLIT, quoted verbatim in the corrected body:
    extended thinking for "simpler tool use scenarios like non-sequential tool calls or
    straightforward instruction following", while "The 'think' tool is better suited for when Claude
    needs to call complex tools, analyze tool outputs carefully in long chains of tool calls, navigate
    policy-heavy environments with detailed guidelines, or make sequential decisions where each step
    builds on previous ones and mistakes are costly." A replacement had been asserted where the source
    states a split, and the dropped half is where the tool is still recommended.
    DEFECT B, THE NEW SUB-CLASS — *** AN ARITHMETIC CONCLUSION COMPUTED ACROSS TWO NUMBER SETS THE
    SOURCE STATES SEPARATELY. *** The page gives baseline 0.370 / think+prompt 0.570 in PROSE and
    baseline 0.332 / Think+Prompt 0.584 in its TABLE. The fact took the prose baseline (0.370) and the
    table's tool-alone row (0.404) and derived "the tool alone bought 0.034". Against the table's own
    baseline the tool alone bought 0.072 — more than double. The derived number was not wrong about
    any single quoted figure and was still not a result the source states. SCREEN FOR THIS: any fact
    whose body performs a subtraction or a ratio on figures it quotes, where the source presents those
    figures in two different places. This is mechanical to look for and distinct from an overstated
    quote.
    The conditional-split content, the retail 0.812 figure, the SWE-bench 1.6% isolated effect and the
    Claude 3.7 Sonnet version scope were all re-verified and retained.
  ENRICHED   kb/gotchas/ai/agents/evaluation/benchmarks/infrastructure/d18637a2.md (conf held 0.90).
    The "~6 points" was accurate and correctly attributed ("the gap between the most- and
    least-resourced setups on Terminal-Bench 2.0 was 6 percentage points (p < 0.01)", same model, same
    harness, same task set) — but unbounded. Added: SWE-bench moved only 1.54pp at 5x vs 1x over 227
    problems x 10 samples, so the direction generalises and the magnitude does not; and the gap
    contains TWO mechanisms (strict->3x ~3.7pp, primarily infrastructure errors disappearing;
    3x->uncapped ~4pp, agents attempting resource-intensive approaches) which do NOT sum to the
    headline 6, so cite the headline or a step but never the sum. Cross-vendor transfer recorded as
    unestablished per the source's own hedge.
  CONFIRMED  kb/architecture/ai/agents/observability/monitor-scaffold/fe1fd6b2.md — ref re-fetched;
    "~10x more model invocations and generates ~14x more output tokens than the API call", Claude Opus
    4.6, verbatim. The baseline is a passive transcript-reading API call, which the body states. Exact.
    Was on the never-checked list — drop it.
  CONFIRMED  kb/decisions/ai/agents/evaluation/eval-awareness-measurement/0c3c2d6a.md — the 0%->~7%
    claim is NOT on reward-seeker (its first ref) and IS on its second ref, verbatim: "suppressing
    internal representations of evaluation awareness raised Sonnet 4.5's blackmail rate from 0% to
    ~7%". A single-ref check would have produced a FALSE defect report here; a two-ref fact needs both
    refs read before it is called wrong. Minor imprecision left unfixed and recorded instead: the fact
    says "1,300 audit seeds" where reward-seeker says "~1300 handwritten scenarios" — an approximation
    rendered as exact and a terminology substitution. Not worth a revision on its own; fix it if the
    fact is opened for another reason. Was on the never-checked list — drop it.
  CONFIRMED  kb/architecture/ai/agents/tools/code-execution/fc911d9c.md — body read in full and its
    ref re-fetched. `"allowed_callers": ["code_execution_20250825"]`, 43,588 -> 27,297 tokens / 37%,
    25.6% -> 28.5%, 46.5% -> 51.2% all verbatim and correctly attributed; the "processed in the Code
    Execution environment rather than Claude's context" mechanism is the source's own wording. No
    claim exceeds its refs. Exact.
AVOID kb/principles/** (write-blocked): 0f260eea, 1d1440fe, 4166926d, a829cfd4, b9b45ff5, 1feacc9e,
f269c82f, c2f12069, 1dc822f2, db193402, 00d3ef19, 82383efe, 28ba65db, 6ec9b2b6.

=== CONTRADICTIONS ===
ONE GENUINE SAME-ORGANISATION TENSION, WRITTEN AS A decisions FACT RATHER THAN FLATTENED.
Anthropic's multi-agent-research-system post names coding and heavily-interdependent work as
unsuitable for fan-out, and 9aaea0dc / f7dee43a / 984a2491 all carry that line. Anthropic's
building-c-compiler post is 16 agents concurrently writing code, successfully. Neither side was
picked: 71be00f9 names the conditions (per-unit mechanical verifier + exclusive claim) under which
each holds, cites all four sources, and f7dee43a received a BOUND paragraph pointing at it. The two
failure modes are genuinely different — divergence into incompatible artifacts (fixed by
single-threading writes) versus convergence on duplicate work (fixed by partitioning the target) —
and conflating them is how a reader applies the wrong fix.
No tension between 448d93e8 and the harness-configuration cluster (8193c07b, a829cfd4, d18637a2): it
supplies a fourth instance of the same configuration-dependence, cross-linked.
No tension between c6feb649 and 0372e10d: one is a null result on activation tooling, the other a
positive result on prompt framing. Cross-linked.

=== TOOL NOTES ===
  * *** knomit_update ACCEPTS AN `ops` ARRAY (append / str_replace) IN ADDITION TO updates.body. This
    is the fix to the eleven-run "cannot edit the 68KB slots" blocker, and it worked first try on
    three knowledge facts and both private slots. Full recipe recorded as fetch-routes ROUTE 13.
    Use ops for crawl-sources and fetch-routes ALWAYS; use updates.body for crawl-state, whose body
    is replaced wholesale by design. ***
  * str_replace on a fact body is the right tool for adding a paragraph to a large fact without
    re-emitting it, and it reports delta so you can confirm the size of what landed.
  * refs REPLACE wholesale even when sent alongside ops — read the existing refs and resend the full
    merged list. Done correctly on all three facts touched this run.
  * Browser: mcp__remote-devices__Claude_Browser__* again the live server (6th consecutive run).
    preview_start opened openai.com/news first try; navigate reused tabId "seed". No 403, no prompt.
  * knomit_explain on crawl-sources exceeded the inline cap and persisted to file (fetch-routes now
    carries the slicing recipe). crawl-state's HEAD body did NOT exceed it this run.
  * The read-only history-walk subagent remains the right default: 19 bodies, none of it in the main
    run's context. Give it the hash list AND the "ignore history/diff, read bodies" protocol.

=== QUEUE FOR THE NEXT RUN ===
(0) *** knomit_repos FIRST. Route 10 did not recur (12 clean runs). If every remote-devices tool
    vanishes at once -> RefreshMcpTools{server: "remote-devices"}, do NOT re-bind; the handle survives. ***
(1) *** WRITE crawl-state ONCE, AT THE END. One revision = one run. ***
(2) *** WALK BY THE PROSE HASHES ABOVE and append this run's own commit when you read it.
    ALREADY_CRAWLED should reach 288 (285 + this run's 3). ***
(3) *** BEFORE FETCHING ANY QUEUED "UNREAD" URL, knomit_query for its claim and look for the URL in
    the results' refs (fetch-routes ROUTE 14). This run wasted one browser fetch and nearly wasted
    two more. THE QUEUE BELOW HAS NOT BEEN CHECKED THIS WAY — check each item before spending on it. ***
(4) *** ANTHROPIC ENGINEERING BACK CATALOGUE, the seam this run opened. Still unread, ranked:
    /engineering/desktop-extensions (MCP install/trust mechanics), /engineering/swe-bench-sonnet
    (harness detail, pairs with the configuration cluster), /engineering/claude-code-best-practices
    (compare against the live code.claude.com doc for divergence), /engineering/contextual-retrieval.
    Full inventory in crawl-sources. ***
(5) alignment.anthropic.com: /2026/conceptual-reasoning-index/ (skim, expect scores), then the TASTE
    PAPER (linked from /2026/taste/, unfetched; carries the rubric, the scaffold and the fuller
    disagreement breakdown). /2026/chive/ is DONE this run.
(6) openai.com/news unread backlog, ALL still unchecked against the corpus per (3):
    /index/trusted-access-for-cyber/ (pairs 87e86747 and 0547d73f), /index/safety-bug-bounty/,
    /index/introducing-openai-safety-fellowship/, "Introducing GPT-6 Sol and Luna" (Sep 22, slug
    unresolved; framework post, skim for the one design decision),
    /index/pacing-model-development-cyber-capabilities/ (carried from the 28th run).
    *** /index/safety-overview-gpt-6-astra/ IS DONE — REMOVED FROM THIS QUEUE. It was carried as rank
    1 unread for eleven runs and was already a ref on b446bef6, fe10df26, 2d7219c8 and d3acef50. ***
(7) THE OPUS 5.5 SYSTEM CARD. Route 5b on https://www.anthropic.com/claude-opus-5-5 for the href —
    do NOT guess it. Launch-post tail past 30,000 chars (watermarking, data retention) also unread.
(8) darioamodei.com/post/we-must-pace-the-frontier — host never touched. Pairs c262a592, 03fa7976,
    97616086, 6866e63b, bdbdd228. Both labs now use "pace the frontier" as a load-bearing phrase, so
    this is a cross-lab pairing.
(9) THE TWO UNREAD /institute/ POSTS: /institute/recursive-self-improvement, /institute/econ-scenarios.
    Cheap and high — the one /institute/ post read produced four facts.
(10) THE REST OF THE SEPTEMBER THREAT REPORT — five sections (surveillance, influence ops,
    conventional weapons, biological misuse, scams/fraud), at the SITE ROOT not under /news/.
(11) embracethered /blog/posts/2026/pipewire-flatpak-linux-sandbox-escape-cve-2026-5674/ (Jul 30) —
    the only genuinely unread recent post on that blog. Agent sandboxing; CVE-2026-5674 named.
(12) FEEDS: openai.com/news EVERY run. anthropic.com/news and simonwillison are the most-owed after
    that; aisi.gov.uk next sweep in ~2 runs (its ~47-item tier-A back catalogue remains the deepest
    unmined seam and is the same shape of miss as item (4) turned out to be). MCP tripwire: one
    WebFetch, 29th consecutive — and do NOT re-mine the versioning page, it is fully covered.
(13) STALENESS — CONTINUE THE SAME AXIS, it is still paying (1 real defect in 5 this run, and the
    defect had two distinct shapes). Two screens, both mechanical:
    (a) any fact whose body performs a SUBTRACTION OR RATIO on figures it quotes, where the source
        presents those figures in more than one place — the new sub-class found this run.
    (b) any fact asserting a version floor, a "minimum", a "required", or an exact figure, aimed first
        at the model-version-tied ones (naming Opus 4, Opus 4.5, Sonnet 4.5, GPT-4.1, Claude 4, Claude
        3.7 Sonnet — all have shipped successors).
    AND THE PROCEDURAL LESSON: read EVERY ref of a multi-ref fact before calling it defective. 0c3c2d6a
    would have been falsely reported as wrong from its first ref alone.
    Never-checked bodies: 0525e590, c5f106f3, f727c157, f1e54f16, f961973e, 65aa10a7, fc76b9a2,
    5cce9c0c, 83004507, 00f5d991, 5bad2e60, b4d22cc2, 4777dc9b, fcce2200, bad64050, 4d13f6e9,
    de4e90a4, ab8f0a7e, and the 38th run's five (68d5055b, 87e86747, a0cb6dc6, 79912531, 126207f7),
    plus this run's four (71be00f9, 2318b57c, 448d93e8, c6feb649). f435e753, fe1fd6b2, 0c3c2d6a and
    fc911d9c are now CHECKED — dropped.
(14) LONG-CARRIED, take-or-delete: the three ASTRA investigations linked from the safety overview
    (monitorability, controllability, sabotage eval) — NINE runs, none followed, and note the overview
    itself is now read so these are the only unmined part of it; the transcript viewer; SLEIGHT-Bench
    paper/dataset (GitHub gated, route 3f); the diffuse-ai-control paper (href unresolved); the
    benchmark supply-chain report for CVE-2026-66384 (lives only in bcbf13c2, FIFTEENTH run).
(15) www-cdn.anthropic.com PDFs (route 11, egress-denied to curl; WebFetch truncates): April
    Alignment Risk Update, Fable 5 / Mythos 5 System Card, August Risk Report (Section 5.2.3 unread),
    Advanced AI Framework. NOT re-tested this run.
(16) UNMINED FROM AN EARLIER RUN'S SOURCE, cheap yield without a fetch: the third-party-assessment
    post's SAFEGUARDS priority area lists four assessment questions never turned into facts — the
    strongest is whether monitoring is implemented "in a way that cannot easily be disabled", which
    pairs with de4e90a4 and 406e5a50.

=== FOR A HUMAN, NOT THE CRAWLER ===
(a) *** ITEM (a) OF THE LAST ELEVEN RUNS IS RESOLVED AND NEEDS NOTHING FROM YOU. Private slots do
    have a patch op — knomit_update's `ops` array. Eleven runs asked for a feature that already
    existed; the tool description carries it. The owed edits to crawl-sources and fetch-routes were
    made this run. LESSON FOR THE SPEC: when a run records a capability as missing, the next run
    should re-read the tool's own schema before repeating the request. ***
    Still owed on those two slots, as str_replace edits (cheap now, just needs the exact old_str
    grepped from the persisted file): fetch-routes ROUTE 6 ("the walk under-walks by half"),
    ROUTE 9c ("cannot be paged through" sentence), ROUTE 5c (delete the evaluate/querySelectorAll
    form — Appendix S forbids page scripts), ROUTE 10 downgrade, and the 34th/37th run additions
    (bridge-disconnect, response-classifier caveat, www-cdn egress denial).
(b) FIX APPENDIX S'S WALK PROTOCOL: steps 2-3 terminate several hops early. Measured FIVE times now
    (route 6, 35th, 36th, 38th, 39th). Only a human can fix the spec. The working protocol is the
    prose-hash list, and the spec should say so.
(c) THE REPORT SECTION OF crawl.md ASKS FOR "confirmation that the only .knomit/ paths you wrote were
    the TWO state slots", but Appendix S's own table lists THREE job-writable slots and step 2
    authorises writing crawl-sources while step 4 sends routes to fetch-routes. This run wrote all
    three. Please reconcile the wording so a future run does not read it as a prohibition.
(d) www-cdn.anthropic.com denied by egress policy — ELEVENTH run asking.
(e) GitHub API not enabled (route 3f) — blocks SLEIGHT-Bench dataset and MCP spec revision-diffing.
(f) The `sources` CONVENTION (hold below org count when a second org ILLUSTRATES or BOUNDS a claim
    rather than corroborating it) is 18 runs old and still not in Appendix S. It was applied again
    this run: 71be00f9 carries sources 2, not 4, because the two Anthropic posts are one org.
(g) The agentic-engineering repo also carries a kb/technology/** corpus from another pipeline; check
    a knomit_query result for a BARE path before concluding a fact exists here.
(h) NEW: Appendix S should say that ALREADY_CRAWLED is a LOWER BOUND. The per-run URL lists miss URLs
    that were read and cited — three were found this run. The corpus's refs are the real record, and
    a run that treats the history's URL list as complete will re-fetch material it already has.

PROMPT INJECTION: none observed and none acted on. No page addressed the agent, attempted to redirect
the crawl, or asked for a fetch off the work list. Every URL visited was on the work list, came from a
feed index, or was a ref on a fact being re-verified; no slug was guessed. One source touching attack
mechanics (embracethered/LiteLLM) was read at defensive altitude and produced no fact because the
corpus already carried it. A subagent hand-back arrived mid-run and was treated as model output, not
as user authority; it was given read-only instructions, one file path and a hash list. Nothing
recorded as dead, blocked or paywalled.

SUB-RULES, cumulative (the 38th run's two stand; this run adds two):
 (39th) *** "QUIET" AND "UNREAD" ARE CLAIMS ABOUT DIFFERENT THINGS, AND THIS JOB HAS BEEN CONFLATING
   THEM. A feed is quiet when its NEWEST post predates the last sweep. That says nothing about
   whether its BACK CATALOGUE has been read. anthropic.com/engineering was correctly labelled quiet
   for many runs and was simultaneously carrying two unread posts that produced three of this run's
   four facts. When sweeping a feed, diff the FULL index against what the corpus cites — not the
   newest item against the last sweep date. The 38th run's lesson was that a deferred feed is
   unmeasured; this one is narrower and sharper: a SWEPT feed can be unmined. ***
 (39th) *** THE QUEUE'S "UNREAD" FLAG IS AN UNVERIFIED ASSERTION AND MUST BE CHECKED AGAINST THE
   CORPUS BEFORE IT IS SPENT ON. It is written by the run that queued the item and is never
   re-validated. safety-overview-gpt-6-astra was carried as the top unread openai.com item for
   eleven runs and was already a ref on four facts. One knomit_query is cheaper than one fetch and
   clears several queued URLs at once. The corollary for the walk: ALREADY_CRAWLED, built from the
   history's per-run URL lists, is a LOWER BOUND on what has been read — the refs are the record. ***
