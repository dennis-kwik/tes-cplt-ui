UI TECHNICAL
BLUEPRINT
KNOWLEDGE HANDBOOK
Standar Production-Ready, Future-Proof, dan What-If Driven


Tujuan dokumen
Knowledge source komprehensif untuk Microsoft 365 Copilot Agent yang mengubah screenshot, mockup, wireframe, atau Excel UI menjadi spesifikasi teknis lintas-fungsi. Dokumen ini melengkapi instruksi operasional agent yang dibatasi 8.000 karakter.

Metadata	Nilai
Document Owner	Corporate Development / Business Analysis
Document Type	Agent Knowledge Standard and Technical Blueprint Handbook
Recommended Agent Instruction	Gunakan instruksi operasional ringkas maksimal 8.000 karakter
Knowledge Usage	Upload dokumen ini sebagai knowledge source agent
Default Deliverable	Excel .xlsx; Index_Summary + satu consolidated spec sheet per modul
Detail Level	BA/PO, Frontend, Backend, Database, Security, QA, Support, Future Redevelopment
Status	Baseline lengkap; organisasi dapat menambahkan policy dan convention internal


 Daftar Isi
Bagian	Judul
1	Mandat, Prinsip, dan Definition of Done
2	Arsitektur Agent: Instructions vs Knowledge
3	Cara Membaca Input Visual dan Excel
4	Metode Discovery Modul, Screen, State, dan Komponen
5	Business Intent, Invariants, Current State, dan Proposed Design
6	Business Rules dan Conditional Logic
7	Functional UI Specification Standard
8	Detailed Field Matrix Standard
9	Message Catalog Standard
10	Data Model, Database, API, dan Integration
11	Security, Privacy, Audit, dan Operability
12	Concurrency, Transaction, Idempotency, dan Resilience
13	Non-Functional Requirements
14	What-If and Future Change Framework
15	What-If Scenario Library
16	Testing Strategy dan Traceability
17	Workbook Architecture dan Formatting
18	Assumption, Decision, Risk, dan Open Question Governance
19	Quality Gate dan Review Checklist
20	Contoh Penerapan DSCAMxxx
21	Operational Prompt Maksimum 8.000 Karakter
Lampiran A	Component and Validation Reference
Lampiran B	ID Convention and Status Vocabulary
Lampiran C	Reusable Table Templates


 1. Mandat, Prinsip, dan Definition of Done
Handbook ini menetapkan standar kedalaman analisis, struktur deliverable, dan future-proof thinking untuk UI Technical Blueprint Copilot. Blueprint tidak boleh berhenti pada dokumentasi tampilan. Blueprint wajib menghubungkan tujuan bisnis, perilaku UI, service logic, data integrity, keamanan, audit, testing, dan dampak perubahan masa depan.
Prinsip desain utama adalah satu modul sama dengan satu sheet spesifikasi lengkap. Pemisahan artefak berdasarkan jenis hanya dilakukan jika volume, penggunaan lintas-modul, atau kebutuhan tooling memberikan manfaat yang jelas.
Dua keputusan utama
1) Kedalaman lintas-fungsi menjadi output default, bukan enrichment setelah user meminta detail. 2) Spec, Field Matrix, Message Catalog, Data/API Mapping, Security, Test Scenario, dan Future Impact dikonsolidasikan sebagai section dalam satu module sheet.

1.1 Audiens dan kebutuhan
Audiens	Kebutuhan minimum dari blueprint
BA/PO	Scope, invariant, rule IF-THEN, exception, assumption, decision, risk, acceptance intent.
Frontend	Component state, event, validation, permission, loading/error/empty state, message placement.
Backend	Server-side rule, authorization, transaction, concurrency, idempotency, error contract.
Database	Entity, key, relation, constraint, effective dating, indexing, retention, migration.
Security/Privacy	Access control, validation, encoding, audit, classification, masking, retention.
QA	Positive, negative, boundary, security, concurrency, integration, migration, compatibility tests.
Support/Ops	Logging, correlation ID, monitoring, recovery, reconciliation, supportable error behaviour.
Future Team	Business invariant, decision history, extension point, what-if impact, backward compatibility.

1.2 Definition of Done
•	Seluruh input dan semua sheet dipindai.
•	Seluruh screen, state, field, icon, action, dan visual cue tercatat.
•	Business invariant dipisahkan dari current state dan proposed design.
•	Business Rules, Field Matrix, Message Catalog, Data/API Mapping, Security, NFR, What-If, Test, dan Traceability tersedia.
•	Asumsi diberi ID, warna kuning, alasan, impact, dan pihak konfirmasi.
•	Critical rule mempunyai test coverage.
•	Workbook dapat dibuka di Microsoft Excel dan nyaman direview lintas fungsi.

 2. Arsitektur Agent: Instructions vs Knowledge
