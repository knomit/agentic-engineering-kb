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
   AGAIN 2026-08-12 (15th run) on three more, and AGAIN 2026-08-14 (17th run) on two more with
   mcp__claude-in-chrome__*, first try, no retries. Seven-plus posts across four runs; this route is settled.
   NOTE ON navigate ERGONOMICS (17th run): calling `navigate` STANDALONE with no tabId auto-creates
   the tab group and returns the tabId in the same result, so the documented
   tabs_context_mcp-then-create dance is not needed for a simple read. Navigate, then get_page_text.
   NOTE THE HOST BOUNDARY: this is openai.com ONLY. developers.openai.com and cdn.openai.com are NOT
   403 — the API guides read fine with plain WebFetch, and cdn.openai.com PDFs download with plain
   curl -A. Do not spend a browser navigation on either.

1b. *** CHEAPEST WAY TO RESOLVE AN UNKNOWN SLUG: WebSearch WITH allowed_domains. NEW, 14th run. ***
   Guessed slugs have now 404'd on cognition, strands, adk and openai. The standing advice was
   "always pull the href off the index", which needs a browser. There is a cheaper first move:
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
   VALIDATED A FOURTH TIME, 17th run, and this is the strongest instance yet: ONE search on
   openai.com returned SIX previously-unknown post URLs, and among them the CORRECT slug for the post
   the 13th run 404'd on by guessing — the real slug is
   /index/responding-next-frontier-critical-cyber-capabilities/ (the guess had inserted "to-the" and
   "of"). A 404 from a guessed slug is worth exactly one search, never a second guess.
   *** ALSO USE THE ARTICLE FOOTER. *** openai.com posts carry a "Keep reading" block listing three
   sibling posts with titles and dates. get_page_text returns it. Reading one post therefore yields
   three more candidate URLs for free — no index sweep, no extra call.

*** 3. modelcontextprotocol.io UNREACHABLE -> READ THE SPEC REPO ON GITHUB. NEW, 16th run. ***
   On 2026-08-12 the host refused connections outright: WebFetch returned
   `connect ECONNREFUSED 76.76.21.21:443` on three separate paths, and `curl` timed out (exit 28,
   HTTP 000). Not a 403, not a block — the origin was down. Every other host that run was fine, so
   isolate before blaming the tool. THE HOST WAS BACK UP AND FULLY RESPONSIVE ON 2026-08-14 (17th
   run) — that outage was transient, not a policy change. The repo route below remains preferred
   anyway, because it is cheaper and enables diffing.
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
   does not depend on the website being up at all — prefer it.

   *** PATH MAPPING — CORRECTED 2026-08-14 (17th run). THE 16th RUN'S VERSION WAS WRONG TWICE. ***
   The two tree prefixes are right:
     site /specification/<rev>/...   -> repo docs/specification/<rev>/...
     site /docs/<rev>/...            -> repo docs/docs/<rev>/...
   CORRECTION 1 — /docs/concepts/tools IS NOT GONE. The 16th run recorded it as dead. It answers
   HTTP 200 and REDIRECTS to https://modelcontextprotocol.io/specification/2026-07-28/server/tools.
   Tested with `curl -o /dev/null -w "%{http_code} %{url_effective}"`, 2026-08-14. The 16th run could
   not test this because the host was down that day, and recorded the guess as a finding. Facts
   citing the old URL were never actually broken.
   CORRECTION 2 — THE SUCCESSOR PAGE NAMED BY THE 16th RUN IS THE WRONG PAGE. It recorded the
   material as having moved to docs/docs/<rev>/learn/server-concepts.mdx. It did not. That page is a
   high-level conceptual overview and contains NO mention of `annotations`, `outputSchema`,
   `structuredContent` or `isError` — grepped for all four, zero hits, in the 2026-07-28 revision.
   The tool CONTRACT material lives in the SPECIFICATION tree:
     docs/specification/<rev>/server/tools.mdx        <- annotations MUST-untrusted warning,
                                                         outputSchema, structuredContent, isError,
                                                         tool-name charset rules, x-mcp-header
   THE LESSON, and it generalises beyond MCP: a redirect target is evidence, a guessed successor is
   not. Confirm a page move by GREPPING THE NEW PAGE FOR THE CONTENT, not by matching titles or
   plausible paths. Both of the 16th run's errors came from reasoning about paths instead of reading
   bytes — and both were recorded with enough confidence to send this run to the wrong file first.
   CAVEAT TO STATE IN ANY FACT BUILT THIS WAY: `main` is the live editing branch, not a release tag.
   Frozen revision directories should be stable, but say in the fact that the text came from the repo
   and that exact strings want re-confirming against the rendered page.
   BONUS THIS ROUTE UNLOCKS FOR FREE: diffing two revisions of the same page is one `diff` command —
   see the note at the foot of this file.

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
     14th pass  "needs a wp-dlm session cookie"    -> wrong; an EMPTY cookie jar downloads fine,
                and the jar it prescribed was verified empty in the run that "proved" it
   Every one was written down from a command that happened to work, crediting all flags equally.
   WHEN A FETCH FINALLY WORKS, DROP ONE FLAG AT A TIME BEFORE RECORDING THE RECIPE. A recipe
   carrying passenger flags is worse than verbose: it sends the next run hunting a cookie that
   does not exist, and it manufactures a false "this source is gated" when the real gate moves.
   The tmstv token is NOT an expiring nonce — the same value worked six days later.
   RE-CONFIRMED 2026-08-12 (15th run) on two NEW ids (49059, 46950), both first try, `-A` alone, no
   Referer and no cookie jar. To be explicit about what this run did and did not establish: it USED
   the recorded recipe, it did not re-run the A/B. RE-CONFIRMED AGAIN 16th run on id 47278 (ANS v1.0),
   and AGAIN 17th run on id 52117 (Agentic Top 10 2026, 1.2MB), first try, `-A` alone.
   Six-for-six across five runs. The tmstv token 1765059207 was recorded 2026-08-12 and still
   worked 2026-08-14 — further evidence it does not expire.

