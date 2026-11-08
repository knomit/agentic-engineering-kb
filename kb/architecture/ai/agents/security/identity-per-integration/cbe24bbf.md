---
type: pattern
domain: [agentic-engineering, security, architecture, authorization, tools, operations, multi-agent]
confidence: 0.8
sources: 1
entities: [LangChain, Deep Agents, Managed Deep Agents, on-behalf-of, OBO, service account, GitHub app identity, Salesforce, Notion, surface-scoped tools, whitelist]
motifs: [identity-chosen-per-integration, shared-credential-ungated]
refs: ['https://www.langchain.com/blog/components-building-company-harness', 'kb://bc6eac5f37df/kb/conventions/ai/agents/security/authorization/7b1488e3.md', 'kb://bc6eac5f37df/kb/invariants/ai/agents/security/authorization/48c4e555.md', 'kb://bc6eac5f37df/kb/architecture/ai/agents/security/identity/069468bb.md']
---
# One agent carries several identities, chosen per integrated service rather than per agent — on-behalf-of where the action is attributable to the asker, a fixed company credential where it is not, with the risky tools gated by surface and whitelist

A team running three internal agents published its identity model, and the unit of decision is the INTEGRATION, not the agent. Each agent holds on-behalf-of (OBO) authority for some services and its own fixed identity for others, in the same agent. The team calls identity "the thorniest and trickiest problem" of the five components it names.

The three worked examples, as published:
- A coding agent "acts on behalf of the user when messaged, and uses its own GitHub app identity when running in the background." So the same agent switches identity by whether a human initiated this run — there is no user to act for on a scheduled run, and borrowing the last user's authority for one would be wrong.
- A go-to-market agent "uses a fixed identity for Salesforce", while "Its email tools act on behalf of the user and are ONLY available in DMs."
- A content agent "acts on behalf of the user for Notion", and for the company's public social account "it uses a fixed set of company credentials" where "Only a whitelisted set of users can invoke certain operations."

THREE DESIGN RULES ARE VISIBLE IN THOSE CHOICES. First, pick OBO when the action should be attributable to, and bounded by, the person asking — reading their mail, writing in their document. Pick a fixed service identity when the action belongs to the organisation rather than the asker, such as posting publicly or writing to a shared CRM, which also keeps the agent's reach from varying with whoever happened to ask. Second, a fixed shared credential removes per-user bounds, so it needs a separate authorisation list of its own: the whitelist on the social-account operations exists because the credential itself grants everything.

Third, and the sharpest detail: TOOL AVAILABILITY IS SCOPED BY CONVERSATION SURFACE. The email tools exist only in direct messages. The reason is that OBO authority in a shared channel is ambiguous — several people can address the agent there, and a tool reaching one person's private mailbox should not be invocable in a room where others can trigger it. Surface is therefore part of the permission decision, not just part of the user experience.

The operational consequence: do not model "the agent's permissions" as one set. Model a matrix of agent by service, with an identity mode in each cell, and treat the invocation surface and the initiating trigger as inputs to which cells are live for this call.

WHAT THIS DOES NOT MEAN: choosing OBO does not make a call authorised. The identity only says whose authority is being presented; the downstream service still has to enforce it, and orchestrator-side filtering of which tools are offered is not authorisation. Scope: this is one team's description of its own internal deployment, with no incident or measurement attached — the reasoning for each choice is reconstructed from the published configuration rather than stated as a rule by the source.