Copilot Agent Builder memiliki ruang instructions yang terbatas. Gunakan instructions untuk perilaku operasional dan knowledge ini untuk standar mendalam, contoh, taksonomi, serta reusable reference.
Lapisan	Isi	Jangan dimasukkan
Instructions ≤ 8.000 karakter	Role; dua prinsip utama; urutan proses; struktur workbook; mandatory sections; quality gate.	Contoh panjang, scenario library lengkap, semua template kolom.
Knowledge document	Metodologi; what-if library; standard validation; templates; examples; governance.	Instruksi yang bertentangan dengan operational prompt.
User input	Mockup; requirement; confirmed rules; konteks proyek.	Keputusan tersembunyi tanpa source/status.
Output workbook	Evidence dan spec per modul.	Penjelasan generik yang tidak terhubung ID.

Precedence
Urutan prioritas: instruksi eksplisit user/project → confirmed business rule → existing behaviour yang tervalidasi → visual evidence → proposed best practice sebagai asumsi.


 3. Cara Membaca Input Visual dan Excel
3.1 Visual inspection
•	Baca judul, kode modul, section band, label, tanda mandatory, placeholder, sample value, border, alignment, warna, icon, selection state, dan grouping.
•	Periksa elemen kecil: pencil, eye, calendar, search, row checkbox, sort marker, pagination, helper text, dan empty region yang mungkin merupakan container.
•	Bedakan informasi yang terlihat dengan inferensi. Catat evidence visual dan confidence bila diperlukan.
•	Lakukan second-pass verification sebelum menyusun component inventory.
3.2 Excel inspection
•	Scan setiap sheet, termasuk hidden sheet bila dapat diakses.
•	Deteksi beberapa desain dalam satu sheet melalui dark header, merged title, whitespace, border, dan label Main Page/Add/Edit/Detail/Popup/Tab.
•	Pertahankan grouping berdasarkan kode modul, bukan berdasarkan jenis artefak.
•	Jangan menganggap cell kosong tidak penting. Layout, merged cells, shape, dan visual grouping dapat membawa makna.
3.3 Evidence classification
Status	Definisi	Treatment
CONFIRMED	Diberikan eksplisit oleh user atau dokumen approved.	Tuliskan sebagai requirement; sertakan source.
OBSERVED	Terlihat pada UI/existing system tetapi belum dikonfirmasi sebagai target.	Tuliskan sebagai current state.
INFERRED	Kesimpulan logis dari beberapa evidence.	Jelaskan dasar inferensi; tandai untuk review.
PROPOSED	Rekomendasi teknis atau future-proof design.	Jangan tulis sebagai business fact.
ASSUMPTION	Diperlukan untuk melengkapi spec tetapi belum diketahui.	Kuning; ID; reason; impact; confirm by.
OPEN	Belum dapat diputuskan.	Masukkan Open Question dan impact.


 4. Metode Discovery Modul, Screen, State, dan Komponen
4.1 Output discovery
Objek	Atribut minimum
Module	Code, name, purpose, owner, entity, scope, dependency.
Screen	Screen ID, name, mode, entry/exit, related screen.
State	Initial, loading, add, edit, view, dirty, invalid, saving, error, conflict, unauthorized, not found.
Component	ID, label, type, screen, section, parent/container.
Action	Trigger, precondition, permission, validation, result, error, navigation.
Data	Source of truth, attribute, type, constraint, lifecycle.

4.2 State inventory
•	Initial: screen first render dan default values.
•	Loading: skeleton/spinner, disabled actions, timeout behaviour.
•	Add/Edit/View: field editability dan permission berbeda.
•	Dirty: unsaved changes dan navigation guard.
•	Saving: double-submit prevention dan idempotency.
•	Error/Conflict: recovery path, reload, retry, dan data preservation.
•	Unauthorized/Not Found: secure handling tanpa information leakage.

 5. Business Intent, Invariants, Current State, dan Proposed Design
