# 3. Cara Membaca Input Visual dan Excel

## 3.1 Visual inspection
* Baca judul, kode modul, section band, label, tanda mandatory, placeholder, sample value, border, alignment, warna, icon, selection state, dan grouping.
* Periksa elemen kecil: pencil, eye, calendar, search, row checkbox, sort marker, pagination, helper text, dan empty region yang mungkin merupakan container.
* Bedakan informasi yang terlihat dengan inferensi. Catat evidence visual dan confidence bila diperlukan.
* Lakukan second-pass verification sebelum menyusun component inventory.

## 3.2 Excel inspection
* Scan setiap sheet, termasuk hidden sheet bila dapat diakses.
* Deteksi beberapa desain dalam satu sheet melalui dark header, merged title, whitespace, border, dan label Main Page/Add/Edit/Detail/Popup/Tab.
* Pertahankan grouping berdasarkan kode modul, bukan berdasarkan jenis artefak.
* Jangan menganggap cell kosong tidak penting. Layout, merged cells, shape, dan visual grouping dapat membawa makna.

## 3.3 Evidence classification
* CONFIRMED: Diberikan eksplisit oleh user atau dokumen approved. Tuliskan sebagai requirement; sertakan source.
* OBSERVED: Terlihat pada UI/existing system tetapi belum dikonfirmasi sebagai target. Tuliskan sebagai current state.
* INFERRED: Kesimpulan logis dari beberapa evidence. Jelaskan dasar inferensi; tandai untuk review.
* PROPOSED: Rekomendasi teknis atau future-proof design. Jangan tulis sebagai business fact.
* ASSUMPTION: Diperlukan untuk melengkapi spec tetapi belum diketahui. Kuning; ID; reason; impact; confirm by.
* OPEN: Belum dapat diputuskan. Masukkan Open Question dan impact.