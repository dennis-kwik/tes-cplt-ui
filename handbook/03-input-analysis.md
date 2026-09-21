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

## 3.3b Ambiguity Handling (WAJIB — root cause kegagalan paling sering ditemukan)
Requirement dari user (terutama requirement teks bebas, bukan mockup visual presisi) sering punya frasa yang secara gramatikal bisa dibaca >1 cara. Contoh nyata: "job nya nanti bentuk pdf per 1 page = 1 faktur" bisa dibaca (a) "1 file PDF, tiap halaman = 1 faktur" ATAU (b) "1 file PDF per faktur (N file terpisah)". Kedua bacaan itu VALID secara gramatikal.
**Aturan wajib:** begitu agent mendeteksi frasa dengan >1 tafsiran valid, JANGAN memilih salah satu secara diam-diam dan menuliskannya seolah itu satu-satunya kebenaran. Sebagai gantinya:
1. Tulis KEDUA (atau semua) tafsiran secara eksplisit di sheet `Assumption_Decision_Risk_Open` sebagai 1 entry Decision, dengan opsi A/B/dst beserta dampak masing-masing ke Data_API, UX, Message Catalog, Test Scenario.
2. Tulis juga 1 entry terkait di `What_If_Critical_Challenge` (Section B) yang menantang tafsiran ini secara eksplisit.
3. Pilih SATU tafsiran sebagai "default sementara" untuk keperluan drafting spec lainnya, tapi tandai eksplisit sebagai default sementara (bukan final).
4. **Konsistensi lintas-sheet WAJIB**: begitu default sementara dipilih, SEMUA sheet lain yang menyinggung topik itu (Business Rules, Field Matrix, Message Catalog, Data_API, Test Scenario) WAJIB memakai tafsiran default yang SAMA — dilarang keras 1 sheet memakai tafsiran A dan sheet lain memakai tafsiran B tanpa disadari. Ini yang paling sering luput karena workbook besar dengan banyak sheet — lihat 20 (Self-Audit Pass) untuk cara mengecek ini sebelum finalisasi.

## 3.3c Configurability Elicitation — HARD STOP (WAJIB)
Kalau user meminta mode "highly configurable" TAPI tidak memberi informasi apapun (satu kata pun) soal: apa yang perlu configurable, siapa yang mengelola config, atau dimensi scope-nya — **PROSES BERHENTI (hard stop)**. Jangan lanjut generate dengan asumsi sendiri untuk keputusan fondasi ini. Ajukan pertanyaan eksplisit dulu:
* Field/parameter apa saja yang perlu configurable (bukan hardcode)?
* Siapa yang mengelola configuration tsb, di level scope apa (lihat 3.3d)?
* Ada precedent/pola existing yang harus diikuti?
Beda dari Assumption biasa (field-level, mudah dikoreksi belakangan) — keputusan scope configurability adalah fondasi struktur data model, salah di awal menjalar ke semua sheet turunan.