Future-proof blueprint harus memisahkan apa yang tidak boleh berubah dari cara implementasi saat ini. Pemisahan ini mencegah redevelopment menyalin limitation UI lama sebagai business rule baru.
Layer	Pertanyaan	Contoh
Business Intent	Nilai bisnis apa yang ingin dicapai?	Mengontrol keterangan bon yang berlaku untuk principal dan periode tertentu.
Business Invariant	Apa yang harus tetap benar di semua teknologi/channel?	Tidak boleh ada dua aturan efektif yang ambigu untuk scope yang sama.
Current State	Bagaimana sistem/mockup saat ini bekerja?	Web dan Mobile ditampilkan sebagai dua checkbox.
Proposed Design	Bagaimana implementasi disarankan?	Gunakan Channel Master agar channel baru dapat ditambah tanpa schema change.
Constraint	Batas nyata apa yang berlaku?	Consumer lama membutuhkan field tertentu selama masa transisi.
Decision	Apa yang dipilih dan mengapa?	Gunakan soft delete karena audit dan restore diperlukan.

Anti-pattern
Jangan mengubah “UI memiliki dua checkbox Web/Mobile” menjadi invariant “sistem hanya boleh memiliki dua channel”. Invariant yang tepat adalah “minimal satu channel harus dipilih untuk activation”.


 6. Business Rules dan Conditional Logic
6.1 Struktur rule
Atribut	Isi
Rule ID	BR-[MODULE]-[NNN]
Name	Nama singkat yang stabil.
Source/Status	Confirmed, Observed, Inferred, Proposed, Assumption.
IF / Trigger	Kondisi pemicu.
AND / Preconditions	Kondisi tambahan, permission, state.
THEN / Result	Perubahan state/data/navigation.
ELSE / Exception	Fallback, error, partial failure.
Priority	Critical, High, Medium, Low.
Related IDs	Component, Message, Data, Risk, Test.

6.2 Rule domains
•	Lifecycle: Add, Edit, View, Submit, Approve, Reject, Activate, Expire, Delete, Restore.
•	Data integrity: mandatory, uniqueness, overlap, dependency, status transition.
•	Interaction: search, filter, sort, page, bulk action, selection, dirty state.
•	Security: role, segregation of duties, authorized scope.
•	Resilience: timeout, retry, duplicate request, partial failure, stale version.
•	Future: channel expansion, hierarchy, workflow, versioning, migration.
6.3 Rule example
BR-DSCAM-008
IF kombinasi business scope, assignment, channel, dan effective period menghasilkan lebih dari satu record efektif; THEN Save ditolak; AND conflicting record ditampilkan; UNLESS exception type yang dikonfigurasi mengizinkan overlap; related: FM-PERIOD-001, VAL-OVL-001, DATA-EFFECTIVITY-001, TC-OVL-001.


 7. Functional UI Specification Standard
Functional table utama mempertahankan tiga kolom agar cepat dibaca, sedangkan detail granular ditempatkan pada section Field Matrix pada sheet modul yang sama.
Elemen	Jenis Komponen	Behaviour/Deskripsi
Initial*	Text box	Mandatory; 1-10 karakter ASUMSI; uppercase; trim; unique case-insensitive; Add enabled; Edit read-only; Message VAL-INI-004.
Periode End*	Datepicker	Mandatory; DD/MM/YYYY; >= Start; overlap check; focus on invalid; Message VAL-DATE-004.
Save	Button	Permission Create/Edit; validate client+server; disable while processing; atomic save; stay in form; success SUC-SAVE-001.

7.1 Action completeness checklist
•	Purpose dan permission.
•	Visible/enabled/disabled condition.
•	Trigger dan precondition.
•	Client dan server validation.
•	Loading dan double-click behaviour.
•	Success, failure, navigation, focus, dan message.
•	Audit dan related API operation.

 8. Detailed Field Matrix Standard
Kolom	Tujuan
Component ID	Stable reference.
Screen/Section	Lokasi UI.
Field/Type	Label dan component type.
M/O/C/System	Required classification.
Data Type, Min/Max	Constraint eksplisit.
Format/Allowed Value	Regex, enum, character set.
Default/Placeholder	Initial presentation.
State	Enabled, disabled, hidden, read-only.
Validation	Client/server, cross-field, uniqueness.
Event/Behaviour	Click/change/blur/Enter/save.
Message ID	Reference ke catalog.
Permission	Role/action scope.
Data Attribute	Reference data/API.
Source/Assumption	Evidence status.

8.1 Standard validation questions
•	Apakah null, blank, whitespace-only, zero, dan omitted mempunyai arti berbeda?
•	Apakah uniqueness global atau scoped by company/principal/channel/status?
•	Apakah boundary date bersifat inclusive?
•	Apakah normalization dilakukan sebelum duplicate check?
•	Apakah field immutable setelah digunakan transaksi?
•	Apakah perubahan field memerlukan cascade, revalidation, atau approval?

 9. Message Catalog Standard
