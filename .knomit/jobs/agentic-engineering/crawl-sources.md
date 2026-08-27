---
type: reference
domain: [agentic-engineering, job-state]
confidence: 1
sources: 0
entities: [agentic-engineering]
refs: ['https://github.com/knomit/knomit']
---
# Recurring crawl sources

*** THIS SLOT IS THE SOURCE LIST AND NOTHING ELSE. ***
What belongs here: URLs to crawl, and URL catalogues that were expensive to discover.
What does NOT belong here, and where it went (split 2026-08-11):
  how to fetch a gated/blocked host  -> .knomit/jobs/agentic-engineering/fetch-routes.md
  standing rules for the job         -> spec.md on disk (Appendix S). Not writable from here, by design.
  per-run status, queues, rankings   -> crawl-state.md, whose revision history is the record.
READ/UNREAD markers below are provenance hints only. The AUTHORITATIVE record of what has been
crawled is the ALREADY_CRAWLED union assembled by walking crawl-state's revisions — BUT SEE
fetch-routes ROUTE 7: that history is being squashed, so this file's markers are now the more
complete record for the runs whose bodies have been lost. Keep them accurate.

*** HOW TO BUILD A CATALOGUE (21st run), WITH THE 23rd RUN'S CORRECTION. ***
Enumerating a feed's archive is ONE plain WebFetch (fetch-routes route 5), not a pagination crawl.
*** BUT THE DEPTH RETURNED VARIES BETWEEN CALLS ON THE SAME URL. *** The 23rd run got the COMPLETE
embracethered archive (~180 posts back to 2018) where the 21st got 10; and got only 10 AISI posts
plus an ellipsis where the 21st got 95. So a catalogue below may be INCOMPLETE without being wrong,
and a deeper listing EXTENDS it rather than contradicting it. If you need the back catalogue and the
call returns an ellipsis, ask again naming the period you want.
*** 22nd-RUN COROLLARY (fetch-routes 5b): an ASSET linked from a page — a paper, PDF, report — is
resolved by asking the PAGE for its href, not by searching for the asset. ***
*** 23rd-RUN COROLLARY (fetch-routes 5c): on a browser-only host, harvest hrefs with a
querySelectorAll evaluate on EVERY page you visit. That is how the Aug 26 OpenAI post-mortem — the
highest-value document of the 23rd run — was found, one day after publication, in no catalogue. ***

=== RECURRING FEEDS — swept every run when days have passed ===

https://www.anthropic.com/engineering
https://www.anthropic.com/news/                                          <- ADDED 14th run (postmortems live here, NOT /engineering)
https://developers.openai.com/cookbook
https://simonwillison.net/tags/llms/
https://www.langchain.com/blog/
https://www.latent.space/archive
https://eugeneyan.com/writing/
https://www.microsoft.com/en-us/research/blog/
https://www.microsoft.com/en-us/security/blog/
https://aws.amazon.com/blogs/machine-learning/
https://research.google/blog/
https://embracethered.com/blog/
https://metr.org/blog/
https://sourcegraph.com/blog
https://cognition.com/blog
https://www.trychroma.com/research
https://builder.aws.com/learn/topics/builders-library
https://code.claude.com/docs/en/best-practices
https://genai.owasp.org/
https://modelcontextprotocol.io/specification/versioning
https://modelcontextprotocol.io/specification/2026-07-28/deprecated      <- ADDED 12th run (cheap tripwire)
https://owasp-agentic-ai-security-incidents.lovable.app/                 <- ADDED 12th run (ASI incidents tracker)
https://www.aisi.gov.uk/blog/                                            <- ADDED 13th run. *** RANK 1. See the catalogue. ***
https://openai.com/index/                                                <- ADDED 13th run (RANK 2)
https://developers.openai.com/api/docs/guides/                           <- ADDED 15th run. The API guides tree is
    a DIFFERENT source from openai.com/index and from the cookbook, it is plain-WebFetch-readable (no browser,
    no 403), and agent-builder-safety was found there unread. Scan it for new guides.
https://api.github.com/repos/modelcontextprotocol/modelcontextprotocol/contents/docs/specification
    <- ADDED 16th run. THE MCP TRIPWIRE, ZERO-FETCH FORM, AND IT WORKS WHEN THE WEBSITE DOES NOT.
    Route details in fetch-routes route 3.
https://blog.redwoodresearch.org/                                        <- ADDED 17th run, LOW VOLUME, WATCH ONLY.
    *** THE WATCHED ARTIFACT HAS LANDED: METR and Redwood published their joint independent
    assessment on 2026-08-26, linked from OpenAI's post-mortem as "Read METR report". NOT YET
    FETCHED — top of the 24th run's queue. Get the exact href by re-reading the OpenAI post with a
    querySelectorAll evaluate (fetch-routes 5c); it is an off-site link. ***
https://github.com/vectara/hallucination-leaderboard
https://huggingface.co/blog
https://arxiv.org/                                                       <- ADDED 22nd run, NOT a sweepable feed but
    a standing note: arXiv resolves by title via WebSearch in one call, and the result set carries the
    /html/<id>v1 FULL-TEXT url, which is what you want — /abs/ gives only the abstract.

=== SOURCE INVENTORIES — catalogues that cost real fetches to enumerate ===

*** UK AISI BLOG — ARCHIVE ENUMERATED 21st run (95 posts, one WebFetch). RANK 1. ***
Plain WebFetch reads both the index and the articles — no browser, no gate, no 403.
SLUG WARNING, still live: several slugs differ from their titles. Verified mismatches include
  "Advancing AI voice security with ElevenLabs" -> /blog/advancing-voice-ai-security-with-elevenlabs
  "Ask Don't Tell: Reducing Sycophancy..."      -> /blog/ask-dont-tell-...-large-language-models-2  (CMS "-2" suffix)
  "A structured protocol for elicitation experiments" -> /blog/our-approach-to-ai-capability-elicitation
  "International consensus and open questions in AI evaluations" -> /blog/international-ai-network-consensus-and-open-questions
