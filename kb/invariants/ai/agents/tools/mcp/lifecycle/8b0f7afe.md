---
type: reference
domain: [agentic-engineering, mcp, tools, interop, governance]
confidence: 0.9
sources: 1
entities: [MCP, SEP-2596, Active, Deprecated, Removed, deprecated registry, Core Maintainers, Tier 1 SDK, expedited removal, schema.ts]
motifs: [window-start-misread, eligibility-not-schedule]
refs: ['https://modelcontextprotocol.io/community/feature-lifecycle', 'kb://bc6eac5f37df/kb/gotchas/ai/agents/tools/mcp/deprecation/012daf73.md']
---
# MCP's deprecation window is measured from the revision that marks a feature Deprecated, not from the SEP going Final — and it is a floor on eligibility, not a schedule for removal

Adopted via SEP-2596. The policy governs features of the MCP core specification — protocol messages, capabilities, transports, schema types and normative behavioural requirements — and is distinct from the revision lifecycle (Draft, Current, Final) of the specification document itself. A feature is in exactly one of three states: Active, Deprecated, Removed.

THE WINDOW. A deprecation SEP must specify a minimum deprecation window: "the number of months, at least twelve, that the feature must remain Deprecated before it is eligible for removal." The measurement point is the part that is easy to get wrong and expensive to get wrong: the window "is measured from the release of the specification revision in which the feature is first marked Deprecated, not from the date the SEP reaches Final." A SEP that reached Final long before its revision shipped buys you no extra time, and one that landed just before a release buys you no less. Earliest removal is then the first specification revision released as Current on or after the window elapses — a revision, not a date, and MCP revisions are dated and irregular.

THE EXPEDITED EXCEPTION IS NARROW, AND THE DEFINITION IS THE WHOLE POINT. The twelve-month floor may be shortened only when the feature presents an active security risk, which the policy defines as "a vulnerability with a published security advisory or documented in-the-wild exploitation for which no in-place mitigation exists." All three clauses bind: a theoretical weakness, an unpublished report, or a risk that can be mitigated in place does not qualify. It requires Core Maintainer approval under the governance decision process, and even then "The shortened window must still provide at least ninety days between the feature becoming Deprecated and its earliest removal." Ninety days is the hard floor under every circumstance the policy contemplates.

WHAT THIS DOES NOT MEAN, and this is the misreading the twelve-month figure invites. Deprecated does not mean removed within twelve months. "Features may remain Deprecated, without removal, for much longer than the minimum deprecation window", and removal "is executed at the discretion of the Core Maintainers after the minimum deprecation window has elapsed." The window is a floor on how soon your migration can be forced, not a prediction of when it will be. Planning a migration to land by the earliest-removal date is sound; reading the date as an announcement that the feature disappears then is not.

SECOND MISREADING, IN THE OPPOSITE DIRECTION: spec removal is not SDK removal. "Removal from the specification does not oblige an SDK to drop the feature from releases" — that timeline is governed by the SDK's own revision-support policy. So a feature removed from the spec may keep working in your SDK for a further unbounded period, and code that still compiles is not evidence the feature is still specified.

SDK OBLIGATIONS, which are what you will actually notice first. Once the revision marking a feature Deprecated is released as Current, Tier 1 SDKs must mark the corresponding API surface deprecated using the language's native mechanism in their next release, referencing the deprecation SEP and the earliest removal date where the mechanism permits, and should emit a runtime warning when the feature is exercised. A Tier 1 SDK that consistently fails to surface a Deprecated feature is subject to the Tier Relegation Process.

TRACKING. The deprecated registry at docs/specification/draft/deprecated.mdx lists every feature in a Deprecated or Removed state with its SEP, the revision it became Deprecated in, its migration path and its earliest removal — the canonical single place to look rather than reconstructing the picture from changelogs. A Deprecated feature may also be restored to Active by a superseding SEP; if it is later deprecated again, the minimum window is measured afresh from the revision in which the new deprecation takes effect.
