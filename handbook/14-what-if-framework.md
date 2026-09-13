# 14. What-If & Critical Challenge QnA (SHEET GABUNGAN: `What_If_Critical_Challenge`)
Perubahan struktural: What-If Matrix dan Critical Challenge QnA (dulu 2 sheet terpisah) SEKARANG DIGABUNG jadi 1 sheet `What_If_Critical_Challenge`, dipisah 2 section berurutan dalam sheet yang sama (pola sama seperti sheet spec per Desain UI yang sudah 5 section dalam 1 sheet). Alasan: mengurangi jumlah sheet total, dan mempermudah cross-check karena kedua topik sering saling terkait dan sekarang bertetangga langsung.

What-if analysis wajib menjadi section, bukan catatan opsional — tujuannya mengidentifikasi change driver bernilai tinggi, coupling tersembunyi, dan extension point yang mencegah redevelopment mahal. Critical Challenge berperan sebagai **reviewer paling galak yang bisa dibayangkan** — profesor senior system analyst yang menjebol blueprint sebelum developer/QA menemukan lubangnya di production.

---

## SECTION A — What-If Matrix

### 14.1 Kolom Wajib
Scenario ID | Driver | What If | **Horizon (patokan waktu eksplisit, lihat 14.2)** | Impact (Rule/UI/API/Data/Test) | Migration/Compatibility | Extension Point | Mitigation | Decision Needed | **Related ID 1-4** (skema 7.3c) | **Jenis Jawaban** (lihat 14.4b) | Status | **Dampak ke Spec** (lihat 14.4c)

### 14.2 Horizon — Patokan Waktu Eksplisit (WAJIB)
* **Near** = kurang dari 2 tahun.
* **Mid** = 2-4 tahun.
* **Long** = 5 tahun atau lebih.
Definisi eksplisit ini WAJIB dipakai konsisten — "Near/Mid/Long" tanpa angka menyebabkan interpretasi bebas antar generate, tidak sejalan dengan target future-proof 5 tahun (lihat 5.1).

### 14.2b Five-level depth model
* L1 Current UI: Apa yang terlihat dan dilakukan saat ini.
* L2 Rule/Exception: Apa yang terjadi pada invalid, boundary, dan alternate flow.
* L3 Cross-layer Impact: Dampak ke API, data, security, audit, integration, test.
* L4 Evolution: Dampak perubahan volume, role, channel, workflow, regulation.
* L5 Transition: Migration, backward compatibility, rollout, rollback, coexistence.

Stop condition: What-if cukup ketika critical change driver memiliki impact, mitigation/extension point, decision owner, dan test strategy. Hindari spekulasi tanpa hubungan dengan modul atau konteks bisnis.

### 14.3 Kelengkapan wajib — checklist 16 kategori (lihat 15 What-If Library)
Untuk SETIAP modul, jalankan ke-16 kategori di 15 SATU PER SATU. Kategori tidak relevan tetap tulis 1 baris What If singkat + Impact "Not Applicable untuk konteks modul ini" + alasan singkat — supaya reviewer melihat kategori itu SUDAH dipertimbangkan dan sengaja dilewati, bukan lupa.

**Kategori tambahan kontekstual (bukan kategori ke-17 tetap)**: pertimbangkan driver spesifik konteks menu ini di luar 16 kategori baku — termasuk tapi TIDAK TERBATAS pada AI/automation (auto-suggest, otomasi keputusan) KALAU genuinely relevan ke sifat menu tersebut. Jangan tambahkan secara mekanis ke semua modul tanpa pertimbangan relevansi — beda dari 16 kategori wajib yang checklist-nya tertutup.

---

## SECTION B — Critical Challenge QnA (Devil's Advocate)

### 14.4 Prinsip Persona
Tulis pertanyaan dengan nada menantang, spesifik, dan sengaja mencari celah — bukan generik:
* LEMAH (jangan dipakai): "Bagaimana jika terjadi error saat submit?"
* KUAT (dipakai): "Kalau dua user beda region membuka record yang sama, satu approve dan satu reject dalam rentang 2 detik — siapa yang menang, dan apakah user yang kalah tahu keputusannya sudah usang?"

### 14.4a Kolom Wajib
Challenge ID | Section/Sheet Terkait | **Related ID 1-4** (skema 7.3c) | Pertanyaan Kritis | Kenapa Ini Penting (risiko kalau tidak dijawab) | Insight/Rekomendasi Awal (WAJIB diisi, **bahasa bisnis dulu** — lihat mandat 01) | **Jenis Jawaban** (lihat 14.4b) | Status (Open/Auto-Applied/Deferred) | Severity (Critical/High/Medium) | **Dampak ke Spec** (lihat 14.4c) | **Berlaku Untuk** (dedup, lihat 14.4e)

### 14.4b Klasifikasi "Jenis Jawaban" — Keputusan Bisnis vs Pola Teknis Standar (WAJIB)
* **Keputusan Bisnis**: jawaban bergantung kebijakan spesifik organisasi, tidak ada jawaban universal (mis. threshold reprint berulang, role yang berhak akses, batas maksimum selection per job). TETAP `Open`/`Assumption` sampai BA/PO konfirmasi — TIDAK dipromosikan otomatis.
* **Pola Teknis Standar**: Insight/Rekomendasi berupa best-practice rekayasa yang hampir selalu dipilih software modern, bukan soal kebijakan bisnis (katalog lengkap: 14.4d). WAJIB auto-apply — lihat 14.4c.

