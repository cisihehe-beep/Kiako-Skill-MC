---
name: addon-validator
description: Audit Minecraft Bedrock Add-on untuk masalah manifest, JSON, UUID, identifier, aset, dependensi, dan kompatibilitas. Gunakan saat memeriksa atau memvalidasi Behavior Pack, Resource Pack, atau Script API.
---

# Add-on Validator

Lakukan audit dengan mengutamakan temuan yang bisa direproduksi dan perbaikan yang tidak merusak proyek.

## Checklist

- Validasi sintaks JSON dan bentuk data yang diwajibkan oleh skema yang sesuai versi.
- Periksa `manifest.json`: format versi, UUID unik, modul, versi, dependensi, dan module API.
- Periksa kecocokan UUID dependensi antara pack serta konsistensi UUID pada berkas terkait.
- Cari identifier tanpa namespace, duplikasi identifier, referensi yang tidak cocok, dan perubahan nama yang memutus kompatibilitas.
- Cocokkan referensi tekstur, model, suara, animasi, UI, dan aset lain dengan berkas yang tersedia.
- Periksa struktur folder, ejaan dan kapitalisasi nama berkas, serta pemisahan BP/RP.
- Verifikasi API/module version dan fitur eksperimental terhadap versi target; jangan menebak dukungan versi.
- Periksa dampak perubahan terhadap data persistent dan jangan menyarankan reset data pemain sebagai perbaikan umum.

## Pelaporan

Untuk setiap temuan, sertakan tingkat keparahan, lokasi berkas/baris bila tersedia, alasan, dampak, dan usulan perbaikan minimal. Bedakan error yang terkonfirmasi dari risiko atau hal yang memerlukan pengujian. Akhiri dengan langkah verifikasi pada versi Minecraft target.
