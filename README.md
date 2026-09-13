# UI Technical Blueprint Knowledge Handbook
Tujuan dokumen: Knowledge source komprehensif untuk Copilot Agent yang mengubah screenshot, mockup, wireframe, atau Excel UI (cell-drawn) menjadi spesifikasi teknis lintas-fungsi (BA/PO, Frontend, Backend, Database, QA). Dokumen ini melengkapi instruksi operasional agent yang dibatasi 8.000 karakter.

## Metadata
* Document Owner: Corporate Development / Business Analysis
* Document Type: Agent Knowledge Standard and Technical Blueprint Handbook
* Recommended Agent Instruction: Gunakan instruksi operasional ringkas maksimal 8.000 karakter
* Knowledge Usage: Upload dokumen ini sebagai knowledge source agent
* Default Deliverable: Excel .xlsx — `Index_Summary` + `Desain UI` (Snap+Redr) + satu sheet spec per Desain UI (Screen-State Inventory, Business Intent/Invariants, Business Rules, Functional UI Spec & Field Matrix dengan row-explosion Mode×Status, Message Catalog) + sheet lintas-modul (`Overview_Scope`, `Actor_Role_Permission`, `Data_API`, `What_If_Critical_Challenge`, `Test_Scenario`, `Assumption_Decision_Risk_Open`)
* Detail Level: BA/PO, Frontend, Backend, Database, QA (Security/NFR/Concurrency/Integration/Traceability TIDAK termasuk — lihat 02)
* Status: v2.8 — standar kelengkapan tertinggi + Self-Audit Pass + auto-apply + Excel safety guardrails

## Navigasi Handbook
* [01. Purpose and Principles](handbook/01-purpose-and-principles.md)
* [02. Source Precedence & Knowledge Base](handbook/02-source-precedence.md)
* [03. Input Analysis](handbook/03-input-analysis.md)
* [04. Module Screen State](handbook/04-module-screen-state.md)
* [05. Business Invariants](handbook/05-business-invariants.md)
* [06. Business Rules](handbook/06-business-rules.md)
* [07. Functional UI Spec & Field Matrix (Unified, Row-Explosion, Related ID)](handbook/07-functional-ui-spec.md)
* [09. Message Catalog](handbook/09-message-catalog.md)
* [10. Data Model & API](handbook/10-data-api.md)
* [14. What-If & Critical Challenge QnA (gabungan)](handbook/14-what-if-framework.md)
* [15. What-If Library](handbook/15-what-if-library.md)
* [16. Testing](handbook/16-testing.md)
* [17. Workbook Architecture](handbook/17-workbook-architecture.md)
* [18. Quality Gate](handbook/18-quality-gate.md)
* [20. Self-Audit Pass](handbook/20-self-audit-pass.md)
* [21. Mode Desain (Enterprise vs Simple)](handbook/21-design-modes.md)
* [22. Excel Generation Safety Guardrails](handbook/22-excel-safety-guardrails.md)

## Navigasi Templates
* [Business Rule Template](templates/business-rule-template.md)
* [Functional UI Spec & Field Matrix Template](templates/functional-field-matrix-template.md)
* [Message Catalog Template](templates/message-catalog-template.md)
* [What-If & Critical Challenge Template](templates/what-if-template.md)
* [Test Case Template](templates/test-case-template.md)
