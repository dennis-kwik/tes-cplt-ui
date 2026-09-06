# 18. Assumption, Decision, Risk, dan Open Question Governance
* Assumption: ID; topic; proposed decision; reason; impact; confirm by; due/status; related IDs.
* Decision: ID; decision; options; rationale; owner; date; status; supersedes; impact.
* Risk: ID; event/cause/impact; likelihood; severity; mitigation; owner; trigger; status.
* Open Question: ID; question; why needed; impact if unresolved; owner; status; due.
* Change Log: Version; date; author; reason; impacted IDs; approval.
Governance rule: Confirmed requirement tidak boleh diubah diam-diam. Perubahan harus menghasilkan Decision/Change entry dan impact analysis terhadap rule, component, message, data, integration, security, migration, serta test.

# 19. Quality Gate dan Review Checklist
* Evidence: Semua input/sheet dan icon kecil diperiksa; observed vs inferred jelas.
* Functional: Semua state/action/exception telah ditentukan.
* Data: Key, constraint, relation, history, retention, migration dianalisis.
* Security: Backend authorization, validation, encoding, audit, privacy tercakup.
* Resilience: Transaction, concurrency, idempotency, timeout, retry, recovery tercakup.
* Future: Business invariant dan What-If Matrix tersedia.
* QA: Critical rule dan what-if memiliki test dan traceability.
* Governance: Assumption, Decision, Risk, Open Question memiliki ID/owner/status.
* Workbook: Satu modul satu consolidated sheet; readable; filter/freeze/hyperlink.
* Delivery: File Excel valid dan ringkasan jumlah artefak diberikan.