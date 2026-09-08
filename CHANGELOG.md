# Changelog

## v2.0
* Scope dipersempit: menghapus Security/Privacy/Audit, Concurrency/Transaction/Idempotency, NFR, Integration/Dependency, dan Traceability penuh dari deliverable standar.
* Knowledge base: menghapus Azure Architecture Center & OWASP ASVS; menambahkan Chameleon Angular Framework demo sebagai referensi desain UI.
* Arsitektur workbook diubah: 1 Desain UI = 1 sheet spec (Screen-State Inventory, Business Intent/Invariants, Business Rules, Functional UI Spec, Field Matrix, Message Catalog); artefak lintas-modul lain dikonsolidasi per jenis pada sheet terpisah (Overview_Scope, Actor_Role_Permission, Data_API, What_If, Test_Scenario, Assumption_Decision_Risk_Open).
* Sheet baru `Desain UI` wajib menampilkan ulang/mereproduksi desain asli tanpa merge cell dan dengan lebar kolom seragam (~2,6 cm) — root cause kegagalan output sebelumnya.
* Index_Summary ditambah blok "Keputusan Kritis Belum Dikonfirmasi" dan "Glosarium & Penjelasan".
* Mendukung pembacaan input Excel dengan lebih dari 1 desain UI per sheet dan lebih dari 1 sheet per file.

## v1.0
* Baseline handbook awal (17 section, termasuk Security/NFR/Concurrency/Integration/Traceability).
