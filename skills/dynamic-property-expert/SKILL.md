---
name: dynamic-property-expert
description: Rancang penyimpanan persistent Minecraft Bedrock menggunakan dynamic properties, termasuk data pemain dan sistem ekonomi. Gunakan saat membuat, membaca, memperbarui, atau memigrasikan data.
---

# Dynamic Property Expert

Rancang penyimpanan yang aman terhadap restart, perubahan versi, dan data lama.

## Prinsip

- Verifikasi API, batasan tipe/nilai, registrasi, dan lifecycle dynamic properties terhadap versi module API target.
- Tentukan pemilik dan cakupan data dengan jelas (world, entity, atau player) berdasarkan API yang tersedia.
- Gunakan nama key yang konsisten dan ber-namespace untuk mengurangi benturan.
- Validasi nilai yang dibaca; sediakan default hanya untuk data yang memang belum ada, bukan untuk menimpa data rusak secara diam-diam.
- Untuk operasi ekonomi, validasi jumlah, batas saldo, input negatif, pembulatan, dan transaksi berulang.
- Hindari menyimpan data berlebihan atau mengandalkan urutan objek yang tidak dijamin.

## Migrasi dan keselamatan

- Jangan reset atau menghapus data pemain yang sudah tersimpan sebagai langkah perbaikan.
- Buat migrasi bertahap dan idempoten: aman dijalankan lebih dari sekali.
- Pertahankan data lama sampai migrasi tervalidasi; jelaskan kompatibilitas mundur dan rencana pemulihan.
- Tangani kegagalan parse/validasi dengan logging yang berguna tanpa membocorkan atau menghilangkan data.

## Jawaban

Jelaskan skema dan cakupan penyimpanan, API/versi yang diperlukan, strategi validasi dan migrasi, serta kasus pengujian seperti data kosong, nilai tidak valid, batas saldo, restart, dan peningkatan versi.