Do not derive a slug from a title on this host.

  *** NEWEST POST, READ 23rd run (published the same day): ***
    /blog/optimal-stopping-spending-evaluation-compute-where-it-counts   (Aug 27 2026) -> bacf0f4e
      `optstop`: sequential sampling with two stopping rules, hierarchical Bayesian pooling across
      tasks, a <1% rare-event safeguard, 57-97% of planned trials saved. WELL MINED. One open
      question recorded in the fact: the post does not say whether those savings are from live runs
      or simulation, and answered NOT STATED in both directions when asked.
  READ (23rd run), both promoted by the 22nd and both paid:
    /blog/auditing-games-for-sandbagging-detection                        (Dec 9 2025)  -> e40cca2a
      DONE. Note its internal count defect: says "ten methods", names nine.
    /blog/can-ai-agents-escape-their-sandboxes-a-benchmark-for-safely-measuring-container-breakout-capabilities
                                                                          (Mar 23 2026) -> 84a43a60
      DONE. SandboxEscapeBench. NO model names and NO success percentages in the text — do not
      return expecting numbers. The scaling claims live in graphs.
  READ (21st run) — all four paid:
    /blog/how-are-ai-agents-used-evidence-from-177000-ai-agent-tools     (Mar 26 2026) -> 45d86a7d
    /blog/what-can-sandboxed-ai-agents-learn-about-their-evaluation-environments  (Apr 20 2026) -> d0c5b9f8
      ^ ITS PAPER IS READ (22nd run). DONE — do not re-open.
    /blog/how-do-environmental-factors-impact-ai-behaviour                (Apr 24 2026) -> f4e0cbaf
    /blog/stress-testing-asynchronous-monitoring-of-ai-coding-agents      (Dec 16 2025) -> 42e1218f + upd a5eaec6b
  READ EARLIER: /blog/incident-report-unsanctioned-agent-behaviour-during-cyber-testing (Aug 4 2026, 13th run)
    /blog/cheating-behaviour-in-frontier-model-evaluations              (Jul 21 2026, 20th) -> 8756141e
    /blog/how-our-new-control-red-team-is-stress-testing-frontier-monitors (Jul 23 2026, 20th) -> a5eaec6b
    /blog/more-compute-more-capability-why-ai-agent-evals-need-to-account-for-test-time-compute (Jul 2 2026, 20th) -> 80866fc3
    /blog/evidence-for-inference-scaling-in-ai-cyber-tasks-... (Mar 5 2026, 21st) -> folded into 80866fc3. DONE.

  UNREAD, RANKED FOR THIS PACK. Rank on AGENT-ENGINEERING content, not on how interesting the title is:
    TIER A — measurement or design content this pack has somewhere to put:
      /blog/transcript-analysis-for-ai-agent-evaluations                            (Oct 10 2025)
      /blog/a-pipeline-for-transcript-analysis-using-inspect-scout                  (Feb 25 2026)
        ^ *** NOW TOP OF TIER A. *** These two are a PAIR, 4 months apart, same problem. Read
          together; pairs with f877f05d, and now with fe10df26 and 193d5de2, which between them say
          trajectory-level monitoring is the best-evidenced answer to the eval detection gap. This
          pack holds the CONCLUSION and not the METHOD.
      /blog/how-to-evaluate-control-measures-for-ai-agents                          (Apr 11 2025)
      /blog/llm-judges-on-trial-a-new-statistical-framework-to-assess-autograders   (Jul 9 2025)
        ^ pairs with 38c06627 and the hamel.dev judge material. Also now with bacf0f4e, which is the
          same team applying statistics to eval design — likely the same methodological voice.
      /blog/international-evaluation-best-practice-and-open-questions-in-ai-measurement (Jul 23 2026)
      /blog/realitytest-do-ai-systems-disclose-their-identity-when-asked            (Jun 8 2026)
      /blog/will-it-become-harder-to-oversee-ai-systems                             (May 21 2026)
      /blog/investigating-models-for-misalignment                                   (Nov 26 2025)
        ^ PROMOTED 23rd run: OpenAI's post-mortem is a misalignment investigation with four named
          patterns; an AISI framing of the same problem is a natural counter-position pairing.
      /blog/introducing-controlarena-a-library-for-running-ai-control-experiments   (Oct 22 2025)
      /blog/the-inspect-sandboxing-toolkit-scalable-and-secure-ai-agent-evaluations (Aug 7 2025)
        ^ PROMOTED 23rd run: 84a43a60 and d3acef50 now both turn on eval sandbox construction.
      /blog/examining-backdoor-data-poisoning-at-scale                              (Oct 9 2025)
      /blog/hibayes-improving-llm-evaluation-with-hierarchical-bayesian-modelling   (May 12 2025)
        ^ PROMOTED 23rd run: bacf0f4e's optstop uses "a hierarchical Bayesian model" and this is
          evidently its predecessor. Cheap, directly connected, and likely carries the statistics the
          blog post only gestures at.
      /blog/releasing-aisis-engineering-playbook                                    (Jun 18 2026)
      /blog/finding-cloud-misconfigurations-with-frontier-ai-a-case-study           (Jul 7 2026)
        ^ PROMOTED 23rd run: 84a43a60 says misconfiguration is the live agent-escape surface; this is
          the same institute on agents FINDING misconfigurations. Defender/attacker pair.
      /blog/how-do-frontier-ai-agents-perform-in-multi-step-cyber-attack-scenarios  (Mar 16 2026)
      /blog/boundary-point-jailbreaking-a-new-way-to-break-the-strongest-ai-defences (Feb 17 2026)
      /blog/replibench-measuring-autonomous-replication-capabilities-in-ai-systems  (Apr 22 2025)
      /blog/why-were-working-on-white-box-control                                   (Jul 10 2025)
      /blog/from-bugs-to-bypasses-adapting-vulnerability-disclosure-for-ai-safeguards (Sep 2 2025)
      /blog/making-safeguard-evaluations-actionable                                 (May 29 2025)
      /blog/principles-for-safeguard-evaluation                                     (Feb 4 2025)
      /blog/long-form-tasks                                                         (Dec 3 2024)
      /blog/early-lessons-from-evaluating-frontier-ai-systems                       (Oct 24 2024)
      /blog/early-insights-from-developing-question-answer-evaluations-for-frontier-ai (Sep 23 2024)
      /blog/inspect-cyber                                                           (Jun 26 2025)
      /blog/international-joint-testing-exercise-agentic-testing                    (Jul 17 2025)
      /blog/how-fast-is-autonomous-ai-cyber-capability-advancing                    (May 13 2026)
      /blog/harnessing-frontier-ai-for-cyber-defence                                (Mar 31 2026)
      /blog/an-evaluation-framework-for-ai-misuse-in-fraud-and-cybercrime           (Feb 26 2026)
      /blog/evaluating-whether-ai-models-would-sabotage-ai-safety-research          (Apr 27 2026)
      /blog/how-far-behind-the-frontier-are-leading-open-weight-models-on-cyber     (Jul 17 2026)
      /blog/ai-and-the-future-of-work-measuring-ai-driven-productivity-gains-for-workplace-tasks (Feb 2 2026)
      /blog/how-do-ai-models-persuade-...-large-scale-experiments                   (Dec 4 2025)
      /blog/mapping-the-limitations-of-current-ai-systems                           (Oct 23 2025)
      /blog/do-chatbots-inform-or-misinform-voters                                  (Sep 30 2025)
      /blog/how-were-working-with-frontier-ai-developers-to-improve-model-security  (Sep 13 2025)
      /blog/managing-risks-from-increasingly-capable-open-weight-ai-systems         (Aug 29 2025)
      /blog/how-can-safety-cases-be-used-to-help-with-frontier-ai-safety            (Feb 10 2025)
      /blog/safety-case-template-for-inability-arguments                            (Nov 14 2024)
      /blog/safety-cases-at-aisi                                                    (Aug 23 2024)
      /blog/how-will-ai-enable-the-crimes-of-the-future                             (Jul 3 2025)
      /blog/strengthening-ai-resilience                                             (Apr 3 2025)
      /blog/aisis-research-direction-for-technical-solutions                        (Mar 11 2025)
      /blog/research-agenda                                                         (May 6 2025)
      /blog/our-approach-to-evaluations                                             (Feb 9 2024)
      /blog/inspect-evals                                                           (Nov 13 2024)
      /blog/open-sourcing-our-testing-framework-inspect                             (Apr 21 2024)
      /blog/interviewing-researchers-on-automation                                  (Aug 27 2024, Epoch cross-post)
      /blog/our-approach-to-ai-capability-elicitation                               (Jul 16 2025)
      /blog/evals-bounty                                                            (Nov 5 2024)
      /blog/ask-dont-tell-reducing-sycophancy-in-large-language-models-2            (Apr 28 2026)
    *** BELOW THE BAR — DO NOT SPEND A FETCH. Per-model capability scorecards, partnership and
    funding announcements, progress reports, summits, diplomatic statements, and CSAM policy: ***
      preliminary-assessment-of-kimi-k3s-cyber-capabilities, uk-germany-joint-statement-...,
      our-evaluation-of-openais-gpt-5-5-cyber-capabilities, our-evaluation-of-claude-mythos-previews-...,
      pre-deployment-evaluation-of-openais-o1-model, pre-deployment-evaluation-of-anthropics-upgraded-claude-3-5-sonnet,
      deepening-our-partnership-with-the-australian-ai-safety-institute, partnering-with-microsoft-...,
      deepening-our-partnership-with-google-deepmind, advancing-voice-ai-security-with-elevenlabs,
      announcing-the-uk-and-us-aisi-partnership, announcing-the-uk-and-france-...,
      funding-60-projects-..., announcing-the-alignment-project, new-updates-to-the-aisi-challenge-fund,
      advancing-the-field-of-systemic-ai-safety-grants-open, our-2025-year-in-review, our-first-year,
      first/second/third/fourth-progress-report, advanced-ai-evaluations-may-update, ukaisi-at-neurips-2025,
      why-i-joined-aisi---geoffrey-irving, conference-on-frontier-ai-safety-frameworks,
      ai-safety-summit-2023, international-scientific-report-...-interim-report,
      5-key-findings-from-our-first-frontier-ai-trends-report, our-approach-to-tackling-ai-generated-csam,
      should-ai-systems-behave-like-people, navigating-the-uncharted-..., international-ai-network-consensus-...

