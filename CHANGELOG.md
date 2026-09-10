# Changelog

## v2.6 — Dual-Sheet Wajib (Snapshot + Redrawn) & Ekspansi Tipe Input
* Cell-drawing TIDAK LAGI fallback opsional — sekarang WAJIB SELALU dibuat untuk setiap Desain UI, berpasangan dengan sheet Snapshot (bukti asli sebagai gambar). Sheet berubah dari 1 ("Desain UI") menjadi 2 per Desain UI: `[KODE]_[Screen]_Snap` dan `[KODE]_[Screen]_Redr`.
* Tipe input diperluas dari gambar/Excel saja menjadi: gambar, Excel, PDF (rasterize per halaman), Word/.docx (ekstrak gambar mockup + ekstrak teks requirement), dan Markdown/.md (input terstruktur pelengkap — business rule/question bank, bukan sumber visual).
* Penamaan sheet disesuaikan supaya tetap muat batas 31 karakter Excel dengan suffix Snap/Redr.

## v2.5
* Aturan teknis cell-drawing diperjelas total (handbook 3.5, baru): lebar kolom wajib seragam 2,57; tanpa merge cell; tanpa wrap text (rata kiri); button multi-cell 1 border luar tanpa border internal; tab aktif/nonaktif harus beda visual; input disabled = fill abu-abu; row selected = fill kuning; error state = fill merah muda; loading & empty state wajib direpresentasikan; dropdown utama wajib pakai Data Validation Excel asli (bukan sekadar gambar).
* Ditegaskan: makna warna di sheet "Desain UI" (state mockup UI) berbeda dari makna warna yang sama di sheet spec (governance/assumption) — dicatat eksplisit di 17.3 supaya tidak tertukar.
* Instruksi operasional dipadatkan lagi untuk memuat aturan cell-drawing baru, tetap di bawah 8.000 karakter (7.968).

## v2.4 — Standar Kelengkapan Tertinggi (Maximal Completeness)
* Field Matrix redesign: row-explosion per Mode×Status wajib untuk SEMUA jenis komponen (bukan cuma field input) — 1 baris = 1 component pada 1 konteks final, kolom baru Mode + Status Context + Editable/Disabled/Hidden eksplisit, Component ID convention baru (`CMP-[FIELD]-[MODE]-[STATUS]`).
* Business Rules: kelengkapan domain checklist (6.2) ditegaskan wajib sampai habis; ditambah 6.5 — setiap Critical Challenge yang terjawab wajib menghasilkan Business Rule baru.
* What-If: ditambah 14.3 — checklist 16 kategori (15) wajib dijalankan semua per modul, kategori tidak relevan tetap dicatat "Not Applicable" beserta alasan, bukan dilewati diam-diam.
* Sheet BARU `Critical_Challenge_QnA` (handbook 19) — devil's advocate persona, pertanyaan kritis + Insight/Rekomendasi wajib per section, 10 domain wajib (concurrency, ambiguitas keputusan, boundary ekstrem, status mustahil, permission edge case, data terpakai transaksi lain, multi-device, kegagalan parsial, interpretasi ganda, reversibilitas).
* Mandat kelengkapan dinaikkan jadi prinsip inti (01) — standar setinggi mungkin di SEMUA section secara merata, bukan cuma di bagian yang kebetulan disorot.

## v2.3
* Ditemukan gap nyata dari hasil produksi: baris assumption diberi teks "ASUMSI - perlu konfirmasi BA/PO" TAPI TIDAK diberi fill kuning; autofilter tidak aktif. Aturan format ditulis ulang jadi imperatif eksplisit ("dieksekusi sebagai kode, bukan sekadar teks") + ditambah "Gate format" sebagai pengecekan wajib sebelum file difinalisasi, supaya tidak terlewat lagi.
* Instruksi operasional (`instruksi_agent_copilot_v2.md`) diperkuat di bagian FORMAT & QUALITY GATE dengan penekanan yang sama, tetap di bawah 8.000 karakter.

## v2.2
* Sheet "Desain UI" TIDAK LAGI direkonstruksi manual cell-per-cell. Sekarang: input gambar → file gambar asli di-embed langsung sebagai objek picture (`ws.add_image()`); input Excel → sheet asli di-copy terprogram (value/style/width/merge) via Code Interpreter/engine kode agent, bukan diketik ulang.
* Aturan "dilarang merge cell / lebar kolom 2,6cm" dicabut sebagai aturan wajib (hanya jadi fallback bila embed image/copy terprogram tidak didukung environment agent) — ini menghilangkan root cause kegagalan yang berasal dari proses rekonstruksi manual.
* Chameleon Angular Framework reference diturunkan statusnya jadi fallback saja.
* Prasyarat: agent harus mengaktifkan "File uploads" + "Code interpreter" di Settings > Generative AI > File Processing Capabilities.

## v2.1
* Functional UI Spec dan Field Matrix DIGABUNG menjadi satu tabel tunggal per Desain UI (sebelumnya 2 tabel terpisah). Satu baris = satu component, memuat behaviour/event sekaligus constraint teknis (type, min/max, format, default, state, validation, permission, message ID).
* `handbook/08-field-matrix.md` dihapus, isinya melebur ke `handbook/07-functional-ui-spec.md`.
* Template digabung: `templates/field-matrix-template.md` → `templates/functional-field-matrix-template.md`.
* Struktur sheet per Desain UI berubah dari 6 section menjadi 5 section.

## v2.0
* Scope dipersempit: menghapus Security/Privacy/Audit, Concurrency/Transaction/Idempotency, NFR, Integration/Dependency, dan Traceability penuh dari deliverable standar.
* Knowledge base: menghapus Azure Architecture Center & OWASP ASVS; menambahkan Chameleon Angular Framework demo sebagai referensi desain UI.
* Arsitektur workbook diubah: 1 Desain UI = 1 sheet spec (Screen-State Inventory, Business Intent/Invariants, Business Rules, Functional UI Spec, Field Matrix, Message Catalog); artefak lintas-modul lain dikonsolidasi per jenis pada sheet terpisah (Overview_Scope, Actor_Role_Permission, Data_API, What_If, Test_Scenario, Assumption_Decision_Risk_Open).
* Sheet baru `Desain UI` wajib menampilkan ulang/mereproduksi desain asli tanpa merge cell dan dengan lebar kolom seragam (~2,6 cm) — root cause kegagalan output sebelumnya.
* Index_Summary ditambah blok "Keputusan Kritis Belum Dikonfirmasi" dan "Glosarium & Penjelasan".
* Mendukung pembacaan input Excel dengan lebih dari 1 desain UI per sheet dan lebih dari 1 sheet per file.

## v1.0
* Baseline handbook awal (17 section, termasuk Security/NFR/Concurrency/Integration/Traceability).
