---
generated: '2026-09-19'
method: generated
name: Create and activate an Agent Mandate
description: Pick a template, create a dual-format Ricardian contract, get the counterparty's handshake, collect the wallet signatures that activate it, and confirm it is in force.
api: mcp/getamber-dev-mcp.yml
operations: [ambr_list_templates, ambr_create_contract, ambr_agent_handshake, 'POST /api/v1/contracts/{id}/sign', ambr_get_contract_status]
source: >-
  MCP tool names, inputSchemas and annotations verified verbatim in mcp/getamber-dev-mcp-tools.json
  (live tools/list, 2026-09-19); REST paths and lifecycle rules from https://getamber.dev/docs and
  https://getamber.dev/developers.
---

# Create and activate an Agent Mandate

An Agent Mandate is a contract that records who authorized an agent, in what scope, under which law. It is created as a `draft`, negotiated by handshake, and activated by ECDSA wallet signatures. Creating one costs money (1 credit, or an x402 payment) and there is no undo — read `conventions/getamber-dev-conventions.yml` § reversibility first.

## Auth
- Send `X-API-Key` (an `amb_` key with credits) on the MCP HTTP request or the REST call. Without a key, `ambr_create_contract` returns an x402 payment challenge (JSON-RPC `-32001`, or HTTP 402 on REST) — pay on Base L2 and retry with the tx hash in `X-Payment`. See `authentication/getamber-dev-authentication.yml`.
- Read-only tools (`ambr_list_templates`, `ambr_get_contract_status`) need no credential.

## Before you spend
- Fetch live prices from `GET https://getamber.dev/api/v1/pricing` — the card and llms.txt say "do not hardcode prices". See `plans/getamber-dev-plans-pricing.yml`.
- There is no idempotency key. A retried create is a second contract and a second charge (`conventions` § idempotency). Do not retry a create on a timeout without first checking whether it landed.

## Steps
1. **Choose a template** — `ambr_list_templates` (no arguments; REST `GET /api/v1/templates`). Read the template's `parameter_schema` (`required[]`, enums, defaults) and `price_cents`. Delegation templates are `d1-general-auth`, `d2-limited-service`, `d3-fleet-auth`, `p2-power-of-attorney`; commerce `c1-api-access`, `c2-compute-sla`, `c3-task-execution`; consumer `a1`–`a3`.
2. **Create the contract** — `ambr_create_contract` (REST `POST /api/v1/contracts`) with `template`, `parameters` conforming to that schema, and `principal_declaration {agent_id, principal_name, principal_type: company | individual}`. Optional: `parent_contract_hash` + `amendment_type` for an amendment, `oversight_threshold_usd` to hold child contracts above a spend level at `awaiting_principal_approval` until a human signs. Capture `contract_id` (`amb-YYYY-NNNN`), `sha256_hash`, `reader_url`, `sign_url`, `handshake_url`. A `400 validation_error` lists every failing path in `details[]` — fix the parameters, do not guess.
3. **Share** — send `reader_url` (it embeds a time-limited share token) to the counterparty so they can read the full terms without an API key.
4. **Handshake** — the counterparty accepts, rejects or requests changes at `POST /api/v1/contracts/{id}/handshake` `{action, visibility, wallet_address}`. If YOU are the delegated agent acting for a principal, use `ambr_agent_handshake` `{contract_id, intent: accept | reject | request_changes, message?, visibility_preference?}` — it needs a key with an active delegation (`/api/v1/delegations`), and the principal must still approve by wallet signature. `accept` moves `draft → pending_signature`; `request_changes` keeps `draft`.
5. **Sign** — `POST /api/v1/contracts/{id}/sign` `{wallet_address, signature, message}` where `message` names the contract and contains its SHA-256 hash (developers page shows the exact format). Bilateral templates need both parties: first signature → `pending_signature`, second → `active` and the cNFT mints on Base. `p2-power-of-attorney` activates on the principal's single signature.
6. **Confirm it is in force** — `ambr_get_contract_status` (or public `GET /api/v1/contracts/{id}/status`). Trust `is_currently_valid`, not `status` alone: expiry is derived and `status` may still read `active` after `expiry_date`.

## Errors
- `401 unauthorized` — missing/invalid key; `402` / `-32001` — pay or add credits; `409 invalid_state` / `422 invalid_status` — the action is not allowed in the current state, re-read status; `429 rate_limited` — back off for `retry_after_ms` (revoke is 5/min/IP). Full catalog: `errors/getamber-dev-problem-types.yml`.

## Ending a mandate
- `POST /api/v1/contracts/{id}/revoke` (key, or a wallet signature stating revocation intent with the hash) while `active`, `pending_signature` or `handshake`. It is terminal and cascades to child delegations. Nothing un-creates a contract.
