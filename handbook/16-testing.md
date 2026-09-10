# 16. Testing Strategy
Sheet gabungan lintas-modul: `Test_Scenario`.

## 16.1 Test taxonomy
* Positive dan alternate flow.
* Negative dan validation.
* Boundary dan equivalence partition.
* Authorization dan segregation of duties (bila role dibedakan pada UI).
* Future-change test untuk setiap what-if kritikal.

## 16.2 Keterhubungan minimal (pengganti Traceability penuh)
Setiap baris Test Scenario wajib mencantumkan kolom Rule/WF ID dan Component ID agar tetap tertelusur ke sheet Desain UI/modul asal tanpa perlu sheet Traceability terpisah.
* Critical Business Rule: minimal 1 test positive + 1 test negative/boundary.
* What-If Kritikal: minimal 1 impact test.
* Assumption berdampak tinggi: test placeholder + status "menunggu konfirmasi".