2b. GETTING THE OWASP DOWNLOAD ID — THE TWO-STEP, CONFIRMED 15th RUN AND AGAIN 16th.
   The id in /download/<id>/ is not derivable from the slug and is not in the ALREADY_CRAWLED list.
   Reliable two-step, both halves cheap:
     (i)  WebFetch https://genai.owasp.org/resource/<slug>/ asking for "the direct PDF download URL
          if present in the page HTML (look for links containing /download/)". The resource PAGE is
          NOT UA-gated — plain WebFetch reads it and returns the full URL including ?tmstv=.
     (ii) curl that URL with -A per route 2.
   Only the DOWNLOAD endpoint is gated, not the resource page. Do not reach for curl on step (i).
   Ids captured so far live in crawl-sources.md, not here — they are catalogue, not route.

The 12th run's WebFetch route still works and needs no headers — keep it as the fallback:
  1. WebFetch the RESOURCE PAGE asking for "the direct PDF download URL if present in the page HTML".
  2. WebFetch that download URL. It REPLIES that the content is unreadable binary — ignore that;
     the same tool result ends with "[Binary content (application/pdf, N MB) also saved to <path>]".
  3. Parse that path with pdftotext, writing a .txt; read the .txt in page slices.
pypdf caveats that still hold: the true page count can exceed what the Read tool advertises
(AIUC-1 announced 15pp, is 55); Read's `limit` counts LINES and one PDF page is one very long line;
slide-deck PDFs lose word spacing but stay readable.
PDF NAVIGATION TIP (15th run): on a long extracted .txt, `grep -n` for numbered section headings
first and read targeted slices. The two OWASP guides read this run extract to 4783 and 3879 lines;
the useful material was four slices totalling ~600 lines. Reading linearly wastes the budget on
licence boilerplate and bullet-list control checklists that are below this pack's altitude bar.
SECOND PDF TIP (16th run): `grep -c` for a distinctive token is a ZERO-COST NEGATIVE TEST. Grepping
the ANS extract for "well-known" returned nothing, which settled in one call that ANS does not
document the key path another fact had reconstructed. Negative results are cheap and publishable.
*** PDF TABLES EXTRACT WITH THEIR COLUMNS SHUFFLED — DO NOT CITE ONE (16th run). ***
Beyond the known hyphen-wrapping problem, pdftotext on a multi-column table interleaves cells so
that rows pair with descriptions belonging to other rows. In the ANS v1.0 "Summary of ANS Functional
Layers" table this produced plausible-looking but wrong pairings, and a third-party summary of ANS
repeats one of them. If a claim rests only on a table cell, either confirm it against the document's
prose or say in the fact that you did not. Prose extracts reliably; tables do not.
*** BUT A TABLE IS STILL SAFE TO COUNT (NEW, 17th run). *** Column interleaving destroys the PAIRING
between a row and its cells; it does NOT destroy the cells themselves. So `grep -oE '<TOKEN>' | sort
| uniq -c` over a table region gives a trustworthy FREQUENCY even when no individual row can be
quoted. That is how the OWASP incident tracker's per-threat-class counts were obtained. State in the
fact which of the two you relied on — frequency is publishable, pairing is not.
*** PDF LINE WRAPS DEFEAT grep IN BOTH DIRECTIONS (reinforced, 17th run). *** A grep for a label that
IS present can return NOTHING because the label is wrapped across two lines ("Agent Behaviour\nHijack").
A negative grep is therefore NOT proof of absence for any multi-word string. Grep the first word
alone, or grep with `-A1`, before recording "the document does not say X". This nearly produced a
false absence claim this run and is the mirror image of the 15th run's 0720e9d7 defect, where a wrap
was silently reconstructed into a literal.
BROWSER CAVEATS: on builder.aws.com the FIRST get_page_text after a navigate SOMETIMES returns a stub
ending in 'Loading article'; call it again. Never conclude 'blocked' from one empty call.
To pull links/hrefs off an index use javascript_tool with a querySelectorAll expression — `find`
returns element refs but NOT hrefs.
NOTE: large learn.microsoft.com and platform.claude.com pages exceed WebFetch's inline limit and are
persisted to a file on disk; just Read the path returned, or grep it. Ask a NARROW prompt to keep the
answer inline instead. Likewise a broad knomit_query can exceed the tool-result limit — CONFIRMED
AGAIN 14th run: sort=recent with limit=60 blew the limit at 69k chars. Use limit<=25.
AND knomit_explain ON crawl-state.md NOW EXCEEDS IT TOO (15th run: 51.5KB, persisted to a file).
That is expected, not an error — the tool result names the path; just Read it. Do not retry the call.
*** BUILDERS' LIBRARY — SOME ARTICLES ARE VIDEO-ONLY ***
Confirmed video-only, no prose body, DO NOT RE-FETCH:
  amazons-approach-to-failing-successfully   | 3F05J4fjklUZCE7kjuIp6LaTacl
  beyond-five-9s-lessons-from-our-highest-available-data-planes | 3F073j4jJOsSRTDlQM3eiZxkFLm
