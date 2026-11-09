# Bedrock API versioning guide

Bedrock add-on compatibility involves more than one version number. A project may target a Minecraft Bedrock game version, declare a minimum engine version for pack content, and request separate versions of Script API modules. Treat those values as related constraints, not interchangeable labels.

## The versions to track

### Minecraft Bedrock game version

Record the actual game/runtime version used for development and testing, and the supported version range if the pack targets more than one release. A feature available in a newer release may not exist in an older runtime.

### `@minecraft/server` and `@minecraft/server-ui`

These are separately versioned Script API modules. The version requested for `@minecraft/server` is not the Minecraft game version, and `@minecraft/server-ui` has its own published versions and compatibility information. Check each module's official reference and release/version information. Do not copy a module version from an unrelated example or assume two module versions advance together.

### Stable, beta, preview, and experimental

- **Stable API**: documented as stable for the relevant module version. Still confirm the target runtime supports that module version.
- **Beta API**: a prerelease API surface that may change. It may require a preview runtime, a beta module version, or a world experiment; follow the requirements stated in the current official documentation for that API.
- **Preview**: a Minecraft distribution/runtime channel. Preview availability is not by itself proof that an API is stable or enabled.
- **Experimental feature**: a game/world feature gated by an experiment or configuration. This is distinct from a module version; verify both the feature's requirements and the API's status.

Do not treat these labels as synonyms. Report uncertainty when current documentation does not clearly establish a feature's status.

## Inspect `manifest.json`

Read the Behavior Pack manifest before proposing script changes. Check at least:

- `header.uuid` and each module UUID are valid and unique within the project; do not casually regenerate existing UUIDs.
- `header.version` and module `version` describe pack/module revisions, not Script API package versions.
- `header.min_engine_version` expresses the minimum engine requirement for pack content; it is not a substitute for checking script module compatibility.
- `modules` includes the intended script module and correct entry point where scripts are used.
- `dependencies` declares the exact module names and versions needed, such as `@minecraft/server` and, when used, `@minecraft/server-ui`.
- BP/RP dependency UUIDs and versions match the packs they refer to.
- Any experiments required by content are documented and enabled only when necessary.

Do not invent a universally valid manifest snippet: required fields and supported versions depend on current Creator documentation and the project's target versions. Preserve project UUIDs and identifiers during repair.

## Verify APIs using official references

For each API, class, method, event, component, or form used:

1. Identify its module and the project's declared module version.
2. Open the official module reference and inspect the member's description and availability/version information.
3. Check official scripting guides, release notes, or migration notes for lifecycle, stability, and breaking changes.
4. Confirm the target Minecraft runtime can provide the declared module version.
5. If the feature requires preview or experiments, record that requirement and provide a stable alternative only if one is documented.
6. If official references do not establish availability, mark the API as unverified instead of guessing.

Primary references:

- [Minecraft Creator documentation](https://learn.microsoft.com/en-us/minecraft/creator/?view=minecraft-bedrock-stable)
- [Script API reference index](https://learn.microsoft.com/en-us/minecraft/creator/scriptapi/?view=minecraft-bedrock-stable)
- [`@minecraft/server` module reference](https://learn.microsoft.com/en-us/minecraft/creator/scriptapi/minecraft/server/minecraft-server?view=minecraft-bedrock-stable)
- [`@minecraft/server-ui` module reference](https://learn.microsoft.com/en-us/minecraft/creator/scriptapi/minecraft/server-ui/minecraft-server-ui?view=minecraft-bedrock-stable)
- [Add-ons `manifest.json` reference](https://learn.microsoft.com/en-us/minecraft/creator/reference/content/addonsreference/packmanifest?view=minecraft-bedrock-stable)
- [Scripting V2 overview](https://learn.microsoft.com/en-us/minecraft/creator/documents/scripting/v2-overview?view=minecraft-bedrock-stable)

Use the version selector and module-version information on the official pages. These references can change as Minecraft documentation is updated.

## Cross-version compatibility strategy

1. Establish the oldest and newest game versions the pack intends to support.
2. List the required module versions and feature requirements for each supported runtime.
3. Prefer the lowest stable module/API surface that provides the feature across the declared range.
4. If a capability is unavailable in older versions, choose a documented fallback, explicitly narrow the supported range, or maintain clearly separated implementation paths only when justified.
5. Avoid silently changing identifiers, manifest UUIDs, persistent property keys, or stored data schemas to accommodate a version change.
6. Validate pack files and imports against the target versions, then test in a copied/test world on each supported runtime where feasible.
7. Document the tested range and distinguish static checks from actual in-game tests.

## Checklist

- [ ] Game/runtime target and supported range are stated.
- [ ] `min_engine_version` and pack/module versions are understood separately.
- [ ] Every Script API module dependency is explicitly checked.
- [ ] API members are present in official references for the chosen module version.
- [ ] Stable, beta, preview, and experimental requirements are distinguished.
- [ ] Existing UUIDs, identifiers, and persistent player data remain intact.
- [ ] Cross-version limitations and testing evidence are reported.

Related guides: [architecture](./architecture.md), [skill development](./skill-development-guide.md), and [troubleshooting](./troubleshooting.md).
