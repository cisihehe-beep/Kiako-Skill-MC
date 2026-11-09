---
name: javascript-debugger
description: Diagnosis dan perbaiki bug JavaScript pada Minecraft Bedrock Add-on dan Script API. Gunakan saat menganalisis error, perilaku tak terduga, atau kode yang gagal.
---

# JavaScript Debugger

Temukan akar masalah berdasarkan bukti, lalu usulkan perbaikan paling kecil yang aman.

## Alur diagnosis

1. Kumpulkan pesan error lengkap, stack trace, langkah reproduksi, versi Minecraft, versi module API, dan konteks kode.
2. Telusuri alur data dan lifecycle event terkait; bedakan error sintaks, runtime, kompatibilitas API, dan logika.
3. Periksa nilai `undefined`/`null`, tipe data, asumsi entity/world, timing, event yang terdaftar, serta operasi asynchronous.
4. Verifikasi setiap API yang dicurigai untuk versi target; jangan menyimpulkan bahwa API tersedia hanya berdasarkan contoh versi lain.
5. Buat perubahan terkecil yang memperbaiki penyebab, bukan sekadar menyembunyikan error.
6. Sertakan langkah reproduksi ulang, pemeriksaan log, dan pengujian regresi.

## Batas keselamatan data

- Jangan menghapus atau mereset dynamic properties maupun data pemain untuk menghilangkan gejala.
- Jangan menelan error tanpa logging atau penanganan yang jelas.
- Pertahankan identifier dan perilaku yang sudah digunakan proyek kecuali perubahan tersebut memang diperlukan dan disertai migrasi.

## Format jawaban

Sajikan akar masalah, bukti yang mendukung, file/baris terkait, perbaikan yang disarankan, serta cara memverifikasi. Jika bukti belum cukup, nyatakan hipotesis dan minta detail reproduksi yang diperlukan.
