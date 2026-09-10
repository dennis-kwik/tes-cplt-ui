# 17. Workbook Architecture dan Formatting

## 17.1 Struktur sheet output
1. `Index_Summary` — daftar seluruh Desain UI/modul + hyperlink ke tiap sheet/section, ringkasan jumlah (screen, rule, field, message, assumption), blok "Keputusan Kritis Belum Dikonfirmasi", dan blok "Glosarium & Penjelasan".
2. Untuk SETIAP Desain UI yang terdeteksi, WAJIB 2 sheet berpasangan (lihat 3.4):
   * `[KODE]_[Screen]_Snapshot` — bukti asli input sebagai gambar embed.
   * `[KODE]_[Screen]_Redrawn` — versi digambar ulang agent mengikuti aturan teknis 3.5, WAJIB selalu ada (bukan opsional).
3. Satu sheet spec per Desain UI/screen-state: `[KODE]_[NamaScreen]` — berisi 5 section berurutan:
   1. Screen-State Inventory
   2. Business Intent/Invariants
   3. Business Rules
   4. Functional UI Spec & Field Matrix — SATU tabel, tapi dengan row-explosion per Mode×Status (lihat handbook 07); 1 baris = 1 component PADA 1 konteks final, bukan 1 baris umum per component
   5. Message Catalog
4. Sheet lintas-modul (satu sheet per jenis artefak, mencakup semua modul dalam file):
   * `Overview_Scope`
   * `Actor_Role_Permission`
   * `Data_API`
   * `What_If`
   * `Test_Scenario`
   * `Assumption_Decision_Risk_Open`
   * `Critical_Challenge_QnA` — devil's advocate, lihat handbook 19

Section yang TIDAK dibuat: Integration/Dependency, Security/Privacy/Audit, Concurrency/Transaction/Idempotency, NFR, Traceability (lihat 02 untuk alasan).

## 17.2 Penamaan sheet
* Sheet spec per screen memakai kode modul + nama screen singkat, contoh: `DSCAT34_MainPage`, `DSCAT34_AddEdit`. Maksimal 31 karakter (batas Excel) — singkat bila perlu dan catat nama penuh di Index_Summary.
* Sheet Snapshot/Redrawn: `[KODE]_[Screen]_Snap` dan `[KODE]_[Screen]_Redr` (disingkat supaya muat 31 karakter, mis. `DSCAT34_MainPage_Snap`, `DSCAT34_MainPage_Redr`) — nama penuh dicatat di Index_Summary.

## 17.3 Visual convention (sheet spec: Index_Summary, sheet per-UI, sheet lintas-modul)
* Dark blue/black: Section header.
* Gray: Table header/static structure.
* Yellow: Assumption/open confirmation.
* Light red: Critical validation/error/risk.
* Purple: Decision/control/technical logic.
* Light blue: Information/current behaviour.
* Green: Confirmed/approved bila status tersedia.

**Catatan penting — konteks warna berbeda di sheet "Desain UI":** aturan warna di atas berlaku untuk sheet SPEC (bukan sheet Desain UI). Di sheet "Desain UI" (khusus saat dipakai teknik cell-drawing, lihat 3.5), kuning berarti **row selected** pada mockup, merah muda berarti **error state** pada mockup, abu-abu berarti **input disabled** pada mockup — ini konvensi UI, bukan konvensi governance. Jangan disamakan maknanya walau warnanya sama.

## 17.4 Aturan format wajib (dieksekusi sebagai kode, bukan sekadar disebut di teks)
* Fill KUNING (solid, mis. FFFF00) WAJIB diterapkan ke SETIAP baris/cell berstatus assumption/proposed-belum-dikonfirmasi. Menulis teks "ASUMSI - perlu konfirmasi BA/PO" tanpa fill warna = TIDAK LENGKAP. Ini adalah gap paling sering ditemukan pada hasil aktual — jangan anggap teks saja cukup.
* Fill pink/merah muda pada baris critical validation/error/risk.
* Autofilter WAJIB aktif pada range header SETIAP tabel data, di semua sheet spec & lintas-modul — bukan hanya sebagian sheet.
* Hide gridlines pada sheet spec (boleh tampil di sheet Desain UI bila membantu grid visual / mengikuti sumber asal).
* Freeze pane pada header tabel; wrap text; kolom cukup lebar untuk dibaca (kecuali area Desain UI, lihat 3.4).
* Setiap sheet spec memiliki hyperlink kembali ke `Index_Summary`.

### Gate format — cek ulang sebelum finalisasi
Sebelum file dianggap selesai, verifikasi eksplisit: (1) semua baris assumption sudah fill kuning bukan cuma teksnya; (2) autofilter aktif di semua tabel; (3) freeze pane aktif. Kalau ada yang belum terpenuhi, perbaiki dulu — ini bagian dari Definition of Done (lihat 01.2), bukan langkah opsional yang boleh dilewati demi kecepatan.