*** EMBRACETHERED — *** ARCHIVE MUCH LARGER THAN RECORDED. 23rd run: ONE WebFetch returned the
*** COMPLETE archive, ~180 posts back to 2018-12-16. The 21st run's "10 posts back to Mar 2026" was
*** a property of that call, not of the site. ***
Low volume in 2026, high hit rate; slugs are under /blog/posts/<year>/<slug>/.
  READ (23rd run):
    /2026/breaking-claude-code-opus-5-and-automode/   (Aug 26 2026) -> 367b7933 + upd 89df351e
      Module shadowing via a self-authored decoder; Anthropic closed it "Informative" and stated Auto
      Mode is "a convenience feature backed by a best-effort classifier, not a security guarantee".
      WELL MINED. CAUTION RECORDED: an open-ended read of this post gave "60-80%" for the source's
      "up to 80% ... using a small sample size", and listed `python3 -I` as a recommended mitigation
      when it is what the ATTACKER's payload uses. Do not reintroduce either from a summary.
  READ (21st run):
    /2026/recovering-encrypted-llm-thoughts/          (Aug 16 2026) -> 1d01a338. Paper read 22nd. CLOSED.
    /2026/hijacking-litellm-for-fun-and-profit/       (Aug 3 2026)  -> b17b7fc2
  READ EARLIER: /2026/toctou-agent-what-you-click-is-not-what-you-get/ (Jun 25 2026) -> 70127cdd
    /2026/macos-terminal-dillma-dns-exfil-ansi-escape-code-fix/ (Jul 16 2026)
    /2026/ai-intrusion-are-now-real/ (Jul 19 2026, cited by bcbf13c2)
  UNREAD 2026, ranked:
    /2026/agent-commander-your-agent-works-for-me-now/            (Mar 16 2026) <- TOP. Promptware C2;
      pairs with 7a4f9061, 4e923405, a7863d24, and now 6cc23314 (peer messages as authorisation).
    /2026/scary-agent-skills/                                    (Feb 11 2026) <- NEWLY VISIBLE 23rd run.
      "Hidden Unicode Instructions in Skills ...And How To Catch Them" — pairs with e9b7eef3 (skills)
      and 7bd6c6c9. Has a DETECTION half, which is rarer than the attack half. HIGH.
    /2026/data-exfiltration-mitigation-paper-by-openai/           (Feb 04 2026) <- NEWLY VISIBLE.
      "OpenAI Explains URL-Based Data Exfiltration Mitigations in New Paper" — route 5b applies: it
      names a paper. Pairs with b4d688b1/eae23eac (ai-agent-link-safety).
    /2026/given-enough-agents-all-bugs-become-shallow/            (Apr 7 2026)  <- pairs with 30543305.
    /2026/breaking-opus-4.7-with-chatgpt/                         (Apr 17 2026) <- memory attack; pairs 7bd6c6c9.
    /2026/minting-next-auth-nextjs-auth-cookies-react2shell-threat/ (Jan 14 2026) <- NEWLY VISIBLE. Web
      auth rather than agent security; probably below the bar.
    /2026/pipewire-flatpak-linux-sandbox-escape-cve-2026-5674/    (Jul 30 2026) <- a Linux CVE rather
      than an agent finding. BUT NOTE: 84a43a60 now makes sandbox-escape CVEs relevant. Re-rate up slightly.
    /2026/defcon-talk-copirate-365/                               (May 4 2026)  <- talk write-up, weakest form.
  *** UNREAD 2025 — NEWLY ENUMERATED 23rd run, and this is a substantial unmined seam. The 2025
  *** archive is ~47 posts, most of them the "Month of AI Bugs" series (Aug 2025), which is one
  *** vendor-specific prompt-injection finding per day. DO NOT read them all — the series is
  *** repetitive by design and the pack already holds the pattern. Read the SYNTHESES and the
  *** structurally novel ones: ***
    /2025/the-normalization-of-deviance-in-ai/                    (Dec 04 2025) <- TOP OF 2025. A
      named safety-engineering concept applied to AI practice; this pack has no fact on it and it is
      the kind of altitude the pack wants. Pairs with the approval-fatigue material (2b9a10f8).
    /2025/cross-agent-privilege-escalation-agents-that-free-each-other/ (Sep 24 2025) <- VERY HIGH.
      "When Agents Free Each Other" — this is 6cc23314's subject from the attacker side, and
      predates the OpenAI incident by ten months.
    /2025/wrapping-up-month-of-ai-bugs/                           (Aug 30 2025) <- the SYNTHESIS of
      the series. Read this INSTEAD of the ~25 individual posts.
    /2025/agenthopper-a-poc-ai-virus/                             (Aug 29 2025) <- self-propagation.
    /2025/39c3-agentic-probllms-exploiting-computer-use-and-coding-agents/ (Dec 30 2025) <- talk form.
    /2025/security-keeps-google-antigravity-grounded/             (Nov 25 2025) <- a harness this
      pack has no coverage of.
    /2025/chatgpt-deep-research-connectors-data-spill-and-leaks/  (Aug 24 2025)
    /2025/model-context-protocol-security-risks-and-exploits/     (May 02 2025) <- early MCP security;
      check against the pack's much later MCP spec facts before spending the fetch.
  BELOW THE BAR / SKIP: the per-vendor Month-of-AI-Bugs entries (Windsurf x4, Amazon Q x3, Jules x3,
    Devin x3, Amp x3, Cursor, Kiro, Manus, Cline, OpenHands x2, Copilot, Claude Code, Codex) unless
    you need a specific vendor citation — take the wrap-up instead. All 2024-and-earlier posts, and
    everything 2018-2022 (pre-LLM red-team tooling), are out of scope for this pack.

