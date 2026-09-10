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

## 3.4 Aturan wajib sheet "Desain UI" — WAJIB 2 SHEET PER UI DESIGN (snapshot asli + redraw agent)
Setiap Desain UI yang terdeteksi WAJIB menghasilkan **2 sheet terpisah**, bukan 1:
1. **`[KODE]_[Screen]_Snapshot`** — bukti asli input, SELALU berupa gambar/foto embed (`ws.add_image()`). IF input berupa Excel (cell design) THEN render/screenshot area desain tersebut jadi gambar dulu (bukan copy sheet mentah) sebelum di-embed — supaya konsisten format snapshot untuk semua tipe input. IF input gambar/PDF/Word yang mengandung gambar mockup THEN embed gambar asli (byte asli) apa adanya.
2. **`[KODE]_[Screen]_Redrawn`** — versi yang DIGAMBAR ULANG oleh agent sendiri di cell Excel, WAJIB SELALU dibuat (bukan lagi fallback opsional) mengikuti aturan teknis 3.5 secara penuh. Ini jadi versi "resmi" yang konsisten stylenya di semua modul, terlepas dari kualitas/resolusi snapshot asli.
"1 sheet = 1 UI": kalau 1 modul punya >1 Desain UI (mis. Main Page + Add/Edit), masing-masing dapat pasangan Snapshot+Redrawn sendiri — jangan digabung jadi 1 sheet campur.

## 3.4b Tipe input yang didukung
* **Gambar** (jpg/png/dll): sumber utama untuk redraw + snapshot langsung.
* **Excel (cell design)**: area desain di-screenshot/render jadi gambar untuk sheet Snapshot; dipakai juga sebagai acuan detail untuk sheet Redrawn.
* **PDF**: tiap halaman yang mengandung mockup dirender jadi gambar (rasterize per halaman), diperlakukan sama seperti input gambar.
* **Word (.docx)**: ekstrak gambar mockup yang di-embed di dalam dokumen (diperlakukan seperti input gambar) DAN ekstrak teks requirement/business rule tertulis di dokumen (jadi input tambahan untuk Business Rules/Assumption, BUKAN untuk redraw UI).
* **Markdown (.md)**: BUKAN sumber visual — dipakai sebagai input terstruktur pelengkap (business rule yang sudah ditulis manusia, question/reference bank per tipe komponen). Isinya di-parse dan dipetakan ke Business Rules/Field Matrix/Critical_Challenge_QnA sesuai konten; tidak menghasilkan sheet Desain UI.

## 3.5 Aturan teknis cell-drawing (WAJIB — dipakai di SETIAP sheet `[KODE]_[Screen]_Redrawn`)
Berlaku untuk sheet Redrawn yang WAJIB selalu dibuat (lihat 3.4). Ini SEMUA wajib dieksekusi sebagai kode (openpyxl), bukan sekadar disebut:
* **Lebar kolom seragam 2,57** (`column_dimensions[col].width = 2.57`) di SELURUH kolom yang menjadi area desain UI — konsisten dari kiri ke kanan, tidak ada kolom lebih lebar/sempit di tengah area.
* **TIDAK ADA merge cell** di area desain sama sekali — bentuk elemen lebar dibuat dari beberapa cell sempit berdampingan, bukan 1 cell yang di-merge.
* **TIDAK ADA wrap text**; semua teks **rata kiri** (`horizontal='left'`), termasuk label yang biasanya rata tengah di UI asli — konsistensi grid lebih penting daripada meniru alignment visual persis.
* **Button multi-cell**: beberapa cell berdampingan yang membentuk 1 tombol WAJIB punya **1 border luar saja** (outer border di 4 sisi rentang), dan **cell internal di antaranya TIDAK punya border vertikal** — supaya terlihat sebagai 1 tombol utuh, bukan beberapa kotak terpisah.
* **Tab aktif vs nonaktif** harus bisa dibedakan visual (mis. aktif = fill lebih gelap/bold/tanpa border bawah menyatu dengan konten; nonaktif = fill lebih terang/normal).
* **Input disabled** = fill abu-abu (mis. D9D9D9).
* **Row selected** (baris grid yang sedang dipilih user) = fill kuning. **PENTING — beda konteks dari kuning "assumption" di sheet spec** (17.3/17.4): kuning di sheet Desain UI berarti "baris terpilih/selection state" pada mockup, BUKAN penanda assumption. Jangan disamakan maknanya.
* **Error state** = fill merah muda (sama seperti convention critical/error di 17.3).
* **Loading state dan empty state** WAJIB direpresentasikan sebagai bagian dari desain (mis. baris tambahan/varian kecil yang menunjukkan skeleton/spinner placeholder dan tampilan "data kosong"), bukan cuma default state terisi data.
* **Dropdown utama** (dropdown yang jadi filter/pilihan penting, bukan dekorasi) WAJIB diberi **Data Validation** Excel asli (`openpyxl.worksheet.datavalidation.DataValidation`, type="list") supaya benar-benar berfungsi sebagai dropdown saat file dibuka, bukan cuma gambar visual dropdown.
