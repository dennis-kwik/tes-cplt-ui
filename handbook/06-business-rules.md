# 6. Business Rules dan Conditional Logic

## 6.1 Struktur rule
* Rule ID: BR-[MODULE]-[NNN]
* Name: Nama singkat yang stabil
* Source/Status: Confirmed, Observed, Inferred, Proposed, Assumption
* IF / Trigger: Kondisi pemicu
* AND / Preconditions: Kondisi tambahan, permission, state
* THEN / Result: Perubahan state/data/navigation — WAJIB nilai final (bukan "sesuai kebutuhan")
* ELSE / Exception: Fallback, error, partial failure
* Priority: Critical, High, Medium, Low
* Related IDs: Component, Message, Data, Risk, Test — DAN sebaliknya: Field Matrix yang terdampak rule ini wajib mencantumkan Rule ID ini di kolom Validation/Behaviour.

## 6.2 Rule domains — CHECKLIST WAJIB PER SCREEN, JANGAN SKIP DIAM-DIAM
Untuk SETIAP screen/mode, jalankan keenam domain berikut satu per satu. Kalau satu domain memang tidak relevan, tulis 1 baris rule dengan THEN "Not Applicable" dan ELE/alasan singkat — JANGAN dihilangkan tanpa jejak. Reviewer harus bisa melihat domain mana yang sudah dicek vs terlewat.
* **Lifecycle**: Add, Edit, View, Submit, Approve, Reject, Activate, Expire, Delete, Restore — untuk setiap transisi status, jelaskan siapa boleh, syarat apa, dan efek ke field lain.
* **Data integrity**: mandatory, uniqueness, overlap, dependency, status transition, boundary value (persis di batas min/max), null/blank/whitespace-only, format invalid.
* **Interaction**: search, filter, sort, page, bulk action, selection (select all/partial/none), dirty state (navigasi dengan unsaved changes), double-submit.
* **Security-adjacent (dalam batas fungsional, BUKAN full audit/encryption spec)**: role/permission yang mengubah tampilan atau aksi yang boleh dilakukan pada layar ini.
* **Resilience-adjacent (dalam batas fungsional, BUKAN full NFR)**: apa yang user lihat kalau submit gagal di tengah jalan, apa yang terjadi kalau data sudah berubah oleh proses lain saat user masih membuka form (stale data), retry manual oleh user.
* **Future**: channel expansion, hierarchy, workflow, versioning, migration — cukup 1-2 rule kalau relevan, detail lengkap ada di What-If.

## 6.3 Kelengkapan per Mode × Status
Rule yang hasilnya berbeda tergantung Mode (Add/Edit/View) dan/atau Status record (Draft/Submitted/Approved/Confirmed/Rejected/dst) WAJIB ditulis sebagai rule terpisah per kombinasi — bukan 1 rule umum dengan kata "tergantung kondisi". Pola ini WAJIB konsisten 1:1 dengan row-explosion di Field Matrix (lihat 07.1-07.3) — Rule ID dan Component ID granular yang sama harus saling mereferensikan lewat Related IDs, supaya reviewer bisa lompat dari 1 baris Field Matrix ke rule yang menjelaskannya dan sebaliknya, tanpa harus menebak.

## 6.5 Kelengkapan menyeluruh, bukan hanya rule yang "kelihatan"
Business Rules bukan cuma dokumentasi rule yang sudah jelas dari gambar — level standar tertinggi berarti rule domain di 6.2 dijalankan SAMPAI HABIS untuk tiap screen, termasuk rule yang baru muncul kalau BA ditanya skenario ekstrem (lihat 19 — Critical Challenge). Setiap entry `Critical_Challenge_QnA` yang jawabannya berupa keputusan bisnis WAJIB menghasilkan 1 Business Rule baru (berstatus Assumption/Proposed sampai dikonfirmasi), bukan berhenti sebagai pertanyaan tak berjawab.

## 6.4 Contoh
BR-DSCAM-008: IF kombinasi business scope, assignment, channel, dan effective period menghasilkan lebih dari satu record efektif; AND status draft; THEN Save ditolak, conflicting record ditampilkan; ELSE UNLESS exception type yang dikonfigurasi mengizinkan overlap; Priority: Critical; related: FM-PERIOD-001, VAL-OVL-001, DATA-EFFECTIVITY-001, TC-OVL-001.

BR-DSCAM-009: IF mode=Edit AND status=Approved; THEN field Start/End Date disabled kecuali user role=Admin; ELSE IF status=Draft THEN field tetap editable mengikuti aturan mode Add; Priority: High; related: CMP-START-EDIT-APPROVED, CMP-END-EDIT-APPROVED.
