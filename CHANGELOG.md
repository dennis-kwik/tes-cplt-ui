# Changelog

## Addendum ke-5 pasca-v2.9 (tanpa bump versi) — Restrukturisasi Besar
Hasil diskusi mendalam menyelaraskan metodologi engine dengan cara kerja manual traversal (kiri-atas→kanan→turun, 1x baca menghasilkan component+spec+business rule sekaligus). Perubahan struktural terbesar sejak v2.9:
* **Traversal Order** (3.4c, baru): urutan baca kiri-atas→kanan→turun WAJIB konsisten di Element Inventory, Component ID numbering (7.3), Business Rule numbering (6.1), dan Narrative Spec Panel — sebelumnya tidak ada aturan urutan eksplisit sama sekali.
* **Element Inventory pindah jadi VISIBLE CONTENT di sheet `_Snap`** (3.4d) — sebelumnya cuma langkah kerja internal (3.4c versi lama), sekarang harus benar-benar terlihat di sheet supaya user bisa cross-check langsung.
* **Narrative Spec Panel** (3.4e, baru) — format `Kolom | Spec` (1 kalimat padat per elemen, dikelompokkan per section) sebagai isi PANEL KANAN sheet `_Redr` — formalisasi dari inventaris, bukan ditulis ulang independen. No-duplikasi trigger yang sudah dijelaskan di Tools tidak diulang di List View Kolom.
* **Depth Balance** (3.4f, baru) — narasi ≤ spec formal; spec formal WAJIB minimal setara, tidak boleh jauh lebih dangkal. Mencegah 2 sumber kebenaran berbeda.
* **Mode Duplikasi jadi FORMAT BAKU WAJIB** (handbook 23 ditulis ulang) — Mode Terpisah DIHAPUS total, bukan pilihan lagi. Menghapus 1 dari 2 dimensi konfirmasi mode (21.3 update) — sekarang hanya Enterprise/Simple yang perlu dikonfirmasi.
* **Urutan sheet workbook diubah total** (17.1): dari per-modul berselang-seling (Snap1-Redr1-Spec1-Snap2...) menjadi PER JENIS dikelompokkan (Index_Summary → semua Snap → semua Redrawn → semua Spec Formal → lintas-modul).
* Self-Audit Pass (20.2) dapat 4 item checklist baru sesuai semua di atas.
* Prinsip eksplisit: contoh spesifik yang dipakai selama diskusi (nama modul tertentu) TIDAK di-hardcode ke handbook — hanya pola umum yang dibakukan.

## Addendum ke-4 pasca-v2.9 (tanpa bump versi)
Ditemukan pola kegagalan baru dari hasil produksi nyata (bandingkan mockup asli vs hasil Copilot Studio): urutan/pengelompokan elemen berubah, teks diparafrase/"dikoreksi" (mis. "Active/Deactive" jadi "Activate/Deactivate"), elemen kecil (icon, box sekunder) hilang total.
* **Element Inventory Extraction** (3.4c, baru): langkah WAJIB terpisah SEBELUM kode redraw ditulis — susun inventaris eksplisit (teks verbatim, tipe, posisi/urutan/grouping asli) dari sumber, kode redraw HANYA boleh mengiterasi inventaris ini, bukan disusun bebas dari kesan visual langsung. Menerapkan prinsip evidence classification (3.3) yang sebelumnya cuma berlaku untuk requirement teks, sekarang juga untuk elemen visual.
* Self-Audit Pass (20) dapat item checklist baru: cross-check redraw vs inventaris (kelengkapan, verbatim, urutan/grouping).

