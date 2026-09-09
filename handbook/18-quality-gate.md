# 18. Assumption, Decision, Risk, dan Open Question Governance
Dicatat pada sheet `Assumption_Decision_Risk_Open`:
* Assumption: ID; topic; proposed decision; reason; impact; confirm by; status; related IDs.
* Decision: ID; decision; options; rationale; owner; date; status.
* Risk: ID; event/cause/impact; likelihood; severity; mitigation; owner; status.
* Open Question: ID; question; why needed; impact if unresolved; owner; status.

Governance rule: Confirmed requirement tidak boleh diubah diam-diam — perubahan menghasilkan entry Decision baru dengan impact analysis ke rule/component/field/message/data terkait.

# 19. Quality Gate dan Review Checklist
* Evidence: Semua input/sheet dan icon kecil diperiksa; observed vs inferred jelas.
* Coverage: Setiap Desain UI (per sheet input maupun per section dalam 1 sheet) terdeteksi dan punya sheet spec sendiri.
* Functional: Semua state/action/exception ditentukan; Field Matrix dan Message Catalog lengkap.
* Data: Key, constraint, relation, history dianalisis pada `Data_API`.
* Future: Business invariant dan `What_If` tersedia untuk skenario relevan.
* QA: Critical rule dan what-if kritikal memiliki test pada `Test_Scenario`.
* Governance: Assumption, Decision, Risk, Open Question memiliki ID/owner/status.
* Devil's Advocate: `Critical_Challenge_QnA` terisi sesuai domain wajib (19.4), setiap entry punya Insight/Rekomendasi (bukan kosong), entry "Answered" sudah menghasilkan Business Rule/Field Matrix/Decision terkait.
* Row-explosion: Field Matrix & Business Rules sudah dipecah per Mode×Status di mana constraint berbeda (07.1, 6.3) — bukan digabung jadi prosa umum.
* Desain UI: Berisi objek asli (embedded image untuk input gambar; copied sheet terprogram untuk input Excel) — bukan hasil ketik ulang/gambar ulang manual. Lihat 3.4.
* Format: Assumption fill kuning benar-benar diterapkan (bukan cuma teks); autofilter aktif di semua tabel; freeze pane aktif. Lihat 17.4 Gate format.
* Workbook: `Index_Summary` lengkap dengan hyperlink, Keputusan Kritis Belum Dikonfirmasi, dan Glosarium; file valid dibuka di Excel.
