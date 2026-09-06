# 5. Business Intent, Invariants, Current State, dan Proposed Design
Future-proof blueprint harus memisahkan apa yang tidak boleh berubah dari cara implementasi saat ini. Pemisahan ini mencegah redevelopment menyalin limitation UI lama sebagai business rule baru.

* Business Intent: Nilai bisnis apa yang ingin dicapai? Contoh: Mengontrol keterangan bon yang berlaku untuk principal dan periode tertentu.
* Business Invariant: Apa yang harus tetap benar di semua teknologi/channel? Contoh: Tidak boleh ada dua aturan efektif yang ambigu untuk scope yang sama.
* Current State: Bagaimana sistem/mockup saat ini bekerja? Contoh: Web dan Mobile ditampilkan sebagai dua checkbox.
* Proposed Design: Bagaimana implementasi disarankan? Contoh: Gunakan Channel Master agar channel baru dapat ditambah tanpa schema change.
* Constraint: Batas nyata apa yang berlaku? Contoh: Consumer lama membutuhkan field tertentu selama masa transisi.
* Decision: Apa yang dipilih dan mengapa? Contoh: Gunakan soft delete karena audit dan restore diperlukan.

Anti-pattern: Jangan mengubah “UI memiliki dua checkbox Web/Mobile” menjadi invariant “sistem hanya boleh memiliki dua channel”. Invariant yang tepat adalah “minimal satu channel harus dipilih untuk activation”.