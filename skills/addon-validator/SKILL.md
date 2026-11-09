---
name: addon-validator
description: Audit Minecraft Bedrock add-on manifests, JSON, UUIDs, identifiers, dependencies, assets, and BP/RP references. Use when checking pack integrity or reviewing changes before release.
---

# Add-on Validator

Perform traceable checks and prioritize reproducible findings. This skill owns pack-wide validation. Delegate deep runtime diagnosis to `javascript-debugger` or a domain skill when needed.

## Responsibilities

- Check pack structure, manifests, UUIDs, versions, dependencies, and script entry points.
- Validate JSON and cross-file references against the target version.
- Find missing, duplicated, or inconsistent identifiers, assets, and dependencies.
- Report severity, evidence, impact, and minimal fixes without risking data loss.

## Technical rules

- Identify the target Minecraft Bedrock and module versions before judging compatibility.
- Treat JSON syntax, schema validity, and runtime behavior as separate checks. Valid JSON may still be invalid for the engine.
- Verify `format_version` and components against official Creator documentation. Do not assume they work across versions.
- Do not replace UUIDs, identifiers, namespaces, or dynamic properties as a generic fix.
- Separate confirmed errors, possible risks, and issues that need runtime testing.

## Audit workflow

1. Map BP/RP folders and relevant manifests before editing.
2. Parse each relevant manifest and JSON file. If no parser is available, state that syntax was not checked automatically.
3. Check pack/module UUIDs, versions, minimum engine, module types, entry points, and BP/RP/API dependencies.
4. Trace defined and referenced identifiers. Find missing definitions, duplicates, spelling differences, and references without a matching target.
5. Compare asset paths and capitalization with files that exist. Check textures, geometry, animation, sound, loot, recipes, and localization where relevant.
6. Verify features, APIs, and formats against Creator documentation for the target version.
7. Rank findings by severity. Include evidence and a specific minimal fix.
8. Repeat available checks after fixes. State which runtime checks remain.

## Reference audit example

Use a table to track references. This is an audit method, not a JSON schema example.

| Source | Reference | Target to check |
|---|---|---|
| BP manifest | Pack UUID dependency, script entry, module dependency | Matching pack UUID/version and existing entry file |
| Content definition | Entity, item, or block identifier | Every file that uses the identifier |
| Recipe or loot | Input and output identifiers | Matching item or block definitions |
| RP | Texture, geometry, or animation reference | Existing file or definition with matching path and name |

Use official documentation to determine valid fields and paths for the target format.

## Report findings

For each issue, state:

- **Severity:** blocker, high, medium, or low, with impact.
- **Location:** file and line, or JSON pointer when available.
- **Evidence:** log message, mismatched reference, or applicable official requirement.
- **Impact:** load failure, missing content, compatibility issue, or data risk.
- **Fix:** smallest appropriate change and any migration risk.

Do not call an API or schema invalid based only on memory. If the target version or official documentation is unavailable, mark the issue as unverified.

## Validation checklist

- [ ] Relevant manifests and JSON files were checked for syntax.
- [ ] Schema, `format_version`, module/API, and minimum engine were checked for the target.
- [ ] UUIDs and dependencies match. No UUID was changed without reason.
- [ ] Identifier references resolve and are spelled consistently.
- [ ] Asset paths and capitalization match existing files.
- [ ] Findings distinguish facts, risks, and runtime test needs.
- [ ] No fix resets player data or breaks public identifiers.

## References

Use the [versioning guide](../../docs/bedrock-api-versioning.md), official [`manifest.json` reference](https://learn.microsoft.com/en-us/minecraft/creator/reference/content/addonsreference/packmanifest?view=minecraft-bedrock-stable), [Minecraft Creator documentation](https://learn.microsoft.com/en-us/minecraft/creator/?view=minecraft-bedrock-stable), and [Script API reference](https://learn.microsoft.com/en-us/minecraft/creator/scriptapi/?view=minecraft-bedrock-stable). Select documentation for the target version.
