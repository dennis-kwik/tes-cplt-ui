# 14. What-If and Future Change Framework
What-if analysis wajib menjadi section, bukan catatan opsional. Tujuannya bukan merancang semua kemungkinan, tetapi mengidentifikasi change driver bernilai tinggi, coupling tersembunyi, dan extension point yang mencegah redevelopment mahal.

## 14.1 Template What-If Matrix
* Scenario ID: WF-[MODULE]-NNN.
* Change Driver: Regulatory, growth, channel, organization, integration, technology.
* What If: Perubahan yang diuji.
* Likelihood/Horizon: Low/Medium/High; near/mid/long term.
* Impacts: Business rule, UI, API, data, security, operation, test.
* Migration/Compatibility: Historical data, consumer lama, rollout, rollback.
* Extension Point: Configuration, abstraction, versioning, relation model.
* Mitigation: Keputusan sekarang untuk menurunkan cost of change.
* Decision Needed: Owner dan kapan harus diputuskan.
* Related IDs: Rule, risk, decision, test.

## 14.2 Five-level depth model
* L1 Current UI: Apa yang terlihat dan dilakukan saat ini.
* L2 Rule/Exception: Apa yang terjadi pada invalid, boundary, dan alternate flow.
* L3 Cross-layer Impact: Dampak ke API, data, security, audit, integration, test.
* L4 Evolution: Dampak perubahan volume, role, channel, workflow, regulation.
* L5 Transition: Migration, backward compatibility, rollout, rollback, coexistence.

Stop condition: What-if cukup ketika critical change driver memiliki impact, mitigation/extension point, decision owner, dan test strategy. Hindari spekulasi tanpa hubungan dengan modul atau konteks bisnis.

## 14.3 Kelengkapan wajib — checklist 16 kategori, JANGAN pilih-pilih diam-diam
Untuk SETIAP modul, jalankan ke-16 kategori di 15 (What-If Scenario Library) SATU PER SATU. Kalau kategori tidak relevan untuk modul ini, tetap tulis 1 baris dengan What If singkat + Impact "Not Applicable untuk konteks modul ini" + alasan singkat — supaya reviewer melihat kategori itu SUDAH dipertimbangkan dan sengaja dilewati, bukan lupa. Ini pola yang sama seperti 6.2 (rule domain checklist) — kelengkapan dibuktikan lewat jejak "sudah dicek", bukan diasumsikan dari banyaknya baris.