## Addendum ke-3 pasca-v2.9 (tanpa bump versi)
Berdasarkan sesi mock-up validasi visual langsung di Excel (3 iterasi kalibrasi) — 2 bug produksi nyata ditemukan dan diperbaiki di sumbernya, bukan cuma di mockup:
* **Bug border box** (3.5a, baru): implementasi lama menimpa sisi atas kotak dengan sisi bawah di cell yang sama untuk box 1-baris (r1==r2), membuat tombol/header terlihat bocor tanpa sisi atas. Algoritma pengganti (1 assignment per cell, gabungkan semua sisi sekaligus) dibakukan sebagai kode wajib, bukan cuma deskripsi.
* **Bug sizing hardcode** (3.5b, baru): lebar elemen (tombol, header) sebelumnya ditebak/nilai tetap, menyebabkan tombol kepanjangan ATAU header terpotong ("No. Surat Kirim" jadi "No"). Formula terkalibrasi: `max(3, ceil(len(text)/2.6)+1)` cell, hasil 3 iterasi pengujian visual nyata (kalibrasi awal 1.6 char/cell terlalu longgar, 2.2 masih longgar di teks panjang, 2.6 disepakati).
* **Bug alignment**: button sebelumnya center-align (melanggar aturan rata-kiri yang sudah ada), menyebabkan teks terlihat meluber/terpotong di box pas-pasan. Diperbaiki jadi rata kiri + 1 spasi indent, konsisten dengan aturan lain.
* **Pola header berjenjang dibakukan** (3.5c, baru): vertical spanning, dual-row (kolom sama beda label per baris), dan grouped (parent menaungi sub-kolom) — SEMUA pakai 1 box besar + divider tambahan, bukan elemen terpisah yang digabung (pendekatan lama menyebabkan gap/misalignment).
* **Grid hierarkis dibakukan** (3.5d, baru): kolom toggle lebar tetap, header toggle blank (tanpa fill), indent baris detail via cell toggle kosong (bukan pengurangan lebar kolom).

## Addendum ke-2 pasca-v2.9 (tanpa bump versi)
Berdasarkan uji coba nyata proyek PROMT02 (Penarikan Material) via Copilot Studio — hasil dinilai layak sebagian, diadopsi sebagai MODE OPSIONAL (bukan default universal) karena beberapa aturan bersifat project-specific:
* **Handbook baru 23 — Layout Mode Redrawn**: Mode Duplikasi (UI+spec panel kanan di Redrawn, spec formal tetap ada terpisah) vs Mode Terpisah (default lama) — WAJIB dikonfirmasi eksplisit sebelum generate, dimensi mode independen dari Enterprise/Simple (21.3).
* Area UI di Redrawn Mode Duplikasi: lebar DINAMIS per screen (bukan rentang tetap A:AN) — 2 kolom spacer wajib + border tebal di tengah gap + freeze panes di kolom spacer kedua (23.4/23.5).
* Input Markdown diperluas (3.4b, 23.7): sekarang ada 2 varian — business-rule bank (existing) DAN hasil konversi dari sumber visual (Excel/PDF/Word/Image/Figma export) yang diperlakukan sebagai pengganti sumber visual untuk redraw. Disambiguasi lewat prinsip Ambiguity Handling (3.3b) kalau tidak jelas.
* Interpretasi pipeline Markdown `|` sebagai kolom logis grid (23.8) — berlaku universal (bukan project-specific), tidak boleh ada karakter `|` literal tersisa di area UI redraw.
* Self-Audit Pass (20) dapat tambahan checklist khusus Mode Duplikasi (23.6): cross-check byte-for-byte panel kanan Redrawn vs sheet spec formal.

