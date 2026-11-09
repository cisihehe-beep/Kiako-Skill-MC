---
name: addon-validator
description: Audit Minecraft Bedrock Add-on untuk konsistensi manifest, JSON, UUID, identifier, dependensi, dan aset BP/RP. Gunakan saat memeriksa integritas pack atau meninjau perubahan sebelum rilis.
---

# Add-on Validator

Lakukan audit yang dapat ditelusuri dan utamakan temuan yang bisa direproduksi. Skill ini bertanggung jawab atas validasi pack secara menyeluruh; diagnosis runtime mendalam tetap dapat didelegasikan ke `javascript-debugger` atau skill domain.

## Tanggung jawab

- Memeriksa struktur pack, manifest, UUID, versi, dependency, dan entry point script.
- Memvalidasi JSON dan referensi silang menurut skema/versi target.
- Mencari identifier, aset, dan dependensi yang hilang, duplikat, atau tidak konsisten.
- Melaporkan severity, bukti, dampak, dan perbaikan minimal tanpa mengubah data secara tidak aman.

## Aturan teknis

- Tentukan versi Minecraft Bedrock dan module API sebelum menilai kompatibilitas.
- Validasi sintaks JSON terpisah dari validasi schema dan runtime; valid JSON belum tentu valid untuk engine.
- Jangan menganggap format_version atau komponen berlaku lintas versi; verifikasi dokumentasi Creator resmi.
- Jangan mengganti UUID, identifier, namespace, atau dynamic properties sebagai perbaikan generik.
- Bedakan error terkonfirmasi, kemungkinan risiko, dan hal yang perlu diuji di runtime.

## Workflow audit

1. Petakan BP/RP dan berkas manifest sebelum mengubah file.
2. Parse setiap manifest/JSON dengan parser yang tersedia; jika tidak ada parser, laporkan bahwa pemeriksaan sintaks belum otomatis.
3. Periksa UUID pack/module, versi, minimum engine, tipe module, entry point, serta dependency BP/RP/API. Cocokkan referensi silang.
4. Kumpulkan identifier yang didefinisikan dan dirujuk; tandai definisi hilang, duplikasi, ejaan berbeda, dan referensi tanpa pasangan.
5. Cocokkan path aset dan kapitalisasi dengan file nyata; periksa tekstur, geometry, animation, sound, loot, recipe, dan localization yang relevan.
6. Verifikasi fitur/API/format terhadap Creator documentation untuk versi target.
7. Susun temuan dari severity tertinggi, sertakan bukti dan perbaikan spesifik.
8. Re-run pemeriksaan yang tersedia sesudah perbaikan dan jelaskan pemeriksaan runtime yang masih harus dilakukan.

## Contoh audit referensi

Buat daftar sederhana sebelum menyatakan referensi lengkap:

| Sumber | Referensi yang ditemukan | Target yang harus ada |
|---|---|---|
| Manifest BP | UUID dependency pack, script entry, module dependency | UUID/versi pack dan berkas entry yang cocok |
| Definisi konten | identifier entity/item/block | semua penggunaan identifier tersebut |
| Recipe/loot | identifier input dan output | definisi item/block yang sesuai |
| RP | texture, geometry, animation, sound reference | file/path dengan kapitalisasi yang cocok |

Contoh ini adalah prosedur audit, bukan klaim schema JSON. Gunakan dokumentasi resmi untuk menentukan path atau field schema yang benar pada format target.

## Pelaporan temuan

Untuk setiap isu tulis:
- **Severity**: blocker, high, medium, atau low, dengan alasan dampaknya.
- **Lokasi**: file/baris atau pointer JSON bila tersedia.
- **Bukti**: pesan log, referensi yang tidak cocok, atau aturan resmi yang berlaku.
- **Dampak**: kegagalan load, konten hilang, kompatibilitas, atau risiko data.
- **Perbaikan**: perubahan sekecil mungkin dan risiko migrasinya.

Jangan menyebut sebuah API/schema invalid hanya berdasarkan ingatan. Jika dokumentasi atau target versi tidak tersedia, klasifikasikan sebagai belum terverifikasi.

## Checklist validasi

- [ ] Seluruh manifest dan JSON yang relevan diperiksa sintaksnya.
- [ ] Schema, `format_version`, module/API, dan minimum engine diverifikasi untuk target.
- [ ] UUID dan dependency pack cocok; tidak ada UUID yang diganti tanpa alasan.
- [ ] Identifier referensi dapat ditelusuri ke definisi dan konsisten ejaannya.
- [ ] Path dan kapitalisasi aset cocok dengan file yang ada.
- [ ] Temuan membedakan fakta, risiko, dan kebutuhan runtime test.
- [ ] Perbaikan tidak mereset player data atau merusak identifier publik.

## Referensi resmi

Gunakan [panduan versioning](../../docs/bedrock-api-versioning.md), referensi resmi [`manifest.json`](https://learn.microsoft.com/en-us/minecraft/creator/reference/content/addonsreference/packmanifest?view=minecraft-bedrock-stable), [Minecraft Creator documentation](https://learn.microsoft.com/en-us/minecraft/creator/?view=minecraft-bedrock-stable), dan [Script API reference](https://learn.microsoft.com/en-us/minecraft/creator/scriptapi/?view=minecraft-bedrock-stable). Pilih versi dokumentasi yang sesuai target.
