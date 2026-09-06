# 2. Arsitektur Agent: Instructions vs Knowledge
Copilot Agent Builder memiliki ruang instructions yang terbatas. Gunakan instructions untuk perilaku operasional dan knowledge ini untuk standar mendalam, contoh, taksonomi, serta reusable reference.

## Lapisan dan Isi
* Instructions <= 8.000 karakter: Role; dua prinsip utama; urutan proses; struktur workbook; mandatory sections; quality gate. Jangan dimasukkan: Contoh panjang, scenario library lengkap, semua template kolom.
* Knowledge document: Metodologi; what-if library; standard validation; templates; examples; governance. Jangan dimasukkan: Instruksi yang bertentangan dengan operational prompt.
* User input: Mockup; requirement; confirmed rules; konteks proyek. Jangan dimasukkan: Keputusan tersembunyi tanpa source/status.
* Output workbook: Evidence dan spec per modul. Jangan dimasukkan: Penjelasan generik yang tidak terhubung ID.

## Precedence
Urutan prioritas: instruksi eksplisit user/project -> confirmed business rule -> existing behaviour yang tervalidasi -> visual evidence -> proposed best practice sebagai asumsi.