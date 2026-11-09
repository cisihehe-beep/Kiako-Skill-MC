# Troubleshooting guide

Use a repeatable process. Record the exact error, reproduction steps, game version, platform, pack versions, and relevant manifest dependencies. Check Minecraft's Content Log and script output where available. Change one likely cause at a time. Test on a copy of the world. Do not reset player data as a general fix.

## Script does not load

1. Confirm that the Behavior Pack is enabled.
2. Check `manifest.json` for valid JSON, a script module, the correct entry-point path, and declared module dependencies.
3. Confirm that the entry-point file exists at the exact path and capitalization used in the manifest.
4. Compare the requested `@minecraft/server` and other module versions with the target runtime and official module references.
5. Check imports for misspelled module names or APIs unavailable in that version. Verify any replacement in official documentation.
6. Read the first load error in Content Log or script output. Later errors may be side effects of the first one.
7. Reproduce the issue in a copied world with only the required packs enabled.

## UI form does not open or respond

1. Confirm that the `@minecraft/server-ui` dependency is declared and supported by the target runtime.
2. Read the first error or rejection. Check form results and cancellation handling against documentation for the declared module version.
3. Check whether another UI or interaction is active and whether the form is shown at a valid point in the script lifecycle.
4. Validate the response before changing player or world data. Handle cancellation, missing values, and stale state.
5. Reproduce with one player and one form. Then test with multiple players.
6. Verify class, method, and result behavior in the official [`@minecraft/server-ui` reference](https://learn.microsoft.com/en-us/minecraft/creator/scriptapi/minecraft/server-ui/minecraft-server-ui?view=minecraft-bedrock-stable). Do not assume examples for another version apply.

## Dynamic properties are missing, invalid, or not persistent

1. Identify the owner and scope: world, entity, or player. Confirm reads and writes use the same owner and key.
2. Check runtime errors, key spelling, value type, and initialization timing. Verify API behavior for the target module version.
3. Distinguish an unset value from malformed or unexpected data. Do not silently replace invalid data with a default.
4. Reproduce in a copy of the world. Check persistence after leaving and reloading where appropriate.
5. If the schema changed, use a guarded, idempotent migration. Keep the old data recoverable until the new data is validated.
6. Do not clear properties or reset player progression as a troubleshooting shortcut.

## Entity, block, or item is missing or behaves incorrectly

1. Confirm that the relevant BP/RP is enabled and pack dependencies resolve.
2. Validate JSON syntax and check the schema for the target version in official Creator documentation.
3. Trace each namespaced identifier from its definition to every reference, including spawn rules, loot, recipes, textures, geometry, animation, and scripts.
4. Check spelling and path capitalization.
5. For entities, inspect spawn conditions, component/event references, and client/server asset links.
6. For blocks and items, inspect BP/RP pairing, asset mappings, placement/use behavior, and recipe/loot output identifiers.
7. Isolate the definition in a test world and read Content Log. Do not change published identifiers without a compatibility or migration plan.

## Watchdog warnings, freezes, or poor performance

1. Record when the issue occurs and the player/entity/load conditions that reproduce it.
2. Inspect loops, repeated scans, expensive per-tick work, unbounded scheduling, duplicate event subscriptions, repeated form creation, and growing retained state.
3. Use available profiling or logging tools. Compare a baseline with one targeted change. Do not claim improvement without measurement.
4. Reduce the scope or frequency of repeated work when this preserves correct behavior. Check that subscriptions and scheduled tasks do not accumulate during repeated initialization.
5. Test under realistic player and entity counts. Confirm cleanup and gameplay state.
6. Do not suppress watchdog warnings or increase limits instead of finding the cause. Verify scheduling or profiling APIs for the target version.

## Manifest or dependency errors

1. Parse each relevant `manifest.json`. Check pack and module UUIDs, versions, module types, script entry paths, and `min_engine_version`.
2. Confirm that BP/RP dependencies reference the intended pack UUID and version.
3. Confirm that Script API dependencies use exact module names and versions supported by the target runtime. Game, pack, and module versions are separate values.
4. Correct only dependencies proven invalid. Do not regenerate existing UUIDs as a general fix.
5. Review the official [manifest reference](https://learn.microsoft.com/en-us/minecraft/creator/reference/content/addonsreference/packmanifest?view=minecraft-bedrock-stable) and the [API versioning guide](./bedrock-api-versioning.md).
6. Re-enable packs in a test world and check Content Log for dependency or module-load errors.

## Details to include when requesting help

- The first full error and relevant surrounding log lines.
- Minecraft version, platform, and stable or preview channel.
- Relevant pack manifests and declared API module versions. Redact private information if needed.
- Minimal reproduction steps and whether the issue occurs in a clean test world.
- Recent changes, including game or pack updates.

Related guides: [architecture](./architecture.md), [API versioning](./bedrock-api-versioning.md), and [skill development](./skill-development-guide.md).