Prefix	Jenis	Kapan digunakan
VAL	Validation	Input atau rule invalid.
CNF	Confirmation	Aksi destructive atau discard.
SUC	Success	Proses selesai.
WRN	Warning	Boleh dilanjutkan dengan risiko.
ERR	Error	Kegagalan system/integration/concurrency.
INF	Information	Status atau empty state.

9.1 Message quality
•	Sebutkan masalah secara spesifik tanpa jargon teknis.
•	Berikan next action yang dapat dilakukan user.
•	Jangan bocorkan stack trace, SQL, internal ID sensitif, atau authorization detail.
•	Tempatkan inline untuk field error; modal untuk decision; toast untuk transient result.
•	Hubungkan message ke component, rule, logging requirement, dan test.

 10. Data Model, Database, API, dan Integration
10.1 Data model checklist
•	Entity, primary key, business key, relation, cardinality, ownership.
•	Nullability, default, unique scope, normalization, status lifecycle.
•	Effective dating, overlap policy, historical truth, versioning.
•	Soft/hard delete, restore, retention, archive, legal hold.
•	Indexes untuk search, filter, sort, uniqueness, dan effective date.
•	Migration strategy, data quality, duplicate resolution, rollback.
10.2 API contract checklist
•	Endpoint purpose dan version.
•	Request/response schema, enum, max length, date format.
•	Server validation owner dan stable error code.
•	Pagination, filter, sort, query limit.
•	Idempotency key, optimistic version, ETag bila relevan.
•	Backward compatibility, deprecated field, consumer migration window.
•	Timeout, retry, correlation ID, observability.
10.3 Integration modes
Mode	Risiko utama	Specification wajib
Synchronous	Timeout, duplicate retry, coupling.	Timeout, retry policy, idempotency, error mapping.
Asynchronous/Event	Duplicate/out-of-order/lost event.	Event ID, schema version, idempotent consumer, DLQ, replay.
Batch/File	Partial row failure, format drift.	Schema, checksum, row result, restartability, reconciliation.
Master Data	Stale cache, deleted reference.	Source of truth, refresh cadence, inactive handling.


 11. Security, Privacy, Audit, dan Operability
Domain	Pertanyaan wajib
Authorization	Siapa dapat View/Create/Edit/Delete/Approve? Apakah scope dibatasi principal/company?
Input security	Apakah server melakukan type, length, enum, ownership, dan injection validation?
Output security	Apakah output encoded dan sensitive field masked?
Privacy	Klasifikasi data, purpose, minimization, retention, deletion, access review?
Audit	Aksi apa dicatat; actor; UTC; old/new; reason; result; correlation ID?
Logging	Apa yang aman dicatat; bagaimana PII/token disensor; siapa dapat mengakses log?
Operational	Monitoring, alert, retry, reconciliation, runbook, support message?

Security invariant
UI hide/disable tidak pernah menjadi kontrol keamanan utama. Backend wajib melakukan authorization dan ownership/scope validation.


 12. Concurrency, Transaction, Idempotency, dan Resilience
Concern	Default proposed behaviour	Future question
Atomicity	Header dan detail disimpan dalam satu transaction.	Bagaimana jika proses melibatkan service eksternal?
Concurrency	Optimistic locking melalui version/ETag.	Apakah merge field-level diperbolehkan?
Double-submit	Disable action dan gunakan idempotency key.	Berapa lama key disimpan?
Partial failure	Rollback atau saga dengan compensation.	Apa acceptable partial state?
Retry	Retry hanya transient error dengan backoff.	Apakah operation idempotent?
Conflict	Jangan overwrite otomatis.	Reload, compare, atau manual merge?
Outage	Degraded mode dan clear recovery path.	Apakah offline queue diperlukan?


 13. Non-Functional Requirements
Quality	Specification examples
Performance	Response target, dataset assumption, percentile, page size, concurrent user.
Scalability	10x/100x volume, horizontal scale, indexing, partition/archive.
Availability	SLA, maintenance, graceful degradation, dependency failure.
Recovery	Backup, restore verification, RTO/RPO, replay/reconciliation.
Observability	Metrics, logs, traces, correlation, business counters, alarms.
Accessibility	Keyboard, focus, label, tooltip, contrast, non-color error cue.
Localization	Language, locale, date/timezone, sorting/collation, text expansion.
Maintainability	Configuration-driven rules, feature flags, versioned contract.
Supportability	Meaningful error code, runbook, audit search, diagnostics.


 14. What-If and Future Change Framework
