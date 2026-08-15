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
   AGAIN 2026-08-12 (15th run) on three more, AGAIN 2026-08-14 (17th run) on two more, AGAIN
   2026-08-15 (18th run) on /index/introducing-aardvark/, and AGAIN 2026-08-15 (19th run) on THREE
   posts back to back (codex-security-now-in-research-preview, designing-agents-to-resist-prompt-
   injection, prompt-injections), all first try, no retries. Twelve-plus posts across six runs;
   this route is settled and needs no further re-confirmation.
   NOTE ON navigate ERGONOMICS (17th run, RE-CONFIRMED 18th and 19th): calling `navigate` STANDALONE
   with no tabId auto-creates the tab group and returns the tabId in the same result, so the
   documented tabs_context_mcp-then-create dance is not needed for a simple read. Navigate, then
   get_page_text. To read several posts in one run, PASS THE SAME tabId to each subsequent navigate —
   one tab, N navigations, no cleanup.
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
   VALIDATED A FIFTH TIME, 19th run: the Codex Security post, whose slug was UNKNOWN (the 18th run
   could only record "linked from the Aardvark banner"), resolved in ONE search to
   /index/codex-security-now-in-research-preview/ — and the search result SNIPPETS alone already
   carried the three-stage architecture and the research-preview rollout scope, i.e. enough to
   confirm the post was worth the browser call before spending it.
   *** ALSO USE THE ARTICLE FOOTER — AND SEE THE CORRECTED CALIBRATION BELOW. *** openai.com posts
   carry a "Keep reading" block listing three sibling posts with titles and dates. get_page_text
   returns it, so reading one post yields three more candidate URLs for free.
   CALIBRATION, CORRECTED 19th run. The 18th run concluded the footer is a pure RECENCY feed, from a
   single observation (a 2025 post returning three Aug-2026 product announcements). Three more
   observations this run say it is narrower than that — it appears to be **recency WITHIN THE POST'S
   PRIMARY CATEGORY**:
     /index/codex-security-now-in-research-preview/ (tagged Product, Security) -> Ultrafast mode
        (Product, Aug 13), Testing ads (Company, Aug 11), Daybreak on AWS (Product, Aug 11)
     /index/designing-agents-to-resist-prompt-injection/ (tagged Security)     -> Expanding Daybreak
        (Security, Aug 10), Putting frontier cyber models (Security, Aug 10), Responding to the next
        frontier (Security, Aug 7)
     /index/prompt-injections/ (tagged Security)                                -> the SAME three
        Security posts
   So a SECURITY-tagged post's footer is a free, current listing of the three newest security posts —
   which is exactly the sweep this pack wants — while a Product-tagged post's footer is noise for our
   purposes. STATED AS A HYPOTHESIS CONSISTENT WITH FOUR OBSERVATIONS, NOT AS A SETTLED RULE: the
   category tag is visible at the top of each post, so it is cheap to check the prediction next time.
   Practical use: to sweep openai.com security posts without an index fetch, open any known
   Security-tagged post and read its footer.

