# 19. Critical Challenge QnA (Devil's Advocate)
Sheet lintas-modul baru: `Critical_Challenge_QnA`. Perannya BUKAN pengulangan What-If (yang fokus ke *future change*) atau Business Rules (fokus ke *current behaviour*) — sheet ini berperan sebagai **reviewer paling galak yang bisa dibayangkan**: profesor senior system analyst yang tugasnya menjebol blueprint SEBELUM developer/QA yang menemukan lubangnya di production. Tujuannya supaya blueprint auto-approved oleh reviewer manapun karena semua pertanyaan sulit sudah diantisipasi duluan.

## 19.1 Prinsip persona
Tulis pertanyaan dengan nada menantang, spesifik, dan sengaja mencari celah — bukan pertanyaan generik seperti "bagaimana kalau error?". Bandingkan:
* LEMAH (jangan dipakai): "Bagaimana jika terjadi error saat submit?"
* KUAT (dipakai): "Kalau dua user beda region membuka record yang sama, satu approve dan satu reject dalam rentang 2 detik — siapa yang menang, dan apakah user yang kalah tahu keputusannya sudah usang?"

## 19.2 Kolom wajib
Challenge ID | Section/Sheet Terkait | Related ID (Rule/Component/Field) | Pertanyaan Kritis | Kenapa Ini Penting (risiko kalau tidak dijawab) | Insight/Rekomendasi Awal (bantu BA menjawab, BUKAN cuma bertanya) | Status (Open/Answered/Deferred) | Severity (Critical/High/Medium) | Related Assumption/Decision ID

## 19.3 Kolom "Insight/Rekomendasi Awal" — WAJIB diisi, bukan kosong
Setiap challenge harus disertai arah jawaban/rekomendasi awal berbasis best-practice umum (bukan tebakan acak) — supaya BA punya starting point, bukan halaman kosong. Kalau benar-benar tidak ada rekomendasi yang aman diberikan, tulis eksplisit alasannya, jangan dikosongkan.

## 19.4 Domain pertanyaan wajib dijalankan per screen/modul (jangan skip diam-diam, sama seperti 6.2/14.3)
* **Concurrency & race condition**: 2+ aktor mengubah data yang sama nyaris bersamaan — siapa menang, siapa diberi tahu, apakah ada data hilang diam-diam.
* **Ambiguitas keputusan (editable/disabled, mandatory/optional)**: setiap kolom Field Matrix yang ditandai "BELUM DIPUTUSKAN" (lihat 07.2) otomatis jadi 1 challenge di sini.
* **Boundary & edge value ekstrem**: nilai di titik batas persis, nilai kosong tapi terlihat terisi (whitespace), nilai maksimum sistem (mis. tanggal 31/12/2099), volume data sangat besar.
* **Perpindahan status yang "mustahil" tapi teknis bisa terjadi**: skip status, rollback status, status berubah oleh proses lain saat user sedang membuka form.
* **Permission edge case**: user kehilangan permission saat sedang mengerjakan form; role ganda dengan permission bertentangan; superuser override normal rule.
* **Data yang sudah dipakai transaksi lain**: field yang diedit ternyata sudah direferensikan record lain — cascade, orphan, atau block?
* **Multi-device/multi-session**: user yang sama login di 2 device, submit dari salah satu.
* **Kegagalan parsial**: bulk action separuh sukses separuh gagal — apa yang user lihat, apakah bisa retry sebagian saja.
* **Interpretasi ganda dari UI yang sama**: label/field yang bisa dibaca 2 makna berbeda oleh user berbeda — mana yang benar.
* **Reversibilitas**: setiap aksi destruktif (delete, reject, expire) — bisa di-undo atau tidak, sampai kapan.

## 19.5 Keterhubungan
Setiap Challenge yang statusnya "Answered" WAJIB menghasilkan atau memperbarui: Business Rule terkait (6.5), baris Field Matrix terkait (7.2), atau entry Assumption/Decision (18). Challenge yang masih "Open" tetap WAJIB muncul di Index_Summary sebagai bagian dari Keputusan Kritis Belum Dikonfirmasi (bukan cuma bagian dari sheet ini saja) — supaya tidak terkubur.

## 19.6 Volume wajar
Untuk screen dengan kompleksitas sedang (10-25 component), target realistis 8-15 challenge question. Untuk screen sederhana (<10 component, read-only/list saja), minimal 3-5 challenge tetap wajib ada — tidak ada screen yang "terlalu simpel untuk ditantang".
