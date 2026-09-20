---
generated: '2026-09-19'
method: generated
name: Verify a mandate before relying on it
description: Given a contract id, hash or reader link, prove the document is untampered, read what it authorizes, and check that the authority is in force right now.
api: mcp/getamber-dev-mcp.yml
operations: [ambr_verify_hash, ambr_get_contract, ambr_get_contract_status, 'GET /api/v1/contracts/{id}/status']
source: >-
  MCP tool names and inputSchemas verified verbatim in mcp/getamber-dev-mcp-tools.json; hash scheme from
  https://ambr.run/spec/ricardian-v1; validity semantics from https://getamber.dev/developers.
---

# Verify a mandate before relying on it

A counterparty agent presenting an Ambr contract is presenting a claim of authority. Three checks turn it into something you can act on: integrity, content, and current validity. All three are free and need no credential for metadata; the full text needs the creator's key or the share token in the `reader_url`.

## Steps
1. **Integrity** — `ambr_verify_hash {hash}` (64-hex SHA-256). `verified: true` means Ambr holds a contract with that hash; the response includes `contract_id`, `status`, `reader_url`. If you hold both payloads, recompute independently per the spec: `sha256_hex(utf8(prose + "\n---\n" + canonical_json))` with keys sorted at every depth and no whitespace — a match needs no trust in Ambr.
2. **Content** — `ambr_get_contract {id}` (contract id, hash or UUID; REST `GET /api/v1/contracts/{id}`). Anonymous calls return metadata only (id, status, hash, dates); with the creator key or `?token=` share token you get `human_readable`, `machine_readable`, `principal_declaration` and the terms. Read scope, spending caps, duration, governing law and `principal_declaration` — who is actually liable.
3. **Validity now** — `ambr_get_contract_status {id}` or the public `GET /api/v1/contracts/{id}/status`. Act only when `is_currently_valid` is `true`; also inspect `is_expired`, `revoked_at`, `expiry_date` and the `amendments[]` / `amendment_chain` — an `amended` contract has been superseded by a child with a new hash, so verify the newest link.
4. **Human-oversight gates** — if the mandate sits at `awaiting_principal_approval`, a human still has to sign; do not treat it as authority.

## Errors
- `404 not_found` (REST) or an MCP `isError` text "Contract '…' not found." — the id/hash is unknown to Ambr; treat the claim as unverified.
- The MCP and A2A surfaces return HTTP 200 with JSON-RPC errors; check `error.code` / `result.isError`, not the status line. See `errors/getamber-dev-problem-types.yml`.

## Notes
- Hash verification "confirms technical integrity ... does NOT constitute legal certification, notarization, authentication of identity, or validation of contract terms" (Terms §8). Identity of the parties is a wallet address; ZK identity attestations, where present, are the trust signal.
