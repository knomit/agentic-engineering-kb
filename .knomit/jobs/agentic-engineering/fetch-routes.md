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
*** ROUTE 6. THE HISTORY WALK SKIPS ONE BODY PER HOP IF YOU ANCHOR ON THE OLDEST REVISION. ***
*** NEW, 22nd run, HIT LIVE. THIS IS A SILENT GAP GENERATOR IN THE ONE PROCEDURE EVERY RUN ***
*** BEGINS WITH. READ BEFORE WALKING crawl-state.                                          ***
*** ====================================================================================== ***
Appendix S says: take the OLDEST commit in `history.revisions` and call knomit_explain again with it.
That advances the window correctly, but it does NOT read every revision, and the shortfall is invisible.
MEASURED THIS RUN, every hop:
  explain(no commit)      -> revisions [4cce7781, 22649951, a5466f42]   more_available true
  explain(a5466f42)       -> revisions [a5466f42, 4feee885, a21ad1c0]
  explain(a21ad1c0)       -> revisions [a21ad1c0, 7a9ec830, 3bc37431]
  explain(3bc37431)       -> revisions [3bc37431, 0ac250fd, 3c6323cd]
  explain(3c6323cd)       -> revisions [3c6323cd, 8b9a768d]             more_available FALSE
EACH CALL RETURNS THE ANCHOR PLUS THE TWO NEXT-OLDER, AND ANCHORING ON THE OLDEST ADVANCES BY TWO. So
the MIDDLE entry of every listing is NAMED but its BODY IS NEVER FETCHED. Skipped this run without
intervention: 22649951, 4feee885, 7a9ec830, 0ac250fd.
WHY IT MATTERS RATHER THAN BEING A CURIOSITY: three of those four were same-run second writes and
losing them costs nothing — but **4feee885 WAS THE ENTIRE 19th RUN**, a distinct run with 4 URLs and
its own findings. I anchored past it and had to go back for it. Appendix S's step 4 warns that
consecutive calls overlap by one revision and to dedupe by hash; it does NOT warn that the middle
entry is never read, because the overlap it describes is the ANCHOR, not the middle.
THE RULE: **the revision LIST is the work list, not the anchor chain.** After each call, add all
returned commits to a to-read set; then read every one whose body you have not already seen, deduping
by hash. A run that only follows anchors reads roughly half the revisions and will report a walk it
did not perform. Cross-check available for free: the bodies self-identify by run number ("crawled:
<date> (Nth run)"), so a gap in the run-number sequence is the tell.

*** ====================================================================================== ***
*** ROUTE 4. THE TOOL ITSELF CAN INVENT THINGS. THE MOST IMPORTANT ENTRY IN THIS FILE FOR  ***
*** FACT QUALITY. 20th run; SCOPE WIDENED TWICE BY THE 21st. READ BEFORE WRITING ANY       ***
*** FIGURE, QUOTATION OR IDENTIFIER INTO ANY FACT.                                        ***
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
THREE FABRICATIONS IN ONE SENTENCE: (i) "out of 100" — a scale maximum the page never gives, which
would have let a reader convert the score into a probability; (ii) "across three runs of 150,000
queries each" — an entire baseline budget, invented, and it was the denominator the whole efficiency
comparison rested on; (iii) "queries" for the source's "steps". Call 1 also dropped "In one run",
turning a single observation into a general result.

*** THE 21st RUN WIDENED THE CLASS TWICE, AND NEITHER NEW CASE IS A NUMBER. ***
Same two-call pattern, two different pages, same run:
  (iv) A VERSION IDENTIFIER. On the AISI async-monitoring post the open-ended call reported the blue
       team's monitor model as "Claude 3.5 Sonnet"; the verbatim call returned "The Blue team builds
       monitoring systems using a weaker model (Claude 3.7 Sonnet)". A minor-version slip, entirely
       plausible, and it would have mis-specified the capability gap the whole experiment turns on.
  (v)  A PARAPHRASE ARRIVING INSIDE QUOTATION MARKS. On the LiteLLM post the open-ended call returned
       LiteLLM described as "a popular AI gateway. It provides a unified interface to LLMs and
       simplifies governance" — in quote marks. The page actually says "LiteLLM is an open-source
       proxy presenting a unified API over OpenAI, Anthropic, Azure OpenAI, Bedrock, and others."
SO THE RULE IS NOT "VERIFY NUMBERS". IT IS: ANY STRING YOU INTEND TO PUT IN QUOTATION MARKS, ANY
FIGURE, ANY THRESHOLD, AND ANY VERSION OR PRODUCT IDENTIFIER GOES THROUGH THE SECOND CALL.

*** 22nd-RUN ADDITION: THE SECOND CALL ALSO CATCHES THE OPPOSITE ERROR — AN OPEN-ENDED CALL
*** REPORTING SOMETHING AS ABSENT THAT IS PRESENT, WHICH PRODUCES AN UNDERCLAIM. ***
On the Echoverse post, an open-ended read left the impression that live-web transfer was described
qualitatively; a targeted call returned "The frozen model clears base on both, WebVoyager 66.5% to
71.5% and Online-Mind2Web 40.5% to 43.4%" and, asked directly whether the post says transfer was
unmeasured, answered NOT STATED. A fact had been carrying the "only qualitative" reading for weeks
AND had depressed its own confidence for it. So the second call is not only a fabrication filter, it
is an absence filter — and ASKING THE NEGATIVE QUESTION EXPLICITLY ("does the post state anywhere
that X was NOT measured?") is what separates "the page does not say it" from "I did not see it".

NOTE THE BIAS, because it is what makes this dangerous: every invention made the account MORE
COMPLETE AND MORE QUOTABLE. Fabrication here is not random noise, it is narrative gap-filling, so the
invented detail is exactly the one that makes a fact worth writing. It will pass a plausibility check
because plausibility is what produced it.

THE RULE, and it is cheap enough that there is no excuse:
  * NEVER write a number, a quotation, a named threshold or a version identifier into a fact from an
    OPEN-ENDED WebFetch.
  * Run a SECOND call on the same URL whose prompt says: "Quote VERBATIM the exact sentences that
    state each of these, or say NOT STATED if absent", enumerating each item you intend to use.
    The "or say NOT STATED" clause is load-bearing — it gives the model a licence to report absence
    instead of manufacturing presence.
  * Anything the second call marks NOT STATED does not go in the fact, and if the fact needs it, say
    in the fact that the source does not supply it.
  * IF YOU DID NOT ASK THE SECOND CALL ABOUT IT, YOU DO NOT HAVE IT. The 21st run dropped two
    figures on this basis; the 22nd dropped an entire worked example (a PowerPoint-exfiltration demo
    on the reasoning-traces paper) that the open-ended call described in detail and the verbatim call
    returned NOT STATED for. Omitting is cheaper than hedging.
  * CALIBRATION, so this is not read as "WebFetch is unreliable": the two-call pattern confirmed 7/7
    and 8/8 figures on two pages and 8/8 quoted strings on a third in the 20th run, 8/8, 6/6 and 8/8
    across three pages in the 21st, and in the 22nd 10/10 and 8/9 on one arXiv paper and 5/5 on the
    Echoverse post. The tool is accurate when the page states the thing. It invents when the page
    does NOT, and only the second call distinguishes those two cases.
  * THIS IS ALSO RETROSPECTIVE. When verifying an old fact, the detail most likely to be fabricated
    is the one that COMPLETES A SET — the remainder of a percentage, the range around a qualitative
    duration, the denominator of a ratio, the expected last step of a pipeline.

*** ====================================================================================== ***
*** ROUTE 5. READING AN INDEX AS A LIST IS ONE PLAIN WebFetch AND IT RETURNS THE WHOLE     ***
*** ARCHIVE. 21st run, and it is the cheapest high-yield call this file has added since    ***
*** the GitHub contents API.                                                               ***
*** ====================================================================================== ***
Appendix S and the 20th run's Finding 1 say a feed is UNREAD until someone has looked at its front
page AS A LIST and made a per-item keep/skip decision. The 21st run ran that test and discovered the
call is far more powerful than "the front page":
  WebFetch {url: "<feed index>", prompt: "List EVERY post visible on this index as a list: exact
    title, exact href/slug, and date, newest first. Do not summarise."}
MEASURED RESULTS, one call each, plain WebFetch, no browser, no gate:
  www.aisi.gov.uk/blog   -> 95 posts, complete archive back to 2023-09-07
  cognition.com/blog     -> 82 posts, complete archive back to 2024-03-12
  embracethered.com/blog -> 10 posts back to 2026-03-16
  microsoft.com/en-us/security/blog -> 12 posts (paginated; front page only)
These sites paginate for a human and serve the full list to this call. So "enumerate the back
catalogue" is ONE fetch, not a pagination crawl.
TWO CAUTIONS:
  * THE OUTPUT IS AN EXTRACTION, SO ROUTE 4 APPLIES. The tell that you are getting real hrefs rather
    than derived ones is a TITLE/SLUG MISMATCH. A list where every slug is a clean slugification of
    its title is the one to distrust.
  * A LIST IS NOT A READ. Record the keep/skip decisions in crawl-sources.

*** 5b. THE SAME CALL PULLS AN EXACT ASSET HREF OFF A PAGE, WHICH BEATS SEARCHING FOR IT.
*** NEW, 22nd run. ***
The AISI blog post naming a paper ("What_OpenClaw_learned_about_us") did not surface that paper via
WebSearch — the search returned the blog post itself plus unrelated OpenClaw papers. Asking the POST
for the link returned it exactly:
  WebFetch {url: "<post>", prompt: "Give me the EXACT href/URL of every link in this post that points
    to a paper, PDF or report. Quote the link text and the full URL verbatim."}
  -> https://cdn.prod.website-files.com/663bd486.../69e63511..._What_OpenClaw_learned_about_us%20(2).pdf
That URL is a Webflow CDN hash path — unguessable and unsearchable, because it is not indexed under
the paper's title. RULE: when a post names an artifact, ASK THE POST FOR THE HREF before searching
for the artifact. Route 1b (WebSearch + allowed_domains) is for a slug on a site that publishes
pages; it does not find hash-named assets on a CDN.
And the same call is the cheapest way to establish an absence: asked what mitigations the post
recommends, it answered NOT STATED and quoted the post deferring to the paper — which is what made
the paper worth fetching.
HOSTING NOTE: cdn.prod.website-files.com serves PDFs to a plain `curl -sL -A "Mozilla/5.0"` with no
gate, no Referer, no cookie. Percent-encoding in the filename (%20) passes through fine. Confirm with
`file` and fingerprint with `pdfinfo` as per route 2 regardless.

*** FETCH ROUTES. READ BEFORE CALLING ANYTHING BLOCKED. ***

1. openai.com/index/<slug> RETURNS HTTP 403 TO WebFetch. IT READS FINE IN A REAL BROWSER.
   THE RULE: the browser server available depends on how the job was invoked, not on the job identity.
   DO NOT hardcode either name. Check what is actually present, then use it:
     mcp__claude-in-chrome__navigate {url}        -> returns a tabId
     mcp__claude-in-chrome__get_page_text {tabId} -> full article text
     mcp__browser__browser_navigate {url}  then  mcp__browser__browser_snapshot
   Both are read-only navigation + text extraction and both cracked openai.com. The server must run
   REAL Chrome, not headless Chromium — headless Chromium gets a Cloudflare "Just a moment..."
   interstitial. Plain curl also 403s. Do NOT record openai.com as paywalled or dead — it is
   WebFetch-403, browser-readable. VERIFIED across runs 14-20 on thirteen-plus posts, and AGAIN
   2026-08-21 (22nd run) on two posts back to back in one tab. This route is settled.
   *** AND THE BROWSER ROUTE HAS A QUALITY ADVANTAGE OVER WebFetch THAT ROUTE 4 MAKES DECISIVE: ***
   `get_page_text` returns the RAW ARTICLE TEXT with no model in the loop, so figures transcribed
   from it are transcriptions, not extractions, and cannot be fabricated. Where a page is
   browser-readable AND number-heavy, prefer the browser over WebFetch even when WebFetch works.
   The 22nd run verified nine separate figures across two facts this way with no second call needed —
   raw text makes route 4's two-call discipline unnecessary, which is a real saving on number-heavy pages.
   NOTE ON navigate ERGONOMICS (17th run, RE-CONFIRMED 18th-20th and 22nd): calling `navigate`
   STANDALONE with no tabId auto-creates the tab group and returns the tabId in the same result. To
   read several posts in one run, PASS THE SAME tabId to each subsequent navigate — one tab, N
   navigations, then tabs_close_mcp once at the end.
   NOTE THE HOST BOUNDARY: this is openai.com ONLY. developers.openai.com and cdn.openai.com are NOT
   403 — the API guides read fine with plain WebFetch, and cdn.openai.com PDFs download with plain
   curl -A. Do not spend a browser navigation on either.
   *** 22nd-RUN NOTE ON THE "Keep reading" FOOTER: it is a cheap DATE oracle even when you do not
   read the linked posts. Two openai.com posts read this run both listed "The Defender's Window —
   Security — Aug 17, 2026", which pinned the date of a slug the 21st run had found with no date
   attached. Two independent footers agreeing is decent evidence for a date; it remains a recency
   feed, not a category index (see the falsified hypothesis in 1b).

1b. *** CHEAPEST WAY TO RESOLVE AN UNKNOWN SLUG: WebSearch WITH allowed_domains. 14th run. ***
   Guessed slugs have now 404'd on cognition, strands, adk, openai AND anthropic.
     WebSearch {query: "<exact article title>", allowed_domains: ["openai.com"]}
   VALIDATED SIX TIMES (runs 14-20), including: the ANS resource slug which contains a TYPO nobody
   would guess ("al" for "AI"); six previously-unknown openai.com posts in one search; and the
   anthropic.com watermark post whose real slug is SHORTER than its title.
   *** VALIDATED A SEVENTH TIME, 22nd run, ON arXiv: *** a paper known only by title resolved in one
   search to arxiv.org/abs/2608.09867, and the result set carried the HTML full-text URL
   (/html/<id>v1) which is what you actually want — /abs/ gives only the abstract.
   *** BUT NOTE THE 22nd RUN'S NEGATIVE RESULT, WHICH BOUNDS THIS ROUTE: *** WebSearch did NOT find
   the AISI OpenClaw paper, because it is a hash-named PDF on a Webflow CDN rather than a published
   page. Search finds documents that are indexed under their titles. For an artifact LINKED FROM a
   page you already have, use route 5b and ask the page for the href.
   *** 21st-RUN NOTE: ROUTE 5 IS NOW USUALLY CHEAPER THAN THIS FOR DISCOVERY. *** Use route 5 for
   sweeps, 1b for a specific unknown slug or a 404 recovery, 5b for a linked asset.
   CALIBRATION ON THE "Keep reading" FOOTER, CORRECTED 19th run AND FALSIFIED 20th: it is a plain
   RECENCY feed of the three newest posts, NOT category-scoped. Recorded as a falsified hypothesis
   rather than deleted, so the next run does not re-derive the category theory from another small sample.

*** 3. modelcontextprotocol.io UNREACHABLE -> READ THE SPEC REPO ON GITHUB. 16th run. ***
   On 2026-08-12 the host refused connections outright. THE HOST WAS BACK UP on 08-14, 08-15 and
   08-17 — that outage was transient. The repo route below remains preferred anyway, because it is
   cheaper and enables diffing.
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
   Listing a single directory is also cheap:
     curl -sL -A "Mozilla/5.0" \
       "https://api.github.com/repos/modelcontextprotocol/modelcontextprotocol/contents/docs/specification"
   *** THE TRIPWIRE HAS A ZERO-FETCH FORM. *** That last call lists one directory per released
   revision (2024-11-05, 2025-03-26, 2025-06-18, 2025-11-25, 2026-07-28, draft). A new revision is a
   new directory. Cheapest possible check and it does not depend on the website being up at all.
   UNCHANGED THROUGH THE 22nd RUN (twelve consecutive).

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
     through 2025-11-25 -> docs/specification/<rev>/basic/authorization.mdx  (ONE FILE)
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
   Guard run on 45 files (19th) and 227 files (20th), 0 hits, and it FIRED on a real case first.

   *** 3d. THE MCP REPO HAS A SEPARATE TOP-LEVEL schema/ TREE. A docs/-SCOPED SWEEP MISSES IT. ***
     schema/<rev>/schema.json (~4000 lines), schema.ts (~2600), schema.mdx
   When establishing that something is ABSENT from a revision, enumerate on the REVISION DATE:
     grep -oE '"path":"[^"]*<rev>[^"]*\.(mdx|json|ts)"' tree.json | sed 's/"path":"//;s/"$//'
   REVISION SIZES, MEASURED: 2025-11-25 = 41 files; 2026-07-28 = 186 files.

   *** 3e. IN .mdx, NORMATIVE KEYWORDS ARE BOLDED — SO GREPPING A NORMATIVE SENTENCE FINDS NOTHING.
   The MCP spec writes every RFC 2119 keyword as markdown emphasis: `**MUST**`, `**MUST NOT**`.
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
Record the pdfinfo fingerprint (pages + CreationDate) for every PDF you read — the 21st run settled
id 50592 in one command, and "proven unchanged" is a stronger claim than "I re-read it".

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
*** (i)-(iii) are extraction artifacts; (iv) is in the source bytes; (v) is in the TOOL and is the
*** only one producing a confident POSITIVE; (vi) is in the SEARCH PROGRAM and is loud if you look.
*** ALWAYS grep the rarest SINGLE word, then read the lines — a fact's own central quotation can be
*** unfindable in the very document it came from (92dc0441, where the wrap falls mid-phrase).
*** PDF TABLES EXTRACT WITH THEIR COLUMNS SHUFFLED — DO NOT CITE ONE (16th run). ***
*** BUT A TABLE IS STILL SAFE TO COUNT (17th run). *** Interleaving destroys the PAIRING, not the
cells, so `grep -oE '<TOKEN>' | sort | uniq -c` gives a trustworthy FREQUENCY. State in the fact which
of the two you relied on — frequency is publishable, pairing is not.
*** AND SOME PDF TABLES DO EXTRACT ROW-FAITHFULLY — CHECK BEFORE GIVING UP (18th run). ***
Narrow tables with short cells serialise cleanly; wide tables with multi-line prose cells interleave.
Look at ten lines of the extract before deciding which regime you are in.
*** AND WHEN THE TABLE IS THE WIDE KIND, PAIR ON CONTENT INSTEAD OF POSITION (19th run). ***
USE A DISCRIMINATING TOKEN, AND SAY IN THE FACT THAT THE PAIRING IS SEMANTIC RATHER THAN POSITIONAL.
*** 22nd-RUN VARIANT, AND IT IS THE EASIEST CASE TO GET RIGHT: a small two-column table can extract
*** as TWO SEPARATE VERTICAL RUNS — all the labels, then all the values. The AISI OpenClaw paper's
*** technical-details table came out that way, and the sixth row's label/value pair landed AFTER the
*** first five values, so a `paste - -` would have desynchronised. It was still safe to use because
*** every value self-identifies ("mitmproxy 12.2.1 as sidecar" can only be the Proxy row). That is
*** semantic pairing on a NARROW table — note it in the fact and move on.
*** AND A DOCUMENT'S PROSE AND ITS NUMBERS CAN SIT 2,300 LINES APART (21st run). *** After writing a
fact from a long PDF's narrative, grep the WHOLE extract for the campaign/product name again and read
every other hit — the appendix tables are where the numbers are.
BROWSER CAVEATS: on builder.aws.com the FIRST get_page_text after a navigate SOMETIMES returns a stub
ending in 'Loading article'; call it again. Never conclude 'blocked' from one empty call.
To pull links/hrefs off an index use javascript_tool with a querySelectorAll expression — `find`
returns element refs but NOT hrefs. (BUT TRY ROUTE 5/5b FIRST: a plain WebFetch asking for the index
as a list, or for a page's asset hrefs, needs no browser at all.)
NOTE: large learn.microsoft.com and platform.claude.com pages exceed WebFetch's inline limit and are
persisted to a file on disk; just Read the path returned, or grep it. Likewise a broad knomit_query
can exceed the tool-result limit — use limit<=25.
AND knomit_explain ON crawl-state.md NOW EXCEEDS IT TOO (51.5KB at the 15th run, 54.2KB by the 21st,
56.8KB at the 22nd). That is expected, not an error — the tool result names the path; just Read it.
Do not retry the call. THE PERSISTED FILE IS ONE LINE OF JSON, so `Read` truncates and paginating it
is useless. 22nd-RUN TIP, simpler than the 21st's python recipe and it needs no interpreter:
  cut -c1-6000 <file>        # head of the body
  cut -c54000-57000 <file>   # the tail, where `history.revisions` lives
Two `cut` calls got the body opening and the full history object out of a 56KB blob. (python3 IS
available in this job's Bash despite an older note in Appendix S; Write and Edit are what is denied.)
*** knomit_query sort=recent IS ORDERED BY LAST TOUCH, NOT BY CREATION (18th run). ***
An update bumps a fact to the front, so the TAIL of a sort=recent walk is the set of facts LEAST
RECENTLY VERIFIED. Reaching it costs ~15k tokens per page at limit=25.
*** CHEAPER WAY TO FIND A FACT'S PATH WHEN YOU ONLY HAVE ITS SHORT ID (19th run). ***
knomit_query CANNOT search by id. Run a TOPICAL query aimed at what the fact is about — the id is the
filename stem, so it is visible in the `file` field of any matching row. 22nd-RUN CALIBRATION: this
works but is not reliable in one shot — two of four queued ids took three differently-angled queries
to surface, and one (af3acf92) never appeared at all. Budget two or three queries, and if an id will
not surface, substitute another fact at the same confidence rather than spending more.
*** AND THE CHEAPEST WAY TO PICK A STALENESS SAMPLE (20th and 21st runs). *** Every knomit_query
result row carries `committed_at` (a UNIX epoch, LAST-TOUCH) AND `refs` in its frontmatter. So the
topical queries you run anyway for the query-first rule hand you BOTH axes for free: sort rows by
`committed_at` for age, group them by identical `refs` for shared-ref. Reference points:
1785089xxx ≈ 2026-07-26 (first run), 1786817xxx ≈ 2026-08-15, 1787275xxx ≈ 2026-08-20,
1787357xxx ≈ 2026-08-21 (22nd run).
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
Cheapest possible check on your own method: read your claim's subject noun, then look at what you
actually grepped.
*** AND A TOKEN CAN SURVIVE A REVISION WHILE ITS MEANING DOES NOT (20th run). *** A POSITIVE grep is
as weak a form of evidence as a negative one when the claim is about SEMANTICS: read the hits, do not
count them.
