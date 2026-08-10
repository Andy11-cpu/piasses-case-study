# PIASSES Validation

PIASSES validates contracts at several layers because transport correctness, financial correctness, and persistence correctness are different properties.

## Contract validation

Request and output schemas are strict. Unknown fields are rejected. Canonical records enforce lifecycle, provenance, relation, money, and value-state invariants at parse time.

## Cross-interface parity

The same capabilities are exercised through REST and MCP against one application core. Authorization, consent, output validation, and audit behavior are expected to remain equivalent across both transports.

## PostgreSQL validation

Database tests cover durable tenancy, credentials, consent, canonical records, idempotency, migration behavior, audit, restart durability, and concurrency-sensitive paths.

## Conformance testing

A fictional institution API and closed conformance suite exercise HTTP behavior and provider adapter expectations without requiring live bank connectivity. The adapter boundary is therefore testable before any production provider is introduced.

## Security-oriented checks

Validation includes:

- fail-closed credential resolution
- closed persisted-scope registry
- timing-safe verifier comparison
- no plaintext bearer-secret persistence
- workspace-scoped target resolution
- consent revocation across both interfaces
- idempotent write replay
- sanitized audit events
- host and request-size guards

## Claim boundary

The current repository proves a locally runnable sandbox, persistent financial-data contracts, REST/MCP parity, institution conformance tooling, and deterministic intelligence over synthetic data.

It does not prove live institution connectivity, production identity, production deployment, or end-to-end live bank ingestion. Those remain separate milestones rather than implied extensions of the sandbox evidence.
