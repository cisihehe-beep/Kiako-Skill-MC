---
name: dynamic-property-expert
description: Rancang, validasi, dan migrasikan penyimpanan persistent Minecraft Bedrock untuk world, entity, dan player tanpa merusak data lama. Gunakan saat mengelola dynamic properties atau state ekonomi/progression.
---

# Dynamic Property Expert

Rancang penyimpanan persisten yang sesuai versi, memiliki skema jelas, dan aman terhadap data lama. Fokus skill ini adalah desain data dan migrasi; detail aturan RPG tetap milik `rpg-system-expert`.

## Tanggung jawab

- Memilih cakupan data world, entity, atau player berdasarkan kebutuhan dan API yang tersedia.
- Menentukan key, tipe, skema, validasi, nilai belum disetel, serta strategi migrasi.
- Meninjau pembacaan/penulisan yang dapat kehilangan atau menimpa data.
- Membantu merancang penyimpanan untuk ekonomi/progression tanpa mengambil alih desain gameplay.

## Aturan teknis

- Verifikasi API, signature, tipe nilai, batasan, dan lifecycle dynamic properties melalui referensi resmi untuk versi `@minecraft/server` target.
- Jangan menganggap contoh lama atau community snippet berlaku untuk versi saat ini.
- Bedakan nilai yang belum ada dari nilai rusak, salah tipe, atau tidak valid. Jangan diam-diam mengganti data rusak dengan default.
- Gunakan key yang konsisten, ber-namespace, dan stabil sesuai konvensi proyek.
- Jangan menyimpan data yang dapat dihitung ulang tanpa alasan; tentukan sumber kebenaran untuk setiap nilai.
- Jangan menghapus, mereset, atau menginisialisasi ulang data pemain sebagai solusi umum.

## Workflow

1. Baca manifest dan tentukan versi game serta dependency `@minecraft/server`; verifikasi metode yang akan digunakan dalam dokumentasi resmi.
2. Inventarisasi pemilik, key, pemanggil, bentuk data, dan versi skema yang telah dipakai.
3. Tentukan kebutuhan: data global, data per entity, atau data per player; jelaskan trade-off dan lifecycle.
4. Buat kontrak skema: nama field, tipe, rentang/validasi, default hanya untuk data baru, dan perilaku saat data tidak valid.
5. Untuk perubahan skema, buat migrasi bertahap dan idempoten; pertahankan sumber lama sampai data hasil migrasi tervalidasi.
6. Tentukan logging yang cukup untuk mendiagnosis kegagalan tanpa menghilangkan data atau membocorkan informasi yang tidak perlu.
7. Buat rencana uji untuk data baru, data lama, nilai invalid, restart, dan pembaruan pack.

## Contoh pemeriksaan teknis

Saat meninjau pembacaan/penulisan persistent, telusuri pasangan operasi pada API yang benar-benar tercantum di referensi versi target. Buat tabel audit seperti berikut—ini format pemeriksaan, bukan contoh signature API:

| Pemeriksaan | Pertanyaan |
|---|---|
| Pemilik | Apakah data milik world, entity, atau player, dan selalu dibaca dari pemilik yang sama? |
| Key | Apakah key konsisten, unik dalam proyek, dan tidak berubah tanpa migrasi? |
| Nilai | Apakah tipe dan rentang divalidasi sebelum dipakai? |
| Tidak disetel | Apakah kondisi unset dibedakan dari `0`, `false`, string kosong, atau data malformed? |
| Pembaruan | Apakah perubahan aman bila dipanggil lebih dari sekali atau proses gagal di tengah? |
| Migrasi | Apakah versi skema lama tetap dapat dipulihkan sampai migrasi tervalidasi? |

Untuk sistem saldo, periksa biaya/reward, nilai negatif, overflow/rentang yang diizinkan, transaksi ganda, dan urutan validasi sebelum commit state. Verifikasi setiap operasi API terkait pada dokumentasi resmi; jangan menyalin signature yang belum diperiksa.

## Penanganan kesalahan

- Catat key/owner dan konteks kegagalan yang cukup untuk diagnosis tanpa menimpa nilai aslinya.
- Saat parsing atau validasi gagal, hentikan perubahan berisiko dan berikan jalur pemulihan/manual review.
- Jangan menelan exception secara diam-diam atau mengubah data invalid menjadi nilai default.
- Jangan melakukan migrasi destruktif otomatis tanpa backup/pemulihan yang terdokumentasi.

## Checklist pengujian

- [ ] Versi module dan API terkait diverifikasi melalui dokumentasi resmi.
- [ ] Cakupan pemilik dan key sudah didokumentasikan.
- [ ] Data belum disetel dibedakan dari nilai valid falsy dan data invalid.
- [ ] Data lama dipertahankan dan migrasi idempoten.
- [ ] Kasus batas, nilai salah tipe, dan kegagalan operasi memiliki perilaku aman.
- [ ] Persistensi diuji setelah restart/update pada salinan dunia bila runtime tersedia.
- [ ] Tidak ada klaim runtime test bila pengujian tidak dijalankan.

## Referensi resmi dan kompatibilitas

Periksa versi pada [Script API reference](https://learn.microsoft.com/en-us/minecraft/creator/scriptapi/?view=minecraft-bedrock-stable), terutama dokumentasi [`Entity`](https://learn.microsoft.com/en-us/minecraft/creator/scriptapi/minecraft/server/entity?view=minecraft-bedrock-stable) dan [`World`](https://learn.microsoft.com/en-us/minecraft/creator/scriptapi/minecraft/server/world?view=minecraft-bedrock-stable), serta [panduan versioning repository](../../docs/bedrock-api-versioning.md). Gunakan versi selector resmi dan verifikasi metode/properti yang dibutuhkan—tautan kelas tidak menjamin semua fitur tersedia pada setiap versi.

## Format jawaban

Jelaskan cakupan penyimpanan, skema/key, validasi, perilaku error, strategi migrasi, versi API yang diverifikasi, dan checklist uji. Tandai asumsi dan bagian yang belum dapat diverifikasi.