*** 3. modelcontextprotocol.io UNREACHABLE -> READ THE SPEC REPO ON GITHUB. NEW, 16th run. ***
   On 2026-08-12 the host refused connections outright: WebFetch returned
   `connect ECONNREFUSED 76.76.21.21:443` on three separate paths, and `curl` timed out (exit 28,
   HTTP 000). Not a 403, not a block — the origin was down. Every other host that run was fine, so
   isolate before blaming the tool. THE HOST WAS BACK UP AND FULLY RESPONSIVE ON 2026-08-14 (17th
   run) and again on 2026-08-15 (18th) — that outage was transient, not a policy change. The repo
   route below remains preferred anyway, because it is cheaper and enables diffing.
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

   *** 3b. A PAGE CAN BE A FILE IN ONE REVISION AND A DIRECTORY IN ANOTHER. NEW, 18th run. ***
   Do NOT build a predecessor path by substituting the revision date into a current path. MCP
   authorization is the worked example:
     2025-03-26 / 2025-06-18 / 2025-11-25 -> docs/specification/<rev>/basic/authorization.mdx  (ONE FILE)
     2026-07-28 / draft                   -> docs/specification/<rev>/basic/authorization/       (A DIRECTORY of
                                             index.mdx, security-considerations.mdx,
                                             client-registration.mdx, authorization-server-discovery.mdx)
   So .../2025-11-25/basic/authorization/security-considerations.mdx does not exist. ALWAYS resolve
   the predecessor path out of tree.json rather than by string substitution.

   *** 3c. THE 404 THAT SILENTLY BECOMES A FALSE "ENTIRELY NEW IN THIS REVISION" FINDING. NEW, 18th. ***
   THIS IS THE SHARPEST TRAP IN THIS FILE AND IT MANUFACTURES VERSION-ATTRIBUTION DEFECTS.
   `raw.githubusercontent.com` answers a missing path with **HTTP 404 whose BODY is the literal text
   `404: Not Found`** — and `curl -sL -o file` WRITES THAT BODY TO THE FILE and exits 0. The file
   exists, `ls` looks fine, and `diff old new` then reports that every line of the new revision was
   added. Read naively that is exactly the shape of "this entire section is new in revision X" —
   a fabricated novelty claim, and the very defect class checklist item 11 exists to catch.
   THE GUARD, cheap and mandatory before any revision diff:
     wc -l *.mdx                      # a 0- or 1-line .mdx is a 404, not a short page
     grep -c "404: Not Found" out.mdx  # must be 0
   Hit live on the 18th run: the naive predecessor path for authorization/security-considerations
   404'd (see 3b), and the resulting diff claimed the whole page was new. It is not — the PKCE
   discovery rules in it date from 2025-11-25, which is what the corrected walk established.
   GENERALISES: any `curl -o` against a host that serves a BODY with its error status has this
   failure. Same family as the OWASP "No Access" HTML arriving with a .pdf filename (route 2) —
   check what you downloaded, never that the download happened.
   19th-RUN NOTE: the guard was run on all 45 files fetched this run (4 split pages, 3 predecessor
   revisions, 41 whole-revision files, overlapping) and returned 0 every time. It costs one command
   and it is the difference between a verified version claim and a fabricated one.

   *** 3d. THE MCP REPO HAS A SEPARATE TOP-LEVEL schema/ TREE. A docs/-SCOPED SWEEP MISSES IT. ***
   NEW, 18th-run review pass. Revision content does NOT all live under docs/. Each released revision
   also has:
     schema/<rev>/schema.json   (the normative JSON Schema, ~4000 lines)
     schema/<rev>/schema.ts     (the TypeScript source of truth, ~2600 lines)
     schema/<rev>/schema.mdx
   A sweep written as `docs/(specification|docs)/<rev>/**.mdx` silently excludes all three. That is
   fine for prose questions and NOT fine for "does field X exist in revision R", which is exactly the
   kind of question a version-attribution check asks. When establishing that something is ABSENT from
   a revision, enumerate on the REVISION DATE, not on a docs/ prefix:
     grep -oE '"path":"[^"]*<rev>[^"]*\.(mdx|json|ts)"' tree.json | sed 's/"path":"//;s/"$//'
   Caught while re-checking an "absent from 2025-11-25" claim that had swept 38 docs/ files and none
   of the three schema/ files. The claim survived — but it was luck, not method.
   CONFIRMED AND COSTED, 19th run: that enumeration on `2025-11-25` returns exactly **41 files**
   across three trees (docs/docs, docs/specification, schema/2025-11-25). Fetching all 41 is one
   shell loop and a few seconds — there is no reason to ever run the narrower sweep again.

   *** 3e. IN .mdx, NORMATIVE KEYWORDS ARE BOLDED — SO GREPPING A NORMATIVE SENTENCE FINDS NOTHING.
   *** NEW AND IMPORTANT, 19th run. A FOURTH INDEPENDENT MECHANISM FOR "A NEGATIVE GREP IS NOT PROOF
   *** OF ABSENCE", AND THE ONE MOST LIKELY TO BITE THIS JOB, BECAUSE THIS JOB GREPS MUSTs ALL DAY.
   The MCP spec writes every RFC 2119 keyword as markdown emphasis: `**MUST**`, `**MUST NOT**`,
   `**SHOULD**`. So the sentence a reader would quote does not exist as a literal string in the file.
   ISOLATED CLEANLY, same file, same run:
     grep -c "MUST NOT assume that credentials"        asd-2026.mdx  -> 0   (looks like absence)
     grep -c "assume that credentials"                 asd-2026.mdx  -> 1   (it is there)
     grep -n  "assume that credentials"                asd-2026.mdx
       32:**MUST NOT** assume that credentials valid for one authorization server will be accepted by
   RULES:
     * NEVER let a search term span a normative keyword. Grep the clause on ONE SIDE of the MUST.
     * The failure is silent and total — zero hits, no warning, and the phrase you searched for is
       the exact phrase the spec means. It reads as a confident negative.
     * Same family as the pdftotext form-feed and line-wrap traps below, but a DIFFERENT cause
       (source markup, not extraction), so it survives even when the file is clean UTF-8 text you
       downloaded yourself. Applies to any docs-as-markdown source, not just MCP.
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
   AGAIN 17th run on id 52117, and AGAIN 18th run on THREE ids in one go (54627, 54018, 50592),
   first try, `-A` alone. Nine-for-nine across six runs.
   The tmstv token 1765059207 was recorded 2026-08-12 and still worked 2026-08-14; 1754459367 was
   recorded 2026-08-05 and still worked 2026-08-15, TEN DAYS LATER. It does not expire.

