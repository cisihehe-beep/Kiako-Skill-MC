# Skill development guide

This guide describes how to create and maintain focused `SKILL.md` files in Kiako-Skill-MC. A skill should help an AI coding agent perform a defined class of Bedrock development tasks without pretending to replace project inspection or official API documentation.

## Before creating or changing a skill

1. Inspect the current repository structure, README, and related skill files.
2. Identify the intended user task and the skill's unique responsibility.
3. Check whether an existing skill already owns that topic. Extend it instead of creating a near-duplicate when practical.
4. Preserve useful existing guidance; avoid broad rewrites without a clear reason.
5. Identify technical claims that require version-specific evidence and link official documentation when relevant.

## Required file and frontmatter

Use one directory and one `SKILL.md` file per skill:

```text
skills/<unique-skill-name>/SKILL.md
```

Every file must start with valid YAML frontmatter delimited by `---`, and include a unique lowercase, hyphenated `name` plus a concise `description` that says what the skill does and when to use it:

```yaml
---
name: example-skill
description: Helps with a clearly bounded task and says when to use this skill.
---
```

Keep frontmatter values valid YAML. Avoid unescaped YAML punctuation in plain scalars; quote a value if needed. The `name` should match its directory name. Descriptions should be specific enough to distinguish the skill from the others.

## Recommended content

Include the following sections, using headings appropriate to the domain:

- **Purpose and responsibilities:** what the skill owns and what it does not own.
- **Technical rules:** version verification, data safety, identifiers, and limits relevant to the domain.
- **Workflow:** concrete steps from gathering context through implementation or diagnosis.
- **Error handling:** how to diagnose failures without hiding errors or causing data loss.
- **Testing checklist:** static checks and runtime checks that apply to the task.
- **Compatibility considerations:** game/module versions, stable versus prerelease/experimental requirements, and uncertainty handling.
- **Final response expectations:** what evidence, assumptions, files, and next steps to report.

A skill may combine sections where that improves clarity, but it should cover these responsibilities in substance.

## Keep skill boundaries clear

Use the following ownership as a guide:

- `addon-architect`: overall feature decomposition and architecture.
- `addon-validator`: pack-wide consistency and structural validation.
- `bedrock-api-expert`: Script API verification and module compatibility.
- `bedrock-ui-expert`: forms and UI interaction flow.
- `block-item-expert`: block/item content and its assets/references.
- `dynamic-property-expert`: persistence schema, validation, and migrations.
- `entity-expert`: entity definitions and behavior.
- `javascript-debugger`: JavaScript/runtime root-cause analysis.
- `performance-optimizer`: measured runtime performance and resource use.
- `rpg-system-expert`: progression and economy rules.

Cross-cutting requirements such as checking versions and protecting player data may appear in multiple skills; that repetition is intentional. Avoid duplicating detailed procedures owned by another specialist. Refer to the relevant skill or documentation instead.

## Technical accuracy and references

- Never invent API names, signatures, JSON schemas, or runtime behavior.
- Verify exact-version claims against Microsoft Learn / Minecraft Creator documentation.
- Distinguish stable, beta, preview, and experimental status; do not present preview information as a stable guarantee.
- Link to authoritative references when they directly support technical guidance. Avoid link lists that do not serve the skill's purpose.
- Preserve UUIDs, identifiers, and persistent data; describe migration when a change requires it.
- Do not claim code or gameplay was tested unless the test was actually run.

## Markdown and repository maintenance

- Use clear heading hierarchy, fenced code blocks with language labels where appropriate, and concise lists.
- Use relative links for repository documentation and verify each target exists.
- Update README skill descriptions and the structure tree when adding, renaming, or moving files.
- Keep `docs/architecture.md`, `docs/bedrock-api-versioning.md`, and `docs/troubleshooting.md` consistent with actual content and scope.
- Do not create empty placeholder files or delete existing skills as a shortcut.

## Review checklist

Before committing a skill change, verify:

- [ ] Frontmatter parses as YAML and contains a unique name and useful description.
- [ ] Name, folder path, README entry, and actual responsibility agree.
- [ ] Required responsibilities, rules, workflow, error handling, testing, and compatibility are covered.
- [ ] No unsupported APIs or false version guarantees are asserted.
- [ ] Instructions do not contradict other skills or project principles.
- [ ] Useful existing content and data-safety guidance are preserved.
- [ ] Internal links resolve and Markdown is readable.
- [ ] Validation claims accurately describe what was checked.

Related guides: [architecture](./architecture.md), [API versioning](./bedrock-api-versioning.md), and [troubleshooting](./troubleshooting.md).
