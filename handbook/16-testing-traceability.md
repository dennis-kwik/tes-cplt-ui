# 16. Testing Strategy dan Traceability

## 16.1 Test taxonomy
* Positive dan alternate flow.
* Negative dan validation.
* Boundary dan equivalence partition.
* Authorization dan segregation of duties.
* Security input/output/access tests.
* Concurrency, duplicate submit, idempotency.
* Integration timeout/retry/duplicate/out-of-order.
* Migration, backward compatibility, contract regression.
* Performance, capacity, recovery, DR.
* Future-change test untuk setiap critical what-if.

## 16.2 Traceability chain
* Contoh: BR-DSCAM-008 -> FM-PERIOD-END-001 -> VAL-OVL-001 -> API.endDate / DB.effective_end -> RISK-OVL-001 -> DEC-EFFECTIVITY-001 -> TC-OVL-001 dan WF-TEMPORAL-001.
* Critical Business Rule: Minimal 1 positive + 1 negative/boundary test.
* Security Rule: Authorization/security test.
* Integration Rule: Success + timeout/retry/duplicate test.
* What-If Critical: Impact test atau contract/migration test.
* Assumption High Impact: Test placeholder dan explicit confirmation gate.