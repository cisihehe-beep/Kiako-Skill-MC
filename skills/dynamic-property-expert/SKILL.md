---
name: dynamic-property-expert
description: Design, validate, and migrate persistent Minecraft Bedrock data for worlds, entities, and players without damaging existing data. Use for dynamic properties and stored economy or progression state.
---

# Dynamic Property Expert

Design persistent storage that matches the target version, uses a clear schema, and protects existing data. This skill focuses on data design and migration. RPG rules belong to `rpg-system-expert`.

## Responsibilities

- Choose world, entity, or player data scope based on the requirement and available API.
- Define keys, types, schema, validation, unset values, and migration strategy.
- Review reads and writes that may lose or overwrite data.
- Support storage for economy and progression without taking ownership of gameplay design.

## Technical rules

- Verify API methods, signatures, value types, limits, and lifecycle in official documentation for the target `@minecraft/server` version.
- Do not assume old examples or community snippets apply to the target version.
- Distinguish unset values from corrupt, wrong-type, or invalid values. Do not silently replace corrupt data with defaults.
- Use stable, namespaced keys that follow project conventions.
- Avoid storing data that can be derived unless there is a clear reason. Define the source of truth for each value.
- Never delete, reset, or reinitialize saved player data as a general fix.

## Workflow

1. Read the manifest. Identify the game version and `@minecraft/server` dependency. Verify required methods in official documentation.
2. Inventory existing owners, keys, callers, data shapes, and schema versions.
3. Choose the storage scope: world, entity, or player. Explain lifecycle and trade-offs.
4. Define the schema contract: field names, types, validation rules, defaults for new data, and behavior for invalid data.
5. For schema changes, design a staged, idempotent migration. Keep old data recoverable until the new data is validated.
6. Define useful error logging that does not erase data or expose unnecessary information.
7. Plan tests for new data, old data, invalid values, restarts, and pack updates.

## Concrete review example

When reviewing persistent reads and writes, trace the paired operations in the official reference for the target version. Use this audit table; it is not an API signature example.

| Check | Question |
|---|---|
| Owner | Is the data stored on the intended world, entity, or player and read from the same owner? |
| Key | Is the key consistent, unique in the project, and stable across updates? |
| Value | Are type and allowed range checked before use? |
| Unset state | Is an unset value distinguished from valid `0`, `false`, empty text, or malformed data? |
| Update | Is the change safe if called more than once or interrupted? |
| Migration | Can old data be recovered until the migration is verified? |

For balances, check costs, rewards, negative values, allowed ranges, duplicate transactions, and validation order before committing state. Verify every related API operation in official documentation. Do not copy an unverified signature.

## Error handling

- Log enough owner/key context to diagnose failures without overwriting the original value.
- If parsing or validation fails, stop risky changes and provide a recovery or review path.
- Do not silently swallow exceptions or replace invalid data with defaults.
- Do not run destructive migrations without a documented backup or recovery plan.

## Testing checklist

- [ ] Module version and API were verified in official documentation.
- [ ] Storage scope and keys are documented.
- [ ] Unset data is distinct from valid false-like values and invalid data.
- [ ] Old data is preserved and migrations are idempotent.
- [ ] Boundary values, wrong types, and operation failures have safe outcomes.
- [ ] Persistence was tested after restart/update in a copied world when runtime is available.
- [ ] No runtime test is claimed unless it was performed.

## Official references and compatibility

Check the version selector in the [Script API reference](https://learn.microsoft.com/en-us/minecraft/creator/scriptapi/?view=minecraft-bedrock-stable), especially [`Entity`](https://learn.microsoft.com/en-us/minecraft/creator/scriptapi/minecraft/server/entity?view=minecraft-bedrock-stable) and [`World`](https://learn.microsoft.com/en-us/minecraft/creator/scriptapi/minecraft/server/world?view=minecraft-bedrock-stable), and the [repository versioning guide](../../docs/bedrock-api-versioning.md). A class reference does not guarantee that every member is available in every version.

## Response format

Explain storage scope, schema and keys, validation, error behavior, migration, verified API version, and tests. Mark assumptions and unverified details.
