# 22. Excel Generation Safety Guardrails
Ditambahkan setelah ditemukan kasus nyata: file blueprint hasil generate **Claude** memicu prompt "We found a problem with some content" saat dibuka di Microsoft Excel — hasil generate Copilot Studio pada kasus yang sama terbukti aman dibuka. Section ini tetap dimasukkan ke knowledge base bersama (dipakai baik oleh Claude maupun Copilot Studio) sebagai pencegahan preventif, karena root cause-nya (nama sheet invalid, hyperlink ke referensi belum final, copy sheet via manipulasi XML mentah, dst) adalah kelas risiko umum pada proses generate `.xlsx` lewat kode apapun platformnya. WAJIB diikuti setiap kali men-generate file .xlsx untuk blueprint ini.

## 22.1 Penyebab Umum File .xlsx Rusak
* Nama sheet melebihi 31 karakter, mengandung karakter terlarang (`: \ / ? * [ ]`), duplikat, atau diawali/diakhiri tanda kutip.
* Merged cell range yang overlap satu sama lain, atau overlap dengan area yang juga kena AutoFilter/Table.
* Data Validation dengan list literal (`formula1='"A,B,C"'`) melebihi 255 karakter — WAJIB pakai named range/reference cell kalau opsi banyak, bukan inline list panjang.
* Hyperlink internal yang menunjuk ke sheet/cell yang TIDAK ADA (mis. nama sheet berubah/dipotong ke 31 karakter setelah link ditulis, sehingga link jadi tidak valid) — lihat 7.3c, index HARUS dibangun dari nama sheet FINAL, bukan nama sebelum dipotong.
* AutoFilter range yang melebihi dimensi aktual data, atau lebih dari 1 AutoFilter region tumpang tindih di 1 sheet.
* Freeze pane menunjuk cell yang tidak valid/di luar area data.
* **Copy sheet mentah antar workbook lewat manipulasi XML langsung** (bukan lewat API resmi seperti openpyxl cell-by-cell value+style copy) — penyebab paling umum untuk kasus "sheet asli di-copy 1:1" (lihat 3.4/17). WAJIB pakai API resmi library (contoh: openpyxl `cell.value`, `cell.font`, `cell.fill`, `cell.border` disalin satu-satu, BUKAN copy elemen XML mentah antar file `.xlsx`).
* Gambar dengan format tidak didukung penuh (mis. webp, bmp eksotik) atau byte gambar yang corrupt/tidak lengkap saat di-embed.
* Style/font object dibuat baru berulang-ulang untuk tiap cell alih-alih di-reuse — bisa membengkakkan style table dan memicu masalah di file besar.

## 22.2 Aturan Wajib Saat Generate
1. Validasi nama sheet SEBELUM dipakai: potong ke 31 karakter, hapus karakter terlarang, pastikan unique dalam 1 workbook — baru dipakai sebagai nama final untuk index hyperlink (7.3c).
2. Jangan buat merge cell yang overlap; kalau ragu, hindari merge sama sekali di area tabel data (sheet spec) — merge hanya dipakai di sheet `_Redrawn` mengikuti sumber asli, dan tetap dicek tidak overlap.
3. Data Validation list panjang → pakai reference ke range/kolom helper, bukan literal string inline.
4. Hyperlink internal HANYA ditulis pada tahap ke-2 (setelah semua sheet final dan nama sheet sudah final) — lihat 7.3c.
5. 1 AutoFilter region per sheet, range-nya PERSIS sama dengan luas data aktual (tidak lebih, tidak kurang).
6. Freeze pane HANYA menunjuk cell yang benar-benar ada dalam data.
7. Copy sheet asli (3.4) SELALU lewat API resmi (baca value/style lalu tulis ulang cell demi cell), TIDAK PERNAH lewat manipulasi arsip/XML mentah.
8. Embed gambar hanya format PNG/JPEG, verifikasi ukuran byte > 0 sebelum embed.
9. Reuse style/font object antar cell dengan format sama, jangan instansiasi baru berulang tanpa perlu.

## 22.3 Aturan Redraw (`_Redrawn`) — Ringkas
Lebar kolom seragam 2,57; TANPA merge cell; TANPA wrap text, rata kiri; button multi-cell = 1 border luar tanpa border vertikal internal; tab aktif/nonaktif beda visual; disabled=abu-abu, selected=kuning (beda makna dari kuning assumption — lihat 17.3), error=pink; loading & empty state direpresentasikan; dropdown utama pakai Data Validation asli (bukan literal list panjang — lihat 22.1). Detail penuh: 3.5.

## 22.4 Urutan Proses Generate yang Aman
1. Tulis SEMUA konten sheet (value, style dasar) TANPA hyperlink dulu.
2. Finalisasi nama semua sheet (setelah dipastikan valid & unique).
3. Bangun index ID→(sheet final, cell) dan Related-ID→cell (7.3c).
4. Tempel SEMUA hyperlink internal — validasi setiap target benar-benar ada sebelum menempel.
5. Terapkan AutoFilter, Freeze Pane per sheet (validasi range sesuai data aktual).
6. Jalankan Self-Audit Pass (20).
7. **File Integrity Check** (22.5) — WAJIB sebelum file dianggap selesai.

## 22.5 File Integrity Check (WAJIB, langkah paling akhir)
Sebelum menyerahkan file ke user:
1. Coba BUKA ULANG file yang baru disimpan menggunakan library yang sama (mis. `openpyxl.load_workbook()` pada file hasil `wb.save()`) — kalau proses buka-ulang ini error/exception, file KEMUNGKINAN BESAR rusak, JANGAN diserahkan ke user. Perbaiki dulu penyebabnya (cek 22.1) dan generate ulang.
2. Verifikasi jumlah sheet, nama sheet, dan beberapa sample cell value cocok dengan yang dimaksud (sanity check ringan, bukan replay penuh).
3. Kalau tersedia tool command-line untuk validasi lebih lanjut (mis. unzip struktur `.xlsx` dan cek `[Content_Types].xml` konsisten dengan isi), jalankan sebagai lapisan tambahan — terutama untuk file dengan banyak gambar/hyperlink/data validation.
