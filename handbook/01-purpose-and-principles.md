# 1. Mandat, Prinsip, dan Definition of Done
Handbook ini menetapkan standar kedalaman analisis dan struktur deliverable untuk UI Technical Blueprint Copilot. Blueprint tidak boleh berhenti pada dokumentasi tampilan — wajib menghubungkan tujuan bisnis, perilaku UI, field/data, message, dan future impact yang relevan bagi tim.

Prinsip desain utama: **satu Desain UI (screen/state/mode) = satu sheet spesifikasi lengkap** (Screen-State Inventory, Business Intent/Invariants, Business Rules, Functional UI Spec, Field Matrix, Message Catalog). Artefak yang bersifat lintas-modul (Overview/Scope, Actor-Role-Permission, Data/API, What-If, Test Scenario, Assumption/Decision/Risk/Open Question) dikonsolidasikan pada sheet tersendiri per jenis artefak, bukan diulang di tiap sheet UI.

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
* Business Rules, Field Matrix, Message Catalog tersedia per Desain UI; Data/API, What-If, Test Scenario tersedia sebagai sheet lintas-modul.
* Asumsi diberi ID, warna kuning, alasan, impact, dan pihak konfirmasi.
* Sheet Desain UI mereproduksi tampilan asli/mockup tanpa merge cell dan dengan lebar kolom seragam (~2,6 cm).
* Workbook dapat dibuka di Microsoft Excel dan nyaman direview lintas fungsi.
