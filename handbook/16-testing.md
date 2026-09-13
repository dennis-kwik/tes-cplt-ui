# 16. Testing Strategy
Sheet gabungan lintas-modul: `Test_Scenario`.

## 16.1 Test taxonomy
* Positive dan alternate flow.
* Negative dan validation.
* Boundary dan equivalence partition.
* Authorization dan segregation of duties (bila role dibedakan pada UI).
* Future-change test untuk setiap what-if kritikal.

## 16.2 Keterhubungan minimal (pengganti Traceability penuh)
Setiap baris Test Scenario wajib mencantumkan kolom Rule/WF ID dan Component ID agar tetap tertelusur ke sheet Desain UI/modul asal tanpa perlu sheet Traceability terpisah.
* Critical Business Rule: minimal 1 test positive + 1 test negative/boundary.
* What-If Kritikal: minimal 1 impact test.
* Assumption berdampak tinggi: test placeholder + status "menunggu konfirmasi".

## 16.3 Formula minimum coverage (WAJIB DIHITUNG, bukan diperkirakan)
Root cause ditemukan pada hasil produksi: jumlah test scenario "terasa cukup" (mis. 10 test) padahal jauh di bawah kebutuhan riil modul dengan banyak Business Rule Critical. Untuk mencegah under-coverage yang tidak disadari:
```
Jumlah Test Scenario minimum = (2 × jumlah Business Rule berprioritas Critical) + (1 × jumlah Critical Challenge, semua severity)
```
Sebelum finalisasi, hitung jumlah aktual Test Scenario dan bandingkan ke formula ini. Kalau di bawah angka minimum, WAJIB tambah test sampai memenuhi — bukan berhenti di angka yang terasa cukup secara subjektif. Angka ini adalah lantai minimum, bukan target ideal; boleh lebih banyak kalau modul memang kompleks.
