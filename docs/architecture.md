# Architecture overview

Kiako-Skill-MC contains focused AI skills for Minecraft Bedrock add-on development. It is a documentation toolkit, not a runtime framework. Each skill covers one main area and may refer work to another skill when a task crosses boundaries.

## Design principles

- Verify support for the target game and module versions.
- Prefer official Microsoft Learn and Minecraft Creator documentation.
- Preserve player data, UUIDs, namespaces, and identifiers.
- Prefer small changes and avoid unnecessary dependencies.
- State assumptions and separate verified results from proposed checks.

## Skill responsibilities

### Planning and validation

- `addon-architect` plans feature structure and BP, RP, and script boundaries.
- `addon-validator` checks pack-wide structure, manifests, JSON, identifiers, dependencies, and asset references.

### Script API and diagnostics

- `bedrock-api-expert` verifies Script API availability and module compatibility.
- `javascript-debugger` investigates JavaScript and runtime failures using logs and reproduction steps.
- `performance-optimizer` investigates measured performance bottlenecks and resource use.

### Feature domains

- `bedrock-ui-expert` handles forms and player interaction flows.
- `entity-expert` handles entity definitions, behavior, spawning, and animation links.
- `block-item-expert` handles block and item definitions and their recipe, loot, and asset references.
- `rpg-system-expert` handles progression and economy rules.
- `dynamic-property-expert` handles persistent data schemas, validation, and migration.

## Suggested workflow

1. Identify the feature and target Minecraft version.
2. Inspect the existing pack, manifests, identifiers, and data before planning changes.
3. Choose the smallest relevant set of skills.
4. Verify API and format support before implementation.
5. Make the smallest practical changes and validate references and schemas.
6. Test in a copy or test world on the target version when possible. Report runtime tests only if they were run.

## Documentation

- [Bedrock API versioning](./bedrock-api-versioning.md) covers game, module, and API stability versions.
- [Skill development](./skill-development-guide.md) explains how to write and maintain `SKILL.md` files.
- [Troubleshooting](./troubleshooting.md) covers common pack and script failures.

This repository does not replace official documentation. See the [Minecraft Creator documentation](https://learn.microsoft.com/en-us/minecraft/creator/?view=minecraft-bedrock-stable) for version-specific references.
