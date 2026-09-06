# 11. Security, Privacy, Audit, dan Operability
* Authorization: Siapa dapat View/Create/Edit/Delete/Approve? Apakah scope dibatasi principal/company?
* Input security: Apakah server melakukan type, length, enum, ownership, dan injection validation?
* Output security: Apakah output encoded dan sensitive field masked?
* Privacy: Klasifikasi data, purpose, minimization, retention, deletion, access review?
* Audit: Aksi apa dicatat; actor; UTC; old/new; reason; result; correlation ID?
* Logging: Apa yang aman dicatat; bagaimana PII/token disensor; siapa dapat mengakses log?
* Operational: Monitoring, alert, retry, reconciliation, runbook, support message?

Security invariant: UI hide/disable tidak pernah menjadi kontrol keamanan utama. Backend wajib melakukan authorization dan ownership/scope validation.