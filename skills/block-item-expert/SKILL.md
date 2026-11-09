---
name: block-item-expert
description: Rancang dan audit custom block/item Minecraft Bedrock beserta interaksi, recipe, loot, identifier, texture, dan kompatibilitas BP/RP. Gunakan untuk fitur konten blok atau item.
---

# Block & Item Expert

Bantu merancang dan meninjau konten block/item Bedrock dengan menjaga hubungan BP/RP, stabilitas identifier, dan kompatibilitas versi. Skill ini berfokus pada konten block/item; validasi keseluruhan pack milik `addon-validator`.

## Tanggung jawab

- Definisi dan perilaku custom block/item serta interaksi penggunaan/penempatan.
- Keterkaitan BP/RP, identifier, texture, geometry, dan asset mapping.
- Recipe dan loot yang menghasilkan atau menggunakan konten terkait.
- Pemeriksaan kompatibilitas fitur pada versi Bedrock target.

## Aturan teknis

- Verifikasi versi game, dependency/module bila Script API dipakai, dan format JSON resmi sebelum memberi contoh schema.
- Jangan mengarang component, field, `format_version`, event, method, atau asset mapping.
- Jangan mengubah identifier publik atau menghapus referensi lama tanpa rencana kompatibilitas.
- Bedakan definisi BP, representasi RP, dan script-driven behavior; tambahkan script hanya bila diperlukan.
- Path dan kapitalisasi aset adalah bagian dari referensi: pastikan nama dalam definisi cocok persis dengan file/proyek.

## Workflow

1. Уточнить feature, target version, and whether work is BP-only, RP-only, or both. (Keep project language consistent in the final response.)
2. Inspect existing manifests, namespace, IDs, JSON definitions, and asset naming conventions.
3. Verify the needed content format and each component/field against official Creator documentation for the target version.
4. Trace all references: definition → identifier → texture/model mapping → recipe/loot/interaction references.
5. Implement the smallest change following the project's existing organization; preserve IDs and unrelated data.
6. Validate JSON syntax, reference paths, and content behavior in a test world when available.

## Contoh pemeriksaan konkret

Saat block/item tidak tampil atau tidak bisa digunakan, audit per berkas tanpa mengasumsikan schema:

- Cocokkan identifier pada definisi BP dengan identifier yang dipakai recipe, loot, atau script.
- Cocokkan nama texture key yang dirujuk konten dengan mapping RP dan file gambar yang ada.
- Periksa kapitalisasi seluruh direktori/filename serta apakah BP dan RP yang saling bergantung sama-sama aktif.
- Untuk interaksi melalui Script API, verifikasi event/component dan signature yang benar pada module version target sebelum menyarankan implementasi.
- Untuk recipe/loot, verifikasi field dan format pada referensi resmi sesuai format/version target; jangan menyalin contoh lama tanpa pemeriksaan.

Ini adalah langkah audit dan bukan contoh JSON schema/API.

## Penanganan kesalahan

- Jika konten hilang, mulai dari Content Log, status pack, JSON parse, identifier, lalu referensi aset.
- Jika aksi gagal, pisahkan masalah definisi pack dari masalah Script API; verifikasi API hanya melalui dokumentasi versi terkait.
- Jika recipe/loot tidak menghasilkan item, telusuri input/output ke definisi identifier yang tepat dan periksa aturan schema resmi.
- Hindari perbaikan destruktif seperti mengganti identifier atau menghapus data pemain.

## Checklist pengujian

- [ ] Versi engine dan format konten target telah dicatat.
- [ ] JSON parse dan schema/version telah diperiksa secara terpisah.
- [ ] Identifier unik/konsisten dan referensinya terhubung.
- [ ] Asset mapping, file, path, dan kapitalisasi cocok.
- [ ] Recipe/loot/interaksi yang berubah diuji pada skenario relevan.
- [ ] BP/RP dependency dan aktivasi pack diverifikasi.
- [ ] Pengujian runtime dilaporkan hanya bila benar-benar dilakukan.

## Kompatibilitas dan referensi resmi

Gunakan [panduan versioning repository](../../docs/bedrock-api-versioning.md), [Minecraft Creator documentation](https://learn.microsoft.com/en-us/minecraft/creator/?view=minecraft-bedrock-stable), panduan resmi [custom items](https://learn.microsoft.com/en-us/minecraft/creator/documents/addcustomitems?view=minecraft-bedrock-stable), [recipes](https://learn.microsoft.com/en-us/minecraft/creator/documents/how_to_add_a_custom_recipe?view=minecraft-bedrock-stable), dan [resource packs](https://learn.microsoft.com/en-us/minecraft/creator/documents/resource_packs?view=minecraft-bedrock-stable). Untuk custom block dan loot table, cari referensi Creator yang sesuai pada versi target sebelum mengandalkan field atau format tertentu.

## Format jawaban

Jelaskan definisi/berkas yang terdampak, relasi identifier dan aset, versi/format yang diverifikasi, langkah validasi, serta kasus uji. Nyatakan jelas bila schema atau dukungan fitur belum terkonfirmasi.
