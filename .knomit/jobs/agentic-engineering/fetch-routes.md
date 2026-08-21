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
       Checklist item 9 (LANGUAGE BINDING AND VERSION) now has a fetch-layer cause, not just an
       author-layer one.
  (v)  A PARAPHRASE ARRIVING INSIDE QUOTATION MARKS. On the LiteLLM post the open-ended call returned
       LiteLLM described as "a popular AI gateway. It provides a unified interface to LLMs and
       simplifies governance" — in quote marks. The page actually says "LiteLLM is an open-source
       proxy presenting a unified API over OpenAI, Anthropic, Azure OpenAI, Bedrock, and others."
       This is the 56986e8f defect class (a paraphrase wearing quote marks) being manufactured BY THE
       TOOL rather than by the fact's author. It means the pack's oldest recurring defect can enter
       a fact without anyone paraphrasing anything.
SO THE RULE IS NOT "VERIFY NUMBERS". IT IS: ANY STRING YOU INTEND TO PUT IN QUOTATION MARKS, ANY
FIGURE, ANY THRESHOLD, AND ANY VERSION OR PRODUCT IDENTIFIER GOES THROUGH THE SECOND CALL.

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
    in the fact that the source does not supply it. "The source does not state the baseline budget,
    so the comparison cannot be quantified" is a publishable sentence and a better one.
  * IF YOU DID NOT ASK THE SECOND CALL ABOUT IT, YOU DO NOT HAVE IT. The 21st run dropped two
    figures on this basis (a geographic download breakdown, an attribution of AI-coauthored servers
    to one coding agent) purely because they were not on the verbatim list. Omitting is cheaper than
    hedging and leaves no half-sourced sentence for a later run to promote.
  * CALIBRATION, so this is not read as "WebFetch is unreliable": the two-call pattern confirmed 7/7
    and 8/8 figures on two pages and 8/8 quoted strings on a third in the 20th run, and 8/8, 6/6 and
    8/8 across three pages in the 21st. The tool is accurate when the page states the thing. It
    invents when the page does NOT, and only the second call distinguishes those two cases.
  * THIS IS ALSO RETROSPECTIVE. Two facts sampled in the 20th run's staleness pass carried invented
    figures of exactly this shape — a "~15%" variance remainder and a "(2-4 seconds)" latency range,
    both plausible, both absent from the source. The 21st run found a third variant in 7a4f9061: a
    quoted technical SCHEME ("chunked+XOR+gzip") that the fact had extended with a fourth step
    ("then base64") the source never names. When verifying an old fact, the detail most likely to be
    fabricated is the one that COMPLETES A SET — the remainder of a percentage, the range around a
    qualitative duration, the denominator of a ratio, the expected last step of a pipeline.

*** ====================================================================================== ***
*** ROUTE 5. READING AN INDEX AS A LIST IS ONE PLAIN WebFetch AND IT RETURNS THE WHOLE     ***
*** ARCHIVE. NEW, 21st run, and it is the cheapest high-yield call this file has added     ***
*** since the GitHub contents API.                                                         ***
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
catalogue" is ONE fetch, not a pagination crawl, and there is no excuse for a feed in the recurring
list to remain un-enumerated.
TWO CAUTIONS:
  * THE OUTPUT IS AN EXTRACTION, SO ROUTE 4 APPLIES. Treat the slugs as high-confidence but not
    certain. The tell that you are getting real hrefs rather than derived ones is a
    TITLE/SLUG MISMATCH: aisi.gov.uk returned `/blog/advancing-voice-ai-security-with-elevenlabs`
    for a post titled "Advancing AI voice security with ElevenLabs" (word order differs) and
    `/blog/ask-dont-tell-...-2` with a CMS dedup suffix. A list where every slug is a clean
    slugification of its title is the one to distrust.
  * A LIST IS NOT A READ. The point of the call is a per-item keep/skip decision, which you still
    have to make. Record the decisions in crawl-sources so the next run inherits them.

*** FETCH ROUTES. READ BEFORE CALLING ANYTHING BLOCKED. ***

