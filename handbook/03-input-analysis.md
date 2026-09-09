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

## 3.4 Aturan wajib sheet "Desain UI" (embed/copy asli, bukan rekonstruksi manual)
Root cause kegagalan versi sebelumnya adalah proses REKONSTRUKSI MANUAL cell-per-cell (rawan merge-cell error). Pendekatan sekarang: gunakan Code Interpreter/engine kode agent untuk mengambil OBJEK ASLI, bukan menggambar ulang.
* **IF input = gambar** THEN embed FILE GAMBAR ASLI (byte asli) ke sheet "Desain UI" sebagai objek picture (mis. `ws.add_image()` pada openpyxl), diberi anchor rapi (mis. mulai sel A1) dan judul/kode modul di atas gambar. TIDAK digambar ulang manual.
  * Fallback (hanya jika embed image tidak didukung environment): gambar ulang mengacu Chameleon reference (lihat 02), pakai teknik cell-drawing tanpa merge & lebar kolom seragam ~2,6 cm.
* **IF input = Excel (desain cell UI)** THEN COPY sheet asli secara terprogram (value, style, fill, border, column width, row height, termasuk merge cell bila memang ada di asal) ke sheet "Desain UI" — bukan diketik ulang manual satu-satu.
* Jika 1 file berisi banyak modul, sheet Desain UI bisa 1 per modul (`[KODE]_DesainUI`) mengikuti sumber asal masing-masing.