Publication date does not predict it. Budget one cheap fetch per article and abandon if the text ends
right after the byline.

*** VERIFICATION TECHNIQUE, NOT A FETCH ROUTE, BUT IT LIVES HERE BECAUSE IT IS A RECIPE (16th run) ***
DIFF TWO REVISIONS OF THE SAME SPEC PAGE. Where a source is versioned and mirrored in git, the
staleness pass stops being "re-read and hope you notice" and becomes a diff:
  curl the <old-rev> and <new-rev> copies of the page, then `diff a b`
On the MCP security page this took one command and yielded, in a single pass: a heading rename that
CONFIRMED a fact's prediction (Session Hijacking -> State Handle Hijacking), a MUST downgraded to
SHOULD that CORRECTED the same fact, a new subsection that explicitly contradicted another fact's
title ("SSRF risks are not limited to MCP clients"), and three wholly new attack sections worth a
fact of their own. Prefer this over re-reading whenever the source is versioned.
CALIBRATION NOTE (17th run): the same technique on docs/docs/<rev>/learn/server-concepts.mdx across
2025-06-18 -> 2026-07-28 produced a THREE-LINE diff (one method rename, resources/subscribe ->
subscriptions/listen). A near-empty diff is a REAL and useful result — it says the page is stable and
costs two curls to establish. Do not read a small diff as a failed technique.
