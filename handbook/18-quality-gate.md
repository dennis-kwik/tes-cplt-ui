# 18. Assumption, Decision, Risk, dan Open Question Governance
Dicatat pada sheet `Assumption_Decision_Risk_Open`:
* Assumption: ID; topic; proposed decision; reason; impact; confirm by; status; related IDs.
* Decision: ID; decision; options; rationale; owner; date; status.
* Risk: ID; event/cause/impact; likelihood; severity; mitigation; owner; status.
* Open Question: ID; question; why needed; impact if unresolved; owner; status.

Governance rule: Confirmed requirement tidak boleh diubah diam-diam — perubahan menghasilkan entry Decision baru dengan impact analysis ke rule/component/field/message/data terkait.

# 18b. Quality Gate dan Review Checklist
* Evidence: Semua input/sheet dan icon kecil diperiksa; observed vs inferred jelas.
* Coverage: Setiap Desain UI (per sheet input maupun per section dalam 1 sheet) terdeteksi dan punya sheet spec sendiri.
* Functional: Semua state/action/exception ditentukan; Field Matrix dan Message Catalog lengkap.
* Data: Key, constraint, relation, history dianalisis pada `Data_API`.
* Future: Business invariant dan `What_If` tersedia untuk skenario relevan.
* QA: Critical rule dan what-if kritikal memiliki test pada `Test_Scenario`.
* Governance: Assumption, Decision, Risk, Open Question memiliki ID/owner/status.
* Devil's Advocate: `What_If_Critical_Challenge` (Section B) terisi sesuai domain wajib (14.4f), setiap entry punya Insight/Rekomendasi (bukan kosong), Jenis Jawaban terklasifikasi (14.4b), entry "Auto-Applied" sudah menghasilkan Business Rule/Field Matrix/Test terkait (14.4c).
* Row-explosion: Field Matrix & Business Rules sudah dipecah per Mode×Status di mana constraint berbeda (07.1, 6.3) — bukan digabung jadi prosa umum; Component ID ikut kosakata baku (07.3b).
* Ambiguity: setiap frasa requirement dengan >1 tafsiran sudah dicatat di Assumption_Decision_Risk_Open + What_If_Critical_Challenge (3.3b), dan tafsiran default dipakai KONSISTEN di semua sheet.
* Test coverage: jumlah Test Scenario >= formula minimum (16.3).
* Self-Audit Pass: sudah dijalankan (20) — tidak ada kontradiksi lintas-sheet untuk topik ambigu yang sama, Component ID konsisten, angka Index_Summary cocok dengan isi aktual.
* Desain UI: Setiap Desain UI punya sepasang sheet Snapshot (gambar bukti asli) + Redrawn (digambar ulang agent sesuai 3.5) — WAJIB dua-duanya, bukan hasil ketik ulang manual. Lihat 3.4.
* Format: Assumption fill kuning benar-benar diterapkan (bukan cuma teks); autofilter aktif di semua tabel; freeze pane aktif. Lihat 17.4 Gate format.
* Cell-drawing (jika dipakai): lebar kolom seragam 2,57; tidak ada merge cell; tidak ada wrap text; button multi-cell 1 border luar tanpa border internal; tab aktif/nonaktif beda visual; disabled/selected/error state pakai fill sesuai 3.5; loading & empty state ada; dropdown utama pakai Data Validation asli.
* Workbook: `Index_Summary` lengkap dengan hyperlink, Keputusan Kritis Belum Dikonfirmasi, dan Glosarium; file valid dibuka di Excel.
* Mode Desain: mode (Enterprise/Configurable atau Simple, lihat 21) sudah dikonfirmasi eksplisit oleh user sebelum generate, kedalaman section disesuaikan mode yang dipilih.
* Excel Safety: File Integrity Check (22.5) sudah dijalankan — file berhasil dibuka ulang tanpa error sebelum diserahkan ke user.
