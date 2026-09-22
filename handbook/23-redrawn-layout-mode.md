# 23. Layout Redrawn — UI + Panel Spec Kanan (FORMAT BAKU, bukan pilihan)
Diformalkan setelah uji coba nyata (proyek PROMT02 - Penarikan Material) menemukan kebutuhan reviewer melihat UI dan spec sekaligus dalam 1 sheet, tanpa berpindah ke sheet spec formal. **Ini SEKARANG format baku wajib untuk SEMUA sheet `_Redr`** — bukan lagi pilihan mode yang perlu dikonfirmasi user (versi sebelumnya sempat ada "Mode Duplikasi vs Mode Terpisah"; Mode Terpisah DIHAPUS, tidak ada lagi pertanyaan konfirmasi untuk dimensi ini).

## 23.1 Struktur Sheet `_Redr`
1. **Area UI** (kiri): mulai kolom A, lebar SESUAI KEBUTUHAN redraw screen ini — TIDAK dibatasi rentang tetap (bukan selalu A:AN). Setiap screen punya lebar area UI sendiri tergantung kompleksitas UI-nya. Lebar kolom seragam 2,57 (lihat 3.5), tanpa merge, tanpa wrap text.
2. **2 Kolom Spacer** (WAJIB, tepat 2 kolom kosong): langsung setelah area UI berakhir.
3. **Panel Spec Kanan** (WAJIB): mulai tepat setelah 2 kolom spacer. Berisi **Narrative Spec Panel** (lihat 3.4e) — narasi `Kolom | Spec` terkelompok per section, mengikuti Traversal Order (3.4c). BUKAN salinan identik sheet spec formal — kedalaman diatur oleh Depth Balance (3.4f): narasi ≤ spec formal, spec formal tidak boleh jauh lebih dangkal dari narasi. Semua tanpa wrap text, rata kiri.

## 23.2 Border Pemisah
Border tebal ditempatkan **di tengah gap**, pada sisi KANAN kolom spacer pertama (setara visual dengan sisi KIRI kolom spacer kedua — garis yang sama). Contoh: spacer = kolom N dan N+1 → border tebal = right-border pada seluruh cell kolom N (baris yang relevan dengan area UI/spec).

## 23.3 Freeze Panes
`freeze_panes` diset ke kolom spacer KEDUA (baris 1). Contoh: spacer N (pertama), N+1 (kedua) → `ws.freeze_panes = cell(row=1, column=N+1_letter)`. Area UI + spacer pertama tetap terlihat saat scroll horizontal; spacer kedua + panel spec ikut ter-scroll bersama.

## 23.4 Self-Audit Pass Tambahan (lihat juga 20.2)
- [ ] Panel spec kanan mengikuti Depth Balance (3.4f) — bukan lebih dangkal, bukan lebih detail dari spec formal?
- [ ] Tidak ada duplikasi trigger antara Tools/Trigger dan List View Kolom di panel narasi (3.4e)?
- [ ] 2 kolom spacer + border + freeze pane diterapkan konsisten di SEMUA sheet `_Redr` (bukan sebagian)?

## 23.5 Input Markdown Hasil Konversi Sumber Visual (perluasan 3.4b)
Selain Markdown sebagai input terstruktur murni (business rule/question bank, lihat 3.4b), Markdown SEKARANG juga bisa berupa **hasil konversi** dari sumber visual asli (Excel/PDF/Word/Image/Figma export) yang dilakukan DI LUAR sistem ini sebelum diupload. Kalau .md yang diupload merepresentasikan struktur UI/grid (mis. tabel pipe `|` yang mendeskripsikan kolom-kolom grid) — PERLAKUKAN SEBAGAI PENGGANTI SUMBER VISUAL untuk redraw, BUKAN cuma business-rule text.
**Disambiguasi (prinsip 3.3b)**: kalau tidak jelas apakah .md itu (a) business-rule/question bank, atau (b) hasil konversi visual — JANGAN tebak diam-diam. Heuristik: isi berupa Question/Reference Bank terstruktur → business-rule bank; isi berupa tabel pipe mendeskripsikan layout/kolom UI tanpa header semacam itu → kemungkinan converted-visual. Kalau masih ambigu, tanya user eksplisit.
**Sheet Snapshot untuk kasus converted-visual**: file visual ASLI tidak tersedia, sheet `_Snap` berisi reproduksi TEKS ASLI dari .md tersebut + label eksplisit "Sumber asli: [tipe file] — hanya tersedia dalam bentuk konversi Markdown."

## 23.6 Interpretasi Pipeline Markdown → Kolom Logis
Kalau requirement (sumber manapun) berisi notasi pipe seperti `Group Principal | Penarik Bon | Sloc | Status | Aksi`, setiap segmen adalah 1 HEADER KOLOM terpisah — WAJIB diterjemahkan jadi kolom visual sungguhan di redraw, TIDAK PERNAH ditulis literal dengan karakter `|` di 1 cell. Berlaku untuk semua grid.
**Quality check**: tidak ada `|` tersisa di area UI; jumlah kolom header = jumlah nilai data per baris; kolom Aksi/View dipisah dari kolom Status.

## 23.7 Precedence Khusus Layout Redrawn
Kalau ada perbedaan antara aturan umum Redrawn (3.5) dan aturan khusus di section ini: instruksi eksplisit user tentang layout > section 23 ini > aturan umum 3.5 > evidence visual sumber > proposed design agent.