2b. GETTING THE OWASP DOWNLOAD ID — THE TWO-STEP, CONFIRMED 15th RUN, AGAIN 16th, AGAIN 18th.
   The id in /download/<id>/ is not derivable from the slug and is not in the ALREADY_CRAWLED list.
   Reliable two-step, both halves cheap:
     (i)  WebFetch https://genai.owasp.org/resource/<slug>/ asking for "the direct PDF download URL
          if present in the page HTML (look for links containing /download/)". The resource PAGE is
          NOT UA-gated — plain WebFetch reads it and returns the full URL including ?tmstv=.
     (ii) curl that URL with -A per route 2.
   Only the DOWNLOAD endpoint is gated, not the resource page. Do not reach for curl on step (i).
   Ids captured so far live in crawl-sources.md, not here — they are catalogue, not route.
   18th-RUN BONUS: step (i) also returns the PUBLICATION DATE, which is the cheapest possible
   staleness check on a PDF you have already read — compare it against the date recorded in the fact
   before spending the download. Pair it with `pdfinfo <file> | grep -i 'pages\|creationdate'` after
   download: page count + creation date together settle "is this the same document I read before"
   in one call, with no re-reading.

*** 2c. `file` REPORTS A PDF PAGE COUNT AND IT CAN BE WRONG. USE `pdfinfo`. NEW, 19th run. ***
The 18th run made page count the cheap "is this the same document" test. That test is only as good
as the tool you read the count with, and the two available tools DISAGREE on the same bytes:
  file masec.pdf     -> "PDF document, version 1.5, 3 pages"     WRONG
  pdfinfo masec.pdf  -> "Pages: 8"                                CORRECT (paper is 8pp, still v1)
