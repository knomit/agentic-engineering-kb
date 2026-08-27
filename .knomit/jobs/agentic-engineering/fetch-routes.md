---
type: process
domain: [agentic-engineering, job-state]
confidence: 1
sources: 1
entities: [agentic-engineering]
refs: ['https://github.com/knomit/knomit']
---
# Per-host fetch routes and tool caveats

*** HOW TO FETCH THINGS THAT DO NOT FETCH NORMALLY. ***
Per-host recipes and tool caveats. Split out of crawl-sources.md on 2026-08-11, where they were
tangled with the source list and with per-run status.

READ THIS BEFORE RECORDING ANY SOURCE AS BLOCKED, PAYWALLED OR DEAD. The standing rule that governs
that decision lives in spec.md (Appendix S) — "never declare a source dead", with the six routes to
exhaust first. This file is the concrete how-to behind it.

Scope: durable operational knowledge. It changes when a WEBSITE changes, not when a run happens.
Do not put run status, queues or rankings here — those go in crawl-state.md.

*** ====================================================================================== ***
*** ROUTE 7. THE REVISION HISTORY GETS SQUASHED. A WALK CAN BE COMPLETE BY THE API'S OWN   ***
*** SIGNAL AND STILL BE MISSING FIVE ENTIRE RUNS. NEW, 23rd RUN, HIT LIVE.                 ***
*** ====================================================================================== ***
This is a STRICTLY WORSE failure than route 6 and it defeats route 6's fix. Route 6 says accumulate
every commit any listing names. Route 7 says: the listing may not name them at all.

MEASURED, 23rd run. The 22nd run recorded reading SEVEN revision bodies and named their commits:
  4cce7781, a5466f42, 4feee885, a21ad1c0, 3bc37431, 3c6323cd, 8b9a768d
On the 23rd run, `knomit_explain` at HEAD returned a history of THREE, with more_available FALSE:
  65e9612b (2026-08-24, "Merge pull request #9")  <- carries the 22nd run's BODY
  3c6323cd (2026-08-12, "Merge pull request #8")  <- the 16th run's body
  8b9a768d (2026-08-12, "Merge pull request #6")  <- the 13th run, the 190-URL floor
The per-run commits for runs 17-21 are GONE, folded into merge #9. Their bodies are unreachable.
Note the shape: every surviving commit is a MERGE COMMIT. Per-run writes are squashed into the merge
for their pull request, so a run's individual revision survives only until the next PR merge.

WHY THE WALK STILL LOOKS CLEAN: more_available was FALSE. The API said the history was complete, and
by its own reckoning it was — those commits no longer exist on this path. A run that trusts
more_available and does not cross-check will report "COMPLETE, NO GAPS" while missing five runs.

*** THE ONLY RELIABLE TELL IS THE RUN-NUMBER SEQUENCE IN THE BODIES. *** Every body opens
"crawled: <date> (Nth run)". Read the numbers you actually got. The 23rd run got 22, 16, 13 — so
runs 14, 15, 17, 18, 19, 20 and 21 are missing, and the ones after 16 were missing SILENTLY and
recently. Route 6 introduced this cross-check as a free bonus; route 7 promotes it to the PRIMARY
integrity test of the walk. more_available is not evidence. The run numbers are.

*** 7b. SHORT COMMIT HASHES DO NOT RESOLVE. `knomit_explain` NEEDS THE FULL 40-HEX. ***
AND THIS IS WHY THE SQUASH IS UNRECOVERABLE: crawl-state bodies record commits in PROSE as 8-char
prefixes. Those cannot be passed back to the tool.
  knomit_explain(commit="4cce7781") -> "could not read ... at 4cce7781"
ISOLATED BEFORE BLAMING THE SQUASH, per Appendix S: the same call with a KNOWN-GOOD commit's short
prefix fails identically — knomit_explain(commit="3c6323cd") errors, while the full
3c6323cd52188f057c16d15b2c7b72ad9d9e91e9 succeeds. So a short-hash failure tells you NOTHING about
whether the commit exists. Do not read it as evidence of a squash, and do not read it as evidence of
a live commit either.
*** ACTION FOR EVERY FUTURE RUN, one line, costs nothing: when recording commits in a crawl-state
body, WRITE THE FULL 40-HEX HASH. The 8-char convention has silently made every prior run's recorded
history unusable for recovery. ***
What is NOT lost when a squash happens: the URL union is anchored on 8b9a768d's enumerated 190 plus
per-run counts that surviving bodies quote, and the QUEUE is carried forward in each body's
per-source section. So a squash costs the URL-level detail of the lost runs, not the work list.

*** ====================================================================================== ***
*** ROUTE 6. THE HISTORY WALK SKIPS ONE BODY PER HOP IF YOU ANCHOR ON THE OLDEST REVISION. ***
*** 22nd run. STILL TRUE, BUT READ ROUTE 7 FIRST — IT IS THE LARGER FAILURE.               ***
*** ====================================================================================== ***
Appendix S says: take the OLDEST commit in `history.revisions` and call knomit_explain again with it.
That advances the window correctly, but it does NOT read every revision, and the shortfall is invisible.
MEASURED ON THE 22nd RUN, every hop:
  explain(no commit)      -> revisions [4cce7781, 22649951, a5466f42]   more_available true
  explain(a5466f42)       -> revisions [a5466f42, 4feee885, a21ad1c0]
  explain(a21ad1c0)       -> revisions [a21ad1c0, 7a9ec830, 3bc37431]
  explain(3bc37431)       -> revisions [3bc37431, 0ac250fd, 3c6323cd]
  explain(3c6323cd)       -> revisions [3c6323cd, 8b9a768d]             more_available FALSE
