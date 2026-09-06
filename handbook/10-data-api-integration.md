# 10. Data Model, Database, API, dan Integration

## 10.1 Data model checklist
* Entity, primary key, business key, relation, cardinality, ownership.
* Nullability, default, unique scope, normalization, status lifecycle.
* Effective dating, overlap policy, historical truth, versioning.
* Soft/hard delete, restore, retention, archive, legal hold.
* Indexes untuk search, filter, sort, uniqueness, dan effective date.
* Migration strategy, data quality, duplicate resolution, rollback.

## 10.2 API contract checklist
* Endpoint purpose dan version.
* Request/response schema, enum, max length, date format.
* Server validation owner dan stable error code.
* Pagination, filter, sort, query limit.
* Idempotency key, optimistic version, ETag bila relevan.
* Backward compatibility, deprecated field, consumer migration window.
* Timeout, retry, correlation ID, observability.

## 10.3 Integration modes
* Synchronous: Timeout, duplicate retry, coupling (Risiko); Timeout, retry policy, idempotency, error mapping (Spec wajib).
* Asynchronous/Event: Duplicate/out-of-order/lost event (Risiko); Event ID, schema version, idempotent consumer, DLQ, replay (Spec wajib).
* Batch/File: Partial row failure, format drift (Risiko); Schema, checksum, row result, restartability, reconciliation (Spec wajib).
* Master Data: Stale cache, deleted reference (Risiko); Source of truth, refresh cadence, inactive handling (Spec wajib).