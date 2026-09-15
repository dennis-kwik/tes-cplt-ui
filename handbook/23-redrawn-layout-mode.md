# 23. Layout Mode Redrawn — Duplikasi Spec vs Terpisah (WAJIB dipilih dulu)
Ditambahkan setelah uji coba nyata (proyek PROMT02 - Penarikan Material) menemukan kebutuhan reviewer melihat UI dan spec sekaligus dalam 1 sheet, tanpa berpindah ke sheet spec formal. Dua mode diformalkan — **bukan default diam-diam, WAJIB dikonfirmasi eksplisit ke user sebelum generate**, sama seperti Mode Desain (21).

## 23.1 Dua Mode
* **Mode Terpisah** (default historis): sheet `_Redr` HANYA berisi UI redraw (kiri saja, tidak ada panel kanan). Sheet spec formal `[KODE]_[Screen]` berisi 5 section lengkap, terpisah total.
* **Mode Duplikasi** (baru): sheet `_Redr` berisi UI redraw DI KIRI + panel spec 5-section lengkap DI KANAN (salinan review cepat). Sheet spec formal `[KODE]_[Screen]` TETAP dibuat, TIDAK dihapus — panel kanan Redrawn adalah salinan, bukan pengganti.

## 23.2 Konsekuensi Mode Duplikasi yang WAJIB disadari sebelum dipilih
* **Duplikasi konten nyata**: 5 section spec sekarang ada di 2 tempat (panel kanan Redrawn + sheet spec formal). Ini menambah beban tulis saat generate (~2x volume konten spec per screen) DAN beban Self-Audit Pass (harus cross-check kedua lokasi identik — lihat 23.6).
* **Tidak semua screen cocok**: screen dengan spec sangat panjang (banyak row-explosion Mode×Status) membuat panel kanan jadi sangat lebar, mungkin kurang nyaman direview dibanding sheet spec formal yang scroll vertikal biasa.
* Kalau user tidak yakin, DEFAULT ke Mode Terpisah (lebih ringan, sudah teruji) dan tawarkan Mode Duplikasi sebagai peningkatan opsional untuk screen yang genuinely butuh reviewer melihat UI+spec bersamaan.

## 23.3 Struktur Sheet `_Redr` pada Mode Duplikasi
1. **Area UI** (kiri): mulai kolom A, lebar SESUAI KEBUTUHAN redraw screen ini — TIDAK dibatasi rentang tetap (mis. bukan selalu A:AN). Setiap screen punya lebar area UI sendiri tergantung kompleksitas UI-nya. Lebar kolom di area ini tetap seragam 2,57 (lihat 3.5), tanpa merge, tanpa wrap text.
2. **2 Kolom Spacer** (WAJIB, tepat 2 kolom kosong): langsung setelah area UI berakhir. Kolom-kolom ini kosong (tidak ada konten), berfungsi sebagai jarak visual sekaligus tempat border pemisah.
3. **Area Spec** (kanan): mulai tepat setelah 2 kolom spacer. Berisi 5 section lengkap (Screen-State Inventory, Business Intent & Invariants, Business Rules, Functional UI Spec & Field Matrix — 24 kolom penuh, Message Catalog), SEMUA tanpa wrap text, rata kiri (beda dari sheet spec formal yang boleh tetap wrap text untuk kenyamanan baca vertikal). Field Matrix di panel ini tetap punya autofilter aktif.

## 23.4 Border Pemisah
Border tebal ditempatkan **di tengah gap**, yaitu pada sisi KANAN kolom spacer pertama (setara secara visual dengan sisi KIRI kolom spacer kedua — garis yang sama). Contoh: kalau spacer adalah kolom N dan N+1, maka border tebal diterapkan sebagai right-border pada seluruh cell di kolom N (baris yang relevan dengan area UI/spec).

## 23.5 Freeze Panes
`freeze_panes` diset ke kolom spacer KEDUA (baris 1). Contoh: spacer = kolom N (pertama) dan N+1 (kedua) → `ws.freeze_panes = cell(row=1, column=N+1_letter)`. Efeknya: area UI + kolom spacer pertama (sampai kolom N) tetap terlihat saat scroll horizontal; kolom spacer kedua (N+1) DAN seluruh area spec ikut ter-scroll bersama (bukan ikut membeku).