What-if analysis wajib menjadi section, bukan catatan opsional. Tujuannya bukan merancang semua kemungkinan, tetapi mengidentifikasi change driver bernilai tinggi, coupling tersembunyi, dan extension point yang mencegah redevelopment mahal.
14.1 Template What-If Matrix
Kolom	Isi
Scenario ID	WF-[MODULE]-NNN.
Change Driver	Regulatory, growth, channel, organization, integration, technology.
What If	Perubahan yang diuji.
Likelihood/Horizon	Low/Medium/High; near/mid/long term.
Impacts	Business rule, UI, API, data, security, operation, test.
Migration/Compatibility	Historical data, consumer lama, rollout, rollback.
Extension Point	Configuration, abstraction, versioning, relation model.
Mitigation	Keputusan sekarang untuk menurunkan cost of change.
Decision Needed	Owner dan kapan harus diputuskan.
Related IDs	Rule, risk, decision, test.

14.2 Five-level depth model
Level	Analisis
L1 Current UI	Apa yang terlihat dan dilakukan saat ini.
L2 Rule/Exception	Apa yang terjadi pada invalid, boundary, dan alternate flow.
L3 Cross-layer Impact	Dampak ke API, data, security, audit, integration, test.
L4 Evolution	Dampak perubahan volume, role, channel, workflow, regulation.
L5 Transition	Migration, backward compatibility, rollout, rollback, coexistence.

Stop condition
What-if cukup ketika critical change driver memiliki impact, mitigation/extension point, decision owner, dan test strategy. Hindari spekulasi tanpa hubungan dengan modul atau konteks bisnis.


 15. What-If Scenario Library
Change Driver	What If	Recommended Lens
Channel expansion	Web/Mobile bertambah tablet, partner API, offline, channel dinamis.	Hindari boolean per channel; evaluasi master+assignment; feature flag; channel capability.
Role/workflow	Single role menjadi maker-checker, approval bertingkat, delegation, SoD.	Status machine, transition authorization, approval history, editability per status.
Principal hierarchy	Single principal menjadi hierarchy, inheritance, mass assignment.	Reference by ID; hierarchy version/effective date; snapshot vs latest semantics.
Volume 10x/100x	Grid, search, export, delete, assignment menjadi besar.	Server pagination; index; async export; batch; archive; performance test.
Business code evolution	Initial length/format/scope berubah atau generated ID.	Pisahkan surrogate key dari business code; migration dan alias/history.
Temporal complexity	Open-ended, timezone, backdate, correction, future approval.	Effective dating model; inclusive boundary; versioned history; conflict policy.
Deletion governance	Hard delete menjadi soft delete, restore, retention/legal hold.	Lifecycle status; deleted audit; uniqueness with deleted rows; purge job.
Integration evolution	Sync menjadi event-driven atau multi-consumer.	Versioned event; idempotent consumer; DLQ; replay; reconciliation.
API evolution	Schema berubah dan consumer lama masih aktif.	Version policy; additive changes; deprecation; contract tests; compatibility window.
Migration/import	Bulk upload, merge/split entity, historical load.	Staging; validation report; dry run; restartable batch; rollback; reconciliation.
Concurrency	Banyak editor, batch dan API mengubah record sama.	Version/ETag; conflict strategy; idempotency; lock scope.
Outage/resilience	Dependency lambat/down; partial outage; DR.	Timeout, retry/backoff, circuit breaker, degraded mode, recovery test.
Localization/accessibility	Bahasa, date, timezone, long labels, keyboard-only.	Locale-aware display; invariant storage; flexible layout; a11y acceptance.
Regulation/privacy	Retention, masking, encryption, access review berubah.	Policy-driven retention; classification; key management; audit evidence.
Delivery model	Feature flag, phased rollout, rollback, A/B, parallel run.	Config audit; backward-compatible DB; telemetry; rollback criteria.
Rule configurability	Hardcoded rule menjadi configuration-driven.	Versioned configuration; effective date; approval; validation; audit; simulation.


 16. Testing Strategy dan Traceability
16.1 Test taxonomy
•	Positive dan alternate flow.
•	Negative dan validation.
•	Boundary dan equivalence partition.
•	Authorization dan segregation of duties.
•	Security input/output/access tests.
•	Concurrency, duplicate submit, idempotency.
•	Integration timeout/retry/duplicate/out-of-order.
•	Migration, backward compatibility, contract regression.
•	Performance, capacity, recovery, DR.
•	Future-change test untuk setiap critical what-if.
16.2 Traceability chain
Contoh
BR-DSCAM-008 → FM-PERIOD-END-001 → VAL-OVL-001 → API.endDate / DB.effective_end → RISK-OVL-001 → DEC-EFFECTIVITY-001 → TC-OVL-001 dan WF-TEMPORAL-001.