## Addendum pasca-v2.9 (tanpa bump versi — sesuai instruksi eksplisit: tidak menaikkan versi tanpa diminta)
Disesuaikan dengan insight dari `Riwayat_Desain_CorDev_Blueprint.md` (dokumen desain arsitektur Claude Enterprise yang dikerjakan paralel), khusus bagian 6d (Goal-Driven Execution) dan 9 (Insight dari Evaluasi Hasil Nyata):
* Self-Audit Pass (20) ditulis ulang jadi **checklist tercentang satu-satu** (format `- [ ]`), bukan lagi 6 poin naratif — sejalan dengan temuan "punya aturan tidak sama dengan menegakkannya" (checklist eksplisit jauh lebih kuat dari "baca ulang lalu dianggap oke").
* Ditambah 20.0 — **penegasan Self-Audit Pass wajib dijalankan meski mahal token**, menjawab insight bahwa dorongan efisiensi token kemungkinan nyata berkontribusi ke kegagalan penerapan aturan mekanis yang sudah eksplisit.
* Ditambah rekomendasi cek independen di chat/sesi baru (20.4) — sejalan dengan pola "cek independen" yang divalidasi silang di dokumen arsitektur.

## v2.9 — Sinkronisasi Penuh Diskusi Lanjutan (ex-Claude Blueprint Engine v0.1)
Menyatukan seluruh keputusan desain dari sesi diskusi lanjutan ke repo House Standard, setelah sebelumnya sempat hanya terdokumentasi di `Claude_Blueprint_Engine.md` (dokumen terpisah untuk Claude Project).
* **Sheet digabung**: `What_If` + `Critical_Challenge_QnA` → `What_If_Critical_Challenge` (1 sheet, 2 section). Handbook 19 dihapus, isinya melebur ke handbook 14.
* **Related ID 4-slot + hyperlink** (7.3c, baru): ganti kolom "Related IDs" bertumpuk jadi 4 kolom terpisah (1 cell = 1 value); Related ID 1 = dampak paling utama, WAJIB di-hyperlink ke cell asal.
* **Kosakata baku Mode/Status** (7.3b) tetap berlaku, sekarang terhubung ke skema Related ID baru.
* **Kolom "Sumber"** (baru, di Business Rules & Field Matrix): `Requirement Asli` / `Auto-Applied dari WF-xxx` / `Auto-Applied dari CQ-xxx`.
* **Klasifikasi Jenis Jawaban** (14.4b, baru): Keputusan Bisnis (tetap Open/Assumption) vs Pola Teknis Standar (WAJIB auto-apply langsung ke Business Rule/Field Matrix/Test, status "Auto-Applied") — dengan pemetaan default per domain Critical Challenge.
* **Katalog Pola Teknis Standar** (14.4d, baru): daftar pola baku (cegah submit dobel, deteksi data usang, kegagalan sebagian, retry otomatis, soft delete, effective dating) ditulis bahasa bisnis dulu, istilah teknis cuma catatan kurung.
* **Kolom "Dampak ke Spec"** (baru): daftar eksplisit semua ID yang ter-generate akibat auto-apply, untuk panduan rollback kalau BA membatalkan.
* **Dedup lintas-screen eksplisit** (14.4e, baru): kolom "Berlaku Untuk" wajib diisi saat konsolidasi entry serupa antar screen.
* **Bahasa bisnis dulu, istilah teknis kedua** (01, mandat baru): berlaku ke SELURUH workbook, bukan cuma katalog pola teknis.
* **Fill warna Auto-Applied** (17.3, baru): oranye muda (FCE4D6), beda dari kuning-assumption dan putih-confirmed.
* **Configurability Elicitation hard-stop** (3.3c, baru): proses berhenti kalau mode "highly configurable" diminta tanpa info apapun soal apa yang perlu configurable.
* **Struktur Scope Configurability generik** (3.3d, baru): Master Configuration Engine dengan scope level generik (bukan hardcode PT/RSO/Area), berlaku ke pilihan konten, parameter validasi, dan visibility field.
* **Future-proof 5 tahun** (5.1, baru): pertanyaan wajib di Business Intent/Invariants; Horizon What-If diberi patokan waktu eksplisit (Near<2th, Mid 2-4th, Long 5th+) di 14.2.
* **Kategori kontekstual tambahan** (14.3): pertimbangkan driver spesifik konteks menu (termasuk tapi tidak terbatas AI/automation) di luar 16 kategori baku, TIDAK ditambahkan mekanis ke semua modul.
* **Mode Desain Enterprise/Configurable vs Simple** (handbook 21, baru): heuristik rekomendasi otomatis + WAJIB konfirmasi user sebelum generate.
* **Excel Generation Safety Guardrails** (handbook 22, baru): penyebab umum file .xlsx corrupt, urutan generate yang aman, File Integrity Check wajib (buka-ulang file sebelum diserahkan) — respons langsung terhadap kasus file corrupt yang ditemukan di produksi.

