# Kiako-Skill-MC

Toolkit skill AI yang modular dan sadar versi untuk membantu pengembangan Minecraft Bedrock Add-on: Behavior Pack (BP), Resource Pack (RP), dan Script API.

## Prinsip kompatibilitas

- Periksa versi Minecraft Bedrock target serta versi module API sebelum menyarankan API atau format fitur.
- Gunakan dokumentasi resmi Microsoft Learn / Minecraft Creator sebagai sumber utama; bedakan API stable, beta, preview, dan fitur eksperimental.
- Jangan mengarang API atau menganggap dukungan satu versi berlaku pada versi lain.
- Pertahankan data pemain, UUID pack, namespace, dan identifier yang sudah ada.
- Pilih perubahan kecil dan praktis, hindari dependensi yang tidak diperlukan, dan jangan menyatakan pengujian berhasil bila belum dilakukan.

## 10 skill yang tersedia

| Skill | Fokus |
|---|---|
| [addon-architect](./skills/addon-architect/SKILL.md) | Merancang arsitektur fitur BP/RP/script, batas komponen, struktur, data, dan rencana implementasi. |
| [addon-validator](./skills/addon-validator/SKILL.md) | Mengaudit manifest, JSON, UUID, identifier, dependensi, aset, dan konsistensi pack. |
| [bedrock-api-expert](./skills/bedrock-api-expert/SKILL.md) | Memverifikasi dan menggunakan Minecraft Bedrock Script API secara sadar versi. |
| [bedrock-ui-expert](./skills/bedrock-ui-expert/SKILL.md) | Merancang UI berbasis form, alur interaksi pemain, validasi input, dan status UI. |
| [block-item-expert](./skills/block-item-expert/SKILL.md) | Membuat dan meninjau block, item, interaksi, recipe, loot, identifier, dan aset BP/RP. |
| [dynamic-property-expert](./skills/dynamic-property-expert/SKILL.md) | Merancang penyimpanan persisten, validasi data, dan migrasi yang aman. |
| [entity-expert](./skills/entity-expert/SKILL.md) | Menangani entity kustom, komponen, event, AI, spawn, animasi, dan integrasi script. |
| [javascript-debugger](./skills/javascript-debugger/SKILL.md) | Mendiagnosis bug JavaScript dan Script API dari bukti serta langkah reproduksi. |
| [performance-optimizer](./skills/performance-optimizer/SKILL.md) | Menganalisis bottleneck dan mengoptimalkan event, tick, entity, memori, UI, dan beban script. |
| [rpg-system-expert](./skills/rpg-system-expert/SKILL.md) | Merancang progression RPG, stats, level, class, ability, ekonomi, equipment, dan persistence. |

## Struktur repository

```text
Kiako-Skill-MC/
��── LICENSE
├── README.md
├── docs/
│   ├── architecture.md
│   ├── bedrock-api-versioning.md
│   ├── skill-development-guide.md
│   └── troubleshooting.md
└── skills/
    ├── addon-architect/SKILL.md
    ├── addon-validator/SKILL.md
    ├── bedrock-api-expert/SKILL.md
    ├── bedrock-ui-expert/SKILL.md
    ├── block-item-expert/SKILL.md
    ├── dynamic-property-expert/SKILL.md
    ├── entity-expert/SKILL.md
    ├── javascript-debugger/SKILL.md
    ├── performance-optimizer/SKILL.md
    └── rpg-system-expert/SKILL.md
```

## Cara menggunakan

1. Clone atau unduh repository.
2. Pilih folder skill yang sesuai dengan tugas; pertahankan nama folder dan `SKILL.md`.
3. Impor folder tersebut ke AI coding agent yang mendukung format skill `SKILL.md`. Dukungan impor berbeda antar-platform, jadi ikuti panduan platform yang digunakan.
4. Bila platform meminta URL, gunakan URL GitHub untuk folder skill atau tautan langsung ke `SKILL.md` pada branch yang ingin digunakan.
5. Untuk tugas lintas domain, gabungkan skill terkait secukupnya—misalnya `addon-architect` untuk rancangan, `bedrock-api-expert` untuk API, dan skill domain fitur untuk implementasi.

## Dokumentasi

- [Arsitektur dan pembagian tanggung jawab skill](./docs/architecture.md)
- [Panduan versi Minecraft Bedrock dan Script API](./docs/bedrock-api-versioning.md)
- [Panduan membuat dan memelihara skill](./docs/skill-development-guide.md)
- [Pemecahan masalah](./docs/troubleshooting.md)

## Kontribusi

- Jaga tiap skill tetap fokus, dengan tanggung jawab yang tidak tumpang tindih tanpa alasan.
- Pertahankan konten berguna dan pola repository yang ada.
- Verifikasi klaim teknis terhadap dokumentasi resmi untuk versi target.
- Jangan mengubah UUID, identifier, atau data pemain tanpa kebutuhan dan rencana migrasi yang jelas.
- Perbarui daftar skill, struktur, dan dokumentasi bila menambah atau memindahkan file.
- Periksa tautan internal, frontmatter YAML, dan format Markdown sebelum mengirim kontribusi.
- Laporkan dengan jujur pemeriksaan statis dan pengujian runtime yang benar-benar dilakukan.

## Batasan

Repository ini adalah toolkit dokumentasi untuk bantuan AI, bukan pengganti dokumentasi resmi atau pengujian pada Minecraft Bedrock. API dan perilaku harus diverifikasi untuk versi target dan proyek nyata.