EACH CALL RETURNS THE ANCHOR PLUS THE TWO NEXT-OLDER, AND ANCHORING ON THE OLDEST ADVANCES BY TWO. So
the MIDDLE entry of every listing is NAMED but its BODY IS NEVER FETCHED. Skipped without
intervention that run: 22649951, 4feee885, 7a9ec830, 0ac250fd — and 4feee885 WAS THE ENTIRE 19th RUN.
Appendix S's step 4 warns that consecutive calls overlap by one revision and to dedupe by hash; it
does NOT warn that the middle entry is never read, because the overlap it describes is the ANCHOR.
THE RULE: **the revision LIST is the work list, not the anchor chain.** After each call, add all
returned commits to a to-read set; then read every one whose body you have not already seen.
NOTE THE INTERACTION WITH ROUTE 7: on the 23rd run this fix was applied and made no difference,
because the listing was only three long and every entry was read. Route 6 protects against a walk
that under-reads what it was offered. Route 7 is about what it is never offered.

*** ====================================================================================== ***
*** ROUTE 4. THE TOOL ITSELF CAN INVENT THINGS. THE MOST IMPORTANT ENTRY IN THIS FILE FOR  ***
*** FACT QUALITY. 20th run; SCOPE WIDENED BY THE 21st, 22nd AND 23rd. READ BEFORE WRITING  ***
*** ANY FIGURE, QUOTATION OR IDENTIFIER INTO ANY FACT.                                     ***
*** ====================================================================================== ***
`WebFetch` answers a prompt against the page using a SMALL FAST MODEL. That model will FILL GAPS
WITH PLAUSIBLE VALUES when the prompt invites a narrative summary. This is not a page problem, not a
fetch failure, and not something the 404-body guard or any download check can catch — the fetch
succeeded and the prose reads perfectly.

ISOLATED CLEANLY, 20th run: SAME URL, two calls, only the PROMPT differed.
  Call 1, open-ended ("extract the full substance ... any specific numbers") returned:
    "a monitor suspicion score of 3 out of 100 within 5,000 queries, compared to Best-of-N baseline
     scores of 14-18 across three runs of 150,000 queries each"
  Call 2, verbatim-demanding ("Quote VERBATIM ... or say NOT STATED") returned:
    "In one run, the evolutionary algorithm achieved a score of 3 in under 5k steps"
    "BoN scores of 14, 15 and 18"      Query count for BoN: **NOT STATED**
THREE FABRICATIONS IN ONE SENTENCE: (i) "out of 100" — a scale maximum the page never gives; (ii)
"across three runs of 150,000 queries each" — an entire baseline budget, invented, and it was the
denominator the whole efficiency comparison rested on; (iii) "queries" for the source's "steps".

*** THE 21st RUN WIDENED THE CLASS TWICE, AND NEITHER NEW CASE IS A NUMBER. ***
  (iv) A VERSION IDENTIFIER. Open-ended reported "Claude 3.5 Sonnet"; verbatim returned "Claude 3.7
       Sonnet". A minor-version slip that would have mis-specified the capability gap under test.
  (v)  A PARAPHRASE ARRIVING INSIDE QUOTATION MARKS, on the LiteLLM post.
SO THE RULE IS NOT "VERIFY NUMBERS". IT IS: ANY STRING YOU INTEND TO PUT IN QUOTATION MARKS, ANY
FIGURE, ANY THRESHOLD, AND ANY VERSION OR PRODUCT IDENTIFIER GOES THROUGH THE SECOND CALL.

