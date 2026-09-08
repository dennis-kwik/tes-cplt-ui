# 9. Message Catalog Standard

## Prefix dan Penggunaan
* VAL: Validation; Input atau rule invalid.
* CNF: Confirmation; Aksi destructive atau discard.
* SUC: Success; Proses selesai.
* WRN: Warning; Boleh dilanjutkan dengan risiko.
* ERR: Error; Kegagalan system/integration/concurrency.
* INF: Information; Status atau empty state.

## 9.1 Message quality
* Sebutkan masalah secara spesifik tanpa jargon teknis.
* Berikan next action yang dapat dilakukan user.
* Jangan bocorkan stack trace, SQL, internal ID sensitif, atau authorization detail.
* Tempatkan inline untuk field error; modal untuk decision; toast untuk transient result.
* Hubungkan message ke component, rule, logging requirement, dan test.