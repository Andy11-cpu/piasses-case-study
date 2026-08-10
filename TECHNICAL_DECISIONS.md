# PIASSES Technical Decisions

## 1. Make canonical financial meaning provider-neutral

Provider payloads are treated as observations, not as the canonical domain model. Balance signs, transaction direction, record identity, and absence semantics are normalized into explicit contracts.

## 2. Model absence as a closed state machine

`missing`, `unknown`, `unsupported`, `redacted`, `not applicable`, and genuine values are distinct. This prevents downstream code from treating absence as zero or assuming every provider can supply every field.

## 3. Preserve field-level provenance

Financially consequential fields retain references to the observations that support them. Provenance is part of the record contract rather than an optional debug appendix.

## 4. Put REST and MCP over one application service

Transport parity is architectural. Neither REST nor MCP may bypass policy, call repositories directly, or invent separate authorization semantics.

## 5. Treat consent as active runtime authority

Consent revocation changes what may be read immediately while preserving historical audit and record state. Authorization checks happen at execution time rather than being assumed from a previously issued token alone.

## 6. Validate persisted scopes as one closed set

One unknown, malformed, case-changed, or whitespace-padded scope invalidates the credential. Ignoring unexpected persisted authority would make the system permissive exactly where it should be conservative.

## 7. Persist idempotency, not merely request IDs

Idempotency state binds workspace, actor, capability, and validated payload identity. Equal retries return the same result. Reusing a key with a different request is a conflict.

## 8. Keep deterministic intelligence deterministic

The financial intelligence layer performs factual transformations over canonical data. It does not smuggle recommendations, forecasts, confidence scores, or generated advice into a system whose evidence only supports deterministic analysis.
