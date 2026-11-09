# Bedrock API versioning guide

Minecraft Bedrock add-on compatibility involves several version values. A project may target a Minecraft game version, set a minimum engine version for pack content, and request separate Script API module versions. These values are related, but they are not interchangeable.

## Versions to track

### Minecraft Bedrock game version

Record the game/runtime version used for development and testing. If the pack supports a range of releases, record the oldest and newest supported versions. A feature available in a newer release may not exist in an older runtime.

### `@minecraft/server` and `@minecraft/server-ui`

These are separately versioned Script API modules. Their versions are not Minecraft game versions, and the two module versions do not necessarily advance together. Check each module's official reference and version information. Do not copy a module version from an unrelated example.

### Stable, beta, preview, and experimental

- **Stable API** is documented as stable for a specific module version. Confirm that the target runtime supports that module version.
- **Beta API** is a prerelease API surface that may change. Follow the documented module, runtime, and world requirements for the feature.
- **Preview** describes a Minecraft distribution/runtime channel. Preview availability alone does not prove that an API is stable or enabled.
- **Experimental feature** is a game or world feature gated by an experiment or configuration. This is separate from the API module version. Check both sets of requirements.

Do not treat these labels as synonyms. If current documentation does not establish a feature's status, mark it as unverified.

## Check `manifest.json`

Review the Behavior Pack manifest before changing scripts. Check the following:

- `header.uuid` and module UUIDs are valid and unique within the project. Do not regenerate existing UUIDs without a clear reason.
- `header.version` and module `version` are pack/module revisions. They are not Script API versions.
- `header.min_engine_version` sets a minimum engine requirement for pack content. It does not replace Script API compatibility checks.
- `modules` contains the intended script module and entry point when scripts are used.
- `dependencies` declares the required module names and versions, such as `@minecraft/server` and, when used, `@minecraft/server-ui`.
- BP/RP dependencies refer to the correct pack UUIDs and versions.
- Required experiments are documented and enabled only when needed.

Use the official manifest reference for required fields and supported versions. Do not assume one manifest example applies to every target.

## Verify APIs in official documentation

For each API, class, method, event, component, or form:

1. Identify its module and the version declared by the project.
2. Open the official module reference. Check the member description and version information.
3. Check official scripting guides, release notes, or migration notes for lifecycle, stability, and breaking changes.
4. Confirm that the target runtime can provide the declared module version.
5. Record preview or experiment requirements. Suggest a stable alternative only when it is documented.
6. If official references do not establish availability, mark the API as unverified instead of guessing.

Official references:

- [Minecraft Creator documentation](https://learn.microsoft.com/en-us/minecraft/creator/?view=minecraft-bedrock-stable)
- [Script API reference index](https://learn.microsoft.com/en-us/minecraft/creator/scriptapi/?view=minecraft-bedrock-stable)
- [`@minecraft/server` module reference](https://learn.microsoft.com/en-us/minecraft/creator/scriptapi/minecraft/server/minecraft-server?view=minecraft-bedrock-stable)
- [`@minecraft/server-ui` module reference](https://learn.microsoft.com/en-us/minecraft/creator/scriptapi/minecraft/server-ui/minecraft-server-ui?view=minecraft-bedrock-stable)
- [Add-ons `manifest.json` reference](https://learn.microsoft.com/en-us/minecraft/creator/reference/content/addonsreference/packmanifest?view=minecraft-bedrock-stable)
- [Scripting V2 overview](https://learn.microsoft.com/en-us/minecraft/creator/documents/scripting/v2-overview?view=minecraft-bedrock-stable)

Use the version selector and module-version information on each official page. Documentation can change over time.

## Cross-version compatibility

1. Define the oldest and newest game versions the pack supports.
2. List the required module versions and feature requirements for each supported runtime.
3. Prefer a stable API surface supported across the declared version range.
4. If an older version lacks a feature, use a documented fallback, narrow the supported range, or maintain separate paths only when justified.
5. Do not silently change identifiers, UUIDs, persistent property keys, or stored data schemas to handle version differences.
6. Validate pack files and imports against target versions. Test in a copy or test world on each supported runtime when possible.
7. Document the supported range and separate static checks from in-game test results.

## Checklist

- [ ] The target game version and supported range are stated.
- [ ] `min_engine_version`, pack versions, and module versions are treated separately.
- [ ] Each Script API module dependency is checked.
- [ ] API members are present in official references for the chosen module version.
- [ ] Stable, beta, preview, and experimental requirements are distinguished.
- [ ] Existing UUIDs, identifiers, and player data are preserved.
- [ ] Compatibility limits and test evidence are reported.

Related guides: [architecture](./architecture.md), [skill development](./skill-development-guide.md), and [troubleshooting](./troubleshooting.md).