## 3.3d Struktur Scope Configurability — Generik (WAJIB, prinsip Highly Configurable)
"Highly Configurable" TIDAK berarti row-explosion lebih banyak — kategori masalah berbeda. Polanya:
* **Master Configuration Engine**: nilai yang berpotensi beda per konteks organisasi (pilihan dropdown, isi notes, batas validasi/range, visibility field) TIDAK hardcode di Business Rule/Field Matrix, melainkan direferensikan ke entity Config Master terpisah dengan dimensi scope GENERIK (Scope Level 1/2/3/... — jangan asumsikan struktur spesifik seperti PT/RSO/Area kecuali user eksplisit menyebutkannya).
* Level scope tertinggi (pusat) mengelola Config Master; level di bawah inherit/override sesuai desain yang dikonfirmasi user.
* Transaction screen query Config Master sesuai scope user login — tanpa logic hardcode "IF Area=X THEN...".
* Berlaku ke semua jenis nilai berpotensi beda per organisasi: pilihan konten, parameter validasi, bahkan visibility/mandatory field.
* Field Matrix yang menulis nilai tetap di Min/Max/Format/Default: tanyakan dulu "genuinely fixed atau configurable per scope?" — kalau ambigu, masuk 3.3c.

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
* **Markdown (.md)**: dua varian, WAJIB dibedakan (disambiguasi lengkap: 23.7):
  1. Input terstruktur murni (business rule/question bank manusia) — BUKAN sumber visual, di-parse ke Business Rules/Field Matrix/What_If_Critical_Challenge, tidak menghasilkan sheet Desain UI.
  2. **Hasil konversi dari sumber visual asli** (Excel/PDF/Word/Image/Figma export, dikonversi di luar sistem sebelum upload) — PERLAKUKAN SEBAGAI PENGGANTI sumber visual untuk keperluan redraw (lihat 23.7 untuk Snapshot & disambiguasi).
* **Teks chat murni (tanpa file apapun)**: TIDAK ADA bukti visual sama sekali. Sheet `_Snapshot` TETAP WAJIB dibuat, tapi isinya bukan gambar — melainkan REPRODUKSI TEKS ASLI requirement user (bukan parafrase/ringkasan bebas) ditempatkan rapi di cell, plus label eksplisit "TIDAK ADA file/gambar visual diupload untuk Desain UI ini — sheet ini berisi requirement asli sebagai bukti tekstual". Ini BEDA dari sekadar menulis 1 kalimat catatan generik "tidak ada evidence" — requirement asli harus benar-benar direproduksi supaya reviewer bisa membandingkan langsung ke sheet Redrawn tanpa perlu scroll ke chat asal.

## 3.5 Aturan teknis cell-drawing (WAJIB — dipakai di SETIAP sheet `[KODE]_[Screen]_Redrawn`)
Berlaku untuk sheet Redrawn yang WAJIB selalu dibuat (lihat 3.4). Ini SEMUA wajib dieksekusi sebagai kode (openpyxl), bukan sekadar disebut:
* **Lebar kolom seragam 2,57** (`column_dimensions[col].width = 2.57`) di SELURUH kolom yang menjadi area desain UI — konsisten dari kiri ke kanan, tidak ada kolom lebih lebar/sempit di tengah area.
* **TIDAK ADA merge cell** di area desain sama sekali — bentuk elemen lebar dibuat dari beberapa cell sempit berdampingan, bukan 1 cell yang di-merge.
* **TIDAK ADA wrap text**; semua teks **rata kiri** (`horizontal='left'`), termasuk label yang biasanya rata tengah di UI asli — konsistensi grid lebih penting daripada meniru alignment visual persis.
* **Button multi-cell**: beberapa cell berdampingan yang membentuk 1 tombol WAJIB punya **1 border luar saja** (outer border di 4 sisi rentang), dan **cell internal di antaranya TIDAK punya border vertikal** — supaya terlihat sebagai 1 tombol utuh, bukan beberapa kotak terpisah. Algoritma implementasi WAJIB (lihat 3.5a) — root cause kegagalan versi sebelumnya adalah border digambar dengan beberapa assignment berurutan yang saling menimpa di cell yang sama, menghilangkan sisi atas kotak.
* **Sizing elemen berbasis panjang teks aktual** (lihat 3.5b) — WAJIB dihitung dari formula, bukan ditebak/nilai tetap sembarangan. Berlaku ke SEMUA elemen bertext: button, label, header kolom, dropdown — bukan cuma tombol.
* **Header grid berjenjang & grid hierarkis** (lihat 3.5c/3.5d) — pola khusus untuk header 2-baris (grouping/dual-purpose) dan grid tree expand-collapse, tanpa merge.
* **Tab aktif vs nonaktif** harus bisa dibedakan visual (mis. aktif = fill lebih gelap/bold/tanpa border bawah menyatu dengan konten; nonaktif = fill lebih terang/normal).
* **Input disabled** = fill abu-abu (mis. D9D9D9).
* **Row selected** (baris grid yang sedang dipilih user) = fill kuning. **PENTING — beda konteks dari kuning "assumption" di sheet spec** (17.3/17.4): kuning di sheet Desain UI berarti "baris terpilih/selection state" pada mockup, BUKAN penanda assumption. Jangan disamakan maknanya.
* **Error state** = fill merah muda (sama seperti convention critical/error di 17.3).
* **Loading state dan empty state** WAJIB direpresentasikan sebagai bagian dari desain (mis. baris tambahan/varian kecil yang menunjukkan skeleton/spinner placeholder dan tampilan "data kosong"), bukan cuma default state terisi data.
* **Dropdown utama** (dropdown yang jadi filter/pilihan penting, bukan dekorasi) WAJIB diberi **Data Validation** Excel asli (`openpyxl.worksheet.datavalidation.DataValidation`, type="list") supaya benar-benar berfungsi sebagai dropdown saat file dibuka, bukan cuma gambar visual dropdown.

