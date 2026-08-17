---
type: pattern
domain: [agentic-engineering, mcp, interop, architecture, tools]
confidence: 0.9
sources: 1
entities: [MCP, extensions, SEP-2133, MCP Apps, MCP Tasks, server/discover, clientCapabilities, ext-auth]
refs: ['https://modelcontextprotocol.io/docs/extensions/overview', 'https://modelcontextprotocol.io/specification/2026-07-28/basic/versioning', 'https://raw.githubusercontent.com/modelcontextprotocol/modelcontextprotocol/main/docs/specification/2026-07-28/basic/versioning.mdx', 'kb://bc6eac5f37df/kb/invariants/ai/agents/tools/mcp/interop/versioning/f4367bd0.md']
---
# MCP conformance no longer implies capability parity — extensions are off by default, SDK-optional, and evolve without core review

`2026-07-28` formalised **extensions**: optional additions defining capabilities beyond the core protocol, identified as `{vendor-prefix}/{extension-name}` (official ones use `io.modelcontextprotocol`; third parties are told to use a reversed domain they own, Java-package style, to avoid collisions).

The consequence that actually changes system design: **two implementations can both be fully conformant to the same MCP revision and still not interoperate on anything that matters to you.** Three stated rules compound to produce that:

- "Extensions are always **disabled by default** and require explicit opt-in from the developer."
- "SDKs can choose to implement extensions, but **it's not required for protocol conformance**." SDK maintainers have full autonomy over which they support.
- Extensions "evolve independently of the core protocol. Updates are managed by the extension repository maintainers and **don't require core maintainer review**."

This matters most because **durable task execution is now an extension**, not core — so long-running agent work has no conformance guarantee behind it at all. Check the specific SDK and the specific server, not the protocol version.

**Negotiation** is per-request on the client side and discovery-time on the server side: clients advertise in `_meta["io.modelcontextprotocol/clientCapabilities"].extensions` on *every* request; servers advertise in the `capabilities.extensions` object of the `server/discover` response. Each extension defines its own settings-object schema; an empty object means no settings.

**Graceful degradation is the implementer's job, and the spec only gestures at it.** If one side supports an extension and the other does not, the supporting side must either fall back to core behaviour or reject the request if the extension is mandatory. The guidance is to document expected fallback per extension — a server offering UI-enhanced tools should still return meaningful text for clients without the UI extension; a server requiring an auth extension may reject clients that lack it. Nothing enforces either choice, so absent explicit fallback design the failure mode is a silently degraded result rather than an error.

**Versioning within an extension:** prefer capability flags or versioning inside the settings object over minting a new identifier; use a new identifier (e.g. `…/my-extension-v2`) only for unavoidable breaking changes. The spec's definition of breaking is broader than most teams' — removing or renaming fields, changing field types, altering the semantics of existing behaviour, **and adding new required fields**.

**Governance, if you are considering publishing one:** the official path is a SEP on the Extensions Track, and **at least one reference implementation in an official SDK is required before the SEP can be reviewed** — implementation precedes approval, not the other way round. Core Maintainers hold final authority over inclusion. Extension specs must use RFC 2119 language and must have an associated working or interest group. Experimental extensions live in `experimental-ext-` repositories as an incubation path and can be archived or removed at Core Maintainer discretion.

Official extensions today: OAuth Client Credentials and Enterprise-Managed Authorization (under `ext-auth`), MCP Apps (interactive inline UI — charts, forms, video players), and MCP Tasks (asynchronous execution for long-running operations, with polling, mid-flight input and durable handles).

**ADDED 2026-08-17, FROM THE NORMATIVE SPECIFICATION RATHER THAN THE DOCS OVERVIEW — TWO CORRECTIONS OF EMPHASIS.**

1. **The degradation rule is a `MUST`, not guidance.** `docs/specification/2026-07-28/basic/versioning.mdx` states it normatively: if one party supports an extension and the other does not, the supporting party "**MUST** either revert to core protocol behavior or reject the request with an appropriate error", and extensions "**SHOULD** document their expected fallback behavior". The paragraph above, drawn from the non-normative extensions overview, understates this — the obligation to pick one of the two branches is mandatory; what is unenforced is only *which* branch, and whether the fallback was documented. The observation that silent degradation is the practical failure mode still stands, because nothing detects a conformant-but-degraded result at runtime.
2. **The identifier prefix is mandatory by cross-reference to the `_meta` key rules.** Extension identifiers "**MUST** follow the `_meta` key naming rules, with a mandatory prefix" — so the naming discipline is not a convention but the same reserved-namespace rule that governs `_meta`, and the second-label reservation trap documented for `_meta` applies here too.

**VERSION ATTRIBUTION, CHECKED ACROSS THE WHOLE PREDECESSOR REVISION.** The capabilities-map negotiation mechanism is genuinely new in `2026-07-28`. All 41 files of revision `2025-11-25` — across `docs/docs`, `docs/specification` and `schema/2025-11-25` — were fetched and grepped unanchored: that revision mentions extensions only as prose in its architecture page ("Additional capabilities can be negotiated through extensions to the protocol", with no mechanism) and as a separate authorization-extensions repository, plus two schema comments about unofficial `params` extensions. There is no `extensions` capability object and no identifier-naming rule. So "conformance no longer implies capability parity" dates precisely to `2026-07-28`, and an implementation targeting `2025-11-25` has nothing to negotiate.
