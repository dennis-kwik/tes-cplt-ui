# 17. Workbook Architecture dan Formatting

## 17.1 Struktur sheet output
1. `Index_Summary` — daftar seluruh Desain UI/modul + hyperlink ke tiap sheet/section, ringkasan jumlah (screen, rule, field, message, assumption), blok "Keputusan Kritis Belum Dikonfirmasi", dan blok "Glosarium & Penjelasan".
2. `Desain UI` (satu sheet, atau satu sheet per modul bila jumlah desain besar: `[KODE]_DesainUI`) — reproduksi/rekonstruksi tampilan UI asli, lihat 3.4.
3. Satu sheet per Desain UI/screen-state: `[KODE]_[NamaScreen]` — berisi 6 section berurutan:
   1. Screen-State Inventory
   2. Business Intent/Invariants
   3. Business Rules
   4. Functional UI Spec
   5. Field Matrix
   6. Message Catalog
4. Sheet lintas-modul (satu sheet per jenis artefak, mencakup semua modul dalam file):
   * `Overview_Scope`
   * `Actor_Role_Permission`
   * `Data_API`
   * `What_If`
   * `Test_Scenario`
   * `Assumption_Decision_Risk_Open`

Section yang TIDAK dibuat: Integration/Dependency, Security/Privacy/Audit, Concurrency/Transaction/Idempotency, NFR, Traceability (lihat 02 untuk alasan).

## 17.2 Penamaan sheet
* Sheet UI per screen memakai kode modul + nama screen singkat, contoh: `DSCAT34_MainPage`, `DSCAT34_AddEdit`. Maksimal 31 karakter (batas Excel) — singkat bila perlu dan catat nama penuh di Index_Summary.
* Sheet Desain UI: `Desain UI` bila 1 modul, atau `[KODE]_DesainUI` bila banyak modul dalam 1 file.

## 17.3 Visual convention
* Dark blue/black: Section header.
* Gray: Table header/static structure.
* Yellow: Assumption/open confirmation.
* Light red: Critical validation/error/risk.
* Purple: Decision/control/technical logic.
* Light blue: Information/current behaviour.
* Green: Confirmed/approved bila status tersedia.

## 17.4 Aturan format wajib
* Hide gridlines pada sheet spec (boleh tampil di sheet Desain UI bila membantu grid visual).
* Freeze pane pada header tabel; filter aktif; wrap text; kolom cukup lebar untuk dibaca (kecuali area Desain UI, lihat 3.4).
* Setiap sheet spec memiliki hyperlink kembali ke `Index_Summary`.