## 3.5a Algoritma Border Box (WAJIB — root cause kegagalan produksi, jangan reimplementasi bebas)
Ditemukan bug nyata: implementasi border yang menggambar sisi atas dan sisi bawah lewat 2 loop/assignment TERPISAH pada rentang 1 baris (r1==r2) saling menimpa di cell yang sama — assignment kedua menghapus assignment pertama, sehingga sisi atas kotak hilang dan tombol terlihat "bocor"/tidak utuh. Algoritma WAJIB (per cell, SATU assignment yang menggabungkan semua sisi relevan sekaligus):
```
def box(ws, r1, c1, r2, c2, fill=None):
    for rr in range(r1, r2+1):
        for cc in range(c1, c2+1):
            top = THIN if rr == r1 else None
            bottom = THIN if rr == r2 else None
            left = THIN if cc == c1 else None
            right = THIN if cc == c2 else None
            cl = ws.cell(row=rr, column=cc)
            if fill: cl.fill = fill
            if top or bottom or left or right:
                cl.border = Border(top=top, bottom=bottom, left=left, right=right)
```
Untuk menambah 1 garis internal TANPA menghapus border box yang sudah ada di cell itu (dipakai di 3.5c untuk divider antar sub-kolom header), WAJIB baca border existing dulu lalu gabungkan, bukan replace total:
```
def add_divider(ws, r, c, side="right"):
    b = ws.cell(row=r, column=c).border
    kwargs = dict(top=b.top, bottom=b.bottom, left=b.left, right=b.right)
    kwargs[side] = THIN
    ws.cell(row=r, column=c).border = Border(**kwargs)
```

## 3.5b Formula Sizing Berbasis Teks (WAJIB, terkalibrasi dari pengujian visual nyata)
Setiap elemen bertext (button, label, dropdown, header) WAJIB dihitung lebarnya (dalam jumlah cell) dari panjang teks aktual — bukan angka tetap yang ditebak. Formula terkalibrasi (hasil 3 iterasi pengujian visual langsung di Excel, jangan diubah tanpa pengujian ulang serupa):
```
CHAR_PER_CELL = 2.6   # jumlah karakter yang muat per 1 cell lebar 2,57
PAD = 1                # padding tambahan (dalam jumlah cell)

def text_width_cells(text, minimum=3):
    import math
    needed = math.ceil(len(text) / CHAR_PER_CELL) + PAD
    return max(minimum, needed)
```
* Teks WAJIB rata kiri (`horizontal='left'`), TIDAK PERNAH center — pelanggaran ini root cause bug kedua yang ditemukan: teks center di box yang pas-pasan menyebabkan efek visual "meluber"/terpotong di Excel. Tambahkan 1 spasi di depan teks sebagai indent visual dari border kiri (mis. `" " + text`).
* Gap antar elemen berdampingan (mis. antar tombol) = 2 cell kosong (tanpa border) di antaranya.
* Formula ini berlaku SAMA untuk header kolom grid, bukan cuma tombol — kegagalan versi sebelumnya adalah header di-hardcode lebar sembarangan (mis. semua header disamakan 8-15 cell tanpa hitung), menyebabkan label panjang seperti "No. Surat Kirim / Material" terpotong jadi "No" karena cell tetangga terisi/border sehingga Excel meng-clip overflow teks.