Same file, same run, no re-download between them. `file` reads a hint near the front of the file and
is not parsing the page tree; `pdfinfo` is. WHY THIS MATTERS MORE THAN IT LOOKS: a run doing a
staleness check with `file` would have seen "3 pages" against a recorded 8 and manufactured a
"THE SOURCE CHANGED" finding on a document that had not changed at all — the false-positive twin of
the 3c trap. `file` is still the right tool for the ONE question route 2 asks it ("is this a PDF or
is it the HTML error page"). It is not a source of page counts. Never compare a `file` count against
a `pdfinfo` count recorded earlier, or vice versa.

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
document the key path another fact had reconstructed. Negative results are cheap and publishable —
BUT SEE THE FORM-FEED RULE BELOW BEFORE TRUSTING ANY ANCHORED NEGATIVE.

*** THE FORM-FEED RULE. NEW AND IMPORTANT, 18th-run review pass. ***
*** pdftotext EMITS \f (0x0C) AT EVERY PAGE BREAK AND PREPENDS IT TO THE FIRST TOKEN OF THE NEXT
*** PAGE. SO ANY ^-ANCHORED PATTERN SILENTLY MISSES EXACTLY ONE ITEM PER PAGE BOUNDARY.
The line looks like `ASI07` in a Read and is byte-for-byte `\f A S I 0 7 \n`. Confirmed with
`od -c`. Consequences, and they are not hypothetical — this produced a wrong count that was nearly
published as an "independently re-derived" verification:
  grep -E "^ASI[0-9]{2}$"   -> 9 of 10 rows. Wrong, and plausible-looking.
  grep -xE "ASI[0-9]{2}"    -> 9 of 10. Same failure; -x is an anchor too.
  grep -oE "ASI[0-9]{2}"    -> 10 of 10. UNANCHORED IS IMMUNE.
RULES:
  * For COUNTING over an extract, always use unanchored `grep -o`. The frequency technique already
    recorded below is unaffected precisely because it was written unanchored.
  * For a NEGATIVE test, an anchored miss is not absence — this is a THIRD mechanism for that,
    alongside line-wrapping and hyphen-breaking. Prefer `grep -o` or add `[[:space:]\f]*` to the anchor.
  * The undercount is SYSTEMATIC, not random: always the first match on each page, always exactly
    one per boundary. So a long table spanning N pages loses N-1 rows and still looks like a table.
  * `paste - -` pairing over an anchored grep desynchronises at the first page break and every
    subsequent pairing is off by one. If pairs stop lining up, suspect \f before suspecting the PDF.
*** FOUR MECHANISMS NOW, NOT THREE — A NEGATIVE GREP FAILS FOR FOUR INDEPENDENT REASONS (19th run):
***   (i) pdftotext line-wrapping splits a multi-word phrase across lines;
***  (ii) pdftotext hyphen-breaking splits a single token ("communica-\ntion");
*** (iii) pdftotext form feeds defeat ^-anchors, one miss per page;
***  (iv) MARKDOWN EMPHASIS in .mdx sources breaks any phrase spanning a **MUST** (route 3e).
*** (i)-(iii) are extraction artifacts; (iv) is in the source bytes themselves. A file being clean
*** text you downloaded yourself rules out the first three and NOT the fourth.
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
*** AND SOME PDF TABLES DO EXTRACT ROW-FAITHFULLY — CHECK BEFORE GIVING UP (NEW, 18th run). ***
The AIUC-1 crosswalk's per-requirement mapping tables extract as a clean vertical run of
  <ASI id> / <blank> / <threat name> / <blank> / <Primary|Secondary>
triples, one field per line, in row order. That is fully reliable to PAIR from, not merely to count,
and it is how B006=8/10, D003=8/10 and E015=10/10 were re-derived. The distinguishing feature is
COLUMN COUNT and cell length: narrow tables with short cells serialise cleanly; wide tables with
multi-line prose cells are the ones that interleave. Look at ten lines of the extract before
deciding which regime you are in — the 16th run's blanket "never cite a table" is too strong.
CAVEAT ADDED BY THE REVIEW PASS: a row-faithful table is still cut by page-break form feeds and by
repeated `genai.owasp.org / Page N` footers landing MID-TABLE. Read such a region with Read, not with
an anchored grep, and expect a footer between any two rows.
*** AND WHEN THE TABLE IS THE WIDE KIND, PAIR ON CONTENT INSTEAD OF POSITION (NEW, 19th run). ***
A wide table is not useless for pairing — it is useless for pairing BY POSITION. In the MASEC paper's
vector/scenario table the extract runs three vector cells consecutively and then three scenario
cells, so position implies nothing. But the vector cell about "active security monitoring ...
sanitisation" and the scenario cell about "a dynamic firewall sanitises a natural language query"
share a distinctive token no other row in the group carries, which identifies the pair with more
confidence than adjacency ever would. USE A DISCRIMINATING TOKEN, AND SAY IN THE FACT THAT THE
PAIRING IS SEMANTIC RATHER THAN POSITIONAL — a reader can then check it the same way.
*** AND EXPECT A SOURCE TO NAME THE SAME THING TWICE (19th run). *** The MASEC paper calls one class
"heterogeneous multi-agent exploits" in its abstract and "Heterogeneous Attackers" in its table;
OWASP's Top 10 double-names T12 the same way. A grep for the abstract's phrase will not find the
table row. Before recording that a document does not discuss X, grep the SHORTEST DISTINCTIVE STEM
("Heterogeneous"), not the full phrase.
*** PDF LINE WRAPS DEFEAT grep IN BOTH DIRECTIONS (reinforced, 17th run). *** A grep for a label that
IS present can return NOTHING because the label is wrapped across two lines ("Agent Behaviour\nHijack").
A negative grep is therefore NOT proof of absence for any multi-word string. Grep the first word
alone, or grep with `-A1`, before recording "the document does not say X". This nearly produced a
false absence claim this run and is the mirror image of the 15th run's 0720e9d7 defect, where a wrap
was silently reconstructed into a literal. HIT AGAIN 19th run: `grep "active monitoring"` returned
nothing on a paper that says it, because the extract reads "active\nmonitoring"; `grep -B1 -A2
"not cover"` recovered it immediately. When a phrase you expect is missing, re-grep on its RAREST
SINGLE WORD with context flags before concluding anything.
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
*** knomit_query sort=recent IS ORDERED BY LAST TOUCH, NOT BY CREATION (NEW, 18th run). ***
An update bumps a fact to the front. That makes the TAIL of a sort=recent walk the set of facts
LEAST RECENTLY VERIFIED — which is exactly the staleness-pass target, and a better one than original
creation date. But reaching the tail is expensive: at limit=25 the pack takes many pages and each
page costs ~15k tokens. Budget 4-6 pages to get into genuinely old territory (the 18th run reached
the 2026-07-28 band in four) and pick the sample from there rather than paging to exhaustion.
*** CHEAPER WAY TO FIND A FACT'S PATH WHEN YOU ONLY HAVE ITS SHORT ID (NEW, 19th run). ***
The queue names facts by 8-hex id (74996815, eae23eac) and knomit_query CANNOT search by id. Paging
sort=recent to find one is the expensive way. Instead run a TOPICAL knomit_query aimed at what the
fact is about — the id is the filename stem, so it is visible in the `file` field of any result row
that matches. Two topical queries this run resolved five queued ids at ~5k tokens total, against the
~15k-per-page cost of walking sort=recent. Keep the queue's one-line descriptions specific enough to
turn into a query; that is what makes this work.
*** THE `grep` ON THIS MACHINE IS ugrep 7.5.0, NOT GNU grep (observed 18th run). ***
It is largely compatible, but it is not the tool most recipes are written against, and its warnings
differ ("ugrep: warning: <file>: No such file or directory"). If a grep behaves unexpectedly, check
`grep --version` before concluding anything about the DATA. Note also that the Bash tool's working
directory PERSISTS between calls — a `cd` in one call changes where the next one runs, which produced
a spurious "No such file or directory" this run. Prefer absolute paths or re-`cd` each call.
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
*** FOUR HARD PRECONDITIONS ON THIS TECHNIQUE, ALL LEARNED THE HARD WAY (18th run). ***
  (a) RESOLVE BOTH PATHS FROM tree.json. Never substitute a revision date into a path — see 3b.
  (b) VERIFY BOTH FILES ARE REAL BEFORE DIFFING. A 404 body diffs as "all new" — see 3c.
  (c) DIFF THE IMMEDIATE PREDECESSOR, NOT A CONVENIENT OLDER ONE. The 16th run diffed
      2025-06-18 -> 2026-07-28, skipping 2025-11-25 entirely, and concluded three security sections
      were "additions in 2026-07-28". True of that page — but the CONTENT of two of them had been
      sitting in 2025-11-25's authorization.mdx all along and was MOVED, not written. A two-revision
      jump cannot distinguish "new" from "moved", and "new in revision X" is a claim a reader will
      act on. If you must skip a revision, say in the fact which revisions you actually compared.
  (d) BOUND THE REGION ON THE FOLLOWING HEADING, NOT ON EOF. Extracting a section with
      `sed -n '/^## Target/,$p'` runs to end of file and sweeps in every SIBLING section after it,
      which then show up as deletions. On the 18th run this made `## MCP Authorization Extensions`
      look deleted when it had merely moved to another page of the same split. Use
      `awk '/^## Target/{f=1} /^## NextHeading/{f=0} f'`. An over-wide range ADDS phantom findings
      rather than hiding real ones — so it will not cost you a true finding, but it will hand you a
      false one, and the 17th run published exactly this mistake as a contaminated count.
  (e) NEW, 19th run — A SPLIT DUPLICATES RULES, AND THE COPIES CAN DIFFER IN MODAL STRENGTH. When one
      page becomes four, a rule that straddles the seam is often RESTATED on the topic page at a
      weaker modality, with the normative statement left on the index page. MCP 2026-07-28 states the
      `scope`-in-WWW-Authenticate rule as "**SHOULD** include" on authorization/index.mdx and as
      "Servers can also include" on authorization-server-discovery.mdx. Read only the topic page and
      it looks like a SHOULD was downgraded between revisions. IT WAS NOT. Before recording any
      weakening, grep EVERY page of the new revision for the rule and cite the strongest statement.
      This is the mirror of (c)/(d): those find content that moved, this finds content that forked.
*** AND WHEN A CLAIM SPANS DOCUMENTS, GREP THE WHOLE REVISION, NOT THE ONE PAGE (18th run). ***
"Feature F is new in revision X" is only established by searching EVERY file of revision X-1, because
the feature may have lived on a different page — AND, per 3d, in a different top-level tree. Enumerate
on the revision date, not on a docs/ prefix:
  grep -oE '"path":"[^"]*<prev-rev>[^"]*\.(mdx|json|ts)"' tree.json | sed 's/"path":"//;s/"$//' > files.txt
  # curl each, then grep the lot (UNANCHORED) for the distinguishing token
Forty-one files, one loop, and it turned "RFC 9207 is new in 2026-07-28" from an assumption into a
verified fact — while the same method showed the PKCE-discovery rules were NOT new and date from
2025-11-25. Two features, one page, opposite answers: that is why the sweep cannot be skipped.
*** AND THE SAME DISCIPLINE APPLIES TO A CITATION CHECK, NOT ONLY A CONTENT CHECK (19th run). ***
The 19th run wrote "revision 2025-11-25 cites RFC 8414 §3.1 and §5 but never §3.3" from a grep over
ONE page, then caught it in self-review and re-ran the grep over all 41 files. The claim survived
(two further bare rfc8414 citations in the tutorial, no §3.3 anywhere) — but "the revision cites" is
a claim about the REVISION and a one-page grep cannot support it. If a sentence's subject is the
revision, the search's scope must be the revision. Cheapest possible check on your own method:
read your claim's subject noun, then look at what you actually grepped.
