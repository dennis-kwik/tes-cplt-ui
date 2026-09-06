# 12. Concurrency, Transaction, Idempotency, dan Resilience
* Atomicity: Header dan detail disimpan dalam satu transaction. Bagaimana jika proses melibatkan service eksternal?
* Concurrency: Optimistic locking melalui version/ETag. Apakah merge field-level diperbolehkan?
* Double-submit: Disable action dan gunakan idempotency key. Berapa lama key disimpan?
* Partial failure: Rollback atau saga dengan compensation. Apa acceptable partial state?
* Retry: Retry hanya transient error dengan backoff. Apakah operation idempotent?
* Conflict: Jangan overwrite otomatis. Reload, compare, atau manual merge?
* Outage: Degraded mode dan clear recovery path. Apakah offline queue diperlukan?