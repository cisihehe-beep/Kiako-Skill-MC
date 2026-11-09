# Skill development guide

This guide explains how to create and maintain focused `SKILL.md` files in Kiako-Skill-MC. A skill should help an AI coding agent with a defined Bedrock development task. It does not replace project inspection or official API documentation.

## Before editing a skill

1. Read the relevant existing skills and repository documentation.
2. Define the task and the skill's unique responsibility.
3. Check whether an existing skill already owns the topic. Extend it instead of creating a near-duplicate when practical.
4. Preserve useful guidance. Avoid broad rewrites without a clear reason.
5. Verify version-specific technical claims and link official documentation when useful.

## File path and frontmatter

Use one directory and one `SKILL.md` file per skill:

```text
skills/<unique-skill-name>/SKILL.md
```

Start each file with valid YAML frontmatter. Include a unique lowercase, hyphenated `name` and a concise `description` that states what the skill does and when to use it:

```yaml
---
name: example-skill
description: Helps with a defined task and explains when to use the skill.
---
```

The `name` should match its folder. Quote YAML values when needed to avoid parsing errors. Keep descriptions specific enough to distinguish skills.

## Recommended content

Cover these topics with clear, domain-specific instructions:

- **Purpose and responsibilities:** what the skill owns and does not own.
- **Technical rules:** version checks, data safety, identifiers, and domain limits.
- **Workflow:** steps from context gathering to implementation or diagnosis.
- **Error handling:** how to investigate failures without hiding errors or losing data.
- **Testing checklist:** static checks and runtime tests relevant to the task.
- **Compatibility:** game/module versions, stable or prerelease status, experiments, and uncertainty.
- **Final response:** what evidence, assumptions, files, and next steps to report.

Sections can be combined when that improves clarity. Cover each topic in substance.

## Keep skill boundaries clear

- `addon-architect`: feature decomposition and BP/RP/script architecture.
- `addon-validator`: pack-wide structure and consistency checks.
- `bedrock-api-expert`: Script API verification and module compatibility.
- `bedrock-ui-expert`: forms and player interaction flows.
- `block-item-expert`: block/item content and related assets/references.
- `dynamic-property-expert`: persistence schema, validation, and migration.
- `entity-expert`: entity definitions and behavior.
- `javascript-debugger`: JavaScript/runtime root-cause analysis.
- `performance-optimizer`: measured runtime performance and resource use.
- `rpg-system-expert`: progression and economy rules.

Cross-cutting requirements, such as checking versions and protecting player data, may appear in several skills. This is intentional. Avoid copying detailed procedures owned by another specialist. Refer to the relevant skill or guide instead.

## Technical accuracy and references

- Never invent API names, signatures, JSON schemas, or runtime behavior.
- Verify version-specific claims in Microsoft Learn or Minecraft Creator documentation.
- Distinguish stable, beta, preview, and experimental status.
- Link authoritative references when they support the guidance. Avoid unrelated link lists.
- Preserve UUIDs, identifiers, and persistent data. Document migration when a change requires it.
- Do not claim that code or gameplay was tested unless the test was run.

## Markdown and repository maintenance

- Use clear headings and concise lists. Label code fences with a language where appropriate.
- Use relative links for repository files and check that each target exists.
- Update the README skill list and structure when adding, renaming, or moving files.
- Keep architecture, API versioning, and troubleshooting documentation consistent with the skills.
- Do not create empty placeholders or delete existing skills as a shortcut.

## Review checklist

- [ ] Frontmatter is valid YAML and includes a unique name and useful description.
- [ ] The name, folder, README entry, and responsibility match.
- [ ] Responsibilities, rules, workflow, error handling, testing, and compatibility are covered.
- [ ] No unsupported APIs or false version guarantees are stated.
- [ ] Instructions do not conflict with other skills or project principles.
- [ ] Useful existing guidance and data-safety rules are preserved.
- [ ] Internal links resolve and Markdown is readable.
- [ ] Validation claims state only what was checked.

Related guides: [architecture](./architecture.md), [API versioning](./bedrock-api-versioning.md), and [troubleshooting](./troubleshooting.md).
