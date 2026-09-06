# 7. Functional UI Specification Standard
Functional table utama mempertahankan tiga kolom agar cepat dibaca, sedangkan detail granular ditempatkan pada section Field Matrix pada sheet modul yang sama.

* Initial*: Text box; Mandatory; 1-10 karakter ASUMSI; uppercase; trim; unique case-insensitive; Add enabled; Edit read-only; Message VAL-INI-004.
* Periode End*: Datepicker; Mandatory; DD/MM/YYYY; >= Start; overlap check; focus on invalid; Message VAL-DATE-004.
* Save: Button; Permission Create/Edit; validate client+server; disable while processing; atomic save; stay in form; success SUC-SAVE-001.

## 7.1 Action completeness checklist
* Purpose dan permission.
* Visible/enabled/disabled condition.
* Trigger dan precondition.
* Client dan server validation.
* Loading dan double-click behaviour.
* Success, failure, navigation, focus, dan message.
* Audit dan related API operation.