**Pemetaan default domain → Jenis Jawaban** (titik awal, boleh override per kasus dengan alasan eksplisit):
| Domain Critical Challenge (lihat 14.4f) | Default |
|---|---|
| Concurrency/race condition | Pola Teknis Standar |
| Boundary/edge value ekstrem | Pola Teknis Standar |
| Kegagalan parsial (bulk) | Pola Teknis Standar |
| Multi-device/multi-session | Pola Teknis Standar |
| Ambiguitas keputusan (editable/disabled) | Keputusan Bisnis |
| Permission edge case | Keputusan Bisnis |
| Reversibilitas aksi destruktif | Keputusan Bisnis |
| Transisi status "mustahil" | Tergantung konteks |
| Data dipakai transaksi lain | Tergantung konteks |
| Interpretasi ganda UI | Tergantung konteks |

What-If dengan Horizon=Near DAN mitigasi konkret (bukan spekulasi jauh) ikut kena aturan auto-apply yang sama (lihat 14.4c). Horizon Mid/Long TETAP murni dokumentasi masa depan, TIDAK di-auto-apply.

### 14.4c Auto-Apply — Mekanisme (WAJIB)
Begitu Challenge/What-If diklasifikasi Pola Teknis Standar (atau Near+mitigasi konkret), LANGSUNG (tidak menunggu konfirmasi manual BA/PO):
1. Buat Business Rule baru di sheet spec terkait, status `Proposed`, kolom Sumber = `Auto-Applied dari CQ-xxx`/`WF-xxx` (lihat 6.1).
2. Update/tambah baris Field Matrix relevan (row-explosion kalau perlu), kolom Sumber sama (lihat 7).
3. Tambah minimal 1 Test Scenario (ikut formula 16.3).
4. Status Challenge/What-If berubah menjadi **`Auto-Applied`** (bukan "Answered").
5. **Kolom "Dampak ke Spec" WAJIB diisi eksplisit** — daftar SEMUA ID yang ter-generate karena auto-apply ini (mis. "BR-RPFAK-015, CMP-SAVE-EDIT-DRAFT (baris baru), TC-RPFAK-011"). Kalau BA nanti membatalkan auto-apply ini, daftar ini jadi panduan persis bagian mana saja di spec yang harus dihapus/direvisi.
6. **Fill warna berbeda**: baris Business Rule/Field Matrix hasil Auto-Applied pakai fill oranye muda (FCE4D6) — beda dari kuning-assumption dan putih-confirmed, lihat 17.3.

### 14.4d Katalog Pola Teknis Standar (referensi baku, bahasa bisnis dulu)
Daftar pola yang SUDAH dianggap Pola Teknis Standar secara default (konsisten antar modul, tidak dinilai ad-hoc tiap generate):
* **Cegah submit dobel**: "Sistem harus bisa kenali kalau user tidak sengaja klik tombol Save 2x, dan tidak boleh menyimpan data itu dua kali." *(istilah teknis: idempotency)*
* **Deteksi data usang saat 2 orang edit bersamaan**: "Kalau 2 orang buka & edit data yang sama, sistem kasih tahu siapa yang datanya jadi usang duluan, bukan diam-diam menimpa." *(optimistic locking)*
* **Kegagalan sebagian saat proses banyak data sekaligus**: "Kalau dari 50 data yang diproses, 3 gagal, yang 47 tetap disimpan; yang gagal dilaporkan terpisah supaya bisa dicoba ulang — bukan semuanya dibatalkan." *(partial success handling)*
* **Retry otomatis saat layanan lain lambat/mati sebentar**: "Kalau sistem lain yang diajak kerja sama sedang lambat, coba lagi otomatis beberapa kali sebelum dianggap gagal." *(retry with backoff)*
* **Data terhapus tetap bisa dipulihkan**: "Data yang dihapus user disimpan dulu, supaya bisa dikembalikan kalau ternyata salah hapus." *(soft delete)*
* **Rentang tanggal berlaku dengan jelas**: "Setiap data yang berlaku untuk periode tertentu harus jelas dari kapan sampai kapan, dan sistem bisa lihat versi lama saat cek riwayat." *(effective dating)*

### 14.4e Dedup Lintas-Screen (WAJIB eksplisit menunjukkan dampak)
Kalau modul multi-screen, Critical Challenge yang mirip antar screen (mis. concurrency muncul di semua screen) WAJIB dikonsolidasi jadi 1 entry, BUKAN diduplikasi berlebihan per screen. Entry hasil konsolidasi WAJIB punya kolom **"Berlaku Untuk"** berisi daftar eksplisit semua screen/component yang kena (mis. "RPFAK_MainPage, RPFAK_ResultList") — jangan disembunyikan jadi 1 baris generik tanpa jejak cakupannya.

### 14.4f Domain Pertanyaan Wajib (per screen/modul, jangan skip diam-diam)
Concurrency & race condition; Ambiguitas keputusan (setiap "BELUM DIPUTUSKAN" di Field Matrix otomatis 1 entry); Boundary & edge value ekstrem; Perpindahan status "mustahil" tapi teknis bisa terjadi; Permission edge case; Data yang sudah dipakai transaksi lain; Multi-device/multi-session; Kegagalan parsial; Interpretasi ganda dari UI yang sama; Reversibilitas aksi destruktif.

### 14.4g Keterhubungan & Volume
Challenge/What-If yang masih `Open` WAJIB muncul di Index_Summary sebagai bagian dari Keputusan Kritis Belum Dikonfirmasi. Volume wajar: screen kompleks (10-25 component) → 8-15 challenge; screen sederhana → tetap minimal 3-5 — tidak ada screen yang "terlalu simpel untuk ditantang".
