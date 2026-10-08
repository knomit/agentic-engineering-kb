# Recurring sources: the seed list

This list is swept on every run, together with every feed in the writable
`artifacts/jobs/agentic-engineering/discovered-sources.md`. It is read-only. It
changes only through git, and a feed the job finds itself goes in
`discovered-sources.md`, never here. The notes give each entry's kind and the
facts an earlier run paid to learn about it. Per-host fetch recipes are in
`fetch-routes.md`.

Kinds:
- **dated**: an index of dated items. Candidates are the items dated on or
  after the feed's high-water date in `feeds.md` that are not in `seen`.
- **undated**: an index or catalogue whose items carry no reliable date.
  Candidates are the items not in `seen`.
- **page**: one page, re-read for a change. It has no items.

## Feeds

- https://www.anthropic.com/engineering (dated)
- https://www.anthropic.com/news/ (dated). Postmortems are published here, not under /engineering.
- https://www.anthropic.com/research (dated). Added on the 47th run. It carries full research write-ups; the index's "See more" link is a placeholder, and older /research/ slugs are linked from the alignment.anthropic.com index.
- https://alignment.anthropic.com/ (dated). The Alignment Science blog: a separate publication from /news/, with the full research write-ups. The depth of the index listing varies between calls (fetch-routes route 33).
- https://alignment.openai.com/misalignment-reports/ (undated). OpenAI's misalignment report series. It publishes in batches; ask for an enumeration, not a count (route 33). It is not 403, unlike openai.com proper.
- https://deploymentsafety.openai.com/ (dated). Added on the 41st run. OpenAI's safety-evaluation hub, one page per model. Not gated.
- https://developers.openai.com/cookbook (undated)
- https://developers.openai.com/api/docs/guides/ (undated). The API guides tree: a different source from openai.com/news and from the cookbook. Plain WebFetch reads it.
- https://simonwillison.net/tags/llms/ (dated)
- https://www.langchain.com/blog/ (dated)
- https://www.latent.space/archive (dated)
- https://eugeneyan.com/writing/ (dated)
- https://www.microsoft.com/en-us/research/blog/ (dated)
- https://www.microsoft.com/en-us/security/blog/ (dated)
- https://aws.amazon.com/blogs/machine-learning/ (dated)
- https://research.google/blog/ (dated)
- https://embracethered.com/blog/ (dated)
- https://metr.org/blog/ (dated). Promoted on the 26th run.
- https://sourcegraph.com/blog (dated)
- https://cognition.com/blog (dated). Demoted on the 26th run to back catalogue only.
- https://www.trychroma.com/research (dated)
- https://builder.aws.com/learn/topics/builders-library (undated). JS-rendered; see fetch-routes.
- https://code.claude.com/docs/en/best-practices (page). The live doc.
- https://genai.owasp.org/ (undated)
- https://owasp-agentic-ai-security-incidents.lovable.app/ (undated). The OWASP agentic incidents tracker; added on the 12th run.
- https://www.aisi.gov.uk/blog/ (dated). Added on the 13th run; a large back catalogue.
- https://openai.com/news/ (dated). The sweep URL; openai.com/index/ redirects here. Posts are still at /index/<slug>, so seen URLs for this feed are on openai.com under /index/. Needs the browser (fetch-routes route 1).
- https://blog.redwoodresearch.org/ (dated). Low volume.
- https://github.com/vectara/hallucination-leaderboard (page)
- https://huggingface.co/blog (dated)

## Tripwires (pages)

- https://modelcontextprotocol.io/specification/versioning (page). THE TRIPWIRE: one plain WebFetch states the current MCP revision in one sentence.
- https://modelcontextprotocol.io/specification/2026-07-28/deprecated (page). Added on the 12th run as a cheap tripwire.
- https://api.github.com/repos/modelcontextprotocol/modelcontextprotocol/contents/docs/specification (page). Added on the 16th run. Gated since the 27th run: HTTP 403 from the harness, not from GitHub. Do not spend a call on it until repo access is granted; use the versioning page above (fetch-routes routes 3 and 3f).

## Standing note: not a feed

- https://arxiv.org/ is not sweepable. arXiv resolves a title through WebSearch in one call, and the result carries the /html/<id>v1 full-text URL, which is the one you want. /abs/ gives only the abstract.
