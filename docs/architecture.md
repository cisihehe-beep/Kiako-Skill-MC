# Kiako-Skill-MC

Kiako-Skill-MC is a modular, version-aware AI skill toolkit for Minecraft Bedrock add-on development. It helps AI coding agents and developers work safely with Behavior Packs, Resource Packs, Script API, UI systems, entities, items, progression systems, and performance-sensitive gameplay logic.

## Project overview

This repository is designed to provide specialized knowledge for common Bedrock add-on tasks without inventing APIs or assuming features work across versions. Every skill follows a simple principle:

- Verify the target Bedrock version before using any API or feature.
- Prefer official Microsoft Learn and Minecraft Creator documentation.
- Protect existing world data, identifiers, and UUIDs.
- Favor small, maintainable changes over broad rewrites.
- Make risks and compatibility assumptions explicit.

## Available skills

### Core skills

- `bedrock-api-expert` — version-aware guidance for Bedrock Script API and module usage.
- `addon-architect` — architecture and technical planning for BP/RP/script-based features.
- `addon-validator` — audit of manifests, JSON, identifiers, dependencies, and pack integrity.
- `dynamic-property-expert` — persistent data design, validation, and migration for player/world/entity state.
- `javascript-debugger` — diagnosis and debugging of JavaScript and Script API runtime issues.

### Expanded Bedrock skills

- `bedrock-ui-expert` — Action Form, Modal Form, Message Form, and player UI state flow.
- `entity-expert` — custom entities, AI behavior, components, events, and animation integration.
- `block-item-expert` — custom blocks, items, recipes, loot tables, interactions, and asset compatibility.
- `rpg-system-expert` — health, mana, stamina, level, economy, progression, and inventory design.
- `performance-optimizer` — event optimization, tick budgeting, memory awareness, and watchdog protection.

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

## Import instructions

These skill files follow the `SKILL.md` convention used by AI coding agents that support GitHub-hosted skills.

To use them:

1. Clone or download the repository.
2. Keep the `skills/` folder structure intact.
3. Import the required skill directory into the agent or platform that supports skill loading.
4. If the platform requires a direct URL, point it to the relevant GitHub folder or raw file path for the skill.

Example:

```text
https://github.com/cisihehe-beep/Kiako-Skill-MC/tree/feature/expand-bedrock-skills/skills
```

If a platform expects a single skill file, point it directly to the folder file:

```text
https://github.com/cisihehe-beep/Kiako-Skill-MC/blob/feature/expand-bedrock-skills/skills/bedrock-api-expert/SKILL.md
```

## Compatibility philosophy

This project is intentionally version-aware rather than version-agnostic.

- We do not assume one Bedrock version behaves like another.
- We distinguish stable APIs from beta or experimental APIs.
- We prefer documentation and project evidence over memory or unsupported assumptions.
- We preserve player data, identifiers, UUIDs, and pack compatibility unless a migration plan is clearly required.
- We avoid unnecessary dependencies and broad architectural churn.

## Contribution guidelines

1. Keep each skill focused on a specific concern.
2. Do not duplicate responsibilities across skills.
3. Always verify API usage against the target Bedrock version.
4. Preserve existing data and identifiers when modifying a project.
5. Document assumptions and document version constraints.
6. Prefer small, practical, maintainable solutions over abstract frameworks.
7. Do not claim code or gameplay behavior was tested if it was not actually validated.
8. Update the relevant documentation when adding or changing a skill.

## Documentation index

- [Architecture overview](./docs/architecture.md)
- [Bedrock API versioning guide](./docs/bedrock-api-versioning.md)
- [Skill development guide](./docs/skill-development-guide.md)
- [Troubleshooting guide](./docs/troubleshooting.md)

## Recommended usage

Use the skills by responsibility instead of by generality:

- Use `addon-architect` to plan the feature and system boundaries.
- Use `addon-validator` before or after a large change to spot manifest and asset issues.
- Use `bedrock-api-expert` for script API questions and compatibility checks.
- Use `dynamic-property-expert` for player/world/state persistence design.
- Use `entity-expert` for custom mobs and AI systems.
- Use `block-item-expert` for custom blocks, items, and recipe logic.
- Use `bedrock-ui-expert` for forms and interactive UI flows.
- Use `rpg-system-expert` for progression and economy systems.
- Use `performance-optimizer` when runtime or tick performance becomes a risk.
- Use `javascript-debugger` for runtime errors and debugging logic issues.

## Maintainer notes

This repository is intended to be a practical knowledge source for AI-assisted Bedrock add-on work. It should remain compact, maintainable, and aligned to actual Bedrock capabilities rather than broad, speculative abstractions.

---

For more details, see the documentation folder and the individual `SKILL.md` files.