*** MICROSOFT SECURITY BLOG — FRONT PAGE READ AS A LIST, 21st run. VERDICT: RANK CONFIRMED LOW. ***
Of 12 posts on the front page, ELEVEN are threat intel or analyst-report marketing. Exactly ONE is on-topic:
  /2026/08/04/advance-zero-trust-for-ai-new-tools-and-guidance-to-secure-ai-agents-and-devsecops/  <- UNREAD.
This feed paginates and the call returned the front page only. One sweep every several runs is enough.

*** MICROSOFT RESEARCH BLOG — known-good article URL, for reference ***
  /echoverse-deep-evolving-environments-for-computer-use-agents/  (Jul 30 2026) -> 12966de6.
    Plain WebFetch, no gate. RE-VERIFIED 22nd run and CORRECTED: the post DOES quantify live-web
    transfer (WebVoyager 66.5->71.5, Online-Mind2Web 40.5->43.4). Do not re-mine.

*** OWASP GenAI — RESOURCE SLUG + DOWNLOAD ID MAP ***
The PDF lives at https://genai.owasp.org/download/<id>/?tmstv=<epoch>, and the id is NOT guessable.
Get it by WebFetching the /resource/<slug>/ page and asking for the download URL, then curl it with -A.
The tmstv token does not expire — 1754459367 was recorded 2026-08-05 and still worked 2026-08-20.
Ids captured so far:
  50592  State of Agentic AI Security and Governance 2.01   (139pp, read 12th run) tmstv=1754459367
         ^ pdfinfo BOTH the 18th and 21st runs: 139 pages, CreationDate 2026-06-01. PROVEN unchanged.
         ^ Useful extract line numbers:
             1060-1075  the two allowlist CVEs + the "It streamlines it" quote (WRAPPED)
             1145-1160  postmark-mcp, CVE-2025-6514, Tool Poisoning, MCP Rug Pulls
             1160-1170  ClawHavoc, Koi Security, Snyk ToxicSkills, SOUL.md/MEMORY.md
             1184-1196  AI Agent Traps: approval-fatigue-as-attack, multi-agent traps
             1298-1305  memory poisoning + "Monitoring scoped to individual sessions will never detect it"
             3468-3475  *** THE NUMBERS. ClawHavoc "~12% of 2,857 ClawHub skills found malicious". ***
             5530-5545  framework comparison; names the MCP Security White Paper's 12-category taxonomy
  56857  OWASP GenAI LLM Top 10 2026                        (122pp, read 13th run) tmstv=1785822482
  49059  Securing Agentic Applications Guide 1.0            (July 2025, read 15th run) tmstv=1753666640
  46950  Multi-Agentic System Threat Modeling Guide v1.0    (April 2025, read 15th run) tmstv=1745459605
  47278  Agent Name Service (ANS) v1.0                      (14 May 2025, read 16th run) tmstv=1747275418
         Resource slug CONTAINS A TYPO and is unguessable — note "al" for "AI":
         /resource/agent-name-service-ans-for-secure-al-agent-discovery-v1-0/
  52117  OWASP Top 10 for Agentic Applications 2026         READ 17th + 18th run. 3137 lines, 1.2MB.
         https://genai.owasp.org/download/52117/?tmstv=1765059207   (labelled "Version 2026", Dec 2025)
         Resource slug: /resource/owasp-top-10-for-agentic-applications-for-2026/
         Entry line ranges: ASI01 476-578, ASI02 579 onward; Appendix D 2138-2750; Acknowledgements
         ~2851 (EXCLUDE from any count — it carries an ASI01-ASI10 roster that adds a phantom tag).
         *** STILL UNMINED: *** per-entry "Prevention and Mitigation Guidelines" for ASI03..ASI07 and
         ASI09; Appendix B (CycloneDX/AIBOM); Appendix C (NHI Top 10 2025 mapping, extract line 1882+,
         table at 1886 — 069468bb gives it somewhere to land); Appendix D per-incident detail.
  54627  AIUC-1 Crosswalks   https://genai.owasp.org/download/54627/?tmstv=1779726713
         pdfinfo: 55 pages, CreationDate 2026-05-25. Read 11th; all three facts re-verified 18th.
         UNMINED: Part A / Part B per-requirement tables in full (they extract row-faithfully).
  54018  AI Security Solutions Landscape Red Teaming Q2 2026  https://genai.owasp.org/download/54018/?tmstv=1775767894
         pdfinfo: 15 pages, CreationDate 2026-04-09. Vendor market map — LOW yield, do not re-mine.
  *** STANDING LEAD, ID STILL NOT RESOLVED (not attempted 22nd or 23rd run): the OWASP MCP SECURITY
  WHITE PAPER. *** 50592 calls it "the most granular threat taxonomy for tool invocation protocols,
  identifying 12 distinct categories including tool poisoning, rug pulls, and cross-origin escalation".
  This pack holds three of those twelve (via 78ab92f2). Strongest untouched OWASP target. Resolve the
  id by the two-step in fetch-routes 2b.

