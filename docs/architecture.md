# Architecture overview

Kiako-Skill-MC is a collection of focused AI skills for Minecraft Bedrock add-on development. The repository provides guidance, not a runtime framework: skills help an agent inspect a project, choose an appropriate domain, and make version-aware changes.

## Design principles

- Verify capabilities against the target game and module versions.
- Prefer official Microsoft Learn / Minecraft Creator documentation.
- Keep existing UUIDs, identifiers, namespaces, and player data intact.
- Avoid unnecessary dependencies and broad rewrites.
- State assumptions and distinguish verified results from proposed checks.

## Skill boundaries

### Planning and validation

- `addon-architect` owns feature decomposition, BP/RP/script boundaries, and implementation planning.
- `addon-validator` owns pack-wide validation of manifests, JSON, identifiers, dependencies, and asset references.

### Script API and debugging

- `bedrock-api-expert` verifies Script API availability, module dependencies, and version-specific usage.
- `javascript-debugger` investigates JavaScript/runtime failures and identifies root causes from logs and reproduction steps.
- `performance-optimizer` investigates measured runtime bottlenecks, event/tick work, and resource growth.

### Feature domains

- `bedrock-ui-expert` owns forms and interaction flow; it does not own general progression or storage design.
- `entity-expert` owns entity definitions, behavior, events, spawn setup, animation integration, and entity-specific script concerns.
- `block-item-expert` owns block/item definitions and their recipe, loot, identifier, and asset links.
- `rpg-system-expert` owns progression and economy rules, while delegating UI, API verification, and persistence details to their respective focused skills when needed.
- `dynamic-property-expert` owns persistent data schema, validation, and migration rather than feature-specific gameplay rules.

## Suggested workflow

1. Identify the feature and target Minecraft version.
2. Inspect the existing pack, manifest, identifiers, and data before designing changes.
3. Use the smallest relevant skill set; combine domain skills only when a task crosses boundaries.
4. Verify API/module availability before implementation.
5. Make the smallest practical changes and validate references and schemas.
6. Test in a copy or test world on the target version; report runtime testing only if it was actually performed.

## Documentation map

- [Bedrock API versioning](./bedrock-api-versioning.md) explains game, module, and stability versions.
- [Skill development guide](./skill-development-guide.md) defines how to author and maintain `SKILL.md` files.
- [Troubleshooting](./troubleshooting.md) gives diagnostic steps for common pack and script failures.

The repository does not replace official platform documentation. See the [Minecraft Creator documentation](https://learn.microsoft.com/en-us/minecraft/creator/?view=minecraft-bedrock-stable) for authoritative, version-specific references.