*** 22nd-RUN ADDITION: THE SECOND CALL ALSO CATCHES THE OPPOSITE ERROR — AN OPEN-ENDED CALL
*** REPORTING SOMETHING AS ABSENT THAT IS PRESENT, WHICH PRODUCES AN UNDERCLAIM. ***
On the Echoverse post an open-ended read left the impression that live-web transfer was described
qualitatively; a targeted call returned the figures and, asked directly whether the post says
transfer was unmeasured, answered NOT STATED. So the second call is an ABSENCE filter as well as a
fabrication filter, and ASKING THE NEGATIVE QUESTION EXPLICITLY ("does the post state anywhere that
X was NOT measured?") is what separates "the page does not say it" from "I did not see it".

*** 23rd-RUN ADDITION (vi): THE OPEN-ENDED CALL DROPS QUALIFYING CLAUSES AND INVERTS AGENCY, AND
*** BOTH SURVIVE A PLAUSIBILITY CHECK BECAUSE THE RESULT READS AS A CLEANER FINDING. ***
Three measured cases in one run:
  * A DROPPED MODAL SCOPE. Open-ended on the embracethered Auto Mode post gave "60-80% success
    rates"; verbatim gave "I got attack success rates up to 80% using a small sample size". The
    range was invented AND the small-sample caveat was dropped.
  * AGENCY INVERTED. The same open-ended call listed `python3 -I` under "Recommended Mitigations".
    Verbatim: "The child uses `python3 -I -c ...` to avoid recursively falling for the same shadowing
    attack" — it is what the ATTACKER's payload does. A defensive recommendation was manufactured
    out of an attacker technique, which is the most dangerous single error class in this pack.
  * A CLAUSE THAT REVERSES A CLAIM'S SCOPE. On the AISI sandbox-escape post, both calls agreed models
    escape misconfigurations "reliably". Only a THIRD, targeted call surfaced the full sentence:
    "Advanced models can reliably escape common misconfigurations **when prompted to do so**." That
    turns a behaviour claim into an elicited-capability claim.
THE LESSON, and it sharpens the existing rule: ENUMERATE THE QUALIFIERS, NOT ONLY THE FACTS. Ask for
the WHOLE SENTENCE containing a claim, not for confirmation that the claim appears. "Quote the full
sentence and note whether the word X actually appears" caught what "does the source say X" missed.

NOTE THE BIAS, because it is what makes this dangerous: every invention made the account MORE
COMPLETE AND MORE QUOTABLE. Fabrication here is not random noise, it is narrative gap-filling, so the
invented detail is exactly the one that makes a fact worth writing. It will pass a plausibility check
because plausibility is what produced it.

THE RULE, and it is cheap enough that there is no excuse:
  * NEVER write a number, a quotation, a named threshold or a version identifier into a fact from an
    OPEN-ENDED WebFetch.
  * Run a SECOND call on the same URL whose prompt says: "Quote VERBATIM the exact sentences that
    state each of these, or say NOT STATED if absent", enumerating each item you intend to use.
    The "or say NOT STATED" clause is load-bearing.
  * Anything the second call marks NOT STATED does not go in the fact.
  * IF YOU DID NOT ASK THE SECOND CALL ABOUT IT, YOU DO NOT HAVE IT. Runs 21-23 dropped figures, an
    entire worked example, and a clause about local MCP servers on this basis. Omitting is cheaper
    than hedging — but see the 23rd run's amendment: VERIFYING IS CHEAPER STILL. Two extra calls in
    the 23rd run's self-review CONFIRMED two claims that would otherwise have been dropped, and
    surfaced the "when prompted to do so" qualifier as a bonus. Prefer one more call to a deletion.
  * CALIBRATION, so this is not read as "WebFetch is unreliable": the two-call pattern confirmed 7/7
    and 8/8 figures on two pages and 8/8 quoted strings on a third in the 20th run, 8/8, 6/6 and 8/8
    across three pages in the 21st, 10/10 and 8/9 on one arXiv paper plus 5/5 on Echoverse in the
    22nd, and in the 23rd 8/8 on the AISI optstop post and 7/7 on the embracethered post. The tool is
    accurate when the page states the thing. It invents when the page does NOT.
  * THIS IS ALSO RETROSPECTIVE. When verifying an old fact, the detail most likely to be fabricated
    is the one that COMPLETES A SET.

*** ====================================================================================== ***
*** ROUTE 5. READING AN INDEX AS A LIST IS ONE PLAIN WebFetch AND IT RETURNS THE WHOLE     ***
*** ARCHIVE. 21st run; VOLUME CORRECTED UPWARD BY THE 23rd.                                ***
*** ====================================================================================== ***
  WebFetch {url: "<feed index>", prompt: "List EVERY post visible on this index as a list: exact
    title, exact href/slug, and date, newest first. Do not summarise."}
MEASURED RESULTS, one call each, plain WebFetch, no browser, no gate:
  www.aisi.gov.uk/blog   -> 95 posts (21st run); the 23rd run's call returned the newest 10 and then
                            summarised the rest as "[Continued with remaining 90+ posts...]".
  cognition.com/blog     -> 82 posts, complete archive back to 2024-03-12
  embracethered.com/blog -> 21st run: 10 posts back to 2026-03-16. *** 23rd run: THE COMPLETE ARCHIVE,
                            ~180 posts back to 2018-12-16. The 21st run's figure was not the site's
                            limit. ***
  microsoft.com/en-us/security/blog -> 12 posts (paginated; front page only)
*** 23rd-RUN CALIBRATION, AND IT MATTERS FOR PLANNING: THE SAME URL RETURNS DIFFERENT DEPTHS ON
*** DIFFERENT RUNS. *** AISI gave 95 posts once and 10-plus-an-ellipsis another time; embracethered
gave 10 once and ~180 another. The depth is a property of the CALL, not of the site. So:
  * Never record "this feed has N posts" as a fact about the feed. Record it as what one call returned.
  * If you need the back catalogue and the call returns an ellipsis, ASK AGAIN naming the period you
    want ("list every post from 2025"), rather than concluding the archive is short.
  * A catalogue in crawl-sources can be INCOMPLETE without being wrong. Treat a new deeper listing as
    an extension, not a contradiction.
TWO STANDING CAUTIONS:
  * THE OUTPUT IS AN EXTRACTION, SO ROUTE 4 APPLIES. The tell that you are getting real hrefs rather
    than derived ones is a TITLE/SLUG MISMATCH. A list where every slug is a clean slugification of
    its title is the one to distrust.
  * A LIST IS NOT A READ. Record the keep/skip decisions in crawl-sources.

*** 5b. THE SAME CALL PULLS AN EXACT ASSET HREF OFF A PAGE, WHICH BEATS SEARCHING FOR IT. 22nd run. ***
  WebFetch {url: "<post>", prompt: "Give me the EXACT href/URL of every link in this post that points
    to a paper, PDF or report. Quote the link text and the full URL verbatim."}
The AISI OpenClaw paper is a Webflow CDN hash path — unguessable and unsearchable, because it is not
indexed under its title. RULE: when a post names an artifact, ASK THE POST FOR THE HREF before
searching for the artifact. Route 1b is for a slug on a site that publishes pages; it does not find
hash-named assets on a CDN.
HOSTING NOTE: cdn.prod.website-files.com serves PDFs to a plain `curl -sL -A "Mozilla/5.0"` with no
gate, no Referer, no cookie. Percent-encoding in the filename (%20) passes through fine.

*** 5c. ON A BROWSER-ONLY HOST, THE HREF-HARVEST IS A querySelectorAll. NEW, 23rd run, AND IT FOUND
*** A POST NO CATALOGUE KNEW ABOUT. ***
openai.com cannot be read by WebFetch (route 1), so 5b does not apply there. The equivalent:
  mcp__browser__browser_evaluate {function: "() => Array.from(document.querySelectorAll('a[href*=\"/index/\"]')).map(a => a.textContent.trim().slice(0,80) + ' -> ' + a.getAttribute('href')).filter((v,i,s) => s.indexOf(v)===i).join('\\n')"}
Run on any openai.com/index post, this returns the "Keep reading" footer's EXACT slugs with titles
and dates attached. On the 23rd run it returned
/index/hugging-face-incident-and-the-road-ahead/ (Aug 26 2026) — OpenAI's full incident post-mortem,
published the day before, in no catalogue, and the single highest-value document of the run.
THE STANDING PRACTICE THIS ESTABLISHES: on any browser-only host, harvest hrefs from EVERY page you
visit, not just from the index. The footer of a post you were reading anyway is a free discovery
sweep, and it is more current than any catalogue.

*** FETCH ROUTES. READ BEFORE CALLING ANYTHING BLOCKED. ***

1. openai.com/index/<slug> RETURNS HTTP 403 TO WebFetch. IT READS FINE IN A REAL BROWSER.
   *** THE RULE IS NOW PROVEN, NOT JUST STATED: THE BROWSER SERVER AVAILABLE VARIES BETWEEN RUNS.
   *** CHECK WHAT IS PRESENT; DO NOT HARDCODE EITHER NAME. ***
   23rd-RUN EVIDENCE: `mcp__claude-in-chrome__*` FAILED — navigate timed out after 8s on its hidden
   tabs_context lookup, and an explicit tabs_context_mcp returned "Browser extension is not
   connected." The runs 14-22 recipe was therefore unusable. `mcp__browser__*` worked first try on
   the same URL. Neither server is the reliable one; the fallback IS the recipe.
     mcp__claude-in-chrome__navigate {url} -> tabId ; then get_page_text {tabId}
     mcp__browser__browser_navigate {url}  -> then EITHER browser_snapshot OR, better, see below
   *** FOR mcp__browser__, PREFER browser_evaluate OVER browser_snapshot FOR ARTICLE TEXT: ***
     browser_evaluate {function: "() => { const el = document.querySelector('article') || document.querySelector('main') || document.body; return el.innerText.slice(0, 40000); }"}
   browser_snapshot writes an accessibility tree to a FILE and returns only a path; the evaluate call
   returns the article text inline, which is what you want. The 23rd run read two long openai.com
   posts this way in one call each.
   The server must run REAL Chrome, not headless Chromium — headless gets a Cloudflare interstitial.
   Plain curl also 403s. Do NOT record openai.com as paywalled or dead.
   *** THE BROWSER ROUTE'S QUALITY ADVANTAGE, WHICH ROUTE 4 MAKES DECISIVE: *** both get_page_text
   and the innerText evaluate return RAW ARTICLE TEXT with no model in the loop, so figures taken
   from them are TRANSCRIPTIONS, not extractions, and cannot be fabricated. Where a page is
   browser-readable AND number-heavy, prefer the browser even when WebFetch works. The 23rd run took
   a dozen figures and quoted strings off the OpenAI post-mortem with no second call needed — the
   single largest saving route 4 permits.
   NOTE ON claude-in-chrome navigate ERGONOMICS (17th run, re-confirmed through the 22nd): calling
   `navigate` STANDALONE with no tabId auto-creates the tab group and returns the tabId. To read
   several posts, PASS THE SAME tabId to each subsequent navigate, then tabs_close_mcp once.
   mcp__browser__ needs no tab management at all — navigate, evaluate, navigate again.
   NOTE THE HOST BOUNDARY: this is openai.com ONLY. developers.openai.com and cdn.openai.com are NOT
   403 — the API guides read fine with plain WebFetch, and cdn.openai.com PDFs download with curl -A.
   *** THE "Keep reading" FOOTER IS A CHEAP DATE ORACLE AND A DISCOVERY FEED. *** It is a plain
   RECENCY feed of the three newest posts, NOT category-scoped (hypothesis falsified, 20th run). Two
   independent footers agreeing pinned The Defender's Window to Aug 17 2026 (22nd run, confirmed
   correct by the 23rd, which read the post: byline Greg Brockman, dated August 17, 2026). See 5c for
   harvesting it properly.

1b. *** CHEAPEST WAY TO RESOLVE AN UNKNOWN SLUG: WebSearch WITH allowed_domains. 14th run. ***
   Guessed slugs have now 404'd on cognition, strands, adk, openai AND anthropic.
     WebSearch {query: "<exact article title>", allowed_domains: ["openai.com"]}
   VALIDATED SIX TIMES (runs 14-20), including the ANS resource slug which contains a TYPO nobody
   would guess ("al" for "AI"), and the anthropic.com watermark post whose real slug is SHORTER than
   its title. VALIDATED A SEVENTH TIME on arXiv (22nd run): a paper known only by title resolved in
   one search, and the result set carried the HTML full-text URL (/html/<id>v1), which is what you
   want — /abs/ gives only the abstract.
   *** THE 22nd RUN'S NEGATIVE RESULT BOUNDS THIS ROUTE: *** WebSearch did NOT find the AISI OpenClaw
   paper, because it is a hash-named PDF on a CDN rather than a published page. For an artifact
   LINKED FROM a page you already have, use route 5b (or 5c on a browser-only host).
   PRIORITY: route 5/5c for sweeps and discovery, 1b for a specific unknown slug or 404 recovery,
   5b for a linked asset.

*** 3. modelcontextprotocol.io UNREACHABLE -> READ THE SPEC REPO ON GITHUB. 16th run. ***
   On 2026-08-12 the host refused connections outright; it was back up on 08-14 and since. That
   outage was transient. The repo route remains preferred anyway — cheaper, and it enables diffing.
   THE MIRROR IS THE SPEC ITSELF: the site renders .mdx files straight out of
   github.com/modelcontextprotocol/modelcontextprotocol.
     # enumerate — the ONLY reliable way to find a page, because paths have moved
     curl -sL -A "Mozilla/5.0" \
       "https://api.github.com/repos/modelcontextprotocol/modelcontextprotocol/git/trees/main?recursive=1" \
       -o tree.json
     grep -oE '"path":"[^"]*<keyword>[^"]*"' tree.json | sort -u
     # then fetch raw
     curl -sL -A "Mozilla/5.0" -o out.mdx \
       "https://raw.githubusercontent.com/modelcontextprotocol/modelcontextprotocol/main/<path>"
   *** THE TRIPWIRE HAS A ZERO-FETCH FORM. ***
     curl -sL -A "Mozilla/5.0" \
       "https://api.github.com/repos/modelcontextprotocol/modelcontextprotocol/contents/docs/specification"
   Lists one directory per released revision (2024-11-05, 2025-03-26, 2025-06-18, 2025-11-25,
   2026-07-28, draft). A new revision is a new directory. Cheapest possible check, works when the
   website does not. UNCHANGED THROUGH THE 23rd RUN (thirteen consecutive).
   23rd-RUN TIP: pipe it through `grep -oE '"name":"[^"]*"' | sort -u` — the raw JSON is large and
   the directory names are the entire signal.

   *** PATH MAPPING — CORRECTED 2026-08-14 (17th run). ***
     site /specification/<rev>/...   -> repo docs/specification/<rev>/...
     site /docs/<rev>/...            -> repo docs/docs/<rev>/...
   CORRECTION 1 — /docs/concepts/tools IS NOT GONE. It answers HTTP 200 and REDIRECTS to
   https://modelcontextprotocol.io/specification/2026-07-28/server/tools.
   CORRECTION 2 — the tool CONTRACT material lives at docs/specification/<rev>/server/tools.mdx, not
   at docs/docs/<rev>/learn/server-concepts.mdx (grepped: zero hits).
   THE LESSON: a redirect target is evidence, a guessed successor is not — confirm a page move by
   GREPPING THE NEW PAGE FOR THE CONTENT.
   CAVEAT TO STATE IN ANY FACT BUILT THIS WAY: `main` is the live editing branch, not a release tag.

   *** 3b. A PAGE CAN BE A FILE IN ONE REVISION AND A DIRECTORY IN ANOTHER — OR IN A DIFFERENT TREE
   *** ENTIRELY. Do NOT build a predecessor path by substituting the revision date into a current path.
   AUTHORIZATION — file becomes directory:
     through 2025-11-25 -> docs/specification/<rev>/basic/authorization.mdx  (ONE FILE, 708 lines)
     2026-07-28 + draft -> docs/specification/<rev>/basic/authorization/     (A DIRECTORY of four pages)
   VERSIONING — TWO DIFFERENT PAGES WITH THE SAME NAME IN TWO DIFFERENT TREES (20th run):
     docs/docs/<rev>/learn/versioning.mdx          EVERY revision. Short conceptual page.
     docs/specification/<rev>/basic/versioning.mdx ONLY 2026-07-28 and draft. The long normative page.
   ALWAYS resolve both paths out of tree.json rather than by string substitution.

   *** 3c. THE 404 THAT SILENTLY BECOMES A FALSE "ENTIRELY NEW IN THIS REVISION" FINDING. 18th run. ***
   `raw.githubusercontent.com` answers a missing path with **HTTP 404 whose BODY is the literal text
   `404: Not Found`** — and `curl -sL -o file` WRITES THAT BODY TO THE FILE and exits 0. `diff old new`
   then reports every line of the new revision as added.
   THE GUARD, cheap and mandatory before any revision diff:
     wc -l *.mdx                      # a 0- or 1-line .mdx is a 404, not a short page
     grep -c "404: Not Found" out.mdx  # must be 0

   *** 3d. THE MCP REPO HAS A SEPARATE TOP-LEVEL schema/ TREE. A docs/-SCOPED SWEEP MISSES IT. ***
     schema/<rev>/schema.json (~4000 lines), schema.ts (~2600), schema.mdx
   When establishing that something is ABSENT from a revision, enumerate on the REVISION DATE:
     grep -oE '"path":"[^"]*<rev>[^"]*\.(mdx|json|ts)"' tree.json | sed 's/"path":"//;s/"$//'
   REVISION SIZES, MEASURED: 2025-11-25 = 41 files; 2026-07-28 = 186 files.

   *** 3e. IN .mdx, NORMATIVE KEYWORDS ARE BOLDED — SO GREPPING A NORMATIVE SENTENCE FINDS NOTHING.
     grep -c "MUST NOT assume that credentials"  -> 0   (looks like absence)
     grep -c "assume that credentials"           -> 1   (it is there)
   RULES: NEVER let a search term span a normative keyword. The failure is silent and total.

2. OWASP PDF DOWNLOADS ARE GATED ON THE USER-AGENT. NOTHING ELSE. `-A` IS THE WHOLE FIX.
     curl -sL -A "Mozilla/5.0" -o out.pdf "https://genai.owasp.org/download/<id>/?tmstv=<epoch>"
     file out.pdf     # MUST say "PDF document". "HTML document" = the default curl UA went out.
     pdftotext out.pdf out.txt      # then Read out.txt
   ISOLATED A/B, 2026-08-11, same URL, four requests back to back:
     bare curl -> HTML (821KB, "No Access");  -A only -> PDF;  Referer only -> HTML;  -A + Referer -> PDF
   THIS SOURCE HAS BEEN MISDIAGNOSED THREE TIMES, EACH BY A RUN THAT SUCCEEDED WITHOUT ISOLATING:
     11th "needs a form" -> wrong;  13th "needs a Referer" -> wrong;  14th "needs a session cookie" -> wrong.
   WHEN A FETCH FINALLY WORKS, DROP ONE FLAG AT A TIME BEFORE RECORDING THE RECIPE.
   The tmstv token is NOT an expiring nonce — 1754459367 worked 15 days after it was recorded.

2b. GETTING THE OWASP DOWNLOAD ID — THE TWO-STEP, CONFIRMED 15th, 16th AND 18th RUNS.
     (i)  WebFetch https://genai.owasp.org/resource/<slug>/ asking for "the direct PDF download URL
          if present in the page HTML (look for links containing /download/)". The resource PAGE is
          NOT UA-gated. (ii) curl that URL with -A per route 2.
   18th-RUN BONUS: step (i) also returns the PUBLICATION DATE. Pair with `pdfinfo`.

*** 2c. `file` REPORTS A PDF PAGE COUNT AND IT CAN BE WRONG. USE `pdfinfo`. 19th run. ***
  file masec.pdf -> "3 pages" WRONG;  pdfinfo masec.pdf -> "Pages: 8" CORRECT.
A run doing a staleness check with `file` would have manufactured a "THE SOURCE CHANGED" finding.
`file` is still the right tool for the ONE question route 2 asks it (PDF vs the HTML error page).
Record the pdfinfo fingerprint (pages + CreationDate) for every PDF you read — "proven unchanged" is
a stronger claim than "I re-read it".

The 12th run's WebFetch route still works and needs no headers — keep it as the fallback:
  1. WebFetch the RESOURCE PAGE asking for the direct PDF download URL.
  2. WebFetch that download URL. It REPLIES that the content is unreadable binary — ignore that;
     the result ends with "[Binary content (application/pdf, N MB) also saved to <path>]".
  3. Parse that path with pdftotext, writing a .txt; read the .txt in page slices.
pypdf caveats: the true page count can exceed what Read advertises; Read's `limit` counts LINES and
one PDF page is one very long line; slide-deck PDFs lose word spacing but stay readable.
PDF NAVIGATION TIP: `grep -n` for numbered section headings first and read targeted slices.

*** 2d. ugrep REJECTS `.{0,N}` CONTEXT PATTERNS ON THIS MACHINE. USE -n PLUS sed. 21st run. ***
The idiom `grep -o -i ".\{0,90\}<term>.\{0,90\}"` fails with "exceeds complexity limits". It fails
LOUDLY, but a run that mistakes the error for "no matches" manufactures a false absence.
  grep -n -i -- "<term>" file.txt        # get line numbers
  sed -n '<start>,<end>p' file.txt       # read the surrounding lines
Note `--` before the pattern: several useful search terms begin with a digit or a dash.

*** THE FORM-FEED RULE. 18th-run review pass. ***
*** pdftotext EMITS \f (0x0C) AT EVERY PAGE BREAK AND PREPENDS IT TO THE FIRST TOKEN OF THE NEXT
*** PAGE. SO ANY ^-ANCHORED PATTERN SILENTLY MISSES EXACTLY ONE ITEM PER PAGE BOUNDARY.
  grep -E "^ASI[0-9]{2}$" -> 9 of 10.  grep -xE -> 9 of 10 (-x is an anchor too).  grep -oE -> 10 of 10.
RULES: for COUNTING, always unanchored `grep -o`. For a NEGATIVE test, an anchored miss is not absence.
*** SIX MECHANISMS — A NEGATIVE OR WRONG RESULT ARRIVES FOR SIX INDEPENDENT REASONS:
***   (i) pdftotext line-wrapping splits a multi-word phrase across lines;
***  (ii) pdftotext hyphen-breaking splits a single token ("communica-\ntion");
*** (iii) pdftotext form feeds defeat ^-anchors, one miss per page;
***  (iv) MARKDOWN EMPHASIS in .mdx sources breaks any phrase spanning a **MUST** (route 3e);
***   (v) AN OPEN-ENDED WebFetch INVENTS THE DETAIL rather than reporting its absence (route 4);
***  (vi) THE GREP ITSELF ERRORS OUT and the error is mistaken for zero matches (route 2d).
*** ALWAYS grep the rarest SINGLE word, then read the lines.
*** PDF TABLES EXTRACT WITH THEIR COLUMNS SHUFFLED — DO NOT CITE ONE (16th run). ***
*** BUT A TABLE IS STILL SAFE TO COUNT (17th run). *** Interleaving destroys the PAIRING, not the
cells, so `grep -oE '<TOKEN>' | sort | uniq -c` gives a trustworthy FREQUENCY. State in the fact which
of the two you relied on — frequency is publishable, pairing is not.
*** AND SOME PDF TABLES DO EXTRACT ROW-FAITHFULLY — CHECK BEFORE GIVING UP (18th run). ***
Narrow tables with short cells serialise cleanly; wide tables with multi-line prose cells interleave.
*** WHEN THE TABLE IS THE WIDE KIND, PAIR ON CONTENT INSTEAD OF POSITION (19th run). ***
*** 22nd-RUN VARIANT: a small two-column table can extract as TWO SEPARATE VERTICAL RUNS — all the
*** labels, then all the values — so `paste - -` desynchronises. Safe only when every value
*** self-identifies. Note in the fact that the pairing is semantic rather than positional.
*** AND A DOCUMENT'S PROSE AND ITS NUMBERS CAN SIT 2,300 LINES APART (21st run). *** After writing a
fact from a long PDF's narrative, grep the WHOLE extract for the campaign/product name again.
BROWSER CAVEATS: on builder.aws.com the FIRST get_page_text after a navigate SOMETIMES returns a stub
ending in 'Loading article'; call it again. Never conclude 'blocked' from one empty call.
To pull links/hrefs off an index on a browser-only host, see 5c — `find` returns element refs but NOT
hrefs, so use an evaluate with querySelectorAll. (TRY ROUTE 5/5b FIRST where WebFetch works at all.)
NOTE: large learn.microsoft.com and platform.claude.com pages exceed WebFetch's inline limit and are
persisted to a file on disk; just Read the path returned, or grep it. Likewise a broad knomit_query
can exceed the tool-result limit — use limit<=25.
AND knomit_explain ON crawl-state.md NOW EXCEEDS IT TOO (51.5KB at the 15th run, 56.8KB at the 22nd).
That is expected, not an error — the tool result names the path; just Read it. Do not retry the call.
THE PERSISTED FILE IS ONE LINE OF JSON, so `Read` truncates and paginating it is useless. 22nd-RUN
TIP, needs no interpreter:
  cut -c1-6000 <file>        # head of the body
  cut -c54000-57000 <file>   # the tail, where `history.revisions` lives
(python3 IS available in this job's Bash despite an older note in Appendix S; Write and Edit are what
is denied. 23rd-run note: on this run the explain result came back inline and no cut was needed —
do not assume the persist-to-file path will trigger.)
*** knomit_query sort=recent IS ORDERED BY LAST TOUCH, NOT BY CREATION (18th run). ***
An update bumps a fact to the front, so the TAIL of a sort=recent walk is the set of facts LEAST
RECENTLY VERIFIED. Reaching it costs ~15k tokens per page at limit=25.
*** THE SAME CAVEAT APPLIES TO `committed_at`, AND IT DEGRADES THE EARLIEST-COMMITTED AXIS (23rd run).
*** committed_at is LAST TOUCH. Facts created on the first run but updated last week carry a recent
*** timestamp, so sorting by it does NOT give you creation order. Use it as a rough signal and rely on
*** the VERIFICATION POOL LIST in crawl-state — "never appears in the pool" is the sound test for
*** never-checked, and it is the one the 23rd run used.
*** CHEAPER WAY TO FIND A FACT'S PATH WHEN YOU ONLY HAVE ITS SHORT ID (19th run). ***
knomit_query CANNOT search by id. Run a TOPICAL query aimed at what the fact is about — the id is the
filename stem, so it is visible in the `file` field of any matching row. 22nd-RUN CALIBRATION: two of
four queued ids took three differently-angled queries to surface, and one (af3acf92) never appeared.
Budget two or three queries, then substitute another fact at the same confidence.
*** 23rd-RUN NOTE ON PICKING A SAMPLE WITHOUT CHASING IDS: *** the queued never-checked list named
eight ids, THREE of which (0f260eea, 1d1440fe, 4166926d) are under kb/principles/ and are write-
blocked, so they can never be sampled. Check the topic prefix before queueing an id, or the next run
inherits a shortlist it cannot use.
*** AND THE CHEAPEST WAY TO PICK A STALENESS SAMPLE (20th and 21st runs). *** Every knomit_query
result row carries `committed_at` AND `refs` in its frontmatter, so the topical queries you run anyway
for the query-first rule hand you both axes for free: sort rows by `committed_at` for age (with the
caveat above), group by identical `refs` for shared-ref. Reference points:
1785089xxx ≈ 2026-07-26 (first run), 1786817xxx ≈ 2026-08-15, 1787275xxx ≈ 2026-08-20,
1787357xxx ≈ 2026-08-21, 1787656xxx ≈ 2026-08-24.
*** THE `grep` ON THIS MACHINE IS ugrep 7.5.0, NOT GNU grep (18th run). ***
If a grep behaves unexpectedly, check `grep --version` before concluding anything about the DATA.
The Bash tool's working directory PERSISTS between calls — prefer absolute paths or re-`cd` each call.
*** BUILDERS' LIBRARY — SOME ARTICLES ARE VIDEO-ONLY ***
Confirmed video-only, no prose body, DO NOT RE-FETCH:
  amazons-approach-to-failing-successfully   | 3F05J4fjklUZCE7kjuIp6LaTacl
  beyond-five-9s-lessons-from-our-highest-available-data-planes | 3F073j4jJOsSRTDlQM3eiZxkFLm
Budget one cheap fetch per article and abandon if the text ends right after the byline.

*** VERIFICATION TECHNIQUE, NOT A FETCH ROUTE, BUT IT LIVES HERE BECAUSE IT IS A RECIPE (16th run) ***
DIFF TWO REVISIONS OF THE SAME SPEC PAGE:
  curl the <old-rev> and <new-rev> copies of the page, then `diff a b`
On the MCP security page this yielded, in one pass: a heading rename that CONFIRMED a fact's
prediction, a MUST downgraded to SHOULD that CORRECTED the same fact, a new subsection that
contradicted another fact's title, and three wholly new attack sections.
CALIBRATION (17th run): a THREE-LINE diff is a REAL and useful result — it says the page is stable.
CALIBRATION (20th run): where a concept page and a normative page both exist, DIFF THE CONCEPT PAGE
(small, stable, every revision) TO LOCATE THE CHANGE, then READ THE NORMATIVE PAGE for its force.
*** SIX HARD PRECONDITIONS ON THIS TECHNIQUE, ALL LEARNED THE HARD WAY. ***
  (a) RESOLVE BOTH PATHS FROM tree.json. Never substitute a revision date into a path — see 3b.
  (b) VERIFY BOTH FILES ARE REAL BEFORE DIFFING. A 404 body diffs as "all new" — see 3c.
  (c) DIFF THE IMMEDIATE PREDECESSOR, NOT A CONVENIENT OLDER ONE. A two-revision jump cannot
      distinguish "new" from "moved", and "new in revision X" is a claim a reader will act on.
  (d) BOUND THE REGION ON THE FOLLOWING HEADING, NOT ON EOF. Use
      `awk '/^## Target/{f=1} /^## NextHeading/{f=0} f'`. An over-wide range ADDS phantom findings.
  (e) A SPLIT DUPLICATES RULES, AND THE COPIES CAN DIFFER IN MODAL STRENGTH. Before recording any
      weakening, grep EVERY page of the new revision and cite the strongest.
  (f) A PAGE THAT DELEGATES A RULE LOSES ITS FORCE IN THE SUMMARY. IF A PAGE SAYS A RULE IS
      SPECIFIED ELSEWHERE, YOU HAVE NOT READ THE RULE. Follow the pointer before writing any modal
      verb, and expect per-binding rules to differ by binding.
*** AND WHEN A CLAIM SPANS DOCUMENTS, GREP THE WHOLE REVISION, NOT THE ONE PAGE (18th run). ***
*** AND IF A SENTENCE'S SUBJECT IS THE REVISION, THE SEARCH'S SCOPE MUST BE THE REVISION (19th). ***
*** AND A TOKEN CAN SURVIVE A REVISION WHILE ITS MEANING DOES NOT (20th run). *** A POSITIVE grep is
as weak a form of evidence as a negative one when the claim is about SEMANTICS: read the hits.
