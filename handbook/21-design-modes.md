# 21. Mode Desain — Enterprise/Configurable vs Simple
Standar maksimal (row-explosion penuh, 16 kategori What-If, 10 domain Critical Challenge, Self-Audit Pass lengkap) terlalu berat untuk aplikasi sederhana — dipaksakan penuh ke semua kasus menghasilkan over-engineering yang justru lebih sulit direview manusia.

## 21.1 Perbandingan Mode
| | Mode Enterprise/Configurable | Mode Simple |
|---|---|---|
| Row-explosion | Penuh, semua Mode×Status | Hanya kalau ada perbedaan behaviour signifikan |
| What-If | Semua 16 kategori wajib | Subset relevan (5-6 kategori paling applicable) |
| Critical Challenge | 8-15/screen, 10 domain penuh | 3-5/screen, domain paling applicable |
| Data model | Effective dating & config-driven by default (lihat 3.3d) | Normalized standar; config-driven hanya kalau diminta eksplisit |
| Self-Audit Pass | 6 item penuh (lihat 20) | Item inti saja (ambiguity check + Component ID check) |

## 21.2 Penentuan Mode
Claude memberi REKOMENDASI otomatis berdasarkan heuristik:
* Jumlah komponen per screen (banyak → indikasi Enterprise).
* Ada/tidaknya data finansial (nilai transaksi, invoice, dsb).
* Ada/tidaknya approval chain multi-aktor (maker-checker, workflow bertingkat).
* Indikasi kebutuhan configurability eksplisit dari requirement (lihat 3.3c/3.3d).

TAPI user WAJIB konfirmasi eksplisit sebelum generate jalan — jangan salah klasifikasi diam-diam. Ini konsisten dengan prinsip 3.3b (Ambiguity Handling): penentuan mode sendiri adalah keputusan yang bisa ambigu, jadi tidak boleh diputuskan sepihak tanpa konfirmasi.
