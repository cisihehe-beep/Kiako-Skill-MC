# Kiako-Skill-MC

Kumpulan skill AI untuk membantu pengembangan Minecraft Bedrock Add-on (Behavior Pack, Resource Pack, dan Script API).

## Isi skill

- `bedrock-api-expert` — API-aware dan version-aware untuk `@minecraft/server` / `@minecraft/server-ui`.
- `addon-architect` — rancangan struktur BP/RP dan arsitektur fitur.
- `javascript-debugger` — diagnosis dan perbaikan bug JavaScript.
- `dynamic-property-expert` — penyimpanan data persisten dan sistem ekonomi.
- `addon-validator` — audit manifest, JSON, UUID, identifier, aset, dan kompatibilitas.

## Cara menggunakan

Impor skill yang dibutuhkan ke AI coding agent yang mendukung format `SKILL.md`. Jika platform meminta URL GitHub, gunakan URL folder skill yang sesuai setelah folder ini diunggah ke repository.

## Prinsip proyek

- Periksa versi Minecraft Bedrock dan versi module API sebelum memakai API.
- Jangan mengarang API atau mengasumsikan semua versi mendukung fitur yang sama.
- Pertahankan UUID dan identifier proyek yang sudah ada.
- Utamakan perubahan kecil, aman, dan mudah dirawat.
- Jangan reset data pemain yang sudah tersimpan.

## Struktur

```text
Kiako-Skill-MC/
├── README.md
└── skills/
    ├── addon-architect/SKILL.md
    ├── addon-validator/SKILL.md
    ├── bedrock-api-expert/SKILL.md
    ├── dynamic-property-expert/SKILL.md
    └── javascript-debugger/SKILL.md
```
