# PIASSES Validation

PIASSES validates contracts at several layers because transport correctness, financial correctness, authorization correctness, and persistence correctness are different properties.

## Capability and authorization registry

The current application core exposes **12 canonical capabilities** backed by **12 client authorization scopes**. The MCP side includes **six resource templates** plus explicit mutation tools where write authority and idempotency matter.

The registry is closed. Unknown persisted scopes do not coexist with a valid credential; the complete credential fails resolution instead.

## Cross-interface parity

REST and MCP both call one shared journey service rather than implementing parallel business logic. That common path owns:

- workspace-scoped target resolution
- authorization-context construction
- fail-closed policy evaluation
- capability execution
- output-schema validation
- one sanitized audit event per invocation, including denials

The persisted runtime has been exercised across process restart with the same provisioned sandbox credential. Equivalent financial-intelligence reads work through REST and MCP, and consent revocation through either interface causes equivalent protected reads to fail closed through both.

## PostgreSQL evidence

The default runnable server uses PostgreSQL-backed repositories for organization and workspace tenancy, API clients and credential verifiers, sandbox consumers, consents, connections, canonical financial records, idempotency entries, and audit events.

Database tests exercise migration behavior, durable tenancy, credentials, consent, canonical records, idempotency, audit, restart durability, and concurrency-sensitive paths. Same-key writes serialize through a dedicated PostgreSQL advisory-lock namespace rather than relying on process-local memory.

## Exact-money and canonical-record validation

Canonical financial values use strict decimal-string money contracts. Provider sign conventions do not define economic meaning.

The six-state absence model is validated as part of the record schema:

1. present
2. missing from source
3. unknown
4. not applicable
5. unsupported by source
6. redacted

Canonical records also require provenance and correction lineage. Financially consequential fields are tied to source observations, and corrected records preserve the prior version internally instead of rewriting history.

## Credential and security checks

Validation covers:

- fail-closed credential resolution
- the closed persisted-scope registry
- HMAC-SHA256 secret verification
- timing-safe verifier comparison
- no plaintext bearer-secret persistence
- workspace-scoped target resolution
- consent revocation across both interfaces
- idempotent write replay and conflict detection
- sanitized audit events
- Host-header and bounded request-body guards

## Institution conformance

A fictional institution HTTP service and a closed conformance testkit exercise institution wire behavior and provider-adapter expectations without requiring live bank connectivity.

That layer proves the conformance and adapter boundary. It does not silently claim the remaining bridge from source observations into durable canonical records. Raw institution payloads in the current conformance path remain quarantined from canonical product state.

## A persistence correction

The first end-to-end developer journey was proven against in-memory deterministic state. That established protocol shape, but it could not prove restart durability, persisted authorization, transactional idempotency, or exactly-once audit ownership.

The default runnable path was therefore moved to PostgreSQL and the in-memory runtime retained only for fast protocol tests. This is an example of a proof boundary becoming an architecture correction rather than a marketing claim.

## Claim boundary

The current repository proves a locally runnable sandbox, persistent financial-data contracts, REST/MCP parity over one application core, consent and credential enforcement, institution conformance tooling, and deterministic intelligence over synthetic canonical data.

It does not prove live institution connectivity, production identity, production deployment, or end-to-end live bank ingestion.
