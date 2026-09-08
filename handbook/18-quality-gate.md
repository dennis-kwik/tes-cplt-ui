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
* Desain UI: Tidak ada merge cell; lebar kolom seragam (~2,6 cm); reproduksi sesuai 3.4.
* Workbook: `Index_Summary` lengkap dengan hyperlink, Keputusan Kritis Belum Dikonfirmasi, dan Glosarium; file valid dibuka di Excel.
