# Troubleshooting guide

Use a repeatable diagnosis: capture the exact error, reproduction steps, game version, platform, pack versions, and relevant manifest/module dependencies. Check Minecraft's Content Log and script output where available. Change one likely cause at a time, preserve a copy of the world, and do not reset player data as a generic repair.

## Script fails to load

1. Confirm the Behavior Pack is enabled and inspect its `manifest.json` for valid JSON, a script module, the correct entry-point path, and declared module dependencies.
2. Check that the entry-point file exists with the exact path and capitalization used by the manifest.
3. Compare the requested `@minecraft/server` and other module versions with the target game runtime and official module references.
4. Check imports for misspelled module names or APIs unavailable in that version. Do not guess replacements; verify them in official documentation.
5. Read the first load error in Content Log/script output; later errors may be cascading consequences.
6. Test on a copied world with only the required packs enabled to isolate conflicts.

## UI form fails to open or respond

1. Verify the `@minecraft/server-ui` dependency is declared and supported by the target runtime.
2. Check the first rejection/error and confirm the code handles the documented form result and cancellation path for that module version.
3. Ensure the player is in a state where the form can be shown; inspect whether another UI or interaction is already active and whether the script attempts to show the form at an invalid lifecycle moment.
4. Validate that input/selection handling checks for cancellation, missing values, and stale state before changing player or world data.
5. Reduce the reproduction to one player and one form, then test multiple players separately.
6. Verify all class, method, and result semantics against the official [`@minecraft/server-ui` reference](https://learn.microsoft.com/en-us/minecraft/creator/scriptapi/minecraft/server-ui/minecraft-server-ui?view=minecraft-bedrock-stable); do not infer availability from an example targeting another version.

## Dynamic Properties missing, invalid, or not persisting

1. Identify the exact owner and scope (player, entity, or world) and verify that the code reads and writes the same owner/key.
2. Inspect runtime errors, key spelling, value type, and initialization timing. Check the API documentation for the target module version before assuming registration or lifecycle behavior.
3. Distinguish an unset value from a malformed or unexpected value. Do not silently replace corrupt data with a default.
4. Reproduce in a copy of the world and verify persistence after leaving/reloading as appropriate.
5. If the stored schema changed, write a guarded, idempotent migration and retain recoverable old data until validation is complete.
6. Never clear all properties or reset player progression as a troubleshooting shortcut.

## Entity, block, or item is missing or behaves incorrectly

1. Confirm the relevant BP/RP is enabled and its manifest dependencies are resolved.
2. Validate JSON syntax and version-specific schema using the official Creator reference for the target version.
3. Trace the namespaced identifier from definition through every reference (spawn rule, loot, recipe, texture, geometry, animation, or script) and check spelling and path capitalization.
4. For entities, inspect spawn conditions, component/event references, and client/server asset links.
5. For blocks/items, inspect BP/RP pairing, asset mappings, placement/use behavior, and recipe/loot output identifiers.
6. Isolate the failing definition in a test world and read Content Log messages. Do not change published identifiers without a compatibility or migration plan.

## Watchdog warnings, freezes, or poor performance

1. Record when the issue occurs and the player/entity/load conditions that reproduce it.
2. Inspect loops, repeated scans, expensive work per tick, unbounded scheduling, duplicate event subscriptions, repeated form creation, and growing retained state.
3. Use available profiling/logging tools and compare a baseline with one targeted change; do not claim improvement without measurement.
4. Reduce scope or frequency of repeated work where correct, and ensure event subscriptions and scheduled tasks do not accumulate on reload or repeated initialization.
5. Re-test under realistic player/entity counts and verify gameplay state remains correct.
6. Treat watchdog messages as evidence of workload or timing problems; do not suppress them or increase limits as a substitute for finding the cause. Verify any scheduling or profiling API against the target version.

## Manifest and dependency failures

1. Parse each relevant `manifest.json` and inspect pack UUIDs, module UUIDs, versions, module types, script entry paths, and `min_engine_version`.
2. Confirm BP/RP dependencies reference the intended pack UUID and version.
3. Confirm Script API dependencies use exact module names and version numbers supported by the target runtime; game version, pack version, and module version are separate values.
4. Remove or correct only dependencies that are proven invalid; do not regenerate existing UUIDs as a generic fix.
5. Review the official [manifest reference](https://learn.microsoft.com/en-us/minecraft/creator/reference/content/addonsreference/packmanifest?view=minecraft-bedrock-stable) and [Script API version guide](./bedrock-api-versioning.md).
6. Re-enable packs in a test world and inspect Content Log for unresolved dependency or module-load errors.

## Information to include when asking for help

- Full first error and relevant surrounding log lines.
- Minecraft version, platform, and whether it is stable or preview.
- Pack manifests and declared API module versions (redact private information if needed).
- Minimal reproduction steps and whether the issue occurs in a clean test world.
- Recent changes and whether the issue began after a version or pack update.

Related guides: [architecture](./architecture.md), [API versioning](./bedrock-api-versioning.md), and [skill development](./skill-development-guide.md).
