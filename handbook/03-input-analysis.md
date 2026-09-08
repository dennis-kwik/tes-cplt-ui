# 3. Cara Membaca Input Visual dan Excel

## 3.1 Visual inspection (input gambar)
* Baca judul, kode modul, section band, label, tanda mandatory, placeholder, sample value, border, alignment, warna, icon, selection state, dan grouping.
* Periksa elemen kecil: pencil, eye, calendar, search, row checkbox, sort marker, pagination, helper text.
* Bedakan informasi yang terlihat dengan inferensi.
* Setelah dianalisis, gambar UI wajib **digambar ulang** sebagai sheet "Desain UI" mengikuti gaya komponen pada Chameleon Angular Framework reference (lihat 02), menggunakan teknik cell-drawing (lihat 3.4). Ini bukan screenshot tempel, melainkan rekonstruksi rapi berbasis cell Excel.

## 3.2 Excel inspection (input Excel desain cell UI)
* Scan SETIAP sheet tanpa terkecuali.
* Satu sheet dapat berisi LEBIH DARI SATU desain UI (contoh: "Main Page" dan "Add/Edit Mode" pada sheet yang sama) — deteksi lewat dark header band, label section ("Main Page", "Add/Edit Mode", "Popup", "Tab ..."), dan whitespace pemisah.
* File dapat berisi LEBIH DARI SATU sheet — setiap sheet dibaca menyeluruh; jangan berhenti di sheet pertama.
* Setiap desain UI yang terdeteksi (baik beda sheet maupun dalam satu sheet) menjadi unit analisis terpisah dan mendapat sheet spec sendiri (lihat 17).
* Sheet "Desain UI" pada output WAJIB berupa salinan PERSIS dari desain asli input (bukan gambar ulang) — lihat 3.4.

## 3.3 Evidence classification
* CONFIRMED: Diberikan eksplisit oleh user/dokumen approved.
* OBSERVED: Terlihat pada UI/existing system, belum dikonfirmasi sebagai target.
* INFERRED: Kesimpulan logis dari evidence; jelaskan dasarnya, tandai untuk review.
* PROPOSED: Rekomendasi teknis/future-proof design; jangan tulis sebagai business fact.
* ASSUMPTION: Diperlukan untuk melengkapi spec tapi belum diketahui — kuning; ID; reason; impact; confirm by.
* OPEN: Belum dapat diputuskan — masuk Assumption/Decision/Risk/Open Question sheet.

## 3.4 Aturan wajib reproduksi sheet "Desain UI" (root cause kegagalan sebelumnya)
* **DILARANG merge cell** dalam area desain UI — merge menyebabkan output gagal/rusak.
* Gunakan lebar kolom SERAGAM dan sempit (~2,6 cm / setara openpyxl width ≈ 11) di seluruh area desain agar cell berperan sebagai "grid pixel".
* Bentuk tombol/box/field dibuat dengan border+fill pada rentang beberapa cell sempit yang berdekatan (bukan 1 cell lebar/merge).
* Teks panjang memakai wrap text dan row height, bukan merge cell antar kolom.
* Jika input Excel: salin persis struktur, teks, dan posisi asal ke sheet "Desain UI" (1:1). Jika input gambar: rekonstruksi dengan teknik yang sama, serapi mungkin, mengacu Chameleon reference untuk gaya komponen (warna tombol, bentuk field, dsb.).