## 23.6 Self-Audit Pass Tambahan Khusus Mode Duplikasi (lihat juga 20.2)
Kalau Mode Duplikasi dipilih, tambahkan ke checklist Self-Audit Pass:
- [ ] Isi panel kanan Redrawn SAMA PERSIS dengan sheet spec formal — Rule ID, Component ID, Message ID, Related ID, status (Confirmed/Proposed/Auto-Applied/Open) semuanya identik?
- [ ] Tidak ada section yang cuma muncul di salah satu lokasi (panel Redrawn ATAU sheet formal) tanpa alasan?
- [ ] 2 kolom spacer + border + freeze pane sudah diterapkan sesuai 23.4/23.5 di SEMUA sheet `_Redr` Mode Duplikasi (bukan sebagian)?

## 23.7 Input Markdown Hasil Konversi Sumber Visual (perluasan 3.4b)
Selain Markdown sebagai input terstruktur murni (business rule/question bank, lihat 3.4b), Markdown SEKARANG juga bisa berupa **hasil konversi** dari sumber visual asli (Excel/PDF/Word/Image/Figma export) yang dilakukan DI LUAR sistem ini (oleh user, pakai tool lain) sebelum diupload. Kalau .md yang diupload merepresentasikan struktur UI/grid (mis. tabel pipe `|` yang mendeskripsikan kolom-kolom grid, layout field, dst) — PERLAKUKAN SEBAGAI PENGGANTI SUMBER VISUAL untuk keperluan redraw, BUKAN cuma business-rule text.
**Disambiguasi (pakai prinsip 3.3b Ambiguity Handling)**: kalau tidak jelas dari konteks/isi apakah .md yang diupload itu (a) business-rule/question bank, atau (b) hasil konversi visual — JANGAN tebak diam-diam. Heuristik bantu: isi berupa Question/Reference Bank terstruktur (ada header "Question:", "What-If:", dst — lihat template 14.4d) → business-rule bank; isi berupa tabel pipe yang mendeskripsikan layout/kolom UI tanpa header semacam itu → kemungkinan besar converted-visual. Kalau masih ambigu setelah heuristik ini, tanya user eksplisit sebelum lanjut.
**Sheet Snapshot untuk kasus converted-visual**: karena file visual ASLI tidak tersedia (cuma hasil konversi .md-nya), sheet `_Snap` berisi reproduksi TEKS ASLI dari .md tersebut (sama seperti perlakuan input teks chat murni di 3.4b), plus label eksplisit "Sumber asli: [tipe file disebutkan user, mis. Figma] — hanya tersedia dalam bentuk konversi Markdown, bukan file visual asli."

## 23.8 Interpretasi Pipeline Markdown → Kolom Logis (berlaku di redraw grid manapun, bukan cuma dari file .md)
Kalau requirement (dari sumber manapun — .md converted, teks chat, dokumen) berisi notasi pipe seperti `Group Principal | Penarik Bon | Sloc | Tgl. Posting | Status | Aksi`, setiap segmen di antara `|` adalah 1 HEADER KOLOM terpisah — WAJIB diterjemahkan jadi kolom visual sungguhan di redraw (grup cell berdampingan dengan border kolom logis, lihat 3.5/6.1), TIDAK PERNAH ditulis literal sebagai 1 baris teks dengan karakter `|` di dalam 1 cell. Baris data di bawah header pipe yang sama dipetakan 1:1 ke kolom yang sesuai (jumlah nilai harus sama dengan jumlah header; posisi data konsisten dengan header). Berlaku untuk semua grid: grid daftar utama, grid detail, grid lookup, grid popup/modal, tabel dokumen cetak.
**Quality check wajib sebelum finalisasi**: tidak ada karakter `|` tersisa di area UI; jumlah kolom header = jumlah nilai data per baris; kolom Aksi/View dipisah dari kolom Status (tidak digabung).

## 23.9 Precedence Khusus Layout Redrawn
Kalau ada perbedaan antara aturan umum Redrawn (3.5) dan aturan khusus di section ini: instruksi eksplisit user tentang layout > section 23 ini > aturan umum 3.5 > evidence visual sumber > proposed design agent.
