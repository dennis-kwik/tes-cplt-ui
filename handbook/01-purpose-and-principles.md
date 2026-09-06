# 1. Mandat, Prinsip, dan Definition of Done
Handbook ini menetapkan standar kedalaman analisis, struktur deliverable, dan future-proof thinking untuk UI Technical Blueprint Copilot. Blueprint tidak boleh berhenti pada dokumentasi tampilan. Blueprint wajib menghubungkan tujuan bisnis, perilaku UI, service logic, data integrity, keamanan, audit, testing, dan dampak perubahan masa depan. 
Prinsip desain utama adalah satu modul sama dengan satu sheet spesifikasi lengkap. Pemisahan artefak berdasarkan jenis hanya dilakukan jika volume, penggunaan lintas-modul, atau kebutuhan tooling memberikan manfaat yang jelas. 
Dua keputusan utama: 1) Kedalaman lintas-fungsi menjadi output default, bukan enrichment setelah user meminta detail. 2) Spec, Field Matrix, Message Catalog, Data/API Mapping, Security, Test Scenario, dan Future Impact dikonsolidasikan sebagai section dalam satu module sheet.

## 1.1 Audiens dan Kebutuhan
* BA/PO: Scope, invariant, rule IF-THEN, exception, assumption, decision, risk, acceptance intent.
* Frontend: Component state, event, validation, permission, loading/error/empty state, message placement.
* Backend: Server-side rule, authorization, transaction, concurrency, idempotency, error contract.
* Database: Entity, key, relation, constraint, effective dating, indexing, retention, migration.
* Security/Privacy: Access control, validation, encoding, audit, classification, masking, retention.
* QA: Positive, negative, boundary, security, concurrency, integration, migration, compatibility tests.
* Support/Ops: Logging, correlation ID, monitoring, recovery, reconciliation, supportable error behaviour.
* Future Team: Business invariant, decision history, extension point, what-if impact, backward compatibility.

## 1.2 Definition of Done
* Seluruh input dan semua sheet dipindai.
* Seluruh screen, state, field, icon, action, dan visual cue tercatat.
* Business invariant dipisahkan dari current state dan proposed design.
* Business Rules, Field Matrix, Message Catalog, Data/API Mapping, Security, NFR, What-If, Test, dan Traceability tersedia.
* Asumsi diberi ID, warna kuning, alasan, impact, dan pihak konfirmasi.
* Critical rule mempunyai test coverage.
* Workbook dapat dibuka di Microsoft Excel dan nyaman direview lintas fungsi.