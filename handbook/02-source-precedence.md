# 2. Arsitektur Agent: Instructions vs Knowledge
Copilot Agent Builder memiliki ruang instructions yang terbatas. Gunakan instructions untuk perilaku operasional dan knowledge ini untuk standar mendalam, contoh, taksonomi, serta reusable reference.

## Knowledge Base Sources (urutan prioritas)
1. Requirement eksplisit user/proyek (chat, dokumen requirement).
2. House Standard — repo ini: https://github.com/dennis-kwik/tes-cplt-ui
3. Current UI (image/Excel) sebagai evidence, bukan otomatis future rule.
4. Referensi desain UI/komponen — Chameleon Angular Framework demo: https://demo.silkroad-app.com/chameleon-angular-framework (dipakai saat input berupa gambar dan sheet "Desain UI" perlu digambar ulang; sebagai acuan jenis komponen, layout, dan penamaan visual yang wajar).
5. ISTQB Body of Knowledge: https://tbok.istqb.org (dipakai khusus untuk menyusun Test Scenario/taxonomy pengujian).

## Catatan perubahan Knowledge Base
Azure Architecture Center dan OWASP ASVS **dihapus** dari knowledge base karena section yang menjadi konsumennya (NFR, Security/Privacy/Audit, Concurrency/Transaction/Idempotency, Integration/Dependency) sudah tidak menjadi bagian dari deliverable standar. Digantikan oleh Chameleon UI reference (poin 4) untuk kebutuhan reproduksi/desain ulang UI.

## Lapisan dan Isi
* Instructions <= 8.000 karakter: Role; prinsip utama; urutan proses; struktur workbook; mandatory section; quality gate.
* Knowledge document (repo ini): Metodologi, what-if library, template kolom, examples, governance.
* User input: Mockup/Excel UI, requirement, confirmed rules, konteks proyek.
* Output workbook: Evidence dan spec per Desain UI/modul.

## Precedence
instruksi eksplisit user/project -> confirmed business rule -> existing behaviour yang tervalidasi -> visual evidence -> proposed best practice sebagai asumsi.