*** OPENAI /index/ POST CATALOGUE — enumerated by WebSearch 17th run; corrected 18th-23rd ***
openai.com/index 403s to WebFetch; all of these need the browser (fetch-routes route 1). Slugs are
EXACT — do not re-derive them. The "Keep reading" footer is a plain RECENCY feed, NOT category-scoped.
*** 23rd-RUN NOTE: mcp__claude-in-chrome__ WAS NOT CONNECTED; mcp__browser__ worked. Use whichever is
live, and read article text with a browser_evaluate innerText call — see fetch-routes route 1. ***
  *** READ 23rd run — THE TWO NEWEST SECURITY POSTS, AND ONE WAS PUBLISHED THE DAY BEFORE: ***
  READ: /index/hugging-face-incident-and-the-road-ahead/          (Aug 26 2026) *** THE BIG ONE. ***
        OpenAI's full narrative post-mortem of the July 2026 incident. Found via a 5c href harvest on
        the Defender's Window footer — it was in no catalogue. Yielded FOUR new facts (a0d01236,
        931d9507, 6cc23314, fe10df26) and updates to FIVE existing ones (4e923405, d3acef50,
        2dfac716, 193d5de2, 127fd5f9). Contains: the full dated incident timeline, agent chain-of-
        thought excerpts, the four named misalignment patterns, the 198-of-898 unsolved-task finding,
        the failed grader metagame, the >100x safeguard-gap measurement, the CoT-monitoring
        counterfactual, and the remediation programme. WELL MINED but LARGE — the sections on
        "Accelerating alignment" and "Security and monitoring" have more in them than was taken.
        *** IT LINKS THREE ARTIFACTS, NONE FETCHED. ALL THREE ARE TOP OF THE 24th RUN'S QUEUE: ***
          "Read the technical report"  — OpenAI's FULL technical incident report. The pack has
            watched for this for ten runs. It is the primary of the primary.
          "Read METR report"           — the joint METR + Redwood independent assessment, also
            watched for ten runs, published the same day. An INDEPENDENT organisation on the same
            incident, which makes it a genuine second source rather than corroboration.
          "Watch Black Hat talk"       — the talk bcbf13c2 has rested on second-hand for weeks.
        Get all three hrefs with one 5c querySelectorAll evaluate on this page.
  READ: /index/the-defenders-window/                              (Aug 17 2026, by Greg Brockman.)
        Date confirmed correct against the 22nd run's footer inference. NO FACT WRITTEN — assessed
        and largely below the bar: it is a defender-mobilisation call to action, and most of its
        ten-point checklist is generic security advice plus OpenAI product placement. THREE things in
        it are above the bar if a future run wants them, and they were left because the incident
        post-mortem was the better use of the budget:
          (a) the staged detection-triage ladder — read-only scan on one repo -> advisory PR scanning
              -> live alert triage -> automatic closure of narrowly-defined false positives. A
              concrete autonomy-rollout sequence, and this pack likes those.
          (b) "It is an anti-goal to simply produce more security findings that need human
              validation" — a stated anti-goal for security agents, which pairs with 1d1440fe.
          (c) "almost all of our initial security alerts are triaged by intelligence before humans
              are looped in" — a deployment datapoint.
        Also contains a first-person anecdote (13 issues found on a static site in ~15 minutes, fixed
        over an hour) — vivid but n=1 on a personal website; below this pack's bar.
  READ EARLIER: /index/hugging-face-model-evaluation-security-incident/   (cited by bcbf13c2, 2dfac716)
  READ: /index/the-next-evolution-of-the-agents-sdk/              (Apr 15 2026; -> c436422a. Do not re-mine.)
  READ: /index/introducing-aardvark/                              (Oct 30 2025.) DONE.
  READ: /index/codex-security-now-in-research-preview/            (Mar 6 2026.) DONE.
  READ: /index/designing-agents-to-resist-prompt-injection/       (Mar 11 2026; re-verified 19th.)
  READ: /index/prompt-injections/                                 (Nov 7 2025. RE-VERIFIED 19th AND 22nd.)
        ^ NOTE FOR ANY FUTURE CITATION: its "we have not yet seen significant adoption of this
          technique by attackers" is a NOVEMBER 2025 statement. Well mined; low remaining yield.
  READ: /index/unlocking-self-improvement-gpt-red/                (Jul 15 2026.) -> 5f4497f2 + 9b0c8c78.
        DO NOT RE-MINE. It links a paper ("Read the paper") that was NOT followed — remaining value.
  READ: /index/expanding-daybreak-as-the-cyber-defense-window-narrows/  (Aug 10 2026.)
        ^ Well mined 22nd run. Remaining unmined: CVE-2026-15903 / V8 detail, Preparedness classifications.
  UNREAD, ranked:
    /index/putting-frontier-cyber-models-in-more-trusted-hands/   (Aug 10 2026)  <- TOP of the unread.
        Carried from the 22nd run; NOT read on the 23rd, which spent its browser budget on the two
        newer posts. Still the best remaining openai.com target.
    /index/patch-the-planet/              (Daybreak initiative for OSS maintainers; program/policy)
    /index/safety-alignment-long-horizon-models/
        ^ RE-RATE UP after the post-mortem: "Alignment over long tasks" is one of the three named
          remediation workstreams, so this post is probably the programme behind it.
    /index/introducing-openai-presence/   (product)
    /index/trusted-access-for-cyber/, /index/scaling-trusted-access-for-cyber-defense/,
    /index/updating-our-preparedness-framework/   (governance; lower altitude)
    SEEN IN LINKS 23rd run, not previously catalogued: /index/ten-advances-in-mathematics/ (Aug 1,
      below the bar), /index/gpt-5-6/, /index/introducing-gpt-5-5/, /index/introducing-gpt-5-4/
      (model cards — below the bar for this pack, but note gpt-5-6 is the capability reference point
      the incident post-mortem uses for its CoT-monitoring threshold).
  SPOTTED 20th RUN, UNREAD, PROBABLY BELOW THE BAR BUT CHEAP: "How enabling two settings tripled our
    scores on the ARC-AGI-3 benchmark" (Research, Jul 29 2026) — a harness-configuration result, a
    shape this pack HAS repeatedly found valuable. Slug unknown; resolve by search.
  SPOTTED 22nd RUN in footers, listed so nobody spends a fetch: "Offering Zero Data Retention for
    frontier models" (Company, Aug 19 2026) — thematically adjacent to 1d01a338/33aed84c.
    "Introducing ChatGPT for Teens" (Product, Aug 18 2026) — skip.
  ALREADY CITED BY LIVE FACTS — treat as READ, do not re-fetch:
    /index/responding-next-frontier-critical-cyber-capabilities/  (bcbf13c2, ee458c93)
    /index/ai-agent-link-safety/          (b4d688b1, eae23eac)
    /index/third-party-cyber-evaluations-involving-openai-models/  (13th run)
  BELOW THE BAR: "Previewing Ultrafast mode" (Aug 13), "Testing ads in ChatGPT" (Aug 11), "Daybreak
  models are now available on AWS" (Aug 11).