## v2.8 — Auto-Promosi Pola Teknis Standar ke Spec Inti (supersede sebagian oleh v2.9 di atas)
Menjawab gap: Critical Challenge/What-If yang jawabannya sudah jelas (best-practice teknis, bukan keputusan bisnis) sebelumnya tetap nyangkut status "Open" sampai konfirmasi manual — padahal insight-nya sendiri sudah cukup untuk langsung diadopsi.
* Critical_Challenge_QnA: kolom baru "Jenis Jawaban" (Keputusan Bisnis / Pola Teknis Standar). Pola Teknis Standar WAJIB auto-promosi jadi Business Rule (status Proposed) + Field Matrix + Test Scenario saat itu juga (19.3b, 19.5b) — status berubah "Answered (Auto-Proposed)". Keputusan Bisnis tetap Open/Assumption seperti sebelumnya.
* What-If: Horizon=Near dengan mitigasi konkret ikut auto-promosi (14.2b). Horizon Mid/Long tetap murni dokumentasi masa depan.
* Self-Audit Pass (20) ditambah item ke-6: verifikasi semua kandidat auto-promosi benar-benar sudah masuk ke spec inti, bukan cuma tertulis di sheet Challenge/What-If.
* Tujuan: memaksimalkan kelengkapan Business Rules/Field Matrix/Test Scenario sejak draft pertama — mengurangi celah spesifikasi yang sebenarnya sudah punya jawaban jelas tapi dibiarkan terbuka.

## v2.7 — Self-Audit Pass & Perbaikan Gap dari Audit Produksi
Dilatarbelakangi audit langsung terhadap hasil produksi nyata (blueprint Reprint Faktur) yang menemukan: interpretasi ambigu requirement diselesaikan diam-diam tanpa ditandai (menyebabkan kontradiksi antar sheet), Component ID tidak konsisten skemanya, Test Scenario under-coverage tanpa disadari, dan sheet Snapshot untuk input teks murni tidak ditangani eksplisit.
* Sheet baru wajib: TIDAK ADA sheet baru, tapi ditambah **langkah proses baru**: Self-Audit Pass (handbook 20) — baca ulang seluruh workbook dengan persona devil's advocate diarahkan ke hasil sendiri, dijalankan SEBELUM file difinalisasi.
* Ambiguity Handling (3.3b, baru): requirement dengan >1 tafsiran valid WAJIB dicatat kedua opsinya, bukan dipilih diam-diam; tafsiran default WAJIB konsisten di semua sheet yang menyinggungnya.
* Kosakata baku Mode & Status Context (7.3b, baru): mencegah Component ID drift dengan token tertutup, bukan teks bebas.
* Formula minimum Test Scenario (16.3, baru): jumlah test >= (2 × Business Rule Critical) + (1 × Critical Challenge) — dihitung eksplisit, bukan diperkirakan.
* Input teks chat murni (3.4b, ditambahkan): sheet Snapshot untuk kasus tanpa file visual sama sekali WAJIB berisi reproduksi requirement asli, bukan catatan generik.
* Instruksi operasional dipadatkan ulang (GATE FORMAT + QUALITY GATE digabung jadi 1 checklist) untuk memberi ruang bagi aturan baru, tetap di bawah 8.000 karakter (5.849).

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
