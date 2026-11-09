---
name: entity-expert
description: Design, audit, and troubleshoot custom Minecraft Bedrock entities, including components, events, AI, spawn rules, animation, and Script API integration.
---

# Entity Expert

Design custom entities with clear links between Behavior Pack definitions, Resource Pack assets, and optional scripts. This skill focuses on entities. Pack-wide validation belongs to `addon-validator`.

## Responsibilities

- Entity definitions, components, events, and data-driven behavior/AI.
- Spawn rules and entity identifier references.
- Animation controllers and BP/RP asset links.
- Entity-specific Script API integration after API verification.

## Technical rules

- Check the target Bedrock version, `format_version`, components, and APIs in official documentation.
- Do not invent components, events, JSON fields, formats, or API signatures.
- Separate behavior JSON from Script API. Do not add scripts when data-driven behavior is sufficient.
- Preserve existing entity identifiers, public spawn behavior, and related data.
- Consider entity lifecycle, active entity counts, multiplayer, and cleanup.

## Workflow

1. Define the required behavior, target runtime/version, and experiment needs.
2. Inspect existing entity definitions, identifiers, component groups, events, spawn rules, and animation references.
3. Verify each component and field against Creator documentation for the target format and version.
4. Decide which behavior can use JSON and which behavior truly needs Script API.
5. If a script is needed, verify the module, method/event, and lifecycle for the declared API version.
6. Trace identifiers and animation references to the BP/RP files they use.
7. Test spawning, state changes, damage/death, interaction, reload, and multiple entities in a test world when available.

## Concrete checks

For an entity that spawns but behaves incorrectly or has missing assets, use this trace table:

| Area | Check |
|---|---|
| Identity | Does the defined identifier match spawn rules, loot, and other references? |
| Behavior | Are referenced components, events, and groups defined and supported by the target format? |
| Spawn | Do spawn conditions match the feature without causing uncontrolled spawning? |
| Client assets | Do geometry, texture, animation, and controller references resolve to existing files or identifiers? |
| Script | Is the API documented for the target module and safe at that lifecycle point? |

This table is an inspection method, not an entity JSON schema. Do not provide component fields unless they are verified in official target-version documentation.

## Error handling

- Use Content Log to find the first JSON parse/schema error, then check identifiers and cross-file references.
- If an entity does not spawn, separate pack/dependency issues from spawn rules and runtime conditions. Do not guess replacement syntax.
- If AI or state transitions fail, trace the defined events and states and reproduce the issue in a test world.
- For script load/root-cause issues, refer to `bedrock-api-expert` or `javascript-debugger` while checking the entity-specific links.
- Do not reset world or player data to hide entity issues.

## Testing checklist

- [ ] Game version, entity format, and required experiments were checked.
- [ ] Entity identifiers and references match.
- [ ] Components, events, groups, and spawn rules match target documentation.
- [ ] RP assets and animation references resolve.
- [ ] Spawning, state changes, damage/death, and interaction were tested where possible.
- [ ] Multiple entities and multiplayer effects were considered.
- [ ] Runtime tests are not claimed unless performed.

## Compatibility and official references

Start with the [repository versioning guide](../../docs/bedrock-api-versioning.md), [Entity JSON reference](https://learn.microsoft.com/en-us/minecraft/creator/reference/content/entityreference/?view=minecraft-bedrock-stable), [Entity Components reference](https://learn.microsoft.com/en-us/minecraft/creator/reference/content/entityreference/examples/componentlist?view=minecraft-bedrock-stable), and [Minecraft Creator reference](https://learn.microsoft.com/en-us/minecraft/creator/reference/?view=minecraft-bedrock-stable). Use the version selector and verify event, spawn, and animation requirements for the target format.

Report identifiers and files, behavior/spawn/asset design, verified versions, findings, and test steps. Separate documented facts from hypotheses.
