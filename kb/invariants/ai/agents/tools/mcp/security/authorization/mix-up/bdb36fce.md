---
type: reference
domain: [agentic-engineering, mcp, security, authorization]
confidence: 0.9
sources: 1
entities: [MCP, "2026-07-28", RFC 9207, iss, mix-up attack, authorization_response_iss_parameter_supported, PKCE, RFC 3986]
refs: ['https://modelcontextprotocol.io/specification/2026-07-28/basic/authorization', 'https://raw.githubusercontent.com/modelcontextprotocol/modelcontextprotocol/main/docs/specification/2026-07-28/basic/authorization/index.mdx', 'https://raw.githubusercontent.com/modelcontextprotocol/modelcontextprotocol/main/docs/specification/2026-07-28/basic/authorization/security-considerations.mdx', 'https://raw.githubusercontent.com/modelcontextprotocol/modelcontextprotocol/main/schema/2025-11-25/schema.json', 'kb://bc6eac5f37df/kb/gotchas/ai/agents/tools/mcp/security/client-identity/066a9dad.md']
---
# MCP's new mix-up defence fails open: if the authorization server neither advertises nor sends `iss`, the client is required to proceed unprotected

MCP `2026-07-28` adds **Authorization Response Validation** (RFC 9207 issuer identification) as the required mitigation for mix-up attacks. `066a9dad` records the attack and why PKCE does not cover it; this fact is the mechanism, read from the normative page.

**VERSION ATTRIBUTION, CHECKED RATHER THAN ASSUMED.** This is genuinely new in `2026-07-28`. Revision `2025-11-25` was searched in full for `9207` and `authorization_response_iss_parameter_supported`: zero hits across all **38 `.mdx` files** under `docs/specification/2025-11-25/` and `docs/docs/2025-11-25/`, **and** across the three files of the separate top-level `schema/2025-11-25/` tree (`schema.json`, `schema.mdx`, `schema.ts`). *The schema tree is called out because it is easy to miss — it sits outside the `docs/` prefixes and a `docs/`-scoped sweep silently excludes it, which is exactly what the first version of this fact did.*

**THE PREREQUISITE, WHICH IS WHERE AN IMPLEMENTATION WILL GET IT WRONG.** Before redirecting the user-agent the client **MUST** record the `issuer` value "from the selected authorization server's validated metadata document" and associate it with the same per-request record that holds the PKCE code verifier (and `state`, if used). The spec states the dependency plainly: "The validation in this section depends on that recorded value being authentic; it provides no protection if the expected issuer was obtained from an unvalidated source." So this control is stacked on top of metadata validation — get discovery wrong and the mix-up defence silently becomes decoration.

**THE DECISION TABLE.** Authorization servers **SHOULD** include `iss` in authorization responses, "including error responses"; those that do **MUST** advertise it by setting `authorization_response_iss_parameter_supported` to `true` in their metadata. Clients **MUST** apply the validation *before transmitting the authorization code to any token endpoint*:

| advertised | `iss` in response | client action |
|---|---|---|
| `true` | present | compare to recorded issuer, simple string comparison (RFC 3986 §6.2.1) |
| `true` | absent | **reject the response** |
| `false` or absent | present | compare to recorded issuer, simple string comparison |
| `false` or absent | absent | **proceed** |

**THE FOURTH ROW IS THE WHOLE BOUNDARY CONDITION.** A client talking to an authorization server that neither advertises nor emits `iss` is required to carry on with no mix-up protection at all. The control is therefore contingent on the *other party*, and a general-purpose MCP client — which by design talks to many authorization servers it does not operate — cannot unilaterally obtain it. That matches what the tutorial page says about the same mitigation: "This mitigation depends on honest authorization servers emitting `iss`; it provides no protection against an honest server that does not." The reading that this constitutes a fail-open default, and the consequence for client authors, is this pack's framing; the spec presents the table without comment.

The third row is the deliberate exception: the spec compares a present `iss` regardless of advertisement, applying RFC 9207 §2.4's local-policy provision "to accommodate authorization servers that emit `iss` before updating their metadata".

**THE COMPARISON RULE IS THE EASIEST THING HERE TO BREAK BY BEING HELPFUL.** After decoding `iss` from the `application/x-www-form-urlencoded` response, clients **MUST NOT** apply "scheme or host case folding, default-port elision, trailing-slash, or percent-encoding normalization" before comparison. Every mainstream URL library does at least one of those by default, and a round-trip through a URL type is enough to violate it. The required comparison is RFC 3986 §6.2.1 simple string comparison — octet-for-octet on the decoded value.

**ERROR RESPONSES ARE IN SCOPE.** "This validation applies equally to error responses - on mismatch the client **MUST NOT** act on or display `error`, `error_description`, or `error_uri`." An unvalidated error channel is an attacker-controlled string rendered in the client's UI, which is why the rule covers display and not just action.

**FORWARD NOTICE THE SPEC GIVES ITSELF.** "A future revision of this specification is expected to upgrade authorization server inclusion of `iss` from **SHOULD** to **MUST**." Client rejection behaviour on `iss` absence stays keyed on the metadata flag until then. Emit and validate `iss` now if you operate either side.

**SOURCING.** Read from the specification repository on branch `main` (`docs/specification/2026-07-28/basic/authorization/index.mdx`, §Authorization Response Validation, and `.../security-considerations.mdx`, §Mix-Up Attacks). `main` is the live editing branch rather than a release tag; the frozen revision directory should be stable, but exact strings are worth re-confirming against the rendered page. The table above is a markdown table in the source `.mdx`, not a PDF extraction, so its row/cell pairings are reliable.
