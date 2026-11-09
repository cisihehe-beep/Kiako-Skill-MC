# Skill development guide

This repository uses a focused skill model. Each `SKILL.md` file should be specific, technically grounded, and useful to an AI coding agent in the context of Bedrock add-on work.

## Skill requirements

Every skill file must include:

- valid YAML frontmatter
- unique `name`
- actionable `description`
- responsibilities
- technical rules
- workflow
- error-handling guidance
- testing checklist
- version/compatibility considerations

## YAML frontmatter template

```yaml
---
name: example-skill
description: Short explanation of the skill purpose and when to use it.
---
```

You may add more metadata if needed, but keep the structure simple and predictable.

## Content structure

A strong skill file usually includes these sections:

1. Purpose and scope
2. When to use the skill
3. Core rules
4. Workflow
5. Safety and compatibility rules
6. Error handling and validation
7. Testing checklist
8. Final answer expectations

## Writing standards

- Stay focused on one domain.
- Do not overlap heavily with another skill unless one is a higher-level orchestrator.
- Avoid vague or generic guidance.
- Prefer actionable steps and checklists.
- State version assumptions explicitly.
- Keep player data, identifiers, and UUIDs protected.
- Do not claim tested results without actual verification.

## Review checklist

Before finishing a new skill, check:

- Name is unique and descriptive.
- Description is clear and not redundant.
- File path matches the skill name.
- Markdown headings are consistent.
- Internal references point to existing files.
- The skill does not rely on unsupported APIs.
- The skill contains version-aware guidance.

## Adding a skill

1. Create the new folder under `skills/<skill-name>/`.
2. Add `SKILL.md` with the required frontmatter and content.
3. Update the main `README.md` with the skill description and repository structure.
4. Add or update the relevant documentation if the skill introduces a new major domain.
5. Verify that all links and paths remain correct.

## Keeping the repository maintainable

- Do not create generic placeholder skills.
- Do not duplicate instructions already covered in a more specific skill.
- Do not broaden a skill into a repository-wide architecture framework.
- Keep files concise but complete.

Related docs:
- [Architecture overview](./architecture.md)
- [Bedrock API versioning guide](./bedrock-api-versioning.md)
- [Troubleshooting guide](./troubleshooting.md)
