---
name: block-item-expert
description: Design and audit custom Minecraft Bedrock blocks and items, including interactions, recipes, loot, identifiers, textures, and BP/RP compatibility. Use for block or item content work.
---

# Block and Item Expert

Design and review Bedrock block and item content. Preserve BP/RP links, identifier stability, and version compatibility. Pack-wide validation belongs to `addon-validator`.

## Responsibilities

- Custom block and item definitions and interactions.
- BP/RP references, identifiers, textures, geometry, and asset mappings.
- Recipes and loot that use or produce the content.
- Feature compatibility for the target Bedrock version.

## Technical rules

- Verify the game version, module dependencies when Script API is used, and official JSON format before giving schema examples.
- Do not invent components, fields, `format_version`, events, methods, or asset mappings.
- Do not change public identifiers or remove old references without a compatibility plan.
- Separate BP definitions, RP assets, and script behavior. Add script only when needed.
- Check asset paths and capitalization against the actual project files.

## Workflow

1. Identify the requested behavior, target version, and whether the work uses BP, RP, or both.
2. Inspect existing manifests, namespaces, identifiers, definitions, and asset naming.
3. Verify required formats and components in official Creator documentation for the target version.
4. Trace references from each definition to identifiers, texture/model mappings, recipes, loot, and interactions.
5. Make the smallest change that follows the project's existing structure.
6. Validate JSON syntax and references. Test in a target-version world when available.

## Concrete checks

When a block or item is missing or cannot be used:

- Compare identifiers in BP definitions with identifiers used by recipes, loot, or scripts.
- Compare texture keys referenced by content with RP mappings and existing image files.
- Check directory and file capitalization. Confirm that dependent BP and RP packs are enabled.
- For Script API interactions, verify the event, component, and signature for the declared module version.
- For recipes and loot, verify fields and format against official documentation for the target version.

These are inspection steps, not JSON schema or API examples.

## Error handling

- Start with Content Log, pack status, JSON parsing, identifiers, and asset references.
- Separate pack-definition errors from Script API errors. Verify API claims against the target-version documentation.
- Trace recipe and loot inputs/outputs to the correct definitions. Check the official schema for the target format.
- Do not change identifiers or delete player data as a generic fix.

## Testing checklist

- [ ] Target game version and content format are known.
- [ ] JSON syntax and target schema/version were checked separately.
- [ ] Identifiers and references are consistent.
- [ ] Asset mappings, paths, files, and capitalization match.
- [ ] Changed recipes, loot, placement, and use behavior were tested where possible.
- [ ] BP/RP dependencies and pack activation were checked.
- [ ] Runtime tests are reported only if performed.

## Compatibility and references

See the [repository versioning guide](../../docs/bedrock-api-versioning.md), [Minecraft Creator documentation](https://learn.microsoft.com/en-us/minecraft/creator/?view=minecraft-bedrock-stable), [custom items guide](https://learn.microsoft.com/en-us/minecraft/creator/documents/addcustomitems?view=minecraft-bedrock-stable), [custom recipes guide](https://learn.microsoft.com/en-us/minecraft/creator/documents/how_to_add_a_custom_recipe?view=minecraft-bedrock-stable), and [resource packs guide](https://learn.microsoft.com/en-us/minecraft/creator/documents/resource_packs?view=minecraft-bedrock-stable). Find the official block and loot references for the target version before relying on specific fields or formats.

Report affected files, identifier and asset links, verified version/format, validation steps, and test cases. Mark unverified schemas or feature support clearly.
