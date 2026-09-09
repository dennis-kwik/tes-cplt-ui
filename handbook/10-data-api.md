# 10. Data Model, Database, dan API
Sheet gabungan lintas-modul: `Data_API`.

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
* Backward compatibility, deprecated field, consumer migration window.

Setiap baris wajib mereferensikan Component ID/Field ID pada sheet Desain UI modul terkait agar tetap tertelusur meski berada di sheet terpisah.
