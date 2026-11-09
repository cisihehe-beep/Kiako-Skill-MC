# Architecture overview

This repository is organized as a collection of focused, version-aware Bedrock development skills. Each skill addresses a bounded domain so an AI assistant can reason about a problem without mixing unrelated concerns.

## Design goals

- Keep each skill specific and usable in isolation.
- Avoid fabricating unsupported APIs or undocumented behavior.
- Favor correctness and compatibility over broad abstraction.
- Keep player data, pack identifiers, and entity definitions stable.
- Make architecture trade-offs explicit.

## Core layers

### 1. Pack and manifest layer

This includes Behavior Pack and Resource Pack definitions, pack structure, versions, identifiers, dependencies, and asset references.

Responsibilities:
- `addon-architect`
- `addon-validator`
- `bedrock-api-expert`

### 2. Gameplay and logic layer

This includes script-driven behavior, entity logic, custom blocks/items, world interaction, and stateful systems.

Responsibilities:
- `entity-expert`
- `block-item-expert`
- `javascript-debugger`
- `performance-optimizer`

### 3. Data and progression layer

This includes persistent state, economy, progression, player metadata, and experience systems.

Responsibilities:
- `dynamic-property-expert`
- `rpg-system-expert`

### 4. User experience layer

This includes forms, menus, instructions, input flows, and UI state.

Responsibilities:
- `bedrock-ui-expert`

## Cross-cutting principles

- Verify version compatibility before adding API usage.
- Prefer official documentation and project evidence over memory.
- Use minimal changes that fix the root cause.
- Keep identifiers and UUIDs stable across pack revisions.
- Document migration and rollback paths for persistent data changes.

## Skill selection guidance

Use the smallest relevant skill for the task:

- planning/architecture -> `addon-architect`
- validation -> `addon-validator`
- API usage -> `bedrock-api-expert`
- forms and UI -> `bedrock-ui-expert`
- entities -> `entity-expert`
- blocks/items -> `block-item-expert`
- progression/economy -> `rpg-system-expert`
- persistence/data -> `dynamic-property-expert`
- debugging -> `javascript-debugger`
- performance -> `performance-optimizer`

## Repository workflow

1. Start with architecture if the task is ambiguous.
2. Validate the pack and manifest if the project already exists.
3. Confirm the exact Bedrock version and module requirements.
4. Implement the minimum required logic or assets.
5. Validate behavior in a test world.
6. Profile performance only when necessary or when runtime risk is identified.

## Limitations

This repository does not replace official Bedrock documentation. It makes those principles easier to apply in AI-assisted workflows, but it still depends on the target version and the actual project state.

Related docs:
- [Bedrock API versioning guide](./bedrock-api-versioning.md)
- [Skill development guide](./skill-development-guide.md)
- [Troubleshooting guide](./troubleshooting.md)
