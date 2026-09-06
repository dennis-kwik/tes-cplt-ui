# 6. Business Rules dan Conditional Logic

## 6.1 Struktur rule
* Rule ID: BR-[MODULE]-[NNN]
* Name: Nama singkat yang stabil
* Source/Status: Confirmed, Observed, Inferred, Proposed, Assumption
* IF / Trigger: Kondisi pemicu
* AND / Preconditions: Kondisi tambahan, permission, state
* THEN / Result: Perubahan state/data/navigation
* ELSE / Exception: Fallback, error, partial failure
* Priority: Critical, High, Medium, Low
* Related IDs: Component, Message, Data, Risk, Test

## 6.2 Rule domains
* Lifecycle: Add, Edit, View, Submit, Approve, Reject, Activate, Expire, Delete, Restore.
* Data integrity: mandatory, uniqueness, overlap, dependency, status transition.
* Interaction: search, filter, sort, page, bulk action, selection, dirty state.
* Security: role, segregation of duties, authorized scope.
* Resilience: timeout, retry, duplicate request, partial failure, stale version.
* Future: channel expansion, hierarchy, workflow, versioning, migration.

## 6.3 Rule example
BR-DSCAM-008: IF kombinasi business scope, assignment, channel, dan effective period menghasilkan lebih dari satu record efektif; THEN Save ditolak; AND conflicting record ditampilkan; UNLESS exception type yang dikonfigurasi mengizinkan overlap; related: FM-PERIOD-001, VAL-OVL-001, DATA-EFFECTIVITY-001, TC-OVL-001.