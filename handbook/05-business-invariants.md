# 5. Business Intent, Invariants, Current State, dan Proposed Design
Future-proof blueprint harus memisahkan apa yang tidak boleh berubah dari cara implementasi saat ini. Pemisahan ini mencegah redevelopment menyalin limitation UI lama sebagai business rule baru.

* Business Intent: Nilai bisnis apa yang ingin dicapai? Contoh: Mengontrol keterangan bon yang berlaku untuk principal dan periode tertentu.
* Business Invariant: Apa yang harus tetap benar di semua teknologi/channel? Contoh: Tidak boleh ada dua aturan efektif yang ambigu untuk scope yang sama.
* Current State: Bagaimana sistem/mockup saat ini bekerja? Contoh: Web dan Mobile ditampilkan sebagai dua checkbox.
* Proposed Design: Bagaimana implementasi disarankan? Contoh: Gunakan Channel Master agar channel baru dapat ditambah tanpa schema change.
* Constraint: Batas nyata apa yang berlaku? Contoh: Consumer lama membutuhkan field tertentu selama masa transisi.
* Decision: Apa yang dipilih dan mengapa? Contoh: Gunakan soft delete karena audit dan restore diperlukan.

Anti-pattern: Jangan mengubah "UI memiliki dua checkbox Web/Mobile" menjadi invariant "sistem hanya boleh memiliki dua channel". Invariant yang tepat adalah "minimal satu channel harus dipilih untuk activation".

## 5.1 Pertanyaan Wajib Future-Proof 5 Tahun
Setiap modul WAJIB dijawab eksplisit di sini: **"Apa yang mungkin berubah dalam 5 tahun yang desain ini harus sudah akomodasi sejak sekarang?"** Target future-proof: minimum 5 tahun tanpa perlu redevelopment struktural. Pertimbangkan (tidak terbatas pada): perubahan struktur organisasi, regulasi, volume data, channel baru, dan driver kontekstual sesuai jenis menu ini — termasuk tapi TIDAK TERBATAS pada AI/automation (auto-suggest, otomasi keputusan) KALAU genuinely relevan ke sifat menu tersebut. Jangan tambahkan pertimbangan AI secara mekanis ke semua modul tanpa menilai relevansinya ke konteks spesifik menu.