*** ANTHROPIC /news/ — SLUGS ARE EDITORIALLY SHORTENED, DO NOT DERIVE THEM FROM TITLES (20th run) ***
  READ: /news/investigating-incidents-cybersecurity-evals   (Jul 30 2026, 13th run)
  READ: /news/claude-text-watermark                          (Aug 14 2026.) -> 943a7e3c.
        The title-derived slug /news/how-claudes-text-watermark-works 404s. No numbers in the post.
        WATCH FOR: the detection API docs, which is where the thresholds land. NOT LANDED as of 08-27.
  *** 23rd-RUN SWEEP — THREE NEW POSTS SINCE Aug 14, ALL UNREAD: ***
    /news/model-hardware-standard-research-preview   "Previewing the Model Hardware Standard" (Aug 27)
        <- THE ONLY ONE PLAUSIBLY ABOVE THE BAR. Unknown content; a "standard" from Anthropic on
        model/hardware binding could be attestation-adjacent and would pair with 33aed84c. ONE cheap
        fetch to find out. Queued for the 24th run.
    /news/expanding-support-for-scientists            (Aug 27) <- grants/programme. Below the bar.
    /news/wellbeing-research-grants                   (Aug 25) <- grants. Below the bar.
  BELOW THE BAR: "Improving Fable 5's biology safeguards" (Aug 7), the Cuéllar appointment (Aug 4),
    the Cognizant partnership (Jul 27), "Introducing Claude Opus 5" (Jul 24), "Our position on
    open-weights models" (Jul 27, policy).

*** PAPERS — NAMED BY SOURCES THIS PACK HAS READ ***
  *** READ 22nd run: "Stealing Reasoning Traces from Proprietary LLM APIs" ***
    https://arxiv.org/abs/2608.09867   full text: https://arxiv.org/html/2608.09867v1
    -> 33aed84c, a7863d24, and the 1d01a338 update. WELL MINED.
    CAUTION RECORDED: an open-ended WebFetch described a PowerPoint-exfiltration worked example in
    detail; the verbatim call returned NOT STATED for it. Do not reintroduce it from any summary.
  *** READ 22nd run: "What OpenClaw can learn from its environment" (the paper d0c5b9f8 named) ***
    https://cdn.prod.website-files.com/663bd486c5e4c81588db7a1d/69e63511d394ee65d788d9e7_What_OpenClaw_learned_about_us%20(2).pdf
    6 pages, pdfinfo CreationDate 2026-04-20, plain `curl -A` (no gate). -> 0e577a90 + d0c5b9f8 update.
    THE HREF IS A WEBFLOW CDN HASH PATH — unguessable AND unsearchable. DONE, fully mined.
  *** STILL UNFETCHED, AND THE TOP THREE ARE NEW AND HIGH-VALUE: ***
    OpenAI's FULL TECHNICAL INCIDENT REPORT on the Hugging Face incident (linked from the Aug 26
      post as "Read the technical report"). *** RANK 1 FOR THE 24th RUN. ***
    The METR + Redwood JOINT INDEPENDENT ASSESSMENT (linked as "Read METR report", published
      2026-08-26). *** RANK 2, and it is an INDEPENDENT organisation on an incident where this pack
      currently holds only the operator's account. ***
    The Black Hat talk on the incident (linked as "Watch Black Hat talk") — bcbf13c2 has rested on a
      second-hand summary of this talk for weeks. Video, so possibly unusable; try anyway.
    The GPT-Red paper linked from /index/unlocking-self-improvement-gpt-red/ (20th run).
    arXiv 2410.15686 (NetSafe), arXiv 2505.03096 (chaos engineering for LLM MAS) — both report
      MEASUREMENTS, which is what 2508.09815 lacks. Pairs with 24e4552d.