Object	Coverage expectation
Critical Business Rule	Minimal 1 positive + 1 negative/boundary test.
Security Rule	Authorization/security test.
Integration Rule	Success + timeout/retry/duplicate test.
What-If Critical	Impact test atau contract/migration test.
Assumption High Impact	Test placeholder dan explicit confirmation gate.


 17. Workbook Architecture dan Formatting
17.1 Default workbook
•	Index_Summary.
•	Satu sheet [KODE]_Spec untuk setiap modul.
•	Seluruh artefak detail menjadi section pada module sheet.
•	Separate sheet hanya jika data >100 komponen, lintas-modul, atau external tool import membutuhkan struktur khusus.
17.2 Module sheet order
No	Section
1	Module Overview dan Scope
2	Actor/Role/Permission Matrix
3	Screen dan State Inventory
4	Business Invariants
5	Business Rules
6	Functional UI Spec
7	Detailed Field Matrix
8	Message Catalog
9	Data Model dan API Mapping
10	Integration dan Dependency
11	Security/Privacy/Audit
12	Concurrency/Transaction/Idempotency
13	NFR
14	What-If Matrix
15	Test Scenario
16	Traceability
17	Assumption/Decision/Risk/Open Question

17.3 Visual convention
Warna/Style	Arti
Dark blue/black	Section header.
Gray	Table header/static structure.
Yellow	Assumption/open confirmation.
Light red	Critical validation/error/risk.
Purple	Decision/control/technical logic.
Light blue	Information/current behaviour.
Green	Confirmed/approved bila status tersedia.


 18. Assumption, Decision, Risk, dan Open Question Governance
Register	Kolom minimum
Assumption	ID; topic; proposed decision; reason; impact; confirm by; due/status; related IDs.
Decision	ID; decision; options; rationale; owner; date; status; supersedes; impact.
Risk	ID; event/cause/impact; likelihood; severity; mitigation; owner; trigger; status.
Open Question	ID; question; why needed; impact if unresolved; owner; status; due.
Change Log	Version; date; author; reason; impacted IDs; approval.

Governance rule
Confirmed requirement tidak boleh diubah diam-diam. Perubahan harus menghasilkan Decision/Change entry dan impact analysis terhadap rule, component, message, data, integration, security, migration, serta test.


 19. Quality Gate dan Review Checklist
Gate	Pass criteria
Evidence	Semua input/sheet dan icon kecil diperiksa; observed vs inferred jelas.
Functional	Semua state/action/exception telah ditentukan.
Data	Key, constraint, relation, history, retention, migration dianalisis.
Security	Backend authorization, validation, encoding, audit, privacy tercakup.
Resilience	Transaction, concurrency, idempotency, timeout, retry, recovery tercakup.
Future	Business invariant dan What-If Matrix tersedia.
QA	Critical rule dan what-if memiliki test dan traceability.
Governance	Assumption, Decision, Risk, Open Question memiliki ID/owner/status.
Workbook	Satu modul satu consolidated sheet; readable; filter/freeze/hyperlink.
Delivery	File Excel valid dan ringkasan jumlah artefak diberikan.


 20. Contoh Penerapan DSCAMxxx
Contoh berikut memperlihatkan kedalaman yang diharapkan untuk modul Maintain Keterangan Bon Produk dari mockup berisi Main Page dan Add/Edit Mode.
20.1 Business invariants contoh
•	Satu business scope tidak boleh menghasilkan dua keterangan bon efektif yang ambigu pada tanggal dan channel yang sama.
•	Assignment harus menggunakan identity Group Principal, bukan hanya display name.
•	Perubahan master tidak boleh menghilangkan kemampuan menelusuri historical assignment.
•	Authorization dan audit tetap berlaku walaupun UI diganti atau API dibuka ke channel baru.
20.2 Current state vs proposed
Topic	Current state dari mockup	Future-proof proposed design
Channel	Checkbox Web dan Mobile.	Channel Master + assignment, agar channel baru tidak memerlukan perubahan column.
Initial	Short text code.	Surrogate key terpisah; Initial sebagai business code yang dapat version/alias.
Period	Start dan End date.	Effective dating formal; open-ended policy; overlap exception config.
Group Principal	Flat list checkbox.	Relationship entity dengan hierarchy/effective date readiness.
Delete	Delete button.	Decision hard/soft delete; retention, restore, audit, uniqueness semantics.

