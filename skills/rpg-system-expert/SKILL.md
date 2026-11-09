---
name: rpg-system-expert
description: Design Minecraft Bedrock RPG and progression systems, including stats, levels, classes, abilities, economy, inventory, equipment, and player progression.
---

# RPG System Expert

Design progression systems that fit Bedrock add-on constraints and protect persistent player state.

## Responsibilities

- Health, mana, stamina, and energy systems.
- Levels, experience, classes, skills, and abilities.
- Currency, economy, and progression loops.
- Inventory, equipment, gear, and unlocks.
- Persistent progression data and migration planning.

## Technical rules

- Never assume player progression data can be reset safely during debugging.
- Use version-aware storage and validation for persistent data.
- Separate presentation data from authoritative gameplay state.
- Keep progression modules practical and avoid coupling unrelated systems.
- Preserve existing identifiers, dynamic property keys, and player data schemas.
- Verify all API use against the target Minecraft and module versions. Do not invent APIs or behavior.

## Workflow

1. Define the progression model and target version.
2. List progression fields, including economy and equipment data.
3. Decide what must persist and what can be derived at runtime.
4. Define classes, abilities, cooldown rules, and unlock conditions.
5. Plan validation and migration for existing players.
6. Test progression edge cases, economy loops, and stat limits.

## Error handling

- If rewards and costs do not match, inspect validation and transaction order.
- If progression becomes inconsistent, check persistence and recovery before considering a reset.
- If abilities or cooldowns fail, inspect event timing and state transitions.
- Never reset progression to hide a logic error. A reset is acceptable only as an explicit, documented migration with safeguards.

## Testing checklist

- [ ] Health, mana, stamina, and stat limits are validated.
- [ ] Experience gains, level thresholds, and class unlocks are checked.
- [ ] Economy rules, equipment state, and cooldowns are tested.
- [ ] Persistence is checked across restarts and updates when runtime is available.
- [ ] Multiplayer fairness and state consistency are reviewed.
- [ ] Existing data is preserved or migrated safely.
- [ ] Runtime testing is not claimed unless performed.

## Compatibility considerations

Progression systems often depend on persistent storage. Verify the storage API and module version. Keep schemas and migrations explicit. Ensure client-only displays do not misrepresent authoritative player state. Use the [dynamic-property skill](../dynamic-property-expert/SKILL.md) for storage details and the [API versioning guide](../../docs/bedrock-api-versioning.md) for compatibility checks.

## Response format

Provide the progression design, data model, economy rules, upgrade logic, persistence plan, and test approach. Preserve any existing schema and explain required migrations.
