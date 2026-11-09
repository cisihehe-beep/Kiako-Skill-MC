# Kiako-Skill-MC

Kiako-Skill-MC is a modular, version-aware AI skill toolkit for Minecraft Bedrock add-on development. It supports Behavior Packs (BP), Resource Packs (RP), and Script API work.

## Compatibility principles

- Check the target Minecraft Bedrock version and Script API module versions before using an API or format feature.
- Prefer official Microsoft Learn and Minecraft Creator documentation.
- Distinguish stable, beta, preview, and experimental features.
- Do not invent APIs or assume that support in one version applies to another.
- Preserve player data, pack UUIDs, namespaces, and identifiers.
- Prefer small, practical changes. Do not claim tests were run unless they were.

## Available skills

| Skill | Focus |
|---|---|
| [addon-architect](./skills/addon-architect/SKILL.md) | Plan BP, RP, and script architecture, data boundaries, and implementation steps. |
| [addon-validator](./skills/addon-validator/SKILL.md) | Audit manifests, JSON, UUIDs, identifiers, dependencies, assets, and pack references. |
| [bedrock-api-expert](./skills/bedrock-api-expert/SKILL.md) | Verify and use Minecraft Bedrock Script API for the target version. |
| [bedrock-ui-expert](./skills/bedrock-ui-expert/SKILL.md) | Design form-based UI, player interaction flows, input validation, and UI state. |
| [block-item-expert](./skills/block-item-expert/SKILL.md) | Design and review blocks, items, interactions, recipes, loot, identifiers, and BP/RP assets. |
| [dynamic-property-expert](./skills/dynamic-property-expert/SKILL.md) | Design persistent storage, validation, and safe data migrations. |
| [entity-expert](./skills/entity-expert/SKILL.md) | Work with custom entities, components, events, AI, spawning, animation, and script integration. |
| [javascript-debugger](./skills/javascript-debugger/SKILL.md) | Diagnose JavaScript and Script API bugs from evidence and reproduction steps. |
| [performance-optimizer](./skills/performance-optimizer/SKILL.md) | Measure and improve event, scheduling, entity, memory, UI, and script performance. |
| [rpg-system-expert](./skills/rpg-system-expert/SKILL.md) | Design RPG progression, stats, levels, classes, abilities, economy, equipment, and persistence. |

## Repository structure

```text
Kiako-Skill-MC/
├── LICENSE
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

## Use the skills

1. Clone or download the repository.
2. Select the skill folder that matches the task. Keep its folder and `SKILL.md` together.
3. Import the folder into an AI coding agent that supports `SKILL.md`. Import steps vary by platform; follow that platform's instructions.
4. If the platform requests a GitHub URL, use the skill folder or the direct `SKILL.md` URL on the branch or release you want.
5. For work across domains, combine only the relevant skills. For example, use `addon-architect` for planning, `bedrock-api-expert` for API checks, and a domain skill for feature details.

## Documentation

- [Architecture and skill boundaries](./docs/architecture.md)
- [Minecraft Bedrock and Script API versioning](./docs/bedrock-api-versioning.md)
- [Creating and maintaining skills](./docs/skill-development-guide.md)
- [Troubleshooting](./docs/troubleshooting.md)

## Contributions

- Keep each skill focused. Avoid unnecessary overlap.
- Preserve useful existing guidance and repository structure.
- Verify technical claims against official documentation for the target version.
- Do not change UUIDs, identifiers, or player data without a clear need and migration plan.
- Update the README and relevant documentation when adding or moving a skill.
- Check Markdown, YAML frontmatter, and relative links before submitting changes.
- Report only checks and tests that were actually performed.

This repository is a documentation toolkit. It does not replace official documentation or testing in Minecraft Bedrock.