20.3 What-if sample
Scenario	Impact	Mitigation/Decision
WF-DSCAM-001: channel ketiga	UI checkbox, API boolean, DB columns, tests berubah.	Gunakan channel collection; confirm apakah current release tetap boolean.
WF-DSCAM-002: maker-checker	Status, button, editability, audit, role, notification berubah.	Siapkan status lifecycle dan transition authorization.
WF-DSCAM-003: 100x data	Search/grid/delete/export berisiko lambat.	Server paging/filter, indexes, async export, batch operation.
WF-DSCAM-004: backdated correction	Overlap dan historical truth menjadi kompleks.	Versioned effective record, correction reason, approval, as-of query.


 21. Operational Prompt Maksimum 8.000 Karakter
Gunakan prompt operasional berikut pada kolom Instructions. Knowledge handbook ini menjadi sumber detail. Jika character counter portal berbeda, hapus whitespace atau contoh, bukan dua prinsip utama maupun What-If requirement.
ROLE: Kamu adalah UI Technical Blueprint Copilot untuk Corporate Development. Analisis screenshot, mockup, wireframe, atau Excel UI dan hasilkan workbook .xlsx production-ready untuk BA/PO, frontend, backend, database, security, QA, support, dan major redevelopment.
PRINSIP: Detail lintas-fungsi adalah default. Gunakan satu Index_Summary dan SATU MODUL = SATU SHEET SPEC LENGKAP. Field Matrix, Message Catalog, Data/API, Security, What-If, Test, dan Traceability menjadi section dalam sheet modul. Sheet tambahan hanya jika diminta, lintas-modul, atau terlalu besar. Scan semua gambar dan seluruh sheet. Dokumentasikan icon kecil, checkbox, mandatory, default, selected, disabled, hidden, read-only. Informasi tidak pasti wajib berupa keputusan spesifik berlabel “ASUMSI - perlu konfirmasi BA/PO” dan fill kuning.
FUTURE-PROOF: Pisahkan Business Invariant, Current State, Proposed Design, dan Assumption. Jangan mengunci business rule pada UI/teknologi saat ini. Analisis redevelopment, major update, channel, role, workflow, volume, integration, data, regulation, migration, dan compatibility.
PROSES: Identifikasi module, purpose, actor, role, screen, state, popup, entity, dependency. Beri ID untuk Rule, Component, Message, Data/API, Assumption, Decision, Risk, What-If, Test. Inventarisasi semua component dan tentukan M/O/C/System, type/length/format, default, state, event, validation, message, mapping, permission, source/status. Buat IF-THEN rules dan What-If sebelum final spec.
MODULE SHEET ORDER: Overview/Scope; Role-Permission; Screen-State; Business Invariants; Business Rules; Functional UI Spec; Field Matrix; Message Catalog; Data/API/Integration; Database Integrity; Security/Privacy/Audit; Concurrency/Transaction/Idempotency; NFR; What-If Matrix; Test; Traceability; Assumption/Decision/Risk/Open Question.
FUNCTIONAL: tabel Elemen | Jenis Komponen | Behaviour/Deskripsi. Behaviour ringkas dengan titik koma: mandatory; format; length; default; state; event; validation; Message ID; permission; result; assumption.
RULES: IF-THEN; trigger, result, exception, priority, status, related IDs. Evaluasi Add/Edit/View/Delete, bulk, search/filter/sort/page, date, uniqueness, overlap, dependency, save/back/dirty, authorization, not-found, partial failure, rollback, concurrency, effective status.
WHAT-IF: wajib. Kolom Scenario ID; Driver; What If; impact rule/UI/API/data/security/operation/test; migration/backward compatibility; extension point; mitigation; decision. Minimal: channel baru; multi-role/maker-checker/approval; principal hierarchy; volume 10x/100x; code length/scope; temporal/open-ended/backdate; soft-delete/restore/retention; sync-to-async/event/retry/reconciliation; API/schema version; migration/import/merge; concurrency/idempotency; outage/DR; localization/a11y; regulation/privacy; feature flag/rollout/rollback; configuration-driven rule.
FIELD MATRIX: Component ID; Screen; Section; Field; Type; M/O/C/System; Data Type; Min/Max; Format/Value; Default; State; Validation; Event; Message; Permission; Data Attribute; Assumption.
MESSAGE: ID; Type; Trigger; Text; Placement; Component; Next Action; Logging; Assumption. Prefix VAL/CNF/SUC/WRN/ERR/INF.
DATA/API: entity/key/relation, nullability, uniqueness scope, effective dating, version/status, retention, source of truth, API/error contract, page/filter/sort, idempotency, events, retry/timeout, reconciliation, versioning/compatibility. Bedakan confirmed dan proposed.
SECURITY: authentication; role/scope; backend/ID authorization; validation; encoding; parameterized query; XSS/injection/CSRF; classification/masking/encryption/retention; CRUD/view audit; old/new; actor; UTC; correlation; secure logging. UI hide/disable bukan security control.
RESILIENCE/NFR: atomic save/rollback; lock/version; stale update; double-submit; retry/conflict; performance/capacity/scalability/availability/recovery/observability/a11y/localization/device/maintainability/configuration/archive/backup/RTO/RPO. Angka tanpa sumber adalah asumsi.
TEST/TRACE: buat positive, negative, boundary, authorization, security, concurrency, integration, migration, compatibility, recovery, performance, future-change tests. Hubungkan Rule → Component → Message → Data/API → Risk/Assumption/Decision → Test. Critical rule dan what-if wajib memiliki test.
FORMAT/DONE: hide gridline, freeze, wrap, filter, hyperlink, dark section header, gray table header, assumption yellow, critical pink. Selesai bila seluruh input dipindai, semua component tercatat, consolidated module sheet lengkap, what-if dan traceability tersedia, assumptions jelas, dan file dapat dibuka di Excel. Final chat: file dan jumlah module, screen, rule, component, what-if, risk, assumption, message, test, serta open question utama.

 Lampiran A. Component and Validation Reference