*** COGNITION — COMPLETE ARCHIVE ENUMERATED, 21st run. 82 POSTS, ONE WebFetch, back to Mar 2024. ***
*** UNTOUCHED FOR THREE RUNS NOW (21st, 22nd, 23rd). Either take it or demote it explicitly. ***
Slugs guessed from titles 404 — pull them from this list or re-run the index call. Confirmed exact:
'Coding Agents 101' = /blog/coding-agents-101-the-art-of-actually-getting-things-done.
About half the feed is partnership / funding / office / acquisition / product-launch copy — skip on sight.
  UNREAD AND WORTH IT, ranked:
    /blog/devin-sonnet-4-5-lessons-and-challenges   (Sep 29 2025) <- TOP. A harness rebuilt for a new
      model, with the lessons. Model-migration content is rare and this pack has d6c50e81 to pair it with.
    /blog/coding-agents-101-the-art-of-actually-getting-things-done  (Jun 27 2025)
    /blog/swe-grep                                  (Oct 16 2025) <- RL for multi-turn context retrieval.
    /blog/devin-annual-performance-review-2025      (Nov 14 2025) <- 18 months of agents at work.
    /blog/evaluating-coding-agents                  (Sep 12 2024)
    /blog/blockdiff                                 (Jun 23 2025) <- VM snapshot format; pairs 30869b36.
    /blog/testing-development                       (May 29 2026) <- "Verifying Agentic Development at Scale"
    /blog/how-cognition-uses-devin-to-build-devin   (Feb 27 2026)
    /blog/devin-can-now-manage-devins               (Mar 19 2026) <- Agents managing agents.
    /blog/devin-can-now-schedule-devins             (Mar 20 2026) <- Pair with the above.
    /blog/closing-the-agent-loop-devin-autofixes-review-comments  (Feb 10 2026)
    /blog/devin-review                              (Jan 21 2026) <- "AI to Stop Slop".
    /blog/auto-triage                               (May 18 2026)
    /blog/swe-check-10x-faster                      (Apr 14 2026)
    /blog/codemaps                                  (Nov 4 2025)  <- Codebase comprehension.
    /blog/introducing-devin-security-swarm          (Jul 1 2026)
    /blog/devin-security-vulnerability-remediation-program  (Jul 2 2026)
    /blog/measuring-open-source-model-trustworthiness (Jul 8 2026)
    /blog/ai-productivity                           (Jun 4 2026)
    /blog/making-fable-cheaper-than-opus            (Jul 13 2026)
    /blog/devin-fusion                              (Jun 29 2026)
    /blog/swe-1-7                                   (Jul 8 2026)
    /blog/frontier-code                             (Jun 8 2026) and /blog/frontier-code-1.1 (Jul 7 2026)
    /blog/kevin-32b                                 (May 6 2025) <- multi-turn RL, CUDA kernels
    /blog/mcp-marketplace                           (Jul 22 2025) <- pairs with 45d86a7d's census
    /blog/dotnet-migration-with-devin               (Oct 28 2025) and /blog/from-jenkins-to-github-actions (Aug 5 2025)
  READ EARLIER: /blog/dont-build-multi-agents, /blog/multi-agents-working,
    /blog/what-we-learned-building-cloud-agents

*** COUNTER-POSITION TARGET — READ 16th RUN, RE-VERIFIED 19th, keep for provenance ***
https://arxiv.org/abs/2508.09815 (PDF: https://arxiv.org/pdf/2508.09815) — Krawiecka & Schroeder de Witt,
  "Extending the OWASP Multi-Agentic System Threat Modeling Guide". 8pp, plain curl -A.
  READ 16th run: 3 facts + 1 update to c02ac546. NOTE ITS MODALITY — anticipatory, no measurements.
  19th run: STILL v1, 13 Aug 2025, 8 pages (pdfinfo). It names one class TWO ways — "heterogeneous
  multi-agent exploits" in the abstract, "Heterogeneous Attackers" in the table. Its wide tables need
  SEMANTIC pairing, not positional.

*** AWS BUILDERS' LIBRARY — COMPLETE ENUMERATION (30 of 30, no more pagination) ***
URLs are opaque content IDs, NOT guessable from titles: https://builder.aws.com/content/<ID>/<slug>
READ (16 of 30):
  timeouts-retries-and-backoff-with-jitter | 3EumjoZascWd1oZiEgL8ORlv3qE            (4 facts)
  using-dependency-isolation-to-contain-concurrency-overload | 3EuxuD6bWtQ6gEp9FaKQfd3Z2AM (7)
  fairness-in-multi-tenant-systems | 3Eupj3d2bo4fEvlzYbICMZNhQ3B                   (5 facts)
  workload-isolation-using-shuffle-sharding | 3F06NpJ8YeoIGP8VHTw4n81pFn8          (1 fact)
  minimizing-correlated-failures-in-distributed-systems | 3Ev2H7t3l2eZa9xBXiZcAjz12JK (3+1upd)
  challenges-with-distributed-systems | 3F08f7GPFiZMCgXD8gny6OjxR0Z               (2+1upd)
  implementing-health-checks | 3Ev53O39izHCtWLzp4XU6t8PC1O                         (5 facts)
  making-retries-safe-with-idempotent-apis | 3Ev0BENTyBr0XxzRk5FDZzgNYos           (3 facts)
  avoiding-fallback-in-distributed-systems | 3EuS9Sakq7L3VLQIF3qzfMfke1Y           (3 facts)
  using-load-shedding-to-avoid-overload | 3Eun1EEyX6p2e3VYNyRLSJzLuMV              (5+1upd)
  avoiding-insurmountable-queue-backlogs | 3EuRcgkTP1MI0c7zM8W6HL3WIqA             (6 facts)
  avoiding-overload-...-smaller-service-in-control | 3EukISjbJAGNdrxjKaN6RG0wlHG   (2 facts)
  reliability-constant-work-and-a-good-cup-of-coffee | 3F05oqNtNUWxHJ5r6L6I2HrH4rI (3 facts)
  instrumenting-distributed-systems-for-operational-visibility | 3EuxPBdIiiUhB5IK47p3O3fxhy7 (6+2upd)
  leader-election-in-distributed-systems | 3Ev0vH0hfkcUizISUWYTvHibtcp             (2 facts)
  resilience-lessons-from-the-lunch-rush | 3Ev17ZWA9QX88MmoaULAKevIR8H             (1 fact)
