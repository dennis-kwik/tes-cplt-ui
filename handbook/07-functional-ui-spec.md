# 7. Functional UI Spec & Field Matrix (Unified, Mode×Status Explosion)
Satu tabel per Desain UI, tapi TIDAK LAGI 1 baris = 1 component secara mutlak. Aturan sekarang: **1 baris = 1 component PADA 1 konteks (Mode × Status) yang constraint/behaviour-nya sudah final untuk konteks itu.** Kalau sebuah component berperilaku sama di semua Mode/Status, cukup 1 baris (Mode/Status diisi "All"). Kalau berbeda, WAJIB dipecah — dilarang menulis 1 baris dengan deskripsi prosa yang menggabungkan banyak kondisi ("tergantung mode", "sesuai kebutuhan").

## Kolom wajib (urutan tetap)
Component ID | Screen | Section | Elemen/Field | Jenis Komponen | **Mode** | **Status Context** | M/O/C/System | Data Type | Min/Max | Format/Allowed Value | Default | Editable/Disabled/Hidden | Behaviour/Event | Validation (client & server) | Permission | Message ID | Data Attribute | Rule ID Terkait | Source/Status

## 7.1 Kapan WAJIB row-explosion (berlaku SEMUA jenis komponen, bukan cuma field input)
Pecah jadi baris terpisah bila salah satu berubah lintas konteks:
* Mode (Add/Edit/View/Duplicate/dst).
* Status record (Draft/Submitted/Approved/Rejected/Confirmed/Expired/dst).
* Kombinasi keduanya (Mode×Status) — paling sering terjadi pada Edit×Status tertentu.
* Permission/role yang mengubah enable-disable atau visibility.
Berlaku untuk button, checkbox, dropdown, grid action icon, tab, popup trigger — bukan hanya datepicker/textbox.

## 7.2 Kolom "Editable/Disabled/Hidden" — WAJIB nilai final, tandai kalau belum diputuskan
Tulis kondisi final: `Editable` / `Disabled` / `Hidden` + syarat pemicunya. Kalau BA belum menentukan, tulis eksplisit: `BELUM DIPUTUSKAN — [pertanyaan spesifik]` dan baris tsb WAJIB juga masuk sheet `Assumption_Decision_Risk_Open` DAN sheet `Critical_Challenge_QnA` (lihat 19) sebagai entry terhubung (Related ID) — supaya kelihatan di 2 tempat: konteks lokal (di sini) dan governance (di sana).

## 7.3 Component ID convention (Mode×Status explosion)
`CMP-[FIELD]-[MODE]` bila cukup 1 dimensi, atau `CMP-[FIELD]-[MODE]-[STATUS]` bila 2 dimensi. Contoh: `CMP-START-ADD`, `CMP-START-EDIT-SUBMITTED`, `CMP-START-EDIT-APPROVED`, `CMP-SAVE-EDIT-DRAFT`. ID dasar tanpa suffix TIDAK dipakai lagi begitu sebuah field punya >1 konteks — semua reference (Business Rule Related IDs, Message Catalog Component, Test Scenario Component) WAJIB mengikuti ID granular ini.

## 7.4 Contoh baris — datepicker Start/End (mengikuti pola user)
* CMP-START-ADD | MainPage_AddEdit | Header | Periode Start | Datepicker | Add | All | O/M(tentukan) | Date | min=SystemDate; max=EndDate | dd/mm/yyyy, bisa ketik | null | Editable | Isi tanggal mulai | min<=EndDate; format valid | - | VAL-START-001 | Master.StartDate | BR-xxx-001 | Confirmed
* CMP-START-EDIT-DRAFT | MainPage_AddEdit | Header | Periode Start | Datepicker | Edit | Draft/Submitted/dst (sebelum lock) | O/M | Date | min=SystemDate; max=EndDate | sama | existing value | Editable | Ubah tanggal mulai | sama seperti Add | - | VAL-START-001 | Master.StartDate | BR-xxx-002 | Confirmed
* CMP-START-EDIT-APPROVED | MainPage_AddEdit | Header | Periode Start | Datepicker | Edit | Approved/Confirmed/dst | - | Date | - | - | existing value | `BELUM DIPUTUSKAN — apakah Start Date pada record Approved boleh diubah oleh role tertentu (mis. Admin override)?` | - | - | - | - | BR-xxx-003 | ASM-xxx-010 | Assumption
* CMP-START-VIEW | MainPage_AddEdit | Header | Periode Start | Datepicker | View | All | - | Date | - | - | existing value | Disabled | Tampilkan saja | - | - | - | - | BR-xxx-004 | Confirmed

## 7.5 Checklist kelengkapan per component (semua jenis, bukan cuma field)
* Semua Mode yang berlaku pada screen ini sudah dicek (Add/Edit/View/dst).
* Semua Status record yang relevan pada Mode Edit sudah dicek satu-satu — bukan "status lain: default sama seperti draft" tanpa verifikasi.
* Permission/role yang mengubah enable-disable sudah eksplisit, bukan diasumsikan seragam.
* Min/Max/Format/Default sudah nilai final per konteks (bukan rumus umum tanpa angka).
* Null/blank/boundary value diperlakukan eksplisit.
* Loading/error/empty state untuk komponen non-field (grid, tombol) tetap mengikuti pola row-explosion yang sama.