1. openai.com/index/<slug> RETURNS HTTP 403 TO WebFetch. IT READS FINE IN A REAL BROWSER.
   CORRECTED AGAIN 2026-08-11 (14th run) — AND THE CORRECTION IS ABOUT WHICH BROWSER SERVER EXISTS.
   The 13th run's route named mcp__claude-in-chrome__*. The 13th run's own correction then said those
   "do not exist in this job" and mandated mcp__browser__*. BOTH CLAIMS ARE TOO ABSOLUTE. The 14th run
   ran with mcp__claude-in-chrome__* PRESENT and working first try on openai.com/index/*.
   THE RULE: the browser server available depends on how the job was invoked, not on the job identity.
   DO NOT hardcode either name. Check what is actually present, then use it:
     mcp__claude-in-chrome__navigate {url}        -> returns a tabId
     mcp__claude-in-chrome__get_page_text {tabId} -> full article text
     mcp__browser__browser_navigate {url}  then  mcp__browser__browser_snapshot
   Both are read-only navigation + text extraction and both cracked openai.com. The server must run
   REAL Chrome, not headless Chromium — headless Chromium gets a Cloudflare "Just a moment..."
   interstitial. Plain curl also 403s. Do NOT record openai.com as paywalled or dead — it is
   WebFetch-403, browser-readable. VERIFIED 2026-08-11 on four separate openai.com/index/ posts,
   AGAIN 2026-08-12 (15th run) on three more, AGAIN 2026-08-14 (17th run) on two more, AGAIN
   2026-08-15 (18th run), AGAIN 2026-08-15 (19th run) on THREE posts back to back, and AGAIN
   2026-08-17 (20th run) on /index/unlocking-self-improvement-gpt-red/, first try, no retries.
   Thirteen-plus posts across seven runs; this route is settled and needs no further re-confirmation.
   *** AND THE BROWSER ROUTE HAS A QUALITY ADVANTAGE OVER WebFetch THAT ROUTE 4 MAKES DECISIVE: ***
   `get_page_text` returns the RAW ARTICLE TEXT with no model in the loop, so figures transcribed
   from it are transcriptions, not extractions, and cannot be fabricated. Where a page is
   browser-readable AND number-heavy, prefer the browser over WebFetch even when WebFetch works.
   NOTE ON navigate ERGONOMICS (17th run, RE-CONFIRMED 18th, 19th and 20th): calling `navigate`
   STANDALONE with no tabId auto-creates the tab group and returns the tabId in the same result, so
   the documented tabs_context_mcp-then-create dance is not needed for a simple read. Navigate, then
   get_page_text. To read several posts in one run, PASS THE SAME tabId to each subsequent navigate —
   one tab, N navigations, no cleanup.
   NOTE THE HOST BOUNDARY: this is openai.com ONLY. developers.openai.com and cdn.openai.com are NOT
   403 — the API guides read fine with plain WebFetch, and cdn.openai.com PDFs download with plain
   curl -A. Do not spend a browser navigation on either.

1b. *** CHEAPEST WAY TO RESOLVE AN UNKNOWN SLUG: WebSearch WITH allowed_domains. NEW, 14th run. ***
   Guessed slugs have now 404'd on cognition, strands, adk, openai AND anthropic. The standing advice
   was "always pull the href off the index", which needs a browser. There is a cheaper first move:
     WebSearch {query: "<exact article title>", allowed_domains: ["openai.com"]}
   This resolved the Aug 7 post in ONE call, no browser, and surfaced THREE sibling posts nobody
   knew existed. Use it before spending a browser navigation. Then still pull hrefs off the page
   with javascript_tool for anything you intend to fetch — a querySelectorAll over a[href*="/index/"]
   returns slug + title + date together and is how the two Aug 10 posts were found.
   VALIDATED AGAIN TWICE, 15th run, and it is now the single highest-leverage call in this file:
     - one search on openai.com surfaced the Safe Url post, a linked cdn.openai.com PAPER, a
       Nov-2025 post nobody had seen, and a developers.openai.com guide — four new targets, one call;
     - two searches on genai.owasp.org resolved both wanted OWASP resource slugs exactly, and one of
       them returned a download id (52117) in the result snippet without any page fetch at all.
   The pattern worth generalising: search results carry SIBLING links, so a search aimed at a URL you
   already want is also the cheapest discovery sweep available. Prefer it over a feed index when you
   have a specific title in hand.
   VALIDATED A THIRD TIME, 16th run: one search resolved the ANS resource slug, which contains a TYPO
   nobody would guess — /resource/agent-name-service-ans-for-secure-al-agent-discovery-v1-0/ spells
   AI as "al". Guessing that slug was impossible; searching it took one call.
   VALIDATED A FOURTH TIME, 17th run: ONE search on openai.com returned SIX previously-unknown post
   URLs, and among them the CORRECT slug for the post the 13th run 404'd on by guessing — the real
   slug is /index/responding-next-frontier-critical-cyber-capabilities/ (the guess had inserted
   "to-the" and "of"). A 404 from a guessed slug is worth exactly one search, never a second guess.
   VALIDATED A FIFTH TIME, 19th run: the Codex Security post, whose slug was UNKNOWN, resolved in ONE
   search to /index/codex-security-now-in-research-preview/ — and the search result SNIPPETS alone
   already carried the three-stage architecture and the rollout scope, i.e. enough to confirm the
   post was worth the browser call before spending it.
   *** VALIDATED A SIXTH TIME ON A NEW HOST, 20th run — AND THE TRAP IS THE OBVIOUS-LOOKING SLUG. ***
   The anthropic.com/news index lists the post as "How Claude's text watermark works". The slug built
   from that title, /news/how-claudes-text-watermark-works, 404s. The real slug is
   /news/claude-text-watermark — SHORTER than the title and with a different noun form ("watermark"
   not "text watermark works"). One WebSearch with allowed_domains resolved it. Anthropic slugs are
   editorially shortened, so a title-derived guess is if anything LESS reliable there than on hosts
   that slugify mechanically. Same rule: one 404 from a guess, then search, never a second guess.
   *** 21st-RUN NOTE: ROUTE 5 IS NOW USUALLY CHEAPER THAN THIS FOR DISCOVERY. *** WebSearch remains
   the right tool when you have ONE title and need ONE slug. When you want the whole feed, route 5's
   index-as-list call returns every slug at once and returns them as hrefs rather than as search
   hits. Use route 5 for sweeps, 1b for a specific unknown slug or a 404 recovery.
   *** ALSO USE THE ARTICLE FOOTER — AND SEE THE CORRECTED CALIBRATION BELOW. *** openai.com posts
   carry a "Keep reading" block listing three sibling posts with titles and dates. get_page_text
   returns it, so reading one post yields three more candidate URLs for free.
   CALIBRATION, CORRECTED 19th run, AND THE 19th RUN'S HYPOTHESIS IS NOW FALSIFIED — SEE BELOW.
   The 18th run concluded the footer is a pure RECENCY feed, from a single observation. The 19th run
   revised that to **recency WITHIN THE POST'S PRIMARY CATEGORY**, from four observations, and
   explicitly asked the next run to test the prediction.
   *** TESTED 20th RUN. THE CATEGORY HYPOTHESIS DOES NOT HOLD. *** /index/unlocking-self-improvement-
   gpt-red/ is tagged **Safety / Publication** and its footer returned: Expanding Daybreak
   (**Security**, Aug 10), Ten advances in mathematics and theoretical computer science
   (**Publication**, Aug 1), How enabling two settings tripled our scores on ARC-AGI-3 (**Research**,
   Jul 29). Three different categories, only one of which the post carries, and they are in strict
   date order. That is consistent with PLAIN RECENCY (the 18th run's original reading) and not with
   category scoping. VERDICT: treat the footer as a cheap recency feed of the three newest posts,
   NOT as a category-scoped index, and do NOT rely on it to sweep security posts — use WebSearch with
   allowed_domains for that. Recorded as a falsified hypothesis rather than deleted, so the next run
   does not re-derive the category theory from another small sample.

*** 3. modelcontextprotocol.io UNREACHABLE -> READ THE SPEC REPO ON GITHUB. NEW, 16th run. ***
   On 2026-08-12 the host refused connections outright: WebFetch returned
   `connect ECONNREFUSED 76.76.21.21:443` on three separate paths, and `curl` timed out (exit 28,
   HTTP 000). Not a 403, not a block — the origin was down. Every other host that run was fine, so
   isolate before blaming the tool. THE HOST WAS BACK UP on 2026-08-14, 08-15 and 08-17 — that
   outage was transient, not a policy change. The repo route below remains preferred anyway, because
   it is cheaper and enables diffing.
   THE MIRROR IS THE SPEC ITSELF, not a copy: the site renders .mdx files straight out of
   github.com/modelcontextprotocol/modelcontextprotocol. This route is authoritative and it worked
   first try for six documents.
     # enumerate — the ONLY reliable way to find a page, because paths have moved (see below)
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
   revision (2024-11-05, 2025-03-26, 2025-06-18, 2025-11-25, 2026-07-28, draft). A new revision
   appears as a new directory. That is the cheapest possible check of the versioning tripwire and it
   does not depend on the website being up at all — prefer it. UNCHANGED THROUGH THE 21st RUN.

   *** PATH MAPPING — CORRECTED 2026-08-14 (17th run). THE 16th RUN'S VERSION WAS WRONG TWICE. ***
   The two tree prefixes are right:
     site /specification/<rev>/...   -> repo docs/specification/<rev>/...
     site /docs/<rev>/...            -> repo docs/docs/<rev>/...
   CORRECTION 1 — /docs/concepts/tools IS NOT GONE. The 16th run recorded it as dead. It answers
   HTTP 200 and REDIRECTS to https://modelcontextprotocol.io/specification/2026-07-28/server/tools.
   CORRECTION 2 — THE SUCCESSOR PAGE NAMED BY THE 16th RUN IS THE WRONG PAGE. The tool CONTRACT
   material lives in the SPECIFICATION tree at docs/specification/<rev>/server/tools.mdx, not at
   docs/docs/<rev>/learn/server-concepts.mdx (grepped for `annotations`, `outputSchema`,
   `structuredContent`, `isError`: zero hits).
   THE LESSON, and it generalises beyond MCP: a redirect target is evidence, a guessed successor is
   not. Confirm a page move by GREPPING THE NEW PAGE FOR THE CONTENT, not by matching titles or
   plausible paths.
   CAVEAT TO STATE IN ANY FACT BUILT THIS WAY: `main` is the live editing branch, not a release tag.
   Frozen revision directories should be stable, but say in the fact that the text came from the repo
   and that exact strings want re-confirming against the rendered page.

   *** 3b. A PAGE CAN BE A FILE IN ONE REVISION AND A DIRECTORY IN ANOTHER — OR IN A DIFFERENT TREE
   *** ENTIRELY. Do NOT build a predecessor path by substituting the revision date into a current
   *** path. TWO worked examples now, and the second (20th run) is a different shape from the first.
   AUTHORIZATION — file becomes directory:
     2025-03-26 / 2025-06-18 / 2025-11-25 -> docs/specification/<rev>/basic/authorization.mdx  (ONE FILE)
     2026-07-28 / draft                   -> docs/specification/<rev>/basic/authorization/       (A DIRECTORY of
                                             index.mdx, security-considerations.mdx,
                                             client-registration.mdx, authorization-server-discovery.mdx)
   VERSIONING — TWO DIFFERENT PAGES WITH THE SAME NAME IN TWO DIFFERENT TREES (20th run):
     docs/docs/<rev>/learn/versioning.mdx          EXISTS FOR EVERY REVISION (2024-11-05 onward). A
                                                   short conceptual page about revision identifiers.
     docs/specification/<rev>/basic/versioning.mdx EXISTS ONLY FOR 2026-07-28 AND draft. The long
                                                   normative page: negotiation, extensions, the
                                                   dual-era compatibility matrix.
   So `docs/specification/2025-11-25/basic/versioning.mdx` 404s, and the naive conclusion — "the
   versioning page is new" — is HALF RIGHT in a way that will produce a wrong fact: the CONCEPT page
   has always existed, a normative page was ADDED to the specification tree at 2026-07-28. Diff the
   learn/ page across revisions to see what actually changed, and treat the specification/ page as
   new material. ALWAYS resolve both paths out of tree.json rather than by string substitution.

   *** 3c. THE 404 THAT SILENTLY BECOMES A FALSE "ENTIRELY NEW IN THIS REVISION" FINDING. 18th run. ***
   THIS IS THE SHARPEST TRAP IN THIS FILE AND IT MANUFACTURES VERSION-ATTRIBUTION DEFECTS.
   `raw.githubusercontent.com` answers a missing path with **HTTP 404 whose BODY is the literal text
   `404: Not Found`** — and `curl -sL -o file` WRITES THAT BODY TO THE FILE and exits 0. The file
   exists, `ls` looks fine, and `diff old new` then reports that every line of the new revision was
   added. Read naively that is exactly the shape of "this entire section is new in revision X".
   THE GUARD, cheap and mandatory before any revision diff:
     wc -l *.mdx                      # a 0- or 1-line .mdx is a 404, not a short page
     grep -c "404: Not Found" out.mdx  # must be 0
   19th-RUN NOTE: guard run on all 45 files fetched, 0 hits every time.
   20th-RUN NOTE: guard run on 227 files (41 of revision 2025-11-25 + 186 of revision 2026-07-28),
   0 hits, AND IT FIRED ON A REAL CASE FIRST — the naive `docs/specification/2025-11-25/basic/
   versioning.mdx` came back as a 0-line file with one "404: Not Found" hit, which is what sent the
   run to tree.json and produced finding 3b above. The guard is not ceremony; it converts a silent
   wrong answer into a signpost.

   *** 3d. THE MCP REPO HAS A SEPARATE TOP-LEVEL schema/ TREE. A docs/-SCOPED SWEEP MISSES IT. ***
   Revision content does NOT all live under docs/. Each released revision also has:
     schema/<rev>/schema.json   (the normative JSON Schema, ~4000 lines)
     schema/<rev>/schema.ts     (the TypeScript source of truth, ~2600 lines)
     schema/<rev>/schema.mdx
   When establishing that something is ABSENT from a revision, enumerate on the REVISION DATE, not on
   a docs/ prefix:
     grep -oE '"path":"[^"]*<rev>[^"]*\.(mdx|json|ts)"' tree.json | sed 's/"path":"//;s/"$//'
   REVISION SIZES, MEASURED — they are NOT comparable, so budget accordingly:
     2025-11-25 =  41 files   (confirmed 19th run, re-confirmed 20th)
     2026-07-28 = 186 files   (measured 20th run)
   Fetching all 41 is a few seconds. Fetching all 186 is still one shell loop and well under a minute,
   and the 20th run did exactly that to settle a modal-strength question — there is no reason to run
   a narrower sweep on either revision.

   *** 3e. IN .mdx, NORMATIVE KEYWORDS ARE BOLDED — SO GREPPING A NORMATIVE SENTENCE FINDS NOTHING.
   *** 19th run. A FOURTH INDEPENDENT MECHANISM FOR "A NEGATIVE GREP IS NOT PROOF OF ABSENCE".
   The MCP spec writes every RFC 2119 keyword as markdown emphasis: `**MUST**`, `**MUST NOT**`,
   `**SHOULD**`. So the sentence a reader would quote does not exist as a literal string in the file.
   ISOLATED CLEANLY, same file, same run:
     grep -c "MUST NOT assume that credentials"        asd-2026.mdx  -> 0   (looks like absence)
     grep -c "assume that credentials"                 asd-2026.mdx  -> 1   (it is there)
   RULES:
     * NEVER let a search term span a normative keyword. Grep the clause on ONE SIDE of the MUST.
     * The failure is silent and total — zero hits, no warning.
     * Same family as the pdftotext traps below, but a DIFFERENT cause (source markup, not
       extraction), so it survives even when the file is clean UTF-8 text you downloaded yourself.
     * It also breaks `diff`-based reasoning if you pre-filter lines by a normative phrase.

2. OWASP PDF DOWNLOADS ARE GATED ON THE USER-AGENT. NOTHING ELSE. `-A` IS THE WHOLE FIX.
     curl -sL -A "Mozilla/5.0" -o out.pdf "https://genai.owasp.org/download/<id>/?tmstv=<epoch>"
     file out.pdf     # MUST say "PDF document". "HTML document" = the default curl UA went out.
     pdftotext out.pdf out.txt      # then Read out.txt
   ISOLATED A/B, 2026-08-11, same URL, four requests back to back:
     bare curl                  -> HTML  (821KB, <title> "No Access - OWASP Gen AI Security Project")
     -A only                    -> PDF   122pp, 2.4MB, 228KB extracted text
     Referer only               -> HTML
     -A + Referer, NO cookies   -> PDF
   THIS SOURCE HAS NOW BEEN MISDIAGNOSED THREE TIMES, EACH BY A RUN THAT SUCCEEDED WITHOUT
   ISOLATING THE VARIABLE:
     11th run   "gated PDF, needs a form"          -> wrong; no form exists
     13th run   "gated on a Referer header"        -> wrong; Referer alone returns HTML
     14th pass  "needs a wp-dlm session cookie"    -> wrong; an EMPTY cookie jar downloads fine
   WHEN A FETCH FINALLY WORKS, DROP ONE FLAG AT A TIME BEFORE RECORDING THE RECIPE.
   The tmstv token is NOT an expiring nonce — 1754459367 was recorded 2026-08-05 and still worked
   2026-08-20, FIFTEEN DAYS LATER. Ten-for-ten across seven runs on `-A` alone.

2b. GETTING THE OWASP DOWNLOAD ID — THE TWO-STEP, CONFIRMED 15th, 16th AND 18th RUNS.
     (i)  WebFetch https://genai.owasp.org/resource/<slug>/ asking for "the direct PDF download URL
          if present in the page HTML (look for links containing /download/)". The resource PAGE is
          NOT UA-gated — plain WebFetch reads it and returns the full URL including ?tmstv=.
     (ii) curl that URL with -A per route 2.
   Only the DOWNLOAD endpoint is gated, not the resource page.
   18th-RUN BONUS: step (i) also returns the PUBLICATION DATE, the cheapest staleness check on a PDF
   you have already read. Pair it with `pdfinfo <file> | grep -i 'pages\|creationdate'` after download.

*** 2c. `file` REPORTS A PDF PAGE COUNT AND IT CAN BE WRONG. USE `pdfinfo`. 19th run. ***
  file masec.pdf     -> "PDF document, version 1.5, 3 pages"     WRONG
  pdfinfo masec.pdf  -> "Pages: 8"                                CORRECT
Same file, same run, no re-download. A run doing a staleness check with `file` would have
manufactured a "THE SOURCE CHANGED" finding on an unchanged document. `file` is still the right tool
for the ONE question route 2 asks it ("is this a PDF or the HTML error page"). It is not a source of
page counts. Never compare a `file` count against a `pdfinfo` count recorded earlier, or vice versa.
21st-RUN NOTE: the pdfinfo fingerprint (pages + CreationDate) settled the staleness question on
id 50592 in one command — 139 pages, CreationDate 2026-06-01, matching what the 12th run recorded.
That is three facts re-verified against a document PROVEN unchanged, which is a much stronger
statement than "I re-read it and it looked the same". Record the fingerprint for every PDF you read.

The 12th run's WebFetch route still works and needs no headers — keep it as the fallback:
  1. WebFetch the RESOURCE PAGE asking for "the direct PDF download URL if present in the page HTML".
  2. WebFetch that download URL. It REPLIES that the content is unreadable binary — ignore that;
     the same tool result ends with "[Binary content (application/pdf, N MB) also saved to <path>]".
  3. Parse that path with pdftotext, writing a .txt; read the .txt in page slices.
pypdf caveats that still hold: the true page count can exceed what the Read tool advertises
(AIUC-1 announced 15pp, is 55); Read's `limit` counts LINES and one PDF page is one very long line;
slide-deck PDFs lose word spacing but stay readable.
PDF NAVIGATION TIP (15th run): on a long extracted .txt, `grep -n` for numbered section headings
first and read targeted slices. Reading linearly wastes the budget on licence boilerplate and
bullet-list control checklists that are below this pack's altitude bar.
SECOND PDF TIP (16th run): `grep -c` for a distinctive token is a ZERO-COST NEGATIVE TEST — BUT SEE
THE FORM-FEED RULE BELOW BEFORE TRUSTING ANY ANCHORED NEGATIVE.

*** 2d. ugrep REJECTS `.{0,N}` CONTEXT PATTERNS ON THIS MACHINE. USE -n PLUS sed. 21st run. ***
The idiom `grep -o -i ".\{0,90\}<term>.\{0,90\}"` for keyword-in-context fails on the OWASP extracts
with `ugrep: error: error at position N ... exceeds complexity limits`, because ugrep expands the
bounded-repeat over multibyte character classes. It fails LOUDLY, which is the good news, but a run
that mistakes the error for "no matches" manufactures a false absence. THE WORKING IDIOM:
  grep -n -i -- "<term>" file.txt        # get line numbers
  sed -n '<start>,<end>p' file.txt       # read the surrounding lines
Also note `--` before the pattern: several useful search terms begin with a digit or a dash.

*** THE FORM-FEED RULE. 18th-run review pass. ***
*** pdftotext EMITS \f (0x0C) AT EVERY PAGE BREAK AND PREPENDS IT TO THE FIRST TOKEN OF THE NEXT
*** PAGE. SO ANY ^-ANCHORED PATTERN SILENTLY MISSES EXACTLY ONE ITEM PER PAGE BOUNDARY.
Confirmed with `od -c`. Consequences:
  grep -E "^ASI[0-9]{2}$"   -> 9 of 10 rows. Wrong, and plausible-looking.
  grep -xE "ASI[0-9]{2}"    -> 9 of 10. Same failure; -x is an anchor too.
  grep -oE "ASI[0-9]{2}"    -> 10 of 10. UNANCHORED IS IMMUNE.
RULES:
  * For COUNTING over an extract, always use unanchored `grep -o`.
  * For a NEGATIVE test, an anchored miss is not absence.
  * The undercount is SYSTEMATIC: always the first match on each page, one per boundary.
  * `paste - -` pairing over an anchored grep desynchronises at the first page break.
*** SIX MECHANISMS NOW — A NEGATIVE OR WRONG RESULT ARRIVES FOR SIX INDEPENDENT REASONS (21st run):
***   (i) pdftotext line-wrapping splits a multi-word phrase across lines;
***  (ii) pdftotext hyphen-breaking splits a single token ("communica-\ntion");
*** (iii) pdftotext form feeds defeat ^-anchors, one miss per page;
***  (iv) MARKDOWN EMPHASIS in .mdx sources breaks any phrase spanning a **MUST** (route 3e);
***   (v) AN OPEN-ENDED WebFetch INVENTS THE DETAIL rather than reporting its absence (route 4);
***  (vi) NEW — THE GREP ITSELF ERRORS OUT and the error is mistaken for zero matches (route 2d).
*** (i)-(iii) are extraction artifacts; (iv) is in the source bytes; (v) is in the TOOL and is the
*** only one producing a confident POSITIVE; (vi) is in the SEARCH PROGRAM and is loud if you look.
*** MECHANISM (i) FIRED AGAIN IN THE 21st RUN AND IS WORTH THE WARNING: the quotation 92dc0441 is
*** built on, "It streamlines it, by auto-approving...", is UNFINDABLE by grepping for itself — the
*** wrap falls between "streamlines" and "it". A fact's own central quotation can be unsearchable in
*** the very document it came from. ALWAYS grep the rarest SINGLE word, then read the lines.
*** PDF TABLES EXTRACT WITH THEIR COLUMNS SHUFFLED — DO NOT CITE ONE (16th run). ***
Column interleaving pairs rows with descriptions belonging to other rows. If a claim rests only on a
table cell, either confirm it against the document's prose or say in the fact that you did not.
*** BUT A TABLE IS STILL SAFE TO COUNT (17th run). *** Interleaving destroys the PAIRING, not the
cells, so `grep -oE '<TOKEN>' | sort | uniq -c` over a table region gives a trustworthy FREQUENCY.
State in the fact which of the two you relied on — frequency is publishable, pairing is not.
*** AND SOME PDF TABLES DO EXTRACT ROW-FAITHFULLY — CHECK BEFORE GIVING UP (18th run). ***
Narrow tables with short cells serialise cleanly; wide tables with multi-line prose cells interleave.
Look at ten lines of the extract before deciding which regime you are in.
CAVEAT: a row-faithful table is still cut by page-break form feeds and by repeated
`genai.owasp.org / Page N` footers landing MID-TABLE. Read such a region with Read, not anchored grep.
*** AND WHEN THE TABLE IS THE WIDE KIND, PAIR ON CONTENT INSTEAD OF POSITION (19th run). ***
USE A DISCRIMINATING TOKEN, AND SAY IN THE FACT THAT THE PAIRING IS SEMANTIC RATHER THAN POSITIONAL.
*** AND EXPECT A SOURCE TO NAME THE SAME THING TWICE (19th run). *** Before recording that a document
does not discuss X, grep the SHORTEST DISTINCTIVE STEM, not the full phrase.
*** AND A DOCUMENT'S PROSE AND ITS NUMBERS CAN SIT 2,300 LINES APART (NEW, 21st run). *** 7bd6c6c9
was written from OWASP 50592's narrative section on skill poisoning (extract line ~1160) and missed
the prevalence figure for the same campaign, which lives in the personal-agents appendix (line 3473).
A fact built from a document's NARRATIVE is systematically missing that document's QUANTITIES. After
writing from a long PDF, grep the whole extract for the campaign/product name again and read every
other hit — the appendix tables are where the numbers are.
*** PDF LINE WRAPS DEFEAT grep IN BOTH DIRECTIONS (17th run). *** When a phrase you expect is
missing, re-grep on its RAREST SINGLE WORD with context flags before concluding anything.
BROWSER CAVEATS: on builder.aws.com the FIRST get_page_text after a navigate SOMETIMES returns a stub
ending in 'Loading article'; call it again. Never conclude 'blocked' from one empty call.
To pull links/hrefs off an index use javascript_tool with a querySelectorAll expression — `find`
returns element refs but NOT hrefs. (BUT TRY ROUTE 5 FIRST: a plain WebFetch asking for the index as
a list returned complete archives on three separate hosts in the 21st run, no browser needed.)
NOTE: large learn.microsoft.com and platform.claude.com pages exceed WebFetch's inline limit and are
persisted to a file on disk; just Read the path returned, or grep it. Likewise a broad knomit_query
can exceed the tool-result limit — use limit<=25.
AND knomit_explain ON crawl-state.md NOW EXCEEDS IT TOO (15th run: 51.5KB, persisted to a file;
54.2KB by the 21st). That is expected, not an error — the tool result names the path; just Read it.
Do not retry the call. 21st-RUN TIP: the persisted file is ONE LINE of JSON, so `Read` truncates and
paginating it is useless. Pipe it through `python3 -c "import json,sys; ..."` to print `body` and
`history` separately, then read the resulting text file with sed slices. That turns a 54KB blob into
four cheap reads. (python3 IS available in this job's Bash despite an older note in Appendix S; the
Write and Edit tools are the ones that are denied.)
*** knomit_query sort=recent IS ORDERED BY LAST TOUCH, NOT BY CREATION (18th run). ***
An update bumps a fact to the front, so the TAIL of a sort=recent walk is the set of facts LEAST
RECENTLY VERIFIED — the right staleness target. Reaching it costs ~15k tokens per page at limit=25.
*** CHEAPER WAY TO FIND A FACT'S PATH WHEN YOU ONLY HAVE ITS SHORT ID (19th run). ***
knomit_query CANNOT search by id. Run a TOPICAL query aimed at what the fact is about — the id is the
filename stem, so it is visible in the `file` field of any matching row.
*** AND THE CHEAPEST WAY TO PICK AN EARLIEST-COMMITTED SAMPLE (NEW, 20th run). *** Every
knomit_query result row carries `committed_at` in its frontmatter as a UNIX epoch, and it is the
LAST-TOUCH timestamp. So a handful of ordinary topical queries — run for other reasons anyway — hands
you the age of every fact they return, for free. Sort the ids you have seen by `committed_at`, drop
the ones already in the verification pool, and you have an earliest-committed sample WITHOUT paging
sort=recent at all. The 20th run picked all five staleness targets this way at zero marginal cost.
Reference points: 1785089xxx ≈ 2026-07-26 (first run), 1786817xxx ≈ 2026-08-15 (19th run),
1787275xxx ≈ 2026-08-20 (21st run).
*** AND THE SAME ROWS GIVE YOU A SHARED-REF SAMPLE FOR FREE TOO (NEW, 21st run). *** The `refs`
array is in the same frontmatter. So one topical query yields BOTH axes at once: sort its rows by
`committed_at` for the age axis, and group them by identical `refs` entries for the shared-ref axis.
The 21st run picked five facts across exactly TWO source documents this way, which meant two fetches
covered the whole sample — and because one of those was a PDF with a stable fingerprint, three of the
five were verified against a document proven byte-stable rather than merely re-read.
*** THE `grep` ON THIS MACHINE IS ugrep 7.5.0, NOT GNU grep (18th run). ***
If a grep behaves unexpectedly, check `grep --version` before concluding anything about the DATA.
See route 2d for the specific incompatibility that has actually bitten.
The Bash tool's working directory PERSISTS between calls — prefer absolute paths or re-`cd` each call.
*** BUILDERS' LIBRARY — SOME ARTICLES ARE VIDEO-ONLY ***
Confirmed video-only, no prose body, DO NOT RE-FETCH:
  amazons-approach-to-failing-successfully   | 3F05J4fjklUZCE7kjuIp6LaTacl
  beyond-five-9s-lessons-from-our-highest-available-data-planes | 3F073j4jJOsSRTDlQM3eiZxkFLm
Budget one cheap fetch per article and abandon if the text ends right after the byline.

*** VERIFICATION TECHNIQUE, NOT A FETCH ROUTE, BUT IT LIVES HERE BECAUSE IT IS A RECIPE (16th run) ***
DIFF TWO REVISIONS OF THE SAME SPEC PAGE. Where a source is versioned and mirrored in git, the
staleness pass stops being "re-read and hope you notice" and becomes a diff:
  curl the <old-rev> and <new-rev> copies of the page, then `diff a b`
On the MCP security page this yielded, in one pass: a heading rename that CONFIRMED a fact's
prediction, a MUST downgraded to SHOULD that CORRECTED the same fact, a new subsection that
contradicted another fact's title, and three wholly new attack sections.
CALIBRATION (17th run): the same technique on learn/server-concepts.mdx across two revisions produced
a THREE-LINE diff. A near-empty diff is a REAL and useful result — it says the page is stable.
CALIBRATION (20th run): diffing docs/docs/<rev>/learn/versioning.mdx across 2025-11-25 -> 2026-07-28
is the model case — a 51-line page, a ~25-line diff, and the diff IS the finding: session-scoped
"**MUST** agree on a single version" replaced by per-request declaration plus a named error type.
Where a concept page and a normative page both exist, DIFF THE CONCEPT PAGE (small, stable, every
revision) TO LOCATE THE CHANGE, then READ THE NORMATIVE PAGE for its force.
*** FIVE HARD PRECONDITIONS ON THIS TECHNIQUE, ALL LEARNED THE HARD WAY. ***
  (a) RESOLVE BOTH PATHS FROM tree.json. Never substitute a revision date into a path — see 3b.
  (b) VERIFY BOTH FILES ARE REAL BEFORE DIFFING. A 404 body diffs as "all new" — see 3c.
  (c) DIFF THE IMMEDIATE PREDECESSOR, NOT A CONVENIENT OLDER ONE. A two-revision jump cannot
      distinguish "new" from "moved", and "new in revision X" is a claim a reader will act on.
  (d) BOUND THE REGION ON THE FOLLOWING HEADING, NOT ON EOF. Use
      `awk '/^## Target/{f=1} /^## NextHeading/{f=0} f'`. An over-wide range ADDS phantom findings.
  (e) A SPLIT DUPLICATES RULES, AND THE COPIES CAN DIFFER IN MODAL STRENGTH. When one page becomes
      four, a rule that straddles the seam is often RESTATED on the topic page at a weaker modality.
      Before recording any weakening, grep EVERY page of the new revision and cite the strongest.
  (f) *** 20th run — THE MIRROR OF (e): A PAGE THAT DELEGATES A RULE LOSES ITS FORCE IN THE
      SUMMARY. *** Where (e) is about a rule RESTATED more weakly, (f) is about a rule NOT RESTATED
      AT ALL. MCP's basic/versioning.mdx gives a compatibility matrix and then says the detection
      mechanics are "specified in the binding pages". Its prose summary carries NO modal keyword,
      and the binding pages turn out to disagree with each other: on stdio a dual-era client
      **SHOULD** probe with `server/discover`; on Streamable HTTP a dual-era client only **MAY**
      detect the era. The stdio page also carries a **MUST NOT** ("The fallback **MUST NOT** be keyed
      to one specific error code") that appears nowhere in the summary. A fact written from the
      summary alone states two different obligations as one and drops a MUST NOT entirely — which is
      exactly what the 20th run did before its own self-review caught it.
      THE RULE: IF A PAGE SAYS A RULE IS SPECIFIED ELSEWHERE, YOU HAVE NOT READ THE RULE. Follow the
      pointer before writing any modal verb, and expect per-binding rules to differ by binding.
*** AND WHEN A CLAIM SPANS DOCUMENTS, GREP THE WHOLE REVISION, NOT THE ONE PAGE (18th run). ***
"Feature F is new in revision X" is only established by searching EVERY file of revision X-1, because
the feature may have lived on a different page — AND, per 3d, in a different top-level tree.
*** AND THE SAME DISCIPLINE APPLIES TO A CITATION CHECK, NOT ONLY A CONTENT CHECK (19th run). ***
If a sentence's subject is the revision, the search's scope must be the revision. Cheapest possible
check on your own method: read your claim's subject noun, then look at what you actually grepped.
*** AND A TOKEN CAN SURVIVE A REVISION WHILE ITS MEANING DOES NOT (20th run). *** Grepping
`protocolVersion` across all 41 files of 2025-11-25 returns 15 hits in 5 files — which reads as "not
new, nothing changed". Every one of them is the `initialize` handshake field on
`InitializeRequestParams`/`InitializeResult`; none is the per-request `_meta` key of 2026-07-28. A
POSITIVE grep is as weak a form of evidence as a negative one when the claim is about SEMANTICS: read
the hits, do not count them. The four negative-grep mechanisms above have a positive twin, and this
is it.
