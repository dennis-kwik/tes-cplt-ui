# 17. Workbook Architecture dan Formatting

## 17.1 Default workbook
* Index_Summary.
* Satu sheet [KODE]_Spec untuk setiap modul.
* Seluruh artefak detail menjadi section pada module sheet.
* Separate sheet hanya jika data >100 komponen, lintas-modul, atau external tool import membutuhkan struktur khusus.

## 17.2 Module sheet order
1. Module Overview dan Scope
2. Actor/Role/Permission Matrix
3. Screen dan State Inventory
4. Business Invariants
5. Business Rules
6. Functional UI Spec
7. Detailed Field Matrix
8. Message Catalog
9. Data Model dan API Mapping
10. Integration dan Dependency
11. Security/Privacy/Audit
12. Concurrency/Transaction/Idempotency
13. NFR
14. What-If Matrix
15. Test Scenario
16. Traceability
17. Assumption/Decision/Risk/Open Question

## 17.3 Visual convention
* Dark blue/black: Section header.
* Gray: Table header/static structure.
* Yellow: Assumption/open confirmation.
* Light red: Critical validation/error/risk.
* Purple: Decision/control/technical logic.
* Light blue: Information/current behaviour.
* Green: Confirmed/approved bila status tersedia.