## 3.5c Header Grid Berjenjang (2 baris, tanpa merge)
Tiga pola header yang WAJIB didukung — SEMUA memakai algoritma `box()` yang SAMA (3.5a): gambar **1 box besar** dulu (mencakup seluruh rentang baris×kolom yang relevan), baru tambahkan divider internal (`add_divider`) HANYA di tempat yang perlu. Jangan pernah menggambar sub-elemen sebagai box terpisah lalu digabung — itu menyebabkan celah/gap tidak presisi antar sub-elemen.
* **Vertical spanning** (1 label menaungi tinggi 2 baris, mis. "No. Surat Kirim", "Status" yang tidak punya sub-kolom): `box(ws, header_row1, c, header_row2, c+width-1, fill=DARKHEADER)` — SATU box mencakup 2 baris, label ditulis di row1 saja, row2 dibiarkan kosong (fill sama, tanpa garis pemisah horizontal karena memang tidak ada assignment terpisah untuk row2).
* **Dual-row** (kolom sama, label BEDA di row1 vs row2 — mis. "NIK" di atas / "Tgl. Transaksi" di bawah, dipakai saat 1 kolom punya makna berbeda tergantung tipe baris data): SAMA seperti vertical spanning (1 box, 2 baris), bedanya row2 DIISI teks berbeda, bukan dikosongkan.
* **Grouped** (1 label parent menaungi beberapa sub-kolom, mis. "Total" menaungi "Qty"+"Uom"): gambar SATU box besar mencakup row1+row2 dan seluruh lebar gabungan sub-kolom sekaligus (`box(ws, header_row1, c, header_row2, c+total_width-1, fill=DARKHEADER)`), tulis label parent di row1 kolom pertama, tulis tiap sub-label di row2 pada posisi kolomnya masing-masing, LALU tambahkan `add_divider(ws, header_row2, <kolom_akhir_subkolom>, side="right")` HANYA di baris row2 sebagai pemisah antar sub-kolom — TIDAK ADA garis horizontal antara row1 (parent) dan row2 (sub-kolom), karena keduanya bagian dari 1 box yang sama.

## 3.5d Grid Hierarkis (tree expand/collapse, indent tanpa merge)
Untuk grid dengan baris grup (bisa di-expand/collapse) dan baris detail di bawahnya:
* Sediakan kolom toggle di paling kiri, lebar tetap (mis. 3 cell: 1 untuk checkbox `[ ]`, 1-2 untuk glyph segitiga `▼`/`▶`). Cell header di atas kolom toggle ini DIBIARKAN KOSONG (tanpa fill gelap) — bukan diberi fill seperti header lainnya.
* Baris grup: isi cell toggle dengan `[ ]` + glyph `▼` (expanded) atau `▶` (collapsed), fill baris sedikit berbeda (mis. abu muda) untuk membedakan dari baris detail.
* Baris detail: kolom toggle DIBIARKAN KOSONG (tetap ada box border kosong, sejajar posisi dengan toggle di atasnya) sebagai bentuk indentasi visual — BUKAN mengurangi lebar kolom atau menggeser konten, cukup cell toggle-nya kosong.
* Lebar kolom data (setelah kolom toggle) tetap dihitung dari formula 3.5b berdasarkan header terpanjang di kolom itu.
