# 1. Mandat, Prinsip, dan Definition of Done
Handbook ini menetapkan standar kedalaman analisis dan struktur deliverable untuk UI Technical Blueprint Copilot. Blueprint tidak boleh berhenti pada dokumentasi tampilan — wajib menghubungkan tujuan bisnis, perilaku UI, field/data, message, dan future impact yang relevan bagi tim.

**Mandat kelengkapan (standar tertinggi):** blueprint ini harus cukup lengkap dan tervalidasi sehingga system analyst dan developer bisa langsung auto-approve tanpa perlu menemukan sendiri pertanyaan kritis yang belum terjawab. Ini berlaku SAMA TINGGINYA di SEMUA section — Field Matrix, Business Rules, What-If, bukan cuma satu section yang "kebetulan" mendapat perhatian lebih. Kelengkapan dibuktikan lewat jejak sistematis (checklist domain di 6.2, 14.3, 19.4 dijalankan sampai habis, bukan dipilih-pilih), bukan lewat asumsi bahwa "sudah cukup detail".

Prinsip desain utama: **satu Desain UI (screen/state/mode) = satu sheet spesifikasi lengkap** (Screen-State Inventory, Business Intent/Invariants, Business Rules, Functional UI Spec & Field Matrix dengan row-explosion per Mode×Status — lihat 07, dan Message Catalog). Artefak yang bersifat lintas-modul (Overview/Scope, Actor-Role-Permission, Data/API, What-If, Test Scenario, Assumption/Decision/Risk/Open Question, **Critical Challenge QnA/devil's advocate — lihat 19**) dikonsolidasikan pada sheet tersendiri per jenis artefak, bukan diulang di tiap sheet UI.

Dua keputusan utama: 1) Kedalaman lintas-fungsi menjadi output default, bukan enrichment setelah user meminta detail. 2) Ruang lingkup dibatasi pada BA/PO, Frontend, Backend, Database, dan QA — Security/Privacy/Audit, Concurrency/Transaction/Idempotency, NFR, Integration/Dependency, dan Traceability penuh TIDAK termasuk deliverable standar (lihat 02).

## 1.1 Audiens dan Kebutuhan
* BA/PO: Scope, invariant, rule IF-THEN, exception, assumption, decision, risk, acceptance intent.
* Frontend: Component state, event, validation, loading/error/empty state, message placement.
* Backend: Server-side rule, validation, error contract.
* Database: Entity, key, relation, constraint, effective dating, indexing.
* QA: Positive, negative, boundary, dan future-change tests.

## 1.2 Definition of Done
* Seluruh input (semua gambar/sheet) dipindai; setiap Desain UI diidentifikasi dan diberi sheet sendiri.
* Seluruh screen, state, field, icon, action, dan visual cue tercatat.
* Business invariant dipisahkan dari current state dan proposed design.
* Business Rules, Functional UI Spec & Field Matrix (row-explosion per Mode×Status), Message Catalog tersedia per Desain UI; Data/API, What-If, Test Scenario, **Critical Challenge QnA** tersedia sebagai sheet lintas-modul.
* Asumsi diberi ID, warna kuning, alasan, impact, dan pihak konfirmasi.
* Setiap component dengan constraint berbeda per Mode/Status sudah dipecah jadi baris terpisah (07.1); setiap kolom "BELUM DIPUTUSKAN" terhubung ke Assumption DAN Critical_Challenge_QnA.
* Domain checklist (6.2 Business Rules, 14.3 What-If, 19.4 Critical Challenge) dijalankan sampai habis per screen — bukan dipilih-pilih diam-diam.
* Sheet Desain UI (Snapshot + Redrawn, lihat 3.4) mereproduksi tampilan asli/mockup: Snapshot sebagai gambar bukti, Redrawn dengan lebar kolom seragam 2,57 tanpa merge cell (lihat 3.5).
* Workbook dapat dibuka di Microsoft Excel dan nyaman direview lintas fungsi.
