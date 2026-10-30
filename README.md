# Ambr

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Ambr (ambr.run; platform and API host getamber.dev) is the "Agent Mandate & Binding Registry" — an agent-native service that creates, signs, verifies and revokes Ricardian contracts for AI agents: delegation mandates recording who authorized an agent, in what scope and under which law, plus agent-to-agent commerce and agent-to-consumer agreements. Every contract is dual-format — legal prose and machine-parsable JSON bound by one SHA-256 hash (urn:ambr:ricardian-v1, MIT) — and once signed by both wallets is minted as an ERC-721 cNFT on Base L2. The surface is a JSON REST API at getamber.dev/api/v1 with a public pricing endpoint, a remote MCP server at /api/mcp (six tools, anonymous tools/list) and an A2A JSON-RPC endpoint discovered via /.well-known/agent-card.json. Auth is an X-API-Key, x402 pay-per-contract on Base, or an ECDSA wallet signature; 25 free developer contracts. No OpenAPI or SDK is published. Not Amber International (Nasdaq: AMBR).

**Areas:** Company · AI Agents · Agentic Commerce · Contracts · Legal · Ricardian Contracts · Delegation · Blockchain · Base L2 · MCP · A2A · x402

## Ambr on APIs.io

Everything profiled for Ambr is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/getamber-dev/](https://apis.io/providers/getamber-dev/)** — or go straight to one of the APIs or properties below.

### APIs (3)

- [Ambr REST API](https://apis.io/apis/getamber-dev/ambr-rest-api/) — JSON REST API at https://getamber.dev/api/v1 for the full mandate lifecycle: list templates (public), create a contract from a template (X-API-Key with…
- [Ambr MCP Server](https://apis.io/apis/getamber-dev/ambr-mcp-server/) — One remote Model Context Protocol server at https://getamber.dev/api/mcp — Streamable HTTP in stateless JSON mode, protocol version 2025-03-26, serverInfo…
- [Ambr A2A Agent](https://apis.io/apis/getamber-dev/ambr-a2a-agent/) — Agent-to-Agent JSON-RPC endpoint at https://getamber.dev/api/a2a implementing message/send, tasks/get and tasks/cancel (tasks are processed synchronously),…

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [getamber-dev-mcp.yml](https://apis.io/servers/getamber-dev/getamber-dev-mcp-yml/)

#### JSON Schema (6)

The data models the API reads and writes.

- [Getamber Dev C1 Api Access](https://apis.io/schemas/getamber-dev/getamber-dev-c1-api-access/)
- [Getamber Dev C2 Compute Sla](https://apis.io/schemas/getamber-dev/getamber-dev-c2-compute-sla/)
- [Getamber Dev C3 Task Execution](https://apis.io/schemas/getamber-dev/getamber-dev-c3-task-execution/)
- [Getamber Dev D1 General Auth](https://apis.io/schemas/getamber-dev/getamber-dev-d1-general-auth/)
- [Getamber Dev D2 Limited Service](https://apis.io/schemas/getamber-dev/getamber-dev-d2-limited-service/)
- [Getamber Dev D3 Fleet Auth](https://apis.io/schemas/getamber-dev/getamber-dev-d3-fleet-auth/)

#### Examples (1)

Example requests and responses.

- [Getamber Dev Templates Response](https://apis.io/examples/getamber-dev/getamber-dev-templates-response/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Getamber Dev Authentication](https://apis.io/security/getamber-dev/getamber-dev-authentication/)
- [Getamber Dev Domain Security](https://apis.io/security/getamber-dev/getamber-dev-domain-security/)
- [Getamber Dev Vulnerability Disclosure](https://apis.io/security/getamber-dev/getamber-dev-vulnerability-disclosure/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Getamber Dev Plans Pricing](https://apis.io/plans/getamber-dev/getamber-dev-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Getamber Dev Rate Limits](https://apis.io/rate-limits/getamber-dev/getamber-dev-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://ambr.run/)
- [Documentation](https://getamber.dev/docs)
- [Getting started](https://getamber.dev/docs)
- [API reference](https://getamber.dev/developers)
- [Pricing](https://getamber.dev/activate)
- [Sign up](https://getamber.dev/activate)
- [Support](https://discord.com/invite/HjvJFfjr)
- [Changelog](https://github.com/getambr/ambr/blob/master/CHANGELOG.md)
- [Terms of service](https://ambr.run/terms)
- [Privacy policy](https://ambr.run/privacy)
- [GitHub](https://github.com/getambr)
- [Status](https://ambr.run/status)

## API Evangelist rating

**Kin Score 53.7** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 80.0 |
| Contract quality | 18.5 |
| Contract governance | 18.2 |
| Operational transparency | 68.4 |
| Developer ergonomics | 56.5 |
| Access clarity | 76.3 |

**Agent readiness 15.0** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | — |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | documented (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | documented (partial credit) |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | flavored (partial credit) |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | na |

**Regulatory alignment 38.2** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/getamber-dev/](https://apis.io/providers/getamber-dev/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Ambr: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/getamber-dev/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
