# 15. What-If Scenario Library
* Channel expansion: Web/Mobile bertambah tablet, partner API, offline, channel dinamis. Hindari boolean per channel; evaluasi master+assignment; feature flag; channel capability.
* Role/workflow: Single role menjadi maker-checker, approval bertingkat, delegation, SoD. Status machine, transition authorization, approval history, editability per status.
* Principal hierarchy: Single principal menjadi hierarchy, inheritance, mass assignment. Reference by ID; hierarchy version/effective date; snapshot vs latest semantics.
* Volume 10x/100x: Grid, search, export, delete, assignment menjadi besar. Server pagination; index; async export; batch; archive; performance test.
* Business code evolution: Initial length/format/scope berubah atau generated ID. Pisahkan surrogate key dari business code; migration dan alias/history.
* Temporal complexity: Open-ended, timezone, backdate, correction, future approval. Effective dating model; inclusive boundary; versioned history; conflict policy.
* Deletion governance: Hard delete menjadi soft delete, restore, retention/legal hold. Lifecycle status; deleted audit; uniqueness with deleted rows; purge job.
* Integration evolution: Sync menjadi event-driven atau multi-consumer. Versioned event; idempotent consumer; DLQ; replay; reconciliation.
* API evolution: Schema berubah dan consumer lama masih aktif. Version policy; additive changes; deprecation; contract tests; compatibility window.
* Migration/import: Bulk upload, merge/split entity, historical load. Staging; validation report; dry run; restartable batch; rollback; reconciliation.
* Concurrency: Banyak editor, batch dan API mengubah record sama. Version/ETag; conflict strategy; idempotency; lock scope.
* Outage/resilience: Dependency lambat/down; partial outage; DR. Timeout, retry/backoff, circuit breaker, degraded mode, recovery test.
* Localization/accessibility: Bahasa, date, timezone, long labels, keyboard-only. Locale-aware display; invariant storage; flexible layout; a11y acceptance.
* Regulation/privacy: Retention, masking, encryption, access review berubah. Policy-driven retention; classification; key management; audit evidence.
* Delivery model: Feature flag, phased rollout, rollback, A/B, parallel run. Config audit; backward-compatible DB; telemetry; rollback criteria.
* Rule configurability: Hardcoded rule menjadi configuration-driven. Versioned configuration; effective date; approval; validation; audit; simulation.