Component	Validation/Behaviour Lens
Text box	Required, min/max, chars, trim, case, uniqueness, paste, IME.
Text area	Max, multiline, line break, counter, script/HTML, resize.
Numeric	Range, decimal, thousand separator, zero/negative, precision.
Datepicker	Format, min/max, inclusive boundary, timezone, invalid manual input.
Dropdown	Source, default, inactive item, no-result, search, clear.
Checkbox group	Min/max selected, select all, indeterminate, dependency.
Grid	Columns, source, sort, filter, page, selection, empty/load/error, export.
Icon action	Tooltip, accessible name, permission, focus, confirmation.
Upload	Type, size, count, virus scan, duplicate, preview, delete, retry.
Modal	Open/close, focus trap, Esc, dirty state, responsive, error.
Button	Permission, state, click, loading, duplicate prevention, result.

Lampiran B. ID Convention and Status Vocabulary
Object	Pattern	Example
Module	[CODE]	DSCAMxxx
Screen	SCR-[MOD]-NN	SCR-DSCAM-01
Rule	BR-[MOD]-NNN	BR-DSCAM-008
Component	CMP-[MOD]-[AREA]-NNN	CMP-DSCAM-FM-001
Message	VAL/CNF/SUC/WRN/ERR/INF-[MOD]-NNN	VAL-DSCAM-004
Data	DATA-[MOD]-NNN	DATA-DSCAM-003
API	API-[MOD]-NNN	API-DSCAM-002
Assumption	ASM-[MOD]-NNN	ASM-DSCAM-006
Decision	DEC-[MOD]-NNN	DEC-DSCAM-004
Risk	RISK-[MOD]-NNN	RISK-DSCAM-003
What-If	WF-[MOD]-NNN	WF-DSCAM-005
Test	TC-[MOD]-NNN	TC-DSCAM-021

Status	Meaning
Draft	Belum review.
In Review	Sedang divalidasi.
Confirmed	Disepakati owner.
Proposed	Usulan teknis.
Assumption	Belum dikonfirmasi.
Deferred	Diputuskan nanti.
Superseded	Digantikan decision/version baru.
Rejected	Tidak digunakan dengan rationale.


 Lampiran C. Reusable Table Templates
Template	Columns
Business Rule	Rule ID | Name | Source/Status | IF/Trigger | AND/Precondition | THEN/Result | ELSE/Exception | Priority | Related IDs
Field Matrix	Component ID | Screen | Section | Field | Type | M/O/C/System | Data Type | Min/Max | Format | Default | State | Validation | Event | Message | Permission | Data | Assumption
Message Catalog	Message ID | Type | Trigger | Text | Placement | Component | Next Action | Logging | Assumption
Data/API	UI Field | Component | Entity/Attribute | Type | Required | Example | Transform | Constraint | Source | Audit | Security | Assumption
What-If	Scenario ID | Driver | What If | Horizon | Impacts | Migration/Compatibility | Extension Point | Mitigation | Decision | Related IDs
Test	TC ID | Rule/WF ID | Component | Preconditions | Data | Steps | Expected | Priority | Type | Assumption
Traceability	Rule | Component | Message | Data/API | Risk | Assumption | Decision | What-If | Test | Status
Decision	Decision ID | Topic | Options | Decision | Rationale | Owner | Date | Impact | Supersedes | Status

END OF CONTROLLED KNOWLEDGE
