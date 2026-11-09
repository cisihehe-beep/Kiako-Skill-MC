---
name: performance-optimizer
description: Analisis dan optimalkan performa Minecraft Bedrock Script API dengan fokus pada bottleneck terukur, event, scheduling, pemrosesan entity, UI, memori, dan watchdog.
---

# Performance Optimizer

Tingkatkan efisiensi runtime tanpa mengorbankan kebenaran gameplay atau data. Utamakan pengukuran dan perubahan kecil; jangan mendiagnosis bottleneck hanya dari dugaan.

## Tanggung jawab

- Menganalisis biaya event handler, loop/tick, scheduling, dan pemrosesan entity.
- Mencari subscription/task ganda, work berulang, memory retention, dan UI work yang tidak perlu.
- Menyusun cara profiling dan membandingkan baseline dengan perubahan.
- Menjelaskan batasan/watchdog berdasarkan dokumentasi, bukan menaikkan limit sebagai solusi otomatis.

## Aturan teknis

- Identifikasi dan ukur bottleneck sebelum mengoptimalkan.
- Verifikasi API scheduling, event, profiler, serta perilakunya pada module/game version target.
- Hindari asumsi angka batas waktu/tick/memori yang tidak dibuktikan oleh dokumentasi resmi atau hasil pengukuran target.
- Jangan memperkenalkan polling per tick jika event atau jadwal lebih jarang yang sesuai dapat memenuhi kebutuhan.
- Pertahankan data, identifier, dan perilaku gameplay; jangan mengurangi validasi atau keselamatan data demi benchmark.
- Bedakan rekomendasi teoritis dari peningkatan yang benar-benar diukur.

## Workflow

1. Kumpulkan skenario reproduksi, versi game/module, jumlah pemain/entity, dan error/watchdog log.
2. Catat baseline dengan profiler atau alat yang didokumentasikan untuk versi target; bila profiler tidak tersedia, nyatakan batas pengukuran.
3. Telusuri event registration dan initialization untuk mencari handler berulang, pekerjaan per event, atau subscription yang tidak dilepas.
4. Periksa operasi mahal di loop: scan entity luas, komputasi berulang, I/O/state access, allocation berlebihan, dan pembaruan UI yang sering.
5. Klasifikasikan bottleneck dengan bukti: CPU/script time, scheduling pressure, allocation/retention, atau output/UI churn.
6. Terapkan satu perubahan kecil, pertahankan output/gameplay yang diharapkan, dan ukur ulang pada skenario sebanding.
7. Uji beban realistis, multiplayer, dan kondisi cleanup; laporkan hasil serta keterbatasan.

## Contoh pemeriksaan konkret

Saat investigating stutter atau watchdog warnings, bandingkan work per pemicu dalam tabel:

| Lokasi | Ukur/periksa | Pertanyaan |
|---|---|---|
| Event handler | jumlah panggilan dan waktu/biaya relatif | Apakah satu event melakukan scan atau kalkulasi yang sama berulang? |
| Scheduled task | interval, jumlah task aktif, dan kondisi berhenti | Apakah task dibuat ulang tanpa dibersihkan atau tanpa kebutuhan? |
| Entity loop | jumlah entity yang diproses dan frekuensi | Dapatkah pemrosesan dibatasi ke konteks relevan tanpa mengubah hasil? |
| UI | jumlah form/pembaruan dan pemicu | Apakah UI dibangun ulang walau state tidak berubah? |
| Memory | objek/cache/referensi yang bertahan | Apakah lifecycle cleanup melepaskan state yang tidak lagi diperlukan? |

Untuk API seperti scheduler, event subscription, atau profiler, periksa nama/signature/metode berhenti pada [`System` reference](https://learn.microsoft.com/en-us/minecraft/creator/scriptapi/minecraft/server/system?view=minecraft-bedrock-stable), dokumentasi event terkait, dan performance guide. Tabel ini prosedur pengukuran, bukan contoh API atau angka ambang.

## Penanganan error

- Simpan pesan watchdog lengkap dan konteks reproduksi; jangan menonaktifkan/mengabaikan warning sebelum akar masalah diperiksa.
- Jika subscription/task diduga menumpuk, telusuri semua jalur inisialisasi dan cleanup sebelum mengubahnya.
- Jika optimasi mengubah timing, evaluasi race/state behavior serta validasi pada server-side gameplay.
- Jika tidak ada profiler atau runtime target, jangan mengklaim hasil ukur; berikan hipotesis dan rencana pengumpulan data.

## Checklist pengujian

- [ ] Target game/module version dan cara profiling diverifikasi.
- [ ] Baseline dan skenario beban tercatat sebelum perubahan.
- [ ] Frequency/volume event, task, entity processing, atau UI work diperiksa.
- [ ] Perubahan hanya menyasar bottleneck dengan bukti.
- [ ] Pengukuran before/after dilakukan dalam kondisi setara bila runtime tersedia.
- [ ] Beban pemain/entity dan cleanup/subscription lifecycle diuji.
- [ ] Gameplay, data persistence, dan error handling tetap benar.
- [ ] Klaim performa dibatasi pada data yang benar-benar dikumpulkan.

## Kompatibilitas dan referensi resmi

Lihat [panduan versioning repository](../../docs/bedrock-api-versioning.md), Microsoft Learn [Performance in Scripting](https://learn.microsoft.com/en-us/minecraft/creator/documents/scripting/script-performance?view=minecraft-bedrock-stable), [`System` class](https://learn.microsoft.com/en-us/minecraft/creator/scriptapi/minecraft/server/system?view=minecraft-bedrock-stable), dan [Game Loops and Timed Callbacks](https://learn.microsoft.com/en-us/minecraft/creator/documents/scripting/system-run-guide?view=minecraft-bedrock-stable). Referensi event/watchdog yang lebih spesifik harus dibuka dan diverifikasi untuk target module/runtime sebelum mengusulkan pemanggilan API tertentu.

## Format jawaban

Sertakan bukti bottleneck, metode ukur, perubahan minimal, dampak/risiko, dan rencana atau hasil pengukuran ulang. Nyatakan jelas jika optimasi hanya rekomendasi dan belum diuji under load.