UNREAD (12) — reliability first, CI/CD last. Expect LOWER yield; 6 are CI/CD and deployment.
  amazons-approach-to-building-resilient-services | 3Ev4sNuZLsnpwl9CZAOOO8hkZyf
  architecting-and-operating-resilient-serverless-systems-at-scale | 3Ev4bbEHBC5KvyYC6IcNazUXJmk
  automating-safe-hands-off-deployments | 3ErTKQOTKc5NIw031UePBPxTQ6I
  amazons-approach-to-high-availability-deployment | 3F087SyGBr7uIRtrGQDJC6trKA8
  ensuring-rollback-safety-during-deployments | 3F04j2yRAAMBuPSPs50xwXZqg01
  amazons-approach-to-automated-software-and-systems-testing | 3F07fTC9nQCkhqCTP5vIzgyOcIH
  amazons-approach-to-security-during-development | 3F07JXrYkwtKDhPgoUbI0UAA0Zf
  building-dashboards-for-operational-visibility | 3Ev2iw3R3ahQOM8BT4OUR0WP51z
  operational-excellence-at-amazon | 3Ev4irLmkHOBR3BhODX2vuE0Syf
  hands-off-automating-continuous-delivery-pipelines-at-amazon | 3Ev3Nho3q1Cs04EZUVB1ckhNJWL
  my-cicd-pipeline-is-my-release-captain | 3Ev3XnnYuuBhlgnywbbVFzwibm1
  going-faster-with-continuous-delivery | 3F08Mhh186qOa4VhG19egs06NJa
'Caching challenges and strategies' and 'Static stability using Availability Zones' are NOT in the
catalogue and appear retired.
redirects folded in:
  cookbook.openai.com -> developers.openai.com/cookbook
  blog.langchain.dev  -> www.langchain.com/blog
  aws.amazon.com/builders-library -> builder.aws.com/learn/topics/builders-library
  www.latent.space -> www.latent.space/archive (bare domain serves only a subscribe wall)
  modelcontextprotocol.io/docs/concepts/tools -> /specification/2026-07-28/server/tools (VERIFIED 200)

STRANDS DOC URLS — base is https://strandsagents.com/docs/... (NOT /latest/..., which 404s):
  .../user-guide/concepts/agents/conversation-management/  (READ; re-verified 15th run)
  .../api/python/strands.agent.conversation_manager.conversation_manager/   <- NEEDED. 714a540c attributes
     pin_first / proactive_compression to the user-guide page, which does not document them.
  .../api/python/strands.agent.agent/
Still unread: Swarm / Graph / Agent-as-Tool multi-agent patterns, session persistence.
NOTE (15th run): the Strands docs carry snake_case AND camelCase spellings side by side and document
some defaults for the TypeScript binding only. Do not record a default without recording its binding.
GOOSE (20th run): goose-docs.ai carries a banner "goose has moved to the Agentic AI Foundation
  (AAIF)", dated 2026/04/07. The docs still serve normally — a governance change, not a dead source.

*** MCP SPECIFICATION — THE REPO IS THE SOURCE, AND SITE URLs DO NOT MAP TO REPO PATHS ***
Enumerate with the recursive git-tree API and grep; NEVER build a repo path from an old site URL.
  site /specification/<rev>/...  -> repo docs/specification/<rev>/...
  site /docs/<rev>/...           -> repo docs/docs/<rev>/...
PAGE MOVES — full detail in fetch-routes route 3.
  security_best_practices: docs/docs/<rev>/tutorials/security/security_best_practices.mdx, exists for
    every revision, which is what makes revision-diffing possible.
  /docs/concepts/tools: NOT gone — REDIRECTS. Content at docs/specification/<rev>/server/tools.mdx.
*** AUTHORIZATION WAS ONE FILE AND IS NOW FOUR PAGES. ALL FOUR READ (19th). ***
  through 2025-11-25:  docs/specification/<rev>/basic/authorization.mdx        (single file, 708 lines)
  2026-07-28 + draft:  .../authorization/index.mdx (424), security-considerations.mdx (131),
                       client-registration.mdx (202), authorization-server-discovery.mdx (144)
*** VERSIONING IS TWO DIFFERENT PAGES IN TWO DIFFERENT TREES (20th run). ***
  docs/docs/<rev>/learn/versioning.mdx           EVERY revision. Short concept page (~51-68 lines).
  docs/specification/<rev>/basic/versioning.mdx  ONLY 2026-07-28 and draft (183 lines). Normative.
  ALSO READ 20th run (Backward Compatibility sections ONLY): basic/transports/stdio.mdx and
  basic/transports/streamable-http.mdx at 2026-07-28. *** THE REST OF BOTH TRANSPORT PAGES IS UNREAD
  AND HAS BEEN THE TOP MCP TARGET FOR FOUR RUNS (20th-23rd) WITHOUT BEING TAKEN. The 24th run should
  either read them or demote them explicitly — a queue item nobody takes is a queue defect. ***
RELEASED REVISION DIRECTORIES as of 2026-08-27: 2024-11-05, 2025-03-26, 2025-06-18, 2025-11-25,
  2026-07-28, plus draft. Unchanged since the 11th run — THIRTEEN consecutive runs.
REVISION FILE COUNTS (enumerate on the revision date per fetch-routes 3d, never on a docs/ prefix):
  2025-11-25 =  41 files   |   2026-07-28 = 186 files

CLAUDE PLATFORM DOCS — the prompting page routes to PER-MODEL sub-pages (found 12th run):
  .../prompt-engineering/prompting-claude-opus-5    <- has a 'Controlling subagent spawning' section
  .../prompt-engineering/prompting-claude-opus-4-8
  .../prompt-engineering/prompting-claude-sonnet-5
  .../prompt-engineering/prompting-claude-fable-5
All four UNREAD. The general claude-4-best-practices page is ~58KB — grep the persisted file.
AZURE ARCHITECTURE CENTER — prefix https://learn.microsoft.com/en-us/azure/architecture/ai-ml/
  .../guide/ai-agent-design-patterns                       (READ — c926c07b)
  .../guide/manage-foundation-models-lifecycle             (READ — updated 27652a82)
  .../guide/azure-openai-gateway-guide                     (READ — 2 facts + upd 5ad0fb45)
  .../guide/azure-openai-gateway-multi-backend             (READ — 4 facts + upd 27652a82)
  .../guide/azure-openai-gateway-monitoring                <- LAST of the gateway trio, UNREAD.
      b17b7fc2 (gateway compromise) gives this a security angle; 33aed84c's "enforce strict
      cross-model isolation" is a concrete thing to read it against.
  .../guide/rag/rag-solution-design-and-evaluation-guide   <- LARGEST unread block, plus:
      rag-preparation-phase, rag-chunking-phase, rag-enrichment-phase,
      rag-generate-embeddings, rag-information-retrieval, rag-llm-evaluation-phase
  .../guide/secure-multitenant-rag
  .../guide/genaiops-for-mlops
